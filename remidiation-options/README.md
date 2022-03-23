```bash
<hub> oc apply -f policy-gatekeeper-operator.yaml 
<hub> cd ~/openshift-4-compliance-automation/redhat-acm/etcd-security/etcdencryption-policy
<hub> oc apply -f etcdencryption-policy.yaml
```


```bash
<managed cluster> oc get kubeapiserver -o=jsonpath='{range .items[0].status.conditions[?(@.type=="Encrypted")]}{.reason}{"\n"}{.message}{"\n"}'
```
