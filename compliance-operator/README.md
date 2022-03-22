```bash
<hub> oc apply -f policy-compliance-operator.yaml
```

Wait until policy finishes

```bash
<managed cluster> oc project openshift-compliance
<managed cluster> oc get pods
<managed cluster> oc get profiles.compliance.openshift.io
<managed cluster> oc get profiles.compliance.openshift.io ocp4-moderate -ojson | jq '.rules' | less
<managed cluster> oc get profiles.compliance.openshift.io ocp4-moderate -ojson | jq '.rules' | grep XXXX
```

```bash
<hub> oc apply -f policy-moderate-scan.yaml
```

Wait until policy finishes

```bash
<managed cluster> oc get ScanSettingBinding moderate -o json | jq '.settingsRef'
<managed cluster> oc get ScanSetting default -o json | jq ' "Shchedule: " + .schedule, "Nodes to Scan: " + .roles[]'
<managed cluster> oc get ScanSettingBinding moderate -o json | jq '.profiles'
<managed cluster> oc get ComplianceSuite
<managed cluster> oc get ComplianceCheckResult
<managed cluster> oc get ComplianceCheckResult | grep PASS
<managed cluster> oc get ComplianceCheckResult | grep MANUAL
<managed cluster> oc get ComplianceCheckResult | grep MANUAL | grep ocp4-moderate-general-default-namespace-use
<managed cluster> oc get compliancecheckresults.compliance.openshift.io ocp4-moderate-general-default-namespace-use -o jsonpath='{.description}'
<managed cluster> oc get compliancecheckresults.compliance.openshift.io ocp4-moderate-general-default-namespace-use -o jsonpath='{.instructions}'
<managed cluster> oc get ComplianceCheckResult | grep FAIL
<managed cluster> oc get ComplianceCheckResult | grep FAIL | grep ocp4-moderate-api-server-encryption-provider-config
<managed cluster> oc get ComplianceCheckResult ocp4-moderate-api-server-encryption-provider-config -o jsonpath='{.description}'
<managed cluster> oc get ComplianceCheckResult ocp4-moderate-api-server-encryption-provider-config -o jsonpath='{.instructions}'
<managed cluster> oc get complianceremediations.compliance.openshift.io
<managed cluster> oc get complianceremediations.compliance.openshift.io  | grep ocp4-moderate-api-server-encryption-provider-config
<managed cluster> oc get complianceremediations.compliance.openshift.io ocp4-moderate-api-server-encryption-provider-config -o json | jq '"Spec:", .spec,"Status:", .status'
```

### Option 1 - complianceremediations apply=true
```bash
<managed cluster> # oc patch complianceremediations/ocp4-moderate-api-server-encryption-provider-config --patch '{"spec":{"apply":true}}' --type=merge
```
### Option 2 - using ACM's Governance feature
**Go to [gatekeeper-operator folder](https://github.com/tommeramber/openshift-commons/tree/master/gatekeeper-operator)**

```

