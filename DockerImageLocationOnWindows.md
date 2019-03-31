[Home](README.md)


![](resources/hyperv-connect-.png)

Run `docker info`

Output of `docker info`

```Powershell
D:\>docker info
Containers: 10
 Running: 2
 Paused: 0
 Stopped: 8
Images: 10
Server Version: 18.09.2
Storage Driver: overlay2
 Backing Filesystem: extfs
 Supports d_type: true
 Native Overlay Diff: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host macvlan null overlay
 Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 9754871865f7fe2f4e74d43e2fc7ccd237edcbce
runc version: 09c8266bf2fcf9519a651b04ae54c967b9ab86ec
init version: fec3683
Security Options:
 seccomp
  Profile: default
Kernel Version: 4.9.125-linuxkit
Operating System: Docker for Windows
OSType: linux
Architecture: x86_64
CPUs: 2
Total Memory: 1.934GiB
Name: linuxkit-00155d862114
ID: 57SA:YP4G:XIQK:72V6:GKJW:MR5Z:UHQB:MIHZ:TQ4N:ZRRZ:XPI4:HFAW
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): true
 File Descriptors: 39
 Goroutines: 78
 System Time: 2019-03-31T10:10:07.4109792Z
 EventsListeners: 1
Registry: https://index.docker.io/v1/
Labels:
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false
Product License: Community Engine
D:\>
```

Observe `Docker Root Dir: /var/lib/docker`, however `/var/lib/docker` does not exist in Windows, 

In Windows Docker runs in VM (MobiLinuxVM), refer [this](ConnectIntoDockerVMOnWindows.md) if you want to explore the VM.

```Powershell
/var/lib/docker # ls
builder  buildkit  containerd  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes
/var/lib/docker # cd image//overlay2/
/var/lib/docker/image/overlay2 # ls
distribution  imagedb  layerdb  repositories.json
/var/lib/docker/image/overlay2 #
```

Docker images

```Powershell
/var/lib/docker/image/overlay2 # cat repositories.json | python -mjson.tool
{
    "Repositories": {
        "alpine": {
            "alpine:latest": "sha256:5cb3aa00f89934411ffba5c063a9bc98ace875d8f92e77d0029543d9f2ef4ad0",
            "alpine@sha256:644fcb1a676b5165371437feaa922943aaf7afcfa8bfee4472f6860aad1ef2a0": "sha256:5cb3aa00f89934411ffba5c063a9bc98ace875d8f92e77d0029543d9f2ef4ad0"
        },
        "busybox": {
            "busybox:latest": "sha256:d8233ab899d419c58cf3634c0df54ff5d8acc28f8173f09c21df4a07229e1205",
            "busybox@sha256:061ca9704a714ee3e8b80523ec720c64f6209ad3f97c0ff7cb9ec7d19f15149f": "sha256:d8233ab899d419c58cf3634c0df54ff5d8acc28f8173f09c21df4a07229e1205"
        },
        "container-registry.oracle.com/database/enterprise": {
            "container-registry.oracle.com/database/enterprise:12.2.0.1": "sha256:12a359cd052828523d9e7479673c26c4c9c23cc628d7a4e7210ea7deae4994d7",
            "container-registry.oracle.com/database/enterprise@sha256:1f700299f7a96c5ffcdb14e251745f1cf3832fc32fff59ee7fdce956bd5b5bf8": "sha256:12a359cd052828523d9e7479673c26c4c9c23cc628d7a4e7210ea7deae4994d7"
        },
        "docker": {
            "docker:latest": "sha256:6065c45f62eb6520a4a59e540db7d2d91ae9779fdaa756264f80a1582071e923",
            "docker@sha256:0559f101de7c5f118f7b4dd6cc6051c68feabe2f2c0ea5b4b45fc9d22b4c2fe2": "sha256:6065c45f62eb6520a4a59e540db7d2d91ae9779fdaa756264f80a1582071e923"
        },
        "mnadeem/dockerize-maven-web-app": {
            "mnadeem/dockerize-maven-web-app:latest": "sha256:93f0b6f9c771f9c20fee76bdb5a7136d8b40aec3709b2c45a260dcf0240a6544"
        },
        "tomcat": {
            "tomcat:9.0-jre8-alpine": "sha256:cfd7426a3e7bbf3adee374d60a01bca75e71f4f95ab5d47cafba70b52edc0bc4",
            "tomcat@sha256:4f477c681f343183e0d72efd1bdfabc93f6dace3389cf6003452c7018f6cf2d9": "sha256:cfd7426a3e7bbf3adee374d60a01bca75e71f4f95ab5d47cafba70b52edc0bc4"
        }
    }
}
/var/lib/docker/image/overlay2 #
```


