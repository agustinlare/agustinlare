## Kubernetes / Openshift
oc patch -n openshift-ingress-operator ingresscontroller/default --patch '{"spec":{"replicas": 2}}' --type=merge
for POD in `oc get pod --all-namespaces -o wide |grep lxworker04 |grep Terminating  |awk '{print $1"@"$2}' `; do oc delete pod `echo $POD |awk -F "@" '{print $2}'` -n `echo $POD |awk -F "@" '{print $1}'` --grace-period=0 --force;done
