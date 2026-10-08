# VMware vSphere Lab: virtualized infrastructure with vMotion

A virtualized enterprise infrastructure built as a **group project** at Odisee (Applied Computer Science, Systems Administration track). The goal was to run a small datacenter on virtual machines and prove that a running VM can move between two hosts **without service interruption**.

## What was built

- **2 nested ESXi hosts** (ESXi running as virtual machines)
- **vCenter Server** to manage both hosts from one place
- **Active Directory domain with DNS** (Windows Server) for authentication and name resolution
- **Shared iSCSI storage** visible to both hosts
- **vMotion live migration** of a running VM from one host to the other

## Architecture

```
                 +----------------------+
                 |  Domain Controller   |
                 |  (Active Directory   |
                 |   + DNS)             |
                 +----------+-----------+
                            |
        +-------------------+-------------------+
        |                                       |
+-------+--------+      vMotion        +--------+-------+
|   ESXi host 1  |<------------------->|   ESXi host 2  |
+-------+--------+                     +--------+-------+
        |                                       |
        +-------------------+-------------------+
                            |
                  +---------+----------+
                  |  Shared iSCSI      |
                  |  storage           |
                  +--------------------+

            vCenter Server manages both ESXi hosts
```

> TODO before publishing: check that this diagram matches your real lab (host names, which machines connect to which) and adjust it if needed.

## Why it is built this way

- **Shared storage:** vMotion moves the running state (memory and CPU) of a VM between hosts. For that, both hosts must see the same datastore, which is why the iSCSI storage is shared.
- **vCenter:** features such as vMotion are managed through vCenter, not through a single host.
- **Active Directory and DNS:** a domain gives the lab realistic name resolution and central authentication, like in a company network.

## Demonstration

A VM was migrated live from one ESXi host to the other while it kept running, with no interruption of service.

> Screenshots: add them to a `docs/` folder (without any password or private information) and link them here.

## What I learned

- Building and connecting the components of a vSphere environment (hosts, vCenter, storage, directory services)
- How iSCSI shared storage and vMotion depend on each other
- Why name resolution (DNS) is a prerequisite for a working domain and virtualization environment

## Tech

VMware ESXi, vCenter Server, vMotion, iSCSI, Windows Server, Active Directory, DNS

## Status

Completed as a school project (group work).
