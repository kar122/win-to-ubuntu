
ubuntu
karthik
Password@00k

https://raw.githubusercontent.com/sumanthvisionify/microsoft_managed_web_app_demo/main/app.zip

https://raw.githubusercontent.com/sumanthvisionify/sample-aks/main/app.zip


https://raw.githubusercontent.com/kar122/aks-app/main/app.zip

##for creating a resource group with managed property as "/subscriptions/8914bde9-610c-4358-9250-68afdf4f3a97/resourceGroups/akscustom/providers/Microsoft.Solutions/applications/resource" instead null

az group create --name aksresourcegroup --location eastus --managed-by "/subscriptions/8914bde9-610c-4358-9250-68afdf4f3a97/resourceGroups/akscustom/providers/Microsoft.Solutions/applications/resource"


##find the application definition id using below cli command
az managedapp definition show --resource-group <resource-group-name> --name <service-catalog-definition-name> --query id --output tsv



az managedapp definition create --name "managedaks" --location eastus --resource-group aksmanagedapp --lock-level ReadOnly --display-name "visionaiaks" --description "aks cluster" --authorizations "394a804b-5258-4ba1-8ddf-1004a747994c:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" --package-file-uri "https://raw.githubusercontent.com/sumanthvisionify/microsoft_managed_web_app_demo/main/app.zip"





