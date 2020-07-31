Requirements on Diagnostic Extract Template
###########################################

.. contents:: Table of Contents
    :depth: 5
    :backlinks: top


Part of Standard Release R19-11

1 Introduction
************************


1.1 Scope of this document
================================

This document collects the requirements on the Diagnostic Extract.

The main goal of the Diagnostic Extract is to exchange diagnostic data between the
different parties involved in the diagnostic development process to support the automatic
code generation process for diagnostic modules :term:`DCM` and :term:`DEM`.

Further, the Diagnostic Extract is used to support the distributed development process
for diagnostic functionality.

Below, the key aspects for the usage of the Diagnostic Extract are mentioned again:

* Exchange of diagnostic data for :term:`DCM` and :term:`DEM`

* Support of distributed development for diagnostic functionality


1.2 Document Conventions
================================

The representation of requirements in AUTOSAR documents follows the table specified
in [`TPS_STDT_00078`_], see Standardization Template, chapter Support for Traceability
([1]).

The verbal forms for the expression of obligation specified in [TPS_STDT_00053] shall
be used to indicate requirements, see Standardization Template, chapter Support for
Traceability ([1]).


1.3 Guidelines
================================

Existing specifications shall be referenced (in form of a single requirement).
Differences to these specifications are specified as additional requirements.
All Requirements shall have the following properties:

* Redundancy

Requirements shall not be repeated within one requirement or in other require-
ments.

* Clearness

All requirements shall allow one possibility of interpretation only. Used technical
terms that are not in the glossary must be defined.

* Atomicity

Each Requirement shall only contain one requirement. A Requirement is atomic
if it cannot be split up in further requirements.

* Testability

Requirements shall be testable by analysis, review or test.

* Traceability

The source and status of a requirement shall be visible at all times.


1.4 Requirements Tracing
================================

Currently no requirements tracing is provided for this document. Requirement tracing
will be included in later revision.


2 Requirements
************************

2.1 Relation to AUTOSAR Features
================================

The section describes a list of features that should be addressed by the requirements:

* [`RS_Main_00300`_] AUTOSAR shall provide data exchange formats to support work-share in large
  inter and intra-company development groups

* [`RS_BRF_01112`_] AUTOSAR shall offer interfaces to boot loaders.

* [`RS_BRF_01440`_] AUTOSAR services shall support system diagnostic functionality.

This is a short selection of features and main requirements which need to be fulfilled
by the requirements on the Diagnostic Extract.

2.2 General Requirements
================================

This chapter contains a collection of general requirements that apply for all aspects of
the Diagnostic Extract.

.. _RS_DEXT_00001:


[RS_DEXT_00001] Diagnostic data exchange
------------------------------------------

.. table:: RS_DEXT_00001

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The diagnostic extract shall support the exchange of diagnostics-related information.                |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The configuration of the AUTOSAR diagnostics stack, in the vast majority of                          |
    |               | cases, is a joint effort with contributions from the OEM and the respective :term:`ECU`              |
    |               | supplier.                                                                                            |
    |               |                                                                                                      |
    |               | For this purpose, the :term:`OEM` and the supplier need to be able to exchange                       |
    |               | configuration information with as little friction as possible. In general, arbitrary                 |
    |               | combinations of particular :term:`OEM` s and specific suppliers are possible. To make                |
    |               | this work it is necessary to standardize the data exchanged between the                              |
    |               | affected parties to the necessary extent.                                                            |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | 0. :term:`OEM` delivers a partial configuration to a supplier that in turn is expected               |
    |               | to fill in the missing pieces and/or review and (where applicable)                                   |
    |               | overwrite configuration done by the :term:`OEM`.                                                     |
    |               |                                                                                                      |
    |               | 0. Supplier feeds back reviewed diagnostics configuration                                            |
    |               | to the :term:`OEM`.                                                                                  |
    |               |                                                                                                      |
    |               | 0. Supplier delivers the final configuration of the diagnostics stack back to                        |
    |               | the :term:`OEM` such that the latter is able to derive a tester configuration from                   |
    |               | this data.                                                                                           |
    |               |                                                                                                      |
    |               | 0. Suppliers or :term:`OEM` s use the Diagnostic Extract to exchange the                             |
    |               | information within the company between related responsible                                           |
    |               | organization parts. By this means a distributed software development is                              |
    |               | supported within the company.                                                                        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00044:

