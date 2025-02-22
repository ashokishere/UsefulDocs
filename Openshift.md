In OpenShift, you can create container images in several ways. The most common methods are:

### 1. Using Source-to-Image (S2I)
S2I is a framework that converts source code into a container image. OpenShift automatically builds the application and packages it into an image.

Steps:
Login to OpenShift

```sh
oc login <openshift-cluster-url>
```
Create a new project (if not already created)

```sh

oc new-project myproject
```

Use oc new-app to create an application

``` sh
oc new-app <builder-image>~<source-code-url>
```

Example:

```sh
oc new-app nodejs~https://github.com/sclorg/nodejs-ex.git
```
This will:

Pull the builder image (e.g., nodejs)
Clone the source code from the provided Git repository
Build and create an image automatically
Check the build status

``` sh
oc logs -f bc/nodejs-ex
```
Expose the application
 
``` sh
 
oc expose svc/nodejs-ex
```
Get the application URL

```
oc get route
```

### 2. Using Docker Build (BuildConfig)
If you have a Dockerfile, you can build the image directly inside OpenShift.

Steps:
Create a BuildConfig
```
oc new-build --binary --name=myapp
```

Start a binary build

``` sh
oc start-build myapp --from-dir=. --follow
```

Deploy the image

``` sh
oc new-app myapp
```

Expose the service

``` sh
oc expose svc/myapp
````

### 3. Using OpenShift Image Streams
Instead of manually pulling images, OpenShift Image Streams allow you to track and automatically update to newer versions of an image.

Steps:
Create an ImageStream

``` sh
oc create imagestream myapp
```
Use the ImageStream in a BuildConfig

``` sh
oc new-build --name=myapp --image-stream=openshift/python:3.9 --binary
```
Start the build

``` sh
oc start-build myapp --from-dir=. --follow
```

Deploy the application

``` sh
oc new-app myapp
```
### 4. Using an External Docker Registry
You can build an image outside OpenShift and then push it to an OpenShift-integrated registry.

Steps:
Login to OpenShift

``` sh
oc login
```
Get the OpenShift registry URL

``` sh
oc registry info
```

Tag the image

``` sh
docker tag myimage:latest <openshift-registry>/myproject/myimage
```
Login to the OpenShift registry

``` sh
docker login -u $(oc whoami) -p $(oc whoami -t) <openshift-registry>
```

Push the image

``` sh
docker push <openshift-registry>/myproject/myimage
```
Create a deployment using the pushed image

``` sh
oc new-app <openshift-registry>/myproject/myimage
```

Use S2I for automated builds from source code.

Use Docker BuildConfig for manual builds with a Dockerfile.

Use ImageStreams to track image updates.

Use an external registry if you're building the image externally.
