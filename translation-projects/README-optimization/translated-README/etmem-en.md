# etmem

## Introduction

With the development of CPU computing power, especially the reduction of ARM core cost, memory cost and memory capacity have become the core pain point that constrains business cost and performance. Therefore, how to save memory cost and how to expand memory capacity has become an urgent problem for storage.

`etmem` memory grading expansion technology, through DRAM + memory compression/high-performance storage new media to form multi-level memory storage, grading the memory data, and migrating the tiered cold memory data from the memory medium to the high-performance storage medium to achieve memory capacity expansion, to achieve memory cost reduction.

## Compilation Tutorial

1. Download `etmem` source code

    $ git clone https://gitee.com/openeuler/etmem.git

2. Compile and run dependencies

    The compilation and running of `etmem` depends on the `libboundscheck` component

3. Compile

    $ cd etmem

    $ mkdir build

    $ cd build

    $ cmake ..

    $ make


## Instructions

### Start the etmemd process

#### How to use

Run the server process by running etmemd binary, for example:

$ etmemd -l 0 -s etmemd_socket

#### Help information

options：

-l|\-\-log-level <log-level>  Log level

-s|\-\-socket <sockect name>  Socket name to listen to

-h|\-\-help  Show this message

-m|\-\-mode-systemctl mode used to start(systemctl)

#### Command-line parameter description

| Parameter              | Meaning                                                      | Required | Available parameter | Range                        | Description                                                  |
| ---------------------- | ------------------------------------------------------------ | -------- | ------------------- | ---------------------------- | ------------------------------------------------------------ |
| -l / -\-log-level      | etmemd log level                                             | NO       | YES                 | 0~3                          | 0: debug level 1: info level 2: warning level 3: error level Only the level greater than or equal to the configured level will be printed to the **/var/log/message** file |
| -s / -\-socket         | Name of the etmemd listener, used to interact with the client | YES      | YES                 | String within 107 characters | Specify the name of the server listener                      |
| -h / -\-help           | Help information                                             | NO       | NO                  | NA                           | Execution with this parameter will print and then exit       |
| -m / -\-mode-systemctl | When etmemd is pulled up as a service, this parameter can be used in the command to support fork mode startup | NO       | NO                  | NA                           | NA                                                           |
### etmem configuration file

Before running `etmem` processes, the administrator needs to plan which processes require memory expansion, configure the process information into the `etmem` configuration file, and configure the period of memory scan, number of scans, memory hot and cold thresholds, and other information.