[RS_DEXT_00044] Derivation of related ECU-C parameter
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00044

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the derivation of related :term:`ECU-C`                         |
    |               | parameters for :term:`Dcm`, :term:`Fim` and :term:`Dem`.                                             |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | A concrete configuration of an AUTOSAR diagnostic stack on the level of                              |
    |               | :term:`ECUC` is, by definition, not portable. It is very much focused on specific details            |
    |               | that reflect the specific implementation of the particular diagnostic stack. This                    |
    |               | approach is reasonable because it allows for a deeper optimization of the                            |
    |               | software stack than a general and more abstract approach would support.                              |
    |               |                                                                                                      |
    |               | However, the more abstract approach has other benefits in terms of being                             |
    |               | exchangeable across different organizations and, to some extent, even                                |
    |               | projects.                                                                                            |
    |               |                                                                                                      |
    |               | Therefore, it is reasonable to define a general and more abstract way of                             |
    |               | configuring the diagnostic stack for which the ultimate goal is to derive the                        |
    |               | concrete and non-portable specific configuration to a large extent.                                  |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | A user wants the specify configuration of the diagnostic stack in a general way                      |
    |               | that can be exchanged with project partners in the same way that e.g. a system                       |
    |               | description can be exchanged.                                                                        |
    |               |                                                                                                      |
    |               | The user wants to specify the diagnostic information on the same conceptual                          |
    |               | level as the system extract and the user wants to relate from the diagnostic                         |
    |               | configuration to elements of a system extract where applicable. Finally,                             |
    |               | someone wants to take this information that is described on a higher                                 |
    |               | conceptual level and use if for the derivation of configuration information on the                   |
    |               | much more specific (and, consequently, less portable) level that is :term:`ECUC`.                    |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+

.. _RS_DEXT_00046:

[RS_DEXT_00046] Variants
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00046

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support variants.                                                       |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | AUTOSAR models in general may consist of different variants of the same                              |
    |               | aspect. The modeling of different variants on one end may have an impact on                          |
    |               | an other end, i.e. the other end also needs variants in order to properly                            |
    |               | implement model consistency. In other words, if the configuration of an :term:`ECU`                  |
    |               | (e.g. in terms of a system description) has variants it is more or less likely that                  |
    |               | also the configuration of the diagnostic stack on the :term:`ECU` needs to consider                  |
    |               | these variants and react accordingly.                                                                |
    |               |                                                                                                      |
    |               | On top of that, the diagnostic extract may need to define variants out of a totally                  |
    |               | different motivation that is not connected to the existence of variants in the                       |
    |               | corresponding system description.                                                                    |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user needs to consider existing variants in the corresponding system                             |
    |               | description and therefore introduce variant points that bind with the same                           |
    |               | expressions as the applicable variation points in the system description.                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+



.. _RS_DEXT_00048:

[RS_DEXT_00048] Diagnostic Properties that are specific for one ECU
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00048

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the definition of diagnostic properties that                    |
    |               | are specific for a given :term:`ECU`.                                                                |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | Some properties differ from :term:`ECU` to :term:`ECU`. In case the diagnostic extract covers        |
    |               | multiple :term:`ECU` s at the same time it is necessary to express their diagnostic                  |
    |               | properties individually.                                                                             |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to specify a diagnostic extract consisting of several :term:`ECU` s and               |
    |               | the user wants to define certain properties individually for each of the included                    |
    |               | :term:`ECU` s.                                                                                       |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+



.. _RS_DEXT_00058:

[RS_DEXT_00058] Indicate that an ECU supports OBD
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00058

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The diagnostic extract shall allow for the definition of whether (and how) a given                   |
    |               | :term:`ECU` supports :term:`OBD`                                                                     |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | There are certain switches to be set in the downstream configuration that                            |
    |               | depend on the information about the :term:`OBD` capabilities of a given ECU.                         |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to specify the applicability of :term:`OBD` for a given :term:`ECU`                   |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00059:

