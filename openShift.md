# Differences Between ReplicaSet and ReplicaSet Controller in OpenShift

In OpenShift (built on Kubernetes), **ReplicaSets** and **ReplicaSet controllers** are closely related but serve distinct roles. This document explains the differences between **ReplicaSet** and **ReplicaSet controller** in both Kubernetes and OpenShift, as well as how OpenShift offers an equity-based approach through the **DeploymentConfig**.

## 1. Kubernetes ReplicaSet Controller (Set-Based)

A **ReplicaSet** is a Kubernetes resource that ensures a specified number of pod replicas (identical copies of a pod) are running at any given time.

- **Primary Function**: It manages the deployment of pods and ensures that the desired number of replicas of a pod are running.
- **How it Works**: If a pod fails (e.g., crashes or is deleted), the ReplicaSet automatically creates new pods to replace the failed ones, maintaining the desired count.
- **Use Case**: While you can use ReplicaSets directly to manage pods, they are typically used in the context of a **Deployment** resource to manage and scale the pods effectively.

**Example of a ReplicaSet**:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: myapp-image:latest
```

# Differences Between Kubernetes ReplicaSet and OpenShift DeploymentConfig

This section compares the differences between **Kubernetes ReplicaSet** and **OpenShift DeploymentConfig** in terms of functionality, deployment strategies, and use cases.

## Key Differences

| Feature                          | Kubernetes ReplicaSet                | OpenShift DeploymentConfig          |
|-----------------------------------|--------------------------------------|-------------------------------------|
| **Management**                    | Set-based, only ensures pod replicas | Equity-based, focuses on gradual, safe updates |
| **Rolling Updates**               | No built-in support                  | Supports rolling updates, configurable |
| **Version Management**            | No version management                | Tracks versions and controls updates |
| **Update Strategy**               | Direct scaling (set-based)           | Rolling updates, canary deployments, controlled scaling |
| **Use Case**                      | Simple replica management            | Advanced deployment with control over lifecycle and updates |

## Summary:

- **Kubernetes ReplicaSet**: 
    - Focuses on maintaining a fixed number of identical pods. 
    - If a pod fails, a new one is created.
    - Does not have built-in support for managing updates or rolling out new versions of pods.
  
- **OpenShift DeploymentConfig**: 
    - Uses an **equity-based** approach to ensure long-term stability of application deployment.
    - Provides advanced strategies like **rolling updates** and **canary deployments**.
    - Allows for controlled, gradual updates, with a focus on balancing the new and old versions of the application to minimize disruptions.

## Conclusion

In Kubernetes, **ReplicaSets** are a basic tool that ensures the desired number of identical pods are running, but it does not offer advanced features for managing updates or pod lifecycles over time. 

In contrast, **OpenShift DeploymentConfig** offers a more flexible, **equity-based** approach, supporting advanced deployment strategies such as **rolling updates**, **canary deployments**, and fine-grained control over pod scaling and updates.

# S2I (Source-to-Image) Overview

**S2I (Source-to-Image)**, a system used in OpenShift to transform application source code into a container image. Here's a summary of the key points covered:

## 1. What is S2I?
- **S2I** stands for **Source-to-Image**. It is a system in OpenShift that takes your source code and creates a container image out of it. The process is driven by scripts bundled together in a **builder image**.

## 2. How does S2I work?
- There are two critical scripts involved in S2I:
  - **Assemble script**: This script is responsible for transforming the source code into a runnable image, similar to the `RUN` command in a Dockerfile.
  - **Run script**: This is equivalent to the `CMD` instruction in a Dockerfile. It is the command that the container will execute when it starts.

## 3. Why use S2I?
- **OpenShift compatibility**: Developers can trust the expertise of the S2I authors to ensure the image is OpenShift-compatible.
- **No need to manage Dockerfiles**: Developers don’t need to write or maintain Dockerfiles themselves, as S2I comes with sensible defaults.
- **Pre-built builder images**: OpenShift provides a variety of builder images for popular programming languages like Node.js, Python, Ruby, and Java.
- **Customization**: S2I allows for customization of builder images, or even creating custom ones.
- **Standardization**: Large organizations benefit from S2I because it helps standardize the toolchain, preventing the need for each team to manage their own Dockerfiles.


# Building containers

# Build an image based on the current directory
docker build .

# Build an image based on the current directory with a tag
docker build -t your-tag .


# Running Containers

# Check the image storage
docker images

# Start a container based on an image ID. Get the ID from docker images.
# control-c will stop the container for all of these docker run commands.
docker run -it <your-image-id>

# Start an image based on a tag
docker run -it <image tag>

# Start hello-world server
docker run -it quay.io/practicalopenshift/hello-world

# Start the Hello World app with port forwarding
docker run -it -p 8080:8080 quay.io/practicalopenshift/hello-world


# Stopping Containers

# Get running images
docker ps

# Stop a running image. The container ID will be in the docker ps output.
docker kill <Container ID>

# Log in, log out

# Uses the pre-configured OpenShift cluster
``` oc  login ```

# Allows you to log in to any OpenShift cluster
``` oc  login <cluster address> ```

# Log out
``` oc  logout ```


# Project Basics

# See current project
``` oc  project ````

