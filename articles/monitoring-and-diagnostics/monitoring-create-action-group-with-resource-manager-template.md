---
title: gruppi di azioni aaaCreate con modelli di gestione risorse | Documenti Microsoft
description: Informazioni su come un'azione toocreate gruppo utilizzando un modello di gestione risorse di Azure.
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="5f65c-103">Creare un gruppo di azione con un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f65c-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="5f65c-104">In questo articolo illustra come toouse un [modello di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure gruppi di azioni.</span><span class="sxs-lookup"><span data-stu-id="5f65c-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="5f65c-105">Tramite i modelli è possibile configurare automaticamente i gruppi di azione che possono essere riusati in determinati tipi di avvisi.</span><span class="sxs-lookup"><span data-stu-id="5f65c-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="5f65c-106">Questi gruppi di azioni di verificare che tutti hello corretto parti vengono informate quando viene attivato un avviso.</span><span class="sxs-lookup"><span data-stu-id="5f65c-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="5f65c-107">passaggi di base di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="5f65c-107">hello basic steps are:</span></span>

1. <span data-ttu-id="5f65c-108">Creare un modello come un file JSON che descrive la modalità toocreate hello gruppo di azioni.</span><span class="sxs-lookup"><span data-stu-id="5f65c-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="5f65c-109">Distribuire il modello di hello utilizzando [qualsiasi metodo di distribuzione](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="5f65c-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="5f65c-110">Innanzitutto, viene descritto come un modello di gestione risorse per un'azione toocreate gruppo in cui le definizioni di azioni hello sono hardcoded nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="5f65c-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="5f65c-111">In secondo luogo, viene descritto come toocreate un modello che accetta informazioni di configurazione webhook hello come parametri di input quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="5f65c-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="5f65c-112">Modelli di Resource Manager per un gruppo di azione</span><span class="sxs-lookup"><span data-stu-id="5f65c-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="5f65c-113">toocreate utilizzando un modello di gestione risorse di un gruppo di azioni, si crea una risorsa di tipo hello `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="5f65c-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="5f65c-114">Compilare quindi tutte le proprietà correlate.</span><span class="sxs-lookup"><span data-stu-id="5f65c-114">Then you fill in all related properties.</span></span> <span data-ttu-id="5f65c-115">Ecco due modelli di esempio che creano un gruppo di azione.</span><span class="sxs-lookup"><span data-stu-id="5f65c-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a><span data-ttu-id="5f65c-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f65c-116">Next steps</span></span>
* <span data-ttu-id="5f65c-117">Altre informazioni sui [gruppi di azione](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="5f65c-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="5f65c-118">[Altre informazioni sugli avvisi](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5f65c-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="5f65c-119">Informazioni su come tooadd [gli avvisi tramite un modello di gestione risorse](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="5f65c-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
