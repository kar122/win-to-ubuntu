https://github.com/kar122/managedapp/blob/main/app.zip


[10/02 17:57] Sumanth Reddy
az managedapp definition create --name "ManagedWebApp" --location eastus --resource-group storageGroup --lock-level ReadOnly --display-name "Managed Web Application" --description "Web App with Azure mgmt" --authorizations "528eeba5-bbd0-4af4-b7ed-ab574b85a152:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" --package-file-uri "https://raw.githubusercontent.com/Azure/azure-managedapp-samples/master/Managed Application Sample Packages/201-managed-web-app/managedwebapp.zip"


[10/02 17:57] Sumanth Reddy
https://learn.microsoft.com/en-us/azure/azure-resource-manager/managed-applications/publish-service-catalog-app?tabs=azure-cli
Publish Azure Managed Application in service catalog - Azure Managed Applications
Describes how to publish an Azure Managed Application in your service catalog that's intended for members of your organization.




[19:24] Sumanth Reddy
https://raw.githubusercontent.com/kar122/managedapp/main/app.zip



az managedapp definition create 
 --name "ManagedVisionAiApp" 
 --location "eastus" 
 --resource-group workplaceos 
 --lock-level ReadOnly 
 --display-name "visionai" 
 --description "Web App with Azure mgmt"  
 --authorizations "528eeba5-bbd0-4af4-b7ed-ab574b85a152:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" 
 --package-file-uri "https://raw.githubusercontent.com/kar122/managedapp/main/app.zip"


az managedapp definition create --name "ManagedVisionAiApp" --location "eastus" --resource-group workplaceos --lock-level ReadOnly --display-name "visionai" --description "Web App with Azure mgmt" --authorizations "528eeba5-bbd0-4af4-b7ed-ab574b85a152:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" --package-file-uri "https://raw.githubusercontent.com/kar122/managedapp/main/app.zip"

Microsoft.Authorization/roleAssignments/write'


az vm show -g workplaceos -n linux -o json


#for personal subscription
az managedapp definition create --name "ManagedVisionAiApp" --location "eastus" --resource-group rg --lock-level ReadOnly --display-name "visionai" --description "Web App with Azure mgmt" --authorizations "5febf171-afca-46a5-85c7-a771308e1dea:b24988ac-6180-42a0-ab88-20f7382dd24c" --package-file-uri "https://umma.blob.core.windows.net/zip/app.zip?sp=r&st=2023-02-23T10:34:07Z&se=2023-02-23T18:34:07Z&spr=https&sv=2021-06-08&sr=c&sig=WvlCwLHWwfo2N405G7zWgiE%2F0cqVNkrcwGbt07q1nUg%3D"


#Service catalog vm details 
Adminusername : karadmin
Password: Karadmin12  

linuxgpu
username: linuxgpu
paswd: linuxgpu@123
[08/02 22:35] Sumanth Reddy
chmod 777 /var/run/docker.sock

winvm
username: winvm
pswd: Password@1234

# Download the installation package
output=$(wget https://aka.ms/azcmagent -O ~/install_linux_azcmagent.sh 2>&1);
if [ $? != 0 ]; then wget -qO- --method=PUT --body-data="{\"subscriptionId\":\"$subscriptionId\",\"resourceGroup\":\"$resourceGroup\",\"tenantId\":\"$tenantId\",\"location\":\"$location\",\"correlationId\":\"$correlationId\",\"authType\":\"$authType\",\"operation\":\"onboarding\",\"messageType\":\"DownloadScriptFailed\",\"message\":\"$output\"}" "https://gbl.his.arc.azure.com/log" &> /dev/null || true; fi;
echo "$output";

# Install the hybrid agent
bash ~/install_linux_azcmagent.sh;

# Run connect command
sudo azcmagent connect --resource-group "workplaceos" --tenant-id "4b690191-91e4-4b08-833d-a384c64b235f" --location "EastUS" --subscription-id "8914bde9-610c-4358-9250-68afdf4f3a97" --cloud "AzureCloud" 




 export subscriptionId="d7a8775a-317b-472a-bdbf-1ad615c18cf9"; export resourceGroup="NetworkWatcherRG"; export tenantId="ece4c752-c4ad-42ab-b69a-ed92cd8cab59"; export location="eastus"; export authType="token"; export correlationId="c11e685f-ac13-418f-9e85-38244635984c"; export cloud="AzureCloud"; 
 
 output=$(wget https://aka.ms/azcmagent -O ~/install_linux_azcmagent.sh 2>&1); if [ $? != 0 ]; then wget -qO- --method=PUT --body-data="{\"subscriptionId\":\"$subscriptionId\",\"resourceGroup\":\"$resourceGroup\",\"tenantId\":\"$tenantId\",\"location\":\"$location\",\"correlationId\":\"$correlationId\",\"authType\":\"$authType\",\"operation\":\"onboarding\",\"messageType\":\"DownloadScriptFailed\",\"message\":\"$output\"}" "https://gbl.his.arc.azure.com/log" &> /dev/null || true; fi; 
 
 echo "$output";
 
  bash ~/install_linux_azcmagent.sh; 
  
  
  sudo azcmagent connect --resource-group "NetworkWatcherRG" --tenant-id "ece4c752-c4ad-42ab-b69a-ed92cd8cab59" --location "East US" --subscription-id "d7a8775a-317b-472a-bdbf-1ad615c18cf9" --cloud "AzureCloud" --correlation-id "$correlationId"; 
