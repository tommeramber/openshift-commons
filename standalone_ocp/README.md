# Instructions

> Regenerate kubeadmin secret if it's already deleted

```bash
<standalone ocp> $ oc login
<standalone ocp> $ oc create secret generic kubeadmin --from-literal=password=lol -n kube-system 
```

## 1 Install Compliance Operator


## 2 Run a Scan


## 3 Show Profile


## 4 Show check results


## 5 Show Remidiation


## 6 Run remidiation


## 7 Regenerate Kubeadmin secret


## 8 Install Gatekeeper Operator and Generate Instance


## 9 Create Constraint + Template


## 10 Show Violation


## 11 Delete Kubeadmin && Show effect on violation


## 12 Try recreate Kubeadmin (Constaint == enforce mode)


Go Back to [MAIN Page](https://github.com/tommeramber/openshift-commons)
