[Home](README.md)

# Build Docker Images

## Build Docker Images By Writing DockerFile


-------------------------------
**DockerFile**  file
```Powershell
FROM debian:jessie
RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y vim
CMD ["echo", "Hello world"]

```

Refer [this](https://docs.docker.com/engine/reference/builder/#from) for more detail

**Alternate** 
```Powershell
FROM debian:jessie
RUN apt-get update && apt-get install -y \
 git \
 vim
CMD ["echo", "Hello world"]
```


Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/images/) for more detail.

-------------------------------

**docker build**  command
```Powershell
PS D:\practices\docker> docker build -t nadeem/debian .
Sending build context to Docker daemon  86.53kB
Step 1/5 : FROM debian:jessie
 ---> 51a215bbbb19
Step 2/5 : RUN apt-get update
 ---> Using cache
 ---> d04c2723e2ef
Step 3/5 : RUN apt-get install -y git
 ---> Using cache
 ---> 381bfd490d58
Step 4/5 : RUN apt-get install -y vim
 ---> Using cache
 ---> 5176427bc829
Step 5/5 : CMD ["echo", "Hello world"]
 ---> Running in ad604ba6aa2d
Removing intermediate container ad604ba6aa2d
 ---> 30a028e42657
Successfully built 30a028e42657
Successfully tagged nadeem/debian:latest
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to double check and reset permissions for sensitive files and directories.
PS D:\practices\docker>

```


Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/build/) for more detail.

-------------------------------



```Powershell
PS D:\practices\docker> docker run nadeem/debian
Hello world
PS D:\practices\docker>


```

-------------------------------

## Build Docker Images By Using Docker Commit 

-------------------------------

```Powershell
PS D:\practices\docker> docker run -it debian:jessie
root@499a341a47d3:/# git
bash: git: command not found
root@499a341a47d3:/# apt-get update &&  apt-get install -y git
0% [Connecting to deb.debian.org (149.20.4.15)] [Connecting to security.debian.org (149.20.4.14)]
```


```Powershell
PS D:\practices\docker> docker ps -a
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS                      PORTS               NAMES
499a341a47d3        debian:jessie                    "bash"                   6 minutes ago       Exited (0) 6 seconds ago                        compassionate_kowalevski

```


```Powershell
PS D:\practices\docker> docker commit 499a341a47d3 nadeem/debian:1.00
sha256:d38c806450ed21ed5e88236bb182b459a8ae0465fca0f089149705f64c7a0f3b
PS D:\practices\docker>
```
Refer the [command line reference](https://docs.docker.com/engine/reference/commandline/commit/) for more detail.

-------------------------------

```Powershell
PS D:\practices\docker> docker images
REPOSITORY                                 TAG                 IMAGE ID            CREATED             SIZE
nadeem/debian                              1.00                d38c806450ed        52 seconds ago      222MB
```


```Powershell
PS D:\practices\docker> docker run -it nadeem/debian:1.00
root@0d7de21de33a:/# git
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
 
The most commonly used git commands are:
   add        Add file contents to the index
   bisect     Find by binary search the change that introduced a bug
   branch     List, create, or delete branches
   checkout   Checkout a branch or paths to the working tree
   clone      Clone a repository into a new directory
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   fetch      Download objects and refs from another repository
   grep       Print lines matching a pattern
   init       Create an empty Git repository or reinitialize an existing one
   log        Show commit logs
   merge      Join two or more development histories together
   mv         Move or rename a file, a directory, or a symlink
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects
   rebase     Forward-port local commits to the updated upstream head
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index
   show       Show various types of objects
   status     Show the working tree status
   tag        Create, list, delete or verify a tag object signed with GPG
 
'git help -a' and 'git help -g' lists available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
root@0d7de21de33a:/#
```

-------------------------------