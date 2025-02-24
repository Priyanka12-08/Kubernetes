# These steps are performed by a new admin that has joined the team
< THE CMD WILL CREATE A NEW PRIVATE KEY WITH THE NAME NEWADMIN.KEY >
openssl genrsa -out newadmin.key 2048 

# this is a private key as it has the extension .key
< THIS STEP WILL CREATE A CERTIFICATE SIGNING REQUEST WITH THE NAME NEWADMIN.CSR > 
openssl req -new -key newadmin.key -out newadmin.csr -subj "/CN=newadmin"

# Commandto check the control plane
docker ps |grep control

# We docker exec into the control plane to read kubeapiserver.yaml file
docker exec -it cka-cluster-control-plane bash

# Once inside the control plane we go to manifests and get the kubeapiserver file
cd /etc/kubernetes/manifests/
root@cka-cluster-control-plane:/etc/kubernetes/manifests# ls -lrt
cat cat kube-apiserver.yaml

# In authorization we see it is Node,RBAC
 command:
    - kube-apiserver
    - --advertise-address=172.18.0.2
    - --allow-privileged=true
    - --authorization-mode=Node,RBAC

# IN CASE OF CERTIFICATE ISSUE THIS IS WHERE WE WILL VERIFY FROM