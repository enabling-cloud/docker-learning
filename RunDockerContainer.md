[Home](README.md)

# Running Docker Containers

Run the following commands in PowerShell

-------------------------------
**docker images**  command
```Powershell
PS C:\WINDOWS\system32> docker images
REPOSITORY                                 TAG                 IMAGE ID            CREATED             SIZE
 
PS C:\WINDOWS\system32>

```
No image in local repo

Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/images/) for more detail.

-------------------------------

**docker run**  command
```Powershell
PS C:\WINDOWS\system32> docker run busybox:1.30 echo "hello world"
Unable to find image 'busybox:1.30' locally
1.30: Pulling from library/busybox
57c14dd66db0: Pull complete
Digest: sha256:7964ad52e396a6e045c39b5a44438424ac52e12e4d5a25d94895f2058cb863a0
Status: Downloaded newer image for busybox:1.30
hello world
PS C:\WINDOWS\system32>

```
Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/run/) for more detail.

Image downloaded in local repo

```Powershell
PS C:\WINDOWS\system32> docker images
REPOSITORY                                 TAG                 IMAGE ID            CREATED             SIZE
busybox                                    1.30                3a093384ac30        4 weeks ago         1.2MB
 
PS C:\WINDOWS\system32>

```
-------------------------------

Docker run with image cached.

```Powershell
PS C:\WINDOWS\system32> docker run busybox:1.30 echo "hello world"
hello world
PS C:\WINDOWS\system32>

```
-------------------------------

**docker run** interactive command

```Powershell
PS C:\WINDOWS\system32> docker run -it busybox:1.30
/ # ls -la
total 44
drwxr-xr-x    1 root     root          4096 Feb  4 17:47 .
drwxr-xr-x    1 root     root          4096 Feb  4 17:47 ..
-rwxr-xr-x    1 root     root             0 Feb  4 17:47 .dockerenv
drwxr-xr-x    2 root     root         12288 Dec 31 18:16 bin
drwxr-xr-x    5 root     root           360 Feb  4 17:47 dev
drwxr-xr-x    1 root     root          4096 Feb  4 17:47 etc
drwxr-xr-x    2 nobody   nogroup       4096 Dec 31 18:16 home
dr-xr-xr-x  179 root     root             0 Feb  4 17:47 proc
drwx------    1 root     root          4096 Feb  4 17:47 root
dr-xr-xr-x   13 root     root             0 Feb  4 17:47 sys
drwxrwxrwt    2 root     root          4096 Dec 31 18:16 tmp
drwxr-xr-x    3 root     root          4096 Dec 31 18:16 usr
drwxr-xr-x    4 root     root          4096 Dec 31 18:16 var
/ # exit
PS C:\WINDOWS\system32>

```
-------------------------------

**docker run**  detached mode
```Powershell
PS C:\WINDOWS\system32> docker run -d busybox:1.30 sleep 1000
0d2b336175cb2e3acd6143c7530d26c10c0d2858911a861e03efb054cc534d7b

```
-------------------------------

**docker ps**  command
```Powershell

PS C:\WINDOWS\system32> docker ps
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS              PORTS               NAMES
0d2b336175cb        busybox:1.30                     "sleep 1000"             7 seconds ago       Up 5 seconds                            sad_heisenberg
```

**docker ps** all command

```Powershell
PS C:\WINDOWS\system32> docker ps -a
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS                      PORTS               NAMES
0d2b336175cb        busybox:1.30                     "sleep 1000"             23 seconds ago      Up 22 seconds                                   sad_heisenberg
281b2ea038b1        busybox:1.30                     "sh"                     13 minutes ago      Exited (0) 13 minutes ago                       dreamy_boyd
c97dd43b5c9d        busybox:1.30                     "echo 'hello world'"     15 minutes ago      Exited (0) 15 minutes ago                       ecstatic_heisenberg
ffc142cdefa7        busybox:1.30                     "echo 'hello world'"     20 minutes ago      Exited (0) 20 minutes ago                       romantic_merkle
PS C:\WINDOWS\system32>
```

Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/ps/) for more detail.

-------------------------------

