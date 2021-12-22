<!-- TOC -->

- [Overview](#Overview)
  - [Background](#Background)
  - [Principle](#Principle)
    - [Framework](#Framework)
    - [Test process](#Test process)
  - [Use process](#Use process)
    - [User flow](#User flow)
    - [Network diagram](#Network diagram)
- [Install test frame](#Install test frame)
  - [Prerequisites](#Prerequisites)
  - [Get installation package](#Get installation package)
  - [Installation process](#Installation process)
    - [Client](#Client)
    - [Server](#Server)
  - [Verify installation correctness](#Verify installation correctness)
- [User guide](#User guide)
  - [Prerequisites](#Prerequisites-1)
  - [Use steps](#Use steps)
- [View Results](#View Results)
  - [How to view](#How to view)
  - [Results Description & Suggestion](#Results Description & Suggestion)
- [Appendix: Test item descriptions](#Appendix: Test item descriptions)
  - [Existing test items](#Existing test items)
  - [New test items](#New test items)

<!-- /TOC -->

# Overview

## Background

To expand the compatibility range of their products, OS manufacturers often seek cooperation with hardware manufacturers for compatibility testing. The OS manufacturer formulates a test standard and provides test cases for the hardware manufacturer to carry out the actual test. After the test is passed, OS manufacturers and hardware manufacturers will jointly publish compatibility information on the corresponding official website.

The purpose of verification is to ensure the compatibility between OS and hardware platforms. Verification is limited to basic function verification, not including performance test and other tests.

The openEuler hardware compatibility verification test framework has the following features:

1. To meet the trustworthy requirements, you must use the openEuler OS, and the kernel module cannot be reprogrammed/inserted at will.
2. Discover the hardware list adaptively through the scanning mechanism to determine the set of test cases to run.
3. Object-oriented abstraction of various hardware types and test case classes for extended development.

## Principle

### Framework

```
.
├── hwcompatible Framework main function
│   ├── compatibility.py  Framework main function
│   ├── client.py         Upload test results to the server
│   ├── command.py        bash command execution package
│   ├── commandUI.py      Command line interactive tool
│   ├── device.py         Scan device information
│   ├── document.py       Collect configuration information
│   ├── env.py            Global variables, mainly paths of each configuration file or directory
│   ├── job.py            Test task management
│   ├── log.py            Log module
│   ├── reboot.py         Dedicated to restart tasks, so that the machine can continue to execute tests even after reboot
│   ├── sysinfo.py        Collect system information
│   └── test.py           Test suite template
├── scripts   Tool scripts
│   ├── oech                  Framework command line tool
│   ├── oech-server.service   Framework server service file, used to start the web server
│   ├── oech.service          Framework client service file, used to take over reboot instances
│   └── kernelrelease.json    Specification of the system and kernel version that can be used for certification
├── server   Server
│   ├── oech-server-pre.sh    Service pre-execution script
│   ├── results/              Test result storage directory
│   ├── server.py             Server main program
│   ├── static/               Picture storage directory
│   ├── templates/            Webpage template storage directory
│   ├── uwsgi.conf            nginx service configuration
│   └── uwsgi.ini             uwsgi service configuration
└── tests   Test suite
```



### Test process

![test-flow](docs/test-flow.png)

## Use process

### User flow

![user-flow](docs/user-flow.png)

### Network diagram

![test-network](docs/test-network.png)

# Install test frame

## Prerequisites

Openeuler 20.03 (LTS) or later is installed.

## Get installation package

https://gitee.com/src-openeuler/oec-hardware/releases

## Installation process

### Client

1. Configure the corresponding version of everything source in [the official repo of openEuler](https://repo.openeuler.org/) and install the client oec-hardware using `dnf`.

   ```
   dnf install oec-hardware-XXX.rpm
   ```

### Server

   1. Configure the corresponding version of everything source in [the official repo of openEuler](https://repo.openeuler.org/) and install the server oec-hardware-server using `dnf`.

      ```
      dnf install oec-hardware-server-XXX.rpm
      ```

   2. Some components required by the web display page are not provided by the system itself and need to be installed using pip3 (please configure the available pip source by yourself).

      ```
      pip3 install Flask Flask-bootstrap uwsgi
      ```

   3. Start the service. This service uses port 8080 by default and provides Web services with nginx (default port 80). Please ensure that these ports are not occupied.

      ```
      systemctl start oech-server.service
      systemctl start nginx.service
      ```

   4. Turn off the firewall and SElinux.

      ```
      systemctl stop firewalld
      iptables -F
      setenforce 0
      ```

   ## Verify installation correctness

 If the client enters the `oech` command and it runs, the installation is successful. If you have any problems with the installation, please send your feedback to oecompatibility@openeuler.org.

   # User guide

   ## Prerequisites

   * `/usr/share/oech/kernelrelease.json` file lists all currently supported system versions. Use `uname -a` command to confirm whether the framework supports the current system kernel version.
   * The framework will scan all NICs by default. Before testing the NIC, please filter the NIC under test and assignit an IP that can `ping` the server. If the client is testing the InfiniBand NIC, the server must also have an InfiniBand NIC and configure the IP in advance.

   ## Use stepsassign it

   1. Start the test framework on the client. Start `oech` on the client, where `ID` and `URL` can be filled in as needed. `ID` is recommended to fill in the issue ID on gitee. `Server` must be filled in as the server domain name or ip that the client can access directly, which is used to display test reports and serve for network testing.

      ```
      # oech
      The openEuler Hardware Compatibility Test Suite
      Please provide your Compatibility Test ID:
      Please provide your Product URL:
      Please provide the Compatibility Test Server (Hostname or Ipaddr):
      ```

   2. Enter the test suite selection interface. In the case selection interface, the framework will automatically scan the hardware and select the test suite available for testing in the current environment. Enter `edit` to enter the test suite selection interface.

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

   3. Select the test suite. `all|none` is used to `select all|cancel all` respectively (the required test item`system` cannot be cancelled); the number can select the test suite, and only one number can be selected each time. After pressing the enter character, `no` changes to `yes`, indicating that the test set has been selected.

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

   4. Start the test. Enter `run` to start the test after the selection is completed.

   5. Upload test results. After the test is completed, you can upload the test results to the server for displaying the results and log analysis. If the upload fails, please check the network configuration and then re-upload the test results.

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

   

   # View Results

   ## How to view

   1. Open the server IP address in the browser, click the `Results` interface in the navigation bar, and find the corresponding test id to enter.

      ![results](docs/results.png)

   2. Enter a single task page to see the specific test results, including environment information and execution results.

      - `Submit` Submit means Upload the results to the official certification server of openEuler (**not yet open**).

      - `Devices` view all test device information.

      - `Runtime` View the test run log.

      - `Attachment` Download test attachments.

        ![result-qemu](docs/result-qemu.png)

   

   ## Results Description & Suggestion

The test results are displayed in the **Result** column. There are two types of results: **PASS** or **FAIL**. If the result is **FAIL**, you can directly click on the result to view the execution log, and check according to the error report and use case code.

   # Appendix: Test item descriptions

   ## Existing test items

   1. **system**

      - Check whether the tool has been modified.
      - Check whether the OS version and kernel version match.
      - Check whether the kernel has been modified/infected.
      - Check whether selinux is enabled properly.
      - Use `dmidecode` tool to read the hardware information.

   2. **cpufreq**

      - Test whether the cpu runs at the same frequency as expected with different tuning strategies.
      - Test whether the time required for a cpu to perform exactly the same amount of computation at different frequencies is inversely correlated with the frequency value.

   3. **clock**

      - Test time vectoriality without backwards.
      - Test the basic stability of the RTC hardware clock.

   4. **memory**

      - Use `memtester` tool for memory read-write test.
      - mmap all available system memory, trigger swap, and perform 120s read and write tests.
      - Test hugetlb。
      - Memory hot-swap test.

   5. **network**

      - Use `ethtool` to get NIC information and `ifconfig` to perform down/up tests on the NIC.
      - Use `qperf` to test tcp/udp latency and bandwidth, as well as http upload and download rates of Ethernet card.
      - Use `perftest` to test InfiniBand or RoCE NIC latency and bandwidth.
      - **NOTE** During the network bandwidth test, please confirm in advance that the server NIC rate is not less than that of the client, and ensure that there is no other traffic interference in the test network.

   6. **disk**

      Use `fio` tool to perform sequential/random read and write tests on bare disks/file systems.

   7. **kdump**

      Trigger `kdump` to test whether the vmcore file can be generated and parsed properly.

   8. **watchdog**

      Trigger `watchdog` to test whether the system can be reset properly.

   9. **perf**

      Test whether the `perf` tool works properly.

   10. **cdrom**

       Use `mkisofs` and `cdrecord` to record and read the optical drive.

   11. **ipmi**

       Use `ipmitool` to query IPMI information.

   12. **nvme**

       Use `nvme-cli` tool to format, read and write, and query the disk.

   13. **usb**

       Plug and unplug the usb device to test whether the usb interface can be recognized properly.

   14. **acpi**

       Use `acpidump` tool to read data.

   ## New test items

   1. Add your own test templates in `tests/` to implement your own test class inheritance framework `Test`.

   2. Important member variables or functions.

      - Function `test` - **Required**, the main process of the test.
      - Function `setup` - Environment preparation before testing. It is mainly used to initialize the related information of the tested device, see the `network test`.
      - Function `teardown` - Clean up the environment after the test is completed. It is mainly used to ensure that the environment can be restored correctly regardless of the success or failure of the test, see the `network test`.
      - Variable `requirements` - An array that stores the names of the rpm packages that the test depends on, and the framework will be installed automatically before the test starts.
      - Variable `reboot` and `rebootup` - If `reboot = True`, the test suite/test case will reboot the system and continue to execute the functions specified by `rebootup` after the reboot, see the `kdump test`.
