---
```bash
<hub> cd ~/openshift-commons/remidiation-options/acm-governance-feature-alone/
<hub> oc apply -f kubeadmin-policy.yaml
<managed cluster> watch oc get secret kubeadmin -n kube-system
```