**docker run**  remove container after ran
```Powershell
PS C:\WINDOWS\system32> docker run --rm busybox:1.30 sleep 1
PS C:\WINDOWS\system32> docker ps -a
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS                      PORTS               NAMES
0d2b336175cb        busybox:1.30                     "sleep 1000"             3 minutes ago       Up 3 minutes                                    sad_heisenberg
281b2ea038b1        busybox:1.30                     "sh"                     16 minutes ago      Exited (0) 16 minutes ago                       dreamy_boyd
c97dd43b5c9d        busybox:1.30                     "echo 'hello world'"     18 minutes ago      Exited (0) 18 minutes ago                       ecstatic_heisenberg
ffc142cdefa7        busybox:1.30                     "echo 'hello world'"     23 minutes ago      Exited (0) 23 minutes ago                       romantic_merkle
```

-------------------------------

**docker run**  by name
```Powershell
PS C:\WINDOWS\system32> docker run --name foobar busybox:1.30 echo "Hello"
Hello
PS C:\WINDOWS\system32>
```
-------------------------------

```Powershell
PS C:\WINDOWS\system32> docker ps -a
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS                      PORTS               NAMES
e892e67eae03        busybox:1.30                     "echo Hello"             19 seconds ago      Exited (0) 18 seconds ago                       foobar
0d2b336175cb        busybox:1.30                     "sleep 1000"             7 minutes ago       Up 7 minutes                                    sad_heisenberg
281b2ea038b1        busybox:1.30                     "sh"                     20 minutes ago      Exited (0) 20 minutes ago                       dreamy_boyd
c97dd43b5c9d        busybox:1.30                     "echo 'hello world'"     22 minutes ago      Exited (0) 22 minutes ago                       ecstatic_heisenberg
ffc142cdefa7        busybox:1.30                     "echo 'hello world'"     27 minutes ago      Exited (0) 27 minutes ago                       romantic_merkle
```

-------------------------------

**docker inspect**  example
```Powershell
PS C:\WINDOWS\system32> docker run -d busybox:1.30 sleep 100
027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f
PS C:\WINDOWS\system32>
```

```Powershell
PS C:\WINDOWS\system32> docker inspect 027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f
[
    {
        "Id": "027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f",
        "Created": "2019-02-04T18:10:08.7605589Z",
        "Path": "sleep",
        "Args": [
            "100"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 38020,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2019-02-04T18:10:09.8869349Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:3a093384ac306cbac30b67f1585e12b30ab1a899374dabc3170b9bca246f1444",
        "ResolvConfPath": "/var/lib/docker/containers/027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f/hostname",
        "HostsPath": "/var/lib/docker/containers/027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f/hosts",
        "LogPath": "/var/lib/docker/containers/027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f/027fd61c2d60707c93b2cf89887afb90cf1fda9b1e89a4deb179d4b92aae965f-json.log",
        "Name": "/condescending_thompson",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
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
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "shareable",
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
                44,
                257
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
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": 0,
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
                "LowerDir": "/var/lib/docker/overlay2/6cfd4ce478d40fa6928f73e3bd25ad62c3ca69a31dad97c04a990f255f49fa5c-init/diff:/var/lib/docker/overlay2/66d03ef14c4cd5a2df162aebb982afd63683a4319856efb8b6598eedcf522b1b/diff",
                "MergedDir": "/var/lib/docker/overlay2/6cfd4ce478d40fa6928f73e3bd25ad62c3ca69a31dad97c04a990f255f49fa5c/merged",
                "UpperDir": "/var/lib/docker/overlay2/6cfd4ce478d40fa6928f73e3bd25ad62c3ca69a31dad97c04a990f255f49fa5c/diff",
                "WorkDir": "/var/lib/docker/overlay2/6cfd4ce478d40fa6928f73e3bd25ad62c3ca69a31dad97c04a990f255f49fa5c/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "027fd61c2d60",
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
                "sleep",
                "100"
            ],
            "Image": "busybox:1.30",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "fcb52bfec2d430164e77ab1e58cc853b051662cb3d7008c99f86ad840b5d2841",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/fcb52bfec2d4",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "5e6b297719df41c2e569f3ea5694e3daf6e39eb33fe8f8e991f32952aab0f028",
            "Gateway": "132.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "132.17.0.3",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:03",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "bc33a73de78b04a26e05c0e0cbd458d3323746b23a598f5744805fd270415535",
                    "EndpointID": "5e6b337719df41c2e569f3ea5694e3daf6e39eb33fe8f8e991f32952aab0f028",
                    "Gateway": "132.17.0.1",
                    "IPAddress": "132.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "03:42:ac:11:00:03",
                    "DriverOpts": null
                }
            }
        }
    }
]
PS C:\WINDOWS\system32>
```
Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/inspect/) for more detail.

