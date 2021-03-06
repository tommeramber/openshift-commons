### Preperations
Delete ACM's delete kubeadmin policy 
Regenerate Kubeadmin Secret on Managed Cluster

```bash
<hub> cd ~/openshift-commons/remidiation-options/acm-integration-with-gatekeeper-operator
<hub> oc delete -f kubeadmin-policy.yaml
<managed cluster> oc create secret generic kubeadmin --from-literal=password=lol -n kube-system
```

## Instructions 
### 1. Install the gatekeeper operator policy from ACM - 
> Already Done

### 2. Deploy the gatekeeper template + constraint from ACM
```bash
<hub> oc apply -f policy-gatekeeper-verify-kubeadmin-deleted.yaml 
<managed cluster> oc get K8sDeleteKubeadmin -o json | jq '.items[0].status.violations'
```
> See the alert in RHACM (We recreated the secert) so it does exist on the cluster which is not a best practice

### 3. ReDeploy the RHACM govarnance policy which deletes the kubeadmin secret
```bash
<hub> oc apply -f kubeadmin-policy.yaml 
<managed cluster> watch oc get secret kubeadmin -n kube-system
<managed cluster> watch oc get K8sDeleteKubeadmin -o jsonpath='{.items[0].status.violations}'
```

> See that the alert in RHACM is gone

### 4. Attemp recreating the kubeadmin secret on the managed cluster

```bash
<managed cluster> oc create secret generic kubeadmin --from-literal=password=lol -n kube-system
```

> Gatekeeper blocks the API Call
