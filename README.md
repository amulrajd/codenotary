# This project provisions immudb using following tools and technologies
 | Type           | Technology            | Comments                                                                                                                                |
|----------------|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
 | Virtualization | Oracle VM and Vagrant | Vagrant tool to manage VM                                                                                                               |
 | GitOps         | Flux                  | Flux is also used to bootstrap the cluster with infrastructure tools such as metallb,ingress controller and grafana.Also deploys immudb |
 | Kubernetes     | Standard              | deployed using kubeadm                                                                                                                  |

# Prerequisites
* Install Oracle VM, vagrant and flux tool using yum or apt depending on the linux variants
* Update the Vagrantfile with IP addresses of the contol plane and worker nodes
```
    vi vagrant/Vagrantfile
```
# Procedure for provisioning VMs and k8s cluster
```
vagrant up
```
* This deploys a 3 node cluster (1 master and 2 workers nodes)
* The bootstrap scripts install necessary packages and creates an empty k8s cluster

# Bootstrap with flux
```
flux bootstrap git \
     --url=ssh://git@gitlab.com/amulraj/codenotary \
     --path=flux/ \
     --branch=main \
     --private-key-file=<path_to_ssh-private-key_to_access_gitlab_repo>

```