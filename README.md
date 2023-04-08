# Local Geohistory Project: Open Data

[![DOI](https://zenodo.org/badge/624773291.svg)](https://zenodo.org/badge/latestdoi/624773291)

## Summary

The Local Geohistory Project aims to educate users and disseminate information concerning the geographic history and structure of political subdivisions and local government. This repository contains the data used to populate the [project website](https://www.localgeohistory.pro/en/). The tab-separated values (TSV) files containing the data are available in the **data** folder, and metadata is available in the **metadata** folder.

Currently, the open dataset only contains information related to New Jersey and Pennsylvania, with several scattered events concerning neighboring jurisdictions, mostly that currently border either state.

This repository does not contain the application code, which can be found in the [Application repository](https://github.com/markconnellypro/local-geohistory-project), nor does it contain the table data for the bundled **calendar** extension.

## File format

The TSV files were created using the [PostgreSQL COPY function](https://www.postgresql.org/docs/15/sql-copy.html) in the Text Format. Each file corresponds with a PostgreSQL table in the application.

An extra header line containing column names is included in each file to facilitate use in other applications. When the data is imported using the build process in the [Application repository](https://github.com/markconnellypro/local-geohistory-project), this line is removed automatically; however, manual data imports into PostgreSQL require manual removals of these lines.

## Metadata

A full list of columns in every TSV, along with the associated datatypes, is available in the **metadata** folder.

## Dates

Most dates in the Local Geohistory Project are stored using a custom **calendar.historicdatetext** domain (essentially, the alias of a datatype) in the **calendar** extension bundled with the [Application repository](https://github.com/markconnellypro/local-geohistory-project). This format serializes the date in a text format similar to [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601); however, the goal is to store the date **as closely to how it was presented at the time it was written**, and not using the [Proleptic Gregorian calendar](https://en.wikipedia.org/wiki/Proleptic_Gregorian_calendar).

Because this format may cause difficulties when reusing data in other contexts, the **calendar** extension bundled with the [Application repository](https://github.com/markconnellypro/local-geohistory-project) contains code that allows for conversion of this serialization format to the **calendar.historicdate** datatype, which contains in the **gregorian** subfield the Proleptic Gregorian date.

### Qualifiers

If present, it constitutes the first character. These are generally not used in the Local Geohistory Project; however, a list of possible qualifiers is stored in the **qualifier** table in the **calendar** extension bundled with the [Application repository](https://github.com/markconnellypro/local-geohistory-project).

### Double years

Prior to the adoption of the [Calendar (New Style) Act 1750](https://en.wikipedia.org/wiki/Calendar_(New_Style)_Act_1750) by the British Parliament, it was common practice in the American colonies for dates from January 1 through March 24 to be listed with two years, the first being the legal year under the British calendar, in which the year started on March 25, and the second being the logical year, in which the year started on January 1.

In general, the year recorded in the Local Geohistory Project will be the legal year, not the logical year. If a double year is involved, either of the following characters may be used to indicate the same immediately after the year integer:

| Character | Description |
| --------- | ----------- |
| *         | A contemporaneous source uses a double year. |
| [         | A contemporaneous source does not use a double year; however, the logical year is added with square brackets for clarity when formatted. |

In the rare case that the logical year is used in lieu of the legal year (normally in situations where a more modern source "corrects" the year), a double year character must appear immediately before the year integer:

| Character | Description |
| --------- | ----------- |
| [         | Sources do not use a double year; however, the legal year is added with square brackets for clarity when formatted. |

### Before Common Era

While dates before the Common Area are not currently used in the Local Geohistory Project, the letter **m** will appear immediately prior to the year integer for these dates.

### Month values

For most calendars, the month value matches the month integer in ISO 8601.

In the Quaker calendar, which uses month numbers exclusively, months in dates prior to Julian year 1753 are shifted by 2, so that March is the First Month, and not January.

While not currently used in the Local Geohistory Project, dates in the French Republican and Hebrew calendars do not use integers; rather, they use the codes specified in the FamilySearch GEDCOM 7.0 specification:

https://github.com/FamilySearch/GEDCOM/blob/main/specification/gedcom-06-calendars.md

### Precision

Because historic records contain gaps, exact dates are not always available. Even so, the **calendar.historicdatetext** domain requires that a full year, month, and day be provided for sorting purposes.

Where the exact month and year are known, but the day is not, a tilde is placed between the hyphen and the day integer.

Where the exact year is known, but the month and day are not, tildes are placed after hyphens in two places: before the month value and before the day integer.

While not often used in the Local Geohistory Project, when the entire date is unknown, a tilde is placed immediately after the day integer.

### Calendars

The Local Geohistory Project supports a number of calendars, including Gregorian, Julian, and Quaker. For calendars other than Gregorian with the year beginning on January 1, the calendar abbreviation is placed at the end of the serialization format, and often incorporates additional characters to signify non-standard year start days. A list of possible calendars is stored in the **part** table in the **calendar** extension bundled with the [Application repository](https://github.com/markconnellypro/local-geohistory-project).

## Geometries

The least common geometries method,[^1] where polygon geometries are split into the smallest geographic areas that share common attributes over time, is used by the Local Geohistory Project to efficiently store GIS data. These least common geometries are stored in the **governmentshape** table, and the geometry data column, **governmentshapegeometry**, is stored in the Extended Well-Known Binary (EWKB) format.

### Using QGIS to view data

[QGIS](https://www.qgis.org/) supports reading this data directly from the TSV via a **Virtual Layer**. Navigate to **Layer**, then **Add/Edit Virtual Layer**. This will open up a dialog to add a Virtual Layer. Press **Add** under **Embedded layers** and set the following values (replacing **FOLDER** with the folder in which the file is located):

**Local name:** governmentshape

**Source:** **FOLDER**/governmentshape.tsv|layername=governmentshape

Populate the following fields:

**Query:**

```SQL
SELECT GeomFromEWKB(governmentshapegeometry) as governmentshapegeometryshape,
   *
FROM governmentshape
```

**Unique identifier column:** governmentshapeid

Then, press **Add**, then **Close**, and the least common geometries should appear on the screen. Additional TSVs may be added as Delimited Text layers for creating Joins.

For further information, see:

https://gis.stackexchange.com/questions/69500/importing-points-in-wkb-format-to-qgis

[^1]: Martina De Moor and Torsten Wiedemann, "Reconstructing Territorial Units and Hierarchies: A Belgian Example," *History and Computing* 13, no. 1 (March 2001): 71-98, https://doi.org/10.3366/hac.2001.13.1.71.