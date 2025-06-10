# chirotraits.build <img src="inst/chirotraits.png" align="right" height="138"/>

Repository to build the ChiroTraits database.

## Overview

This repository compiles the code and data used to build the ChiroTraits database, a Global Bat Trait Database. This database is part of the first chapter of the PhD thesis "*Assessment of knowledge gaps in bats: A macroecological perspective*" which is being carried out by [Roberto Antonio Ruiz-Ramírez](https://maevolab.mx/authors/roberto/) at the [Evolutionary Macroecology Lab](https://maevolab.mx/).

This repository is a work in progress maintained by Roberto A. Ruiz-Ramírez. If you have any questions or inquiries regarding the use of this document, please write to: [roberto.ruiz\@posgrado.ecologia.edu.mx](mailto:roberto.ruiz@posgrado.ecologia.edu.mx)

A detailed report of the data, methodology, and references used can be found in the following [Quarto document](https://robertoruizr.github.io/GBTD_litrev_traitcat_cleaning/).

## File organization

### /config folder

The database is built around the following files, which can be found in the configuration files (**config**) folder:

-   *metadata.yml*: Contains the database description, authors, and affiliations.
-   *traits.yml*: Contains the definitions of the traits included in the database.
-   *taxon_list.csv*: Contains the taxon names to be included in the database.
    -   Obtained from the [Mammal Diversity Database 2.1](https://www.mammaldiversity.org/)
-   *unit_conversions.csv*: Contains common unit conversion formulas.

### /data folder

The /data folder contains the individual publications included in this database. Each publication is in a folder named **FirstAuthor_YearofPublication**, and in each of those the following files are included.

-   *data.csv*: A csv file with the trait data from the publication.
-   *metadata.yml*: Metadata from the individual study. Includes publishing information, names and description of the included traits, as well as methods and context from the study.

## License

The contents of this repository are made available under the Open Data Commons Attribution License (ODC-By): http://opendatacommons.org/licenses/by/1.0/