# BioDATEN Minimalschema 1.0 – Documentation

# Motivation

Research data are the output of research as well as a possible input for research, but only if its creators share it with other researchers attributed with a re-use friendly licence, and annotated with useful metadata. Sharing, storing, and annotating research data is part of the overall topic called research data management (RDM). The challenge is to help and motivate researchers to annotate their data with appropriate metadata and to foster free and open exchange of research data. While promoting open data is not only considered good scientific practice, it is also expected by funding agencies as a requirement in project proposals. Metadata, including descriptive data about authorship as well as scientific metadata about research workflows etc., are essential for the creation of [FAIR data](https://doi.org/10.1038/sdata.2016.18). The challenge is to provide researchers with a schema that neither too generic nor too specific. A too generic schema lacks the possibility to capture necessary data while a too specific schema overburdens the researcher with irrelevant information. The [Science Data Center BioInformatics DATa ENvironment (SDC BioDATEN)](https://portal.biodaten.info/) created a schema that aims at providing the right granularity by reducing complexity while maximizing scientific benefit. The following text provides more details about the BioDATEN minimal schema and provides an overview about the technical details and implementation.


# Introduction

The BioDATEN minimal metadata schema is a set of elements to describe bioinformatic research datasets. The schema was developed as part of the BioDATEN project and aims at providing researchers the possibility to describe their datasets with domain specific terms to enable findability, accessibility, interoperability and reusability as defined by the FAIR principles. As the BioDATEN project has a very heterogeneous community, the schema tries to be generic enough to be of use to different scientific fields as well as fullfilling different domain specific requirements.


The schema is XML based and constructed with the help of the [CLARIN Component Registry (CCR)](https://catalog.clarin.eu/ds/ComponentRegistry/#/browser). It consists of the main components _Studied Object, Method, Run and File. When the XSD is exported from the CCR, we manually remove occurrences of_

- xml:base

- cmd:ref attributes.



Note that components have an attribute cmd:ComponentId which is a value that is always fixed to a component's identifier. This is needed for the validation of the schema. It should not be offered to users filling out the schema.


_The schema was designed to be used in_ _[conjunction with other metadata schemas](https://portal.biodaten.info/content/?id=131)_(BioDATEN login required) _such as the_ [DataCite](https://schema.datacite.org/) _schema or_ [PREMIS](http://www.loc.gov/standards/premis/) _to achieve a detailed enough description of a dataset to enable other researchers than the originator to work with it._

The current way of describing a dataset with the BioDATEN minimal schema is by using the BioDATEN metadata annotation tool.

# Design principles
- Conditional mandatory fields: Some of the metadata fields are only meant to be filled out, if another field was filled out in a specific way (e.g. „typeOfMethod“:“Sequencing method“ is the condition for the field „sequencingMethod“ to become relevant). These fields are modelled with a minimal occurence of „0“ in the xsd. If a field that triggers a condition has been filled out, filling out the dependent field becomes mandatory. The dependency on another field is expressed as an "cue:dependsOn_valueSelection" attribute.
- Automatically generated identifiers: For each instance of each component of the schema an automated identifier is created. This is true for each element with the attribute „cue:dependsOn_autogeneration="true". These identifiers are used to link different components together (e.g. Studied Objects and Methods in a Run, Files linked to a Run, etc.)

# Schema components
All attributes in the components “Studied Object” and “Method” are mandatory unless they are explicitly labelled as optional. The use of the suggested ontologies is strongly recommended, but not mandatory, as they may not apply in some cases.


INSERT IMAGE 230130_BioDATEN_metadata_schema_components_1.jpg


# Studied Object component
The Studied Object component describes the material entity from which the data was derived. It will be linked to the method used on it, (Method component) yielding an experimental run (Run component). After the description of the studied object as free text, it must be decided whether it is an organism or a non-organism ("type of the studied object/sample"). In case of organism, the “name of the organism of the studied object/sample” is to be provided, based on a suggested ontology. In the same vein, the “name of the cell type used in the sample” is to be provided, based on two suggested ontologies. If “Non-Organism” was chosen as “type of the studied object/sample” the two aforementioned elements are not relevant. “Additional information” on the type of the Studied Object may be provided optionally as free text. The “name of the material (structure, substance, device) removed from a source (patient, donor, physical location, product) OR a material entity that has the specimen role” has to be provided based on a suggested ontology. Finally, information on the “measurement target (e.g., protein, gene, compound)” is required as free text.

# Method component

The Method component describes the measurement conditions under which the experiments, that yielded the research data of a described dataset, were performed. After the description of the method as free text, it must be specified how the sample was prepared or processed, based on a suggested ontology. The selection of the “class of method used” implies the selectable options of the “name of method used”. If “Other” was chosen for “class of method used”, the field “name of method used” becomes irrelevant. If “Other” was chosen for “name of method used”, the field “description of method” will appear, prompting the user to describe the used method as free text. Finally, the user gets the optional opportunity to name a “link to scientific paper where method has been described”, preferably through a persistent identifier, such as a DOI.

# Run component
The Run component links together instances of the Studied Object and the Method component. It consists of two elements that each stores the identifier of one Studied Object and one Method, which are part of the same dataset metadata description.

INSERT IMAGE 230130_BioDATEN_metadata_schema_components_2.jpg

# File component

The File component describes the files that are part of a dataset. Each file gets its own autogenerated identifier and repeatable fields, which store references to Run or other File instances, that the specific File instance was created out of.
