# hl7-fhir-udap-test-client-ui

## Overview

This nodejs/express/handlebars user interface project represents a user interface/test harness for a full UDAP Client implementation.   The user interface is part of a 4 repository collection for a full [UDAP](https://www.udap.org/) implementation.   

The implementation adheres to the published version 1.0 of the [HL7 UDAP Security Implementation Guide](https://hl7.org/fhir/us/udap-security).

The client side components of the following features of the IG are supported:
- [UDAP trusted dynamic client registration](https://hl7.org/fhir/us/udap-security/registration.html)
- [B2B Authorization](https://hl7.org/fhir/us/udap-security/b2b.html)
- [B2C Authorization](https://hl7.org/fhir/us/udap-security/consumer.html)
- [Tiered OAuth](https://hl7.org/fhir/us/udap-security/user.html)

The user interface supports the UDAP version of OAuth2 Client Credentials Flow and Authorization Code Flow.  Through out the user interface (and code base) they are referred to as B2B (Client Credentials Flow) and B2C (Authorization Code Flow).

Links to the other repositories in the collection:
- [hl7-fhir-udap-common](https://github.com/Evernorth/hl7-fhir-udap-common#readme)
- [hl7-fhir-udap-client](https://github.com/Evernorth/hl7-fhir-udap-client#readme)
- [hl7-fhir-udap-server](https://github.com/Evernorth/hl7-fhir-udap-server#readme)

## Client User Interface
![Client User Interface](./doc/ClientUIFull.png)

## User Interface UDAP Features
The following features are supported by the user interface:

**Add Servers**: The user interface supports adding different UDAP servers so the client can connect with multiple different servers in the community.
![Add Server Screen](./doc/AddServer.png)

**UDAP trusted dynamic client registration**: Once a new server is added using the register button will trigger the client to use UDAP trusted dynamic client registration to dynamically get a client id for that server.  The registreation is executed twice, once for Authorization Code Flow (B2C Registration), and once for Client Credentials Flow (B2B Registration).  This is triggered by clicking the Register Client button for the selected server.  If a client id already exists an "edit registration" is preformed.

**UDAP B2B Authorization**: This supports the UDAP version of OAuth2 Client Credentials Flow for obtaining an access token.  It is trigged by clicking the Get Token button in the B2B Token section of the user interface.

**UDAP B2C Authorization**: This supports the UDAP version of OAuth2 Authorization Code Flow for authenticating, and obtaining an access token.  It is triggered but clicking the Get Token button in the B2C Token section of the user interface.

**UDAP Tiered OAuth**: This supports the [Tiered OAuth](https://hl7.org/fhir/us/udap-security/user.html) floe, where the client passes in a preferred OpenID Connect Identity Provider (IDP) that the client wishes to user for user authentication.   This is triggerd by populating the Upstream IDP URL text box in the B2C Token section of the user interface, and then clicking the Get Token button of the same section.  The Upstream IDP URL box will be disabled if the currently selected server does not support Tiered OAuth.

## User Interface FHIR Features

**FHIR Request**: This section supports issuing various FHIR resource get requests using a patient identifier.  The resources supported today are Patient, Allergy, Condition, and Medication.  The resources are selected by using the resource radio buttons in the FHIR Request section of the user interface.  The requests can be issued using either the B2B or B2C token by using the token radio button in the same section.  The request is triggerd by clicking the Get Patient Data button.

**FHIR Patient Search**: This section supports issuing a FHIR search on the Patient resource using the text boxes.   The request can be issued using either the B2B or B2C token by using the token radio button in the same section.  The request is triggerd by clicking the Get Patient Search button.

**FHIR Patient $match**: This section supports issuing a post FHIR patient $match operation request.  There are radio buttons to select the IDI Patient profile used in the request as defined here [Patient Weighted Input Information](http://hl7.org/fhir/us/identity-matching/2022May/patient-matching.html#patient-weighted-input-information).  The request can be issued using either the B2B or B2C token by using the token radio button in the same section.  The request is triggerd by clicking the Post Patient Match button.

## Usage

In order to use the user interface the following pre-requisites are required:

- [hl7-fhir-udap-common](https://github.com/Evernorth/hl7-fhir-udap-common#readme)
- [hl7-fhir-udap-client](https://github.com/Evernorth/hl7-fhir-udap-client#readme)
- Node.js
- At least one base URL of the UDAP secured FHIR server you are going to use

## Installation

Currently the repositories are set up for local installation.  Placing all 4 repositories under the same parent folder will allow the package.json local file references to be resolved accurately.  Eventually this repository will be an npm package. 

### Step 1- Clone needed UDAP repositories
- [hl7-fhir-udap-common](https://github.com/Evernorth/hl7-fhir-udap-common#readme)
- [hl7-fhir-udap-client](https://github.com/Evernorth/hl7-fhir-udap-client#readme)

### Step 2- Install dependencies
```
npm install
```

### Step 3- Configure default.json file
Fill in all the fields in the config/default.json file.  You will need to place your community certificate, and trust anchor file in the udap_pki folder.

### Step 4- Run the app
Run the user interface locally
```
node app.js
```

Once you run the app the first thing you will be presented with is the Add Server screen.  


## Getting help

If you have questions, concerns, bug reports, etc, please file an issue in this repository's Issue Tracker.

## Getting involved

Please see the [CONTRIBUTING.md](CONTRIBUTING.md) file for info on how to get involved.

## License

hl7-fhir-udap-test-client is Open Source Software released under the [Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0.html).

## Original Contributors

The hl7-fhir-udap-client was developed originally as a collaborative effort between [Evernorth](https://www.evernorth.com/) and [Okta](https://www.okta.com/).  We would like to recognize the following people for their initial contributions to the project: 
 - Tom Loomis - Evernorth
 - Dan Cinnamon - Okta