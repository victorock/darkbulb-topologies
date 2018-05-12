Topologies
================================

This is an automated lab setup for Ansible training. It creates a standard topology adopting network devices from different vendors.

The functional environment will have:

* One Tower node from which Ansible will be executed and where Ansible Tower is installed.
* One Management switch for network OOB.
* Two Spine switches with four network interfaces each one.
* Four Leaf switches with four network interfaces each one.
* Two Linux Servers with two network interfaces each one.

```
[CONTROL]
TOWER:
  E0: VAGRANT-MGMT


[SPINE]
SPINE01:
  E0: VAGRANT-MGMT
  E1: LEAF01-E1
  E2: LEAF02-E1
  E3: LEAF03-E1
  E4: LEAF04-E1

SPINE02:
  E0: VAGRANT-MGMT
  E1: LEAF01-E2
  E2: LEAF02-E2
  E3: LEAF03-E2
  E4: LEAF04-E2

[POD01]
LEAF01:
  E0: VAGRANT-MGMT
  E1: SPINE01-E1
  E2: SPINE02-E1
  E3: SRV01-E1
  E4: LEAF02-E4

LEAF02:
  E0: VAGRANT-MGMT
  E1: SPINE01-E2
  E2: SPINE02-E2
  E3: SRV01-E2
  E4: LEAF01-E4

SRV01:
  E0: VAGRANT-MGMT
  E1: LEAF01-E3
  E2: LEAF02-E3

[POD2]
LEAF03:
  E0: VAGRANT-MGMT
  E1: SPINE01-E3
  E2: SPINE02-E3
  E3: SRV02-E1
  E4: LEAF04-E4

LEAF04:
  E0: VAGRANT-MGMT
  E1: SPINE01-E4
  E2: SPINE02-E4
  E3: SRV02-E2
  E4: LEAF03-E4

SRV02:
  E0: VAGRANT-MGMT
  E1: LEAF03-E3
  E2: LEAF04-E3

```

## What's Provided

The topologies are created adopting Virtualbox tunnels to provide the interfaces connectivity.
These topologies are expandable to multi-node deployment.

* Cisco
* Juniper

### Build
You need to download the images if they are not publicly available (Ex: Cisco IOS/NXOS, Arista EOS).

Juniper does provides vQFX images in Vagrant Box public repository.

*Enter the <Vendor> Lab folder:*

```
cd <darkbulb-topologies>/<vendor>/<NOS>
```

*Build the Lab Environment*

>2 Spines, 4 Leafs and 2 Servers
```
ansible-playbook build.yml
```

*Launch the Desired Topology/Nodes*
>TODO: Create playbook to launch process.

>2 Spines, 4 Leafs and 2 Servers
```
cd files
vagrant up
```

>1 Spine
```
cd files
vagrant up spine01
```
