# `chirotraits.build` <img src="inst/chirotraits.png" align="right" width="138"/>

Source repository to build the `ChiroTraits` database.

## Overview

This repository compiles the code and data used to build the `ChiroTraits` database. This database is part of the first chapter of the PhD thesis "*Assessment of knowledge gaps in bats: A macroecological perspective*" which is being carried out by [Roberto Antonio Ruiz-Ramírez](https://maevolab.mx/authors/roberto/) at the [Evolutionary Macroecology Lab](https://maevolab.mx/).

This database is a work in progress maintained by Roberto A. Ruiz-Ramírez. If you have any questions or inquiries regarding the use of this document, please write to: [roberto.ruiz\@posgrado.ecologia.edu.mx](mailto:roberto.ruiz@posgrado.ecologia.edu.mx).

A detailed report of the data, methodology, and references used for the trait selection and literature review process can be found in the following [Quarto document](https://robertoruizr.github.io/GBTD_litrev_traitcat_cleaning/).


# The `ChiroTraits` database

Functional traits (FT) – well-defined, measurable, morphophysiological and ecological characteristics that influence the fitness of individuals – have been used to model numerous ecological processes, as well as responses to environmental changes in diverse organisms and biological communities (Funk et al., 2017; Zakharova et al., 2019; Etard et al., 2020; Dawson et al., 2021). The focus on functional traits has driven a multidisciplinary effort to create and update comprehensive databases in numerous taxa  (e.g. plants, Kattge et al., 2020; fishes, Brosse et al., 2021; mammals, Soria et al., 2021; birds, Tobias et al., 2022; and amphibians, Huang et al., 2023). However, despite their importance, to date there is no comprehensive dataset of functional traits for the order Chiroptera at a global level.

`ChiroTraits` aims to be a comprehensive database of functional traits for the order Chiroptera. Additionally, the workflow used allows for the constant update of the dataset in response to taxonomic updates, future addition of functional traits, and continuous data integration from interested parties.

Currently, `ChiroTraits` includes 65238 records for 1293 bat species and 29 functional traits.

The creation of `Chirotraits` was greatly pushed forward thanks to two recent releases: the traits.build R package (Wenk et al., 2024) and the [Mammal Diversity Database 2.1 (2025)](https://www.mammaldiversity.org/).

The name `ChiroTraits` follows from the naming convention used by Falster et al., 2021 in their `AusTraits` database. Likewise, the name `chirotraits.build` follows the `austraits.build` and `traits.build` naming convention used by Wenk et al., 2024.


## File organization

### /config folder

`ChiroTraits` is built using the following files, which can be found in the **/config** folder:

-   *metadata.yml*: Contains the database description, authors, and affiliations.
-   *traits.yml*: Contains the definitions of the traits included in the database.
-   *taxon_list.csv*: Contains the taxon names to be included in the database.
    -   Obtained from the [Mammal Diversity Database 2.1](https://www.mammaldiversity.org/)
-   *unit_conversions.csv*: Contains common unit conversion formulas.

### /data folder

The /data folder contains the individual publications included in this database. Each publication is in a folder named **FirstAuthor_YearofPublication**, and in each of those the following files are included:

-   *data.csv*: A csv file with the trait data from the publication.
-   *metadata.yml*: Metadata from the individual study. Includes publishing information, names and description of the included traits, as well as methods and context from the study.

## Structure

Once built, the `ChiroTraits` database is a list of related tables, each one contains a different dimension of the data.

A detailed description of the following components, as established in the traits.build R package (Wenk et al., 2024), can be found [here](https://traitecoevo.github.io/traits.build-book/database_structure.html).

### traits

Table with all the trait data integrated in `ChiroTraits`, each data point has the study of origin, units, context, and locations from the original source. Additionally, the type of measurement (e.g. mean, raw data, or median) as well as the entity context of the organism (e.g sex, lifestage, or number of individuals of which a data point comes from) are also documented.

### excluded_data

Table with data points which were excluded during the build process. The reason for the exclusion is documented for each row.

Data was excluded from integration into `ChiroTraits` if: 
- The data value falls out of the allowed value range specified for the trait (e.g. a tail length of 0 mm). 
- Data which could not be mapped into a species (e.g. record is specified at genus level). 
- The data corresponds to an extinct bat species. In which case, a link to the corresponding entry in the [REPAD: The Recently Extinct Plants and Animals Database](https://recentlyextinctspecies.com/chiroptera) was added. 
- The data record was imputed by statistical methods (e.g. gap-filling).

### taxonomic_updates

When the species listed in the trait data was out of alignment with the taxonomy used, a taxonomic update was specified in the corresponding `metadata.yml` file of the study. This table contains the list of updated scientific names assigned in the study, the new accepted taxon, the study which lists the outdated name, and the reason given for the update.

Each taxonomic update is written in the `metadata.yml` file for each study with the following structure: 
- *Find*: The species name reported in the source. 
- *Replace*: The current accepted species name, as established in the MDD. 
- *Reason*: The reason listed for the change in the correponding page for the species. Also includes the current webpage for the species listed in the MDD website.

*Add table with taxonomic updates in ChiroTraits*


### taxa

Table with the list of bat species currently recognized. The taxonomy used was obtained from the most recent version of [The Mammal Diversity Database (MDD)](https://www.mammaldiversity.org/), which recognises 1492 species, 238 genera, and 21 families of bats. 

### definitions
Every functional trait included in `ChiroTraits` has a corresponding definition in the `config/traits.yml` file, which acts as a thesaurus for the complete database. Each trait includes their assigned name, definition, allowed values (numerical variables) or levels (categorical variables), expected unit, and a link to an existing Ontology found in the [Ontobee Data Server](https://ontobee.org/). When a trait definition was not found in the existing ontologies, the definition was obtained from a published trait dataset for bats (e.g. EuroBaTrait, Froidevaux et al., 2023; AfroBat, Cosentino et al., 2023) and the corresponding DOI was added as a source.

### Other tables included in the structure of `ChiroTraits`

Descriptions obtained directly from Wenk et al., 2024.

- *locations*: A table containing observations of location/site characteristics associated with information in `traits`.
- *contexts*: A table containing observations of contextual characteristics associated with information in `traits`. 
- *methods*: A table containing details on methods with which data were collected, including time frame and source.
- *contributors*: A table of people contributing to each study. Obtained from the `metadata.yml` file from each study included.
- *identifiers*: A table of identifiers that cross-references observations between datasets or with other data resources such as
museum specimens.
- *sources*: Bibtex entries for all primary and secondary sources in the compilation.
- *schema*: A copy of the schema for all tables and terms. Information included here was used to process data and generate any
documentation for the study.
- *metadata*: Metadata associated with the dataset, including title, creators, license, subject, funding sources.
- *build_info*: A description of the computing environment used to create this version of the dataset, including version number, git
commit and R session_info.



## References

- Brosse, S., Charpin, N., Su, G., Toussaint, A., Herrera-R, G. A., Tedesco, P. A., & Villéger, S. (2021). FISHMORPH: A global database on morphological traits of freshwater fishes. Global Ecology and Biogeography, 30(12), 2330–2336. https://doi.org/10.1111/geb.13395
-   Cosentino, F., Castiello, G., & Maiorano, L. (2023). A dataset on African bats’ functional traits. Scientific Data, 10(1), 623. https://doi.org/10.1038/s41597-023-02472-w
- Dawson, S. K., Carmona, C. P., González-Suárez, M., Jönsson, M., Chichorro, F., Mallen-Cooper, M., Melero, Y., Moor, H., Simaika, J. P., & Duthie, A. B. (2021). The traits of “trait ecologists”: An analysis of the use of trait and functional trait terminology. Ecology and Evolution, 11(23), 16434–16445. https://doi.org/10.1002/ece3.8321
- Etard, A., Morrill, S., & Newbold, T. (2020). Global gaps in trait data for terrestrial vertebrates. Global Ecology and Biogeography, 29(12), 2143–2158. https://doi.org/10.1111/geb.13184
- Falster, D., Gallagher, R., Wenk, E. H., Wright, I. J., Indiarto, D., Andrew, S. C., Baxter, C., Lawson, J., Allen, S., Fuchs, A., Monro, A., Kar, F., Adams, M. A., Ahrens, C. W., Alfonzetti, M., Angevin, T., Apgaua, D. M. G., Arndt, S., Atkin, O. K., … Ziemińska, K. (2021). AusTraits, a curated plant trait database for the Australian flora. Scientific Data, 8(1), 254. https://doi.org/10.1038/s41597-021-01006-6
-   Froidevaux, J. S. P., Toshkova, N., Barbaro, L., Benítez-López, A., Kerbiriou, C., Le Viol, I., Pacifici, M., Santini, L., Stawski, C., Russo, D., Dekker, J., Alberdi, A., Amorim, F., Ancillotto, L., Barré, K., Bas, Y., Cantú-Salazar, L., Dechmann, D. K. N., Devaux, T., … Razgour, O. (2023). A species-level trait dataset of bats in Europe and beyond. Scientific Data, 10(1), 253. https://doi.org/10.1038/s41597-023-02157-4\
- Funk, J. L., Larson, J. E., Ames, G. M., Butterfield, B. J., Cavender-Bares, J., Firn, J., Laughlin, D. C., Sutton-Grier, A. E., Williams, L., & Wright, J. (2017). Revisiting the Holy Grail: Using plant functional traits to understand ecological processes. Biological Reviews, 92(2), 1156–1173. https://doi.org/10.1111/brv.12275
- Huang, N., Sun, X., Song, Y., Yuan, Z., & Zhou, W. (2023). Amphibian traits database: A global database on morphological traits of amphibians. Global Ecology and Biogeography, 32(5), 633–641. https://doi.org/10.1111/geb.13656
- Kattge, J., Bönisch, G., Díaz, S., Lavorel, S., Prentice, I. C., Leadley, P., Tautenhahn, S., Werner, G. D. A., Aakala, T., Abedi, M., Acosta, A. T. R., Adamidis, G. C., Adamson, K., Aiba, M., Albert, C. H., Alcántara, J. M., Alcázar C, C., Aleixo, I., Ali, H., … Wirth, C. (2020). TRY plant trait database – enhanced coverage and open access. Global Change Biology, 26(1), 119–188. https://doi.org/10.1111/gcb.14904
-  Mammal Diversity Database. (2025). Mammal Diversity Database (Version 2.0) \[Data set\]. Zenodo. https://doi.org/10.5281/zenodo.15007505
- Soria, C. D., Pacifici, M., Di Marco, M., Stephen, S. M., & Rondinini, C. (2021). COMBINE: a coalesced mammal database of intrinsic and extrinsic traits. Ecology, 102(6). https://doi.org/10.1002/ecy.3344
- Tobias, J. A. (2022). A bird in the hand: Global-scale morphological trait datasets open new frontiers of ecology, evolution and ecosystem science. Ecology Letters, 25(3), 573–580. https://doi.org/10.1111/ele.13960
-   Wenk, E., Bal, P., Coleman, D., Gallagher, R., Yang, S., & Falster, D. (2024). Traits.build: A data model, workflow and R package for building harmonised ecological trait databases. Ecological Informatics, 83, 102773. https://doi.org/10.1016/j.ecoinf.2024.102773
- Zakharova, L., Meyer, K. M., & Seifan, M. (2019). Trait-based modelling in ecology: A review of two decades of research. Ecological Modelling, 407, 108703. https://doi.org/10.1016/j.ecolmodel.2019.05.008


## License

The contents of this repository are made available under the Open Data Commons Attribution License (ODC-By): http://opendatacommons.org/licenses/by/1.0/