---
title: un avviso di metrica con un modello di gestione risorse aaaCreate | Documenti Microsoft
description: Informazioni su come toouse un toocreate modello di gestione risorse una metrica tooreceive le notifiche tramite posta elettronica o webhook.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 41d62044-6bc5-4674-b277-45b919f58efe
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/21/2017
ms.author: johnkem
ms.openlocfilehash: dcf92b189f56a8389fff007c82197527239b96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-metric-alert-with-a-resource-manager-template"></a><span data-ttu-id="a64af-103">Creare un avviso metrica con un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a64af-103">Create a metric alert with a Resource Manager template</span></span>
<span data-ttu-id="a64af-104">Questo articolo viene illustrato come utilizzare un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Azure metrici avvisi.</span><span class="sxs-lookup"><span data-stu-id="a64af-104">This article shows how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Azure metric alerts.</span></span> <span data-ttu-id="a64af-105">In questo modo tooautomatically configurare avvisi per le risorse quando vengono create tooensure che tutte le risorse vengono monitorate in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="a64af-105">This enables you tooautomatically set up alerts on your resources when they are created tooensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="a64af-106">come indicato di seguito sono riportati i passaggi di base Hello:</span><span class="sxs-lookup"><span data-stu-id="a64af-106">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="a64af-107">Creare un modello come un file JSON che descrive la modalità toocreate hello avviso.</span><span class="sxs-lookup"><span data-stu-id="a64af-107">Create a template as a JSON file that describes how toocreate hello alert.</span></span>
2. <span data-ttu-id="a64af-108">[Distribuire il modello di hello utilizzando qualsiasi metodo di distribuzione](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a64af-108">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="a64af-109">Di seguito viene descritto come toocreate un modello di gestione risorse per un avviso da solo, quindi per un avviso durante la creazione di un'altra risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="a64af-109">Below we describe how toocreate a Resource Manager template first for an alert alone, then for an alert during hello creation of another resource.</span></span>

## <a name="resource-manager-template-for-a-metric-alert"></a><span data-ttu-id="a64af-110">Modello di Resource Manager per un avviso metrica</span><span class="sxs-lookup"><span data-stu-id="a64af-110">Resource Manager template for a metric alert</span></span>
<span data-ttu-id="a64af-111">toocreate un avviso utilizzando un modello di gestione delle risorse, si crea una risorsa di tipo `Microsoft.Insights/alertRules` e inserire tutte le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="a64af-111">toocreate an alert using a Resource Manager template, you create a resource of type `Microsoft.Insights/alertRules` and fill in all related properties.</span></span> <span data-ttu-id="a64af-112">Di seguito è riportato un modello che crea una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="a64af-112">Below is a template that creates an alert rule.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "type": "string",
            "metadata": {
                "description": "Name of alert"
            }
        },
        "alertDescription": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Description of alert"
            }
        },
        "isEnabled": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether alerts are enabled"
            }
        },
        "resourceId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Resource ID of hello resource emitting hello metric that will be used for hello comparison."
            }
        },
        "metricName": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Name of hello metric used in hello comparison tooactivate hello alert."
            }
        },
        "operator": {
            "type": "string",
            "defaultValue": "GreaterThan",
            "allowedValues": [
                "GreaterThan",
                "GreaterThanOrEqual",
                "LessThan",
                "LessThanOrEqual"
            ],
            "metadata": {
                "description": "Operator comparing hello current value with hello threshold value."
            }
        },
        "threshold": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "hello threshold value at which hello alert is activated."
            }
        },
        "aggregation": {
            "type": "string",
            "defaultValue": "Average",
            "allowedValues": [
                "Average",
                "Last",
                "Maximum",
                "Minimum",
                "Total"
            ],
            "metadata": {
                "description": "How hello data that is collected should be combined over time."
            }
        },
        "windowSize": {
            "type": "string",
            "defaultValue": "PT5M",
            "metadata": {
                "description": "Period of time used toomonitor alert activity based on hello threshold. Must be between five minutes and one day. ISO 8601 duration format."
            }
        },
        "sendToServiceOwners": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether alerts are sent tooservice owners"
            }
        },
        "customEmailAddresses": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Comma-delimited email addresses where hello alerts are also sent"
            }
        },
        "webhookUrl": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "URL of a webhook that will receive an HTTP POST when hello alert activates."
            }
        }
    },
    "variables": {
        "customEmails": "[split(parameters('customEmailAddresses'), ',')]"
    },
    "resources": [
        {
            "type": "Microsoft.Insights/alertRules",
            "name": "[parameters('alertName')]",
            "location": "[resourceGroup().location]",
            "apiVersion": "2016-03-01",
            "properties": {
                "name": "[parameters('alertName')]",
                "description": "[parameters('alertDescription')]",
                "isEnabled": "[parameters('isEnabled')]",
                "condition": {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource": {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri": "[parameters('resourceId')]",
                        "metricName": "[parameters('metricName')]"
                    },
                    "operator": "[parameters('operator')]",
                    "threshold": "[parameters('threshold')]",
                    "windowSize": "[parameters('windowSize')]",
                    "timeAggregation": "[parameters('aggregation')]"
                },
                "actions": [
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                        "sendToServiceOwners": "[parameters('sendToServiceOwners')]",
                        "customEmails": "[variables('customEmails')]"
                    },
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleWebhookAction",
                        "serviceUri": "[parameters('webhookUrl')]",
                        "properties": {}
                    }
                ]
            }
        }
    ]
}
```

<span data-ttu-id="a64af-113">Una spiegazione delle proprietà e schema hello per una regola di avviso [è disponibile qui](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="a64af-113">An explanation of hello schema and properties for an alert rule [is available here](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span>

## <a name="resource-manager-template-for-a-resource-with-an-alert"></a><span data-ttu-id="a64af-114">Modello di Resource Manager per una risorsa con un avviso</span><span class="sxs-lookup"><span data-stu-id="a64af-114">Resource Manager template for a resource with an alert</span></span>
<span data-ttu-id="a64af-115">In genere, un avviso in un modello di Resource Manager è più utile quando si crea un avviso durante la creazione di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="a64af-115">An alert on a Resource Manager template is most often useful when creating an alert while creating a resource.</span></span> <span data-ttu-id="a64af-116">Ad esempio, è consigliabile tooensure che un "CPU > 80%" regola viene impostata ogni volta che si distribuisce una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a64af-116">For example, you may want tooensure that a “CPU % > 80” rule is set up every time you deploy a Virtual Machine.</span></span> <span data-ttu-id="a64af-117">toodo, si aggiunge la regola di avviso hello come risorsa in una matrice di risorse hello per il modello di macchina virtuale e aggiunge una dipendenza utilizzando hello `dependsOn` ID risorsa di proprietà toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a64af-117">toodo this, you add hello alert rule as a resource in hello resource array for your VM template and add a dependency using hello `dependsOn` property toohello VM resource ID.</span></span> <span data-ttu-id="a64af-118">Di seguito è riportato un esempio completo che consente di creare una macchina virtuale di Windows e aggiunge un avviso che notifica amministratori della sottoscrizione quando hello utilizzo della CPU supera l'80%.</span><span class="sxs-lookup"><span data-stu-id="a64af-118">Here’s a full example that creates a Windows VM and adds an alert that notifies subscription admins when hello CPU utilization goes above 80%.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "newStorageAccountName": {
            "type": "string",
            "metadata": {
                "Description": "hello name of hello storage account where hello VM disk is stored."
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "Description": "hello name of hello administrator account on hello VM."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "Description": "hello administrator account password on hello VM."
            }
        },
        "dnsNameForPublicIP": {
            "type": "string",
            "metadata": {
                "Description": "hello name of hello public IP address used tooaccess hello VM."
            }
        }
    },
    "variables": {
        "location": "Central US",
        "imagePublisher": "MicrosoftWindowsServer",
        "imageOffer": "WindowsServer",
        "windowsOSVersion": "2012-R2-Datacenter",
        "OSDiskName": "osdisk1",
        "nicName": "nc1",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "sn1",
        "subnetPrefix": "10.0.0.0/24",
        "storageAccountType": "Standard_LRS",
        "publicIPAddressName": "ip1",
        "publicIPAddressType": "Dynamic",
        "vmStorageAccountContainerName": "vhds",
        "vmName": "vm1",
        "vmSize": "Standard_A0",
        "virtualNetworkName": "vn1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "vmID":"[resourceId('Microsoft.Compute/virtualMachines',variables('vmName'))]",
        "alertName": "highCPUOnVM",
        "alertDescription":"CPU is over 80%",
        "alertIsEnabled": true,
        "resourceId": "",
        "metricName": "Percentage CPU",
        "operator": "GreaterThan",
        "threshold": "80",
        "windowSize": "PT5M",
        "aggregation": "Average",
        "customEmails": "",
        "sendToServiceOwners": true,
        "webhookUrl": "http://testwebhook.test"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('newStorageAccountName')]",
            "apiVersion": "2015-06-15",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[variables('publicIPAddressName')]",
            "location": "[variables('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
                }
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[variables('virtualNetworkName')]",
            "location": "[variables('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[variables('nicName')]",
            "location": "[variables('location')]",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
                "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "publicIPAddress": {
                                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
                            },
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[variables('vmName')]",
            "location": "[variables('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
            ],
            "properties": {
                "hardwareProfile": {
                    "vmSize": "[variables('vmSize')]"
                },
                "osProfile": {
                    "computername": "[variables('vmName')]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "imageReference": {
                        "publisher": "[variables('imagePublisher')]",
                        "offer": "[variables('imageOffer')]",
                        "sku": "[variables('windowsOSVersion')]",
                        "version": "latest"
                    },
                    "osDisk": {
                        "name": "osdisk",
                        "vhd": {
                            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
                        },
                        "caching": "ReadWrite",
                        "createOption": "FromImage"
                    }
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
                        }
                    ]
                }
            }
        },
        {
            "type": "Microsoft.Insights/alertRules",
            "name": "[variables('alertName')]",
            "dependsOn": [
                "[variables('vmID')]"
            ],
            "location": "[variables('location')]",
            "apiVersion": "2016-03-01",
            "properties": {
                "name": "[variables('alertName')]",
                "description": "variables('alertDescription')",
                "isEnabled": "[variables('alertIsEnabled')]",
                "condition": {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource": {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri": "[variables('vmID')]",
                        "metricName": "[variables('metricName')]"
                    },
                    "operator": "[variables('operator')]",
                    "threshold": "[variables('threshold')]",
                    "windowSize": "[variables('windowSize')]",
                    "timeAggregation": "[variables('aggregation')]"
                },
                "actions": [
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                        "sendToServiceOwners": "[variables('sendToServiceOwners')]",
                        "customEmails": "[variables('customEmails')]"
                    },
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleWebhookAction",
                        "serviceUri": "[variables('webhookUrl')]",
                        "properties": {}
                    }
                ]
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a64af-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a64af-119">Next Steps</span></span>
* [<span data-ttu-id="a64af-120">Altre informazioni sugli avvisi</span><span class="sxs-lookup"><span data-stu-id="a64af-120">Read more about Alerts</span></span>](insights-receive-alert-notifications.md)
* <span data-ttu-id="a64af-121">[Aggiungere le impostazioni di diagnostica](monitoring-enable-diagnostic-logs-using-template.md) tooyour modello di gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a64af-121">[Add Diagnostic Settings](monitoring-enable-diagnostic-logs-using-template.md) tooyour Resource Manager template</span></span>

