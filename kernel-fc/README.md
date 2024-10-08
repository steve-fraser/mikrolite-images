# Kernel images

This creates a kernel image suitable for using with Firecracker.

A couple of things to note:

- modules are disabled
- The **microvm-kernel-ci-x86_64-6.1.config** file comes from the supported kernel configs published by Firecracker from [here](https://github.com/firecracker-microvm/firecracker/tree/main/resources/guest_configs).
- The **microvm-kernel-ci-x86_64-6.1.config** is downloaded and shouldn't be modified in any way

