<!-- TOC -->

- [Overview](#overview)
  - [Background](#Background)
  - [Introdution](#Introdution)
    - [Framework Overview](#Framework Overview)
    - [Test Flow](#Test Flow)
  - [Usage Flow](#Usage Flow)
    - [User Flow](#User Flow)
    - [Network Diagram](#Network Diagram)
- [Installing the Test Framework](#Installing the Test Framework)
  - [Prerequisites](#Prerequisites)
  - [Obtaining the Installation Package](#Obtaining the Installation Package)
  - [Installation](#Installation)
    - [Client](#Client)
    - [Server](#Server)
  - [Verifying the Installation](#Verifying the Installation)
- [Usage Guide](#Usage Guide)
  - [Prerequisites](#Prerequisites-1)
  - [Procedure of Using](#Procedure of Using)
- [Viewing the Results](#Viewing the Results)
  - [How to View the Results](#How to View the Results)
  - [Result Description and Suggestions](#Result Description and Suggestions)
- [Appendix: Test Item Description](#Appendix Test Item Description)
  - [Existing Test Items](#Existing Test Items)
  - [Adding Test Items](#Adding Test Items)

<!-- /TOC -->

# Overview

## Background

OS vendors often seek cooperation with hardware vendors to perform compatibility tests, to expand the compatibility scope of their products. The OS vendor formulates a test standard and provides test cases for the hardware vendor to perform tests. After the test is passed, the OS and hardware vendors will jointly release the compatibility information on the corresponding official websites.

The purpose of the verification is to ensure the compatibility between the OS and hardware platform. The verification scope is limited to basic function verifications and does not include other tests such as performance tests.

The openEuler hardware compatibility test framework has the following features:

1. To meet the trustworthiness requirements, the openEuler operating system must be used, and the kernel modules shall not be recompiled or inserted randomly.
2. The scanning mechanism adaptively discovers the hardware list to determine the test cases to be run.
3. Various hardware types and test case classes are abstracted in an object-oriented way for extended development.

## Introdution

### Framework Overview 

```
.
├── hwcompatible   Main functions of the framework
│   ├── compatibility.py Core functions of the framework
│   ├── client.py        Uploading the test result to the server
│   ├── command.py       bash command execution encapsulation
│   ├── commandUI.py     Command line interaction tools
│   ├── device.py        Scanning device information
│   ├── document.py      Collecting configuration information
│   ├── env.py           Global variables, mainly the paths of the configuration files or directories
│   ├── job.py           Test task management
│   ├── log.py           Log module
│   ├── reboot.py        Dedicated for reboot tasks so that the test can be continued after the device is   │   │                    rebooted
│   ├── sysinfo.py       Collecting system information
│   └── test.py          Test suite template
├── scripts        Tool scripts
│   ├── oech                  Command line tools of the framework
│   ├── oech-server.service   Server side service file of the framework, used to start the web server
│   ├── oech.service          Client side service file of the framework, used to take over reboot cases
│   └── kernelrelease.json    Specifying the system and kernel versions that can be used for authentication
├── server         Server side
│   ├── oech-server-pre.sh    Service pre-execution scripts
│   ├── results/              Directory for storing test results
│   ├── server.py             Main program of the server
│   ├── static/               Directory for storing images
│   ├── templates/            Directory for storing web page templates
│   ├── uwsgi.conf            Nginx service configurations
│   └── uwsgi.ini             uWSGI service configurations
└── tests          Test suites
```



### Test Flow

![test-flow](docs/test-flow.png)

## Usage Flow

### User Flow

![user-flow](docs/user-flow.png)

### Network Diagram

![test-network](docs/test-network.png)

# Installing the Test Framework

## Prerequisites

openEuler 20.03 (LTS) or later has been installed.

## Obtaining the Installation Package

https://gitee.com/src-openeuler/oec-hardware/releases

## Installation

### Client

1. Configure the everything source of the corresponding version in [openEuler Repo](https://repo.openeuler.org/) then use `dnf` to install the client oec-hardware package.

   ```
   dnf install oec-hardware-XXX.rpm
   ```


### Server

1. Configure the everything source of the corresponding version in [openEuler Repo](https://repo.openeuler.org/) then use `dnf` to install the oec-hardware-server package.

   ```
   dnf install oec-hardware-server-XXX.rpm
   ```

2. Some components required for web page display on the server are not provided by the system and need to be installed using `pip3`. (Configure the pip source as required.)

   ```
   pip3 install Flask Flask-bootstrap uwsgi
   ```

3. Start the service. The service uses port 8080 by default and works with Nginx (default port 80) to provide web services. Ensure that these ports are not occupied.

   ```
   systemctl start oech-server.service
   systemctl start nginx.service
   ```

4. Disabling firewalld and SElinux

   ```
   systemctl stop firewalld
   iptables -F
   setenforce 0
   ```

## Verifying Installation

Run `oech` on the client. If the command runs properly, the installation is successful. If you have any questions about the installation, send an email to oecompatibility@openeuler.org.

# Usage Guide

## Prerequisites

* The `/usr/share/oech/kernelrelease.json` file lists all supported system versions. Run `uname -a` to check whether the current system kernel version is supported by the framework.

* By default, the framework scans all NICs. Before testing an NIC, select the NIC to be tested and configure an IP address that can ping the server. If an InfiniBand NIC is to be tested on the client, the server must also have an InfiniBand NIC and an IP address configured in advance.

## Procedure of Using

1. Start the test framework on the client. Start `oech` on the client. `ID` and `URL` can be set as required. It is recommended that `ID` be set to the issue ID on Gitee. `Server` must be set to a domain name or an IP address that can be directly accessed by the client. `Server` is used to display the test report and function as the server for network tests.

   ```
   # oech
   The openEuler Hardware Compatibility Test Suite
   Please provide your Compatibility Test ID:
   Please provide your Product URL:
   Please provide the Compatibility Test Server (Hostname or Ipaddr):
   ```

2. The test suite selection page is displayed. On the test case selection page, the framework automatically scans hardware and selects test suites that can be tested in the current environment. You can enter `edit` to go to the test suite selection page.

   ```
   These tests are recommended to complete the compatibility test:
   No. Run-Now?  Status  Class         Device
   1     yes     NotRun  acpi
   2     yes     NotRun  clock
   3     yes     NotRun  cpufreq
   4     yes     NotRun  disk
   5     yes     NotRun  ethernet      enp3s0
   6     yes     NotRun  ethernet      enp4s0
   7     yes     NotRun  ethernet      enp5s0
   8     yes     NotRun  kdump
   9     yes     NotRun  memory
   10    yes     NotRun  perf
   11    yes     NotRun  system
   12    yes     NotRun  usb
   13    yes     NotRun  watchdog
   Ready to begin testing? (run|edit|quit)
   ```

3. Select test items. `all|none` is used to `select all|cancel all` (the mandatory item `system` cannot be cancelled). You can select only one test suite number at a time. After you press Enter, the `no` following the number changes to `yes`, indicating that the test suite is selected.

   ```
   Select tests to run:
   No. Run-Now?  Status  Class         Device
   1     no      NotRun  acpi
   2     no      NotRun  clock
   3     no      NotRun  cpufreq
   4     no      NotRun  disk
   5     yes     NotRun  ethernet      enp3s0
   6     no      NotRun  ethernet      enp4s0
   7     no      NotRun  ethernet      enp5s0
   8     no      NotRun  kdump
   9     no      NotRun  memory
   10    no      NotRun  perf
   11    yes     NotRun  system
   12    no      NotRun  usb
   13    no      NotRun  watchdog
   Selection (<number>|all|none|quit|run):
   ```

4. Start the test. After selecting a test suite, enter `run` to start the test.

5. Upload the test result. After the test is complete, you can upload the test result to the server for result display and log analysis. If the upload fails, check the network configuration and upload the test result again.

   ```
   ...
   -------------  Summary  -------------
   ethernet-enp3s0                  PASS
   system                           FAIL
   Log saved to /usr/share/oech/logs/oech-20200228210118-TnvUJxFb50.tar succ.
   Do you want to submit last result? (y|n) y
   Uploading...
   Successfully uploaded result to server X.X.X.X.
   ```



# Viewing the Results

## How to View the Results

1. Open the browser, enter the server IP address, click `Results` in the navigation tree, and find the corresponding test ID.

   ![results](docs/results.png)

2. You can view the detailed test result on the page of a single task, including the environment information and execution result.

   - `Submit` to upload the test result to the Euler official authentication server (**not open currently**).

   - `Devices` displays information about all test devices.

   - `Runtime` to view test run logs.

   - `Attachment` to download the test attachment.

     ![result-qemu](docs/result-qemu.png)



## Result Description and Suggestions

The **Result** column displays the test result, which can be **PASS** or **FAIL**. If the result is **FAIL**, click the result to view the execution log and rectify the fault based on the case code.

# Appendix: Test Item Description

## Existing Test Items

1. **system**
   
   - Checking whether this tool is modified.
   - Checking whether the OS version matches the kernel version.
   - Checking whether the kernel is modified or infected.
   - Checking whether the SELinux is properly enabled.
   - Using the dmidecode tool to read hardware information.

2. **cpufreq**

   - Testing whether the CPU running frequency is the same as expected when different frequency control policies are used.
   - Testing whether the time required for the CPU to calculate the same specifications at different frequencies is inversely correlated with the frequency.

3. **clock**

   - Testing the clock direction and if the clock goes backwards.
   - Testing the basic stability of the RTC hardware clock.

4. **memory**

   - Using the memtester tool to perform the memory read/write test.
   - Performing mmap to all available memory to trigger memory swapping, then performing the read/write test for 120s.
   - Testing the HugeTLB.
   - Testing memory hot swap.

5. **network**

   - Running the ethtool command to obtain the NIC information and using the ifconfig tool to perform the down/up test on the NIC.
   - Using qperf to test the TCP/UDP latency and bandwidth, and HTTP upload and download rates of the Ethernet NIC.
   - Using perftest to test the InfiniBand or RoCE NIC latency and bandwidth.
   - ** Note: **Before performing a network bandwidth test, ensure that the rate of the server NIC is greater than or equal to that of the client NIC and that the test network is not affected by other traffic.

6. **disk**

   Using the fio tool to perform sequential or random read/write tests on raw disks or file systems.

7. **kdump**

   Triggering kdump to check whether vmcore files can be properly generated and parsed.

8. **watchdog**

   Triggering the watchdog to check whether the system can be reset properly.

9. **perf**

   Testing whether the perf tool can be used normally.

10. **cdrom**

    Using mkisofs and cdrecord to test the burning and reading functions of the optical disk drive.

11. **ipmi**

    Using IPMItool to query IPMI information.

12. **nvme**

    Using the nvme-cli tool to test formatting, reading, writing, and querying of the disk.

13. **usb**

    Removing and inserting the USB device to test whether the USB port can be identified properly.

14. **acpi**

    Using the acpidump tool to read data.

## Adding Test Items

1. You can add a test template to `tests/` to implement your own test class inheritance framework `Test`.

2. Important member variables or functions:

   - `test` function - **Mandatory**, which is the main test flow.

   - `setup` function  - Used to prepare the environment before the test. It is used to initialize the information about the tested device. The network test can be used as reference.

   - `teardown` function - Clearing the environment after the test is complete. It is used to ensure that the environment can be correctly restored whether the test is successful or not. The network test can be used as reference.

   - `requirements` variable - An array to store the names of the test dependency RPM packages. The RPM packages are automatically installed by the framework before the test starts.

   - `reboot` and `rebootup` variables - If `reboot = True`, the test suite or test case will reboot the system and continue to execute the function specified by `rebootup` after the reboot. The kdump test can be used as reference.
