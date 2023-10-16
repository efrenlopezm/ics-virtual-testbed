# CPSandbox: A Virtual Testbed for CPS Security Research

CPSandbox is a virtual testbed that aims to provide security researchers with a feature-rich ICS testbed.

## Research Paper

**CPSandbox: A Virtual Testbed for CPS Security Research** 

If you use our work in a scientific publication, please do cite us using this **BibTex** entry:

``` tex
@inproceedings{placeholder,
 author    = {placeholder},
 booktitle = {placeholder},
 title     = {placeholder},
 year      = {placeholder}
}
```

## Quickstart

Based on Mininet and NEFICS, CPSandbox instantiates whichever devices the user specifies within the configuration file used at runtime:

> `python3 -m run_nefics conf/simple_powergrid_iec104.json`

The configuration file is in JSON format and specifies the network topology of the simulation, detailing the switches and devices that Mininet will instantiate. A device configuration directive contains its name and DPID. On the other hand, each device has an identifier, network interfaces associated with any corresponding switches, a launcher configuration that determines the process to run within the device, and the network routes.

*conf/simple_powergrid_iec104.json:*

```
    {
        "switches": [
            {
                "name": "s1",
                "dpid": 1
            }
        ],
        "devices": [
            {
                "name": "hsrc",
                "interfaces": [
                    {
                        "name": "eth0",
                        "mac": "68:1f:d8:6a:7f:81",
                        "ip": "10.0.1.11/24",
                        "switch": "s1"
                    }
                ],
                "launcher": {
                    "module": "simplepowergrid",
                    "device": "Source",
                    "handler": "IEC104DeviceHandler",
                    "guid": 1,
                    "in": [],
                    "out": [2],
                    "parameters": {
                        "voltage": 526315.79
                    }
                },
                "routes": [
                    ["default", "10.0.1.1"]
                ]
            },
            {
                "name": "htx",
                "interfaces": [
                    {
                        "name": "eth0",
                        "mac": "68:1f:d8:de:89:a2",
                        "ip": "10.0.1.12/24",
                        "switch": "s1"
                    }
                ],
                "launcher": {
                    "module": "simplepowergrid",
                    "device": "Transmission",
                    "handler": "IEC104DeviceHandler",
                    "guid": 2,
                    "in": [1],
                    "out": [3],
                    "parameters": {
                        "loads": [0.394737, 0.394737, 0.394737],
                        "state": 7
                    }
                },
                "routes": [
                    ["default", "10.0.1.1"]
                ]
            },
            {
                "name": "hld",
                "interfaces": [
                    {
                        "name": "eth0",
                        "mac": "68:1f:d8:ac:7e:21",
                        "ip": "10.0.1.13/24",
                        "switch": "s1"
                    }
                ],
                "launcher": {
                    "module": "simplepowergrid",
                    "device": "Load",
                    "handler": "IEC104DeviceHandler",
                    "guid": 3,
                    "in": [2],
                    "out": [],
                    "parameters": {
                        "load": 12.5
                    }
                },
                "routes": [
                    ["default", "10.0.1.1"]
                ]
            }
        ]
    }
```

## Getting Started

Coming soon!

## Help

Coming soon!

## License

This project is licensed under the MIT License - see the LICENSE.md file for details

## Acknowledgments

Coming soon!