```Powershell
D:\>docker images
REPOSITORY                                          TAG                 IMAGE ID            CREATED             SIZE
mnadeem/dockerize-maven-web-app                     latest              93f0b6f9c771        16 hours ago        116MB
tomcat                                              9.0-jre8-alpine     cfd7426a3e7b        36 hours ago        112MB
docker                                              latest              6065c45f62eb        37 hours ago        171MB
alpine                                              latest              5cb3aa00f899        3 weeks ago         5.53MB
busybox                                             latest              d8233ab899d4        6 weeks ago         1.2MB
container-registry.oracle.com/database/enterprise   12.2.0.1            12a359cd0528        19 months ago       3.44GB

D:\>
```

```Powershell
/var/lib/docker/image/overlay2/imagedb/content/sha256 # cat d8233ab899d419c58cf3634c0df54ff5d8acc28f8173f09c21df4a07229e1205 | python -mjson.tool
{
    "architecture": "amd64",
    "config": {
        "ArgsEscaped": true,
        "AttachStderr": false,
        "AttachStdin": false,
        "AttachStdout": false,
        "Cmd": [
            "sh"
        ],
        "Domainname": "",
        "Entrypoint": null,
        "Env": [
            "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        ],
        "Hostname": "",
        "Image": "sha256:896f6e65107acffcae30fe593503aebf407fc30ad4566a8db04921dbfb6c0721",
        "Labels": null,
        "OnBuild": null,
        "OpenStdin": false,
        "StdinOnce": false,
        "Tty": false,
        "User": "",
        "Volumes": null,
        "WorkingDir": ""
    },
    "container": "197cb47b0e98a00daefcb62c5fa84634792dd22f11aa29bc95fdd4e10d654d30",
    "container_config": {
        "ArgsEscaped": true,
        "AttachStderr": false,
        "AttachStdin": false,
        "AttachStdout": false,
        "Cmd": [
            "/bin/sh",
            "-c",
            "#(nop) ",
            "CMD [\"sh\"]"
        ],
        "Domainname": "",
        "Entrypoint": null,
        "Env": [
            "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        ],
        "Hostname": "197cb47b0e98",
        "Image": "sha256:896f6e65107acffcae30fe593503aebf407fc30ad4566a8db04921dbfb6c0721",
        "Labels": {},
        "OnBuild": null,
        "OpenStdin": false,
        "StdinOnce": false,
        "Tty": false,
        "User": "",
        "Volumes": null,
        "WorkingDir": ""
    },
    "created": "2019-02-15T00:19:37.830935034Z",
    "docker_version": "18.06.1-ce",
    "history": [
        {
            "created": "2019-02-15T00:19:37.703602988Z",
            "created_by": "/bin/sh -c #(nop) ADD file:9ce77bda0ecf8a7f559c143ea91876057a8684775239a68639198fe64d38ca0c in / "
        },
        {
            "created": "2019-02-15T00:19:37.830935034Z",
            "created_by": "/bin/sh -c #(nop)  CMD [\"sh\"]",
            "empty_layer": true
        }
    ],
    "os": "linux",
    "rootfs": {
        "diff_ids": [
            "sha256:adab5d09ba79ecf30d3a5af58394b23a447eda7ffffe16c500ddc5ccb4c0222f"
        ],
        "type": "layers"
    }
}
/var/lib/docker/image/overlay2/imagedb/content/sha256 #
```


```Powershell

```