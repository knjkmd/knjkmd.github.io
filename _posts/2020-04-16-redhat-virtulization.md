---
layout: post
author: kenji
category: general
---
# RHEV
RHEV stands for Red Hat Enterprise Virtulization or it is called RHV. This is alternative to vmware. RHEV uses the KVM (the Kernel-based Virtual Machine). RHV is based on upstream opensource projects KVM and Ovirt. RHV is composed of Red Hat Enterprise Linux (RHEL which includes KVM) and Red Hat Enterprise Virtualization Management (RHV-M), based on Ovirt.


### What is the Kernel-based Virtual Machine (KVM)

>Kernel-based Virtual Machine (KVM) is a virtualization module in the Linux kernel that allows the kernel to function as a hypervisor.
This means virtualization is native in Linux.

## Why RHEV?
> * 100% opensource no proprietary code and no proprietary licencing.
Best Hypervisor for running Red Hat Enterprise Linux (RHEL).
> * Integrated and built with RHEL, uses SELinux to secure Hypervisor.
RHV leads VMware in SPECvirt performance and price per performance (last results 2013).
> * RHV scales vertically and performs extremely well on 4 or even 8 socket servers.
> * All features are included in RHV subscription, no licensing for extra capabilities.
> * KVM is future proof and is the defacto standard for OpenStack and modern virtualizations platforms.


## Two installation possibilities
* Standalone manager set up, standard (non-HA): Installing on separate VM or physical server
* Self-hosted engine setup: Running the manager on a virtual machine on the hosts managed by that Manager

## How to monitor virtulization?
Whichever the install option is, the infromation will be retrieved from the virtulization manager, RHV-M. The REST APIs are listed here.

* https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.2/pdf/rest_api_guide/Red_Hat_Virtualization-4.2-REST_API_Guide-en-US.pdf

Simply calling the end points from a script or oVirt SDK can be used as in the Best practices for Monitoring Red Hat Virtualization. (https://access.redhat.com/solutions/3255981)

The entry point of api, `GET /ovirt-engine/api`

## To create test envrionment
In order to create a test environment, you have to create to a virtual machine inside a virtual machine. Maybe for standalone install it's not necessary unless it manages a vm there. For self-hosted engine, this is must.

Virtualbox with version 6.1 or higher support nested virtualization for Intel CPU.


## Reference:
* https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.3/html/product_guide/installation
* https://keithtenzer.com/2017/05/02/rhev-4-1-lab-installation-and-configuration-guide/
https://www.youtube.com/watch?v=_Hu-3D-duCk&t=537s
* https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.2/pdf/rest_api_guide/Red_Hat_Virtualization-4.2-REST_API_Guide-en-US.pdf
* https://access.redhat.com/solutions/3255981
* https://answers.splunk.com/answers/482589/can-a-rhel-universal-forwarder-be-installed-on-a-r.html
* https://www.linuxtechi.com/enable-nested-virtualization-virtualbox-linux/

