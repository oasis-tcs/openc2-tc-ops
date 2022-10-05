# OpenC2 Frequently Asked Questions

> NOTE: This markdown document exists to support group review and
> updates to the FAQ list. The questions and answers will be
> ported to the OpenC2.org website [FAQ
> page](https://openc2.org/faq.html) for general public
> visibility.

> Initial content created from https://openc2.org/faq.html by
> re-editing HTML content to GFM, 5 October 2022

### What is OpenC2?

OpenC2 is a standardized language for machine-to-machine
communications for the command and control of technologies that
provide or support cyber defenses.


### What is the difference between OpenC2 and OASIS?

OpenC2 is an open source language, available for use and input
across the cyber-security community. Many open source languages
and technologies benefit from support of standards bodies, to
help guide and champion on-going use and evolution of the
software or technology. OpenC2 is a project under OASIS. OASIS is
the Organization for the Advancement of Structured Information
Standards, a nonprofit international consortium that develops
open IT standards.


### What can OpenC2 do for me?

As cyber-defense technology vendors and providers adopt OpenC2,
OpenC2 can dramatically improve incident response to
cyber-threats and allow for enterprise wide interoperability for
cyber-security policy orchestration. Management and development
of cyber-defense responses is simplified and greater
collaboration and integration across a wide range of technologies
is enabled.


### How can I access OpenC2?

OASIS Specifications are open for all to use. See [this
page](https://openc2.org/openc2-org.github.io/specifications.html)
for the specifications.

Open source software to implement OpenC2 can be found [in this
page](https://openc2.org/openc2-org.github.io/opensource.html).


### Do I have to be a member of OASIS to use OpenC2?

No, OASIS OpenC2 specifications are available to all. There are
no known intellectual property rights associated with OpenC2. See
[this page](https://www.oasis-open.org/committees/openc2/ipr.php)
for additional information.

If you desire to participate in the OpenC2 Technical Committee
and draft future specifications, then OASIS membership would be
required.


### How long has this been around?

The OASIS OpenC2 TC was formed in 2017 and the first 3 OpenC2
Specifications were approved in 2019.


> _NOTE: at the 5 October 2022 working meeting, it was agreed the
> following FAQ should be re-written as a "how relates to ...?"
> question. A new answer regarding "similar efforts" may be
> appropriate to retain this FAQ._

### What similiar efforts exist?

There are some similarities between OpenC2 and the recently
announced [Open Cybersecurity Alliance's OpenDXL
Ontology](https://opencybersecurityalliance.github.io/opendxl-ontology/).
OpenDXL is a cybersecurity messaging format for use with the
OpenDXL messaging bus. However, OpenC2 is transport agnostic
allowing for granular implementations to various operational
environments.


> _NOTE: the following FAQ should probably also refer to transfer
> specifications beyond HTTPS. Also, ensure the HTTPS link is
> pointing to the current specification._

### Is there an OpenC2 API?

The OpenC2 Language Specification and Actuator Profiles taken
together define the request and response message content and
expected actions, and a Transfer Specification defines the
communications method. The exchange of OpenC2 command and
response messages using the [HTTPS Transfer
Specification](https://docs.oasis-open.org/openc2/open-impl-https/v1.0/open-impl-https-v1.0.html)
can be considered a Remote Procedure Call (RPC)-style Web API.
OpenC2 does not have a Web API defined in terms of
Representational State Transfer (REST).


### What is the TC's process for creating work products?

The OpenC2 TC's process for creating and managing work products
is captured in the TC's [Documentation
Norms](https://github.com/oasis-tcs/openc2-tc-ops/blob/master/Documentation-Norms.md).


> _NOTE: Suggest the following FAQ answer be replaced with a link
> (at least for the details) to the appropriate document in the
> TC Ops repo that describes the meeting schedule, so that it
> only needs to be maintained in one place._

### What is the meeting schedule?

All TC meetings are nominally scheduled for 1 hour duration, and
are conducted using [Lucid
Meetings](https://www.lucidmeetings.com/).

Currently, the TC holds one "voting" meeting on the third
Wednesday of each month. This meeting conducts official business
and counts towards voting rights. The voting meeting is held in
two parts to facilitate participation across timezones. The first
part of the meeting is held at 11 AM Eastern and the second part
(same agenda) is held at 9 PM Eastern. For minutes and attendance
purposes, the two sessions are treated as a single meeting and
attendance is only required at one of the two.

The TC also holds "working" meetings on the 1st, 2nd, and 3rd
Wednesdays at 11 AM Eastern. There is no meeting on the 5th
Wednesday of the month.


### How does OpenC2 relate to the OASIS [Collaborative Automated Course of Action Operations (CACAO) for Cyber Security TC](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=cacao)? 

CACAO's goal is defining the standard for creating
machine-readable course of action playbooks for cybersecurity
operations. CACAO will have the ability of integrating different
languages for controlling components that are part of cyber
defense ecosystems, thus, OpenC2 is a candidate.

### How does OpenC2 relate to STIX COA? 

Structured Threat Information Expression (STIX™) is a language
and serialization format used to exchange cyber threat
intelligence (CTI). One of the STIX Domain Objects (SDOs), Course
of Action, has the ability to capture structured/automated
courses of action. OpenC2 can be utilized to populate STIX COA
SDOs for sharing automated courses of action for the purpose of
responding to cyber incidents in cyber-relevant time.

### How does OpenC2 relate to [MISP](https://www.misp-project.org/features.html)? 

MISP originally stood for Malware Information Sharing Platform
but it has evolved to "Open Source Threat Intelligence Platform &
Open Standards For Threat Information Sharing" according to its
homepage.

### How does OpenC2 relate to [OpenDXL](https://www.opendxl.com/)? 

An initiative to create adaptive systems of interconnected
services that communicate and share information for real-time,
accurate security decisions and actions.

### How does OpenC2 relate to the [Open Cybersecurity Alliance](https://opencybersecurityalliance.org/)?

### How does OpenC2 relate to the Open Cybersecurity Alliance's [OpenDXL Ontology](https://opencybersecurityalliance.github.io/opendxl-ontology/)?

### How does OpenC2 relate to the [Open Connectivity Foundation](https://openconnectivity.org/)?


### How does OpenC2 relate to the [Open Security Controls Assessment Language (OSCAL)](https://pages.nist.gov/OSCAL/)?

OSCAL is a set of formats expressed in XML, JSON, and YAML. These
formats provide machine-readable representations of control
catalogs, control baselines, system security plans, and
assessment plans and results. OSCAL development is being managed
in a GitHub repository.

### How does OpenC2 relate to the [FIRST Information Exchange Policy (IEP)](https://www.first.org/iep/)? 

IEP is a framework that Computer Security Incident Response Teams
(CSIRT), security communities, organizations, and vendors may
consider implementing to support their information sharing and
information exchange initiatives.

### How does OpenC2 relate to [Turbinia](https://github.com/google/turbinia)? 

Turbinia is an open-source framework from Google for deploying,
managing, and running distributed forensic workloads.

### How does OpenC2 relate to [OpenDDS](https://opendds.org/)? 

OpenDDS is an open source C++ implementation of the Object
Management Group (OMG) [Data Distribution Service
(DDS)](https://www.omg.org/spec/DDS/About-DDS/), a Data-Centric
Publish-Subscribe (DCPS) model for distributed application
communication and integration.



### How does OpenC2 relate to [Open Network Automation Platform (ONAP)](https://www.onap.org/)?

### How does OpenC2 relate to [Security Content Automation Protocol (SCAP)](https://csrc.nist.gov/projects/security-content-automation-protocol)?



### How does OpenC2 relate to Business Process Modeling Notation (BPMN)?


### How does OpenC2 relate to [ROLIE](https://datatracker.ietf.org/doc/rfc8322/)? 
ROLIE is the Resource-Oriented Lightweight Information Exchange,
defined in [RFC 8322](https://datatracker.ietf.org/doc/rfc8322/).
ROLIE defines a resource-oriented approach for security
automation information publication, discovery, and sharing. Using
this approach, producers may publish, share, and exchange
representations of software descriptors, security incidents,
attack indicators, software vulnerabilities, configuration
checklists, and other security automation information as
web-addressable resources. Furthermore, consumers and other
stakeholders may access and search this security information as
needed, establishing a rapid and on-demand information exchange
network for restricted internal use or public access
repositories. The specification extends the Atom Publishing
Protocol and Atom Syndication Format to transport and share
security automation resource representations.


### How does OpenC2 relate to [Manufacturer Usage Descriptions (MUD)](https://developer.cisco.com/docs/mud/#!what-is-mud)? 

Manufacturer Usage Description (MUD) is an embedded software
standard defined by the IETF that allows IoT Device makers to
advertise device specifications, including the intended
communication patterns for their device when it connects to the
network. The network can then use this intent to author a
context-specific access policy, so the device functions only
within those parameters. In this manner, MUD becomes the
authoritative identifier and enforcer of policy for devices on
the network. MUD is defined in [RFC
8520](https://tools.ietf.org/html/rfc8520).
