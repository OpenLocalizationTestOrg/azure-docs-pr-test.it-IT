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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Abilitare automaticamente le impostazioni di diagnostica durante la creazione di risorse con un modello di Resource Manager
In questo articolo è illustrata la modalità è possibile utilizzare un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure le impostazioni di diagnostica su una risorsa quando viene creato. In questo modo inizio tooautomatically streaming il tooEvent i log di diagnostica e le metriche di hub di archiviazione delle immagini in un Account di archiviazione o inviarli tooLog Analitica quando viene creata una risorsa.

metodo Hello per abilitare i log di diagnostica utilizzando un modello di gestione risorse dipende dal tipo di risorsa hello.

* **risorse non di calcolo** , ad esempio Gruppi di sicurezza di rete, App per la logica e Automazione, usare le [impostazioni di diagnostica descritte in questo articolo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Calcolo** (WAD/LAD-) le risorse basate su utilizzano hello [file di configurazione di WAD/LAD descritto in questo articolo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

In questo articolo viene descritto come tooconfigure diagnostica usando dei metodi.

come indicato di seguito sono riportati i passaggi di base Hello:

1. Creare un modello come un file JSON che descrive la modalità toocreate hello risorse e abilitare la diagnostica.
2. [Distribuire il modello di hello utilizzando qualsiasi metodo di distribuzione](../azure-resource-manager/resource-group-template-deploy.md).

Fornita di seguito è riportato un esempio di modello hello file JSON, è necessario toogenerate per non di calcolo e le risorse di calcolo.

## <a name="non-compute-resource-template"></a>Modello per risorse non di calcolo
Per le risorse non di calcolo, è necessario toodo due operazioni:

1. Aggiungere blob parametri toohello di parametri per il nome di account di archiviazione hello, ID regola bus di servizio e/o ID area di lavoro OMS Log Analitica (abilitazione dell'archivio di log di diagnostica in un account di archiviazione, il flusso di log tooEvent hub e/o l'invio di log tooLog Analitica).
   
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
2. Nella matrice di risorse hello della risorsa hello per cui si desidera tooenable i log di diagnostica, aggiungere una risorsa di tipo `[resource namespace]/providers/diagnosticSettings`.
   
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

segue Hello blob di proprietà per l'impostazione diagnostica hello [formato hello descritto in questo articolo](https://msdn.microsoft.com/library/azure/dn931931.aspx). Aggiunta di hello `metrics` proprietà consentirà toothese metriche di tooalso trasmissione risorse stesso genera, a condizione che [risorse hello supporta le metriche di monitoraggio di Azure](monitoring-supported-metrics.md).

Di seguito è riportato un esempio completo che crea un'App di logica e attiva il flusso tooEvent hub e archiviazione in un account di archiviazione.

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

## <a name="compute-resource-template"></a>Modello per risorse di calcolo
diagnostica tooenable su una risorsa di calcolo, ad esempio una macchina virtuale o il cluster di Service Fabric, è necessario:

1. Aggiungere la definizione di risorsa VM hello diagnostica Azure estensione toohello.
2. Specificare un account di archiviazione e/o un hub eventi come parametro.
3. Aggiungere contenuto hello del file XML WADCfg nella proprietà XMLCfg hello, caratteri di escape correttamente tutti i caratteri XML.

> [!WARNING]
> Quest'ultimo passaggio può essere difficile tooget destra. [Vedere l'articolo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) per un esempio che divisioni hello dello Schema di configurazione di diagnostica in variabili che vengono sottoposti a escape e formattate correttamente.
> 
> 

Hello intera, compresi gli esempi, descritto più avanti [in questo documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sui log di diagnostica di Azure](monitoring-overview-of-diagnostic-logs.md)
* [Flusso i log di diagnostica Azure tooEvent hub](monitoring-stream-diagnostic-logs-to-event-hubs.md)

