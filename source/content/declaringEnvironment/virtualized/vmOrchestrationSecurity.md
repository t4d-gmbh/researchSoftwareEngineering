{% if page %}
### Cloud Orchestration, Tooling, and Security Models

Managing hardware virtualization at scale requires a cloud orchestration platform. **OpenStack** serves as the standard open-source paradigm for institutional and private research clouds, modularizing compute, networking, and security into discrete APIs.



#### Core Orchestration Components

An OpenStack environment is composed of interacting microservices, each managing a specific domain of hardware virtualization:

* **Nova (Compute)**: The primary engine that communicates with the underlying hypervisors (e.g., KVM) to provision, schedule, and terminate virtual machines across a cluster of physical physical nodes.
* **Glance (Image Service)**: The central registry for virtual disk images. It stores base operating system images (e.g., Rocky Linux, Ubuntu) and custom snapshots created by researchers. It serves a similar architectural purpose to a container registry (like Docker Hub), but distributes full OS payloads.
* **Neutron (Networking)**: Manages Software-Defined Networking (SDN). It provisions virtual switches, routers, subnets, and floating IP addresses, allowing isolated private networks to be dynamically constructed for specific research groups.

#### Virtualized Security Models

Because VMs operate as full network citizens with complete operating systems, their security model is managed via network-level firewalls and cryptographic access, rather than Linux namespaces.

**1. Security Groups**
Traffic to and from a VM is strictly governed by Security Groups—virtualized, stateful firewalls evaluated at the hypervisor level. By default, all ingress (incoming) traffic to a newly provisioned VM is implicitly denied. Explicit rules must be defined to permit access. 

For example, to allow remote administration, a Security Group rule must be configured to permit ingress TCP traffic on Port 22 (SSH). To host a web dashboard (e.g., JupyterHub), Port 443 (HTTPS) must be explicitly opened.

**2. Keypair Authentication**
Password authentication is universally disabled on standard cloud images to prevent brute-force attacks. Access to a VM is granted exclusively via asymmetric cryptography. During instantiation, a public SSH key (the Keypair) is injected into the VM's `~/.ssh/authorized_keys` file via a metadata service (often `cloud-init`). Only the holder of the corresponding private key can authenticate.

{% endif %}
