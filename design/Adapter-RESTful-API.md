Adapter RESTful API Reference
=======================
Version 0 

See also: [legacy MapleHaskell RESTful API reference.](https://github.com/snlab/MapleGUI/wiki/MapleHaskell-REST-Interface)

Topology
========

| Endpoint | Description |
| -------- | ----------- |
| [GET /v0/topology/:topology-id](#get-v0topologytopology-id) | gets network topology graph data |
| [GET /v0/hostlocations](#get-v0hostlocations) | gets locations of hosts in the network |
| [GET /v0/flows](#get-v0flows-wip) | gets all flows in the network (WIP) |

###GET /v0/topology/:topology-id

Get parameters

| Name | Notes |
| ---- | ---- |
| `:topology-id` | integer or 'default' |

####Example query

````bash
# using HTTPie by jkbrzt
http GET localhost:3000/v0/topology/default
````

Return parameters

| Name | Type |
| ---- | ---- |
| `links` | Link[] |
| `nodes` | Node[] |

Link object parameters

| Name | Type |
| ---- | ---- |
| `linkID` | integer |
| `sourceNode` | integer |
| `sourcePort` | integer |
| `destinationNode` | integer |
| `destinationPort` | integer |

Node object parameters

| Name | Type |
| ---- | ---- |
| `nodeID` | integer |

####Example response

````json

{
    "links": [
        {
            "linkID": 0,
            "sourceNode": 1, 
            "sourcePort": 1, 
            "destinationNode": 2, 
            "destinationPort": 4
        }, 
        ...
    ], 
    "nodes": [
        {
            "nodeID": 1
        }, 
        ...
    ]
}
````

###GET /v0/hostlocations

Host object parameters

| Name | Type |
| ---- | ---- |
| `hostID` | integer |
| `switchID` | integer |
| `port` | integer |

####Example response

````json
[
    {
        "hostID": 4, 
        "switchID": 3
        "port": 1, 
    }, 
    ...
]
````

###GET /v0/flows (WIP)

Flow object parameters

| Name | Type |
| ---- | ---- |
| `egressLocations` | [ { port: integer, switch: integer } ] |
| `ethType` | |
| `flowID` | integer |
| `flowRate` | float |
| `ingressLocation` | { port: integer, switch: integer } |
| `isActive` | boolean |
| `links` |  [ { cap: integer, source: { port: integer, switch: integer }, target: { port: integer, switch: integer } } ] |
| `match` | string |
| `matchRaw` | { contents": [ integer (??), { dstEthAddress: integer, ethFrameType: null, srcEthAddress: integer, vLANID: null, vLANPriority: null}, { dstIPAddress: integer[], dstTransportPort: null, ipTypeOfService: null, matchIPProtocol: null, srcIPAddress: integer[], srcTransportPort: null}], "tag": string } |

####Example response

````json
[
    {
        "egressLocations": [
            {
                "port": 2, 
                "switch": 2
            }
        ], 
        "ethType": null, 
        "flowID": 0, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 1, 
            "switch": 2
        }, 
        "isActive": false, 
        "links": [], 
        "match": "<srcEth=00:00:00:00:00:01,dstEth=00:00:00:00:00:02>", 
        "matchRaw": {
            "contents": [
                1, 
                {
                    "dstEthAddress": 2, 
                    "ethFrameType": null, 
                    "srcEthAddress": 1, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 1, 
                "switch": 2
            }
        ], 
        "ethType": null, 
        "flowID": 1, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 2, 
            "switch": 2
        }, 
        "isActive": false, 
        "links": [], 
        "match": "<srcEth=00:00:00:00:00:02,dstEth=00:00:00:00:00:01>", 
        "matchRaw": {
            "contents": [
                2, 
                {
                    "dstEthAddress": 1, 
                    "ethFrameType": null, 
                    "srcEthAddress": 2, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 1, 
                "switch": 3
            }
        ], 
        "ethType": null, 
        "flowID": 2, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 1, 
            "switch": 2
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 2
                }, 
                "target": {
                    "port": 1, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 2, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 3
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:01,dstEth=00:00:00:00:00:03>", 
        "matchRaw": {
            "contents": [
                1, 
                {
                    "dstEthAddress": 3, 
                    "ethFrameType": null, 
                    "srcEthAddress": 1, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 1, 
                "switch": 2
            }
        ], 
        "ethType": null, 
        "flowID": 3, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 1, 
            "switch": 3
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 3
                }, 
                "target": {
                    "port": 2, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 1, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 2
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:03,dstEth=00:00:00:00:00:01>", 
        "matchRaw": {
            "contents": [
                1, 
                {
                    "dstEthAddress": 1, 
                    "ethFrameType": null, 
                    "srcEthAddress": 3, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 2, 
                "switch": 3
            }
        ], 
        "ethType": null, 
        "flowID": 4, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 1, 
            "switch": 2
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 2
                }, 
                "target": {
                    "port": 1, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 2, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 3
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:01,dstEth=00:00:00:00:00:04>", 
        "matchRaw": {
            "contents": [
                1, 
                {
                    "dstEthAddress": 4, 
                    "ethFrameType": null, 
                    "srcEthAddress": 1, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 1, 
                "switch": 2
            }
        ], 
        "ethType": null, 
        "flowID": 5, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 2, 
            "switch": 3
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 3
                }, 
                "target": {
                    "port": 2, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 1, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 2
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:04,dstEth=00:00:00:00:00:01>", 
        "matchRaw": {
            "contents": [
                2, 
                {
                    "dstEthAddress": 1, 
                    "ethFrameType": null, 
                    "srcEthAddress": 4, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 1, 
                "switch": 3
            }
        ], 
        "ethType": null, 
        "flowID": 6, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 2, 
            "switch": 2
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 2
                }, 
                "target": {
                    "port": 1, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 2, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 3
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:02,dstEth=00:00:00:00:00:03>", 
        "matchRaw": {
            "contents": [
                2, 
                {
                    "dstEthAddress": 3, 
                    "ethFrameType": null, 
                    "srcEthAddress": 2, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 2, 
                "switch": 2
            }
        ], 
        "ethType": null, 
        "flowID": 7, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 1, 
            "switch": 3
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 3
                }, 
                "target": {
                    "port": 2, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 1, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 2
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:03,dstEth=00:00:00:00:00:02>", 
        "matchRaw": {
            "contents": [
                1, 
                {
                    "dstEthAddress": 2, 
                    "ethFrameType": null, 
                    "srcEthAddress": 3, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 2, 
                "switch": 3
            }
        ], 
        "ethType": null, 
        "flowID": 8, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 2, 
            "switch": 2
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 2
                }, 
                "target": {
                    "port": 1, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 2, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 3
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:02,dstEth=00:00:00:00:00:04>", 
        "matchRaw": {
            "contents": [
                2, 
                {
                    "dstEthAddress": 4, 
                    "ethFrameType": null, 
                    "srcEthAddress": 2, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 2, 
                "switch": 2
            }
        ], 
        "ethType": null, 
        "flowID": 9, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 2, 
            "switch": 3
        }, 
        "isActive": false, 
        "links": [
            {
                "cap": 1250000000, 
                "source": {
                    "port": 3, 
                    "switch": 3
                }, 
                "target": {
                    "port": 2, 
                    "switch": 1
                }
            }, 
            {
                "cap": 1250000000, 
                "source": {
                    "port": 1, 
                    "switch": 1
                }, 
                "target": {
                    "port": 3, 
                    "switch": 2
                }
            }
        ], 
        "match": "<srcEth=00:00:00:00:00:04,dstEth=00:00:00:00:00:02>", 
        "matchRaw": {
            "contents": [
                2, 
                {
                    "dstEthAddress": 2, 
                    "ethFrameType": null, 
                    "srcEthAddress": 4, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 2, 
                "switch": 3
            }
        ], 
        "ethType": null, 
        "flowID": 10, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 1, 
            "switch": 3
        }, 
        "isActive": false, 
        "links": [], 
        "match": "<srcEth=00:00:00:00:00:03,dstEth=00:00:00:00:00:04>", 
        "matchRaw": {
            "contents": [
                1, 
                {
                    "dstEthAddress": 4, 
                    "ethFrameType": null, 
                    "srcEthAddress": 3, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }, 
    {
        "egressLocations": [
            {
                "port": 1, 
                "switch": 3
            }
        ], 
        "ethType": null, 
        "flowID": 11, 
        "flowRate": 0.0, 
        "ingressLocation": {
            "port": 2, 
            "switch": 3
        }, 
        "isActive": false, 
        "links": [], 
        "match": "<srcEth=00:00:00:00:00:04,dstEth=00:00:00:00:00:03>", 
        "matchRaw": {
            "contents": [
                2, 
                {
                    "dstEthAddress": 3, 
                    "ethFrameType": null, 
                    "srcEthAddress": 4, 
                    "vLANID": null, 
                    "vLANPriority": null
                }, 
                {
                    "dstIPAddress": [
                        0, 
                        0
                    ], 
                    "dstTransportPort": null, 
                    "ipTypeOfService": null, 
                    "matchIPProtocol": null, 
                    "srcIPAddress": [
                        0, 
                        0
                    ], 
                    "srcTransportPort": null
                }
            ], 
            "tag": "Match"
        }
    }
]
````

FIB
====

| Endpoint | Description |
| -------- | ----------- |
| [GET /v0/fib](#get-v0fib) | gets list of FIB rules |

###GET /v0/fib

Fib object parameters

| Name | Type |
| ---- | ---- |
| `inPort` | integer |
| `match` | string |
| `outPorts` | [{Left: integer, Right: {contents:[], tag:string}}] ?? |
| `priority` | integer |
| `switch` | integer |

####Example response

````json
[
    {
        "inPort": 4, 
        "match": "<dstEth=00:00:00:00:00:09>", 
        "outPorts": [
            {
                "Right": {
                    "contents": [], 
                    "tag": "StripVLAN"
                }
            }, 
            {
                "Left": 3
            }
        ], 
        "priority": 0, 
        "switch": 4
    },
    ...
]
````

Ports
=====

| Endpoint | Description |
| -------- | ----------- |
| [GET /v0/ports](#get-v0ports) | gets list of ports |

###GET /v0/ports

Port object parameters

| Name | Type | Notes |
| ---- | ---- | ----- |
| `capacity` | integer ||  
| `number` | integer | port number |
| `address` | string | Mac address of port |
| `config` | string[] | |
| `name` | string ||
| `state` | string[] | |
| `portUtil` | float ||
| `rxkbps` | float ||
| `txkbps` | float ||
| `switch` | integer ||

####Example response

````json
[ 
    {
        "capacity": 10000, 
        "number": 1, 
        "address": "2e:34:d8:40:48:d5", 
        "config": "[]", 
        "name": "s3-eth1", 
        "state": [ "up" ], 
        "portUtil": 1.3860492587246415e-08, 
        "rxkbps": 0.0, 
        "switch": 3, 
        "txkbps": 0.13535637292232827
    }, 
    ...
]
````

TT
=====

| Endpoint | Description |
| -------- | ----------- |
| [GET /v0/tt](#get-v0tt) | gets trace tree structure |

###GET /v0/tt

Return parameters

####Example response

| Name | Type | Notes |
| ---- | ---- | ----- |
| `tt-nodes` | TTNode[] ||  
| `tt-links` | TTLink[] ||

####TTNode parameters
| Name | Type | Notes |
| ---- | ---- | ----- |
| `id` | integer ||
| `type` | string | The label describing the predicate/action |

####TTLink parameters
| Name | Type | Notes |
| ---- | ---- | ---- |
| `id` | integer | |
| `predicateID` | integer | id of "from" node |
| `operator` | string | label describing the operation (EG: "==", "!=", ">", "<", "else") |
| `condition` | Object | the result to apply the operator against; or null if the predicate node is a T node |
| `destinationID` | integer | id of "to" node |

####Example response

````json
{
    "tt-nodes": [
        {
            "id": 0,
            "type": "srcMac",
        }, 
        {
            "id": 1,
            "type": "dstMac",
        },
        {
            "id": 2,
            "type": "drop",
        }
        ...
    ],
    "tt-links": [
        {
            "id": 0,
            "predicateID": 0,
            "operator": "==",
            "condition": 1, 
            "destinationID": 1, 
        },
        {
            "id": 1,
            "predicateID": 1,
            "operator": "!=",
            "condition": 1, 
            "destinationID": 2, 
        },
        ...
    ], 
}
````