# Create a new project
``` oc  new-project demo-project ```

# List all projects
``` oc  projects  ```

# Switch projects
``` oc  project <project name> ```
# Get Pod Documentation

# Get built-in documentation for Pods
``` oc  explain pod ```

# Get details on the pod's spec
``` oc  explain pod.spec  ```

# Get details on the pod's containers
``` oc  explain pod.spec.containers ```


# Creating Pods from files

# Create a Pod on OpenShift based on a file
``` oc  create -f pods/pod.yaml ```

# Show all currently running Pods
``` oc  get pods ```


# Port forwarding for Pods

# Open a local port that forwards traffic to a pod
``` oc  port-forward <pod name> <local port>:<pod port> ```

# Example of 8080 to 8080 for hello world
``` oc  port-forward hello-world-pod 8080:8080 ```


# Shell into Pods

# ``` oc  rsh will work with any Pod name from ``` oc  get pods
``` oc  rsh <pod name>

# In the shell, check the API on port 8080
``` wget localhost:8080

# Exit the rsh session
exit
```

# Watch live updates to pods
``` oc  get pods --watch ```


# Delete (stop) Pods

# Delete any OpenShift resource
``` oc  delete <resource type> <resource name> ```

# Delete the pod for this section
``` oc  delete pod hello-world-pod ```


# Deploying applications as DeploymentConfigs

## Deploy an existing image based on its tag
```
oc  new-app <image tag> \
  --as-deployment-config
 ```

# Deploy the Hello World image for this course
```
oc  new-app quay.io/practicalopenshift/hello-world \
  --as-deployment-config
```

# Deploy from Git using ``` oc  new-app
``` oc  new-app <git repo URL> \
  --as-deployment-config
```

# Deploy the Hello World application from Git
``` oc  new-app https://gitlab.com/practical-openshift/hello-world.git \
  --as-deployment-config
```
# Follow build progress (Git only)
``` oc  logs -f bc/hello-world
```
# Set the name for the DeploymentConfig 
``` oc  new-app <image tag> --name <desired name> \
  --as-deployment-config
```
# Example with a name
``` oc  new-app quay.io/practicalopenshift/hello-world \
  --name demo-app \
  --as-deployment-config
```
# Get more information about a DeploymentConfig

# Describe the DC to get its labels
``` oc  describe dc/hello-world
```
# Get the full YAML definition
``` oc  get -o yaml dc/hello-world
```

# Deleting all ``` oc  new-app resources

# Delete all application resources using labels (get them from ``` oc  describe)
``` oc  delete all -l app=hello-world
```

# Starting new versions and reverting changes

# Roll out the latest version of the application
``` oc  rollout latest dc/hello-world
```
# Roll back to the previous version of the application
``` oc  rollback dc/hello-world ```
# Trigger management
# Both ImageChange and ConfigChange triggers are enabled by default

# List triggers
``` oc  set triggers dc/<dc name>
```
# Remove the ConfigChange trigger
``` oc  set triggers dc/<dc name> \
  --remove
  --from-config
```
# Re-add the ConfigChange trigger
``` oc  set triggers dc/<dc name> --from-config
```
# Remove the ImageChange trigger
``` oc  set triggers dc/<dc name> \
  --remove \
  --from-image <image name>:<tag>
```
# Re-add the ImageChange trigger
# You need to pick a container in your pod spec that corresponds to the image in --from-image
``` oc  set triggers dc/<dc name> \
  --from-image <image name>:<tag> \
  -c <container name>
```

# Deployment Hooks

