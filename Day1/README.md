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
- Examples
  - VMWare
    - VMWare Fusion (Virtualization Software that works in Mac OS-X) - Type 2
    - VMWare Workstation ( Virtualization Software that works on Windows/Linux ) - Type 2
    - VMWare vSphere/v-center - Type 1 Hypervisor ( Bare Metal Servers - Servers with no OS )
  - Oracle
    - Virtual Box (Free - works in Windows/Mac/Linux) - Type 2
  - Parallels ( Mac OS-X)
  - Microsoft
    - Hyper-V (Works from Windows 10 Pro onwards )
- this type of Virtualization is called Heavy Weight 
- each Virtual Machine represents one fully function Operating System
- the Operating System has its own dedicated OS Kernel

## Multi Chip Module
- Single Integrated Chip (IC) hosting multiple Processors
- The MCM Chip can be installed in a Single Socket on your Server grade Motherboard
- Let's assume a MCM IC hosting 8 Processors each supporting 128 Cores
  - total cores supported - 8 x 128 x 2 = 2048 cores

## Linux Kernel Features
- Supports two interesting features that enable container technology
  1. Namespace and
     - each container is separated from other containers as they run in a virtual sandbox environment
     - each container gets many namespaces
       - PID namespace
       - Network namespace, etc
  2. Control Group (CGroup)
     - it is through this feature, we can restrict a container hardware resource utilization
     - For instance, we can restrict a container using only 25% of CPU ( if the OS has let's 4 cores, the container can only use 1 core at the max )
 

## What is Containerization?
- is an application virtualization technology
- each container will host one application
- containers are not operating system
- certain container features are similar to Operating System features but still container is a process not an OS
- each container gets its own Virtual Network Card(NIC)
- hence every container gets an IP Address
- each container has a Network Stack (7 OSI layers)
- each container has a file system
- container doesn't not OS Kernel
- each container runs in its namespace

## What are the different Container Tools available?

## Difference between Docker(Containers) and Virtualization

## High Level Architecture of Virtualization(Hypervisor)

## High Level Architecture of Docker

## What is Docker Local Registry?

## What is Docker Remote Registry?

## What is Docker Private Registry?


# Docker Commands

## Listing Docker Images from Local Docker Registry
```
docker images
```