The sample configuration file is in the source package, placed in **conf/example_conf.yaml** in the root directory of the source code. It is recommended to be placed in the **/etc/etmem/** directory when in use. The sample content is:

```
[project]
name=test
loop=1
interval=1
sleep=1

#slide engine example
[engine]
name=slide
project=test

[task]
project=test
engine=slide
name=background_slide
type=name
value=mysql
T=1
max_threads=1

#cslide engine example
[engine]
name=cslide
project=test
node_pair=2,0;3,1
hot_threshold=1
node_mig_quota=1024
node_hot_reserve=1024

[task]
project=test
engine=cslide
name=background_cslide
type=pid
name=23456
vm_flags=ht
anon_only=no
ign_host=no

#thirdparty engine example
[engine]
name=thirdparty
project=test
eng_name=my_engine
libname=/usr/lib/etmem_fetch/my_engine.so
ops_name=my_engine_ops
engine_private_key=engine_private_value

[task]
project=test
engine=my_engine
name=backgroud_third
type=pid
value=12345
task_private_key=task_private_value
```

Description of each field of the configuration file:

| Configuration item | Meaning                                                      | Required                                         | Available parameter | Range                                                        | Description                                                  |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------ | ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [project]          | Project common configuration segment start ID                | NO                                               | NO                  | NA                                                           | The beginning identification of the project parameter, which indicates that the following parameters are parameters of the project section until another [XXX] or the end of the file |
| name               | Name of the project                                          | YES                                              | YES                 | String within 64 characters                                  | Used to identify the project. Engine and task need to specify the project to be mounted when configuring |
| loop               | Number of cycles of memory scan                              | YES                                              | YES                 | 1~10                                                         | loop=3 // Scan 3 times                                       |
| interval           | Time interval between each memory scan                       | YES                                              | YES                 | 1~1200                                                       | interval=5 // 5s between each scan                           |
| sleep              | Time interval between major cycles of each memory scan and operation | YES                                              | YES                 | 1~1200                                                       | sleep=10 // 10s between each major cycle                     |
| [engine]           | engine common configuration segment start ID                 | NO                                               | NO                  | NA                                                           | The beginning identification of the engine parameter, which indicates that the following parameters are parameters of the engine section until another [XXX] or the end of the file |
| project            | Declare the project                                          | YES                                              | YES                 | String within 64 characters                                  | If a project named test already exists, it can be written as project=test |
| engine             | Declare the engine                                           | YES                                              | YES                 | slide/cslide/thridparty                                      | Declare that the slide or cslide or thirdparty strategy is used |
| node_pair          | Configuration item of cslide engine, declares the node pair of AEP and DRAM in the system | Must be configured when engine is **cslide**     | YES                 | Configure the node numbers of AEP and DRAM in pairs. AEP and DRAM are separated by commas and each pair is separated by semicolons | node_pair=2,0;3,1                                            |
| hot_threshold      | Configuration item of cslide engine, declare the threshold of memory cold and hot threads | Must be configured when engine is **cslide**     | YES                 | Integer >= 0                                                 | hot_threshold=3 // Memory accessed less than 3 times is recognized as cold memory |
| node_mig_quota     | Configuration item of cslide engine, flow control, declares the maximum one-way flow rate each time DRAM and AEP migrate to each other | Must be configured when engine is **cslide**     | YES                 | Integer >= 0                                                 | node_mig_quota=1024 // In MB, AEP to DRAM or DRAM to AEP relocation up to 1024M at a time |
| node_hot_reserve   | Configuration item of cslide engine, declares the reserved space size of the hot memory in DRAM | Must be configured when engine is **cslide**     | YES                 | Integer >= 0                                                 | node_hot_reserve=1024 // In MB, when the hot memory of all virtual machines is greater than this configuration value, the hot memory will also be migrated to AEP |
| eng_name           | Configuration item of thirdparty engine, declares the name of the engine for task mounting | Must be configured when engine is **thirdparty** | YES                 | String within 64 characters                                  | eng_name=my_engine // When mounting a task on this third-party strategy engine, write engine=my_engine in the task |
| libname            | Configuration item of thirdparty engine, declares the address(absolute address) of the dynamic library of the third-party strategy | Must be configured when engine is **thirdparty** | YES                 | String within 64 characters                                  | libname=/user/lib/etmem_fetch/code_test/my_engine.so         |
| ops_name           | Configuration item of thirdparty engine, declares the name of the operation symbol in the dynamic library of the third-party strategy | Must be configured when engine is **thirdparty** | YES                 | String within 64 characters                                  | ops_name=my_engine_ops // Name of the structure of the third-party strategy implementation interface |
| engine_private_key | Configuration item of thirdparty engine, which is reserved for third-party strategy task parsing private parameter configuration items, optional | NO                                               | NO                  | Self-restriction according to third-party strategy private parameters | Self-configuration according to the third-party strategy private engine parameters |
| [task]             | task common configuration segment start ID                   | NO                                               | NO                  | NA                                                           | The beginning identification of the task parameter, which indicates that the following parameters are parameters of the task section until another [XXX] or the end of the file |
| project            | Declare the project to be mounted                            | YES                                              | YES                 | String within 64 characters                                  | If a project named test already exists, it can be written as project=test |
| engine             | Declare the engine to be mounted                             | YES                                              | YES                 | String within 64 characters                                  | Name of the engine to be mounted                             |
| name               | Name of the task                                             | YES                                              | YES                 | String within 64 characters                                  | name=background1 // Declare the name of the task as backgound1 |
| type               | Type for target process identification                       | YES                                              | YES                 | pid/name                                                     | pid means identified by process number, name means identified by process name |
| value              | Specific fields for target process identification            | YES                                              | YES                 | Actual process number/process name                           | Used in conjunction with the type field to specify the process number or process name of the target process. The user ensures the correctness and uniqueness of the configuration. |
| T                  | Task configuration item when engine is slide, declare the threshold of memory cold and hot threads | Must be configured when engine is **slide**      | YES                 | 0~loop * 3                                                   | T=3 //Memory accessed less than 3 times is recognized as cold memory |
| max_threads        | Task configuration item when engine is slide, the maximum number of threads in the etmemd internal thread pool, each thread handles the memory scanning and operation tasks of a process/sub process | NO                                               | YES                 | 1~2 * (number of cores) + 1, default is 1                    | No external appearance, control the number of internal processing threads on the etmemd server. When the target process has multiple sub-processes, the larger the configuration, the more concurrent executions, but also the more resources are occupied. |
| vm_flags           | Task configuration item when engine is cslide, specifying the flag to scan vma, the scan will not be distinguished if this item is not configured | Must be configured when engine is **cslide**     | YES                 | Only ht is currently supported                               | vm_flags=ht // Scan vma memory whose flags are ht (large pages) |
| anon_only          | Task configuration item when engine is cslide, which identifies whether to scan only anonymous pages | NO                                               | YES                 | yes/no                                                       | anon_only=no // When configured as yes, only anonymous pages will be scanned, and when configured as no, non-anonymous pages will also be scanned |
| ign_host           | Task configuration item when engine is cslide, which identifies whether to ignore the page table scan information on the host | NO                                               | YES                 | yes/no                                                       | ign_host=no // yes to ignore, no to not ignore               |
| task_private_key   | Task configuration item when engine is thirdparty, which is reserved for third-party strategy task parsing private parameter configuration items, optional | NO                                               | NO                  | Self-restriction according to third-party strategy private parameters | Self-configuration according to the third-party strategy private task parameters |



### Creation and deletion of etmem project/engine/task objects

#### Use case

1）The administrator creates the project/engine/task of etmem (a project can contain more than one etmem engine, and an engine can contain more than one task)

2）The administrator deletes the existing etmem project/engine/task (all tasks in the project will be stopped automatically before deleting the project)

#### How to use

Run the `etmem` binary and specify the second parameter as obj to create or delete. For **project/engine/task**, it is identified and distinguished by the content configured in the configuration file. The prerequisite is that the `etmem` configuration file has been configured correctly and the `etmemd` process has been started.

Add object:

etmem obj add -f /etc/example_config.yaml -s etmemd_socket

Delete object:

etmem obj del -f /etc/example_config.yaml -s etmemd_socket

Print help information:

etmem obj help

#### Help information

Usage:

etmem obj add [options]

etmem obj del [options]

etmem obj help

Options:

-f|\-\-file <conf_file> Add configuration file

-s|\-\-socket <socket_name> Socket name to connect

**Notes:**

1. Configuration file must be given.

#### Command-line parameter description


| Parameter       | Meaning                                                      | Required                                 | Available parameter | Description                                                  |
| --------------- | ------------------------------------------------------------ | ---------------------------------------- | ------------------- | ------------------------------------------------------------ |
| -f / -\-file    | Specify the configuration file                               | Must contain subcommand **add**, **del** | YES                 | Path name needs to be specified                              |
| -s / \-\-socket | The socket name to communicate with the etmemd server. Must be the same as that specified when etmemd is started | Must contain subcommand **add**, **del** | YES                 | Must be configured. When there is more than one etmemd, the administrator chooses which etmemd to communicate with |

### etmem task start/stop/query

#### Use case

After the project has been added via `etmem obj add`, you can start and stop the project of `etmem` before calling `etmem obj del` to delete the project.

1）The administrator starts the added project

2）The administrator stops the started project

When the administrator calls `obj del` to delete the project, if the project has been started, it will stop automatically.

#### How to use

For projects that have been successfully added, you can control the start and stop of the project by using the `etmem project` command. Examples are as follows:

Start project

etmem project start -n test -s etmemd_socket

Stop project

etmem project stop -n test -s etmemd_socket

Query project

etmem project show -n test -s etmemd_socket

Print help

etmem project help

#### Help information

Usage:

etmem project start [options]

etmem project stop [options]

etmem project show [options]

etmem project help

Options:

-n|\-\-name <proj_name> Add project name

-s|\-\-socket <socket_name> Socket name to connect

Notes:

1. Project name and socket name must be given when executing add or del option.

2. Socket name must be given when executing show option.

#### Command-line parameter description

| Parameter      | Meaning                                                      | Required                                              | Available parameter | Description                                                  |
| -------------- | ------------------------------------------------------------ | ----------------------------------------------------- | ------------------- | ------------------------------------------------------------ |
| -n / -\-name   | Specify the name of the project                              | Must contain subcommand **start**, **stop**, **show** | YES                 | Project name, corresponding to the configuration file        |
| -s / -\-socket | The socket name to communicate with the etmemd server. Must be the same as that specified when etmemd is started | Must contain subcommand **start**, **stop**, **show** | YES                 | Must be configured. When there is more than one etmemd, the administrator chooses which etmemd to communicate with |

### etmem supports self-starting with the system

#### Use case

`etmemd` supports being pulled up in fork mode as a `systemd` service after the `systemd` configuration file is configured by the user.

#### How to use

Write a service configuration file to start `etmemd`, you must use the -m parameter to specify this mode, for example:

etmemd -l 0 -s etmemd_socket -m

#### Help information

options:

-l|\-\-log-level <log-level> Log level

-s|\-\-socket <sockect name> Socket name to listen to

-m|\-\-mode-systemctl mode used to start(systemctl)

-h|\-\-help Show this message

#### Command-line parameter description
| Parameter               | Meaning                                                      | Required | Available parameter | Range                        | Description                                                  |
| ----------------------- | ------------------------------------------------------------ | -------- | ------------------- | ---------------------------- | ------------------------------------------------------------ |
| -l / \-\-log-level      | etmemd log level                                             | NO       | YES                 | 0~3                          | 0: debug level 1: info level 2: warning level 3: error level Only the level greater than or equal to the configured level will be printed to the **/var/log/message** file |
| -s / \-\-socket         | Name of the etmemd listener, used to interact with the client | YES      | YES                 | String within 107 characters | Specify the name of the server listener                      |
| -m / \-\-mode-systemctl | When etmemd is pulled up as a service, this parameter can be used in the command to support fork mode startup | NO       | NO                  | NA                           | NA                                                           |
| -h / \-\-help           | Help information                                             | NO       | NO                  | NA                           | Execution with this parameter will print and then exit       |




