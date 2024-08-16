# ocp-sysctl
# Using sysctl kernel settings in a pod
This document provides an example of modifying the kernel value for "net.ipv4.tcp_keepalive_time" from the default to "1800"

## Red Hat Documentation
https://docs.openshift.com/container-platform/4.14/nodes/containers/nodes-containers-sysctls.html

## Components

### Add kernel setting to the allowlist
[Multus allowed list of kernel values > "NetworkAttachmentDefinition.yml"](cm-cni-sysctl-allowlist.yml)

...
oc edit cm -n openshift-multus cni-sysctl-allowlist 
...

### Create NetworkAttachmentDefinition (Change namespace in the yaml!)
[NetworkAttachmentDefinition yaml > "NetworkAttachmentDefinition.yml"](NetworkAttachmentDefinition.yml)

...
oc create -f NetworkAttachmentDefinition.yml 
...

### This is an example pod definition that references the NetworkAttachmentDefinition
[Example pod with required annotation pod-with-annotation.yml](pod-with-annotation.yml)

...
oc create -f pod-with-annotation.yml
...

```
<managed cluster> $ kustomize build impersonation-resources/ | oc apply -f -
```
