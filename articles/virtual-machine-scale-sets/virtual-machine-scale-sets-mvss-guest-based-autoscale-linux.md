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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="b8de6-103">Eseguire la scalabilità automatica usando metriche guest in un modello di set di scalabilità Linux</span><span class="sxs-lookup"><span data-stu-id="b8de6-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="b8de6-104">Esistono due tipi di metriche in Azure che vengono raccolti da macchine virtuali e i set di scalabilità: alcuni provengono da hello host macchina virtuale e altri utenti provengono da macchina virtuale guest hello.</span><span class="sxs-lookup"><span data-stu-id="b8de6-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="b8de6-105">Le metriche di host non richiedono configurazione aggiuntiva poiché vengono raccolti dall'host hello macchina virtuale, mentre le metriche guest richiedono la tooinstall hello [estensione di diagnostica Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) o hello [diagnostica Azure per Linux estensione](../virtual-machines/linux/diagnostic-extension.md) in hello VM guest.</span><span class="sxs-lookup"><span data-stu-id="b8de6-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="b8de6-106">Un motivo toouse guest metriche di uso comune anziché le metriche di host sono che le metriche guest forniscano una selezione più ampia di metriche di metriche di host.</span><span class="sxs-lookup"><span data-stu-id="b8de6-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="b8de6-107">Le metriche relative al consumo di memoria, disponibili solo tramite metriche guest, ne sono un esempio.</span><span class="sxs-lookup"><span data-stu-id="b8de6-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="b8de6-108">sono elencate le metriche di host supportato Hello [qui](../monitoring-and-diagnostics/monitoring-supported-metrics.md), e sono elencate le metriche usate comunemente guest [qui](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b8de6-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="b8de6-109">Questo articolo viene illustrato come hello toomodify [scala valida minima Imposta modello](./virtual-machine-scale-sets-mvss-start.md) toouse le regole di scalabilità automatica in base alle metriche di guest per il set di scalabilità di Linux.</span><span class="sxs-lookup"><span data-stu-id="b8de6-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="b8de6-110">Modificare la definizione di modello hello</span><span class="sxs-lookup"><span data-stu-id="b8de6-110">Change hello template definition</span></span>

<span data-ttu-id="b8de6-111">Può essere visualizzato il modello di set di scala valida minima [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e può essere visualizzato il modello per la distribuzione di hello Linux set di scalabilità con scalabilità automatica basata su guest [qui](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b8de6-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="b8de6-112">Questo modello si esamineranno hello diff utilizzato toocreate (`git diff minimum-viable-scale-set existing-vnet`), elemento per elemento:</span><span class="sxs-lookup"><span data-stu-id="b8de6-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="b8de6-113">Per prima cosa, si aggiungono i parametri per `storageAccountName` e `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="b8de6-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="b8de6-114">agente di diagnostica Hello archivierà i dati di metrica in un [tabella](../cosmos-db/table-storage-how-to-use-dotnet.md) in questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b8de6-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="b8de6-115">A partire da hello agente Linux di diagnostica versione 3.0, utilizzando una chiave di accesso di archiviazione non è più supportata.</span><span class="sxs-lookup"><span data-stu-id="b8de6-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="b8de6-116">È necessario usare invece un [token di firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="b8de6-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="b8de6-117">Successivamente, è possibile modificare il set di scalabilità di hello `extensionProfile` estensione di diagnostica tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="b8de6-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="b8de6-118">In questa configurazione è specificare risorsa hello toocollect metriche di impostare l'ID della scala hello, nonché hello account di archiviazione e metriche hello toostore toouse token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="b8de6-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="b8de6-119">È anche di specificare la frequenza con cui vengono aggregate metriche hello (in questo caso ogni minuto) e quali tootrack metriche (in questo caso memoria utilizzata percentuale).</span><span class="sxs-lookup"><span data-stu-id="b8de6-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="b8de6-120">Per informazioni più dettagliate su questa configurazione e sulle metriche diverse dalla percentuale di memoria usata, vedere [questa documentazione](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b8de6-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="b8de6-121">Infine, viene aggiunto un `autoscaleSettings` scalabilità automatica tooconfigure risorse in base a queste metriche.</span><span class="sxs-lookup"><span data-stu-id="b8de6-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="b8de6-122">Questa risorsa è un `dependsOn` clausola che fa riferimento a scala hello impostata tooensure set di scalabilità hello esistente prima di tentare di tooautoscale è.</span><span class="sxs-lookup"><span data-stu-id="b8de6-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="b8de6-123">Se si sceglie un tooautoscale metrica diverse, si utilizzerebbe hello `counterSpecifier` dalla configurazione dell'estensione diagnostica hello come hello `metricName` nella configurazione della scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="b8de6-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="b8de6-124">Per ulteriori informazioni sulla configurazione della scalabilità automatica, vedere hello [le procedure consigliate di scalabilità automatica](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) hello e [la documentazione di riferimento API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8de6-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="b8de6-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8de6-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
