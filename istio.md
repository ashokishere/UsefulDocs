Monolothic 
  - All function implented at the same time, 
  - same code base, 
  - no clear boundaries, 
  - tightly coupled, 
  - single database
  - funcionalite like Authetication, Auth,Netowkring, logging, monittoring, Tracing
  - Stuck wiht same Program(Java)
  - Partial Segmenation of testing for a particaly funcationlity
  - A big Ball of Mud

MicroServices
- Pros
  - Culture change is required
  - each module is speparte appliction
  - Mutiple program (Java, rubym nodejs) can used parllely, Language Agnostic
  - Mulitple verions of product can co exist
  - Scalable
  - Faster and smaller releases and less risky
  - System Resilency and isolation
  - Independent and easy to udnerstand Services
  
- Cons
    - Authetication, Auth,Netowkring, logging, monittoring, Tracing at the indvidaul elve and part of microservices.
    - Problem of fat Microservices
    - Complex Service Networking
    - Traffic Rule, what time outs,
    - Increase complexity when more microsercces are added
    - Security issue when loosely copupled
    - Need an observablity strategies
    - Overload for Tradition opeation Models

How Micorserci solve it?

 Replace with Single Proxy as Sidecar containers
 Proxy communucate with each other thru Data Plane
 They communucate to serve side complente Control Plane
 Data plane and Control Plane toget called Service Mesh
 
 FEW MISSING.... LAST 10 MINS
 
 
 ISTIO



In mini kube

minikube start
minikube addon enable ingress
minikube delete
minikube start --vm=true
minikube addon enable ingress
curl -L https://istio.io.downloadItio | sh -
cd istio-1.10.3
ls tools/
export PATH=$PWD/bin:$PATH
istio verify-install  (will get error)
istioctl install -set profile=dempo -y
istio verify-install
kubeclt app -f /samples
instioclt analyze
kubectl label namesapce defult istio-injection=enabled
delete




KIALI







  
 
 
  
