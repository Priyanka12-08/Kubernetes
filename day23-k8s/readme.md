# To check if a user has access to get po
kubectl auth can-i get pod
# To know your role 
kubectl auth whoami
# As admin you can check for other users as well. Example newadmin
k auth can-i get pod --as newadmin
o/p : no
# Now we can do role binding to allow few access to the user newadmin
k config set-credentials newadmin \--client-key=../day21-k8s/newadminkey \--client-certificate=../day21-k8s/newadmin.csr
using the certificates and key from the day21-ks folder

o/p:  User "newadmin" set.

# Create a new context for newadmin
k config set-context newadmin --cluster=kind-cka-cluster \--user=newadmin

# To see all the available contexts
k config get-contexts

# Next we have to switch to the context newadmin
 kubectl config use-context newadmin
Switched to context "newadmin".

 # 
 openssl x509 -req -in ../day21-k8s/newadmin.csr

 # Command to generate .crt file
 k get csr -o yaml > krishna.crt

 # Now we can do role binding to allow few access to the user newadmin
   kubectl config set-credentials krishna --client-key=krishna.key --client-certificate=krishna.crt --embed-certs=true

# Create a new context for krishna
k config set-context krishna --cluster=kind-cka-cluster \--user=krishna

# Need to check again
