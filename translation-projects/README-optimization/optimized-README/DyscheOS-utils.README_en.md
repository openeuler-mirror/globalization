# DyscheOS-utils

#### Introduction
This repo is about Dysche solutions  that are misc tools with regard to userspace part.

Note, the Master branch may not contain the latest dev kits. See the list of branches
for more details.

#### Architecture
The overall architecture of Dysche is originated from Linux AMP(Asychronous Multi-Processing) architecture.
In general, there are two parts in Dysche architecture: the Linux kernel part and the Linux userspace part. In this repo, we'll focus on userspace part.

For Dysche userspace design,it is logically divided into following parts:

- A tool to load and verify APP-OS images.

- Interface with the Dysche kernel part, and run the APP-OS.

- A system service to interfere with Dysche kernel part, maintain/operate APP-OS on the fly, provide devices emulation, etc.

#### Instructions

See README.md of each sub-dir for more details please.

#### Contribution

1.  Fork the repository
2.  Create a branch
3.  Commit your changes
4.  Create Pull Request