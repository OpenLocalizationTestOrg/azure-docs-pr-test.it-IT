---
title: "Fare riferimento a una rete virtuale esistente in un modello di set di scalabilità di Azure | Microsoft Docs"
description: "Informazioni su come tooadd un virtuale rete tooan modello di Set di scalabilità macchina virtuale di Azure esistente"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Aggiungere la rete virtuale di riferimento tooan esistente in un modello di set di scalabilità di Azure

Questo articolo viene illustrato come hello toomodify [scala valida minima Imposta modello](./virtual-machine-scale-sets-mvss-start.md) toodeploy in una rete virtuale esistente anziché crearne uno nuovo.

## <a name="change-hello-template-definition"></a>Modificare la definizione di modello hello

Può essere visualizzato il modello di set di scala valida minima [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e il modello per la distribuzione di scala hello impostato in una rete virtuale esistente può essere visto [qui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Questo modello si esamineranno hello diff utilizzato toocreate (`git diff minimum-viable-scale-set existing-vnet`), elemento per elemento:

Prima di tutto si aggiunge un parametro `subnetId`. Verrà passata hello la configurazione di set di scalabilità, consentendo di set di scalabilità di hello subnet creato in precedenza di hello tooidentify toodeploy le macchine virtuali in questa stringa. Questa stringa deve essere formato hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Ad esempio, di set di scalabilità di hello toodeploy in una rete virtuale esistente con nome `myvnet`, subnet `mysubnet`, gruppo di risorse `myrg`, sottoscrizione e `00000000-0000-0000-0000-000000000000`, sarebbe struttura hello: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

Successivamente, è possibile eliminare la risorsa di rete virtuale hello da hello `resources` matrice, poiché si utilizza una rete virtuale esistente e non è necessario toodeploy uno nuovo.

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

esiste già la rete virtuale Hello prima di distribuita il modello di hello, pertanto non c'è alcuna necessità toospecify una clausola di dependsOn dalla scala hello imposta toohello di rete virtuale. Vengono quindi eliminate le righe seguenti:

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

Infine, viene passata in hello `subnetId` parametro impostato dall'utente hello (anziché `resourceId` id hello tooget di una rete virtuale nella stessa distribuzione, ovvero quali scala valida minima hello Imposta modello hello).

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
