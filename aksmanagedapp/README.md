
ubuntu
karthik
Password@00k

https://raw.githubusercontent.com/sumanthvisionify/microsoft_managed_web_app_demo/main/app.zip

https://raw.githubusercontent.com/kar122/aksmanagedapp/master/app.zip


az managedapp definition create --name "Managedaks" --location "eastus" --resource-group aksmanagedapp --lock-level ReadOnly --display-name "Visionaiaks" --description "aks cluster" --authorizations "528eeba5-bbd0-4af4-b7ed-ab574b85a152:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" --package-file-uri "https://raw.githubusercontent.com/kar122/aksmanagedapp/master/app.zip"



az managedapp definition create --name "sampleManagedApplication" --location eastus --resource-group aksmanagedapp --lock-level ReadOnly  --display-name "Sample managed applicationaks" --description "Sample managed application that deploys aks" --authorizations "528eeba5-bbd0-4af4-b7ed-ab574b85a152:8e3af657-a8ff-443c-a75c-2fe8c4bcb635" --package-file-uri "https://raw.githubusercontent.com/kar122/aksmanagedapp/master/app.zip"


{
	"$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json#",
	"handler": "Microsoft.Azure.CreateUIDef",
	"version": "0.1.2-preview",
	"parameters": {
		"config": {
			"isWizard": false,
			"basics": {
				"location": {
					"visible": "[basics('createNewCluster')]",
					"allowedValues": [
						"eastus",
						"westcentralus",
						"westeurope"
					]
				},
				"resourceGroup": {
					"allowExisting": true
				}
			}
		},
		"basics": [
			{
				"name": "createNewCluster",
				"type": "Microsoft.Common.OptionsGroup",
				"label": "Create new dev cluster?",
				"defaultValue": "No",
				"toolTip": "Create new cluster",
				"constraints": {
					"allowedValues": [
						{
							"label": "Yes",
							"value": true
						},
						{
							"label": "No",
							"value": false
						}
					],
					"required": true
				},
				"visible": true
			}
		],
		"steps": [
			{
				"name": "clusterDetails",
				"label": "Cluster Details",
				"elements": [
					{
						"name": "existingClusterSection",
						"type": "Microsoft.Common.Section",
						"elements": [
							{
								"name": "clusterLookupControl",
								"type": "Microsoft.Solutions.ArmApiControl",
								"request": {
									"method": "GET",
									"path": "[concat(subscription().id, '/resourcegroups/', resourceGroup().name,  '/providers/Microsoft.ContainerService/managedClusters?api-version=2022-03-01')]"
								}
							},
							{
								"name": "existingClusterResourceName",
								"type": "Microsoft.Common.DropDown",
								"label": "AKS Cluster Name",
								"toolTip": "AKS Cluster Resource Name",
								"constraints": {
									"allowedValues": "[map(steps('clusterDetails').existingClusterSection.clusterLookupControl.value, (item) => parse(concat('{\"label\":\"', item.name, '\",\"value\":\"', item.name, '\"}')))]",
									"required": true
								}
							}
						],
						"visible": "[equals(basics('createNewCluster'), false)]"
					},
					{
						"name": "newClusterSection",
						"type": "Microsoft.Common.Section",
						"elements": [
							{
								"name": "aksVersionLookupControl",
								"type": "Microsoft.Solutions.ArmApiControl",
								"request": {
									"method": "GET",
									"path": "[concat(subscription().id, '/providers/Microsoft.ContainerService/locations/', location(),  '/orchestrators?api-version=2019-04-01&resource-type=managedClusters')]"
								}
							},
							{
								"name": "newClusterResourceName",
								"type": "Microsoft.Common.TextBox",
								"label": "AKS cluster name",
								"defaultValue": "",
								"toolTip": "Use only allowed characters",
								"constraints": {
									"required": true,
									"regex": "^[a-z0-9A-Z]{6,30}$",
									"validationMessage": "Only alphanumeric characters are allowed, and the value must be 6-30 characters long."
								}
							},
							{
								"name": "kubernetesVersion",
								"type": "Microsoft.Common.DropDown",
								"label": "Kubernetes version",
								"toolTip": "The version of Kubernetes that should be used for this cluster. You will be able to upgrade this version after creating the cluster.",
								"constraints": {
									"allowedValues": "[map(steps('clusterDetails').newClusterSection.aksVersionLookupControl.properties.orchestrators, (item) => parse(concat('{\"label\":\"', item.orchestratorVersion, '\",\"value\":\"', item.orchestratorVersion, '\"}')))]",
									"required": true
								}
							},
							{
								"name": "vmSize",
								"type": "Microsoft.Compute.SizeSelector",
								"label": "VM size",
								"toolTip": "The size of virtual machine for VM.",
								"recommendedSizes": [
									"Standard_B4ms",
									"Standard_DS2_v2",
									"Standard_D4s_v3"
								],
								"constraints": {
									"allowedSizes": [
										"Standard_B4ms",
										"Standard_DS2_v2",
										"Standard_D4s_v3"
									],
									"excludedSizes": []
								},
								"osPlatform": "Linux"
							},
							{
								"name": "enableAutoScaling",
								"type": "Microsoft.Common.CheckBox",
								"label": "Enable auto scaling",
								"toolTip": "Enable auto scaling",
								"defaultValue": true						
							},
							{
								"name": "vmCount",
								"type": "Microsoft.Common.Slider",
								"min": 1,
								"max": 10,
								"label": "VMCount",
								"subLabel": "",
								"defaultValue": 1,
								"showStepMarkers": false,
								"toolTip": "Specify VM count",
								"constraints": {
									"required": false
								},
								"visible": true
							}
						],
						"visible": "[basics('createNewCluster')]"
					}
				]
			}
		],
		"outputs": {
			"location": "[location()]",
			"createNewCluster": "[basics('createNewCluster')]",
			"clusterResourceName": "[if(basics('createNewCluster'), steps('clusterDetails').newClusterSection.newClusterResourceName, steps('clusterDetails').existingClusterSection.existingClusterResourceName)]",
			"kubernetesVersion": "[steps('clusterDetails').newClusterSection.kubernetesVersion]",
			"vmSize": "[steps('clusterDetails').newClusterSection.vmSize]",
			"vmEnableAutoScale": "[steps('clusterDetails').newClusterSection.enableAutoScaling]",
			"vmCount": "[steps('clusterDetails').newClusterSection.vmCount]"
				}
	}
}















