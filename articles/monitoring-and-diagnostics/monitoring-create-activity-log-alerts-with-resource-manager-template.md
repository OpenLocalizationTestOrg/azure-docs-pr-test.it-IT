---
title: "Creare un avviso di log attività con un modello di Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: 92076c7fe1f867919b7e02abf79cf0fb74fb7eb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="730cc-103">Creare un avviso di log attività con un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="730cc-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="730cc-104">L'articolo descrive come usare un [modello di Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) per configurare gli avvisi del log attività.</span><span class="sxs-lookup"><span data-stu-id="730cc-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span></span> <span data-ttu-id="730cc-105">Tramite i modelli è possibile configurare facilmente numerosi avvisi che vengono attivati in base a condizioni specifiche degli eventi del log attività nell'ambito del processo di distribuzione automatica.</span><span class="sxs-lookup"><span data-stu-id="730cc-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="730cc-106">I passaggi di base sono:</span><span class="sxs-lookup"><span data-stu-id="730cc-106">The basic steps are:</span></span>

1. <span data-ttu-id="730cc-107">Creare un modello come file JSON che descrive come creare l'avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="730cc-107">Create a template as a JSON file that describes how to create the activity log alert.</span></span>

2. <span data-ttu-id="730cc-108">[Distribuire il modello con un metodo di distribuzione qualsiasi](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="730cc-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="730cc-109">Modello di Resource Manager per un avviso del log attività</span><span class="sxs-lookup"><span data-stu-id="730cc-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="730cc-110">Per creare un avviso del log attività usando un modello di Resource Manager, creare una risorsa di tipo `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="730cc-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="730cc-111">Compilare quindi tutte le proprietà correlate.</span><span class="sxs-lookup"><span data-stu-id="730cc-111">Then you fill in all related properties.</span></span> <span data-ttu-id="730cc-112">Il modello seguente crea un avviso del log attività.</span><span class="sxs-lookup"><span data-stu-id="730cc-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
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

<span data-ttu-id="730cc-113">Per alcuni esempi di modelli di avvisi del log attività, visitare la [raccolta di modelli di avvio rapido](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights).</span><span class="sxs-lookup"><span data-stu-id="730cc-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="730cc-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="730cc-114">Next steps</span></span>
- <span data-ttu-id="730cc-115">[Altre informazioni sugli avvisi](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="730cc-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="730cc-116">Informazioni su come aggiungere [gruppi di azione usando un modello di Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="730cc-116">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="730cc-117">Informazioni su come [creare un avviso del log attività per monitorare tutte le operazioni del motore di scalabilità automatica della sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="730cc-117">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="730cc-118">Informazioni su come [creare un avviso di log attività per monitorare tutte le operazioni di scalabilità automatica in riduzione e in aumento non riuscite per la sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="730cc-118">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
