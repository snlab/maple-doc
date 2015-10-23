# Architecture of Maple System


## System Overview

Maple system consists of the following key components:

* *GUI*: <Not well defined yet. One possibility is that GUI is just an APP, such that users can write GUI in their APPs.>
* *APPs*: applications written by users.
* *MapleCore*:
* *MapleAdapter<ODL>*: adapter layer between OpenDaylight and Maple system. MapleAdapter has two kinds of interfaces: (1) to MapleCore, and (2) to MapleApps.
  
Following diagram demonstrates relationship between different components .

      UI (ODL restful API to get state such as topo, flows; configuration UI to APPs)
      ---------------------------
        ^  APPsInJava
      --|------------------------
        |     ^  MapleCoreInJava
      --|-----|------------------
        |     |  ^  MapleODL
      --|-----|--|---------------
        v     v  v
      ODL Data Store


## Design Goals

* GUI should be flexible, in the sense it should not be tied to specific operating system (e.g. Windows or Linux), APPs, and network OS (e.g. ODL or ONOS).
* Multiple GUI instances are allowed register to the system.


## Overview of Workflow

**Workflow Initialization:**

1. MapleODL starts and listens at a known service point SP.
2. UI registers interest with SP.
    1. The registration msg indicates what the interests are (what data, what events)
    2. MapleODL registers listener for aggregated interest events at ODL Data Store

**Runtime at the beginning:**

1. UI queries data from MapleODL SP (CrossPlatform)
2. MapleODL SP translate the request and then get data from ODL Data Store

**Asynchronous notification: **

1. A event happens, for example a new switch is added
2. MapleODL handler registered at ODL Data Store is invoked
3. MapleODL handler pushes (e.g, SSE) the needed data json to the registered UI


### Key Components

* **Interface between GUI and MapleODL**: [https://github.com/snlab/MapleGUI/wiki/Current-REST-interface-(reference)](https://github.com/snlab/MapleGUI/wiki/Current-REST-interface-(reference))
  1. What are the principles that guided our definition of the API (data model)? Does it map naturally to ODL/ONOS, or conceptually clean?
    * Approach 1: Use one community model (e.g., ODL YANG model mostly)
    * Approach 2: Appoint Shenshen as God of the model and just listens to him
    * Approach 3: ONOS as the God
    * Approach 4: Take 30% from ODL and 60% from ONOS, and 10% from Shenshen
    * Approach 5: Minimal work (Since Daivd's version already compiles and we use it)
    * **Current Decision** Proposal (by David, which Richard seconds): Adopt a major community model

 2. How to visualize wildcard flows (Is a flow one entry in the flow table of one switch?), multicast.
    * David/Jason is working on this part.

* **Asynchronous notification protocol between GUI and MapleODL**: [SSE](http://www.w3.org/TR/eventsource/)
  1. Given the time, we implement the first version in the following way:
    1.  UI app periodcally query (e.g.https://github.com/snlab/MapleGUI/wiki/Current-REST-interface-(reference)).
    2.  MapleODL Adapter implements the preceding.
    3.  UI app do the merge by itself.
  
* **Interface between MapleCore and MapleODL**: [https://github.com/snlab/maple-doc/blob/master/design/MapleCore-API-Design-Document.md](https://github.com/snlab/maple-doc/blob/master/design/MapleCore-API-Design-Document.md)

* **Callback registration from MapleODL to ODL Data Store**: [https://wiki.opendaylight.org/view/OpenDaylight_Controller:MD-SAL:Restconf:Change_event_notification_subscription](https://wiki.opendaylight.org/view/OpenDaylight_Controller:MD-SAL:Restconf:Change_event_notification_subscription)

* **Proposal of MapleAdapterCommon**. Different versions of MapleAdapter are required when we run Maple system across different networking OSes. For example, in the near future, MapleAdapterODL, MapleAdapterONOS, and MapleAdapterFloodlight are required. To reuse code as much as possible, one possible design is that we identify common functions among different versions of MapleAdapter and put these functions into an library named MapleAdapterCommon. In other words, *Common = MapleODL ^ MapleONOS ^ MapleFloodlight*, and *MapleODLAdapter = MapleODL - Common*.