[RS_DEXT_00059] Support for different protocols
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00059

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The diagnostic extract shall support the definition of different diagnostic                          |
    |               | protocols (e.g. :term:`UDS`, :term:`OBD`, etc.) and their priority in relation to each other.        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | Different protocols shall be handled with different priorities. This requires a                      |
    |               | formal definition of a diagnostic protocol and its relation to further model                         |
    |               | elements that are already part of the diagnostic extract.                                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to define a diagnostic extract that supports different diagnostic                     |
    |               | protocols.                                                                                           |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+

2.3 Requirements against the Support for UDS Diagnostic Services
================================================================================================

This chapter contains a collection of requirements against the context of UDS
diagnostic services according to [2].


.. _RS_DEXT_00003:

[RS_DEXT_00003] SessionControl
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00003

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x10                   |
    |               | (SessionControl).                                                                                    |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The usage of different diagnostic sessions is very common and therefore                              |
    |               | needs to be supported by the Diagnostic Extract Template.                                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | Support the switching from one diagnostic session to another.                                        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00004:

[RS_DEXT_00004] ECUReset
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00004

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x11                   |
    |               | (ECUReset).                                                                                          |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The ability to reset the server is crucial for conducing a diagnostic session.                       |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to reset the connected server.                                                        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00005:

[RS_DEXT_00005] ClearDiagnosticInformation
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00005

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x14                   |
    |               | (ClearDiagnosticInformation).                                                                        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for clearing the diagnostic memory of a server. This is a                         |
    |               | frequently used functionality.                                                                       |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to clear diagnostic memory on the connected server.                                   |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+




.. _RS_DEXT_00006:

[RS_DEXT_00006] ReadDTCInformation
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00006

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x19                   |
    |               | (ReadDTCInformation).                                                                                |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for accessing the status of a diagnostic trouble code on the                      |
    |               | server. This is a frequently used functionality.                                                     |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to access DTC information via a tester on the server.                                 |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00007:

[RS_DEXT_00007] ReadDataByIdentifier
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00007

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x22                   |
    |               | (ReadDataByIdentifier).                                                                              |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for reading values on the server according to the definition                      |
    |               | of a given data identifier. This is a frequently used functionality.                                 |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to read the values associated with a given data identifier from                       |
    |               | the server.                                                                                          |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+



.. _RS_DEXT_00008:

[RS_DEXT_00008] ReadMemoryByAddress
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00008

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x23                   |
    |               | (ReadMemoryByAddress).                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for accessing the content of a piece of memory on the                             |
    |               | server. This is a frequently used functionality.                                                     |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to read memory content from the diagnostic server.                                    |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+



.. _RS_DEXT_00009:

[RS_DEXT_00009] SecurityAccess
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00009

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x27                   |
    |               | (SecurityAccess).                                                                                    |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | This service allows for data and diagnostic services for which specific security                     |
    |               | restrictions apply.                                                                                  |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The application of security restrictions limits the access to data and diagnostic                    |
    |               | services to authorized personnel. The restriction may be applied for safety                          |
    |               | and/or security reasons.                                                                             |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00010:

[RS_DEXT_00010] CommunicationControl
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00010

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x28                   |
    |               | (CommunicationControl).                                                                              |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | This service allows for switching on and off the communication of certain                            |
    |               | messages (e.g. application-related communication).                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to switch off normal communication messages.                                          |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+



.. _RS_DEXT_00011:

[RS_DEXT_00011] ReadDataByPeriodicIdentifier
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00011

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x2A                   |
    |               | (ReadDataByPeriodicIdentifier).                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for requesting the periodic transmission of diagnostic data                       |
    |               | by the server according to the definition of a periodic data identifier.                             |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to get access to diagnostic data that is transmitted periodically                     |
    |               | without the necessity to request each transmission individually.                                     |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+



.. _RS_DEXT_00012:

