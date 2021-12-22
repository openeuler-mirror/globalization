# Operator-manager
[![](https://img.shields.io/badge/language-Go-brightgreen.svg)](https://github.com/golang/go)
[![](https://img.shields.io/badge/Dependence-Kubebuilder-blue.svg)](https://book.kubebuilder.io/) 
[![](https://img.shields.io/badge/Reference-OLM-important.svg)](https://operatorframework.io)

## Overview

`Operator-Manager` is a lightweight Operator management framework designed based on [kubebuilder](https://book.kubebuilder.io/) architecture. The framework is mainly based on [kubenetes](https://kubernetes.io/) custom resources, deploying the required version of `Operator` through stateful operation management mode, and can support `Operator` uninstallation, version update, and other operations to achieve convenient cloud-native application management. 

## Architecture

<img src="https://z3.ax1x.com/2021/03/31/cA4nw6.png" alt="Architecture" style="zoom:30%;" align="left"/>

The design principle of `Operator-Manager` is to use `operator` to manage `operator`, which is based on Kubernetes secondary development and can help operations and maintenance staff to manage stateful applications efficiently. The `operator-manager` regards the `operator` to be managed as a kind of stateful application and manages the `crd`, `service account`, `webhook`, and other dependencies of the `operator`.

`Operator-Manager` is mainly based on the following three types of `crd` and `controller`.

| Resource              | Controller                       | Version  | Description                                                  |
| --------------------- | -------------------------------- | -------- | ------------------------------------------------------------ |
| ClusterServiceVersion | ClusterServiceVersion_Controller | v1alpha1 | Including Operator's application metadata, name, version, logo, required resources, installation strategy, etc... |
| BluePrint             | BluePrint_Controller             | v1       | Resolve and deploy the crd resources that csv and operator depend on, and implement version management based on BluePrint in the cluster |
| Subscription          | Subscription_controller          | v1       | Connect with the user, and the user initiates a request by modifying the relevant instance of the subscription deployed in the cluster |

| controller                       | Creatable Resources        |
| -------------------------------- | -------------------------- |
| ClusterServiceVersion_Controller | Deployment                 |
| ClusterServiceVersion_Controller | Service Account            |
| ClusterServiceVersion_Controller | (Cluster)Roles             |
| ClusterServiceVersion_Controller | (Cluster)RoleBindings      |
| BluePrint_Controller             | Custom Resource Definition |
| BluePrint_Controller             | ClusterServiceVersion      |
| Subscription_Controller          | BluePrint                  |

## Design

Compared with the [OLM](https://operatorframework.io) architecture designed by `CoreOS`, our lightweight `operator` management architecture eliminates directory management and reduces resource overhead. `Operator Manager` consists of three Controllers: `Subscription Controller`, `BluePrint Controller` and `ClusterServiceVersion Controller`. The `Subscription Controller` is responsible for processing the subscription request initiated by the user, interacting with the [operatorhub](https://operatorhub.io/), completing the operator verification, downloading the required dependent resources from the cloud server, and resolving the user subscription to create the corresponding `BluePrint CRD`. `BluePrint Controller` is responsible for resolving dependencies and creating CRDs for operators to be created/upgraded/rolled back/deleted. The `ClusterServiceVersion Controller` is responsible for deploying the operators to be created/upgraded/rolled back/deleted to the cluster through the `deployment` controller. After checking the dependent resources and dependent permissions, deploy the `service account` and `RBAC rules`.

## Features

| Feature                             | Completion Status  |
| ----------------------------------- | ------------------ |
| User initiated subscription request | :heavy_check_mark: |
| Operator dependency resolution      | :heavy_check_mark: |
| Install and deploy operator         | :heavy_check_mark: |
| Version management                  | :heavy_check_mark: |
| Bind service account                | :heavy_check_mark: |
| Authority management                | :heavy_check_mark: |
| Status check                        | :heavy_check_mark: |
| Uninstall and remove operator       | :heavy_check_mark: |
| Docking operatorhub.io              | :heavy_check_mark: |
| Web Dashboard                       | :x:                |


## Prerequisites
- [git][git_tool]
- [go][go_tool] version v1.13+.
- [docker][docker_tool] version 17.03+.
- [kubectl][kubectl_tool] version v1.11.3+.
- [kubebuilder][kubebuilder_tool] 
- Access to a Kubernetes v1.16.3+ cluster.

The `MakeFile` exists in the root directory of the project. After the file is executed, the following tools will be installed during the process of creating the project:
- [kustomize](https://kubernetes-sigs.github.io/kustomize/) 
- [controller-gen](https://github.com/kubernetes-sigs/controller-tools) 


## Quick Start

### Install

1. Execute `cd $GOPATH/src/github.com && mkdir -p buptGophers && cd buptGophers`
2. Download the project source code to the local repository, execute `git clone https://gitee.com/openeuler2020/team-1924513571.git`
3. Change the project name, make sure the project path is correct, execute `mv team-1924513571 operator-manager && cd operator-manager`
4. Install the `operator-manager` project dependencies according to `MAKEFILE`, execute `make install`

**NOTE:** The project now supports ARM/AMD architecture deployment. You may encounter installation errors after executing the `make install` command. Please make sure the following operations: `ENV GOPROXY="https://goproxy.io`/`ENV GO111MODULE=onGOPROXY`.If you encounter other problems, please contact us.

## Use loaclly

1. Start Project

    Excute `make run ` locally
    
2. Subscription Request

   Once the project starts normally, users can initiate operator management by deploying a `cr` instance of `subscription` and deploying that `cr` instance to the cluster manually. 

   For `cr` instances, see the project directory `/config/samples`.

   ```yaml
   apiVersion: operators.coreos.com.operator-manager.domain/v1
   kind: Subscription
   metadata:
     name: subscription-sample
   spec:
     # Add fields here
     startingCSV: prometheus.0.22.2
     option: create
     foo: bar
   status:
     opstatus: not operate
   ```
   **NOTE:** To delete, change the `spec.option` field to `delete`.

3. Monitor the running status of the cluster
   
    Users can check the running status of `operator-manager` according to the log information printed by the cluster, or obtain the running status of `subscription`, `blueprint`, `clusterserviceversion`, `crd`, `deployment`, ` pod`, `serviceaccount`, `RBAC rules` and other related resources through the `kubect` command to check whether the user subscription content is completed.

4. Other operations

    The user can also directly design the `cr` instance of `BluePrint` to complete the management operation of `operator`. However, the `cr` instance of `BluePrint` requires a lot of manual modification information. It is recommended that the user complete the `operator` management operation by the `cr` of `Subscription`.

5. Start the file server

    Users can access the `community-operators` directory and execute `go mod download` operation to configure the `Gin` environment. Execute `go run main.go` to start the local file server.  

# Key Concepts

## Subscription

Connect with the user. The user initiates a request by modifying the relevant instance of the subscription deployed in the cluster.

## BluePrint

Resolve and deploy `crd` resources that `csv` and `operator` depend on, and implement version management based on `BluePrint` inside the cluster.

## ClusterServiceVersion

Include:

- Application metadata. (name, description, version definition, links, icons, labels, etc.)
- Installation strategies, including the set of deployments required during the `Operator` installation and the set of permissions such as `service accounts`, RBAC roles, and bindings.
- CRDs: Including the type of `CRD`, the service it belongs to, other k8s native resources interacted by `operator` and `spec`, `status` field descriptors that contain semantic information about the model.

## CRD

To simplify the cost of running applications in `Kubernetes`, OLM can discover and resolve dependencies between running applications by defining additional metadata on the application.

Each `Operator` must define the following:

- The `CRD` that it is responsible for managing, for example, `Operator Etcd` is used to manage `EtcdCluster`;
- The `CRD` it depends on, for example, `Operator Valut` depends on `EtcdCluster` because Valut is supported by etcd.
  The basic dependency resolution is then achieved by finding the corresponding `Operator` to manage and install the `CRD`s required by the application. The way users interact with the directory may further limit dependency resolution.

### Controller

Controller is the core concept of `Kubernetes`. The job of the controller is to ensure that the actual state (including the cluster state, as well as the external state) matches the desired state of any given object. This process is called reconciling. In `controller-runtime`, the logic that implements reconciling for a specific type is called `Reconciler`, which is the key logic of the controller.

## Acknowledgement

- [OpenEuler](https://openeuler.org/): `Operator-manager` project uses the OpenEuler operating system for development;
- [OSCHINA](https://www.oschina.net/): `Operator-manager` project comes from the OSCHINA open-source competition;
- [PENG CHENG LABORATORY](https://www.pcl.ac.cn/): `Operator-manager` project developed and tested on the Kunpeng server of Pengcheng laboratory；

[architecture]: /doc/design/architecture.md
[philosophy]: /doc/design/philosophy.md
[installation guide]: /doc/install/install.md
[git_tool]:https://git-scm.com/downloads
[go_tool]:https://golang.org/dl/
[docker_tool]:https://docs.docker.com/install/
[kubectl_tool]:https://kubernetes.io/docs/tasks/tools/install-kubectl/
[kubebuilder_tool]:https://book.kubebuilder.io/quick-start.html
