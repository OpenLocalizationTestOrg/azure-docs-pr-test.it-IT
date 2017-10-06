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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Creare un avviso di log attività con un modello di Resource Manager
In questo articolo illustra come toouse un [modello di Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure gli avvisi del registro attività. Tramite i modelli è possibile configurare facilmente numerosi avvisi che vengono attivati in base a condizioni specifiche degli eventi del log attività nell'ambito del processo di distribuzione automatica.

passaggi di base di Hello sono:

1. Creare un modello come un file JSON che descrive la modalità attività hello toocreate log avviso.

2. Distribuire il modello di hello utilizzando [qualsiasi metodo di distribuzione](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Modello di Resource Manager per un avviso del log attività
toocreate un avviso di log attività utilizzando un modello di gestione delle risorse, si crea una risorsa di tipo hello `microsoft.insights/activityLogAlerts`. Compilare quindi tutte le proprietà correlate. Il modello seguente crea un avviso del log attività.

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

Per alcuni esempi di modelli di avvisi del log attività, visitare la [raccolta di modelli di avvio rapido](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights).

## <a name="next-steps"></a>Passaggi successivi
- [Altre informazioni sugli avvisi](monitoring-overview-alerts.md).
- Informazioni su come tooadd [gruppi di azioni utilizzando un modello di gestione risorse](monitoring-create-action-group-with-resource-manager-template.md).
- Informazioni su come troppo[creare tutte le operazioni del motore di scalabilità automatica per la sottoscrizione di un log di attività avviso toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Informazioni su come troppo[creare tutte le operazioni di scala/scalabilità di scalabilità automatica non riuscita per la sottoscrizione di un log di attività avviso toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