# General syntax
``` oc  set deployment-hook dc/<dc name> \
  (--pre, --post, or --mid) \
  -c <container name to execute hook in>
  -- <command to execute for the hook>
```
# Example: Add a simple deployment hook
``` oc  set deployment-hook dc/hello-world \
  --pre \
  -c hello-world \
  -- /bin/echo Hello from pre-deploy hook
```
# Check the hook in the DeploymentConfig definition
``` oc  describe dc/hello-world
```

# Switching to the Recreate Strategy
# No ``` oc  set deployment-strategy as of writing, so you'll need to manually update the resource definition

# Start editing the DeploymentConfig
``` oc  edit dc/hello-world ``

# To change to Recreate, switch the spec.strategy to be:

  strategy:
    type: Recreate


# Readiness and Liveness probes

# General syntax
``` oc  set probe dc/<dc name> (--liveness or --readiness) (--open-tcp, --get-url, or -- for a command) ```

# Example: Add a liveness probe that opens TCP port 8080 for its test
``` oc  set probe dc/hello-world --liveness --open-tcp=8080  ```

# Example: Add a readiness probe that requests localhost port 8080 with the path /health/readiness for its test
``` oc  set probe dc/hello-world --readiness --get-url=http://:8080/health/readiness ```

# Example: Add a readiness probe that runs "exit 0" inside the container as its test
``` oc  set probe dc/hello-world --readiness -- exit 0 ```



# Creating new BuildConfigs

# Create a new BuildConfig from a Git repository URL
``` oc  new-build <Git URL> ```

# Example
``` oc  new-build https://gitlab.com/practical-openshift/hello-world.git ```

# Start a new build from the update-message branch
``` oc  new-build https://gitlab.com/practical-openshift/hello-world.git#update-message ```

# Use --context-dir to build from a subdirectory
``` oc  new-build https://gitlab.com/practical-openshift/labs.git --context-dir hello-world ```


# Working with existing BuildConfigs

# Start a build
``` oc  start-build bc/hello-world ```

# Get logs for a single build
``` oc  logs -f build/hello-world-1 ```

# Get logs for the latest build for a BuildConfig
# This is the best way (usually)
``` oc  logs -f bc/hello-world ```

# Cancel a running build
``` oc  cancel-build bc/hello-world ```

# Get more information about the build
``` oc  get -o yaml buildconfig/hello-world ```

# See builds that have run
``` oc  get build ```

# Start a build for an existing BuildConfig
``` oc  start-build bc/hello-world ```


# Set build hooks

# Set a post-commit hook
``` oc  set build-hook bc/hello-world \
  --post-commit \
  --script="echo Hello from build hook"
 ```

# Check the logs output for "Hello from build hook"
``` oc  logs -f bc/hello-world ```

# Set a failing build hook to observe the behavior
``` oc  set build-hook bc/hello-world \
  --post-commit \
  --script="exit 1" ````
```
# Check the events to see if it ran
``` oc  get events
```
# Remove the build hook
``` oc  set build-hook bc/hello-world \
  --post-commit \
  --remove

# See all of your pods
``` oc  get pods
```

# Working with WebHooks

# Get the secret token
``` oc  get -o yaml buildconfig/hello-world
```
# Export the secret as a variable
export GENERIC_SECRET=<generic token from previous command>

# Get the webhook URL
``` oc  describe buildconfig/hello-world
```
# Copy the webhook URL and replace <secret> with $GENERIC_SECRET
``` curl -X POST -k <webhook URL with secret replaced with $GENERIC_SECRET>
```

# Creating ConfigMaps

# Create a ConfigMap using literal command line arguments
``` oc  create configmap <configmap-name> --from-literal KEY="VALUE" ```

# Create from a file
``` oc  create configmap <configmap-name> --from-file=MESSAGE.txt ```

# Create from a file with a key override
``` oc  create configmap <configmap-name> --from-file=MESSAGE=MESSAGE.txt ```

# Same --from-file but with a directory
``` oc  create configmap <configmap-name> --from-file pods ```

# Verify
``` oc  get -o yaml configmap/<configmap-name> ```


# Consuming ConfigMaps as Environment Variables

# Set environment variables (same for all types of ConfigMap)
``` oc  set env dc/hello-world --from cm/<configmap-name> ```

# Creating Secrets

# Create a simple generic (Opaque) Secret
``` oc  create secret generic <secret-name> --from-literal KEY="VALUE" ```

# Check the Secret
``` oc  get -o yaml secret/<secret-name> ```
 

# Consume the Secret as Environment Variables

# Almost the same as ConfigMaps
``` oc  set env dc/<dc-name> --from secret/<secret-name> ``` 

# Create ImageStreams

# Create the ImageStream (but don't deploy yet)
``` oc  import-image --confirm <image tag> ```

# Example with this course's image
``` oc  import-image --confirm quay.io/practicalopenshift/hello-world ```

# Importing any new images
``` oc  import-image --confirm quay.io/practicalopenshift/hello-world ```


# Importing extra ImageStreamTags for an existing ImageStream

# ``` oc  tag syntax
``` oc  tag <original> <destination> ```

