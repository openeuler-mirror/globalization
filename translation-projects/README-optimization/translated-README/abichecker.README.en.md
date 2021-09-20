# **abichecker**

### Introduction

abichecker is an ABI compatibility check tool. It calls the [abi-compliance-checker](https://github.com/lvc/abi-dumper) and [abi-dumper](https://github.com/lvc/abi-dumper) APIs to analyze .rpm and debuginfo packages, implementing ABI compatibility check.

### **Installation Guide**

1. Install the **abi-dumper** and **ompliance-checker** tools.

​       `yum install -y abi-dumper abi-compliance-checker`

2. Download the **abichecker.py** script.

### Usage Guide

1. Create the working directory **/root/checkdir/**, and the directory for storing rpm packages, that is, **libfoo**.

2. Store the .rpm package ***libfoo*-xxx**.**rpm** of libfoo and the debuginfo package **libfoo-debuginfo-*xxx*.rpm** to the **libfoo** directory.

3. Run **python abichecker.py 'libfoo' '/root/checkdir/'**.

4. Store the ABI check result to the **/root/checkdir/libfoo/compat_reports** directory.

### How to Contribute

1. Fork this repository.

2. Create the **Feat_*xxx*** branch.

3. Commit your code.

4. Create a Pull Request (PR).

