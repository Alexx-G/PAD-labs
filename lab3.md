
# Cloud (native) apps

## Prerequisites

- Check [GitHub Students pack](https://education.github.com/pack);
- Basic understanding of test automation;
- [Lab 2](lab2.md);

## Objectives

- Study and use a Cloud provider;
- Learn basic principles of IaC (Infrastructure as Code);
- Learn basic concepts of CI/CD;
- Deploy some (or all) services of your project to Cloud-based instances;
- Use Cloud-managed services (if applicable) as a replacement for some project parts;

## Background

A distributed system by definition is supposed to transparently run across multiple nodes.
Thus when delivering (or even testing) such a system, there's an open question - how and where the distributed system is going to be deployed?

While during development cycle individual services can be tested separately, or smaller systems can just run on developer's PC, for production and pre-production use-cases it's necessary to have a dedicated environment the system can be deployed to.
At this point there are 2 choices:
- (Buy and) Manage your own hardware & networking infrastructure, setup a virtualization layer and finally proceed to deployment;
- Use a Cloud provider that will manage hardware, networking and virtualization for you;

While managing own hardware is the most flexible option, it adds tons of operational overhead and usually it's just not sustainable.
This is where Cloud providers manage infrastructure (to different extent), offering compute, storage and networking resources as a service.

> **Deployment**
> Deployment is the process of delivering an artifact to an environment it's supposed to run in.

## Tasks

- [**Mandatory** - Migrate project to Cloud-based instances]()
- [Setup automated build & deployment pipelines]()
- [Replace regular instances with container-based stack]()
- [Automate infrastructure provisioning]()
- [Integrate one (or more) cloud services with the project]()

### **Mandatory** - Migrate project to Cloud-based instances

Use regular virtual instance offered by the Cloud provider to host your services.
While all cloud providers have a different name for this kind of service (see the list below), 
they offer almost the same functionality - a virtual machine that you can access remotely (e.g. SSH) and you can configure the instance (OS settings, packages etc) to your needs.

Cloud providers:
- AWS - EC2 instances
- Azure - Virtual Machines
- DigitalOcean - droplets

### Setup automated build & deployment pipelines

- Setup a CI (Continuous Integration) pipeline, that will build services from the Git repo and run some simple unit/integration tests;
- Integrate the CI pipeline with Git repo (the main branch);
- Setup a CD (Continuous Deployment) pipeline that will deploy services once they are successfully built & tests pass;

### Replace regular instances with container-based stack

Instead of building platform-specific artifact and relying on a pre-configured virtual machine this artifact will be deployed to, 
use Containers-as-a-Service environment from a Cloud provider and deploy services as Docker images.

### Automate infrastructure provisioning

Instead of provisioning Cloud instances manually, use APIs/SDKs offered by Cloud providers to provision these instances in an automated and reproducible way.

### Integrate one (or more) cloud services with the project

Replace (R)DBMS and/or Message Broker with equivalent solutions offered by Cloud provider as a service.
