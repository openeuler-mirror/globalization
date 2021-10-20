#  EulerRobot

####  Introduction

A virtualized automated test project, integrated compilation test, UT test, smoke test, Avocado-VT test,etc.

#### Description

- **Service for virtualized components developer**

  Developers can conduct compiling of virtualized components' own branch code,  address sanitizing compiling, UT test (including qemu-ut, libvirt-ut, kvm-unit-test), static check and other verifications. Now, qemu and libvirt are available, and can be used to connect to openEuler and upstream.

- **Service for smoke testing and integration testing of virtualized components**

  You can run smoke testing and integration testing with designated versions, and replace qemu in the running environment with the address sanitization version delivered with openEuler or upstream qemu.

- **Service for performance testing of virtualized components**

  It provides virtualized benchmark performance testing, including cpu, mem and io. It also provides a performance test model for openEuler virtualization scenarios for a fast performance verification of a designated version.

- **Service for other DFX testing**

  Subsequently, there will be more services for testing, including UZZ, semantic search and reliability. 

#### Software Architecture

Based on various virtualized test suits and testing capability,  EulerRobot can be conneted to compass-ci in order to provide a virtualized platform for users to verify services.![EulerRobot架构](https://gitee.com/openeuler/EulerRobot/raw/master/docs/design/EulerRobot-architecture.png)

Test suite sites of relevant virtualization platforms are as follows:

<https://gitee.com/src-openeuler/avocado>

<https://gitee.com/openeuler/avocado-vt>

<https://gitee.com/openeuler/tp-libvirt>

<https://gitee.com/openeuler/tp-qemu>

####  Installation

1. With a compass-ci account, users should be qualified with submitting tasks via compass-ci. For more specific, please refer to <https://gitee.com/openeuler/compass-ci.git>.
2. Users should downloads EulerRobot repository and run scrip/autopatch.sh to copy the files to lkp-tests directory.

####  Instructions

1. Service for developers

   jobs/openEuler-qemu.yaml - this task provides qemu version compilation, UT test and cppcheck static check. It also supports the configuration of address sanitization compilation, and the compilation of different branches integrated by designated upstream and openEuler.

   jobs/openEuler-libvirt.yaml - this task provides libvirt version compilation and UT test. It also supports the compilation of different branches integrated by upstream and openEuler.

2. Service for smoking and integration test

   jobs/virttest-depends.yaml - this task needs to be performed before virttest_at/virttest_st. It also builds a dep package of rpm that the test framework and test cases rely on for proper operation.

   jobs/virttest-makepkg.yaml - this task needs to be performed before virttest_at/virttest_st. It also builds a pkg package that runs before test framework deployment and test case deployment. It supports the building of qemu address sanitization version.

   jobs/virttest_at.yaml - this task runs virtualized smoking test in a single-physical host test environment. It also supports the configuration of  address sanitization version running on openEuler integrated qemu and upstream qemu.

   jobs/virttest_at_2hosts.yaml - this task runs virtualization test in double-physical host test environment. It also supports the configuration of  address sanitization version running on openEuler integrated qemu and upstream qemu.

   jobs/virttest_st.yaml - this task runs virtualization integrated test in a single-physical host test environment. It also supports the configuration of  address sanitization version running on openEuler integrated qemu and upstream qemu.

   jobs/virttest_st_2hosts.yaml - this task runs virtualization integrated test in a double-physical host test environment. It also supports the configuration of  address sanitization version running on openEuler integrated qemu and upstream qemu.

3. service for performance test

   To be supplemented.

####  Contribution

1. Fork the repository
2. Create Feat_xxx branch
3. Commit your code
4. Create Pull Request

####  Gitee Feature

1. You can use Readme_XXX.md to support different languages, such as Readme_en.md, Readme_zh.md
2. Gitee blog [blog.gitee.com](https://blog.gitee.com) 
3. Explore open source project <https://gitee.com/explore> 
4. The most valuable open source project [GVP](https://gitee.com/gvp) 
5. The manual of Gitee <https://gitee.com/help> 
6. The most popular members  <https://gitee.com/gitee-stars/> 