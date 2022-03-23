First we will install the gatekeeper operator same as we did with the compliance operator so it will install in the background

```bash
<hub> oc apply -f ~/openshift-commons/remidiation-options/acm-integration-with-gatekeeper-operator/policy-gatekeeper-operator.yaml 
```
---
```bash
<hub> cd ~/openshift-commons/remidiation-options/acm-governance-feature-alone/
<hub> oc apply -f kubeadmin-policy.yaml
```
---
```bash
<hub> cd ~/openshift-commons/remidiation-options/acm-integration-with-gatekeeper-operator/
<hub> oc apply -f etcdencryption-policy.yaml
```

```bash
<managed cluster> oc get kubeapiserver -o=jsonpath='{range .items[0].status.conditions[?(@.type=="Encrypted")]}{.reason}{"\n"}{.message}{"\n"}'
```
