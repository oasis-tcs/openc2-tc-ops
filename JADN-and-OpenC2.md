# Information Modeling: JADN and OpenC2

Information models (IMs) are used to define and generate physical
data models, validate information instances, and enable lossless
translation across data formats. An IM defines the essential
content of entities used in computing, independently of how those
entities are represented (i.e., serialized) for communication or
storage. The [OpenC2 Technical Committee
(TC)](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2)
recognized the need to define the [OpenC2
language](https://docs.oasis-open.org/openc2/oc2ls/v1.0/oc2ls-v1.0.html)
in such an implementation-independent manner in order to achieve
the project's goals, and created an information modeling
language, [JSON Abstract Data Notation
(JADN)](https://docs.oasis-open.org/openc2/jadn/v1.0/cs01/jadn-v1.0-cs01.html),
to support information modeling. While JADN was created by the
OpenC2 TC, it is entirely general purpose in its design and can
be used to create IMs for nearly any purpose. Examples of
possible JADN applications include defining:

 - Data structures, such as Software Bills of Materials (SBOMs)
 - Information exchanges, such as are described by NIEM

The IETF ([RFC 8477](https://www.rfc-editor.org/info/rfc8477)) has attributed challenges in achieve interoperability to a lack of information modeling:

> _One common problem is the lack of an encoding-independent
   standardization of the information, the so-called information
   model. Another problem is the strong relationship between data
   formats and the underlying communication architecture_

The same RFC defines information and data models to clarify the differences:

 - **Information Model** -- An information model defines an
      environment at the highest level of abstraction and
      expresses the desired functionality. Information models can
      be defined informally (e.g., in prose) or more formally
      (e.g., Unified Modeling Language (UML), Entity-
      Relationship Diagrams, etc.).  Implementation details are
      hidden.

 - **Data Model** -- A data model defines concrete data
      representations at a lower level of abstraction, including
      implementation- and protocol- specific details.  Some
      examples are SNMP Management Information Base (MIB)
      modules, World Wide Web Consortium (W3C) Thing Description
      (TD) Things, YANG modules, Lightweight Machine-to- Machine
      (LwM2M) Schemas, Open Connectivity Foundation (OCF)
      Schemas, and so on.

JADN provides a means to develop abstract IMs to facilitate clear
definition of information requirements and support flexibility of
implementation that supports interoperability.

# A Brief JADN Overview

# Information Models in OpenC2

## OpenC2 Language

## OpenC2 Actuator Profiles