# AMDVLK

AMD Open Source Driver for Vulkan. Binary version packaged for Archlinux.

No compile time. 

https://github.com/GPUOpen-Drivers/AMDVLK

## Supported GPUs

Supported GPUs v-2024.Q1.1 and newer        |
-----                                       |
Radeon™ RX 7900/7800/7700/7600 Series       |
Radeon™ RX 6900/6800/6700/6600/6500 Series  |
Radeon™ RX 5700/5600/5500 Series            |
Radeon™ Pro W5700/W5500 Series              |
                                            
Supported GPUs v-2023.Q3.3 and lower        |
-----                                       |
Radeon™ RX 7900/7800/7700/7600 Series       |
Radeon™ RX 6900/6800/6700/6600/6500 Series  |
Radeon™ RX 5700/5600/5500 Series            |
Radeon™ RX Vega Series                      |
Radeon™ RX 400/500 Series                   |
Radeon™ Pro WX 9100, x200 Series            |
Radeon™ Pro W5700/W5500 Series              |

For Pre-Polaris and Pre-Raven GPUs, please use v-2021.Q2.5 or older release.

## Feature Support and Performance

The AMD Open Source Driver for Vulkan is designed to support the following features:

- Vulkan 1.3
- More than 170 extensions
- Radeon™ GPUProfiler tracing
- Built-in debug and profiling tools
- Mid-command buffer preemption and SR-IOV virtualization

The following features and improvements are planned in future releases (Please refer to Release Notes for update of each release):

- Upcoming versions of the Vulkan API
- Hardware performance counter collection through RenderDoc
- LLPC optimizations to improve GPU-limited performance and compile time
- Optimizations to improve CPU-limited performance

## Profile

To switch the defualt driver for Vulkan and OpenGL you can use this script in /etc/profile.d/

    #!/usr/bin/bash

    ICD_DIR="/usr/share/vulkan/icd.d"

    # RADV
    #export VK_ICD_FILENAMES="${ICD_DIR}/radeon_icd.i686.json:${ICD_DIR}/radeon_icd.x86_64.json"

    # AMDVLK
    #export VK_ICD_FILENAMES="${ICD_DIR}/amd_icd32.json:${ICD_DIR}/amd_icd64.json"

    # AMDGPU-PRO
    #export VK_ICD_FILENAMES="${ICD_DIR}/amd_pro_icd32.json:${ICD_DIR}/amd_pro_icd64.json"

### Prebuild package

Prebuild package are available at https://repo.archdevlab.org/x86_64/amdvlk-bin

You can add this repo to your pacman.conf

    [amdvlk-bin]
    SigLevel = Optional TrustAll
    Server = https://repo.archdevlab.org/$arch/$repo
