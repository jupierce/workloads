# MasterVertical Workload

The mastervertical workload playbook is `workloads/mastervertical.yml` and will run the mastervertical workload on your cluster.

Mastervertical purpose is a cluster density focused test that creates pods, builds, secrets, routes and more across the entire cluster.

Running from CLI:

```sh
$ cp workloads/inventory.example inventory
$ # Add orchestration host to inventory
$ # Edit vars in workloads/vars/mastervertical.yml or define Environment vars (See below)
$ time ansible-playbook -vv -i inventory workloads/mastervertical.yml
```

## Environment variables

### PUBLIC_KEY
Default: `~/.ssh/id_rsa.pub`  
Public ssh key file for Ansible.

### PRIVATE_KEY
Default: `~/.ssh/id_rsa`  
Private ssh key file for Ansible.

### ORCHESTRATION_USER
Default: `root`  
User for Ansible to log in as. Must authenticate with PUBLIC_KEY/PRIVATE_KEY.

### WORKLOAD_IMAGE
Default: `quay.io/openshift-scale/scale-ci-workload`  
Container image that runs the workload script.

### WORKLOAD_JOB_NODE_SELECTOR
Default: `true`  
Enables/disables the node selector that places the workload job on the `workload` node.

### WORKLOAD_JOB_TAINT
Default: `true`  
Enables/disables the toleration on the workload job to permit the `workload` taint.

### WORKLOAD_JOB_PRIVILEGED
Default: `true`  
Enables/disables running the workload pod as privileged.

### KUBECONFIG_FILE
Default: `~/.kube/config`  
Location of kubeconfig on orchestration host.

### PBENCH_SSH_PRIVATE_KEY_FILE
Default: `~/.ssh/id_rsa`  
Location of ssh private key to authenticate to the pbench results server.

### PBENCH_SSH_PUBLIC_KEY_FILE
Default: `~/.ssh/id_rsa.pub`  
Location of the ssh public key to authenticate to the pbench results server.

### ENABLE_PBENCH_AGENTS
Default: `false`  
Enables/disables the collection of pbench data on the pbench agent pods. These pods are deployed by the tooling playbook.

### PBENCH_SERVER
Default: There is no public default.  
DNS address of the pbench results server.

### SCALE_CI_RESULTS_TOKEN
Default: There is no public default.  
Future use for pbench and prometheus scraper to place results into git repo that holds results data.

### JOB_COMPLETION_POLL_ATTEMPTS
Default: `360`  
Number of retries for Ansible to poll if the workload job has completed. Poll attempts delay 10s between polls with some additional time taken for each polling action depending on the orchestration host setup.

### MASTERVERTICAL_TEST_PREFIX
Default: `mastervertical`  
Test to prefix the pbench results.

### MASTERVERTICAL_CLEANUP
Default: `true`  
Enables/disables cluster loader cleanup of this workload on completion.

### MASTERVERTICAL_BASENAME
Default: `mastervertical0`  
Basename used by cluster loader for the project(s) it creates.

### MASTERVERTICAL_PROJECTS
Default: `1000`  
Maximum number of projects that will be created by the mastervertical workload. Typically much higher values are used than the default for large scale tests.

## Smoke test variables

```
MASTERVERTICAL_TEST_PREFIX=mastervertical_smoke
MASTERVERTICAL_CLEANUP=true
MASTERVERTICAL_BASENAME=mastervertcial
MASTERVERTICAL_PROJECTS=1
```
