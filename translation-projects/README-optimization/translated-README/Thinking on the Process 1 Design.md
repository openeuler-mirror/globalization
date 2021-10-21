# Thinking on the Process 1 Design

## Context

In all Unix systems, there is a process whose ID is 1. This is the first user-mode application executed after the operating system kernel is started. Therefore, the process ID is only second to the idle process.

In terms of function positioning, init has two basic functions:

1. Starting and stopping system services: For example, init starts daemon processes of user space in the startup phase. This process depends on activities such as file system mounting, device discovery, and network configuration. Accordingly, when the system is shut down or restarted, init is also responsible for shutting down the network interface, flushing data to disks, clearing resources, and uninstalling the file system. If the system shutdown process is incomplete, the next startup will fail.
2. Reclaiming orphan processes: In the Unix operating system, if the parent process exits earlier than the child process, the child process will become an orphan process. In such cases, init is responsible for reclaiming the running status of the orphan process.

From the perspective of users, reclaiming orphan processes is a basic function. If they are not implemented, a large number of zombie processes will occur in the system, affecting system stability. However, it is more important to manage the starting and stopping of system services. An excellent init process should be fast and reliable. There are several key approaches to achieving the goal of speediness:

- On-demand startup: During startup, only necessary services are started. Other operations are delayed to a proper time (when necessary). For example, services such as update and reporting are processed when the system is idle.
- More parallels: High concurrency is maintained to maximize the use of CPU, memory, and bandwidth resources. In this way, the system can quickly go to the login page, instead of wasting time.
- Ensure high performance of each startup script to avoid unnecessary forks and scripts.

## Comparison of Mainstream init Implementation Modes

Many people have been trying to improve the conventional init daemon processes in some ways to make them more complete. They include simple, reliable, but inefficient sysvinit, and efficient but slightly complex systemd.

The analysis and comparison of adding *todo* and Android init

| Init Software| Description| Startup Management| Process Reclaiming| Service Management| Parallel Startup| Device Management| Resource Control| Log Management|
| -------- | ------------------------------------------------------------ | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| sysvinit | The initialization process tool used in earlier versions gradually step down from the stage of history.| ✓        | ✓        |          |          |          |          |          |
| upstart  | initdaemon used by systems such as Debian and Ubuntu| ✓        | ✓        | ✓        | ✓        |          |          |          |
| systemd  | Compared with the conventional System V, the system startup speed has been improved, which is an innovation. So far, it has been used by most Linux distributions.| ✓        | ✓        | ✓        | ✓        | ✓        | ✓        | ✓        |

## systemd Problem Analysis

systemd is now the standard configuration for most distributions. It is developed to solve the problems of long startup time and complex startup scripts. It is designed to provide a complete set of solutions for system startup and management.

Based on the practical result of systemd's integration with openEuler, improvement need to be made for systemd from the perspective of developers even though it is user friendly.

1. With nearly 1000 versions submitted every month, the version iteration is fast. No mature and stable community version is provided.
2. As the C language is used for coding, the code quality is poor. Simple programming errors and bugs often occur during submission.
3. The community forces users to use the latest unstable version. The maintainer often uses the excuse "version too old" when users seek help. The preceding three points make the maintenance cost of systemd very high.
4. The system resilience is weak. Modules are severely coupled, which leads to easy spread of problems among modules. Mechanisms such as sd-event, sd-bus, and unit are intertwined. Once a problem occurs, the system becomes unavailable or breaks down.
5. More than 100 features are integrated and some of the functions overlap with other software packages. When used in complex scenarios, it is difficult to perform integration tests.
6. The debugging and detection methods are insufficient. Assert messages are often displayed on the screen, which may cause the lose of key information.
7. The boundary is not clear as some functions overlap with other software packages. Once a problem occurs, many people with different backgrounds need to work together to analyze and locate it. The management scope of some system capabilities can be wide but not comprehensive. For example, in cgroup, another set of configuration items is used. The preceding four points make systemd prone to errors when new features are added. Once an error occurs, the overall reliability of the system is affected.
8. The workload of downward compatibility is heavy. For the services that are just transferred from the conventional sysvinit, some behaviors seem unreasonable.
9. The requirements for new developer cultivation can be high, and the mechanism is not as simple and intuitive as sysv init. The preceding two points make the migration of legacy services to the new system unnecessary and complex.

In general, we believe that the systemd architecture and community operation positioning make it unable to satisfy the need for rapid service development and iteration in cloud scenarios. In cloud-native scenarios, an init system is required to ensure fast service development and iteration.

## Design Objectives and Constraints

**Design objectives**

- **Stable and durable system**: A new feature that has not been fully tested affects only its own stability and does not affect the overall stability of the system.
- **Convenient management**: Easy installation, deployment, upgrade, and O&M.
- **Lightweight**: Less resources are occupied. The systemd requires more than 100 MB installation space, however, our new design makes it in single digits.
- **Easy to use**: More flexible and simple architecture, easy to understand and maintain.
- **Ultimate security**: Process tracing Is maintained to provide the minimum running environment.

## Design Idea

### Build a lightweight base (function tailoring/self-developed replacement) with simple but not easy design

**Trend**

- All major OS publishers release lightweight OSs.
- Process 1 becomes more and more mature, building a user-mode kernel.
- Conventional OSs are increasingly unsuitable for the cloud, edge, and device.

**Approach**

The process1 base is provided in the form of **framework+component**, which simplifies complex relationships and is encapsulated in the module, facilitating selection, management, and upgrade.

Provide only the framework and do the least things to reduce the load of init process, mitigating the impact when a fault occurs.

**Integrate or develop ** necessary libraries and tools to ensure that the OS is lightweight enough. Only necessary basic functions and tools are provided. Other functions are containerized and virtualized.

**Provides a unified and lightweight base**, kernel+process 1, **that is, the minimum OS**.

### Applicable to Scenarios Such As Cloud, Edge, and Device with Component-Based Customization and Version Control

**Approach**

Provide a unified framework to **shield underlying differences**.

**Component-based**,  which can be **configured freely** based on the hardware.

**Version control** of components leads to easy installation, deployment, and upgrade.

### More reliable, keep-alive + self-recovery

**Status quo**

The probability for triggering problems is high because process 1 provides too many functions.

The code quality security are poor.

**Approach**

Release process 1 and do only necessary things. Start+process reclaiming + keep-alive of key modules. **Always online**.

Process 1 is automatically recovered, and the component is kept alive.

RUST is used, which makes it secure, concurrent, efficient, and practical.

Fault monitoring/reporting.

## Layer View

## Architecture

## Code Directory Structure
