> [!CAUTION]
> Use at your own risk. This patch is only validated with Buildroot 2022.8.1, and needs to be modified and tested before use on different versions.

## Attribution
This is an easily patchable version of the [Buildroot compiler on target](https://luplab.cs.ucdavis.edu/2022/01/06/buildroot-and-compiler-on-target.html) post from UC Davis, updated to work with Buildroot 2022.8.1 from 2021.08-rc1

## Why this is a bad idea
It's not always a bad idea -- the original use case is for a localised development environment for students as it promotes a better understanding of the environment as a whole,
but generally adding a compiler to a dedicated embedded system is a security risk and introduces unnecessary complexity to your system. Use at your own risk, this patch is intended for personal use in development. 
### Resource Constraints
Embedded systems often have limited resources (memory, storage, processing power). Compilers are resource-intensive programs. For instance, if a compiler is added to a target distribution in an IoT device with limited memory, it can lead to performance degradation, as the compiler consumes resources required for core functionality.
### Increased Attack Surface
Including a compiler in the distribution enlarges the attack surface. Each additional piece of software, especially something as complex as a compiler, introduces potential vulnerabilities. In a real-world scenario, this could mean that a networked embedded device like a router could allow remote compilation of malware tailored to the device and network it operates on. Not a selling point.

## Instructions
### Direct Apply
Straightforward, clone the patch at the root of your Buildroot and apply. Creates a dirty Buildroot git configuration 
```
cd ~/my_distro/buildroot # Navigate to the root of your main Buildroot tree
git clone https://github.com/haelyons/gcc-target-package.gitv # Clone patch
git apply gcc-target-2022-08-1.patch # Apply patch
```

### Run as Buildroot package (maintain clean Buildroot config) [WIP]
Creates and enables the new package at build time. Clean configuration, but with a compiler package -- still having some trouble with the post build hooks on this one :) 
