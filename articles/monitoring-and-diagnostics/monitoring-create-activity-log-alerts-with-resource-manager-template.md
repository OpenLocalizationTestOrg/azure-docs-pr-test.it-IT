---
title: "un avviso di log di attività con un modello di gestione risorse aaaCreate | Documenti Microsoft"
description: Ricevere notifica della creazione di risorse di Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="daaad-103">Creare un avviso di log attività con un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="daaad-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="daaad-104">In questo articolo illustra come toouse un [modello di Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure gli avvisi del registro attività.</span><span class="sxs-lookup"><span data-stu-id="daaad-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="daaad-105">Tramite i modelli è possibile configurare facilmente numerosi avvisi che vengono attivati in base a condizioni specifiche degli eventi del log attività nell'ambito del processo di distribuzione automatica.</span><span class="sxs-lookup"><span data-stu-id="daaad-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="daaad-106">passaggi di base di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="daaad-106">hello basic steps are:</span></span>

1. <span data-ttu-id="daaad-107">Creare un modello come un file JSON che descrive la modalità attività hello toocreate log avviso.</span><span class="sxs-lookup"><span data-stu-id="daaad-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="daaad-108">Distribuire il modello di hello utilizzando [qualsiasi metodo di distribuzione](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="daaad-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="daaad-109">Modello di Resource Manager per un avviso del log attività</span><span class="sxs-lookup"><span data-stu-id="daaad-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="daaad-110">toocreate un avviso di log attività utilizzando un modello di gestione delle risorse, si crea una risorsa di tipo hello `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="daaad-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="daaad-111">Compilare quindi tutte le proprietà correlate.</span><span class="sxs-lookup"><span data-stu-id="daaad-111">Then you fill in all related properties.</span></span> <span data-ttu-id="daaad-112">Il modello seguente crea un avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="daaad-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

<span data-ttu-id="daaad-113">Per alcuni esempi di modelli di avvisi del log attività, visitare la [raccolta di modelli di avvio rapido](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights).</span><span class="sxs-lookup"><span data-stu-id="daaad-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daaad-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="daaad-114">Next steps</span></span>
- <span data-ttu-id="daaad-115">[Altre informazioni sugli avvisi](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="daaad-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="daaad-116">Informazioni su come tooadd [gruppi di azioni utilizzando un modello di gestione risorse](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="daaad-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="daaad-117">Informazioni su come troppo[creare tutte le operazioni del motore di scalabilità automatica per la sottoscrizione di un log di attività avviso toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="daaad-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="daaad-118">Informazioni su come troppo[creare tutte le operazioni di scala/scalabilità di scalabilità automatica non riuscita per la sottoscrizione di un log di attività avviso toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="daaad-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
