---
title: le impostazioni di diagnostica utilizzando un modello di gestione risorse di abilitare aaaAutomatically | Documenti Microsoft
description: Informazioni su come toouse un gestore di risorse modello toocreate le impostazioni di diagnostica che consentono di toostream la diagnostica registra tooEvent hub o archiviarli in un account di archiviazione.
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
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="43e72-103">Abilitare automaticamente le impostazioni di diagnostica durante la creazione di risorse con un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43e72-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="43e72-104">In questo articolo è illustrata la modalità è possibile utilizzare un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure le impostazioni di diagnostica su una risorsa quando viene creato.</span><span class="sxs-lookup"><span data-stu-id="43e72-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="43e72-105">In questo modo inizio tooautomatically streaming il tooEvent i log di diagnostica e le metriche di hub di archiviazione delle immagini in un Account di archiviazione o inviarli tooLog Analitica quando viene creata una risorsa.</span><span class="sxs-lookup"><span data-stu-id="43e72-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="43e72-106">metodo Hello per abilitare i log di diagnostica utilizzando un modello di gestione risorse dipende dal tipo di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="43e72-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="43e72-107">**risorse non di calcolo** , ad esempio Gruppi di sicurezza di rete, App per la logica e Automazione, usare le [impostazioni di diagnostica descritte in questo articolo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="43e72-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="43e72-108">**Calcolo** (WAD/LAD-) le risorse basate su utilizzano hello [file di configurazione di WAD/LAD descritto in questo articolo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="43e72-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="43e72-109">In questo articolo viene descritto come tooconfigure diagnostica usando dei metodi.</span><span class="sxs-lookup"><span data-stu-id="43e72-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="43e72-110">come indicato di seguito sono riportati i passaggi di base Hello:</span><span class="sxs-lookup"><span data-stu-id="43e72-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="43e72-111">Creare un modello come un file JSON che descrive la modalità toocreate hello risorse e abilitare la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="43e72-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="43e72-112">[Distribuire il modello di hello utilizzando qualsiasi metodo di distribuzione](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="43e72-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="43e72-113">Fornita di seguito è riportato un esempio di modello hello file JSON, è necessario toogenerate per non di calcolo e le risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="43e72-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="43e72-114">Modello per risorse non di calcolo</span><span class="sxs-lookup"><span data-stu-id="43e72-114">Non-Compute resource template</span></span>
<span data-ttu-id="43e72-115">Per le risorse non di calcolo, è necessario toodo due operazioni:</span><span class="sxs-lookup"><span data-stu-id="43e72-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="43e72-116">Aggiungere blob parametri toohello di parametri per il nome di account di archiviazione hello, ID regola bus di servizio e/o ID area di lavoro OMS Log Analitica (abilitazione dell'archivio di log di diagnostica in un account di archiviazione, il flusso di log tooEvent hub e/o l'invio di log tooLog Analitica).</span><span class="sxs-lookup"><span data-stu-id="43e72-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="43e72-117">Nella matrice di risorse hello della risorsa hello per cui si desidera tooenable i log di diagnostica, aggiungere una risorsa di tipo `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="43e72-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="43e72-118">segue Hello blob di proprietà per l'impostazione diagnostica hello [formato hello descritto in questo articolo](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="43e72-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="43e72-119">Aggiunta di hello `metrics` proprietà consentirà toothese metriche di tooalso trasmissione risorse stesso genera, a condizione che [risorse hello supporta le metriche di monitoraggio di Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="43e72-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="43e72-120">Di seguito è riportato un esempio completo che crea un'App di logica e attiva il flusso tooEvent hub e archiviazione in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="43e72-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="43e72-121">Modello per risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="43e72-121">Compute resource template</span></span>
<span data-ttu-id="43e72-122">diagnostica tooenable su una risorsa di calcolo, ad esempio una macchina virtuale o il cluster di Service Fabric, è necessario:</span><span class="sxs-lookup"><span data-stu-id="43e72-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="43e72-123">Aggiungere la definizione di risorsa VM hello diagnostica Azure estensione toohello.</span><span class="sxs-lookup"><span data-stu-id="43e72-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="43e72-124">Specificare un account di archiviazione e/o un hub eventi come parametro.</span><span class="sxs-lookup"><span data-stu-id="43e72-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="43e72-125">Aggiungere contenuto hello del file XML WADCfg nella proprietà XMLCfg hello, caratteri di escape correttamente tutti i caratteri XML.</span><span class="sxs-lookup"><span data-stu-id="43e72-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="43e72-126">Quest'ultimo passaggio può essere difficile tooget destra.</span><span class="sxs-lookup"><span data-stu-id="43e72-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="43e72-127">[Vedere l'articolo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) per un esempio che divisioni hello dello Schema di configurazione di diagnostica in variabili che vengono sottoposti a escape e formattate correttamente.</span><span class="sxs-lookup"><span data-stu-id="43e72-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="43e72-128">Hello intera, compresi gli esempi, descritto più avanti [in questo documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43e72-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43e72-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43e72-129">Next Steps</span></span>
* [<span data-ttu-id="43e72-130">Altre informazioni sui log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="43e72-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="43e72-131">Flusso i log di diagnostica Azure tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="43e72-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