### etmem supports third-party memory expansion strategies

#### Use case

`etmem` supports users to register third-party memory expansion strategies, and provides a dynamic library of scanning modules. At runtime, memory is eliminated through the third-party strategy elimination algorithm.

Users use the dynamic library of scan modules provided by `etmem` and implement the interfaces in the structures required by `etmem`

#### How to use

Users use their own third-party extension elimination strategy, which mainly needs to be implemented and operated according to the following steps:

1. Call the scanning interface provided by the scanning module as needed;

2. Implement each interface according to the function template provided in the etmem header file, and finally package it into a structure;

3. Compile the dynamic library of the third-party extension elimination strategy;

4. Declare the engine of `thirdparty` type in the configuration file as required;

5. Fill the name of the dynamic library and the name of the interface structure into the fields corresponding to the task in the configuration file as required.

Other steps are similar to other engines using `etmem`

Interface structure template:

struct engine_ops {

/* Parsing for engine private parameters, if there is, needs to be implemented, otherwise set to NULL */

int (*fill_eng_params)(GKeyFile *config, struct engine *eng);

/* Cleanup for engine private parameters, if there is, needs to be implemented, otherwise set to NULL */

void (*clear_eng_params)(struct engine *eng);

/* Parsing of task private parameters, if there is, need to be implemented, otherwise set to NULL */

int (*fill_task_params)(GKeyFile *config, struct task *task);

/* Cleanup for task private parameters, if there is, need to be implemented, otherwise set to NULL */

void (*clear_task_params)(struct task *tk);

/* Interface to start the task */

int (*start_task)(struct engine *eng, struct task *tk);

/* Interface to stop the task */

void (*stop_task)(struct engine *eng, struct task *tk);

/* Fill in PID related private parameters */

int (*alloc_pid_params)(struct engine *eng, struct task_pid **tk_pid);

/* Destroy PID related private parameters */

void (*free_pid_params)(struct engine *eng, struct task_pid **tk_pid);

/* Private command support required by the third party strategy, if not, set to NUL */

int (*eng_mgt_func)(struct engine *eng, struct task *tk, char *cmd, int fd);

};

