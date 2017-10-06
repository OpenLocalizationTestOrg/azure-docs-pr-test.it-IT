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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="51793-103">Aggiungere la rete virtuale di riferimento tooan esistente in un modello di set di scalabilità di Azure</span><span class="sxs-lookup"><span data-stu-id="51793-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="51793-104">Questo articolo viene illustrato come hello toomodify [scala valida minima Imposta modello](./virtual-machine-scale-sets-mvss-start.md) toodeploy in una rete virtuale esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="51793-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="51793-105">Modificare la definizione di modello hello</span><span class="sxs-lookup"><span data-stu-id="51793-105">Change hello template definition</span></span>

<span data-ttu-id="51793-106">Può essere visualizzato il modello di set di scala valida minima [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e il modello per la distribuzione di scala hello impostato in una rete virtuale esistente può essere visto [qui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="51793-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="51793-107">Questo modello si esamineranno hello diff utilizzato toocreate (`git diff minimum-viable-scale-set existing-vnet`), elemento per elemento:</span><span class="sxs-lookup"><span data-stu-id="51793-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="51793-108">Prima di tutto si aggiunge un parametro `subnetId`.</span><span class="sxs-lookup"><span data-stu-id="51793-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="51793-109">Verrà passata hello la configurazione di set di scalabilità, consentendo di set di scalabilità di hello subnet creato in precedenza di hello tooidentify toodeploy le macchine virtuali in questa stringa.</span><span class="sxs-lookup"><span data-stu-id="51793-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="51793-110">Questa stringa deve essere formato hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="51793-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="51793-111">Ad esempio, di set di scalabilità di hello toodeploy in una rete virtuale esistente con nome `myvnet`, subnet `mysubnet`, gruppo di risorse `myrg`, sottoscrizione e `00000000-0000-0000-0000-000000000000`, sarebbe struttura hello: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="51793-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

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

<span data-ttu-id="51793-112">Successivamente, è possibile eliminare la risorsa di rete virtuale hello da hello `resources` matrice, poiché si utilizza una rete virtuale esistente e non è necessario toodeploy uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="51793-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

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

<span data-ttu-id="51793-113">esiste già la rete virtuale Hello prima di distribuita il modello di hello, pertanto non c'è alcuna necessità toospecify una clausola di dependsOn dalla scala hello imposta toohello di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="51793-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="51793-114">Vengono quindi eliminate le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="51793-114">Thus, we delete these lines:</span></span>

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

<span data-ttu-id="51793-115">Infine, viene passata in hello `subnetId` parametro impostato dall'utente hello (anziché `resourceId` id hello tooget di una rete virtuale nella stessa distribuzione, ovvero quali scala valida minima hello Imposta modello hello).</span><span class="sxs-lookup"><span data-stu-id="51793-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="51793-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51793-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
