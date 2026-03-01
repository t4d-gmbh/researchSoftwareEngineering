{% if page %}
### Virtual Disks, Storage, and State Management

The filesystem of a Virtual Machine is managed fundamentally differently than the layered union filesystems utilized by containers. VM storage relies on virtual disk images and block storage abstractions.

#### Virtual Disk Images and Formats

A VM's primary filesystem is encapsulated within a single file known as a virtual disk image. When a VM boots, the hypervisor mounts this file, and the guest OS treats it as a physical hard drive.

The **QCOW2** (QEMU Copy On Write) format is the standard for OpenStack and KVM environments. Unlike raw disk images, which immediately consume their fully allocated size on the host disk, QCOW2 images are dynamically expanding. Furthermore, QCOW2 inherently supports internal snapshotting, allowing the exact state of a VM to be frozen and reverted.



#### Ephemeral vs. Persistent Storage

In cloud architectures like OpenStack, storage state is divided into two distinct paradigms:

**1. Ephemeral Storage (Nova)**
When a standard VM is instantiated from an image, the boot disk is often ephemeral. It is directly tied to the lifecycle of the compute instance. If the VM is explicitly terminated or permanently crashes, the ephemeral disk and all data written to it are permanently destroyed. Ephemeral disks are typically utilized for the base OS installation and temporary scratch space.

**2. Persistent Block Storage (Cinder)**
For research data, databases, and critical state preservation, persistent block storage is required. In OpenStack, the **Cinder** service provisions block storage volumes. These volumes are highly available, physically detached from the compute node, and attached to the VM over the network (typically via iSCSI or Ceph). 

If the attached VM is destroyed, the Cinder volume persists independently. It can subsequently be detached and reattached to a newly provisioned VM, ensuring data lineage is maintained across compute lifecycles.

#### Snapshots and Image Capture

To capture a reproducible state of a virtual machine (including its installed libraries, kernel modifications, and configurations) a snapshot is generated.

In OpenStack, snapshotting a VM creates a new image of the root disk and uploads it to the image registry. This snapshot can then be utilized as a base image to spawn identical clone VMs, facilitating rapid horizontal scaling for distributed computing tasks.

{% endif %}
