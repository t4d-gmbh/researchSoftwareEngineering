### VM Limitations & Pitfalls

{% if slide %}

**The Cost of Ultimate Isolation**
While hardware virtualization provides comprehensive isolation, it introduces structural and operational burdens that must be managed to maintain reproducibility and cluster efficiency.

#### Operational Pitfalls

::::{grid} 2
:gutter: 2

:::{grid-item-card} ❄️ Configuration Drift
**The "Snowflake" Server**
Manual SSH modifications create undocumented, fragile environments that cannot be replicated.

*Mitigation*: Treat VMs as **Immutable Infrastructure**. Automate all configurations via `Ansible`, `Puppet`, or `cloud-init`.
:::

:::{grid-item-card} 🛡️ Maintenance Burden
**Independent Entities**
Unlike containers, VM owners assume full responsibility for:

* Guest OS security patches.
* Firewall configurations (`ufw`, `iptables`).
* Routine updates (`apt-get upgrade`).
:::
::::

{% else %}
While hardware virtualization provides ultimate flexibility and isolation, it introduces specific operational burdens that must be systematically managed to prevent systemic failures and reproducibility loss.

#### Operational Pitfalls

##### 1. Configuration Drift and "Snowflake" Servers

The most significant threat to VM reproducibility is configuration drift. Because a VM behaves exactly like a physical computer, users frequently SSH into the instance to manually install packages, tweak configuration files, or update dependencies. Over time, the VM becomes a "snowflake": a unique, fragile environment whose exact state is undocumented and impossible to replicate.

*Mitigation*: VMs should be treated as **Immutable Infrastructure**. Manual SSH modifications should be strictly prohibited. Instead, all configuration should be automated using provisioning tools (e.g., Ansible, Puppet, or `cloud-init`). If a change is required, the provisioning script is updated, and a entirely new VM is instantiated to replace the old one.

##### 2. The Maintenance Burden

Unlike containers, which rely on the host OS for security patches and kernel updates, each Virtual Machine is an independent entity. The owner of the VM assumes full responsibility for securing the guest operating system, managing firewall configurations (e.g., `ufw` or `iptables`), and applying critical security updates (e.g., `apt-get upgrade`). Unmaintained VMs rapidly become vulnerable vectors within institutional networks.
{% endif %}

{% if slide %}

#### Hardware Limitations

::::{grid} 2
:gutter: 2

:::{grid-item-card} 🛑 Resource Inflexibility

* **Hard Reservations**: CPU and RAM are fully locked by the hypervisor.
* Resources cannot burst or share idle cycles seamlessly across the host.
* Results in lower overall utilization density on compute clusters.
:::

:::{grid-item-card} 🔌 Pass-through Complexity

* Direct access to GPUs/InfiniBand requires **PCIe Passthrough** or **SR-IOV**.
* The hypervisor detaches the device from the host and maps it to the VM memory space.
* **Trade-off**: Breaks advanced features like live-migration, limiting high-availability.
:::
::::

{% else %}

#### Hardware Limitations

##### 1. Resource Overhead and Inflexibility

Virtual Machines require hard reservations of host resources. If a VM is allocated 16 CPU cores and 64GB of RAM, those resources are fully locked by the hypervisor, even if the guest OS is currently sitting idle. Unlike containers, which can burst and share idle CPU cycles seamlessly across the host, VMs inherently lead to lower overall utilization density on compute clusters.

##### 2. Hardware Pass-through Complexity

Assigning physical host hardware (such as NVIDIA GPUs or high-speed InfiniBand network interfaces) directly to a virtual machine is structurally complex. It requires technologies like **PCIe Passthrough** or **SR-IOV** (Single Root I/O Virtualization).

The hypervisor must detach the physical PCIe device from the host kernel and map it directly into the guest VM's memory space. This breaks advanced virtualization features; a VM with a passthrough GPU typically cannot be live-migrated to another physical compute node without being completely shut down, thereby limiting high-availability configurations.
{% endif %}
