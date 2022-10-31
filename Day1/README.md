# Day1

## What is HyperThreading(Intel)/SMT(AMD)?
- Processors that support Hyperthreading/SMT allow each phyical core to execute 2 to 8 threads at the same time
- Hyperthreading is Intel technology
- While SMT(Simulateneous Multi Threading) is AMD's equivalent technology
- Virtualization Softwares they see each Physical core as 2 Virtual Cores
- In modern Processors, each Physical core are seen as 8 Virtual Cores

## What is Hypervisor?
- general term used to refer to the Virtualization Technology
- Virtualization allows us to run many Operating Systems side by side as Guest OS on a single Desktop/Laptop/Server
- many Operating Systems can be active at the same time
- each Virtual Machine aka Guest OS are allocated with dedicated Hardware resources
- Each Virtual Machine will get
  - its own dedicated CPU Cores
  - its own dedicated RAM
  - its own dedicated Storage
  - its own Network Card(Virtual - Software Defined Network Card - NIC)
  - its own Graphics Card(Virtual)
- Assume you have a laptop with 4 Cores(Quad Core Processor), 16 GB RAM and 500 GB Hard Disk
  - in such a laptop/desktop how many maximum Virtual Machine(VMs - Guest OS) we can run in parallel?
- AMD Processor
  - the virtualization feature is called AMD-V
  - this must be enabled on the BIOS
- Intel Processor
  - the virtualization features is called VT-X
  - this must be enabled on the BIOS

## What is Containerization?

## What are the different Container Tools available?

## Difference between Docker(Containers) and Virtualization

## High Level Architecture of Virtualization(Hypervisor)

## High Level Architecture of Docker

## What is Docker Local Registry?

## What is Docker Remote Registry?

## What is Docker Private Registry?