[RS_DEXT_00012] DynamicallyDefineDataIdentifier
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00012

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x2C                   |
    |               | (DynamicallyDefineDataIdentifier).                                                                   |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for the ad-hoc definition of a data identifier that can then be                   |
    |               | accessed by the respective diagnostic services.                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | In contrast to the case where data identifiers are defined in advance of a                           |
    |               | diagnostic session, this service allows for defining data identifiers while a                        |
    |               | diagnostic session is ongoing.                                                                       |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+



.. _RS_DEXT_00013:

[RS_DEXT_00013] WriteDataByIdentifier
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00013

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x2E                   |
    |               | (WriteDataByIdentifier).                                                                             |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for transmitting diagnostic data identified by the association                    |
    |               | with a diagnostic data identifier to a diagnostic server. This is a frequently used                  |
    |               | functionality.                                                                                       |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to transmit data associated with a given data identifier to the                       |
    |               | diagnostic server.                                                                                   |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00014:

[RS_DEXT_00014] IOControl
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00014

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x2F                   |
    |               | (IOControl).                                                                                         |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service allows for substituting values of the I/O layer with values provided                     |
    |               | by the diagnostic tester.                                                                            |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to bypass a sensor and feeds substitution values instead. The                         |
    |               | user wants to substitute values provided to a given actuator.                                        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00015:

[RS_DEXT_00015] RoutineControl
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00015

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x31                   |
    |               | (RoutineControl).                                                                                    |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service can be used to execute specific code on the server according.                            |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to execute code on the remote server in order to achieve a                            |
    |               | given functionality that goes beyond the capabilities provided by any of the                         |
    |               | "simple" data exchange services.                                                                     |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00016:

[RS_DEXT_00016] RequestDownload
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00016

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x34                   |
    |               | (RequestDownload).                                                                                   |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | This service has the ability to request the server to accept the transfer of a                       |
    |               | piece of data from the client (e.g. tester) to the server. Support for this service                  |
    |               | is the prerequisite for a support of the service described in [`RS_DEXT_00018`_].                    |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to transmit a piece of (mostly complex) data from the client to                       |
    |               | the server.                                                                                          |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00017:

[RS_DEXT_00017] RequestUpload
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00017

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x35                   |
    |               | (RequestUpload).                                                                                     |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | This service has the ability to request the server to accept the transfer of a                       |
    |               | piece of data from the server to a client (e.g. tester). Support for this service is                 |
    |               | the prerequisite for a support of the service described in [`RS_DEXT_00018`_].                       |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to transmit a piece of (mostly complex) data from the server to                       |
    |               | the client.                                                                                          |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00018:

[RS_DEXT_00018] TransferData
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00018

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x36                   |
    |               | (TransferData).                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | This service is used to actually execute a data transfer between client and                          |
    |               | server.                                                                                              |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to transmit a piece of (mostly complex) data between client and                       |
    |               | server.                                                                                              |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00019:

[RS_DEXT_00019] RequestTransferExit
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00019

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x37                   |
    |               | (RequestTransferExit).                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service can be taken to request the termination of a data transmission                           |
    |               | between server and client (independent of the direction of the data                                  |
    |               | transmission).                                                                                       |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to actively end a data transmission between client and server.                        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00020:

[RS_DEXT_00020] WriteMemoryByAddress
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00020

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x3D                   |
    |               | (WriteMemoryByAddress).                                                                              |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service can be used to write a piece of data to the server's memory.                             |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to overwrite the values in a given piece of server memory.                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00021:

[RS_DEXT_00021] ControlDTCSetting
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00021

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x85                   |
    |               | (ControlDTCSetting).                                                                                 |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service can be used to control the updating of status bits of diagnostic                         |
    |               | trouble codes in the server.                                                                         |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to either stop or resume the updating of status bits of                               |
    |               | diagnostic trouble codes in the server.                                                              |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00022:

[RS_DEXT_00022] ResponseOnEvent
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00022

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x86                   |
    |               | (ResponseOnEvent).                                                                                   |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service can be used to control the behavior of the server with respect to                        |
    |               | the transmission of data in response to a given event.                                               |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to control the behavior of the server in terms of how the server                      |
    |               | sends response messages according to the existence of a given event.                                 |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00057:

