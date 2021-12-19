# DyscheOS-utils

#### Description
This repo is about misc tools regard to userspace part of the Dysche solution.

Note, the master branch may not contain the latest and most complete dev toolset. See the branch list for more comprehensive timely information.

#### Software Architecture
The overall architecture of Dysche is originated from Linux AMP(Asychronous Multi-Processing) architecture. 

In general, there are two parts in Dysche arch: Linux kernel part and the Linux userspace part. In this repo, we'll focus on userspace part.

For Dysche userspace design, there are several componets logically:

- A tool to handle APP-OS images, load and verify the image.
- Interface provided by Dysche kernel part, and run the APP-OS by interacting with it.
- A Linux resident system service that provides online functionality extensions such as device emulation, maintenance, user management by interacting with Dysche kernel part.

#### Instructions

Refer to README.md file of each sub-dir in this repo please.

#### Contribution

1.  Fork the repository
2.  Create a branch
3.  Commit your changes
4.  Create Pull Request



#### Acknowledgements
Thanks.