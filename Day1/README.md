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
![Hypervisor Architecture](HypervisorHighLevelArchitecture.png)

## High Level Architecture of Docker

## What is Docker Local Registry?

## What is Docker Remote Registry?

## What is Docker Private Registry?

## What is a Container Runtime?
- container Runtime is the software that manages containers
  - creating a container
  - listing a container
  - deleting a container
  - start a container
  - restarting a container
  - stopping a container
- end-users like us doesn't use Container Runtimes directly
- Container Runtimes are used by Container Engines to manage containers
- Example
  - runC is a Container Runtime
  - CRI-O is a Container Runtime
 
## What is a Container Engine?
- Container Runtimes are low-level tools
- Container Runtimes are used by Container Engine
- is a high-level user-friendly tool that allows to create containers and manage them without knowing any container technology internals
- Container Engines provide user-friendly commands to manage images and containers
- Examples
  - Docker is a Container Engine that uses runC Container Runtime
  - Podman is a Container Engine that used CRI-O Container Runtime

# Docker Commands

## Docker Overview
- Docker is developed in Go Programming Language by Docker Inc organization
- Docker comes in 2 flavours
  1. Community Edition (CE) - No official support (Good for opensource projects and learning purpose)
  2. Enterprise Edition (EE) - For commercial use (Comes with Support from Docker Inc)

## ⛹️‍♂️ Lab - Listing Docker Images from Local Docker Registry
```
docker images
```

