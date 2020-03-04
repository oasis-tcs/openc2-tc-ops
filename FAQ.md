# OpenC2 Frequently Asked Questions

* __What is OpenC2?__ A standardized language for the command and control of technologies that provide or support cyber defenses.

* __What similar efforts exist?__ There are some similarities between OpenC2 and the 
recently announced 
[Open Cybersecurity Alliance's OpenDXL Ontology](https://opencybersecurityalliance.github.io/opendxl-ontology/)

* __How is the OpenC2 TC organized?__ The [OpenC2 Technical Committee](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2), 
an OASIS TC, has three sub-committees:
  * [Language](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2-lang): Responsible for the 
  development, maintenance, and resolution of comments to the OpenC2 language documentation, including the 
  language specification documents, use cases, glossary, etc.
  * [Actuator Profiles](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2-actuator): Defining actuator profiles, the mapping and description of OpenC2 elements applicable to specific cyber defense functions.
  * [Implementation Considerations](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2-imple): 
  Provides guidance for implementation aspects such as message transport and information assurance.

* __What is the TC's process for creating work products?__

* __What are the TC and Subcommittee meeting schedules?__ All TC and SC meetings are nominally scheduled for 1 hour duration, 
and are conducted using [Lucid Meetings](https://www.lucidmeetings.com/). The current meeting schedule is as follows:
  * TC meetings are normally the 3rd Wednesday of the month, with two sessions: one at 11:00 AM and one at 9:00 PM US Easter time.
  * Language SC meetings are held the first Monday of each month at 1:00 PM US Eastern time.
  * Actuator Profile SC meetings are held the second and forth Tuesday of each month at 1:00 PM US Eastern time.
  * Implementation Considerations SC meetings are held the first Wednesday of each month at 2:00 PM US Eastern time.

 
* __Is there an OpenC2 API?__ Yes.  A network API can be considered a contract that says if a client sends a request to a server in a specified format, the server will always return a response in a specified format or initiate a defined action.  The OpenC2 Language Specification and Actuator Profiles together define the request and response content and expected actions, and a Transfer Specification defines the communication-related portions of the "specified format".

* __How does OpenC2 relate to...__
  * _the [OASIS Collaborative Automated Course of Action Operations (CACAO) for Cyber Security TC](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=cacao)?_ CACAO's goal is defining the standard for implementing course of action 
  playbooks for cybersecurity operations.
  * _STIX COA?_
  * _[MISP](https://www.misp-project.org/features.html)?_ MISP originally stood for 
  Malware Information Sharing Platform but it has evolved to "Open Source Threat 
  Intelligence Platform & Open Standards For Threat Information Sharing" according to its homepage.
  * _[OpenDXL](https://www.opendxl.com/)?_ an initiative to create adaptive systems of interconnected 
  services that communicate and share information for real-time, accurate security decisions and actions.
  * _the [Open Cybersecurity Alliance](https://opencybersecurityalliance.org/)?_
  * _the [Open Cybersecurity Alliance's OpenDXL Ontology](https://opencybersecurityalliance.github.io/opendxl-ontology/)?_
  * _the [Open Connectivity Foundation](https://openconnectivity.org/)?_
  * _[Open Security Controls Assessment Language (OSCAL)](https://pages.nist.gov/OSCAL/)?_ OSCAL is a set of formats 
  expressed in XML, JSON, and YAML. These formats provide machine-readable representations of control catalogs, 
  control baselines, system security plans, and assessment plans and results. OSCAL development is being managed 
  in a [GitHub repository](https://github.com/usnistgov/OSCAL).
  * _[FIRST Information Exchange Policy (IEP)](https://www.first.org/iep/)?_ IEP is a framework that Computer 
  Security Incident Response Teams (CSIRT), security communities, organizations, and vendors may consider 
  implementing to support their information sharing and information exchange initiatives.
  * _[Turbinia](https://github.com/google/turbinia)?_ Turbinia is an open-source framework from Google for deploying, managing, and running distributed forensic workloads. 
  * _[OpenDDS](https://opendds.org/)?_ OpenDDS is an open source C++ implementation of the Object Management Group (OMG) [Data Distribution Service (DDS)](https://www.omg.org/spec/DDS/About-DDS/), a Data-Centric Publish-Subscribe (DCPS) model for distributed application communication and integration.
  * _[Open Network Automation Platform (ONAP)](https://www.onap.org/)?_
  * _[Security Content Automation Protocol (SCAP)](https://csrc.nist.gov/projects/security-content-automation-protocol)?_
  * _Business Process Modeling Notation (BPMN)_?

