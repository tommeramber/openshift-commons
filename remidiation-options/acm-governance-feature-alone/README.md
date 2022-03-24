```bash
<hub> cd ~/openshift-commons/remidiation-options/acm-governance-feature-alone/
<hub> oc apply -f kubeadmin-policy.yaml
<managed cluster> watch oc get secret kubeadmin -n kube-system
```
---
Finally, [integrate Gatekeeper](https://github.com/tommeramber/openshift-commons/tree/master/remidiation-options/acm-integration-with-gatekeeper-operator)

