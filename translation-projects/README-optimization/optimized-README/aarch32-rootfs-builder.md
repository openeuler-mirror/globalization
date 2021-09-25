# aarch32-rootfs-builder

#### Introduction
aarch32-rootfs-builder provides a set of tools and patches, so that openEuler rootfs software packages can support armv7hf.

#### Scope of Work
- Provide Arm-based 32-bit versions for openEuler common software.
- Develop Arm-based 32-bit build process script for openEuler. 
- Develop patches that are necessary for SRPM to adapt to aarch32-architecture compilation
- Manage aarch32 SIG related matters.
- Respond to user feedback in a timely manner and solve related problems.

#### Introduction to this Repo
```
.
├── conf
│   └── aarch32_support_list.yaml
├── patches
│   ├── gcc_secure
│   │   └── spec
│   │       └── 0001-support-for-arm32-compilation-on-mock.patch
│   └── glibc
│       └── spec
│           └── 0001-add-arm32-support.patch
├── tools
│   ├── auto_build_pkgs.sh
│   ├── auto_make_rootfs.sh
│   └── rpmmacros_openeuler
├── src
│   └── base-files
├── documents
│   └── mock_env_build.md
└── assets
    └── aarch32-roadmap.png
```
- [conf/aarch32_support_list.yaml](conf/aarch32_support_list.yaml)
  - Maintained list of currently supported rpms.
- patches/*/\* 
  - Stores the aarch32 patches of the rpm package. 
- tools/*
  - [auto_build_pkgs.sh](tools/auto_build_pkgs.sh)  Automated compilation tool.
  - [auto_make_rootfs.sh](tools/auto_make_rootfs.sh) Auto make of arm32 rootfs tools.
  - [rpmmacros_openeuler](tools/rpmmacros_openeuler) Compilation of required macros files.
- src/*/\* 
  - Stores packages not currently supported by openEuler (will be pushed into the main openEuler repository later).
- documents/*
  - [mock_env_build.md](documents/mock_env_build.md)  Guidance for building mock compilation environment.
- assets/*
  - [aarch32-roadmap.png](assets/aarch32-roadmap.png) Roadmap pictures

#### Roadmap
![aarch32-roadmap](./assets/aarch32-roadmap.png)