A sample configuration file is shown below, please refer to the configuration file description section for details:

#thirdparty

[engine]

name=thirdparty

project=test

eng_name=my_engine

libname=/user/lib/etmem_fetch/code_test/my_engine.so

ops_name=my_engine_ops

engine_private_key=engine_private_value

[task]

project=test

engine=my_engine

name=background1

type=pid

value=1798245

task_private_key=task_private_value

**NOTE** ：

Users need to use the dynamic library of the scan module provided by `etmem` and implement the interface in the structure required by `etmem`

The fd in `eng_mgt_func` interface cannot write 0xff and 0xfe words

Support adding multiple different third-party strategy dynamic libraries in a project, distinguished by `eng_name` in the configuration file

### etmem supports memory expansion using AEP

#### Use case

Use the `etmem` component package to enable memory hierarchical expansion to the path of AEP.

Scan large pages of VMs within the node and perform strategy elimination through the `cslide` engine to move the cold memory to the AEP.

#### How to use

Use the `cslide` engine for memory expansion, the following parameter examples are available, please refer to the configuration file description chapter for specific parameter meanings.

#cslide

[engine]

name=cslide

project=test

node_pair=2,0;3,1

hot_threshold=1

node_mig_quota=1024

node_hot_reserve=1024

[task]

project=test

