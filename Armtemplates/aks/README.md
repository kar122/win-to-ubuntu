ubuntu
ubuntuVm@001




for generating SSH key 
sudo ssh-keygen -t ed25519 -C "karthikummareddy@gmail.com" -f /home/Documents/git/new_ssh_key

for finding SSH key
cat /home/Documents/git/new_ssh_key.pub

sudo cat /home/Documents/git/new_ssh_key 
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACDPOAhDemEoe3DAQs3CNcLuhTb1nSR+vRam+fxHLTy6NgAAAKD4hmZ5+IZm
eQAAAAtzc2gtZWQyNTUxOQAAACDPOAhDemEoe3DAQs3CNcLuhTb1nSR+vRam+fxHLTy6Ng
AAAEAkypQloUJe+UC2ZelluJWzpvCKcVlA9X6GD/fVVebuPs84CEN6YSh7cMBCzcI1wu6F
NvWdJH69Fqb5/EctPLo2AAAAGmthcnRoaWt1bW1hcmVkZHlAZ21haWwuY29tAQID
-----END OPENSSH PRIVATE KEY-----

PAT - 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


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

ubuntu karthik Password@00k

https://raw.githubusercontent.com/sumanthvisionify/microsoft_managed_web_app_demo/main/app.zip

https://raw.githubusercontent.com/sumanthvisionify/sample-aks/main/app.zip

https://raw.githubusercontent.com/kar122/microsoft_managed_web_app_demo/main/app.zip

https://raw.githubusercontent.com/kar122/aks-app/main/app.zip

https://raw.githubusercontent.com/kar122/aks-app/main/test/app.zip

https://raw.githubusercontent.com/Azure/azure-managedapp-samples/master/Managed Application Sample Packages/101-minimal-template/minimal-template.zip

https://raw.githubusercontent.com/kar122/aks-app/main/Managed Application Packages/1-Managed-AKS/app.zip

https://raw.githubusercontent.com/kar122/managedapp/main/app.zip

##for creating a resource group with managed property as "/subscriptions/8914bde9-610c-4358-9250-68afdf4f3a97/resourceGroups/akscustom/providers/Microsoft.Solutions/applications/resource" instead null

az group create --name aksresourcegroup --location eastus --managed-by "/subscriptions/8914bde9-610c-4358-9250-68afdf4f3a97/resourceGroups/akscustom/providers/Microsoft.Solutions/applications/resource"

##find the application definition id using below cli command az managedapp definition show --resource-group --name --query id --output tsv

az managedapp definition create --name "managedaks" --location eastus --resource-group aksmanagedapp --lock-level ReadOnly --display-name "visionaiaks" --description "aks cluster" --authorizations "394a804b-5258-4ba1-8ddf-1004a747994c:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" --package-file-uri "https://raw.githubusercontent.com/kar122/managedapp/main/app.zip"




az managedapp definition create \
  --name "ManagedAKS" \
  --location eastus \
  --resource-group aksmanagedapp \
  --lock-level ReadOnly \
  --display-name "Managed AKS" \
  --description "AKS" \
  --authorizations "394a804b-5258-4ba1-8ddf-1004a747994c:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" \
  --package-file-uri "https://raw.githubusercontent.com/kar122/aks-app/main/Managed Application Packages/1-Managed-AKS/app.zip"