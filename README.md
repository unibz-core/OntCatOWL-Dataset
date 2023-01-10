# OntCatOWL-Dataset

Dataset with results of OntCatOWL tests performed on the OntoUML/UFO Catalog.

# Description

The OntCatOWL-Dataset is composed of files with results of [OntCatOWL](https://github.com/unibz-core/OntCatOWL) tests performed via the [OntCatOWL-Tester](https://github.com/unibz-core/OntCatOWL-Tester) on the [OntoUML/UFO Catalog](https://github.com/unibz-core/OntCatOWL).

The FAIR Model Catalog for Ontology-Driven Conceptual Modeling Research, short-named OntoUML/UFO Catalog, is a structured and open-source catalog that contains OntoUML and UFO ontology models. The catalog was conceived to allow collaborative work and to be easily accessible to all its users. Its goal is to support empirical research in OntoUML and UFO, as well as for the general conceptual modeling area, by providing high-quality curated, structured, and machine-processable data on why, where, and how different modeling approaches are used. The catalog offers a diverse collection of conceptual models, created by modelers with varying modeling skills, for a range of domains, and for different purposes.

The tests were performed using the automation tool named [OntCatOWL-Tester](https://github.com/unibz-core/OntCatOWL-Tester), which runs over OntCatOWL. OntCatOWL is the abbreviated name for Identification of Ontological Categories for OWL Ontologies, a software that aims to support the semi-automatic semantic improvement of lightweight web ontologies. We aim to reach the referred semantic improvement via the association of [gUFO](https://nemo-ufes.github.io/gufo/)—a lightweight implementation of the [Unified Foundational Ontology (UFO)](https://nemo.inf.ufes.br/wp-content/uploads/ufo_unified_foundational_ontology_2021.pdf)—concepts to the OWL entities. The aim of gUFO is "_to provide a lightweight implementation of the Unified Foundational Ontology (UFO) suitable for Semantic Web OWL 2 DL applications_".

This document presents the structure of the files generated during the OntCatOWL-Tester execution. For a complete comprehension of the tests (regarding scope, objectives, implementation, etc.), please refer to the OntCatOWL-Tester [description file](https://github.com/unibz-core/OntCatOWL-Tester#readme).

The aim of the publication of the resulting datasets is to share with the community data that can be analyzed in different ways, even though all executed tests are totally reproducible.

# Contents

- [Nomenclature of Files and Folders](#nomenclature-of-files-and-folders)
- [Build Generated Files](#build-generated-files)
  - [Taxonomical Graph _ttl_ File](#taxonomical-graph-ttl-file)
  - [Taxonomical Graph Information _csv_ File](#taxonomical-graph-information-csv-file)
  - [Hashes Register _CSV_ File](#hashes-register-csv-file)
- [Tests – Generated Files and their Descriptions](#tests--generated-files-and-their-descriptions)
- [Contributors](#contributors)
- [Acknowledgements](#acknowledgements)

# Nomenclature of Files and Folders

For avoiding long names for files and directories, all content available in the datasets in this repository follows the nomenclature here presented:

1. Numbers with up to three digits are always presented with three digits (e.g., 001). Numbers higher than three digits must be presented without additional digits
2. All numbers must be attached directly to its corresponding item (e.g., test, execution, etc.)
3. The following words must be changed for the corresponding simplifications:
   - test: tt
   - taxonomy: tx
   - execution: ex
   - percentage: pc
4. The OntCatOWL parameters must be represented using the following simplifications:
   - automatic: a
   - interactive: i
   - complete: c
   - incomplete: n
5. The automation parameter (a or i) must come first, and the completion parameter must follow it (c or n)
6. The parameters must be displayed integrated (e.g., ac, in, etc.)
7. Files names must be without spaces, which must be substituted by hyphens
8. Separation between different items in the file name must be done using underlines
9. The following item order must be used whenever possible: file name, dataset name, test name/number, test parameters, taxonomy number, execution number, percentage number

# Build Generated Files

The OntCatOWL-Tester creates a directory for each one of the catalog's datasets that are tested. Each directory contains other folders with the results of the tests that were performed, but they also contain two different files generated by the OntCatOWL-Tester to be used as input for the tests. For generating these files, the Tester decomposes the original taxonomy from a dataset in its (possibly multiple) independent taxonomies (isolated group of classes related via specialization/generalization relations between each other). Both files are presented in this document, as well as a hashes register file.

## Taxonomical Graph _ttl_ File

Each `XXX_txYYY.ttl` file (with XXX being the dataset name and YYY ranging from 001 to the number of independent taxonomies available in the dataset's OntoUML model) contains an isolated taxonomical graph in OWL (in turtle syntax) got from the OWL taxonomy provided in the catalog's dataset to be tested. An example of a generated taxonomy file is: _aguiar2018rdbs-o\_tx001.ttl_.

For instance, a single model that has two not connected hierarchical structures of concepts will generate two files, each one containing only the following properties: `rdfs:subClassOf`, `owl:Class`, and `rdf:type`.

For generating the concept's URIs, the OntCatOWL-Tester uses the following namespace for all taxonomies generated for all datasets: _http://taxonomy.model/_

## Taxonomical Graph Information _csv_ File

Each `data_XXX_txYYY.csv` file (with XXX being the dataset name and with YYY ranging from 01 to the number of independent taxonomies available in the dataset's OntoUML model) contains information about all the classes that are part of the taxonomical graph with the corresponding number (i.e., the file _data\_aguiar2018rdbs-o\_tx001.csv_ refers to the taxonomy saved in the file _aguiar2018rdbs-o\_tx001.ttl_). The difference between the results of a test and the inputted data should use this file, as it contains the source data.

The generated _csv_ file contains the following columns:

- `class_name`: name of the OntoUML class as it is in the original model (i.e., without namespace)
- `ontouml_stereotype`: the class's OntoUML stereotype as was attributed by its modeler
- `gufo_classification`: the class's OntoUML stereotype mapped to a gUFO endurant type **(click here for more information—link to be created)**
- `is_root`: Boolean value that shows if the class is a root node in the taxonomical graph (i.e., if it has no superclasses)
- `is_leaf`: Boolean value that shows if the class is a leaf node in the taxonomical graph (i.e., if it has no subclasses)
- `is_intermediate`: Boolean value that shows if the class is an intermediate node in the taxonomical graph (i.e., if it has subclasses and superclasses)
- `number_superclasses`: the sum of the number of all direct and indirect superclasses that the class have
- `number_subclasses`: the sum of the number of all direct and indirect subclasses that the class have

As every class must be a root, a leaf, or an intermediate node, note that this file would be inconsistent if:

- is\_root OR is\_leaf OR is\_intermediate != True, or if
- is\_root AND is\_leaf AND is\_intermediate != False

## Hashes Register _CSV_ File

For traceability, the OntCatOWL-Tester provides a function for generating a SHA256 hash of its generated files and of the files that originated them (for more information, click here–link to be created). The whole dataset contains a single _csv_ register file named `hash_sha256_register.csv`, containing four columns of data that are incremented every time the Tester creates new files. The columns are:

- `file_name`: complete path of the file being hashed
- `file_hash`: SHA256 hash of the file
- `source_file_name`: file used as a source for the generation of the file being hashed
- `source_file_hash`: SHA256 hash of the source file

We could cite as an example of use of this file the case where a user would like to know if he is using the same source data for generating his results, so he can get the SHA256 hash of the files she/he is using check if it exists in the hashes register file.

# Tests – Generated Files and their Descriptions

Currently, datasets generated from the execution of two tests are available. Please use the following links for accessing the tests descriptions and results.

- [**Test 1:** single class used as input](https://github.com/unibz-core/OntCatOWL-Dataset/blob/main/documentation/OntCatOWL-Dataset-Test1.md)
- [**Test 2:** increasing percentage of classes used as input](https://github.com/unibz-core/OntCatOWL-Dataset/blob/main/documentation/OntCatOWL-Dataset-Test2.md)

# Contributors

- PhD. Pedro Paulo Favato Barcelos [[GitHub](https://github.com/pedropaulofb)] [[LinkedIn](https://www.linkedin.com/in/pedropaulofavatobarcelos/)]
- PhD. Tiago Prince Sales [[GitHub](https://github.com/tgoprince)] [[LinkedIn](https://www.linkedin.com/in/tiagosales/)]
- MSc. Elena Romanenko [[GitHub](https://github.com/mozzherina)] [[LinkedIn](https://www.linkedin.com/in/mozzherina/)]
- Prof. PhD. Giancarlo Guizzardi [[LinkedIn](https://www.linkedin.com/in/giancarloguizzardibb51aa75/)]
- MSc. Gal Engelberg [[GitHub](https://github.com/GalEngelberg)] [[LinkedIn](https://www.linkedin.com/in/galengelberg/)]
- MBA Dan Klein [[GitHub](https://github.com/danklein10)] [[LinkedIn](https://www.linkedin.com/in/~danklein/)]

# Acknowledgements

This work is a collaboration between the Free University of Bozen-Bolzano, the University of Twente, and Accenture Israel Cybersecurity Labs.
