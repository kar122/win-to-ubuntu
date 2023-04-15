Aks Service principal client id : 0f6b8d37-78b8-4a9b-9a03-af74980ccc4f
Aks Service principal client secret : TZv8Q~RAkxq3xkDUh5cmaPjiohlV.KEOTLb5HcQ-

az managedapp definition create --name "ManagedVisionAiAKS" --location "eastus" --resource-group aksrg --lock-level ReadOnly --display-name "visionaiaks" --description "Aks Cluster" --authorizations "5febf171-afca-46a5-85c7-a771308e1dea:b24988ac-6180-42a0-ab88-20f7382dd24c" --package-file-uri "https://akszip.blob.core.windows.net/app/app.zip?sp=rcwl&st=2023-04-03T13:19:38Z&se=2025-07-08T21:19:38Z&spr=https&sv=2021-12-02&sr=c&sig=j2BBgyhUIfX8krkQOMtLVgVlkH0cWtGOIVg8pLPJZi8%3D"


https://akszip.blob.core.windows.net/app/app.zip?sp=rcwl&st=2023-04-03T13:19:38Z&se=2025-07-08T21:19:38Z&spr=https&sv=2021-12-02&sr=c&sig=j2BBgyhUIfX8krkQOMtLVgVlkH0cWtGOIVg8pLPJZi8%3D


{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "aksClusterName": {
      "type": "String",
      "metadata": {
        "description": "The name of the AKS cluster."
      }
    },
    "aksLocation": {
      "type": "String",
      "metadata": {
        "description": "The location of the AKS cluster."
      }
    },
    "aksDnsPrefix": {
      "type": "String",
      "metadata": {
        "description": "The DNS prefix to use with the AKS cluster."
      }
    },
    "aksServicePrincipalClientId": {
      "type": "SecureString",
      "metadata": {
        "description": "The client ID of the service principal used by the AKS cluster."
      }
    },
    "aksServicePrincipalClientSecret": {
      "type": "SecureString",
      "metadata": {
        "description": "The client secret of the service principal used by the AKS cluster."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.ContainerService/managedClusters",
      "apiVersion": "2022-06-01",
      "name": "[parameters('aksClusterName')]",
      "location": "[parameters('aksLocation')]",
      "properties": {
        "dnsPrefix": "[parameters('aksDnsPrefix')]",
        "kubernetesVersion": "1.26.0",
        "servicePrincipalProfile": {
          "clientId": "[parameters('aksServicePrincipalClientId')]",
          "secret": "[parameters('aksServicePrincipalClientSecret')]"
        },
        "networkProfile": {
          "networkPlugin": "azure",
          "serviceCidr": "10.3.64.0/24",
          "dnsServiceIp": "10.3.64.10",
          "dockerBridgeCidr": "172.17.0.1/16"
        },
        "networkPolicy": {
          "enabled": "true",
          "networkPolicyType": "azure",
          "podCidr": "10.3.244.0/24"
        }
      },
      "resources": [
        {
          "type": "deployments",
          "apiVersion": "2021-07-01",
          "name": "my-deployment",
          "properties": {
            "apiVersion": "apps/v1",
            "kind": "Deployment",
            "metadata": {
              "name": "my-deployment"
            },
            "spec": {
              "replicas": 3,
              "selector": {
                "matchLabels": {
                  "app": "my-app"
                }
              },
              "template": {
                "metadata": {
                  "labels": {
                    "app": "my-label"
                  }
                },
                "spec": {
                  "containers": [
                    {
                      "name": "my-container",
                      "image": "visionify/visionaiweb:latest,
                    }
                  ]
                }
              }
            }
          }
        }
      ]
    }
  ],
  "outputs": {
    "aksClusterResourceId": {
      "type": "String",
      "value": "[resourceId('Microsoft.ContainerService/managedClusters', parameters('aksClusterName'))]"
    }
  }
}