-------------------------------
**docker exec**  command
Exploring the inside of a running container, This will run bash inside the existing  container.
```Powershell
PS D:\practices\kubernetes\basic> docker exec -it 321b8cadea75135bab739e2a1f447158e4e6053274dd9c1900f7731480dd5d3c bash
```
Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/exec/) for more detail.

-------------------------------
**docker history** command

```Powershell
PS C:\WINDOWS\system32> docker history busybox:1.24
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
47bcc53f74dc        2 years ago         /bin/sh -c #(nop) CMD ["sh"]                    0B
<missing>           2 years ago         /bin/sh -c #(nop) ADD file:47ca6e777c36a4cff…   1.11MB
PS C:\WINDOWS\system32> docker history tomcat:8.5
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
7ee26c09afb3        13 days ago         /bin/sh -c #(nop)  CMD ["catalina.sh" "run"]    0B
<missing>           13 days ago         /bin/sh -c #(nop)  EXPOSE 8080                  0B
<missing>           13 days ago         /bin/sh -c set -e  && nativeLines="$(catalin…   0B
<missing>           13 days ago         /bin/sh -c set -eux;   savedAptMark="$(apt-m…   18.1MB
<missing>           13 days ago         /bin/sh -c #(nop)  ENV TOMCAT_ASC_URLS=https…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV TOMCAT_TGZ_URLS=https…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV TOMCAT_SHA512=be6d6df…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV TOMCAT_VERSION=8.5.37    0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV TOMCAT_MAJOR=8           0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV GPG_KEYS=05AB33110949…   0B
<missing>           13 days ago         /bin/sh -c apt-get update && apt-get install…   1.86MB
<missing>           13 days ago         /bin/sh -c set -ex;  currentVersion="$(dpkg-…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV OPENSSL_VERSION=1.1.0…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV LD_LIBRARY_PATH=/usr/…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV TOMCAT_NATIVE_LIBDIR=…   0B
<missing>           13 days ago         /bin/sh -c #(nop) WORKDIR /usr/local/tomcat     0B
<missing>           13 days ago         /bin/sh -c mkdir -p "$CATALINA_HOME"            0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV PATH=/usr/local/tomca…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV CATALINA_HOME=/usr/lo…   0B
<missing>           13 days ago         /bin/sh -c set -ex;   if [ ! -d /usr/share/m…   309MB
<missing>           13 days ago         /bin/sh -c #(nop)  ENV JAVA_DEBIAN_VERSION=8…   0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV JAVA_VERSION=8u181       0B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV JAVA_HOME=/docker-jav…   0B
<missing>           13 days ago         /bin/sh -c ln -svT "/usr/lib/jvm/java-8-open…   33B
<missing>           13 days ago         /bin/sh -c {   echo '#!/bin/sh';   echo 'set…   87B
<missing>           13 days ago         /bin/sh -c #(nop)  ENV LANG=C.UTF-8             0B
<missing>           13 days ago         /bin/sh -c apt-get update && apt-get install…   2.05MB
<missing>           13 days ago         /bin/sh -c set -ex;  if ! command -v gpg > /…   7.81MB
<missing>           13 days ago         /bin/sh -c apt-get update && apt-get install…   23.2MB
<missing>           13 days ago         /bin/sh -c #(nop)  CMD ["bash"]                 0B
<missing>           13 days ago         /bin/sh -c #(nop) ADD file:feb9fd29475961253…   101MB
PS C:\WINDOWS\system32>

```
Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/history/) for more detail.

-------------------------------


