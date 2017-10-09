---
title: "Usare la scalabilità automatica di Azure con metriche guest in un modello di set di scalabilità Linux | Microsoft Docs"
description: "Informazioni su come tooautoscale uso delle metriche del guest in un modello di Set di scalabilità della macchina virtuale Linux"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Eseguire la scalabilità automatica usando metriche guest in un modello di set di scalabilità Linux

Esistono due tipi di metriche in Azure che vengono raccolti da macchine virtuali e i set di scalabilità: alcuni provengono da hello host macchina virtuale e altri utenti provengono da macchina virtuale guest hello. Le metriche di host non richiedono configurazione aggiuntiva poiché vengono raccolti dall'host hello macchina virtuale, mentre le metriche guest richiedono la tooinstall hello [estensione di diagnostica Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) o hello [diagnostica Azure per Linux estensione](../virtual-machines/linux/diagnostic-extension.md) in hello VM guest. Un motivo toouse guest metriche di uso comune anziché le metriche di host sono che le metriche guest forniscano una selezione più ampia di metriche di metriche di host. Le metriche relative al consumo di memoria, disponibili solo tramite metriche guest, ne sono un esempio. sono elencate le metriche di host supportato Hello [qui](../monitoring-and-diagnostics/monitoring-supported-metrics.md), e sono elencate le metriche usate comunemente guest [qui](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). Questo articolo viene illustrato come hello toomodify [scala valida minima Imposta modello](./virtual-machine-scale-sets-mvss-start.md) toouse le regole di scalabilità automatica in base alle metriche di guest per il set di scalabilità di Linux.

## <a name="change-hello-template-definition"></a>Modificare la definizione di modello hello

Può essere visualizzato il modello di set di scala valida minima [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e può essere visualizzato il modello per la distribuzione di hello Linux set di scalabilità con scalabilità automatica basata su guest [qui](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Questo modello si esamineranno hello diff utilizzato toocreate (`git diff minimum-viable-scale-set existing-vnet`), elemento per elemento:

Per prima cosa, si aggiungono i parametri per `storageAccountName` e `storageAccountSasToken`. agente di diagnostica Hello archivierà i dati di metrica in un [tabella](../cosmos-db/table-storage-how-to-use-dotnet.md) in questo account di archiviazione. A partire da hello agente Linux di diagnostica versione 3.0, utilizzando una chiave di accesso di archiviazione non è più supportata. È necessario usare invece un [token di firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

Successivamente, è possibile modificare il set di scalabilità di hello `extensionProfile` estensione di diagnostica tooinclude hello. In questa configurazione è specificare risorsa hello toocollect metriche di impostare l'ID della scala hello, nonché hello account di archiviazione e metriche hello toostore toouse token di firma di accesso condiviso. È anche di specificare la frequenza con cui vengono aggregate metriche hello (in questo caso ogni minuto) e quali tootrack metriche (in questo caso memoria utilizzata percentuale). Per informazioni più dettagliate su questa configurazione e sulle metriche diverse dalla percentuale di memoria usata, vedere [questa documentazione](../virtual-machines/linux/diagnostic-extension.md).

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

Infine, viene aggiunto un `autoscaleSettings` scalabilità automatica tooconfigure risorse in base a queste metriche. Questa risorsa è un `dependsOn` clausola che fa riferimento a scala hello impostata tooensure set di scalabilità hello esistente prima di tentare di tooautoscale è. Se si sceglie un tooautoscale metrica diverse, si utilizzerebbe hello `counterSpecifier` dalla configurazione dell'estensione diagnostica hello come hello `metricName` nella configurazione della scalabilità automatica hello. Per ulteriori informazioni sulla configurazione della scalabilità automatica, vedere hello [le procedure consigliate di scalabilità automatica](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) hello e [la documentazione di riferimento API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931928.aspx).

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
