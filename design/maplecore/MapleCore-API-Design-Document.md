% A Reasonable API Design for Maple
% Jensen
% Sep. 25, 2015

## Abstract

Maple is one of the most popular SDN controller nowadays, SDN programmers can use it to make programming in SDN easily. The APIs design of Maple is very important. This paper defines some practical APIs for Maple controller, which are based on several reasonable principles. The major principle in our consideration is to provide _As Less Information as Possible_.

<!-- TODO: make it more detail when the main body finished. -->

## 1. Introduction

<!-- TODO: Introduction should be completed after following and before abstract -->

## 2. Preparations

Before making our major design, we need some preparations to make sense. We should make sure that our design is totally reasonable, which is really not an easy work.

### 2.1 Principles

A good API design SHOULD follow these basic principles:

Principle 1

: API should do one thing and do it well.

Principle 2

: API should be as small as possible but no smaller.

Principle 3

: Implementation should not impact API. (avoid content coupling)

Principle 4

: Minimize accessibility of everything.

### 2.2 Axioms

There are several very basic items which MUST be included in our APIs. They are the foundation to get a complete API design.

These APIs are noted as follow (We will call them **Axioms**):

Axiom 1

: We MUST have a class `PacketIn` to reference in the callback function `onPacket`.

Axiom 2

: `PacketIn` MUST have a method `Port getIngressPort()` to get the ingress port of this packet.

Axiom 3

: `PacketIn` MUST have a method `MACAddress getSrcEthernet()` to get the MAC address of the source of this packet.

Axiom 4

: `PacketIn` MUST have a method `MACAddress getDstEthernet()` to get the MAC address of the destination of this packet.

### 2.3 Algorithmic Policy

Maple is based on algorithmic policies (AP). Every application in Maple MUST be defined as an AP, and include a callback function named `onPacket`.

The `onPacket` MUST take an object `PacketIn` as input, and return an object `Route` to forward the packet to the openflow switch.

The formal definition of this `onPacket` function is:

    onPacket :: (PacketIn, Env) -> Route

So there are three sections which have to be defined in the API design:

1. APIs for the class `PacketIn`.
2. APIs for `Env` to get the environment of the current topology.
3. APIs to set a valid route.

But according to the **Principle 4**, users don't have to get many information from `Env`. Maple need to abstract the network topology, and make the information hidden.

## 3. Minimal API Design

This part will discuss a minimal and reasonable API design from the following three sections refered to above.

### 3.1 About `PacketIn` Section

Proposal 1

: Add `Switch getSwitch()` method to class `PacketIn`.

Proof 1

: In many cases, users need to map the MAC address to an unique inport. We have had `Port getIngressPort()` to get an inport, but it is just a port number and doesn't include any information about switch. We MUST have an interface to get the id of the switch.

    Example: xxx.

<!-- End of Proposal -->

Proposal 2

: Add `IpPrefix getSrcIpPrefix()` and `IpPrefix getDstIpPrefix()` methods to class `PacketIn`.

Proof 2

: Some cases will require the L2 information of the packet.

    Example: xxx.

<!-- End of Proposal -->

Proposal 3

: Add `TcpPort getSrcTcpPort()` and `TcpPort getDstTcpPort()` methods to class `PacketIn`.

Proof 3

: Some cases will require the L3 information of the packet.

    Example: xxx.

<!-- End of Proposal -->

### 3.2 About `Env` Section

### 3.3 About `Route` Section

## 4. Evaluation

## Reference
