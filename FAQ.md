# OpenC2 Frequently Asked Questions

* __What is OpenC2?__ A standardized language for the
  command and control of technologies that provide or
  support cyber defenses. The [OpenC2 Technical
  Committee](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2)
  is developing a suite of specifications that define the
  OpenC2 language, tailor its use to specific cyber defense
  functions, and specify how to convey OpenC2 messages using
  various industry-standard transfer protocols.

* __What similar efforts exist?__ There are some similarities between OpenC2 and the 
recently announced [Open Cybersecurity Alliance's OpenDXL Ontology](https://opencybersecurityalliance.github.io/opendxl-ontology/). OpenDXL is a cybersecurity messaging format for use with the OpenDXL messaging bus. However, OpenC2 is transport agnostic allowing for granular implementations to various operational environments.

* __How is the OpenC2 TC organized?__ The [OpenC2 Technical Committee](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2), 
an OASIS TC, has three sub-committees:
  * [Language](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2-lang): Responsible for the 
  development, maintenance, and resolution of comments to the OpenC2 language documentation, including the 
  language specification documents, use cases, glossary, etc.
  * [Actuator Profiles](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2-actuator): Defining actuator profiles, the mapping and description of OpenC2 elements applicable to specific cyber defense functions.
  * [Implementation Considerations](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2-imple): 
  Provides guidance for implementation aspects such as message transport and information assurance.

* __What is the TC's process for creating work products?__
      The OpenC2 TC's process for creating and managing work
      products is capture in the TC's [_Documentation
      Norms_](https://github.com/oasis-tcs/openc2-tc-ops/blob/master/Documentation-Norms.md)

* __What are the TC and Subcommittee meeting schedules?__ All TC and SC meetings are nominally scheduled for 1 hour duration, 
and are conducted using [Lucid Meetings](https://www.lucidmeetings.com/). The current meeting schedule is as follows:
  * TC meetings are normally the 3rd Wednesday of the month,
    with two sessions: one at 11:00 AM and one at 9:00 PM US
    Easter time. For minutes and attendance purposes, the
    two sessions are treated as a single meeting.
  * Language SC meetings are held the first Monday of each month at 1:00 PM US Eastern time.
  * Actuator Profile SC meetings are held the second and forth Tuesdays of each month at 1:00 PM US Eastern time.
  * Implementation Considerations SC meetings are held the first Wednesday of each month at 2:00 PM US Eastern time.

 
* __Is there an OpenC2 API?__ The OpenC2 Language Specification and Actuator Profiles taken together define the request and response message content and expected actions, and a Transfer Specification defines the communications method. The exchange of OpenC2 command and response messages using the [HTTPS Transfer Specification](https://docs.oasis-open.org/openc2/open-impl-https/v1.0/open-impl-https-v1.0.html) can be considered a Remote Procedure Call (RPC)-style Web API.  OpenC2 does not have a Web API defined in terms of Representational State Transfer (REST).

* __How does OpenC2 relate to...__
  * _the [OASIS Collaborative Automated Course of Action Operations (CACAO) for Cyber Security TC](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=cacao)?_ CACAO's goal is defining the standard for creating machine-readable course of action playbooks for cybersecurity operations. CACAO will have the ability of integrating different languages for controlling components that are part of cyber defense ecosystems, thus, OpenC2 is a candidate.
  
  * _STIX COA?_ Structured Threat Information Expression (STIX™) is a language and serialization format used to exchange cyber threat intelligence (CTI). One of the STIX Domain Objects (SDOs), Course of Action, has the ability to capture structured/automated courses of action. OpenC2 can be utilized to populate STIX COA SDOs for sharing automated courses of action for the purpose of responding to cyber incidents in cyber-relevant time.
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
  * _[ROLIE](https://datatracker.ietf.org/doc/rfc8322/)_?
    ROLIE is the _Resource-Oriented Lightweight Information
    Exchange_, defined in [RFC
    8322](https://www.rfc-editor.org/info/rfc8322).  ROLIE
    defines a resource-oriented approach for security
    automation information publication, discovery, and
    sharing.  Using this approach, producers may publish,
    share, and exchange representations of software
    descriptors, security incidents, attack indicators,
    software vulnerabilities, configuration checklists, and
    other security automation information as web-addressable
    resources. Furthermore, consumers and other stakeholders
    may access and search this security information as
    needed, establishing a rapid and on-demand information
    exchange network for restricted internal use or public
    access repositories.  The specification extends the Atom
    Publishing Protocol and Atom Syndication Format to
    transport and share security automation resource
    representations.
  * _[Manufacturer Usage Descriptions
    (MUD)](https://developer.cisco.com/docs/mud/#!what-is-mud)_?
    Manufacturer Usage Description (MUD) is an embedded
    software standard defined by the IETF that allows IoT
    Device makers to advertise device specifications,
    including the intended communication patterns for their
    device when it connects to the network. The network can
    then use this intent to author a context-specific access
    policy, so the device functions only within those
    parameters. In this manner, MUD becomes the
    authoritative identifier and enforcer of policy for
    devices on the network.  MUD is defined in [RFC 8520](https://tools.ietf.org/html/rfc8520).