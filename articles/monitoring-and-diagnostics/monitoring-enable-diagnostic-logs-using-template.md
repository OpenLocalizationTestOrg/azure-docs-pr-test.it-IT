---
title: Abilitare automaticamente le impostazioni di diagnostica con un modello di Resource Manager | Microsoft Docs
description: Informazioni su come usare un modello di Resource Manager per creare impostazioni di diagnostica che permettono di trasmettere i log di diagnostica a Hub eventi o di memorizzarli in un account di archiviazione.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="60d3d-103">Abilitare automaticamente le impostazioni di diagnostica durante la creazione di risorse con un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="60d3d-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="60d3d-104">Questo articolo illustra come usare un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) per configurare le impostazioni di diagnostica in una risorsa durante la sua creazione.</span><span class="sxs-lookup"><span data-stu-id="60d3d-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="60d3d-105">Ciò consente di iniziare automaticamente a trasmettere le metriche e i log di diagnostica a Hub eventi, di memorizzarli in un account di archiviazione o di inviarli a Log Analytics quando viene creata una risorsa.</span><span class="sxs-lookup"><span data-stu-id="60d3d-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="60d3d-106">Il metodo da usare per abilitare i log di diagnostica tramite un modello di Resource Manager dipende dal tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="60d3d-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="60d3d-107">**risorse non di calcolo** , ad esempio Gruppi di sicurezza di rete, App per la logica e Automazione, usare le [impostazioni di diagnostica descritte in questo articolo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="60d3d-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="60d3d-108">**risorse di calcolo** , basate su WAD/LAD, usare il [file di configurazione WAD/LAD descritto in questo articolo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="60d3d-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="60d3d-109">Questo articolo illustra come configurare la diagnostica con entrambi i metodi.</span><span class="sxs-lookup"><span data-stu-id="60d3d-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="60d3d-110">I passaggi di base sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="60d3d-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="60d3d-111">Creare un modello come file JSON che descrive come creare la risorsa e abilitare la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="60d3d-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="60d3d-112">[Distribuire il modello con un metodo di distribuzione qualsiasi](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="60d3d-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="60d3d-113">Di seguito viene fornito un esempio del file JSON modello da generare per le risorse di calcolo e non di calcolo.</span><span class="sxs-lookup"><span data-stu-id="60d3d-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="60d3d-114">Modello per risorse non di calcolo</span><span class="sxs-lookup"><span data-stu-id="60d3d-114">Non-Compute resource template</span></span>
<span data-ttu-id="60d3d-115">Per le risorse non di calcolo, è necessario eseguire due operazioni:</span><span class="sxs-lookup"><span data-stu-id="60d3d-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="60d3d-116">Aggiungere parametri al BLOB dei parametri per il nome dell'account di archiviazione, l'ID dell'area regola del bus di servizio e/o l'ID dell'area di lavoro di Log Analytics OMS, abilitando la memorizzazione dei log di diagnostica in un account di archiviazione, la trasmissione dei log a Hub eventi e/o l'invio dei log a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="60d3d-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="60d3d-117">Nella matrice di risorse della risorsa per cui si vuole abilitare i log di diagnostica, aggiungere una risorsa di tipo `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="60d3d-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="60d3d-118">Il BLOB delle proprietà per l'impostazione di diagnostica è nel [formato descritto in questo articolo](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="60d3d-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="60d3d-119">L'aggiunta della proprietà `metrics` consentirà anche di inviare le metriche delle risorse a questi stessi output, purché [la risorsa supporti le metriche di Monitoraggio di Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="60d3d-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="60d3d-120">Di seguito è riportato un esempio completo che crea un'app per la logica e abilita la trasmissione agli hub eventi e la memorizzazione in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="60d3d-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="60d3d-121">Modello per risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="60d3d-121">Compute resource template</span></span>
<span data-ttu-id="60d3d-122">Per abilitare la diagnostica su una risorsa di calcolo, ad esempio una macchina virtuale o un cluster di Service Fabric, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="60d3d-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="60d3d-123">Aggiungere l'estensione Diagnostica di Azure alla definizione della risorsa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="60d3d-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="60d3d-124">Specificare un account di archiviazione e/o un hub eventi come parametro.</span><span class="sxs-lookup"><span data-stu-id="60d3d-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="60d3d-125">Aggiungere il contenuto del file XML WADCfg nella proprietà XMLCfg, usando le sequenze di escape corrette per i caratteri XML.</span><span class="sxs-lookup"><span data-stu-id="60d3d-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="60d3d-126">Quest'ultimo passaggio può risultare difficile.</span><span class="sxs-lookup"><span data-stu-id="60d3d-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="60d3d-127">[vedere questo articolo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) .</span><span class="sxs-lookup"><span data-stu-id="60d3d-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="60d3d-128">L'intero processo, esempi compresi, viene descritto in [questo documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60d3d-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60d3d-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60d3d-129">Next Steps</span></span>
* [<span data-ttu-id="60d3d-130">Altre informazioni sui log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="60d3d-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="60d3d-131">Trasmettere log di diagnostica di Azure a Hub eventi</span><span class="sxs-lookup"><span data-stu-id="60d3d-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

