<img src="misc/A-Tune-logo.png" width="50%" height="50%"/>

English | [简体中文](./README-zh.md)

## Introduction 

**A-Tune** is an OS performance tuning engine based on AI. A-Tune uses AI technologies to enable the OS to understand services, simplify IT system optimization, and maximize optimal application performance at the same time.


I. Installation
----------

Supported OS: openEuler 20.03 LTS and above

### Method 1 (applicable to common users): Use the default A-Tune of openEuler.

```bash
yum install -y atune
```
For openEuler 20.09 and above, atune-engine is needed.

```bash
yum install -y atune-engine
```

### Method 2 (applicable to developers): Use source code in the repository for installation.

#### 1. Install dependent system software packages.
```bash
yum install -y golang-bin python3 perf sysstat hwloc-gui
```

#### 2. Install Python dependent packages.  

#### 2.1 Install dependent packages for A-Tune service.
```bash
yum install -y python3-dict2xml python3-flask-restful python3-pandas python3-scikit-optimize python3-xgboost python3-pyyaml
```
Or
```bash
pip3 install dict2xml Flask-RESTful pandas scikit-optimize xgboost scikit-learn pyyaml
```

#### 2.2 Install dependent packages for database. (Optional) 
Once you have already installed database application and wants to store A-Tune's collection data and tuning data to the database, the following dependent packages should also be installed:
```bash
yum install -y python3-sqlalchemy python3-cryptography
```
Or
```bash
pip3 install sqlalchemy cryptography
```
To use database, you should also select either of the following methods to install dependent packages based on the database applications.
| **Database** | **Yum**                         | ** Pip**              |
| ------------ | ------------------------------- | --------------------- |
| PostgreSQL   | yum install -y python3-psycopg2 | pip3 install psycopg2 |
#### 3. Download Source Code.
```bash
git clone https://gitee.com/openeuler/A-Tune.git
```

#### 4. Compile.
```bash
cd A-Tune
make models
make
```

#### 5. Install.
```bash
make collector-install
make install
```

II. Guide
------------

### 1. Configure the A-Tune service.

#### Modify the information of network and disk in the atuned.cnf.

You can run the following command to search the NIC that need to be collected data or to be optimized and modify the network configuration item in the /etc/atuned/atuned.cnf to the specified NIC.

```bash
ip addr
```

You can run the following command to search the disk that need to be collected data or to be optimized and modify the disk configuration item in the /etc/atuned/atuned.cnf to the specified disk.

```bash
fdisk -l | grep dev
```

### 2. Manage the A-Tune service.

#### Load and start the atuned and atune-engine service.

```bash
systemctl daemon-reload
systemctl start atuned
systemctl start atune-engine
```

#### Check the atuned or atune-engine service status.

```bash
systemctl status atuned
systemctl status atune-engine
```

### 3、Generate AI models.

You can save the newly collected data to the A-Tune/analysis/dataset directory and run the model generation tool to update the AI model in the A-Tune/analysis/models directory.

**Format**

python3 generate_models.py <OPTIONS>

**Parameter**

- OPTIONS

| Parameter        | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| --csv_path, -d   | Path for storing CSV files required for model training. The default path is A-Tune/analysis/dataset. |
| --model_path, -m | Path for storing the new models generated during training. The default path is A-Tune/analysis/models. |
| --select, -s     | Indicates whether to generate feature models. The default value is false. |
| --search, -g     | Indicates whether to enable parameter space search. The default value is false. |

Example：

```
python3 generate_models.py
```

### 4. Run the atune-adm command.

#### The list command.

This command is used to list the supported profiles and active profiles.

Format:

atune-adm list

Example:

```bash
atune-adm list
```

#### The profile command.

Manually activate the profile to make it in the active state.

Format:

atune-adm profile <PROFILE>

Example: Activate the profile corresponding to the web-nginx-http-long-connection.

```bash
atune-adm profile web-nginx-http-long-connection
```

#### The analysis command. (Online static tuning)

This command is used to collect real-time statistics of the system to identify and automatically optimize workload types.

Format:

atune-adm analysis [OPTIONS]

Example 1: Identify applications and automatically tune OS with the default model.

```bash
atune-adm analysis
```

Example 2: Identify applications with the user-defined training model.

```bash
atune-adm analysis --model /usr/libexec/atuned/analysis/models/new-model.m
```

#### The tuning command. (Offline dynamic tuning)

Search the dynamic space for parameters in the specified and find the optimal solution under the current environment configuration.

Format:

atune-adm tuning [OPTIONS] <PROJECT_YAML>

Example: Details in [the A-Tune offline tuning example](./examples/tuning). Each example has a corresponding README guide.

Details about other commands in the atune-adm help or [A-Tune User Guide](./Documentation/UserGuide/A-Tune-User-Guide.md).

III. Web UI
--------

[A-Tune-UI](https://gitee.com/openeuler/A-Tune-UI) is a web project base on A-Tune. Please check A-Tune-UI [README](https://gitee.com/openeuler/A-Tune-UI/blob/master/README.en.md) for details.

IV. How to contribute
--------

We welcome new contributors to participate in the project. And we are happy to provide guidance for new contributors. You need to sign [CLA](https://openeuler.org/en/cla.html) before contribution.

### Mail list
If you have any question or discussion, please contact [A-Tune](https://mailweb.openeuler.org/postorius/lists/a-tune.openeuler.org/).

### Routine Meeting
SIG Meeting is held at 10:00-12:00 AM on Friday every two weeks. You can submit topic by [A-Tune](https://mailweb.openeuler.org/postorius/lists/a-tune.openeuler.org/) mail list.