# Example
``` oc  tag quay.io/image-name:tag image-name:tag ```


# Check the current ImageStreams and ImageStreamTags

# List ImageStreams
``` oc  get is ```

# List tags
``` oc  get istag ```


# Use the ImageStream with ``` oc  new-app ```

# Deploy an application based on your new ImageStream
``` oc  new-app myproject/hello-world ```


# Creating and pushing a private image
# These require signing up for a Quay.io account and pushing a private image

# Remote Tag syntax
<host name>/<your username>/<image name>

# Building an image with a remote tag
``` docker build -t quay.io/$REGISTRY_USERNAME/private-repo . ```

# Log into a registry
`` docker login <hostname>```
 
# Log into quay.io
```docker login quay.io ```

# Push (send) an image to a remote registry
``` docker push <remote tag> ```

# Push the image to Quay
``` docker push quay.io/$REGISTRY_USERNAME/private-repo ```


# Use Private images with OpenShift

# You may need to run this command 
``` source credentials.env ```

# Create a Docker registry secret
``` oc  create secret docker-registry \
  <secret name> \
  --docker-server=$REGISTRY_HOST \
  --docker-username=$REGISTRY_USERNAME \
  --docker-password=$REGISTRY_PASSWORD \
  --docker-email=$REGISTRY_EMAIL
 ```

# A touch of secrets magic
# This command links the secret to the service account named "default"
``` oc  secrets link default <secret name> --for=pull ```

# Check that the service account has the secret associated
``` oc  describe serviceaccount/default ```

# Once authentication is set up, start the application 
``` oc  new-app quay.io/$REGISTRY_USERNAME/private-repo \
  --as-deployment-config
 ```

# Get service documentation

# Access ``` oc  explain documentation
``` oc  explain service

# Get more information about Service's spec
``` oc  explain service.spec
```
# Get YAML definition for a service
``` oc  get -o yaml service/hello-world
```
# Get YAML definition for a route
``` oc  get -o yaml route/hello-world
```

# Creating services

# Create a service for a single pod
``` oc  expose --port 8080 pod/hello-world-pod
```
# Create a service for a DeploymentConfig 
``` oc  expose --port 8080 dc/hello-world
```
# Check that the service and pod are connected properly
``` oc  status
```

# Using Pod environment variables to find service Virtual IPs

# Inside the pod, get all environment variables
```env```

# Use the environment variables with wget
```wget -qO- $HELLO_WORLD_POD_PORT_8080_TCP_ADDR:$HELLO_WORLD_POD_PORT_8080_TCP_PORT
```

# Creating Routes

# Create a Route based on a Service
``` oc  expose svc/hello-world

# Get the Route URL
``` oc  status```

# Check the route
```curl <route from ``` oc  status>```


# Use S2I in a build
# The syntax is the same as normal Builds. OpenShift uses S2I when there is no Dockerfile

# ``` oc  new-app works with S2I 
``` oc  new-app <Git URL with no Dockerfile> \
  --as-deployment-config
```
# ``` oc  new-build works with S2I 
``` oc  new-build <Git URL with no Dockerfile>
```
# Example: build the s2i/ruby directory of the labs project
``` oc  new-app https://gitlab.com/practical-openshift/labs.git \
  --context-dir s2i/ruby \
  --as-deployment-config
```

# Specifying a builder image
``` oc  new-app builder-image~<Git URL> \
  --as-deployment-config
```

# Example: Deploy with the ruby image explicitly declared
``` oc  new-app \
  ruby~https://gitlab.com/practical-openshift/labs.git \
  --context-dir s2i/ruby \
  --as-deployment-config
```


# Overriding S2I Scripts
# Assemble and Run are the two main scripts
# Overrides go in your source at .s2i/bin/assemble or .s2i/bin/run
# They need to call the original scripts, which are usually at /usr/libexec/s2i/assemble or /usr/libexec/s2i/run


