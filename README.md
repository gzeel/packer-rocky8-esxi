# packer-rocky8-esxi

## What is packer-rocky8-esxi ?

packer-rocky8-esxi is a set of configuration files used to build an automated Rocky Linux 8 virtual machine images using [Packer](https://www.packer.io/).
This Packer configuration file allows you to build images for VMware ESXi.

## Prerequisites

- [Packer](https://www.packer.io/downloads.html)
  - <https://www.packer.io/intro/getting-started/install.html>
- A Hypervisor
  - [VMware ESXi](https://www.vmware.com/nl/products/esxi-and-esx.html)
  - With SSH enabled.
- Plugins
  - [Vagrant-vmware-esxi plugin]?(https://github.com/josenk/vagrant-vmware-esxi)

## How to use Packer

Commands to create an automated VM image:

To create a Rocky Linux 8 VM image using VMware Workstation use the following commands:

```cmd
packer build -var 'version=<version>' -var 'esxi_password=<password>' rocky8.json
```

By default the .iso of Rocky Linux 8 is pulled from <https://nlrtm1-edge1.cdn.i3d.net/o1/k9999/pub/rockylinux/8.5/isos/x86_64/Rocky-8.5-x86_64-boot.iso>

You can change the URL to one closer to your build server. To do so change the **"iso_url"** parameter in the **"variables"** section of the rocky8.json file.

```json
{
  "variables": {
      "iso_url": "https://nlrtm1-edge1.cdn.i3d.net/o1/k9999/pub/rockylinux/8.5/isos/x86_64/Rocky-8.5-x86_64-boot.iso"
}
```

## Keyboard configuration

By default the keyboard is set to be US qwerty.
To switch it to something else edit the following file:

- ./http/ks.cfg

Set the `keyboard` parameter as desired, for example: `keyboard --vckeymap=fr --xlayouts='fr'`

## Ansible Role
These configuration files use a Ansible Role : [ansible-role-packer_rhel8](https://github.com/gzeel/ansible-role-packer_rhel8)

## Default credentials

The default credentials for this VM image are:

|Username|Password|
|--------|--------|
|packer|packer|
|root|packer|
|vagrant|vagrant|
