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
    ```diff
    + Installing on Windows 10 (Pro or Enterprise)
    + Installing on Windows 7, 8, or 10 Home Edition
    + Installing on Mac
    + Installing on Linux
    + Play With Docker (PWD) Online
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
- [Generic Examples](#generic-examples)
    ```diff
    + Running 3 Containers: nginx (80:80), mysql (3306:3306), httpd (Apache Server - 8080:80)
    + To clean up apt-get cache
    + To get a Shell inside Container
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

----------------------------------------
