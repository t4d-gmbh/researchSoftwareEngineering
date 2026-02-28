### VM Environments 

{% if slide %}

**Hardware Virtualization**
Exact system states, custom kernels, and specialized drivers can be reliably versioned and replicated through Hardware Virtualization.

:::{admonition} Absolute Emulation
:class: note
**Virtual Machines (VMs)** emulate an entire physical computer system. Each VM operates a complete, independent guest operating system to guarantee absolute environmental isolation.
:::

{% else %}
Exact system states, custom kernels, and specialized drivers can be reliably versioned and replicated using Hardware Virtualization. Virtual Machines (VMs) provide a mechanism to emulate an entire physical computer system. Each VM operates a complete, independent guest operating system, ensuring absolute computational reproducibility and environmental control.

#### Principles of Hardware Virtualization

{% endif %}

{% if slide %}

**The Hypervisor (Virtual Machine Monitor)**
Actively intercepts and allocates CPU, memory, and peripheral requests between the physical hardware and the virtualized guests.

:::{admonition} Architectural Trade-off
:class: warning
VMs incur **computational overhead** due to booting a full guest kernel and translating hardware calls. However, this strict boundary guarantees comprehensive **computational reproducibility**, ensuring that exact environments can be reliably replicated across disparate host machines.
:::

{% else %}

Hardware virtualization is orchestrated by a hypervisor (or Virtual Machine Monitor). The hypervisor sits between the physical hardware (host) and the virtualized environments (guests), actively intercepting and allocating CPU, memory, and peripheral requests.

Hypervisors are structurally categorized into two types:

1. **Type 1 (Bare-Metal)**: The hypervisor is installed directly on the physical hardware, replacing a traditional host operating system. Examples include KVM (Kernel-based Virtual Machine), VMware ESXi, and Xen. This architecture is the foundation of modern cloud computing and High-Performance Computing (HPC) virtualization.
2. **Type 2 (Hosted)**: The hypervisor runs as a standard application atop an existing host operating system (e.g., Oracle VirtualBox, VMware Workstation). This is typically utilized for local desktop development rather than production deployments.

Because a full guest kernel must be booted and hardware calls must be translated by the hypervisor, VMs incur a computational overhead. However, this strict boundary provides absolute environmental determinism and enhanced security isolation.

#### Infrastructure as Code (IaC)

{% endif %}

{% if slide %}

**Declarative Infrastructure**
Virtual Machines and their supporting network topologies can be built declaratively using Infrastructure as Code (IaC).

::::{grid} 2
:gutter: 2

:::{grid-item-card} 🛠️ Orchestration Tools

* **OpenStack Heat** (Native cloud engine)
* **Terraform** (Third-party declarative standard)
* **Ansible** (Configuration management and provisioning)
:::

:::{grid-item-card} 🔄 Reproducible Infrastructure
By treating infrastructure as code, the exact hardware allocation, network topology, and security policies of a research environment can be rigorously version-controlled and instantly reproduced.
:::
::::

{% else %}

The deployment of Virtual Machines in cloud environments is typically managed via Infrastructure as Code (IaC). IaC allows VMs and their supporting infrastructure—comprising subnets, routers, and storage volumes—to be built declaratively using configuration files.

In OpenStack environments, this is natively managed by the **Heat** orchestration engine, or via third-party tools such as **Terraform** (for infrastructure provisioning) and **Ansible** (for configuration management).

```hcl
# Example Terraform block defining an OpenStack VM instance
resource "openstack_compute_instance_v2" "research_node" {
  name            = "data-processing-vm"
  image_name      = "Ubuntu 22.04 LTS"
  flavor_name     = "m1.large"
  key_pair        = "researcher-ssh-key"
  security_groups = ["default", "allow-ssh"]
}

```

By version-controlling these declarative templates, the exact hardware allocation and network topology of a research environment can be reliably reproduced.
{% endif %}
