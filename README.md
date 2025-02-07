# udpgen [![CircleCI](https://circleci.com/gh/OpenNMS/udpgen.svg?style=svg)](https://circleci.com/gh/OpenNMS/udpgen)

## Overview

This tool was written to help stress test OpenNMS' UDP protocol hanlding by generating large volumes of traffic.

It currently supports generating:
* SNMP Traps
* Syslog Messages
* Netflow 5 flows
* Netflow 9 flows

The tool does not currently give fine grained control over the payload generation.

## Building

### Requirements

* cmake
* netsnmp-devel

### Compiling

```sh
mkdir build
cd build
cmake ..
make
```

## Usage

### Generate Syslog Message

Generate 100000 Syslog messages per second over 10 threads, targeted at 172.23.1.1:514.

```sh
./udpgen -r 100000 -t 10 -h 172.23.1.1 -p 514
```

Pin `udpgen` to the first core, and generate as many Syslog messages as possible using a single thread.
```sh
taskset -c 0 ./udpgen -r 0
```

### Generate SNMP Traps

Generate 200000 SNMPv2 traps per second over 8 threads, targeted at 127.0.0.1:1162.

```sh
./udpgen -x snmp -r 200000 -t 8
```

### Generate Netflow 9 flows

Generate as many Netflow 9 flows as possible using a single thread pinned to the first core:

```sh
taskset -c 0 ./udpgen -x netflow9 -r 0
```

