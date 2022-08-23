# This repo contains anible definitions for setting up server for CPC cluster
Ansible playbooks are ment to be used on non deprecated CentOS (CentOS 7). If you run it on any other (highter, not supported) version, it will crash unexpectly.

It's not fully compatible with debian based servers. If you run it on them, it will crash expectly. Compatibility for debian based distros is planned, once it will be needed. 

## List of playbooks
`./playbook.yaml`
- role: `server`
    - Install cockpit
    - Configure firewall
- role: `k8s_node`
    - Intall containerd
    - Configures containerd
    - **todo cgroups**
    - Intall K8S
    - Disables SWAP (K8S)
- role: `k8s_master`
    - Creates user for administrating cluster, see `./roles/k8s_master/vars/main.yaml`

`./playbooks/read_k8s_conf.yaml`
- Add read rights for `kube` user to `/etc/kubernetes/admin.conf` file  

## How to run it?
### Requirements
- ansible installed
- ssh access to nodes
- python3 installed on nodes

### How to run it
1. Modify `./inventorys/inventory.yaml`
2. Install all requirements
    ```shell
    ansible-galaxy install -r requirements.yml
    ```
3. Run playbooks
    ```shell
    ansible-playbook playbook.yaml
    ```