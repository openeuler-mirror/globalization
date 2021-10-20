# eggo

### Introduction
The Eggo project was designed to automate flexibly the deployment of K8S clusters and to track deployment processes in mass production environments. In Cloud Native architecture, you can deploy clusters by tracking configuration with GitOps management.

- Support multiple versions of Linux: such as openEuler/CentOS/Ubuntu；
- Support multiple architectures (amd64/arm64) : a cluster supports nodes of multiple architectures;
- Support multiple deployments: binary and kubeadm (to be implemented);
- Support deploying online and offline, and deploying cluster via Gitops;

Currently, eggo has deployed clusters by executing commands. The following are three deployment modes that are supported by eggo:


- Deploy online. You only need to write the `yaml` configuration file for the deployment. You can download required rpm packages/binary files/plug-ins/docker images during the installation and deployment via the Internet (You can download from Google, so make sure your computer access to the Internet). Online deployment currently cannot support download and installation of plug-ins , and it will be implemented. 【Details in [eggo operation manual](/docs/manual.md)】
- Deploy Offline. Package all rpm packages/binary files/plug-ins/docker images into a `tar.gz` file in a required format. Then compile the corresponding `yaml` configuration file (details in [eggo operation manual](/docs/manual.md)), so that you can deploy clusters by executing commands.  
- Deploy new clusters with meta cluster via Gitops (to be implemented).

### Architecture
Details in [Software architecture description](./docs/general_design.md)

### Details
Details in [eggo operation manual](https://docs.openeuler.org/zh/docs/21.09/docs/Kubernetes/eggo%E8%87%AA%E5%8A%A8%E5%8C%96%E9%83%A8%E7%BD%B2.html)


### Versions

```
# Step 1: update file of VERSION, and push pr
$ vi VERSION
# Step 2: get release note by call releasenote.sh
$ ./hack/releasenote.sh
```

### Acknowledgement

The design of Eggo was inspired by [Kubekey](https://github.com/kubesphere/kubekey).

### Contribution

1.  Fork the repository
2.  Create Feat_xxx branch
3.  Commit your code
4.  Create Pull Request