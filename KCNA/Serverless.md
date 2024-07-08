
Serverless does involve servers. These servers are managed by the serverless provider, which means users don't have to 
worry about managing or maintaining systems.The provider handles all the necessary resources on demand, looking after the
servers and services involved in running the serverless offering. 
This removes the burden of server maintenance and cost deprecation, and there's no need to worry about infrastructure details such as the number of cores, 
memory, networking, storage, or even the operating system and its patching.

What is Serverless?

Serverless typically means interacting directly with the service via code or container images. To understand this better,
let's look at AWS Lambda, a common serverless provider.

AWS Lambda: Function as a Service (FaaS)

AWS Lambda allows you to upload your code as a zip file or a container image. It automatically responds to code execution requests at any scale, 
from a dozen events per day to hundreds of thousands per second.

Key points about AWS Lambda:

Event-Driven Architecture: It runs in response to events and you are billed only when your code runs, based on the resources utilized.
Auto Scaling: This is built-in, meaning you don't need to worry about setting up or configuring auto scaling. It scales automatically based on demand, 
but you should set cost limits to manage your workload and billing.
Provisioned Concurrency
Serverless offerings often handle concurrency automatically, reducing the overhead and complexities involved in managing this yourself.

Open Source Serverless Solutions

In the cloud-native ecosystem, there are open-source solutions like Knative and OpenFaaS that provide serverless functionality on top of Kubernetes. 
For example, a serverless web application running on Kubernetes can automatically create a load balancer and configure a minimum number of pods. When not in use,
the application can scale down, and as it is accessed, Knative can automatically scale it back up.

Challenges and Standards in Serverless

Serverless presents challenges, particularly because many cloud providers offer proprietary solutions with no standardized APIs. The CloudEvents specification was 
established to provide a consistent way of describing event data in a common format, ensuring interoperability across services, platforms, and systems. 
It is hosted by the CNCF (Cloud Native Computing Foundation) and has SDKs in most major languages, with coverage for common protocols.

Conclusion

Understanding serverless and its implications is crucial, especially for those preparing for the CCNa exam. Serverless architecture offers significant 
advantages in terms of scalability, cost-efficiency, and reduced maintenance,
but it's essential to be aware of its challenges and the solutions available to address them.