[RS_DEXT_00057] RequestFileTransfer
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00057

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the configuration of :term:`UDS` service 0x38                   |
    |               | (RequestFileTransfer).                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The service RequestFileTransfer is part of the subset of :term:`UDS` services                        |
    |               | supported by the Diagnostic Extract.                                                                 |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to specify a file transfer to/from the server.                                        |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | More information about this diagnostic service can be found in the respective                        |
    | Material:     | ISO specification [2].                                                                               |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00047:

[RS_DEXT_00047] Custom Diagnostic Service
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00047

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the definition of custom diagnostic                             |
    |               | services.                                                                                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | In some cases diagnostic services beyond the set of services standardized in                         |
    |               | ISO14229 are needed.                                                                                 |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to execute a diagnostic functionality that is not part of the                         |
    |               | specification of ISO 14229 [2]                                                                       |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00049:

[RS_DEXT_00049] Properties of individual diagnostic services
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00049

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the definition of properties that are specific                  |
    |               | for a given diagnostic service.                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | Some properties of diagnostic services need to be individually fine-tuned for                        |
    |               | every instance of a given class of diagnostic service, e.g. ReadDataByIdentifier.                    |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to define specific properties differently for all instances of a                      |
    |               | given diagnostic service.                                                                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00050:

[RS_DEXT_00050] Properties of all diagnostic services of a given kind
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00050

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the definition of properties that are                           |
    |               | common for all instances of a kind of diagnostic service.                                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | Some properties of diagnostic services are common for all instances of the                           |
    |               | specific diagnostic service. If these were specifiable on an individual basis                        |
    |               | there would be potential for inconsistencies in the specification of different                       |
    |               | instances of the diagnostic service.                                                                 |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to define specific properties that are shared among all                               |
    |               | instances of a given diagnostic service.                                                             |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00051:

[RS_DEXT_00051] Subfunctions of Diagnostic Services
------------------------------------------------------------------------------------

.. table:: RS_DEXT_00051

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the definition of subfunctions of diagnostic                    |
    |               | services.                                                                                            |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The definition of subfunctions is an important part of the definition of diagnostic                  |
    |               | services. Also, the existence of subfunctions for certain diagnostic services is                     |
    |               | regulated by the applicable ISO 14229-1 [2].                                                         |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to specify subfunctions for given diagnostic services.                                |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+


.. _RS_DEXT_00052:

[RS_DEXT_00052] Mapping of diagnostic services to the PortPrototypes of ApplicationSwComponentTypes
------------------------------------------------------------------------------------------------------------

.. table:: RS_DEXT_00052

    +---------------+------------------------------------------------------------------------------------------------------+
    | Type:         | valid                                                                                                |
    |               |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Description:  | The Diagnostic Extract shall support the specification of how diagnostic                             |
    |               | services are mapped to the PortPrototypes of ApplicationSwComponentTypes                             |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Rationale:    | The mapping of diagnostic services to the the PortPrototypes of                                      |
    |               | ApplicationSwComponentTypes connects the definition of diagnostic services                           |
    |               | with the actual application software that these services are about. Therefore,                       |
    |               | this mapping is an important step in the workflow and also provides essential                        |
    |               | information for the integration of the software on a given :term:`ECU`.                              |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Use case:     | The user wants to map diagnostic services to application software in order to                        |
    |               | express the conceptual connection between these two aspects of the :term:`ECU`                       |
    |               | configuration.                                                                                       |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Dependencies: | --                                                                                                   |
    +---------------+------------------------------------------------------------------------------------------------------+
    | Supporting    | --                                                                                                   |
    | Material:     |                                                                                                      |
    |               |                                                                                                      |
    +---------------+------------------------------------------------------------------------------------------------------+








Chapter
************************

Chapter text

Section
=================

Section text

Subsection
------------------

Subsection text

Subsubsection
^^^^^^^^^^^^^^^^^^^

Subsubsection text

Paragraph
""""""""""""""""""""""""

Paragraph text

.. _RS_Main_00300: #
.. _RS_BRF_01112: #
.. _RS_BRF_01440: #
.. _TPS_STDT_00078: #