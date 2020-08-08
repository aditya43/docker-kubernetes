## Docker and Kubernetes with Swarm
My personal notes, projects and configurations.

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
    ```diff
    + Installing on Windows 10 (Pro or Enterprise)
    + Installing on Windows 7, 8, or 10 Home Edition
    + Installing on Mac
    + Installing on Linux
    + Play With Docker (PWD) Online
    + Install using get.docker.com
    ```
- [Theory](#theory)
    ```diff
    - Important Points To Remember
    - Difference between Containers and Virtual Machines (VMs)
    - To see what's going on in containers
    - Docker netwroks concepts for Private and Public communications
    - Docker netwroks CLI management of Virtual Networks
    - Docker networks: Default Security
    - What are Images
    - Image Layers
    - Docker Image tagging and pushing to Docker Hub
    - Dockerfile
    - Inside Dockerfile
    - To build Image from Dockerfile
    ```
- [Cleaning Up Docker](#cleaning-up-docker)
    ```diff
    + To cleanup all dangling images:
    + To cleanup everything:
    + To see space usage:
    ```
- [Container Lifetime And Persistent Data](#container-lifetime-and-persistent-data)
    ```diff
    + Data Volumes
        - Named Volumes
        - When would we ever want to use 'docker volume create' command?
        - Data Volumes: Important Docker Commands
    + Bind Mounts
        - Bind Mounts: Important Docker Commands
    ```
- [Docker Compose - The Multi-Container Tool](#docker-compose---the-multi-container-tool)
    ```diff
    + docker-compose.yml
    + docker-compose CLI
    + docker-compose to build Images at runtime
    ```
- [Docker Swarm - Built-In Orchestration](#docker-swarm---built-in-orchestration)
    ```diff
    + How to check if swarm mode is activated and how to activate it
    + What happens behind the scene when we run docker swarm init?
    + Key Concepts
    + Creating a 3-node Swarm Cluster
    ```
- [Swarm - Scaling Out With Virtual Networking](#swarm---scaling-out-with-virtual-networking)
    ```diff
    + Overlay Network Driver
    + Example: Drupal with Postgres as Services
    ```
- [Swarm - Routing Mesh](#swarm---routing-mesh)
    ```diff
    + Docker service logs to see logs from different nodes
    ```
- [Swarm - Stacks](#swarm---stacks)
    ```diff
    + How to deploy Swarm stack using compose file?
    ```
- [Swarm - Secret Storage](#swarm---secret-storage)
    ```diff
    + What is a Secret?
    + How to create a Secret?
    + How to decrypt a Secret?
    + How to remove a Secret?
    ```
- [Swarm - Service Updates Changing Things In Flight](#swarm---service-updates-changing-things-in-flight)
    ```diff
    + Swarm Update Examples
    ```
- [Docker Healthchecks](#docker-healthchecks)
    ```diff
    + Where do we see Docker Healthcheck status?
    + Healthcheck Docker Run Example
    + Healthcheck in Dockerfile
    ```
- [Container Registeries](#container-registeries)
    ```diff
    + Docker Hub
    + Running Docker Registry
    + Running A Private Docker Registry
    + Registry And Proper TLS
    + Private Docker Registry In Swarm
    ```
- [Kubernetes](#kubernetes)
    ```diff
    + What is Kubernetes
    + Why Kubernetes
    + Kubernetes vs. Swarm
    ```
- [Kubernetes Installation And Architecture](#kubernetes-installation-and-architecture)
    ```diff
    + Kubernetes Installation
        - Docker Desktop
        - Docker Toolbox on Windows
        - Linux or Linux VM in Cloud
        - Kubernetes In A Browser
    + Kubernetes Architecture Terminology
    ```
- [Kubernetes Container Abstractions](#kubernetes-container-abstractions)
    ```diff
    + Kubernetes Container Abstractions
    + Kubernetes Run, Create and Apply
    ```
- [Kubernetes - Basic Commands](#kubernetes---basic-commands)
    ```diff
    + Creating First Pods - nginx
    + Scaling Replica Sets - Apache Httpd
    + Inspecting Kubernetes Objects - Apache Httpd
    ```
- [Kubernetes Services](#kubernetes-services)
    ```diff
    + Kubernetes Services - ClusterIP (default)
    + Kubernetes Services - NodePort
    + Kubernetes Services - LoadBalancer
    ```
- [Kubernetes Management Techniques](#kubernetes-management-techniques)
    ```diff
    + Run, Create, Expose Generators
    + Generators Example
    + Imperative vs. Declarative
    ```
- [Generic Examples](#generic-examples)
    ```diff
    + Running 3 Containers: nginx (80:80), mysql (3306:3306), httpd (Apache Server - 8080:80)
    + To clean up apt-get cache
    + To get a Shell inside Container
    + To create a temp POD in cluser and get an interactive shell in it
    + Docker Swarm - Create Our First Service and Scale it Locally
    + Creating a 3-Node Swarm Cluster
    + Scaling Out with Overlay Networking
    + Scaling Out with Routing Mesh
    + Create a Multi-Service Multi-Node Web App
    + Swarm Stacks and Production Grade Compose
    + Using Secrets in Swarm Services
    + Using Secrets with Swarm Stacks
    + Create A Stack with Secrets and Deploy
    + Service Updates: Changing Things In Flight
    + Healthchecks in Dockerfile
    ```

----------------------------------------

## Must Check Links
- How DNS works? DNS basics:
    * [https://howdns.works](https://howdns.works)
    * [https://dyn.com/blog/dns-why-its-important-how-it-works](https://dyn.com/blog/dns-why-its-important-how-it-works)
- Round-Robin DNS, what is it:
    * [https://en.wikipedia.org/wiki/Round-robin_DNS](https://en.wikipedia.org/wiki/Round-robin_DNS)
- Official Docker Image specifications:
    * [https://github.com/moby/moby/blob/master/image/spec/v1.2.md](https://github.com/moby/moby/blob/master/image/spec/v1.2.md)
    * [https://github.com/moby/moby/tree/master/image/spec](https://github.com/moby/moby/tree/master/image/spec)
- List of official Docker Images:
    * [https://github.com/docker-library/official-images/tree/master/library](https://github.com/docker-library/official-images/tree/master/library)
    * [https://github.com/docker-library/official-images](https://github.com/docker-library/official-images)
- The Cloud Native Trail Map is CNCF's recommended path through the cloud native landscape. The cloud native landscape, serverless landscape, and member landscape are dynamically generated on this website:
    * [https://landscape.cncf.io](https://landscape.cncf.io)
- The 12-Factor App. Key to Cloud Native App Design, Deployment, and Operation.
    * [https://12factor.net](https://12factor.net)
- 12 Fractured Apps.
    * [https://medium.com/@kelseyhightower/12-fractured-apps-1080c73d481c#.cjvkgw4b3](https://medium.com/@kelseyhightower/12-fractured-apps-1080c73d481c#.cjvkgw4b3)
- `YAML` quick reference:
    * [https://yaml.org/refcard.html](https://yaml.org/refcard.html)
    * Sample `yaml` file. Generic: [https://yaml.org/start.html](https://yaml.org/start.html)
- `docker-compose` tool download for `linux`:
    * [https://github.com/docker/compose/releases](https://github.com/docker/compose/releases)
- Only one host for production environment. What to use: docker-compose or single node swarm?
    * [https://github.com/BretFisher/ama/issues/8](https://github.com/BretFisher/ama/issues/8)
- An introduction to immutable infrastructure.
    * [https://www.oreilly.com/radar/an-introduction-to-immutable-infrastructure](https://www.oreilly.com/radar/an-introduction-to-immutable-infrastructure)
- MacOS shell tweaking:
    * [https://www.bretfisher.com/shell](https://www.bretfisher.com/shell)
- MacOS - Commands for getting into local Docker VM:
    * [https://www.bretfisher.com/docker-for-mac-commands-for-getting-into-local-docker-vm](https://www.bretfisher.com/docker-for-mac-commands-for-getting-into-local-docker-vm)
- Windows - Commands for getting into local Docker Moby VM:
    * [https://www.bretfisher.com/getting-a-shell-in-the-docker-for-windows-vm](https://www.bretfisher.com/getting-a-shell-in-the-docker-for-windows-vm)
- Docker Internals - Cgroups, namespaces, and beyond: what are containers made from?:
    * [https://www.youtube.com/watch?v=sK5i-N34im8&feature=youtu.be&list=PLBmVKD7o3L8v7Kl_XXh3KaJl9Qw2lyuFl](https://www.youtube.com/watch?v=sK5i-N34im8&feature=youtu.be&list=PLBmVKD7o3L8v7Kl_XXh3KaJl9Qw2lyuFl)
- Windows Containers and Docker: 101:
    * [https://www.youtube.com/watch?v=066-9yw8-7c](https://www.youtube.com/watch?v=066-9yw8-7c)
- Heart of the SwarmKit Topology Management (Youtube & slides):
    * YouTube: [https://www.youtube.com/watch?v=EmePhjGnCXY](https://www.youtube.com/watch?v=EmePhjGnCXY)
    * Slides: [https://speakerdeck.com/aluzzardi/heart-of-the-swarmkit-topology-management](https://speakerdeck.com/aluzzardi/heart-of-the-swarmkit-topology-management)
- Swarm Mode Deep Dive:
    * Part1: [https://www.youtube.com/watch?v=dooPhkXT9yI](https://www.youtube.com/watch?v=dooPhkXT9yI)
    * Part2: [https://www.youtube.com/watch?v=_F6PSP-qhdA](https://www.youtube.com/watch?v=_F6PSP-qhdA)
- Raft Consensus Visualization (Our Swarm DB and how it stays in sync across nodes):
    * [http://thesecretlivesofdata.com/raft/](http://thesecretlivesofdata.com/raft/)
- Docker Swarm Firewall Ports:
    * [https://www.bretfisher.com/docker-swarm-firewall-ports](https://www.bretfisher.com/docker-swarm-firewall-ports)
- How To Configure Custom Connection Options for your SSH Client:
    * [https://www.digitalocean.com/community/tutorials/how-to-configure-custom-connection-options-for-your-ssh-client](https://www.digitalocean.com/community/tutorials/how-to-configure-custom-connection-options-for-your-ssh-client)
- Create and Upload a SSH Key to Digital Ocean:
    * [https://www.digitalocean.com/docs/droplets/how-to/add-ssh-keys](https://www.digitalocean.com/docs/droplets/how-to/add-ssh-keys)
- Only one host for production environment. What to use: docker-compose or single node swarm?
    * [https://github.com/BretFisher/ama/issues/8](https://github.com/BretFisher/ama/issues/8)
- Kubernetes Components:
    * [https://kubernetes.io/docs/concepts/overview/components/#master-components](https://kubernetes.io/docs/concepts/overview/components/#master-components)
- `MikroK8s` for Linux Hosts:
    * [https://github.com/ubuntu/microk8s](https://github.com/ubuntu/microk8s)
- `Minikube` Download:
    * [https://github.com/kubernetes/minikube/releases/](https://github.com/kubernetes/minikube/releases/)
- Install `kubectl` on Windows when you don't have `Docker Desktop`:
    * [https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-windows)
- `Kubernetes Service`:
    * [https://kubernetes.io/docs/concepts/services-networking/service/](https://kubernetes.io/docs/concepts/services-networking/service/)
- `Kubernetes Namespaces`:
    * [https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)
- `Kubernetes Pod Overview`:
    * [https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)
- `kubectl` for `Docker Users`:
    * [https://kubernetes.io/docs/reference/kubectl/docker-cli-to-kubectl/](https://kubernetes.io/docs/reference/kubectl/docker-cli-to-kubectl/)
- **`kubectl` Cheat Sheet**:
    * [https://kubernetes.io/docs/reference/kubectl/cheatsheet/](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- `Stern (Multi pod and container log tailing for Kubernetes)` for better multi-node log viewing at the CLI:
    * [https://github.com/wercker/stern](https://github.com/wercker/stern)
- What is `Kubernetes Service`:
    * [https://kubernetes.io/docs/concepts/services-networking/service/](https://kubernetes.io/docs/concepts/services-networking/service/)
- `Kubernetes Service Types`:
    * [https://kubernetes.io/docs/tutorials/services/](https://kubernetes.io/docs/tutorials/services/)
- Using a `Kubernetes Service` to Expose Our App:
    * [https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/)
- `Kubernetes NodePort Service`:
    * [https://kubernetes.io/docs/concepts/services-networking/service/#nodeport](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)
- `CoreDNS` for `Kubernetes`:
    * [https://www.coredns.io/plugins/kubernetes/](https://www.coredns.io/plugins/kubernetes/)
- `Kubernetes` DNS Specifications:
    * [https://github.com/kubernetes/dns/blob/master/docs/specification.md](https://github.com/kubernetes/dns/blob/master/docs/specification.md)

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

```diff
+ Install using get.docker.com
```
- Go to [https://get.docker.com](https://get.docker.com) and read the instructions.

----------------------------------------

## Theory
```diff
- Important Points To Remember
```
- **Forget IP's**: Static IP's and using IP's for talking to Containers is an `anti-pattern`. Always try best to avoid it!
- Docker daemon has a built-in DNS server that Containers use by default.
- Docker defaults the `hostname` to the Container's name, but we can also set aliases.
- Containers shouldn't rely on IP's for inter-communication.
- Make sure that we are always creating custom networks instead of using default ones.
- `Alpine` is a destribution of linux which is very very small in size. i.e. less than `5 mb`.

```diff
- Difference between Containers and Virtual Machines (VMs)
```
- **Containers:**
    * Containers aren't Mini-VM's.
    * Containers are just processes. They are processes running in our host OS.
    * Containers are limited to what resources they can access.
    * Containers exit when process stops.
- A VM provides an abstract machine that uses device drivers targeting the abstract machine, while a container provides an abstract OS.
- A para-virtualized VM environment provides an abstract hardware abstraction layer (HAL) that requires HAL-specific device drivers.
- Typically a VM will host multiple applications whose mix may change over time versus a container that will normally have a single application. However, it’s possible to have a fixed set of applications in a single container.
- Containers provide a way to virtualize an OS so that multiple workloads can run on a single OS instance.
- With VMs, the hardware is being virtualized to run multiple OS instances.
- Containers’ speed, agility, and portability make them yet another tool to help streamline software development.

```diff
- To see what's going on in containers
```
- List all processes in one container:
    ```sh
    docker container top
    ```
- To see details of specific container config:
    ```sh
    docker container inspect
    ```
- To see live performance stats for all containers:
    ```sh
    docker container stats
    ```

```diff
- Docker netwroks concepts for Private and Public communications
```
- When we start a Container, in the background we are connecting to a particular Docker network. And by default that is the `bridge` network.
- Each Container is connected to a private virtual network `bridge`.
- Each virtual network routes through `NAT Firewall` on host IP.
- All Containers on a virtual network can talk to each other without `-p`.
- **Best Practice** is to create a new virtual network for each app. For e.g.
    * Network `my_api` for `mongo` and `nodejs` containers.
    * Network `my_web_app` for `mysql` and `php/apache` containers.
- Use different `Docker Network Drivers` to gain new abilities.
- **`-p` is always in `HOST:CONTAINER` format.** For e.g.
    ```sh
    # In below command, '-p 80:80' means forward traffic of port 80 of 'host' to port 80 of container.
    docker container run -p 80:80 --name webhost -d nginx
    ```
- To see information about published ports for any Container i.e. which ports of Container are listening to which ports of `host`:
    ```sh
    # 'webhost' is the name of our already running nginx container.
    docker container port webhost
    ```
- To know the IP address of running Container using `inspect` command:
    ```sh
    # 'webhost' is the name of our already running nginx container.
    docker container inspect --format "{{ .NetworkSettings.IPAddress }}" webhost
    ```
- `--network bridge` is the default Docker Virtual Network `NAT'ed` behind the `host` ip.
- `--network host` gains performace by skipping virtual networks but sacrifices security of container model.
- `--network none` removes `eth0` and only leaves us with `localhost` interface in Container.
- `Network Drivers` are built-in or 3rd party extensions that gives us `Virtual Network` features.

```diff
- Docker netwroks CLI management of Virtual Networks
```
- To list/show all networks:
    ```sh
    docker network ls
    ```

- To `inspect` a network:
    ```sh
    docker network inspect NETWORK_ID
    ```
- To `create` a network:
    ```sh
    docker network create --driver
    ```
- To `attach` a network to Container:
    ```sh
    docker network connect
    ```
- To `detach/disconnect` a network from Container:
    ```sh
    docker network disconnect
    ```

```diff
- Docker networks: Default Security
```
- While creating apps, we should make `frontend, backend` sit on same Docker network.
- Make sure that their (frontend, backend) inter-communication never leaves host.
- All externally exposed ports are closed by default in Containers.
- We must manually expose ports using `-p` option, which is better default security!
- This gets even better with `Swarm` and `Overlay Networks`.

```diff
- What are Images
```
- `Images` are nothing but application binaries and dependencies for our apps and the metada - `how to run it`.
- `Official Definition`: An image is an ordered collection of root filesystem changes and the corresponding execution parameters for use within a Container runtime.
- Inside an `Image`, there's no complete OS. No kernel and kernel modules (e.g. drivers). It contains just binaries that our application needs. It is because the `host` provides the `kernel`.
- Image can be small as one file (our app binary) like a `golang` static binary.
- Or an Image can be big as a `Ubuntu distro` with `apt` and `Apache`, `PHP` and more installed.
- Images aren't necessarily named, Images are `tagged`. And a version of an Image can have more than 1 `tag`.
- To pull the specific version of Image:
    ```sh
    docker pull nginx:1.17.9
    # Or to pull the latest version of any image
    docker pull nginx:latest
    ```
- **In production**, always lock version by specifying exact version number.

```diff
- Image Layers
```
- This is a fundamental concept about how Docker works.
- Images are made up of file system changes and metadata.
- Each layer is uniquely identified (SHA) and only stored once on a `host`. This saves storage space on `host` and transfer time on `push/pull`.
- A Container is just a single `read/write layer` on top of Image.
- Docker uses a `Union File System` to present it's series of file system changes as an actual file system.
- Container runs as an additional layer on top of an Image.
- Images are designed using `Union File System` concept to make layers about the changes.
- Use `docker history` command to see layers of changes made in image:
    ```sh
    docker history IMAGE_NAME
    ```
- Each layer has a unique SHA associated with it.
- **Copy on Write:** When a change is made into some file in base image, Docker will copy that file from base image and put it in Container layer itself.
- To see the JSON metadata of the Image:
    ```sh
    docker image inspect IMAGE_NAME
    ```

```diff
- Docker Image tagging and pushing to Docker Hub
```
- Images don't technically have names. They have `tags`. When we do `docker image ls`, there's no `name column`, instead there is `tag` column.
- `latest` tag doesn't always means latest version of that Image. It's just the default tag, but Image owners should assign it to the newest stable version.
- We refer to Image with 3 distinct categories: `<user>/<repo>:<tag>`.
    * `<repo>` is made of either an organisation name or username.
- **Official Repositories** live at the `Root Namespace` of the registery, so they don't need account name in front of repo name.
- `tag` is just a pointer to a specific image commit, and really could be anything into that repository.
- To `re-tag` and existing image:
    ```sh
    # Assuming 'mysql' image already exists in our system.
    docker image tag mysql adityahajare/mysql adityahajare/latestmysql adityahajare/additionaltagname
    ```
- To push our own Image:
    ```sh
    # Uploads changed layers to a image registery.
    docker image push TAG_NAME
    # For e.g.
    docker image push adityahajare/mysql
    ```
- If we get `Access Denied` error, we need to login with our Docker Hub account. To login:
    ```sh
    docker login
    ```
- `docker login` defaults to logging into a `Docker Hub`, but we can modify by adding `server url`. Do following to see default:
    ```sh
    cat .docker/config.json
    ```
    * **NOTE:** `Docker For MAC` now stores this auth into `Keychain` for better security.
- **Always logout from shared machines or servers when done, to protect our account.**
- To make a `private` repository, login to Docker Hub and create the private repo first and then push Image to it.

```diff
- Dockerfile
```
- `Dockerfile` is a recipe to create Image.
- `Dockerfile` is not a shell script or a batch file it's a totally different language of file that's unique to Docker and the default name is `Dockerfile` with a capital `D`.
- From a command line, whenever we need to deal with a `Dockerfile` using the `docker` command, we can actually use the `-f` (which is common amongst lot of tools with Docker) option to specify a different file than default `Dockerfile`. For e.g.
    ```sh
    docker build -f SOME_DOCKER_FILE
    ```

```diff
- Inside Dockerfile
```
- `From` command:
    * It's in every `Dockerfile` and required to be there.
    * It denotes a minimal distribution For e.g. `debian`, `alpine` etc.
    * One of the main benifits to use these distributions in Containers is to use their `package distribution systems` to install whatever software we need in our packages.
    * `Package Manager`: `package managers` like `apt` and `yum` are one of the reasons to build Containers from `debian`, `ubuntu`, `fedora` or `centos`.
- `Env`:
    * **Optional** block.
    * It's a way to set environment variables.
    * One reason they were chosen as preferred way to inject `key/value` is they work everywhere, on every OS and config.
- `Run`:
    * **Optional** block.
    * Used to execute shell commands inside Container. It is used when we need to install software with a package repository, on we need to do some `unzipping` or some file edits inside the Container itself.
    * `Run` commands can also run `shell scripts`, or any commands that we can access from inside the Container.
    * `Dockerfile` can have multiple `Run` command blocks.
    * **All commands are run as `root`.** This is a common problem in Docker. If we are downloading any files using `run` command and if those files require different permissions then we will have to run another command to change it's permissions. For e.g:
    ```sh
    # -R means recursively.
    # Syntax: chown -R USER:GROUP DIRECTORY
    chown -R www-data:www-data bootstrap
    ```
- `Expose`:
    * **Optional** block.
    * By default no `TCP` or `UDP` ports are open inside a Container.
    * It doesn't expose anything from the Container to a `virtual network` unless we list it under `Expose` block.
    * `Expose` command does not mean those `ports` will be opened automatically on our `host`.
    * We still have to use `-p` with `docker run` to open up these ports.
    * By specifying `ports` under `Expose` block, we are only allowing Containers to receive packets comming at these ports.
- `WORKDIR`:
    * **Optional** block.
    * Used to change `Working Directory`.
    * Using `WORKDIR` is preferred over using `RUN cd /some/path`.
- `COPY`:
    * **Optional** block.
    * Used to copy files/source code from our local machine, or `build servers`, into our Container Image.
- `CMD`:
    * It is a required parameter in every `Dockerfile`.
    * It is the final command that will be run every time we launch a new Container from the Image, or every time we restart a stopped Container.

```diff
- To build Image from Dockerfile
```
- To build an Image from `Dockerfile`:
    ```sh
    # '-t' to specify tag name.
    # '.' says Dockerfile is in current directory location.
    docker image build -t SOME_TAG_NAME .
    ```

----------------------------------------

## Cleaning Up Docker
- We can use `prune` commands to clean up `images`, `volumes`, `build cache`, and `containers`.
- Useful YouTube video about `prune`: [https://youtu.be/_4QzP7uwtvI](https://youtu.be/_4QzP7uwtvI)

```diff
+ To cleanup all dangling images:
```
```sh
    # We can use '-a' option to clean up all images.
    docker image prune
```

```diff
+ To cleanup everything:
```
```sh
    docker system prune
```

```diff
+ To see space usage:
```
```sh
    docker system df
```

- If we're using `Docker Toolbox`, the `Linux VM` won't auto-shrink. We'll need to delete it and re-create (make sure anything in docker containers or volumes are backed up). We can recreate the `toolbox default VM` with following commands:
```sh
    docker-machine rm
    docker-machine create
```

----------------------------------------

## Container Lifetime And Persistent Data
- Containers are **usually** meant to be `immutable` and `ephemeral`. i.e. Containers are `unchanging`, `temporary`, `disposable` etc.
- **Best Practice:** Never update application in Containers, rather replace Containers with new version of application.
- The idea of Containers having `Immutable Infrastructure` (Only re-deploy Containers, never change), simply means that we don't change things once they're running. And if a `config` change needs to happen, or may be the `Container Version` upgrade needs to happen, then we `redeploy` a whole new Container.
- Docker provides 2 solutions for `Persistent Data`:
    * `Data Volumes`.
    * `Bind Mounts`.

```diff
+ Data Volumes
```
- `Docker Volumes` are a special option for Containers which creates a special location outside of that Container's `UFS (Union File System)` to store `unique data`.
- This preserves it acrosss Container removals and allows us to attach it to whatever Container we want.
- The Container just sees it like a local file path or a directory path.
- **Volumes need manual deletion. We can't just clear them out by removing a Container.**
- We might want to use following command to `cleanup` unused volumes and make it easier to see what we're doing there.
    ```sh
    docker volume prune
    ```
- A friendly way to assign new volumes to Container is using `named volumes`.

    ```diff
    - Named Volumes
    ```
    * It provides us an ability to specify things on the `docker run` command.
    * `-v` allows us to specify either a `new volume` we want to create or a named volume by specifying volume name attached by colon. For e.g.
    ```sh
    # Check '-v mysql-db:/var/lib/mysql'
    # 'mysql-db' is a volume name.
    docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=true -v mysql-db:/var/lib/mysql mysql
    ```
    * `Named Volumes` allows us to easily identify and attach same volumes to multiple Containers.

    ```diff
    - When would we ever want to use 'docker volume create' command?
    ```
    * There are only few cases when we have to create `volumes` before we run Containers.
    * When we want to use `custom drivers` and `labels` for `volumes`, we will have to create them `volumes` before we run our Containers.

    ```diff
    - Data Volumes: Important Docker Commands
    ```
    ```sh
    docker pull mysql
    docker image inspect mysql
    docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql
    docker container ls
    docker container inspect mysql
    docker volume ls
    docker volume inspect TAB COMPLETION
    docker container run -d --name2 mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True mysql
    docker volume ls
    docker container stop mysql
    docker container stop mysql2
    docker container ls
    docker container ls -a
    docker volume ls
    docker container rm mysql mysql2
    docker volume ls
    docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql
    docker volume ls
    docker volume inspect mysql-db
    docker container rm -f mysql
    docker container run -d --name mysql3 -e MYSQL_ALLOW_EMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql
    docker volume ls
    docker container inspect mysql3
    docker volume create --help
    ```
- **`-v` command is not compatible with `docker services`. To use `volumes` with `docker services`, we have to use `--mount` command and specify verious required options with it.** For e.g. Creating a `volume` for `postgres service`:
    ```sh
    docker service create --name db --network backend -e POSTGRES_HOST_AUTH_METHOD=trust --mount type=volume,source=db-data,target=/var/lib/postgresql/data postgres:9.4
    ```

```diff
+ Bind Mounts
```
- `Bind Mounts` are simply us sharing or mounting a `host directory`, or `file`, into a Container.
- In other words, `Bind Mounts` maps a host files or directories to a Container file or directory.
- The Container just sees it like a local file path or a directory path.
- In the background, it's just 2 locations pointing to the same file(s).
- Skips `UFS (Union File System)` and `host` files overwrite existing (if any) in Container.
- Since `Bind Mounts` are `host` specific, they need specific data to be on the hard drive of the `host` in order to work:
    * We can only specify `Bind Mounts` at `docker container run` command.
    * We cannot specify `Bind Mounts` in `Dockerfile`.
- It's similar to creating `Named Volumes` with `-v` command. Only difference is - instead of `named volume name`, we specify `full path` before colon. For e.g.
    ```sh
    # Windows:
    # Check '-v //c/Users/Aditya/stuff:/path/container/'
    # '//c/Users/Aditya/stuff' is a full path
    docker container run -v //c/Users/Aditya/stuff:/path/container/ IMAGE_NAME

    # Mac/Linux:
    # Check '-v /Users/Aditya/stuff:/path/container/'
    # '/Users/Aditya/stuff' is a full path
    docker container run -v /Users/Aditya/stuff:/path/container/ IMAGE_NAME
    ```
- **NOTE: Docker identifies difference between `Named Volumes` and `Bind Mounts` since there is forward slash (In Windows, there are 2 forward slashses) when we set `-v` option value.**
- `Bind Mounts` are great for local development, local testing.

    ```diff
    - Bind Mounts: Important Docker Commands
    ```
    ```sh
    pcat Dockerfile
    docker container run -d --name nginx -p 80:80 -v $(pwd):/usr/share/nginx/html nginx
    docker container run -d --name nginx2 -p 8080:80 nginx
    docker container exec -it nginx bash
    ```

----------------------------------------

## Docker Compose - The Multi-Container Tool
- `Docker Compose` Why's:
    * Helps configure relationships between Containers.
    * Allows us to save our Docker Container `run` settings in easy-to-read file.
    * With `Docker Compose`, we can create one-liner developer environment startups.
- There are 2 parts to Docker Compose:
    * `YAML` formatted file that describes our solution options for:
        - Containers
        - Networks
        - Volumes
        - Environment Variables
        - Images
    * CLI tool `docker-compose`:
        - Used for local dev/test automation with those `YAML` files to simplify our Docker commands.

```diff
+ docker-compose.yml
```
- It was originally called `Fig` (years a go).
- Compose YAML format has it's own versions. For e.g. `1, 2, 2.1, 3, 3.1` etc.
- It can be used with `docker-compose` command for local Docker automation or can now be used (`v1.13 and above`) directly with the Docker command line in `production` with `swarm`.
- `docker-compose.yml` is the default filename, but any other filename can be used with `docker-compose -f` option, as long as it's a proper `YAML`.

```diff
+ docker-compose CLI
```
- `docker-compose` CLI tool comes with Docker for `windows` and `mac` as well as Toolbox, but there's a separate download of `docker-compose` CLI for `linux`.
- `docker-compose` CLI is not a `production-grade` tool but ideal for local development and test.
- Two common commands that we use are:
    ```sh
    docker-compose up       # Setup Volumes, Networks and start all Containers.
    docker-compose down     # Stop all Containers and remove Containers, Volumes and Networks
    pcat docker-compose.yml
    docker-compose up
    docker-compose up -d
    docker-compose logs
    docker-compose --help
    docker-compose ps
    docker-compose top
    docker-compose down
    ```
- If all our projects had `Dockerfile` and `docker-compose.yml` then a `new developer onboarding` would be running just following 2 commands:
    ```sh
    git clone github.com/some/project
    docker-compose up
    ```

```diff
+ docker-compose to build Images at runtime
```
- Another thing `docker-compose` can do is build our Images at runtime.
- `docker-compose` can also build our custom Images.
- It will look in the `cache` for Images, and if it has build options in it, it will build the Image when we use the `docker-compose up` command.
- It won't build the Image every single time. It will only build it only if it doesn't find it. We will have to use `docker-compose build` to rebuild Images if we change 'em or we can use `docker-compose up --build`.
- This is great for complex builds that have lots of `vars` or `build args`.
- **`Build Arguments` are `Environment Variables` that are available only during Image builds.**
- Important commands:
    ```sh
    docker-compose.yml
    docker-compose up
    docker-compose up --build
    docker-compose down
    docker image ls
    docker-compose down --help
    docker image rm nginx-custom
    docker image ls
    docker-compose up -d
    docker image ls
    docker-compose down --help
    docker-compose down --rmi local
    ```

----------------------------------------

## Docker Swarm - Built-In Orchestration
- `Swarm Mode` is a `clustering` solution built inside Docker.
- **Swarm Mode** is not enabled by default in Docker.
- Its a new feature launched in 2016 (Added in `v1.12` via `SwarmKit Toolkit`) that brings together years of understanding the needs of Containers and how to actually run them live in production.
- At it's core, `Swarm` is actually a `server clustering` solution that brings together different operating systems or hosts or nodes, into a single manageable unit that we can then orchestrate the lifecycle of our Containers in.
- This is not related to `Swarm Classic` for `pre-1.12` versions.
- `Swarm Mode` answers following questions:
    * How do we automate Container lifecyle?
    * How can we easily scale out/in/up/down?
    * How can we ensure our Containers are re-created when they fail?
    * How can we replace Containers without downtime (`blue/green` deployment)?
    * How can we control where Containers get started?
    * How can we track where Containers get started?
    * How can we create `cross-node` virtual networks?
    * How can we ensure only trusted servers run our Containers?
    * How can we store `secrets`, `keys`, `passwords` and get them to the right Container (and only that Container)?
- Once we enable `Swarm Mode`, following are the set of new commands we can use:
    ```sh
    docker swarm
    docker node
    docker service
    docker stack
    docker secret
    ```
- **When we're in a `Swarm`, we cannot use an `image` that's only on 1 node. A `Swarm` has to be able to pull `Images` on all nodes from some repository in a `registry` that they can all reach.**

```diff
+ How to check if swarm mode is activated and how to activate it
```
- To check if `Swarm` mode is activated or not
    * execute
        ```sh
        docker info
        ```
    * Look for `Swarm: inactive/active`. For e.g. consider following output of `docker info` command:
        ```sh
        Client:
        Debug Mode: false

        Server:
        Containers: 0
        Running: 0
        Paused: 0
        Stopped: 0
        Images: 0
        Server Version: 19.03.8
        Storage Driver: overlay2
        Backing Filesystem: <unknown>
        Supports d_type: true
        Native Overlay Diff: true
        Logging Driver: json-file
        Cgroup Driver: cgroupfs
        Plugins:
        Volume: local
        Network: bridge host ipvlan macvlan null overlay
        Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
        Swarm: inactive     # Check for this one.
        Runtimes: runc
        Default Runtime: runc
        Init Binary: docker-init
        containerd version: 7ad184331fa3e55e52b890ea95e65ba581ae3429
        runc version: dc9208a3303feef5b3839f4323d9beb36df0a9dd
        init version: fec3683
        Security Options:
        seccomp
        Profile: default
        Kernel Version: 4.19.76-linuxkit
        Operating System: Docker Desktop
        OSType: linux
        Architecture: x86_64
        CPUs: 4
        Total Memory: 2.924GiB
        Name: docker-desktop
        ID: J2KP:ZPIE:5DLS:SLVA:RC2C:OJVX:7GK6:3T77:WY4G:XCXP:U4RB:2JV2
        Docker Root Dir: /var/lib/docker
        Debug Mode: true
        File Descriptors: 36
        Goroutines: 53
        System Time: 2020-03-21T05:55:58.0263795Z
        EventsListeners: 3
        HTTP Proxy: gateway.docker.internal:3128
        HTTPS Proxy: gateway.docker.internal:3129
        Registry: https://index.docker.io/v1/
        Labels:
        Experimental: false
        Insecure Registries:
        127.0.0.0/8
        Live Restore Enabled: false
        Product License: Community Engine
        ```
- To enable `Swarm` mode:
    ```sh
    docker swarm init
    ```

```diff
+ What happen behind the scenes when we run docker swarm init?
```
- It does lot of `PKI` and security automation:
    * `Root Signing Certificate` created for our `Swarm` that it will use to establish `trust` and `sign` certificates for all `nodes` and all `managers`.
    * Special `Certificate` is issued for first `Manager Node` because it's a `manager` vs. a `worker`.
    * `Join Tokens` are created which we can actually use on other `nodes` to join this `Swarm`.
- `Raft Consensus Database` created to store `root CA`, `configs` and `secrets`.
    * Encrypted by default on disk (1.13+).
    * No need for another `key/value` system to hold `orchestration/secrets`.
    * Replicates logs amoungst `Managers` via mutual TLS in `control plane`.
- `Raft` is a protocol that actually ensures consistency across multiple nodes and it's ideal for using in the Cloud where we can't guarentee that any one thing will be available for any moment in time.
- It creates `Raft` database on disk. Docker stores the configuration of the `Swarm` and that `first Manager`, and it actually encrypts it.
- Then it will waut for any other nodes before it starts actually replicating the database over to them.
- All of this traffic that it would be doing once we create other nodes, it all going to be encrypted.
- We don't need an additional key value storage system or some database architecture to be the backend configuration management of our `Swarm`.

```diff
+ Key Concepts
```
- A `Service` in a `Swarm` replaces the `docker run`.
- There can only be one `Leader` at a time amoungst all `managers`.
- To remove all Containers, we have to remove `Swarm Service`.

```diff
+ Creating a 3-node Swarm Cluster
```
- Following example demonstrates where we use multiple `hosts/nodes/instances` or `multiple OS's`. And we're going to setup a `3-node Swarm` across all 3 of those nodes.
- How we can try out and implement this setup first:
    * [http://play-with-docker.com](http://play-with-docker.com)
        - Only needs a browser but resets after `4 hours`.
    * `docker-machine + VirtualBox`.
        - Free and runs locally, but requires a machine with `8gb` memory.
        - Comes default with `Docker for Win and Mac`.
        - For `Linux`, we will have to download explicitely and setup first.
    * `Digital Ocean + Docker Install`.
        - Most like a `production` setup, but costs `$5 to $10` per node per month.
        - They run everything on `SSD` so it's nice and fast.
    * `Roll our own`.
        - `docker-machine` can provision machines for `Amazon Instances`, `Azure Instances`, `Digital Ocean Droplets`, `Google Compute Nodes` etc.
        - Install docker anywhere with `get.docker.com`.
        - It is a tool to simply automate dev and test environments. It was never really designed to set up all of the production settings we might need for `multi-node Swarm`.
- To experiment setting up `3-node Swarm Cluster` on [http://play-with-docker.com](http://play-with-docker.com):
    * Go to [http://play-with-docker.com](http://play-with-docker.com).
    * Launch 3 instances.
    * On any 1 instance, execute:
        ```sh
        # First execute below command, it will give error and display public ips available on eth0 and eth1.
        docker swarm init

        # Copy eth0 ip and specify it as a --advertise-addr
        docker swarm init --advertise-addr 192.168.0.6
        ```
    * Copy the `docker swarm join` command from there.
    * Go to other 2 nodes and paste `docker swarm join` command.
    * Go to 1st node and execute following command to list out nodes:
        ```sh
        docker node ls
        ```
    * To promore `node2` to `manager`, execute following command on `node1` (Leader):
        ```sh
        docker node update --role manager node2
        ```
    * To make `node3` join as `manager` by default, go to `node1` and execute following command to get `join token`:
        ```sh
        docker swarm join-token manager
        ```
    * Copy join command and execute it on `node3`.
    * On `node1`, execute `docker node ls to see status of swarm nodes.
    * Now to run Docker `service` with `3 replicas` on `alpine` and ping 1 of the Google open DNS (8.8.8.8), execute following command on `node1`:
        ```sh
        docker service create --replicas 3 alpine ping 8.8.8.8
        ```
    * Execute:
        ```sh
        docker service ps SERVICE_NAME
        # For e.g.
        docker service ps busy_hertz
        ```

----------------------------------------

## Swarm - Scaling Out With Virtual Networking
- With `Swarm` mode enabled, we get access to new networking driver called `overlay`.
- To create a `network` using `overlay` driver:
    ```sh
    # When we don't specify anything, default driver used is 'bridge'.
    docker network create --driver overlay
    # Or
    docker network create --driver overlay
    ```

```diff
+ Overlay Network Driver
```
- It's like creating a `Swarm` wide `bridge` netowrk where the Containers across `hosts` on the same `virtual network` can access each other kind of like they're on a `VLAN`.
- This driver is only for `intra-Swarm communication`. i.e. For `container-to-container` traffic inside a single `Swarm`.
- It acts as everything is like on the same `subnet`.
- `overlay` network is the only kind of network we could use in a `Swarm`. Because `overlay` allows us to span across nodes as if they are all on the `local network`.
- The `overlay` driver doesn't play a huge amount in traffic coming inside, as it's trying to take a wholistic `Swarm` view of the network so that we're not constantly messing around with networking settings on individual nodes.
- We can also optionally enable full network encryption using `IPSec (AES)` encryption on network creation.
    * It will setup `IPSec tunnels` between all the different nodes of our `Swarm`.
    * `IPSec (AES) Encryption` is off by default for performance reasons.
- Each `services` can be connected to multiple `networks`. For e.g. (front-end, back-end).
- When we create our `services`, we can add them to none of the `overlay` networks, or one or more `overlay` networks.
- Lot of traditional apps would have their back-end on the back-end network and front-end on the front-end network. THen maybe they would have an API between the two that would be on both networks. And we can totally do this in `Swarm`.

```diff
+ Example: Drupal with Postgres as Services
```
- Create an `overlay` network first:
    ```sh
    docker network create --driver overlay NETWORK_NAME
    # For e.g.
    docker network create --driver overlay mydrupal
    ```
- Create a `Postgres` service on `mydrupal` network:
    ```sh
    docker service create --name psql --network mydrupal -e POSTGRES_PASSWORD=adi123 postgres
    ```
    * After running above command, we don't see image downloading and all that. That is because `Services` can't be run in the foreground.
    * `Services` have to go through `orchestrator` and `scheduler`. Execute following command to see and list out `services`:
    ```sh
    docker service ls
    ```
- To see details:
    ```sh
    # To see the specific `service` details such as on which `node` it is running.
    docker service ps psql
    # To see the logs from Container:
    docker container logs psql.1.gfdsnjkfdjk3kbr3289d # Tab completion is available
    ```
- Create a `Drupal` service on same `mydrupal` network:
    ```sh
    docker service create --name drupal --network mydrupal -p 80:80 drupal
    ```
- To see details:
    ```sh
    # To see the specific `service` details such as on which `node` it is running.
    docker service ps drupal
    ```
- Now we have database running on `node1` and website running on `node2`. They can talk to each other using `Service Name`.

----------------------------------------

## Swarm - Routing Mesh
- `Routing Mesh` is a `Stateless Load Balancer`.
- `Routing Mesh` load balancer acts at `OSI Layer 3 (TCP)` and not at `Layer 4 (DNS)`.
- `Routing Mesh` routes `ingress (incoming)` packets for a `Service` to a proper `Task.`
- The `Routing Mesh` is an `incoming` or `ingress` network that distributes packets for our `service` to the `Tasks` for that `service`, because we can have more than one `Task`.
- Spans all nodes in `Swarm`.
- It uses `Kernel Primitives` called `IPVS` from `Linux Kernel`.
- `Routing Mesh` load balances `Swarm Services` across their `Tasks`.
- Two ways `Routing Mesh` works:
    * `Container-to-Container` in an `Overlay Network` (uses `Virtual IP (VIP)`). `Virtual IP (VIP)` is something `Swarm` puts infront of all `Services`. It's a private IP inside the `virtual networking` of `Swarm`, and it ensures that the load is distributed amongst all the `Tasks` for a `Service`.
    * External traffic incoming to published ports (all nodes listen).
- The benefit of `Virtual IP (VIP)` over `DNS Round Robin` is that a lot of times `DNS Cache` inside our apps prevent us from properly distributing the load.
- To run multiple websites on a same port, we could use:
    * `Nginx Proxy` which is also known as `HAProxy Load Balancer Proxy`. This load balancer will act in `OSI Layer 4 (DNS)`.
    * `Docker Enterprise Edition` comes with built-in `OSI Layer 4 (DNS) Web Proxy`. It is called `UCP or Docker Data Center`.
- `Web Sockets` don't do well with `Routing Mesh`. That is because `socket` needs persistent connection to a specific Container and because of load balancing `Routing Mesh` keeps switching between Containers. We could have `proxy` infront of it to make it work with `Web Sockets`.

```diff
+ Docker service logs to see logs from different nodes
```
- To see logs from different `docker services`, execute:
    ```sh
    docker service logs NODE_NAME
    #For e.g.
    docker service logs adipostgres
    ```
- If `logging` is not available, turn it on by enabling `experimental features` of docker.
    ```javascript
    // Open /etc/docker/daemon.json and specify following:
    {"experimental": true}
    ```

----------------------------------------

## Swarm - Stacks
- `Stacks` is another layer of abstraction added to `Swarm`.
- `Swarm` is basically a `Docker Engine` and it can accept `Compose File` using `stack` command.
- `Swarm` reads the `Compose File` without needing `Docker Compose` anywhere on the server.
- Basically it's a `Compose File` for `Swarm` in production.
- `Stacks` accept `Compose File` as their declarative definition for `services`, `networks` and `volumes`.
- We use following command to deploy our `Stack`:
    ```sh
    docker stack deploy
    ```
- `Stacks` manages all those objects for us, including `overlay` network per `Stack`. Also adds `Stack Name` to start of their name.
- The key `deploy:` is what we use in our `Compose File`. It allows to specify things that are specific to `Swarm`. For e.g.
    * How many `replicas` do we want?
    * What we want to do when we `failover`?
    * How do we want to do `rolling updates`?
    * And all those sort of things that we wouldn't care about on our local development machine.
- `Stacks Config File` doesn't allow `Building`. And `Building` should never ever happen on `production`.
- `docker-compose` now ignores `deploy:` key in Config File.
- `Swarm` ignores `build:` key in Config File.
- `docker-compose` cli not needed on `Swarm Server`. It's not a `production` tool. It was designed to be a developer and sysadmin helper tool. It's best for local work.

```diff
+ How to deploy Swarm stack using compose file?
```
- To deploy a `Swarm` stack using Compose File:
    ```sh
    # '-c' option is for Compose File.
    docker stack deploy -c COMPOSE_FILE APP_NAME
    # For e.g.
    docker stack deploy -c adi-swarm-stack.yml myapp
    ```

----------------------------------------

## Swarm - Secret Storage
- Easiest `secure` solution for storing `secrets` in `Swarm`.
- Encrypted on disk and encrypted in transit as well.
- There are lots of other options like `Vault` available for storing `secrets`.
- Supports generic strings or binary content up to `500kb` in size.
- Doesn't require apps to be rewritten.
- From `Docker v1.13.0`, the `Swarm Raft Database` is encrypted on disk.
- It's only stored on the disk of the `manager` nodes and they're the only ones that have the keys to unlock it or decrypt it.
- Default is `Managers` and `Workers` `control plane` is `TLS + Mutual Auth`.
- Secrets are first stored in `Swarm` (using `docker secrets` command), then assigned to a `Service(s)`.
- Only Containers in assigned `Service(s)` can see them.
- They look like files in Containers but are actually `in-memory` filesystem.
- On disk, they are located at:
    ```sh
    /run/secrets/<secret_name>
    # OR
    /run/secrets/<secret_alias>
    ```
- Local `docker-compose` can use `file-based` secrets, but they are not secure.

```diff
+ What is a Secret?
```
- Usernames and Passwords
- `TLS` certificates and keys.
- SSH Keys.
- Any data we would prefer not to be `on the front page of the news`.

```diff
+ How to create a Secret?
```
- There are 2 ways we can create a `secret` in `Swarm`:
    * Create a text file and store value in it.
        - Assume, we have a file `db_username.txt` with text content `aditya`:
            ```sh
            > cat db_username.txt
            aditya
            ```
        - Now, to create a `secret` from above file,
            ```sh
            docker secret create SECRET_NAME FILE_PATH
            # For e.g.
            docker secret create DB_USER db_username.txt
            ```
        - Running above command will spit out a key in return.
    * Pass `secret value` at the command line.
        - To pass a `value` at command line and create a `secret` out of it:
            ```sh
            echo "myPasswordAdi123" | docker secret create DB_PASSWORD
            ```
        - Running above command will spit out a key in return.

```diff
+ How to decrypt a Secret?
```
- Only `Containers` and `Services` have access to the decrypted `secrets`.
- For e.g.
    ```sh
    # Demo

    # Create a service first.
    docker service create --name adidb --secret DB_USER --secret DB_PASS -e POSTGRES_PASSWORD_FILE=/run/secrets/DB_PASS -e POSTGRES_USER_FILE=/run/secrets/DB_USER postgres

    # List containers of 'adidb' service and copy the container name.
    docker service ps adidb

    # Get a shell inside Container.
    docker exec -it adidb.1.fbhdbj3738dh2 bash # 'adidb.1.fbhdbj3738dh2' is CONTAINER_NAME

    # Once we have the shell inside Container, list all secrets:
    ls /run/secrets/

    # 'cat' contents of any secret file and it will display decrypted value.
    cat DB_USER
    ```

```diff
+ How to remove a Secret?
```
- Only `Containers` and `Services` have access to the decrypted `secrets`.
- When we remove/add a `secret`, it will stop the Container and redeploy a new one. This is not ideal for database `services` in `Swarm`.
- To remove a `secret` from `Swarm`:
    ```sh
    # SSH/Get a shell inside Container.

    # List containers of 'adidb' service and copy the container name.
    docker service ps adidb

    # Get a shell inside Container.
    docker exec -it adidb.1.fbhdbj3738dh2 bash # 'adidb.1.fbhdbj3738dh2' is CONTAINER_NAME

    # To remove
    docker service update --secret-rm
    ```

----------------------------------------

## Swarm - Service Updates Changing Things In Flight
- Swarm's update functionality is centered around a `rolling update` pattern for our `replicas`.
- Provides `rolling replacement` of `tasks/containers` in a `service`.
- In other words, if we have a `service` with more than one `replica`, it's going to roll through them by default, one at a time, updating each `Container` by replacing it with the new settings that we're putting in the `update command`.
- Limits `downtime` (be careful with `prevents` downtime).
- Will replace `Containers` for most changes.
- There are loads of `CLI options (77+)` available to control the `update`.
- `create` options will usually change, adding `-add` or `-rm` to them.
- Also includes `rollback` and `healthcheck` options.
- Also has `scale` and `rollback` subcommands for quicker access. For e.g.
    ```sh
    docker service scale web=4
    # And
    docker service rollback web
    ```
- If a `stack` already exists and if we do `stack deploy` to a same `stack`, it will issue `service updates`.
- In `Swarm Updates`, we don't have a different `deploy` command. It's just same `docker stack deploy`, with the file that we have edited, and it's job is to work with all of the other parts of the `API` to determine if there are any changes needed, and then roll those out with a `service update`.

```diff
+ Swarm Update Examples
```
- Just update the `image` to a newer version, that is already being used. We will have to use `service update` command:
    ```sh
    docker service update --image myapp:1.2.1 <SERVICE_NAME>
    ```
- Adding an `environment` variable and remove a `port`. We will have to use `service update` command:
    ```sh
    docker service update --env-add NODE_ENV=production --publish-rm 8080
    ```
- Change number of `replicas` of two `services`. We will have to use `service scale` command:
    ```sh
    # Set number of `web` replicas to 8 and number of `api` replicas to 6.
    docker service scale web=8 api=6
    ```
- `Swarm Update`, first edit the `YAML` file and then execute:
    ```sh
    docker stack deploy -c FILE_NAME.yml <STACK_NAME>
    ```

----------------------------------------

## Docker Healthchecks
- Supported in `Dockerfile`, `Compose YAML`, `docker run` and `Swarm Services`.
- Docker engine will `exec`'s the command in the Container.
    * For e.g. `curl localhost`.
- Docker runs `Healthcheck` command from inside the Container, and not from outside the Container.
- It expects `exit 0 (OK)` or `exit 1 (Error)`.
- `Healthcheck` commands are run every `30 seconds` by default.
- `Healthcheck` in Docker specifically has only 3 `states`. Follwing are the `states`:
    * `starting`: first `30 seconds` by default, where it hasn't run a `healthcheck` command yet.
    * `healthy`.
    * `unhealthy`.
- This is much better than `is binary still running?`.
- This isn't a external monitoring replacement. 3rd party monitoring tools provide much better insights including graphs and all.

```diff
+ Where do we see Docker Healthcheck status?
```
- The `Healthcheck status` shows up in `docker container ls`.
- We can check `last 5 healthchecks` with `docker container inspect`.
- `docker run` command does not take action on an `unhealthy` Container. Once the `healthcheck` is considers a Container `unhealthy`, `docker run` is just going to indicate that in the `ls` and `inspect` commands.
- `Swarm Services` will replace `tasks/containers` if they fail `healthcheck`.
- `service update` commands wait for `healthcheck` before continuing.

```diff
+ Healthcheck Docker Run Example
```
- Adding `healthcheck` at runtime using `docker run` command:
    ```sh
    docker run \
        --health-cmd="curl -f localhost:9200/_cluster/health || false" \
        --health-interval=5s \
        --health-retries=3 \
        --health-timeout=2s \
        --health-start-period=15s \
        elasticsearch:2
    ```

```diff
+ Healthcheck in Dockerfile
```
- Basic `HEALTHCHECK` command in `Dockerfile`:
    ```yaml
    HEALTHCHECK curl -f http://localhost/ || false
    ```
- Custom options with `HEALTHCHECK` command in `Dockerfile`:
    ```yaml
    HEALTHCHECK --timeout=2s --interval=3s --retries=3 \
    CMD curl -f http://localhost/ || exit 1     # `exit 1` is equivalent to `false`.
    ```
- All options for `healthcheck` command in `Dockerfile`:
    ```sh
    # How often it should check `healthcheck`.
    --interval=DURATION # Default 30s

    # How long it should wait before marking Container `unhealthy`.
    --timeout=DURATION # Default 30s

    # When should it fire first `healthcheck` command. This gives us
    # ability to specify longer wait period than first 30 seconds.
    --start-period=DURATION # Default 0s.

    # Max number of times it should run `healthcheck` before
    # it marks that container `unhealthy`.
    --retries=N # Default 3.
    ```

----------------------------------------

## Container Registeries
- An image registry needs to be part of our `Container Plan`.
- `Docker Store` is different than `Docker Hub`.
- `Docker Cloud` is different than `Docker Hub`.

```diff
+ Docker Hub
```
- It is the most popular public `Image` registry.
- `Docker Hub` is a `Docker Registry` plus `Lightweight Image Building`.
- It provides 1 free `private repository`. We have to pay for there on wards.
- We can make use of `webhooks` to make our `repository` send `webhook notification` to services like `Jenkins`, `Codeship`, `Travis CI` or something like that, to have automated builds continue down the lines.
- `Webhooks` are there to help us automate the process of getting our code all the way from something like `Git` or `Github` to `Docker Hub` and all the way to our servers where we want to run them.
- `Collaborators` are where we provide permissions for other users to our `Image`.

```diff
+ Running Docker Registry
```
- Using `Docker Registry`, we can run a `private` Image registry for our `network`.
- It's a part of `Docker/distribution GitHub Repo`.
- The de facto in private container registries.
- Not as full featured as `Docker Hub` or `Others`, no web UI, basic auth only.
- At it's core, it's just a web API and storage system, written in `Go Lang`.
- Storage supports `local`, `S3`, `Azure`, `Alibaba`, `Google Cloud` and `OpenStack Swift`.
- We should secure our registry with `TLS (Transport Layer Security)`.
- Storage cleanup via `Garbage Collection`.
- Enable `Docker Hub Caching` via `--registry-mirror` option.

```diff
+ Running A Private Docker Registry
```
- Run the registry image on default port `5000`.
- Re-tag an existing Image and push it to our new `registry`.
- Remove that Image from our local cache and pull it from new `registry`.
- Re-create `registry` using a `bind mount` and see how it stores data.
- Following commands demonstrate `How to run private Docker registry`:
    ```sh
    docker container run -d -p 5000:5000 --name registry registry
    docker container ls
    docker image ls
    docker pull hello-world
    docker run hello-world
    docker tag hello-world 127.0.0.1:5000/hello-world
    docker image ls
    docker push 127.0.0.1:5000/hello-world
    docker image remove hello-world
    docker image remove 127.0.0.1:5000/hello-world
    docker container rm admiring_stallman
    docker image remove 127.0.0.1:5000/hello-world
    docker image ls
    docker pull 127.0.0.1:5000/hello-world:latest
    docker container kill registry
    docker container rm registry
    docker container run -d -p 5000:5000 --name registry -v $(pwd)/registry-data:/var/lib/registry registry TAB COMPLETION
    docker image ls
    docker push 127.0.0.1:5000/hello-world
    ```

```diff
+ Registry And Proper TLS
```
- `Secure by Default`: Docker won't talk to registry without `HTTPS`.
- Except, `localhost (127.0.0.0/8)`.
- For remote `self-signed TLS`, enable `insecure-registry` option in engine.

```diff
+ Private Docker Registry In Swarm
```
- Works the same way as localhost.
- Only difference is we don't have to run `docker run` command. We have to run `docker service` command or a `stack file`.
- Because of `Routing Mesh`, all nodes can see `127.0.0.1:5000`.
- We don't have to enable `insecure registry` because that's already enabled by `Docker Engine`.
- Remember to decide how to store Images (volume driver).
- **When we're in a `Swarm`, we cannot use an `image` that's only on one node. A `Swarm` has to be able to pull `Images` on all nodes from some repository in a `registry` that they can all reach.**
- **Note:** All nodes must be able to access `images`.
> **Pro Tip:** Use a hosted `SaaS Registry` if possible.
- Following commands demonstrate `How to run Private Docker Registry In Swarm?`:
    * Go to [https://labs.play-with-docker.com](https://labs.play-with-docker.com).
    * Start session and click on wrench/spanner icon and launch `5 Managers And No Workers` template.
    * Commands:
        ```sh
        # http://play-with-docker.com
        docker node ls
        docker service create --name registry --publish 5000:5000 registry
        docker service ps registry
        docker pull hello-world
        docker tag hello-world 127.0.0.1:5000/hello-world
        docker push 127.0.0.1:5000/hello-world
        docker pull nginx
        docker tag nginx 127.0.0.1:5000/nginx
        docker push 127.0.0.1:5000/nginx
        docker service create --name nginx -p 80:80 --replicas 5 --detach=false 127.0.0.1:5000/nginx
        docker service ps nginx
        ```

----------------------------------------

## Kubernetes
```diff
+ What is Kubernetes
```
- `Kubernetes` is a popular Container orchestrator.
- `Container Orchestration` is **Make many servers act like one**.
- `Kubernetes` was released in 2015 by Google Inc. and now it is maintained by open source community which Google Inc. is also part of.
- `Kubernetes` runs on top of Docker (usually) as a set of APIs in Containers.
- `Kubernetes` provides set of `APIs` or `CLI` to manage Containers across servers/nodes.
- Like in Docker we were using `docker` command a lot, in `Kubernetes` we use `kubectl (kube control)` command.
- `kubectl` is also referred to as `Kube Control` tool or `Kube Cuddle` tool or `Koob Control` etc. but the standard name from official repo is now `Kube Control`.
- Many cloud vendors provide `Kubernetes` as a service to run our Containers.
- Many vendors make a `distribution` of `Kubernetes`. It's similar to the concept of `linux distribution`. For e.g. same `linux kernel` is running of different `distributions` of `linux`.
- **In short, `Kubernetes` is a series of Containers, CLI's and configurations.**

```diff
+ Why Kubernetes
```
- Not every solution needs orchestration.
- Simple formula whether or not to use orchestration:
    * Take the `number of servers` that we need for particular environment and then the `change rate` of our applications or the environment itself. The multiplication of those 2 is equals to the benefit of Orchestration.
- If our application is changing only 1ce a month or less, then the Orchestration and the efforts involved in deploying it, managing it, securing it, may be unnecessary at this state. Especially if we're a solo developer or just a very small team. That's where things like `Elastic Beanstalk`, `Heroku` etc. start to shine as alternatives to doing our own Orchestration.
- Carefully decide which Orchestration platform we need.
- There are Cloud specific Orchestration platforms like `AWS ECS`. It is more traditional offering that have been around a little bit longer like `Cloud Foundry`, `Mesos` and `Marathon`.
- If we're concerned about running Containers on premise, and in the Cloud or potentially multi-Cloud, then we may not want to go with those Cloud specific offerings like `ECS`. Because those were around before `Kubernetes` was. So, that was sort of a legacy solution that Amazon still supports and it's still a neat option, but only if we're specific to `AWS` and that's the only place we ever plan to deploy Containers.
- `Swarm` and `kubernetes` are most popular Container Orchestrators that run on every Cloud, and in data centers, and even small environments possibly like `IoT`.
- If we decide on `Kubernetes` as our Orchestrator then next big decision comes down to `which distribution we are going to use?`
    * First part of this decision is to figure out if we want a Cloud Managed solution or if we want to roll our own solution with a vendor's product that we would install on the servers ourselves.
    * Some of the common distributions that are vendor supported are `Docker Enterprise`, `Rancher`, `OpenShift from RedHat`, `Canonical from Ubuntu Company`, `PKS from VMware` etc. Check out this list of [Kubernetes Certified Distributors](https://kubernetes.io/partners/#conformance)
    * We probably don't usually need pure upstream version of `GitHub's Kubernetes`.

```diff
+ Kubernetes vs. Swarm
```
- `Kubernetes` and `Swarm` both solve similar problems. THey are both Container orchestrators that run on top of a Container runtime. There are different Container runtimes like `Docker`, `Containerd`, `CRI-O`, `frakti` etc. `Docker` is #1.
- `Kubernetes` and `Swarm` both are solid platforms with vendor backing.
- `Swarm` is easier to `deploy/manage`.
- `Kubernetes` has more features and flexibility. It can solve more problems in more ways and also has wide adoption and support.
- **Advantages Of `Swarm`:**
    * Comes with Docker, single vendor Container platform i.e Container runtime and the Orchestrator both built by the same company (Docker).
    * Easiest orchestrator to deploy/manage ourselves.
    * Follows 80/20 rule i.e. 20% of features for 80% of use cases.
    * Runs anywhere where Docker can run:
        - local, cloud, datacenter
        - ARM, Windows, 32-bit
    * Secure by default.
    * Easier to troubleshoot because there are less moving parts in it and less things to manage.
- **Advantages Of `Kubernetes`:**
    * Clouds will deploy/manage `Kubernetes` for us. Has the widest Cloud and vendor support.
    * Now a days, even Infrastructure vendors like `VMware`, `Red Hat`, `NetApp` etc. are making their own distributions.
    * Widest adoption and community.
    * Flexible: Covers widest set of use cases.
    * `Kubernetes First` vendor support.
    * `No one ever got fired for buying IBM`.
        - i.e. Picking solution isn't 100% rational.
        - Trendy, will benefit our career.
        - CIO/CTO Checkbox.

----------------------------------------

## Kubernetes Installation And Architecture
```diff
+ Kubernetes Installation
```
- **Docker Desktop**:
    * Best one! It provides many things out of the box.
    * Enable `Kubernetes` in Docker's settings and installation is done!
    * Sets up everything inside Docker's existing `Linux VM`.
    * Runs/Configures `Kubernetes Master Containers`.
    * Manages `kubectl` install and `certs`.
    * `Docker Desktop Enterprise (paid)` allows us to swap between different versions of `Kubernetes` on the fly.
- **Docker Toolbox on Windows**: `MiniKube`
    * If we're using `Docker Toolbox on Windows` then we should use `MiniKube`.
    * We don't even need `Docker Toolbox` installed. We can run `MiniKube` separately.
    * Download `MiniKube` windows installer `minikube-installer.exe` from GitHub.
    * Type `minikube start` in shell after installation.
    * `MiniKube` has similar to `docker-machine` experience.
    * Creates a `VirtualBox VM` with `Kubernetes` master setup.
    * **We separately have to install `kubectl` for Windows.**
- **Linux or Linux VM in Cloud**: `MicroK8s`
    * If we are using `Linux OS` or any `VM` with `Linux` on it, we should use `MicroK8s`.
    * `MicroK8s` is made by `Ubuntu`.
    * `MicroK8s` installs `Kubernetes` right on the OS.
    * `MicroK8s` installs `Kubernetes` (without Docker Engine) or `localhost` (Linux).
    * Uses `snap` (rather than `apt` or `yum`) for install. So we have to install `snap` first on our Linux OS. `snap` can be installed using `apt-get` or `yum`.
    * Control the `MicroK8s service` via `microk8s.` commands. For e.g. `microk8s.enable` command.
    * `kubectl` accessible via `microk8s.kubectl`. It's better to add alias for this command in our `bash/zsh` profile:
        - `alias kubectl=microk8s.kubectl`.
- **Kubernetes In A Browser**:
    * Easy to get started.
    * Downside is it doesn't keep our environments. They are not saved.
    * Try [https://labs.play-with-k8s.com](https://labs.play-with-k8s.com)
    * Or try [https://www.katacoda.com/courses/kubernetes/playground](https://www.katacoda.com/courses/kubernetes/playground)

```diff
+ Kubernetes Architecture Terminology
```
- **`Kubernetes`**:
    * The whole orchestration system.
    * Shortly mentioned as `K8s` or `Kube`.
- **`Kubectl`**:
    * `Kubectl` stands for `Kube Control`.
    * It's a CLI to configure `Kubernetes` and manage apps.
- **`Node`**:
    * `Node` is a single server in the `Kubernetes Cluster`.
- **`Kubelet`**:
    * `Kubelets` are the `Kubernetes Agent` running on nodes.
- **`Control Plane`**:
    * Sometimes called as `master`.
    * `Control Plane` are the set of Containers that manage the `cluster`.
    * `Control Plane` includes `API Server`, `Scheduler`, `Controller Manager`, `etcd`, `coreDNS` and more..
- **`Kube-Proxy`**:
    * It's for networking in `Control Plane`..

----------------------------------------

## Kubernetes Container Abstractions
```diff
+ Kubernetes Container Abstractions
```
- **Pod**: One or more Containers running together on one `Node`.
    * `Pod` is the basic unit of deployment.
    * Containers are always in `Pod`.
    * We don't deploy Containers independently. Instead, Containers are inside `Pods` and we deploy `Pods`.
- **Controller**: For creating/updating `Pods` and other objects.
    * `Controllers` are on top of `Pods` and we use them for creating/updating `Pods` and other objects.
    * It's a differencing engine that has many types.
    * There are many types of `Controllers` such as:
        - `Deployment Controller`.
        - `ReplicaSet Controller`.
        - `StatefulSet Controller`.
        - `DemonSet Controller`.
        - `Job Controller`.
        - `CronJob Controller`.
        - And lot more..
- **Service**: The `Service` is a little bit different in `Kubernetes` than it is in `Swarm`.
    * A `Service` is specifically the endpoint that we give to a set of `Pods`, often when we use a `Controller` For e.g. `deployment controller` to deploy a set of `replica pods`, we would then set a `service` on that.
    * `Service` means a persistent endpoint in the `cluster` so that everything else can acess that set of `Pods` at a specific `DNS name` and `port`.
- **Namespace**: Filtered group of objects in a `cluster`.
    * It's an optional, advanced feature.
    * It's a simply a filter for our views when we are using `kubectl` command line.
    * For e.g. When we are using Docker desktop, it defaults to the `default namespace` and filters out all of the system containers running `Kubernetes` in the background. Because normally, we don't want to see them containers when working with `kubectl` command line.
- There are many other things to `Kubernetes` such as:
    * `Secrets`.
    * `ConfigMaps`.
    * And more..

```diff
+ Kubernetes Run, Create and Apply
```
- `kubectl run`: This command is changing to be only for `Pod` creation.
- `kubectl create`: Create some resources via CLI or YAML.
- `kubectl apply`: Create/update anything via YAML.

----------------------------------------

## Kubernetes - Basic Commands
```diff
+ Creating First Pods - nginx
```
- **Create**:
    ```sh
    kubectl version
    kubectl run my-nginx --image nginx
    kubectl get pods
    kubectl get all
    ```
- **Cleanup**
    ```sh
    kubectl get pods
    kubectl get all
    kubectl delete deployment my-nginx
    kubectl get all
    ```

```diff
+ Scaling Replica Sets - Apache Httpd
```
- **Create**:
    ```sh
    kubectl run my-apache --image httpd     # 'run' gives us a single 'pod' or 'replica'
    kubectl get all
    ```
- **Scale**
    ```sh
    # Use either below command to scale:
    kubectl scale deploy/my-apache --replicas 2
    # Or use following command:
    # kubectl scale deployment my-apache --replicas 2 # Both above and this command are same.

    kubectl get all
    ```

```diff
+ Inspecting Kubernetes Objects - Apache Httpd
```
- **Create**:
    ```sh
    kubectl run my-apache --image httpd     # 'run' gives us a single 'pod' or 'replica'
    kubectl scale deploy/my-apache --replicas 2     # Scale it to 2 replica sets.
    kubectl get all
    ```
- **Inspect Kubernetes Objects Commands**
    ```sh
    kubectl get pods

    # Get Container logs
    kubectl logs deployment/my-apache
    kubectl logs deployment/my-apache --follow --tail 1
    kubectl logs -l run=my-apache   # '-l' is for label.

    # Get bunch of details about an object, including events!
    kubectl get pods
    kubectl describe pod/my-apache-<pod id>

    # Watch a command (without needing 'watch')
    kubectl get pods -w     # Run this command in one terminal window.
    kubectl delete pod/my-apache-<pod id>   # Run this command in another terminal window.
    kubectl get pods    # Run this command in another terminal window.
    ```
- **Cleanup**
    ```sh
    kubectl delete deployment my-apache
    ```

----------------------------------------

## Kubernetes Services
- **A `service` is a stable address for `pod(s)`.**
- If we want to connect to `pod(s)`, we need a `service`.
- `kubectl expose` command creates a `service` for existing `pods`.
- `CoreDNS` allows us to resolve `services` by their `names`.
    * But this only works for services in a same `namespace`. To get all `namespaces`, run `kubectl get namespaces`.
- `Services` also has **`FQDN (Fully Qualified Domain Name)`**.
    * We can do CURL hit service with `FQDN` as below:
    ```sh
    curl <hostname>.<namespace>.svc.cluster.local
    ```
- There are four different types of `services` in `Kubernetes`:
    * `ClusterIP`
    * `NodePort`
    * `LoadBalancer`
    * `ExternalName`
- `ClusterIP` and `NodePort` are the `services` which are always available in `Kubernetes`.
- There's one more way, external traffic can get inside our `Kubernetes` - It is called `Ingress`.
- Following 3 service types are additive, each one creates the ones above it:
    * `ClusterIP`
    * `NodePort`
    * `LoadBalancer`

```diff
+ Kubernetes Services - ClusterIP (default)
```
- It's only available in the `cluster`.
- This is about one set of `Kubernetes Pods` talking to another set of `Kubernetes Pods`.
- It gets it's own  `DNS` stress. That's going to be the `DNS` address in the `core DNS` control plane.
- Single, internal virtual IP allocated. In other words, it's going to get an IP address in that virtual IP address space inside the cluster. And that allows our other `pods` running in the cluster to talk to this `service` using the port of the `service`.
- Only reachable from within `cluster (nodes and pods)`.
- `Pods` can reach service on apps port number.
- Following commands are useful for creating `ClusterIP` service:
    ```sh
    kubectl get pods -w
    kubectl create deployment httpenv --image=bretfisher/httpenv
    kubectl scale deployment/httpenv --replicas=5
    kubectl expose deployment/httpenv --port 8888
    kubectl get service
    kubectl run --generator run-pod/v1 tmp-shell --rm -it --image bretfisher/netshoot -- bash
    curl httpenv:8888
    curl [ip of service]:8888
    kubectl get service
    ```

```diff
+ Kubernetes Services - NodePort
```
- When we create a `NodePort`, we're going to get a `High Port` on each `node` that's assigned to this `service`.
- Port is open on every `node`'s IP.
- Anyone can connect (if they can reach `node`).
- `NodePort` service also creates a `ClusterIP` internally.

```diff
+ Kubernetes Services - LoadBalancer
```
- This `service` is mostly used in `Clouds`.
- It controls a `LB` endpoint external to the cluster.
- When we create `LoadBalancer` service, it will automatically create `ClusterIP` and `NodePort` services internally.
- Only available when `infra` provider gives us a `LB (e.g. AWS ELB etc)`.
- Creates `ClusterIP` and `NodePort` services and then tells `LB` to send to `NodePort`.
- Following commands are useful for creating a `NodePort` and `LoadBalancer` service:
    ```sh
    kubectl get all
    kubectl expose deployment/httpenv --port 8888 --name httpenv-np --type NodePort
    kubectl get services
    curl localhost:32334
    kubectl expose deployment/httpenv --port 8888 --name httpenv-lb --type LoadBalancer
    kubectl get services
    curl localhost:8888
    kubectl delete service/httpenv service/httpenv-np
    kubectl delete service/httpenv-lb deployment/httpenv
    ```

```diff
+ Kubernetes Services - ExternalName
```
- This `service` is used less often.
- Adds `CNAME DNS` record to `CoreDNS` only.
- Not used for `Pods`, but for giving `Pods` a `DNS Name` to use for something outside `Kubernetes`.

----------------------------------------

## Kubernetes Management Techniques
```diff
+ Run, Create, Expose Generators
```
- `Generators` are like templates. They essentially create the `spec` or specification to apply to `Kubernetes Cluster` based on our command line options.
- Commands like `Run`, `Create`, `Expose` etc. use helper templates called `Generators`.
- Every resource in `Kubernetes` has a specification or `spec`. For e.g.
    ```sh
    kubectl create deployment aditest --image nginx --dry-run -o yaml
    ```
- We can output these templates with **`--dry-run -o yaml`**. We can use these `YAML default`s as a startin point.
- Generators are `opinionated defaults`.

```diff
+ Generators Example
```
- Using dry-run with yaml output we can see the generators.
- Examples:
    ```sh
    kubectl create deployment aditest --image nginx --dry-run -o yaml
    kubectl create job aditest --image nginx --dry-run -o yaml

    # We need the deployment "aditest " to exist before below command works.
    kubectl expose deployment/aditest --port 80 --dry-run -o yaml
    ```

```diff
+ Imperative vs. Declarative
```
- **Imperative:** Focus on **how** a program operates.
- **Declarative:** Focus on **what** a program should accomplish.
- For e.g. Coffee
    * **Imperative:** I will boil water, scoop out 42 grams of medium-fine grounds, pour over 700g of water, etc.
    * **Declarative:** Barista, I would like a cup of coffee.
        - Barista is a engine that works through the steps, including retrying to make a cup of coffee, and is only finished when I have a cup of coffee.

---------------------------------****-------

## Generic Examples
```diff
+ Running 3 Containers: nginx (80:80), mysql (3306:3306), httpd (Apache Server - 8080:80)
```
- **MySQL**:
    * To run `MySQL`:
        ```sh
        docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
        ```
    * View logs to see generated random password for the `root` user. To view logs:
        ```sh
        docker container logs db # 'db' is the name we have given in above command.
        ```
    * Look for something like below line for the generated random password:
        ```
        2020-03-14 12:20:33+00:00 [Note] [Entrypoint]: GENERATED ROOT PASSWORD: ChooHxafdsasd2dsx1ouovo7aegha
        ```
- **httpd (Apache Server)**:
    * To run `httpd`:
        ```sh
        docker container run -d -p 8080:80 --name webserver httpd
        ```
- **nginx**:
    * To run `nginx`:
        ```sh
        docker container run -d -p 80:80 --name proxy nginx
        ```
- All containers are running by now. To list all running containers:
    ```sh
    docker container ls
    # OR
    docker ps   # Old command
    ```
- To clean these containers up:
    ```sh
    docker container stop   # Press TAB to get a list of all running containers
    # OR
    docker container stop proxy webserver db
    ```
- To remove these containers:
    ```sh
    docker container ls -a  # This will give list of all containers, even stopped ones.

    # To remove containers, specify their ids like below:
    docker container rm b520f9b00f89 5eaa2a2b09c6 c782914b7c66
    ```
- To remove `Images` as well:
    ```sh
    # To remove images, specify their ids like below:
    docker image rm b520f4389 5eaa22b09c6 c782432b7c66
    ```

```diff
+ To clean up apt-get cache
```
- By cleaning up `apt-get` cache in Containers, we get to keep our Image size small.
- It's a best practice to clear up `apt-get` cache once the required packages are installed.
- Following command cleans up `apt-get` cache and it is used across many popular Images same way:
    ```sh
    rm -rf /var/lib/apt/lists/*
    ```
- **FOR EXAMPLE:** After installing `git` in Image, we should clean up `cache` to save almost `10mb` space:
    ```sh
    # Below command installs 'git' and clears cache after installation.
    RUN apt-get update && apt-get install -y git \
    && rm -rf /var/lib/apt/lists/*
    ```

```diff
+ To get a Shell inside Container
```
- To start new Container interactively:
    ```sh
    docker container run -it
    ```
- To run additional command in existing container:
    ```sh
    docker container exec -it
    ```
- For e.g. To start a `httpd` container interactively and get a `bash` shell inside it:
    ```sh
    docker container run -it --name webserver httpd bash
    ```
- For e.g. To get a `bash` shell inside already running `nginx` Container named as `proxy`:
    ```sh
    docker container exec -it proxy bash
    ```

```diff
+ To create a temp POD in cluser and get an interactive shell in it
```
- This command will create a temporary `POD` in a running cluser and launch an interactive shell inside it.
- **NOTE:** This temporary `POD` will be deleted once we exit out of the shell.
    ```sh
    kubectl run --generator run-pod/v1 tmp-shell --rm -it --image bretfisher/netshoot -- bash
    ```

```diff
+ Docker Swarm - Create Our First Service and Scale it Locally
```
- To create a Docker Swarm service and scale it locally, following are the useful commands:
    ```sh
    docker info
    docker swarm init
    docker node ls
    docker node --help
    docker swarm --help
    docker service --help
    docker service create alpine ping 8.8.8.8
    docker service ls
    docker service ps frosty_newton
    docker container ls
    docker service update TAB COMPLETION --replicas 3
    docker service ls
    docker service ps frosty_newton
    docker update --help
    docker service update --help
    docker container ls
    docker container rm -f frosty_newton.1.TAB COMPLETION
    docker service ls
    docker service ps frosty_newton
    docker service rm frosty_newton
    docker service ls
    docker container ls
    ```

```diff
+ Creating a 3-Node Swarm Cluster
```
- To create a 3-Node Swarm Cluster, following are the useful commands:
    ```sh
    # http://play-with-docker.com
    docker info
    docker-machine
    docker-machine create node1
    docker-machine ssh node1
    docker-machine env node1
    docker info
    # http://get.docker.com
    docker swarm init
    docker swarm init --advertise-addr TAB COMPLETION
    docker node ls
    docker node update --role manager node2
    docker node ls
    docker swarm join-token manager
    docker node ls
    docker service create --replicas 3 alpine ping 8.8.8.8
    docker service ls
    docker node ps
    docker node ps node2
    docker service ps sleepy_brown
    ```

```diff
+ Scaling Out with Overlay Networking
```
- Following set of commands orchestrate scaling out with overlay networking:
    ```sh
    docker network create --driver overlay mydrupal
    docker network ls
    docker service create --name psql --netowrk mydrupal -e POSTGRES_PASSWORD=mypass postgres
    docker service ls
    docker service ps psql
    docker container logs psql TAB COMPLETION
    docker service create --name drupal --network mydrupal -p 80:80 drupal
    docker service ls
    watch docker service ls
    docker service ps drupal
    docker service inspect drupal
    ```

```diff
+ Scaling Out with Routing Mesh
```
- Following set of commands orchestrate scaling out with Routing Mesh:
    ```sh
    docker service create --name search --replicas 3 -p 9200:9200 elasticsearch:2
    docker service ps search
    ```

```diff
+ Create a Multi-Service Multi-Node Web App
```
- Following set of commands orchestrate creation of a Multi-Service Multi-Node Web App:
    ```sh
    docker node ls
    docker service ls
    docker network create -d overlay backend
    docker network create -d overlay frontend
    docker service create --name vote -p 80:80 --network frontend -- replica 2 COPY IMAGE
    docker service create --name redis --network frontend --replica 1 redis:3.2
    docker service create --name worker --network frontend --network backend COPY IMAGE
    docker service create --name db --network backend COPY MOUNT INFO
    docker service create --name result --network backend -p 5001:80 COPY INFO
    docker service ls
    docker service ps result
    docker service ps redis
    docker service ps db
    docker service ps vote
    docker service ps worker
    cat /etc/docker/
    docker service logs worker
    docker service ps worker
    ```

```diff
+ Swarm Stacks and Production Grade Compose
```
- Following set of commands demonstrate Swarm Stacks and Production Grade Compose:
    ```sh
    docker stack deploy -c example-voting-app-stack.yml voteapp
    docker stack
    docker stack ls
    docker stack ps voteapp
    docker container ls
    docker stack services voteapp
    docker stack ps voteapp
    docker network ls
    docker stack deploy -c example-voting-app-stack.yml voteapp
    ```

```diff
+ Using Secrets in Swarm Services
```
- Useful commands:
    ```sh
    docker secret create psql_usr psql_usr.txt
    echo "myDBpassWORD" | docker secret create psql_pass - TAB COMPLETION
    docker secret ls
    docker secret inspect psql_usr
    docker secret create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres
    docker service ps psql
    docker exec -it psql.1.CONTAINER NAME bash
    docker logs TAB COMPLETION
    docker service ps psql
    docker service update --secret-rm
    ```

```diff
+ Using Secrets with Swarm Stacks
```
- Useful commands:
    ```sh
    vim docker-compose.yml
    docker stack deploy -c docker-compose.yml mydb
    docker secret ls
    docker stack rm mydb
    ```

```diff
+ Create A Stack with Secrets and Deploy
```
- Useful commands:
    ```sh
    vim docker-compose.yml
    docker stack deploy - c docker-compose.yml drupal
    echo STRING |docker secret create psql-ps - VALUE
    docker stack deploy -c docker-compose.yml drupal
    docker stack ps drupal
    ```

```diff
+ Service Updates: Changing Things In Flight
```
- Useful commands:
    ```sh
    docker service create -p 8088:80 --name web nginx:1.13.7
    docker service ls
    docker service scale web=5
    docker service update --image nginx:1.13.6 web
    docker service update --publish-rm 8088 --publish-add 9090:80 web
    docker service update --force web
    ```

```diff
+ Healthchecks in Dockerfile
```
- Useful commands:
    ```sh
    docker container run --name p1 -d postgres
    docker container ls
    docker container run --name p2 -d --health-cmd="pg_isready -U postgres || exit 1" postgres
    docker container ls
    docker container inspect p2
    docker service create --name p1 postgres
    docker service create --name p2 --health-cmd="pg_isready -U postgres || exit 1" postgres
    ```

----------------------------------------
