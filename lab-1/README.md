# Lab 1: Docker 101 (Linux): Basic Docker Commands,Building Docker Images, and Accessing Local Files

In this lab we'll take a look at some basic Docker commands and a simple build-ship-run workflow. We'll start by running some simple docker containers. Then we'll use a *Dockerfile* to build a custom app. Finally, we'll look at how to use bind mounts to modify a running container as you might if you were actively developing using Docker.

> **Difficulty**: Beginner (assumes no familiarity with Docker)

> **Time**: Approximately 10 minutes

> **Tasks**:
>

> * [Task 0: Prerequisites](#Task_0)
> * [Task 1: Run some simple Docker containers](#Task_1)

## <a name="task0"></a>Task 0: Prerequisites

Before we start, you'll need to gain access to your Linux VM, clone a GitHub repo, and make sure you have a DockerID.

### Make sure you have a DockerID

If you do not have a DockerID (a free login used to access Docker Cloud, Docker Store, and Docker Hub), please visit [Docker Cloud](https://cloud.docker.com) to register for one.


### Access your Linux VM
1. Visit [Play With Docker](https://hybrid.play-with-docker.com)
2. Click `Start Session`
2. On the left click `+ Add New Instance`

All of the exercises in this lab will be performed in the console window on the right of the Play With Docker screen.

### Clone the Lab GitHub Repo

Use the following command to clone the lab repo from GitHub.

```
$ git clone https://github.com/leecalcote/containers-101.git
Cloning into 'containers-101'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 14 (delta 5), reused 14 (delta 5), pack-reused 0
Unpacking objects: 100% (14/14), done.
```

## <a name="Task_1"></a>Task 1: Run some simple Docker containers

There are different ways to use containers:

1. **To run a single task:** This could be a shell script or a custom app
2. **Interactively:** This connects you to the container similar to the way you SSH into a remote server
3. **In the background:** For long-running services like websites and databases

In this section you'll try each of those options and see how Docker manages the workload.

### Run a single-task Alpine Linux container

In this step we're going to start a new container and tell it to run the `hostname` command. The container will start, execute the `hostname` command, then exit.

1. Run the following command in your Linux console:

    ```
    $ docker container run alpine hostname
    Unable to find image 'alpine:latest' locally
    latest: Pulling from library/alpine
    88286f41530e: Pull complete
    Digest: sha256:f006ecbb824d87947d0b51ab8488634bf69fe4094959d935c0c103f4820a417d
    Status: Downloaded newer image for alpine:latest
    888e89a3b36b
    ```

    The output above shows that the `alpine:latest` image could not be found locally. When this happens, Docker automatically *pulls* it form Docker Hub.

    After the image is pulled, the container's hostname is displayed (`888e89a3b36b` in the example above).

2. Docker keeps a container running as long as the process it started inside the container is still running. In this case, the `hostname` process completes when the output is written, so the container exits. The Docker platform doesn't delete resources by default, so the container still exists in the `Exited` state.

    List all containers

    ```
    $ docker container ls --all
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS            PORTS               NAMES
    888e89a3b36b        alpine              "hostname"          50 seconds ago      Exited (0) 49 seconds ago                       awesome_elion
    ```

    Notice that your Alpine Linux container is in the `Exited` state.

    > **Note:** The container ID *is* the hostname that the container displayed. In the example above it's `888e89a3b36b`
