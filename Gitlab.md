
Summary of all Git repositories, I use during the course. You can use the git repositories as a reference or fork to follow along.



Starting from chapter 2:

Simple demo Node.js project: https://gitlab.com/nanuchi/mynodeapp-cicd-project


Starting from chapter 7 (Microservices):

Microservice mono-repo: https://gitlab.com/nanuchi/mymicroservice-cicd
Microservice poly-repo: https://gitlab.com/mymicroservice-cicd
CI-templates (in the poly-repo group): https://gitlab.com/mymicroservice-cicd/ci-templates

# Create Cluster in Linode

<img width="1647" alt="image" src="https://github.com/ashokishere/UsefulDocs/assets/46769524/37c3d71e-fbaa-4a9f-9590-014b3c82a7c0">

#Update the config file

Create a admin user by default and uses a token based mechanism
• Permissions to define what the ServiceAccount is allowed to do inside the cluster
• Admin user wide privileges

chmod 400 ~/Downloads/my-micro-service-kubeconfig.yaml
export KUBECONFIG=~/Downloads/my-micro-service-kubeconfig.yaml

Security Best Practice

• Give user only the permissions it needs
• If someone hacked into GitLab, they would have full access to K8s cluster!

1) Create a dedicated User (ServiceAccount) for GitLab sa
2) Create restricted permissions (Role)
3) Generate kubeconfig file for ServiceAccount


Create a less privileged user, create a role and permission and associate a role binding  and Generate a kubecofig file for that user

When a serice account is created, a secret  reource is created which has the token Info

echo token | base64 D
name can be anthing, token should be base64 converted, update the username  in the contex section

Add the Config.ymal content to

<img width="753" alt="image" src="https://github.com/ashokishere/UsefulDocs/assets/46769524/0ca0a93a-25e7-4434-9974-b8c013905618">


Kubernetes Configuration
• Write Deployment & Servicefor each microservice
• Create a Docker Registry Secret for K8s to be able to pull the Docker images secret

GitLab Configuration
• Install kubectl on GitLab Runner
• Update the deploy job to use kubectl instead of docker-compose

NOTE:

Check more on envsubst

script:
- envsubst ‹ kubernetes/deployment.yaml | kubectl apply -f -
 


Dedicated Secret type: Docker config Secrets
• Stores the credentials for accessing a container image registry
docker-registry(Special secret for K8S)
ImagepullSecrets

