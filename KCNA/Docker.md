Differences Between Docker and Docker Desktop

Docker was originally released back in 2013. Traditionally, Docker runs on the following stack:

Hardware: This could be physical or virtualized hardware with virtualization enabled.
Operating System: Requires a minimum kernel version of 3.1 or greater, which any modern Linux distribution should meet.
Docker Installation: Sets up the container runtime that uses containerd and runc to run containers.
CLI: Conveniently run and build containers.

Docker Desktop

Docker Inc. created Docker Desktop as a friendly solution for common operating systems like macOS, Windows, and Linux desktops. 

Docker Desktop also provides:

A friendly user interface
An inbuilt Kubernetes server
Docker Desktop Extensions, which allow developers to bundle Docker-based applications quickly

Architectural Viewpoint

Docker Desktop uses a hidden virtual machine or subsystem to run an isolated instance of Docker. Depending on your OS and its version and
architecture, Docker Desktop will use different virtualization technologies to create this hidden virtual machine or subsystem.
This isolated instance runs a Linux OS with the Docker runtime, providing a Docker CLI and UI, as well as transparent networking 
between your host system and Docker.

Docker Desktop's segmented environment provides flexibility, such as easy environment reset options, making it great for learning and experimenting.

Installation Steps

macOS

Download Docker Desktop: Visit Docker.com, navigate to the Docker Desktop section, and download the installer for your system. 
Choose between Intel Chip or Apple Chip (Apple Silicon) based on your system.
Install Docker Desktop: Open the downloaded installer and drag Docker to Applications. Then, open Docker using Spotlight for convenience.
Complete Installation: Follow the tutorial if you're new to Docker. Otherwise, skip it and ensure Docker is running 
(check the bottom left corner for a green Docker icon).

Windows

Download Docker Desktop: Visit Docker.com and download the installer for Windows.
Run the Installer: Follow the prompts and reboot if necessary.
Update WSL: If prompted, open a command prompt and run wsl --update.

Complete Installation: Open Docker Desktop and ensure it's running (check the bottom left corner for a green Docker icon).

Running Containers

macOS Example

Open Terminal: Open a terminal window.

Run a Container: Execute the following command to run an interactive Ubuntu container:

```bash
docker run -it ubuntu bash
```

The system will download the Ubuntu image and start a container with the bash shell.

Windows Example

Open Command Prompt: Open a command prompt window.

Run a Container: Execute the following command to run an interactive Ubuntu container:
```bash

Copy code
docker run -it ubuntu bash
```

Kubernetes Setup

Enable Kubernetes: Go to Docker Desktop preferences, select the Kubernetes pane, and enable Kubernetes.
Verify Setup: Open a terminal or command prompt and run:

```bash
Copy code
kubectl get nodes
```

What is a Container Image?

A container image is a portable, self-contained bundle of software and dependencies, allowing us to run software consistently across 
different compute environments. Sometimes you'll hear them referred to as Docker images, but a more accurate term is 
OCI (Open Container Initiative) compliant container images. These images can be created with Docker or any other OCI-compliant tool, 
and they can be used in Docker, Kubernetes, or any platform that supports OCI container images.


Difference Between a Container Image and a Container

A container image is a bundle of software, while a container is an instance of that software running. For example, you can have a single 
container image of nginx and run multiple independent instances of the nginx web server from that one container image.

Container Registries

Container images are hosted and shared using container registries. Docker Hub is a popular cloud-based registry for hosting and
distributing container images.

Container Image Tags

Tags are labels used to distinguish versions of a container image. For example, you can use tags to specify different versions or operating 
systems of your container images. The latest tag is a convenient default tag used when a specific tag is not specified.

Container Layers

Container images are made up of layers. Each step in creating a container image results in a new layer. These layers are stacked on top of 
each other to form the final image. When you run a container, Docker uses a union file system to merge these layers into a single view. 
This approach is storage efficient because multiple containers running from the same image share the underlying layers, with only a thin,
writable layer on top for any changes.

Pulling a Container Image

Let's pull a container image from Docker Hub using the funbox example:


Open a terminal.
Run the pull command:

```bash
docker pull funbox/funbox:latest
```

This will download the image and its layers.

Union File Systems
A union file system merges the layers of a container image into a single view. When running a container, changes are written to a thin, 
writable layer on top of the read-only layers. This means deleting a file from a running container only removes it from the writable layer's
perspective, while it still exists in the lower read-only layers.

Container Image Digests and Image IDs

A digest is a secure, unique identifier for an image from the container registry, calculated as a SHA-256 hash of the image's manifest.
This digest allows you to verify the image's integrity. The image ID is a checksum based on the local container image's JSON configuration.

Viewing and Using Image Digests

To pull an image by its digest:

```bash

docker pull funbox/funbox@sha256:<digest>
```

You can view local images and their digests with:

```bash
Copy code
docker images --digests
```

Understanding Image IDs

Image IDs are checksums of the local JSON configuration used by Docker. You can save an image locally with docker save,
extract it, and view the internal JSON configuration to see the details used to calculate the image ID.
 
 
