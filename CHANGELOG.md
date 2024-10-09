# Changelog

## [2.1.0] - 2024-10-09

### Added

- In extract file documentation.tsv, disclaimer text (formerly in Application repository).
- In extract file plsstownship.tsv, plsstownshipname column.
- In extract files governmentidentifier.tsv and governmentidentifiertype.tsv, tax district identifiers for the following Pennsylvania counties: Clinton, Lebanon, McKean, Northumberland, Potter, and Venango.

### Changed

- Minor data quality improvements in New Jersey and Pennsylvania.
- Standardized eventrelationship values related to placeholder events for alternate government name spellings.

### Fixed

- Field names and datatypes that had been incorrectly interpolated from fields with masked data or that were incorrectly aliased.

### Removed

- In extract file eventtype.tsv and related extracts, Municipal Manager Form event type (substituted with Council-Manager Form).

## [2.0.0] - 2024-05-04

### Added

- Estimated years for key government sources (charter commission reports, elections, ordinances) related to New Jersey Optional Municipal Charter Law (Faulkner Act) proceedings based on New Jersey County and Municipal Government Study Commission reports.
- Extract file locale.tsv.
- Remaining legal descriptions for unabstracted New Jersey laws to extract files metesdescription.tsv and metesdescriptionline.tsv.

### Changed

- Extract file event.tsv to change data type for eventgranted column and replace data with foreign key reference.
- Extract file governmentidentifiertype.tsv to replace column governmentidentifiertypeprefixlength with governmentidentifiertypeprefixlengthfrom and governmentidentifiertypeprefixlengthto, and to replace column governmentidentifiertypelength with governmentidentifiertypelengthfrom and governmentidentifiertypelengthto.
- Extract file lawgroup.tsv to remove columns eventtype and lawgroupgovernmenttype and replace with new extract files lawgroupeventtype.tsv and lawgroupgovernmenttype.tsv.
- Extract file plss.tsv to change data type for plssfirstdivisionpart column.
- Extract file source.tsv to remove sourcegovernment column and replace with new extract file sourcegovernment.tsv.
- Extract file sourcecitation.tsv to remove sourcecitationdetail column and replace with new extract files sourcecitationnote.tsv and sourcecitationnotetype.tsv.
- Extract files adjudicationevent.tsv, governmentsourceevent.tsv, lawgroupsection.tsv, lawsectionevent.tsv, and recordingevent.tsv to replace columns adjudicationeventrelationship, governmentsourceeventrelationship, lawsectionrelationship, lawsectioneventrelationship, and recordingeventrelationship, respectively, with eventrelationship column with foreign key reference.
- Other minor data quality improvements in New Jersey and Pennsylvania.

### Removed

- In extract file researchlog.tsv, internetarchivehandle column.
- In extract file sourcecitation.tsv, sourcecitationnotes column.
- References to Panama Canal Zone.

## [1.2.1] - 2023-11-12

### Changed

- Repository paths to accommodate moving repository to organization.

### Fixed

- Governmentidentifier data to reflect that tax district 48 of Cumberland County, Pennsylvania is located in the Township of Lower Allen instead of the Borough of Shiremanstown.

## [1.2.0] - 2023-10-01

### Added

- Line ending description in README.

### Changed

- Minor data quality improvements in New Jersey and Pennsylvania.

## [1.1.0] - 2023-07-01

### Added

- Changelog.
- Columns lawgroup in lawsectionevent.tsv and event in researchlog.tsv.
- Extract files lawgroup.tsv and lawgroupsection.tsv.
- TSV delimiter explanation in README.
- Zenodo DOI badge to README.
- Zenodo metadata file.

### Changed

- Columns in government.tsv to remove governmentclass and governmentcurrenthomerule and substitute with governmentcurrentform.
- Data quality improvements in New Jersey from more detailed abstracting of County Clerk and Secretary of State Statutory Filing records.
- Event data for Towamencin Township 2023 Home Rule, which was approved by the electorate and took effect since prior release.
- Event method descriptor for Court to Judicial.
- Stylistic and minor changes to README.

### Fixed

- Linting errors in README.
- Missing metesdescriptionacres values in metesdescription.tsv.

### Removed

- Obsolete handles in researchlog.tsv.
- Partial or full omission from open data from lawdescriptiondone column in law.tsv, and recordingrepositoryitemfrom and recordingrepositoryitemto columns in recording.tsv.
- Placeholder affected government part references.

## [1.0.0] - 2023-04-07

### Added

- Public release of the Local Geohistory Project: Open Data repository.

[2.1.0]: https://github.com/localgeohistoryproject/open-data/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/localgeohistoryproject/open-data/compare/v1.2.1...v2.0.0
[1.2.1]: https://github.com/localgeohistoryproject/open-data/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/localgeohistoryproject/open-data/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/localgeohistoryproject/open-data/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/localgeohistoryproject/open-data/releases/tag/v1.0.0