## ⛹️‍♂️ Lab - Finding more details about your docker setup
```
docker info
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker info</b>
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Docker Buildx (Docker Inc., v0.9.1-docker)
  compose: Docker Compose (Docker Inc., v2.12.2)
  scan: Docker Scan (Docker Inc., v0.21.0)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 20.10.21
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runtime.v1.linux runc io.containerd.runc.v2
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c90a442489720eec95342e1789ee8a5e1b9536f
 runc version: v1.1.4-0-g5fd4c4d
 init version: de40ad0
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.15.0-52-generic
 Operating System: Ubuntu 20.04.3 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 4.072GiB
 Name: tektutor.org
 ID: PIAH:5RHX:IQ5Q:W35O:7SDD:J6CI:X33T:HKLS:MCFW:LOYC:NYOJ:6EXS
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
</pre>

## ⛹️‍♂️ Lab - Downloading Docker Image from Docker Remote Registry (Docker Hub website) to Docker Local Registry
```
docker pull hello-world:latest
```

## ⛹️‍♂️ Lab - Finding more details about an image
```
docker image inspect hello-world:latest
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker image inspect hello-world:latest</b>
[
    {
        "Id": "sha256:feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412",
        "RepoTags": [
            "hello-world:latest"
        ],
        "RepoDigests": [
            "hello-world@sha256:e18f0a777aefabe047a671ab3ec3eed05414477c951ab1a6f352a06974245fe7"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2021-09-23T23:47:57.442225064Z",
        "Container": "8746661ca3c2f215da94e6d3f7dfdcafaff5ec0b21c9aff6af3dc379a82fbc72",
        "ContainerConfig": {
            "Hostname": "8746661ca3c2",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"/hello\"]"
            ],
            "Image": "sha256:b9935d4e8431fb1a7f0989304ec86b3329a99a25f5efdc7f09f3f8c41434ca6d",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "20.10.7",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/hello"
            ],
            "Image": "sha256:b9935d4e8431fb1a7f0989304ec86b3329a99a25f5efdc7f09f3f8c41434ca6d",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 13256,
        "VirtualSize": 13256,
        "GraphDriver": {
            "Data": {
                "MergedDir": "/var/lib/docker/overlay2/00b84eed1addd323d784c90f968848158bf3e8275cc0b0dc6de2970dcc98b964/merged",
                "UpperDir": "/var/lib/docker/overlay2/00b84eed1addd323d784c90f968848158bf3e8275cc0b0dc6de2970dcc98b964/diff",
                "WorkDir": "/var/lib/docker/overlay2/00b84eed1addd323d784c90f968848158bf3e8275cc0b0dc6de2970dcc98b964/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:e07ee1baac5fae6a26f30cabfe54a36d3402f96afda318fe0a96cec4ca393359"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
</pre>

## ⛹️‍♂️ Lab - Creating a container and running the container
```
docker run hello-world:latest
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker run hello-world:latest</b>

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
</pre>


## ⛹️‍♂️ Lab - Creating an ubuntu container
```
docker run -dit --name c1 --hostname c1 ubuntu:16.04 /bin/bash
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ docker run -dit --name c1 --hostname c1 ubuntu:16.04 /bin/bash
Unable to find image 'ubuntu:16.04' locally
16.04: Pulling from library/ubuntu
58690f9b18fc: Pull complete 
b51569e7c507: Pull complete 
da8ef40b9eca: Pull complete 
fb15d46c38dc: Pull complete 
Digest: sha256:1f1a2d56de1d604801a9671f301190704c25d604a416f59e03c04f5c6ffee0d6
Status: Downloaded newer image for ubuntu:16.04
eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd
</pre>

## ⛹️‍♂️ Lab - Listing the currently running containers
```
docker ps
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker ps</b>
CONTAINER ID   IMAGE          COMMAND       CREATED              STATUS              PORTS     NAMES
eecfa4ad6752   ubuntu:16.04   "/bin/bash"   About a minute ago   Up About a minute             c1
</pre>

## ⛹️‍♂️ Lab - Finding more details about the container
```
docker inspect c1
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker inspect c1</b>
[
    {
        "Id": "eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd",
        "Created": "2022-10-31T10:56:43.994465442Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 6466,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2022-10-31T10:56:44.779031657Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:b6f50765242581c887ff1acc2511fa2d885c52d8fb3ac8c4bba131fd86567f2e",
        "ResolvConfPath": "/var/lib/docker/containers/eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd/hostname",
        "HostsPath": "/var/lib/docker/containers/eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd/hosts",
        "LogPath": "/var/lib/docker/containers/eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd/eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd-json.log",
        "Name": "/c1",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/a647af5db11f9868b74e90265b5d8ff77028bf143496c247e65b1cdaecceb543-init/diff:/var/lib/docker/overlay2/8577c7c75e49c6d5fadd912ae32411a984ac3ae1059d84406ca250d3c6aa001c/diff:/var/lib/docker/overlay2/532b3f8e47057e1c9ad415479e200102e6d3099cf95cb5bc7862dd4568377738/diff:/var/lib/docker/overlay2/c874c623654d00d8574e68d99e7c5b6dbd5f13acbc32622a34c955797718b878/diff:/var/lib/docker/overlay2/f24ce5398abe32b4a475fae91b691269ebffae597d66a58759ebdf73e6c2fb6a/diff",
                "MergedDir": "/var/lib/docker/overlay2/a647af5db11f9868b74e90265b5d8ff77028bf143496c247e65b1cdaecceb543/merged",
                "UpperDir": "/var/lib/docker/overlay2/a647af5db11f9868b74e90265b5d8ff77028bf143496c247e65b1cdaecceb543/diff",
                "WorkDir": "/var/lib/docker/overlay2/a647af5db11f9868b74e90265b5d8ff77028bf143496c247e65b1cdaecceb543/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "c1",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "ubuntu:16.04",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "70eb1099bd5066bfacfeb21483b16df931cdb8b72189eade3ddd0f4cf88f9856",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/70eb1099bd50",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "b99ae8444e9830d8b308a5d2a2cc0006ed64287fbc8ed97de04a38d71b6e50d5",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "0b9dccdc3ff5354b71458bc221f002bdd753b97e18f5f59944e7c479a9288de9",
                    "EndpointID": "b99ae8444e9830d8b308a5d2a2cc0006ed64287fbc8ed97de04a38d71b6e50d5",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
</pre>

## ⛹️‍♂️ Lab - Finding the IP Address of a running container
```
docker inspect c1 | grep IPA
docker inspect -f {{.NetworkSettings.IPAddress}} c1
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker inspect c1 | grep IPA</b>
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.2",
jegan@tektutor.org:~/Desktop$ <b>docker inspect -f {{.NetworkSettings.IPAddress}} c1</b>
172.17.0.2
</pre>

## ⛹️‍♂️ Lab - Finding the Mac Address of the running container
```
docker inspect -f {{.NetworkSettings.MacAddress}} c1
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker inspect -f {{.NetworkSettings.MacAddress}} c1</b>
02:42:ac:11:00:02
</pre>

## ⛹️‍♂️ Lab - Stopping a running container
```
docker ps
docker stop c1
docker ps 
docker ps -a
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker ps</b>
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS          PORTS     NAMES
eecfa4ad6752   ubuntu:16.04   "/bin/bash"   12 minutes ago   Up 12 minutes             c1
jegan@tektutor.org:~/Desktop$ <b>docker stop c1</b>
c1
jegan@tektutor.org:~/Desktop$ <b>docker ps</b>
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
jegan@tektutor.org:~/Desktop$ <b>docker ps -a</b>
CONTAINER ID   IMAGE                COMMAND       CREATED          STATUS                      PORTS     NAMES
eecfa4ad6752   ubuntu:16.04         "/bin/bash"   12 minutes ago   Exited (0) 4 seconds ago              c1
578ea075c2d4   hello-world:latest   "/hello"      25 minutes ago   Exited (0) 25 minutes ago             hello-container1
</pre>


## ⛹️‍♂️ Lab - Starting an exited container
```
docker ps -a
docker start c1
docker ps
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker ps -a</b>
CONTAINER ID   IMAGE                COMMAND       CREATED          STATUS                      PORTS     NAMES
eecfa4ad6752   ubuntu:16.04         "/bin/bash"   12 minutes ago   Exited (0) 4 seconds ago              c1
578ea075c2d4   hello-world:latest   "/hello"      25 minutes ago   Exited (0) 25 minutes ago             hello-container1
jegan@tektutor.org:~/Desktop$ <b>docker start c1</b>
c1
jegan@tektutor.org:~/Desktop$ <b>docker ps</b>
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS        PORTS     NAMES
eecfa4ad6752   ubuntu:16.04   "/bin/bash"   15 minutes ago   Up 1 second             c1
</pre>

## ⛹️‍♂️ Lab - Restarting a running container
```
docker restart c1
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$<b>docker ps</b>
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS        PORTS     NAMES
eecfa4ad6752   ubuntu:16.04   "/bin/bash"   15 minutes ago   Up 1 second             c1
jegan@tektutor.org:~/Desktop$ <b>docker restart c1</b>
c1
jegan@tektutor.org:~/Desktop$ <b>docker ps</b>
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS         PORTS     NAMES
eecfa4ad6752   ubuntu:16.04   "/bin/bash"   17 minutes ago   Up 3 seconds             c1
</pre>

## ⛹️‍♂️ Lab - Deleting a running container gracefully
We need to stop the container before deleting it.

```
docker stop c1
docker rm c1
```

Expected output
<pre>
jegan@tektutor.org:~/Desktop$ <b>docker ps</b>
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS              PORTS     NAMES
eecfa4ad6752   ubuntu:16.04   "/bin/bash"   19 minutes ago   Up About a minute             c1
jegan@tektutor.org:~/Desktop$ <b>docker rm c1</b>
Error response from daemon: You cannot remove a running container eecfa4ad6752f8177314d2c244b1609fd6bfe09a8679c9a1d967ab313034f0bd. Stop the container before attempting removal or force remove
jegan@tektutor.org:~/Desktop$ <b>docker stop c1</b>
c1
jegan@tektutor.org:~/Desktop$ <b>docker rm c1</b>
c1
jegan@tektutor.org:~/Desktop$ <b>docker ps</b>
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
jegan@tektutor.org:~/Desktop$ <b>docker ps -a</b>
CONTAINER ID   IMAGE                COMMAND    CREATED          STATUS                      PORTS     NAMES
578ea075c2d4   hello-world:latest   "/hello"   31 minutes ago   Exited (0) 31 minutes ago             hello-container1
</pre>
