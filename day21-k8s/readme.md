#These steps are performed by a new admin that has joined the team

openssl genrsa -out newadmin.key 2048 # this is a private key as it has the extension .key
< THE ABOVE CMD WILL CREATE A NEW PRIVATE KEY WITH THE NAME NEWADMIN.KEY >
openssl req -new -key myuser.key -out myuser.csr -subj "/CN=myuser"