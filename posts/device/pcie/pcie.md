---
title: "Pcie"
date: 2022-01-24T10:47:51+08:00
draft: true
---

[wiki](https://en.wikipedia.org/wiki/PCI_Express)

# Definition
- PCI Express (Peripheral Component Interconnect Express), officially abbreviated as PCIe or PCI-e,[1] is __a high-speed serial computer expansion bus standard__, designed to replace the older PCI, PCI-X and AGP bus standards. 
- More recent revisions of the PCIe standard provide __hardware support for I/O virtualization__.
- Defined by its number of lanes,[4] (the number of simultaneous sending and receiving lines of data as in a highway which features traffic in both directions) the PCI Express __electrical interface__ is also used in a variety of other standards, most notably the laptop expansion card interface ExpressCard and computer storage interfaces SATA Express, U.2 (SFF-8639) and M.2.


# Architecture
- topology
    - In contrast, PCI Express is based on __point-to-point__ topology, with separate serial links connecting every device to the __root complex (host)__.
    - In contrast, a PCI Express bus link supports full-duplex communication between any two endpoints, with no inherent limitation on concurrent access across multiple endpoints.
- bus protocol
    - PCI Express communication is encapsulated in __packets__. The work of packetizing and de-packetizing data and status-message traffic is handled by the __transaction layer__ of the PCI Express port (described later). 
    - PCI slots and PCI Express slots are not interchangeable
        - Radical differences in electrical signaling and bus protocol require the use of a different mechanical form factor and expansion connectors (and thus, new motherboards and new adapter boards); 
    - backward compatibility
        - At the software level, PCI Express preserves backward compatibility with PCI; legacy PCI system software can detect and configure newer PCI Express devices without explicit support for the PCI Express standard, though new PCI Express features are inaccessible.
- PCI Express link
    - The PCI Express link between two devices can vary in size from one to 16 lanes. In a multi-lane link, the packet data is striped across lanes, and peak data throughput scales with the overall link width. The lane count is automatically negotiated during device initialization, and can be restricted by either endpoint.

## Interconnect
- PCI Express devices communicate via a __logical connection__ called an interconnect[9] or link.
- A link is a __point-to-point communication channel__ between two PCI Express ports allowing both of them to send and receive ordinary PCI __requests__ (configuration, I/O or memory read/write) and __interrupts__ (INTx, MSI or MSI-X).

## Lane
- A lane is composed of __two differential signaling pairs__, with one pair for receiving data and the other for transmitting. Thus, each lane is composed of four wires or signal traces.
- Conceptually, each lane is used as a __full-duplex__ byte stream, transporting data packets in eight-bit "byte" format simultaneously in both directions between endpoints of a link.

## Serial bus
- A serial interface does __not exhibit timing__ skew because there is only one differential signal in each direction within each lane
- and there is __no external clock signal__ since clocking information is embedded within the serial signal itself.
- As such, typical bandwidth limitations on serial signals are in the __multi-gigahertz__ range.
- PCI Express is one example of the __general trend__ toward replacing parallel buses with serial interconnects
- Multichannel serial design increases __flexibility__ with its ability to allocate fewer lanes for slower devices.

# Hardware protocol summary
- PCI Express is a layered protocol, consisting of a transaction layer, a data link layer, and a physical layer.
- The Data Link Layer is subdivided to include a media access control (MAC) sublayer.
- The Physical Layer is subdivided into logical and electrical sublayers.
- The Physical logical-sublayer contains a physical coding sublayer (PCS).

## Physical layer

### Data transmission
- The PCIe Physical Layer (PHY, PCIEPHY, PCI Express PHY, or PCIe PHY) specification is divided into __two__ sub-layers, corresponding to __electrical__ and __logical__ specifications. The logical sublayer is sometimes further divided into a MAC sublayer and a PCS, although this division is not formally part of the PCIe specification.

- At the electrical level, each lane consists of two unidirectional differential pairs operating at 2.5, 5, 8, 16 or 32 Gbit/s, depending on the negotiated capabilities. Transmit and receive are separate differential pairs, for a total of four data wires per lane.

- A connection between any two PCIe devices is known as a link, and is built up from a collection of one or more lanes.

## Data Link Layer

## Transaction layer

# Competing protocols

Other communications standards based on high bandwidth serial architectures include InfiniBand, RapidIO, HyperTransport, Intel QuickPath Interconnect, and the Mobile Industry Processor Interface (MIPI). 

- The differences are based on the trade-offs between flexibility and extensibility vs latency and overhead.

    - flexibility and extensibility ???
        - For example, making the system hot-pluggable, as with Infiniband but not PCI Express, requires that software track network topology changes.
    - latency and overhead
        - Another example is making the packets shorter to decrease latency (as is required if a bus must operate as a memory interface). Smaller packets mean packet headers consume a higher percentage of the packet, thus decreasing the effective bandwidth. Examples of bus protocols designed for this purpose are RapidIO and HyperTransport.

- PCI Express falls somewhere in the middle, targeted by design as a __system interconnect__ (local bus) rather than a device interconnect or routed network protocol. Additionally, its design goal of __software transparency constrains the protocol and raises its latency__ somewhat.

- Cluster interconnect
    - Certain data-center applications (such as large computer clusters) require the use of fiber-optic interconnects due to the __distance limitations__ inherent in copper cabling.
    - Typically, a network-oriented standard such as Ethernet or Fibre Channel suffices for these applications, but in some cases __the overhead introduced by routable protocols__ is undesirable and a lower-level interconnect, such as InfiniBand, RapidIO, or NUMAlink is needed. Local-bus standards such as PCIe and HyperTransport can in principle be used for this purpose,[135] but as of 2015, solutions are only available from niche vendors such as Dolphin ICS.



# TODO 
- non-transparent bridge
    - https://unix.stackexchange.com/questions/552684/direct-pcie-to-pcie-connection-for-communications
- 


https://www.embedded.com/using-pci-express-as-a-fabric-for-interconnect-clustering/


# nvidia
- https://docs.nvidia.com/drive/drive_os_5.1.6.1L/nvvib_docs/index.html#page/DRIVE_OS_Linux_SDK_Development_Guide/System%20Programming/sys_components_non_transparent_bridging.html

- A limitation of the PCI Express (PCIe) architectural model is that it allows only a single root, and that the root and all of the End Points (EP) must share a common address space. In many applications there is a need to interconnect two independent PCI domains. A Non-Transparent Bridge (NTB) enables this inter-domain communication, facilitating communication between devices in different switch partitions. This ability enables both hosts and EPs to initiate transactions to hosts and/or EPs in another switch partition.
- An NTB or NT Interconnection consists of two or more PCI functions each defined by a Type 0 PCI header that are interconnected by a bridging function. The Type 0 PCI functions are referred to as Non-Transparent EPs (NT EP). Each partition can have at most one NT EP.
- The Microsemi’s PM8534 PFX switch on Pegasus board can be used to establish NTB connection which will allow one Root Complex device on board to establish and communicate to another Root Complex device on same board or another Pegasus board.

# NTB Drivers
- https://www.kernel.org/doc/Documentation/ntb.txt
- NTB (Non-Transparent Bridge) is a type of PCI-Express bridge chip that connects
the separate memory systems of two or more computers to the same PCI-Express
fabric. Existing NTB hardware supports a common feature set: doorbell
registers and memory translation windows, as well as non common features like
scratchpad and message registers. Scratchpad registers are read-and-writable
registers that are accessible from either side of the device, so that peers can
exchange a small amount of information at a fixed address. Message registers can
be utilized for the same purpose. Additionally they are provided with with
special status bits to make sure the information isn't rewritten by another
peer. Doorbell registers provide a way for peers to send interrupt events.
Memory windows allow translated read and write access to the peer memory.