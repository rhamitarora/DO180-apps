# DO180-apps
DO180 Repository for Sample Applications

image:
  repository: registry.ocp4.example.com:8443/etherpad
  name: etherpad
  tag: 1.8.18
route:
  host: development-etherpad.apps.ocp4.example.com

helm search repo

helm install example-app do280-repo/etherpad -f values.yaml --version 0.0.6


htpasswd -c -B -b htpasswdfile armstrong indionce
htpasswd -B -b htpasswdfile user2 password2

oc create secret generic htpasswd-secret --from-file=htpasswd=filename -n namespace
oc get oauth/cluster -o yaml > oauth.yaml
vi oauth.yaml
oc replace -f oauth.yaml 

oc adm policy remove-cluster-role-from-group self-provisioner system:authenticated:oauth

oc adm policy add-cluster-role-to-user cluster-admin jobs
oc adm policy add-cluster-role-to-user self-provisioner wozniak
oc adm policy remove-cluster-role-from-user cluster-admin wozniak
oc adm policy remove-cluster-role-from-user self-provisioner armstrong

oc new-project apollo
oc adm policy add-role-to-user admin armstrong -n apollo
oc adm policy add-role-to-user admin armstrong -n gemini
oc adm policy add-role-to-user view wozniak -n titan

oc adm groups new commander
oc adm groups new pilot
oc adm groups add-users commander armstrong
oc adm groups add-users pilot collins aldrin
oc adm policy add-role-to-group edit commander -n apollo
oc adm policy add-role-to-group view pilot -n apollo

oc create quota ex280-quota --hard=cpu=2,memory=1Gi,pods=3,services=6,replicationcontrollers=3 -n manhattan

oc adm taint nodes worker0 key1=value1:NoSchedule-
oc delete routes rocky
oc expose service rocky --hostname=rocky.apps.domainXX.example.com

oc scale --replicas=5 dc minion

oc autoscale dc hydra --max=9 --min=6  --cpu-percent=60
oc set resources dc hydra --limits=cpu=100m --requests=cpu=25m

./newcert "/C=US/ST=NV/L=Hiko/O=CIA/OU=USAF/CN=classified.apps.domainXX.example.com"
..................................
openssl genrsa -des3 -out mycert.key 2048
openssl req -x509 -new -key mycert.key -sha256 -days 3650 -out mycert.pem -subj "/C=US/ST=NV/L=Hiko/O=CIA/OU=USAF/CN=classified.apps.domainXX.example.com" 
openssl genrsa -out tls.key 2048
openssl req -new -key tls.key -out tls.csr -subj "/C=US/ST=NV/L=Hiko/O=CIA/OU=USAF/CN=classified.apps.domainXX.example.com" 
openssl x509 -req -in tls.csr -CA mycert.pem -CAkey mycert.key -CAcreateserial -out tls.crt -days 1650

oc create route edge oxcart \
  --hostname=secureapp.apps-crc.testing \
  --service=secureapp \
  --cert=tls.crt \
  --key=tls.key
curl -k https://classified.apps.domainXX.example.com

oc create secret generic magic --from-literal key=decoder_ring --from-literal value=XpWy9KdcP3Tr9FFHGQgZgVRCKukQdrQsbcl0c2ZYhDk= -n math

oc set env --from=secret/magic dc/qed

oc create serviceaccount ex280sa
oc adm policy add-scc-to-user anyuid -z ex280sa

oc set serviceaccount dc oranges ex280sa
oc describe svc oranges
oc edit  svc oranges
Change "Selector: deploymentconfig=orange" --> "Selector: deploymentconfig=oranges"

oc describe  node worker0.domain2.example.com
oc label node worker0 star=trek --overwrite

oc get events | grep -i menory 
oc describe dc atlas
oc set resources dc atlas  --resources=memory=80Mi

oc label namespace <your-namespace> openshift.io/cluster-monitoring=true


0 0 2 * * /path/to/your/script.sh
0 0 * * 2 /path/to/command
0 19 2 * * <command>
25 5 2 * * command_to_run


oc delete secrets kubeadmin -n kube-system


oc set volumes deployment.apps/postgresql-persistent --add --name postgresql-storage --type pvc --claim-class nfs-storage --claim-mode rwo --claim-size 10Gi --mount-path /var/lib/pgsql --claim-name postgresql-storage11

oc label namespace test x=y

oc login -u admin -p redhatocp https://api.ocp4.example.com:6443

oc adm must-gather --dest-dir /home/student/must-gather

tar cvaf mustgather.tar /home/student/must-gather

oc adm inspect clusteroperator/openshift-apiserver clusteroperator/kube-apiserver
oc adm inspect clusteroperator/openshift-apiserver --since 10m
ls ~/must-gather
tail -5 ~/must-gather/quay-io.../host_service_logs/masters/kubelet_service.log

oc adm inspect clusteroperator/openshift-apiserver --dest-dir /home/student/inspect --since 5m

ls inspect/

cat ~/inspect/cluster-scoped-resources/operator.openshift.io/openshiftapiservers/cluster.yaml


oc label namespace different-namespace network=different-namespace

spec:
podSelector:
	matchLabels:
		deployment: hello
ingress:
	- from:
		- namespaceSelector:
			matchLabels:
				network: different-namespace 
		  podSelector:
			matchLabels:
				deployment: sample-app
		ports:
		- port: 8080
		  protocol: TCP

deployment: hello 
network-policy project
pod: deployment=hello

oc label namespace different-namespace network=different-namespace
different-namespace
pod: deployment=sample-app

oc adm create-bootstrap-project-template -o yaml > template.yaml

oc set volumes deployment/db-pod --add --name="lvm-storage" --type="pvc" --claim-mode="readwriteowner" --claim-size="1Gi" --mount-path="/var/lib/mysql" --claim-class="lvms-vg1" --claim-name="db-pod-pvc"

policy-group.network.openshift.io/ingress: ""
network.openshift.io/policy-group: monitoring

helm repo list
helm repo add do280-repo http://helm.ocp4.example.com/charts
helm search repo --versions
helm install example-app do280-repo/etherpad -f values.yaml --version 0.0.6
helm list

image:
	repository: registry.ocp4.example.com:8443/etherpad
	name: etherpad
	tag: 1.8.18
route:
	host: etherpad.apps.ocp4.example.com


192.168.50.254
/exports-ocp4/
