## About This Project
Docker and Kubernetes with Swarm. My personal notes, projects and configurations.

## Author
Aditya Hajare ([Linkedin](https://in.linkedin.com/in/aditya-hajare)).

## Current Status
WIP (Work In Progress)!

## License
Open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).

----------------------------------------

## Important Notes
- [Must Check Links](#must-check-links)
- [Docker Installation Tips](#docker-installation-tips)
- [Theory](#theory)

----------------------------------------

## Must Check Links
- The Cloud Native Trail Map is CNCF's recommended path through the cloud native landscape. The cloud native landscape, serverless landscape, and member landscape are dynamically generated on this website:
    * [https://landscape.cncf.io](https://landscape.cncf.io)
- MacOS shell tweaking:
    * [https://www.bretfisher.com/shell](https://www.bretfisher.com/shell)

----------------------------------------

## Docker Installation Tips

```diff
+ Installing on Windows 10 (Pro or Enterprise)
```
- This is the best experience on Windows, but due to OS feature requirements, it only works on the Pro and Enterprise editions of Windows 10 (with latest update rollups). We need to install [Docker for Windows](https://www.docker.com/docker-windows) from the Docker Store.
- With this Edition we should use PowerShell for the best CLI experience.
- Install [Docker Tab Completions For PowerShell Plugin](https://github.com/matt9ucci/DockerCompletion).
- Useful commands:
    ```sh
        docker version
        docker ps
        docker info
    ```

```diff
+ Installing on Windows 7, 8, or 10 Home Edition
```
- Unfortunately, Microsoft's OS features for Docker and Hyper-V don't work in these older versions, and `Windows 10 Home` edition doesn't have Hyper-V, so we'll need to install the [Docker Toolbox](https://docs.docker.com/toolbox/overview/), which is a slightly different approach to using Docker with a VirtualBox VM. This means Docker will be running in a Virtual Machine that sits behind the IP of our OS, and uses NAT to access the internet.
- **NOTE FOR TOOLBOX USERS**: On localhost, all urls that use `http://localhost` , we'll need to replace with `http://192.168.99.100`
- Useful commands:
    ```sh
        docker version
        docker-machine ls
        docker-machine start
        docker-machine help
        docker-machine env default
    ```

```diff
+ Installing on Mac
```
- We'll want to install [Docker for Mac](https://www.docker.com/docker-mac), which is great. If we're on an older Mac with less than `OSX Yosemite 10.10.3`, we'll need to install the [Docker Toolbox](https://docs.docker.com/toolbox/overview/) instead.
- Useful commands:
    ```sh
        docker version
        docker container
        docker container run --
        docker
        docker pause
    ```

```diff
+ Installing on Linux
```
- **Do not use built in default packages like `apt/yum install docker.io`** because those packages are old and not the Official Docker-Built packages.
- Prefer to use the Docker's automated script to add their repository and install all dependencies: `curl -sSL https://get.docker.com/ | sh` but we can also install in a more manual method by following specific instructions on the Docker Store for our distribution, like [this one for Ubuntu](https://store.docker.com/editions/community/docker-ce-server-ubuntu).
- Useful commands:
    ```sh
        # http://get.docker.com
        curl -fsSL get.docker.com -o get-docker.sh
        sh get-docker.sh
        sudo usermod -aG docker bret
        sudo docker version
        docker version
        sudo docker version
        docker-machine version
        # http://github.com/docker/compose
        # http://github.com/docker/compose/releases
        curl -L https://github.com/docker/compose/releases/download/1.15.0/docker-compose- `uname -s `- `uname -m` >/usr/local/bin/docker-compose
        docker-compose version
        # http://github.com/docker/machine/releases
        docker image
        docker image ls --
    ```

```diff
+ Play With Docker (PWD) Online
```
- The best free online option is to use [play-with-docker.com](http://play-with-docker.com/), which will run one or more Docker instances inside our browser, and give us a terminal to use it with.
- We can actually create multiple machines on it, and even use the URL to share the session with others in a sort of collaborative experience.
- **It's only limitation really is it's time bombed to 4 hours, at which time it'll delete our servers.**

----------------------------------------

## Theory

```diff
- Difference between Containers and Virtual Machines (VMs)
```
- A VM provides an abstract machine that uses device drivers targeting the abstract machine, while a container provides an abstract OS.
- A para-virtualized VM environment provides an abstract hardware abstraction layer (HAL) that requires HAL-specific device drivers.
- Typically a VM will host multiple applications whose mix may change over time versus a container that will normally have a single application. However, it’s possible to have a fixed set of applications in a single container.
- Containers provide a way to virtualize an OS so that multiple workloads can run on a single OS instance.
- With VMs, the hardware is being virtualized to run multiple OS instances.
- Containers’ speed, agility, and portability make them yet another tool to help streamline software development.