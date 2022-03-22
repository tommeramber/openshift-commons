```bash
<hub> oc apply -f policy-compliance-operator.yaml
```

Wait until policy finishes

```bash
<managed cluster> oc project openshift-compliance
<managed cluster> oc get pods
<managed cluster> oc get profiles.compliance.openshift.io
```

```bash
<hub> oc apply -f policy-moderate-scan.yaml
```

Wait until policy finishes

```bash
<managed cluster> oc describe ScanSettingBinding
<managed cluster> oc get ComplianceSuite
<managed cluster> oc get ComplianceCheckResult
```

