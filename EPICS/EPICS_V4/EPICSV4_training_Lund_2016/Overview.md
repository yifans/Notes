# Overview

---

# 1. Key Concepts

## pvData -- V4的数据结构
- System of structured data types
- Scalar fields 标量域
- Variant and regular (tagged) unions 变化的和规律的(可标记的)共用体???
- Arrays
- Structured fields (nested structures)

## pvAccess -- V4的传输协议
- Defined by pvAccess protocol specification
- pvAccess is the EPICS Version 4 communication protocol.
- High performance network protocol.
- Designed to carry pvData.
- Successor to Channel Access. CA的接班人

## Normative Types -- 规范的类型
- Standard types to aid interoperability(互用性)
- Defines standard structures for alarm, timestamps enumerations(枚举)
- Standard types for scalar, scalar array and enum PVs
- More complex types such as tables and detector images

```
NTScalar :=

structure
    scalar_t    value
    string      descriptor  :opt
    alarm_t     alarm       :opt
    time_t      timeStamp   :opt
    display_t   display     :opt
    control_t   control     :opt
```
- Specification of standard, named type
- Often choices (field types, field names)
- Required and optional fields
- Extra fields can be added
- Italics(斜体) denote definitions (non-terminal terms)

## pvRequest and pvRequest string
- Draft standard
- Requests for part of a structure
- Processing options (process, block)
- Monitoring options: Queue size. (Deadband, server-side filtering in the future)
- RPC: TBD

### pvRequest
### pvRequest string

- A string representation of this is
    `field(value,alarm.severity,timeStamp{secondsPastEpoch,nanoseconds})`
- The short form is also possible
    `value,alarm.severity,timeStamp{secondsPastEpoch,nanoseconds}`

# 2. EPICS V4 work
- EPICS V4 ...
	- Is a colaboration
	- Produces open standards
	- Provides reference implementations, including releases
	- Is administered through the working group

- Regular comunication (email/github, teleconference, face-to-face)

# 3. Resources
## EPICS V4 Resouces
- SourceForge Website: http://epics-pvdata.sourceforge.net/
- Github: https://github.com/epics-base

## Key documents
On the documentation page:

- [pvAccess Protocol Specification](http://epics-pvdata.sourceforge.net/pvAccess_Protocol_Specification.html)
- [Normative Types Specification](http://epics-pvdata.sourceforge.net/alpha/normativeTypes/normativeTypes.html)
- [pvRequest specification](http://epics-pvdata.sourceforge.net/informative/pvRequest.html)
- [Getting started guide](http://epics-pvdata.sourceforge.net/gettingStarted.html)
- [Developer Guide](http://epics-pvdata.sourceforge.net/informative/developerGuide/developerGuide.html)

# 4. Modules
- pvDataCPP/pvDataJava: Implementation of pvData
- pvAccessCPP/pvAccessJava: Implementation of pvAccess
- normativeTypesCPP/normativeTypesJava: Implementation of Normative Types
- pvCommonCPP: Boost shared pointers (for RTEMS/VxWorks) and micro-benchmarking
- pvaSrv: Adding pvAccess to existing V3 IOC (C++ only)
- pvDatabaseCPP/pvDatabaseJava: Record/Database library for creating V4 IOCs
- pvaClientCPP/pvaClientJava: High-level client library
- pvaPy: EPICS V4 Python library

- Revision numbering
`<Major>.<Minor><.Revision> `
where
	- major denotes ABI changes
	- minor denotes API changes (for major version 0 minor changes can be ABI changing).
	- Also release bundles with numbering
