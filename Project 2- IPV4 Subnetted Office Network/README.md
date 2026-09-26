 # IPv4 Subnetted Office Network

## Project Overview

This project demonstrates the design and implementation of a subnetted IPv4 office network using Cisco Packet Tracer.

A single private IPv4 network, `192.168.10.0/24`, was divided into two smaller `/26` subnets. Each subnet represents a separate department and is connected to a different router interface.

The project demonstrates practical IPv4 subnetting, router configuration, host addressing, default gateways, and connectivity testing between different subnets.

## Objectives

- Divide a `/24` IPv4 network into smaller `/26` subnets.
- Calculate network addresses, usable host ranges, and broadcast addresses.
- Configure two different IPv4 subnets on a Cisco router.
- Configure PCs with appropriate IPv4 addresses and subnet masks.
- Configure default gateways for each subnet.
- Verify router interface status.
- Test communication within each subnet.
- Test communication between different subnets.
- Document the complete network configuration and results.

## Network Topology

The network consists of:

- 1 Cisco 1941 Router
- 2 Cisco 2960 Switches
- 4 PCs
- Ethernet connections

Topology:

```text
                 Router0
                /       \
             G0/0       G0/1
              /           \
         Switch0         Switch1
         /    \           /    \
       PC0    PC1       PC2    PC3
     Dept A             Dept B
```

Department A is connected to Router0 GigabitEthernet0/0.

Department B is connected to Router0 GigabitEthernet0/1.

## Subnetting Design

The original network was:

`192.168.10.0/24`

The `/24` network was divided into two `/26` subnets.

### `/26` Subnet Calculation

A `/26` prefix uses 26 network bits and leaves 6 host bits.

Number of addresses:

`2^6 = 64`

Usable host addresses:

`64 - 2 = 62`

Subnet mask:

`255.255.255.192`

Block size:

`256 - 192 = 64`

Therefore, the `/26` subnet boundaries occur every 64 addresses.

## Subnet 1 — Department A

Network:

`192.168.10.0/26`

Subnet mask:

`255.255.255.192`

Usable host range:

`192.168.10.1 - 192.168.10.62`

Broadcast address:

`192.168.10.63`

Default gateway:

`192.168.10.1`

## Subnet 2 — Department B

Network:

`192.168.10.64/26`

Subnet mask:

`255.255.255.192`

Usable host range:

`192.168.10.65 - 192.168.10.126`

Broadcast address:

`192.168.10.127`

Default gateway:

`192.168.10.65`

## IP Addressing Plan

| Device | Interface | IPv4 Address | Subnet Mask | Default Gateway | Subnet |
|---|---|---|---|---|---|
| Router0 | G0/0 | 192.168.10.1 | 255.255.255.192 | N/A | 192.168.10.0/26 |
| PC0 | NIC | 192.168.10.10 | 255.255.255.192 | 192.168.10.1 | 192.168.10.0/26 |
| PC1 | NIC | 192.168.10.20 | 255.255.255.192 | 192.168.10.1 | 192.168.10.0/26 |
| Router0 | G0/1 | 192.168.10.65 | 255.255.255.192 | N/A | 192.168.10.64/26 |
| PC2 | NIC | 192.168.10.70 | 255.255.255.192 | 192.168.10.65 | 192.168.10.64/26 |
| PC3 | NIC | 192.168.10.80 | 255.255.255.192 | 192.168.10.65 | 192.168.10.64/26 |

## Router Configuration

Router0 GigabitEthernet0/0 was configured as the gateway for Department A.

```text
interface gigabitEthernet 0/0
ip address 192.168.10.1 255.255.255.192
no shutdown
```

Router0 GigabitEthernet0/1 was configured as the gateway for Department B.

```text
interface gigabitEthernet 0/1
ip address 192.168.10.65 255.255.255.192
no shutdown
```

Both router interfaces were verified using:

```text
show ip interface brief
```

The interfaces were confirmed to be operational with an `up/up` status.

## PC Configuration

### PC0

- IPv4 Address: `192.168.10.10`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `192.168.10.1`

### PC1

- IPv4 Address: `192.168.10.20`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `192.168.10.1`

### PC2

- IPv4 Address: `192.168.10.70`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `192.168.10.65`

### PC3

- IPv4 Address: `192.168.10.80`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `192.168.10.65`

## Connectivity Testing

Connectivity was tested using the `ping` command.

### Department A Testing

PC0 successfully communicated with PC1:

```text
ping 192.168.10.20
```

PC0 also successfully reached its default gateway:

```text
ping 192.168.10.1
```

### Department B Testing

PC2 successfully communicated with PC3:

```text
ping 192.168.10.80
```

PC2 also successfully reached its default gateway:

```text
ping 192.168.10.65
```

### Inter-Subnet Testing

Communication between the two different `/26` subnets was also tested.

From PC0:

```text
ping 192.168.10.70
```

and:

```text
ping 192.168.10.80
```

The tests were successful, demonstrating communication between:

`192.168.10.0/26`

and:

`192.168.10.64/26`

through Router0.

## Results

The subnetted office network was successfully implemented.

The original `192.168.10.0/24` network was divided into two `/26` subnets. Each department was assigned its own subnet, gateway, and host addresses.

All configured devices successfully communicated within their respective subnets, and communication between the two subnets was successfully verified through the router.

The router interfaces were also verified as `up/up`.

## Skills Demonstrated

- IPv4 subnetting
- CIDR notation
- `/24` to `/26` subnetting
- Subnet mask calculation
- Block size calculation
- Network address identification
- Broadcast address identification
- Usable host range calculation
- IPv4 addressing
- Default gateway configuration
- Cisco router interface configuration
- Router-based inter-subnet communication
- Connectivity testing
- Network documentation
- Cisco Packet Tracer

## Tools Used

- Cisco Packet Tracer
- Cisco 1941 Router
- Cisco 2960 Switches
- Packet Tracer PCs

## Project Evidence

The `Screenshots` folder contains nine screenshots documenting the project, including:

- PC0 IPv4 configuration
- PC1 IPv4 configuration
- PC2 IPv4 configuration
- PC3 IPv4 configuration
- Router interface verification
- Successful Department A connectivity tests
- Successful Department B connectivity tests
- Successful inter-subnet connectivity tests
- Final network topology

## Conclusion

This project demonstrates how a larger IPv4 network can be divided into smaller logical networks using subnetting.

By converting the original `192.168.10.0/24` network into two `/26` subnets, separate address spaces were created for two departments. The router was configured with a gateway interface for each subnet, while the PCs were assigned addresses from their appropriate ranges.

Successful connectivity testing confirmed that the subnetting and router configuration were functioning correctly.

This project strengthened practical understanding of IPv4 subnetting, addressing, routing between subnets, and network verification using Cisco Packet Tracer.
