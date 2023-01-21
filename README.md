# ELGA-CDA FHIR Mapping Project

This project provides maps for transforming ELGA-CDA Microbiology Laboratory Reports to FHIR. The manual provides useful information about the requirements and the execution of the maps as well as instructions for creating your own maps.

## Getting Started

To be able to execute ELGA-CDA FHIR transformations two things are needed: A FHIR Server with FHIR Mapping Language capabilities and a REST Client. I personally use Visual Studio Code as there are a number of convenient, FHIR Mapping Language-related extensions available and it seems to be kind of an "industry standard".

### Prerequisites

#### A FHIR Server with FHIR Mapping Language capabilities:

* Matchbox (https://github.com/ahdis/matchbox), populated with the FHIR Logical Model for CDA (https://github.com/HL7/cda-core-2.0).


#### Visual Studio Code with the following extensions: 

* FHIR Mapping Language (Healex Systems) for syntax highlighting

* REST Client (Huachao Mao) for REST interactions with FHIR Servers


### Executing maps

A step by step series of examples that tell you how to execute the FHIR Maps. All necessary REST-Requests are included in the .http file (CDASample2FHIRSample.http for matchbox) which will be used for the execution of the transformation. Please adapt the http file according to your transformation needs, as there are slight implementation and execution differences depending on which transformation server is used.

Before executing the contained REST-Requests please make sure the @host-Variable is set to the correct/valid Server URL. In the case that no local server instance is avaliable, a public API endpoint is available for each server which can be used for executing transformations as well. (Matchbox: @host = https://test.ahdis.ch/matchboxv3/fhir)

#### Step 1 - Prepopulating the server with the required FHIR Resources

* Matchbox: Please execute REST-Requests Number 1 and 1b. As Matchbox supports embedded concept maps only, the other requests are only necessary for the completist mapping approach, which is not implemented completely.

#### Step 2 - Executing the transformation

* Matchbox: Please execute REST-Request Number 2b. It asks the server to transform the attached ELGA-CDA Document via the specified structure map into a FHIR Bundle resource.

In any case, final result is not stored on the server, so keep in mind to save it if you want to keep it. I normally save it manually into the FHIRDiagnosticReport.json file inside the output directory.

#### Step 3 - Validating the result

If the result should be validated against the FHIR R4 Specification there are two possibilities:

* The first one would be the $validate-Operation of a FHIR server (https://www.hl7.org/fhir/r4/resource-operation-validate.html). Unfortunately, that operation is not supported by some servers, so make sure to check if your used FHIR server supports the operations and is prepopulated with the adequate StructureDefinition resources.

* The second option however would be the console-based official FHIR Validation Jar (https://confluence.hl7.org/display/FHIR/Using+the+FHIR+Validator).

<!--## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.-->

## Authors

* **Maximilian Ossana** - *ELGA-CDA Maps and Mapping of ELGA-CDA Microbiology Laboratory Report*


<!-- See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project. -->

## License

This project is licensed under the Creative Commons CC0 License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

<!--* Hat tip to anyone whose code was used
* Inspiration
* etc -->

* **Oliver Egger** - *Initial work and support with matchbox-related questions and issues* - [CDAFHIRMaps](https://github.com/hl7ch/cda-fhir-maps)
* **Stefan Sabutsch** - *Support with ELGA-CDA specific questions and issues*