# Manual Scaling

# General Syntax
``` oc  scale dc/<dc name> --replicas=<desired replicas>
```
# Example: Manual scale to 3 pods
``` oc  scale dc/hello-world --replicas=3
```
# Example: Scale back down to one
``` oc  scale dc/hello-world --replicas=1
```

# Autoscaling

# General Syntax to create a HorizontalPodAutoscaler (HPA)
``` oc  autoscale dc/<dc name> \
  --min <desired minimum pods> \
  --max <desired maximum pods> \
  --cpu-percent=<desiredTargetCPU>
```
# Example of scaling Hello World between 1 and 10 pods with an 80% CPU target
``` oc  autoscale dc/hello-world \
  --min 1 \
  --max 10 \
  --cpu-percent=80
```
# Check the HPA
``` oc  get hpa
```
# More information on the HPA
``` oc  describe hpa/hello-world
```
# Get the YAML for the HPA
``` oc  get -o yaml hpa/hello-world
```

# Mount an emptyDir volume

# Main syntax
``` oc  set volume dc/<dc name> --add --type emptyDir --mount-path <path inside container>
```
# Example:Add an emptyDir volume
``` oc  set volume dc/hello-world \
  --add \
  --type emptyDir \
  --mount-path /empty-dir-demo
```

# Mount ConfigMaps as volumes

# Main command
``` oc  set volume <DC name> --add --configmap-name <configmap name> --mount-path <path inside container>
```
# Example: Create the configmap to use as a Volume
``` oc  create configmap cm-volume \
  --from-literal file.txt="ConfigMap file contents"
```
# Example: Mount the ConfigMap
``` oc  set volume dc/hello-world \
  --add \
  --configmap-name cm-volume \
  --mount-path /cm-directory

```
# Using other Volume Suppliers
# There are a wide variety of suppliers
# oc  explain and the online documentation are both very helpful

# The official Kubernetes Documentation for Volumes
https://kubernetes.io/docs/concepts/storage/volumes/

# Check out the built-in documentation
``` oc  explain persistentvolume.spec```
# Manage templates as OpenShift resources

# Create the template from the file
``` oc  create -f template/hello-world-template.yaml```

# Check the template
``` oc  get template```

# Create an application based on the template
``` oc  new-app hello-world```


# Set parameter values

``` oc  new-app hello-world \
  -p MESSAGE="Hello from parameter override."


# Process templates

# Basic processing (gives you JSON)
``` oc  process hello-world```

# Get the processed results in YAML
``` oc  process hello-world -o yaml```

# With parameters
``` oc  process hello-world -o yaml \
  -p MESSAGE="Hello from ``` oc  process" ```

# Save the processed template to a file
``` oc  process hello-world -o yaml \
  -p MESSAGE="Hello from ``` oc  process" \
  > processed-objects.yaml
```

# Check the file
head processed-objects.yaml

# Create the objects
``` oc  create -f processed-objects.yaml ```



# Use a template file

``` oc  process -o yaml -f <template file>```

# Use a file-based template
``` oc  process -o yaml \
  -f template/hello-world-template.yaml ```

# Example with ``` oc  new-app and a parameter
``` oc  new-app \
  -f template/hello-world-template.yaml
  -p MESSAGE="Hello from ``` oc  new-app with a file"
```

# Creating your own Template

# Get YAML for existing objects on the OpenShift server
# The dc,is... syntax lists the types of resources that you would like to export
# Add hpa or any other type if you need them
``` oc  get -o yaml dc,is,bc,svc,route

# Save output to a file
``` oc  get -o yaml dc,is,bc,svc,route \
  > test-template.yaml
```
# Open it up in your favorite text editor
```vi test-template.yaml```

Steps for a custom template:
1. Change the items property to objects
2. Change kind from List to Template
3. Add a name property to the metadata section
4. Remove status from each resource
5. Remove most of metadata except for name, labels, and annotations
6. Remove any automatically-assigned resources such as service Virtual IPs and Route hosts
7. (optional) Add template parameters 

# Example parameter definition
- description: Message to respond to requests with
  displayName: Message
  name: MESSAGE
  required: false
  value: Hello from the default value for the template

# Using the parameter in your template YAML
          env:
            - name: MESSAGE
              # This syntax copies the template parameter value as a YAML string
              value: ${MESSAGE}


