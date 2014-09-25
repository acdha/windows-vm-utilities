# windows-vm-utilities

Utilities for working with Windows virtual machines for testing

Currently these assume the use of VMware Fusion but future utilities may be portable across engines. Pull
requests welcome…

## Getting VMs

Microsoft has generously provided a stable of test VMs for the various versions of Windows and
Internet Explorer which the average web developer needs to support:

https://www.modern.ie/en-us/virtualization-tools

## The Scripts

### update-vm

This automates the process of starting a VM, forcing it to poll Windows Update and install updates, and
shutdown later:

```./update-vm PATH_TO_VMWAREVM```

The username and password to login to the guest can be provided using environmental variables:

```GUEST_USER=MyTestAccount GUEST_PASSWORD=insecure ./update-vm PATH_TO_VMWAREVM```

For convenience it defaults to the `IEUser` / `Passw0rd!` values used by the modern.ie VMs.

If you have a collection of test VMs keeping them all up to date looks something like this:

```
cadams@ganymede:~/Documents/Virtual Machines $ for vm in *.vmwarevm; do ./update-vm "$vm"; done
Starting IE10 - Win8.vmwarevm
	Forcing Windows Update to detect
	Forcing Windows Update to update
	Scheduling a shutdown in 15 minutes
Starting IE11 - Win7.vmwarevm
	Forcing Windows Update to detect
	Forcing Windows Update to update
	Scheduling a shutdown in 15 minutes
Starting IE11 - Win8.1.vmwarevm
	Forcing Windows Update to detect
	Forcing Windows Update to update
	Scheduling a shutdown in 15 minutes
Starting IE8 - Win7.vmwarevm
	Forcing Windows Update to detect
	Forcing Windows Update to update
	Scheduling a shutdown in 15 minutes
Starting IE9 - Win7.vmwarevm
Error: Cannot connect to the virtual machine
	Forcing Windows Update to detect
	Forcing Windows Update to update
	Scheduling a shutdown in 15 minutes
```

### Blocking automatic Internet Explorer upgrades

It's great that Internet Explorer is moving towards the automatic major upgrade model used by Chrome and
Firefox but until enterprise IT departments stop blocking upgrades we still need test VMs for the older
versions and don't want them to be upgraded unexpectedly:

```block-automatic-ie10 "IE9 - Win7.vmwarevm"```

```block-automatic-ie11 "IE10 - Win7.vmwarevm"```