engine=cslide

name=background1

type=pid

value=1823197

vm_flags=ht

anon_only=no

ign_host=no

 **WARNING** : Prohibit concurrent scanning of the same process

Meanwhile, this `cslide` strategy supports private commands.


- showtaskpages
- showhostpages

For the engine and all tasks that use this strategy engine, you can use these two commands to view task-related page access and the use of system large pages on the host of the virtual machine.

Example commands are as follows:

etmem engine showtaskpages <-t task_name> -n proj_name -e cslide -s etmemd_socket

etmem engine showhostpages -n proj_name -e cslide -s etmemd_socket

**Note**: showtaskpages and showhostpages are only supported when the engine uses `cslide`.

#### Command-line parameter description
| Parameter         | Meaning                                                      | Required | Available parameter | Description                                                  |
| ----------------- | ------------------------------------------------------------ | -------- | ------------------- | ------------------------------------------------------------ |
| -n / -\-proj_name | Specify the name of the project                              | YES      | YES                 | Specify the name of the project that already exists and needs to be executed |
| -s / -\-socket    | The socket name to communicate with the etmemd server. Must be the same as that specified when etmemd is started | YES      | YES                 | Must be configured. When there is more than one etmemd, the administrator chooses which etmemd to communicate with |
| -e / -\-engine    | Specify the name of the engine to be executed                | YES      | YES                 | Specify the name of the engine that already exists and needs to be executed |
| -t / -\-task_name | Specify the name of the task to be performed                 | NO       | YES                 | Specify the name of the task that already exists and needs to be executed |

## Contribution

1.  Fork the repository.
2.  Create Feat_xxx branch.
3.  Commit local code.
4.  Create Pull Request.
