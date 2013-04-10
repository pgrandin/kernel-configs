kernel-configs
==============

This repository contains a collection of Linux kernel configuration files (`defconfig`) for various hardware platforms and use cases. Each configuration file is optimized for its specific hardware or use case, enabling only the necessary kernel modules and features.

# Hardware Configs
The fragments are meant to enable hardware specific support for their respective platforms. The configurations are optimized for the specific hardware and may not work on other platforms.

# Use Case Configs
The use case configurations are meant to enable specific features or disable unnecessary ones. These configurations are not hardware specific and can be used on any platform. Examples:
- `bluez_defconfig` - Bluetooth functionality using BlueZ
- `docker_defconfig` - Docker container support
- `gvt_defconfig` - Intel GVT-g graphics virtualization
- `kvm_defconfig` - KVM virtualization support
- `libvirt_defconfig` - libvirt virtualization platform

# Common Configs
- `common_defconfig` - Shared base configuration with common settings and useful drivers

# Usage
## Basic Configuration

The repository provides modular kernel configurations that can be combined with the architecture specific configuration (e.g. `x86_64_defconfig`).

## Prepare the Base Configuration
1. Place your combined configuration fragment in the kernel's architecture config directory:
```bash
cat /path/to/kernel/source/arch/x86/configs/x86_64_defconfig common_defconfig docker_defconfig > /path/to/kernel/source/arch/x86/configs/custom_defconfig
```

2. Build the kernel using the combined defconfig:
```bash
cd /path/to/kernel/source
make defconfig custom_defconfig
```

This will generate the `.config` file from your combined configuration fragments.

## Build the Kernel
Build the kernel using the generated configuration:
```bash
make -j$(nproc)
make modules_install
```

## Example Combinations

For a system with Docker support:
```bash
cat arch/x86/configs/x86_64_defconfig common_defconfig docker_defconfig > arch/x86/configs/docker_custom_defconfig
make defconfig docker_custom_defconfig
```

For a virtualization host:
```bash
cat arch/x86/configs/x86_64_defconfig common_defconfig kvm_defconfig libvirt_defconfig > arch/x86/configs/virt_custom_defconfig
make defconfig virt_custom_defconfig
```

## Install and Configure the Kernel
Install the compiled kernel and set up your bootloader (e.g., GRUB or EFI).

# License

MIT License

Copyright (c) 2013 

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
