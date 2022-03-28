
* Terminal 1 - Cluster Hub
* Terminal 2 - Managed Cluster

### Import managed cluster to ACM Hub

### Terminal 1
```bash
# ssh to hub ocp cluster
<hub> oc login 
<hub> git clone https://github.com/tommeramber/openshift-commons.git 
```

### Terminal 2
```
# ssh to managed ocp cluster
<managed cluster> oc login 
<managed cluster> git clone https://github.com/tommeramber/openshift-commons.git 
```

If in manged cluster kubeadmin secret already deleted, recreate it for the demo;
```bash
<managed cluster> oc get secret/kubeadmin -n kube-system
```
**IF output == empty:** 
```bash
<managed cluster> oc create secret generic kubeadmin --from-literal=password=lol -n kube-system
```

[Back to main page](https://github.com/tommeramber/openshift-commons)
