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
- [Generic Examples](#generic-examples)

----------------------------------------

## Must Check Links
- How DNS works? DNS basics:
    * [https://howdns.works](https://howdns.works)
    * [https://dyn.com/blog/dns-why-its-important-how-it-works](https://dyn.com/blog/dns-why-its-important-how-it-works)
- Round-Robin DNS, what is it:
    * [https://en.wikipedia.org/wiki/Round-robin_DNS](https://en.wikipedia.org/wiki/Round-robin_DNS)
- The Cloud Native Trail Map is CNCF's recommended path through the cloud native landscape. The cloud native landscape, serverless landscape, and member landscape are dynamically generated on this website:
    * [https://landscape.cncf.io](https://landscape.cncf.io)
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

----------------------------------------

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

----------------------------------------
