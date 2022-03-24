First we will install the gatekeeper operator same as we did with the compliance operator so it will install in the background

```bash
<hub> oc apply -f ~/openshift-commons/remidiation-options/acm-integration-with-gatekeeper-operator/policy-gatekeeper-operator.yaml 
```

Next, apply [this RHACM govarnance policy](https://github.com/tommeramber/openshift-commons/tree/master/remidiation-options/acm-governance-feature-alone)
