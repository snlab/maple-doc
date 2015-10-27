Topology
========

| Endpoint | Description |
| -------- | ----------- |
| [GET /topology](#get-topology) | gets network topology graph data |
| [GET /hostlocations](#get-hostlocations) | gets locations of hosts in the network |
| [GET /flows](#get-flows) | gets all flows in the network (WIP) |

###GET /topology/<topology-id>

Parameters

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

###GET /hostlocations

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

###GET /flows (WIP)

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
| [GET /fib](#get-fib) | gets list of FIB rules |

FIB
====

###GET /fib

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
| [GET /ports](#get-ports) | gets list of ports |

###GET /ports

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
