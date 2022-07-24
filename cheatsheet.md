# Things I never remeber from the top of my head

## Kubernetes / Openshift

```
oc patch -n openshift-ingress-operator ingresscontroller/default --patch '{"spec":{"replicas": 2}}' --type=merge
for POD in `oc get pod --all-namespaces -o wide |grep lxworker04 |grep Terminating  |awk '{print $1"@"$2}' `; do oc delete pod `echo $POD |awk -F "@" '{print $2}'` -n `echo $POD |awk -F "@" '{print $1}'` --grace-period=0 --force;done
for i in `oc get csr |grep Pending |awk '{print $1}'`; do oc adm certificate approve $i; done
oc adm prune images --keep-tag-revision=1 --confirm
oc get secrets kube-apiserver-to-kubelet-signer -n openshift-kube-apiserver-operator -o yaml | grep tls.crt | awk '{ print $2}' | base64 -d > new_cert.crt && openssl x509 -text -noout -in new_cert.crt
oc -n netdata patch daemonset netdata-slave -p '{"spec": {"template": {"spec": {"nodeSelector": {"non-existing": "true"}}}}}'
```

## Elasticsearch (old)

```
es_util --query=_cat/health?v
es_util --query=_cat/shards?h=index,shard,prirep,state,unassigned.reason%7C | grep UNASSIGNED
es_util --query=_all/_settings -d '{"index.blocks.read_only_allow_delete": null}' -XPUT
es_util --query=_cat/shards -XGET | grep UNASSIGNED |  awk {'print $1'} | xargs -i es_util --query={} -XDELETE
curl -k -XDELETE --cert /etc/elasticsearch/secret/admin-cert --key /etc/elasticsearch/secret/admin-key https://elasticsearch:9200/.kibana.647a750f1787408bf50088234ec0edd5a6a9b2ac
```

## Tar.gz

```
tar -cvf camara-enviada.tar.gz logs
tar -xf camara-enviada.tar.gz
```

## Random

```
ldapsearch -z 0 -H ldap://ldapdns:389 -w 'your_password' -D "CN=your_user,OU=X,OU=X,OU=X,DC=X,DC=X,DC=X" -b "dc=X,dc=X,dc=X" "(cn=user_to_find)" sn givenName lastName -LLL
pbrun -h someserver.you.wanna.login -u root pobksh
scp -i .ssh/the_required_key user@dns/ip:origin_path destination_path
ansible infras -m shell -a "ping"
```

## GOVC

```
govc vm.option.info -vm lxworker01.ocp.com  -json
govc vm.power -off=true  lxworker19.ocp.com
govc vm.power -on=true  lxworker19.ocp.com
govc vm.destroy lxworker19.ocp.com
```
