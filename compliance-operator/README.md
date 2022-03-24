```bash
<hub> cd ~/openshift-commons/compliance-operator
<hub> oc apply -f policy-compliance-operator.yaml
```

**Wait until policy finishes**

---
```bash
<managed cluster> oc project openshift-compliance
<managed cluster> oc get pods
<managed cluster> oc get profiles.compliance.openshift.io
<managed cluster> oc get profiles.compliance.openshift.io ocp4-moderate -ojson | jq '.rules' | less
```
---
```bash
<hub> oc apply -f policy-moderate-scan.yaml
```
---
```bash
<managed cluster> oc get ScanSettingBinding moderate -o json | jq '.settingsRef'
<managed cluster> oc get ScanSetting default -o json | jq ' "Shchedule: " + .schedule, "Nodes to Scan: " + .roles[]'
<managed cluster> oc get ScanSettingBinding moderate -o json | jq '.profiles'
<managed cluster> oc get ComplianceSuite

<managed cluster> oc get ComplianceCheckResult
<managed cluster> oc get ComplianceCheckResult | grep PASS

<managed cluster> oc get ComplianceCheckResult | grep MANUAL
<managed cluster> oc get ComplianceCheckResult | grep MANUAL | grep ocp4-moderate-general-default-namespace-use
<managed cluster> oc get compliancecheckresults.compliance.openshift.io ocp4-moderate-general-default-namespace-use -o jsonpath='{.description}' ; echo
<managed cluster> oc get compliancecheckresults.compliance.openshift.io ocp4-moderate-general-default-namespace-use -o jsonpath='{.instructions}' ; echo

<managed cluster> oc get ComplianceCheckResult | grep ocp4-moderate-api-server-encryption-provider-config
<managed cluster> oc get complianceremediations.compliance.openshift.io
<managed cluster> oc get complianceremediations.compliance.openshift.io  | grep ocp4-moderate-api-server-encryption-provider-config
<managed cluster> oc get complianceremediations.compliance.openshift.io ocp4-moderate-api-server-encryption-provider-config -o json | jq '"Desired State:", .spec.current.object,"Status:", .status'
<managed cluster> oc get apiserver cluster -o json | jq '"Kind: "+ .kind, "Name: " + .metadata.name, "Spec: ", .spec' 


<managed cluster> oc get ComplianceCheckResult | grep ocp4-moderate-kubeadmin-removed
<managed cluster> oc get ComplianceCheckResult ocp4-moderate-kubeadmin-removed -o jsonpath='{.description}' ; echo
<managed cluster> oc get ComplianceCheckResult ocp4-moderate-kubeadmin-removed -o jsonpath='{.instructions}' ; echo


```

## How it should look in ACM's UI

1. A violation has been fired
![Screenshot from 2022-03-23 00-35-31](https://user-images.githubusercontent.com/60185557/159587810-ce16e5f5-41b6-4fae-b20c-65bc3b9334e0.png)

2. We can investigate the placement and cluster
![Screenshot from 2022-03-23 00-35-37](https://user-images.githubusercontent.com/60185557/159587818-a02bab3f-7c5f-4f9b-a987-ab488be2b5f8.png)

3. And also see the msg of the voilation => Go to `View details` to see the detailed information
![Screenshot from 2022-03-23 00-35-45](https://user-images.githubusercontent.com/60185557/159587844-10a57b01-8a98-4f75-9403-b6c959b157c8.png)

4. Down at the bottom you can see all the ComplianceCheckResult objects that have status of `FAIL` as the policy declared they should not exist on the managed cluster
![Screenshot from 2022-03-23 00-36-06](https://user-images.githubusercontent.com/60185557/159587862-0a2f70ef-73eb-4f8b-8802-fe8623b1ab2e.png)

5. Finaly we can see the specific ComplianceCheckResult we saw earlier, but now from the ACM's Hub UI, which means we can do everything from ACM directly
![Screenshot from 2022-03-23 00-36-27](https://user-images.githubusercontent.com/60185557/159587871-425c669c-12cb-4678-b3d8-46bcb49470db.png)


### Option 1 - complianceremediations apply=true
```bash
<managed cluster> # oc patch complianceremediations/ocp4-moderate-api-server-encryption-provider-config --patch '{"spec":{"apply":true}}' --type=merge
```
### Option 2 - using ACM's Governance feature
[Back to main page](https://github.com/tommeramber/openshift-commons)