{
	"$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json#",
	"handler": "Microsoft.Azure.CreateUIDef",
	"version": "0.1.2-preview",
	"parameters": {
		"config": {
			"basics": {
				"location": {
					"visible": "[basics('createNewCluster')]",
					"allowedValues": [
						"eastus",
						"westcentralus",
						"westeurope"
					]
				},
				"resourceGroup": {
				}
			}
		},
		"basics": [
			{
				"name": "createNewCluster",
				"type": "Microsoft.Common.OptionsGroup",
				"label": "Create new dev cluster?",
				"defaultValue": "No",
				"toolTip": "Create new cluster",
				"constraints": {
					"allowedValues": [
						{
							"label": "Yes",
							"value": true
						},
						{
							"label": "No",
							"value": false
						}
					],
					"required": true
				},
				"visible": true
			}
		],
		"steps": [
			{
				"name": "clusterDetails",
				"label": "Cluster Details",
				"elements": [
					{
						"name": "existingClusterSection",
						"type": "Microsoft.Common.Section",
						"label": "label",
						"elements": [
							{
								"name": "clusterLookupControl",
								"type": "Microsoft.Common.Selector",
								"bladeSubtitle": "Subtitle Text",
								"label": "Control Label",
								"bladeTitle": "Title Text",
								"elements": [{
								"name": "clusterLookupControl",
								"type": "Microsoft.Common.Selector",
								"bladeSubtitle": "Subtitle Text",
								"sublabel": "",
								"label": "Control Label",
								"bladeTitle": "Title Text"
							}]
							  },
							{
								"name": "existingClusterResourceName",
								"type": "Microsoft.Common.DropDown",
								"label": "AKS Cluster Name",
								"toolTip": "AKS Cluster Resource Name",
								"constraints": {
									"allowedValues": "[map(steps('clusterDetails').existingClusterSection.clusterLookupControl.value, (item) => parse(concat('{\"label\":\"', item.name, '\",\"value\":\"', item.name, '\"}')))]",
									"required": true
								}
							}
						],
						"visible": "[equals(basics('createNewCluster'), false)]"
					},
					{
						"name": "newClusterSection",
						"type": "Microsoft.Common.Section",
						"label": "Label",
						"elements": [
							{
								"name": "aksVersionLookupControl",
								"type": "Microsoft.Common.Selector",
								"label": "AKS Version", 
								"sublabel": "1.26.0", 
								"bladeSubtitle": "Choose AKS Version", 
								"elements": [
									{
										"name": "aksVersionDropdown",
										"type": "Microsoft.Common.DropDown",
										"constraints": {
											"allowedValues": "[listAvailableVersions()]",
											"required": true
										},
										"toolTip": "AKS Version",
										"label": "AKS Version" 
									}
								]
							},
							{
								"name": "newClusterResourceName",
								"type": "Microsoft.Common.TextBox",
								"label": "AKS cluster name",
								"defaultValue": "",
								"toolTip": "Use only allowed characters",
								"constraints": {
									"required": true,
									"regex": "^[a-z0-9A-Z]{6,30}$",
									"validationMessage": "Only alphanumeric characters are allowed, and the value must be 6-30 characters long."
								}
							},
							{
								"name": "kubernetesVersion",
								"type": "Microsoft.Common.DropDown",
								"label": "Kubernetes version",
								"toolTip": "The version of Kubernetes that should be used for this cluster. You will be able to upgrade this version after creating the cluster.",
								"constraints": {
									"allowedValues": "[map(steps('clusterDetails').newClusterSection.aksVersionLookupControl.properties.orchestrators, (item) => parse(concat('{\"label\":\"', item.orchestratorVersion, '\",\"value\":\"', item.orchestratorVersion, '\"}')))]",
									"required": true
								}
							},
							{
								"name": "vmSize",
								"type": "Microsoft.Compute.SizeSelector",
								"label": "VM size",
								"toolTip": "The size of virtual machine for VM.",
								"recommendedSizes": [
									"Standard_B4ms",
									"Standard_DS2_v2",
									"Standard_D4s_v3"
								],
								"constraints": {
									"allowedSizes": [
										"Standard_B4ms",
										"Standard_DS2_v2",
										"Standard_D4s_v3"
									]
								},
								"osPlatform": "Linux"
							},
							{
								"name": "enableAutoScaling",
								"type": "Microsoft.Common.CheckBox",
								"label": "Enable auto scaling",
								"toolTip": "Enable auto scaling"					
							},
							{
								"name": "vmCount",
								"type": "Microsoft.Compute.UserNameTextBox",
								"osPlatform": "Window",
								"label": "VMCount",
								"defaultValue": "string",
								"toolTip": "Specify VM count",
								"constraints": {
									"required": false
								},
								"visible": true
							}
						],
						"visible": "[basics('createNewCluster')]"
					}
				]
			}
		],
		"outputs": {
			"location": "[location()]",
			"createNewCluster": "[basics('createNewCluster')]",
			"clusterResourceName": "[if(basics('createNewCluster'), steps('clusterDetails').newClusterSection.newClusterResourceName, steps('clusterDetails').existingClusterSection.existingClusterResourceName)]",
			"kubernetesVersion": "[steps('clusterDetails').newClusterSection.kubernetesVersion]",
			"vmSize": "[steps('clusterDetails').newClusterSection.vmSize]",
			"vmEnableAutoScale": "[steps('clusterDetails').newClusterSection.enableAutoScaling]",
			"vmCount": "[steps('clusterDetails').newClusterSection.vmCount]"
		}
	}
}
