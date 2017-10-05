---
title: "Fare riferimento a una rete virtuale esistente in un modello di set di scalabilità di Azure | Microsoft Docs"
description: "Informazioni su come aggiungere una rete virtuale in un modello di set di scalabilità di macchine virtuali di Azure esistente"
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
ms.openlocfilehash: 28117d467b491704aed8d45e5eba42530579dfa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-reference-to-an-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="47751-103">Aggiungere un riferimento a una rete virtuale esistente in un modello di set di scalabilità di Azure</span><span class="sxs-lookup"><span data-stu-id="47751-103">Add reference to an existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="47751-104">Questo articolo illustra come modificare il [modello di set di scalabilità minimo valido](./virtual-machine-scale-sets-mvss-start.md) per eseguire la distribuzione in una rete virtuale esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="47751-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="47751-105">Modificare la definizione del modello</span><span class="sxs-lookup"><span data-stu-id="47751-105">Change the template definition</span></span>

<span data-ttu-id="47751-106">Il modello di set di scalabilità minimo valido è disponibile [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), mentre il modello per la distribuzione del set di scalabilità in una rete virtuale esistente è disponibile [qui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="47751-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="47751-107">Viene ora esaminato il diff usato per creare questo modello, `git diff minimum-viable-scale-set existing-vnet`, passo per passo:</span><span class="sxs-lookup"><span data-stu-id="47751-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="47751-108">Prima di tutto si aggiunge un parametro `subnetId`.</span><span class="sxs-lookup"><span data-stu-id="47751-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="47751-109">Questa stringa viene passata nella configurazione del set di scalabilità e permette di identificare la subnet, creata in precedenza, in cui distribuire le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="47751-109">This string will be passed into the scale set configuration, allowing the scale set to identify the pre-created subnet to deploy virtual machines into.</span></span> <span data-ttu-id="47751-110">La stringa deve essere nel formato seguente: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="47751-110">This string must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="47751-111">Ad esempio, per distribuire il set di scalabilità in una rete virtuale esistente denominata `myvnet`, subnet `mysubnet`, gruppo di risorse `myrg` e sottoscrizione`00000000-0000-0000-0000-000000000000`, l'ID subnet sarebbe il seguente: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="47751-111">For instance, to deploy the scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, the subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

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

<span data-ttu-id="47751-112">Dal momento che si usa una rete virtuale esistente e non è necessario distribuirne una nuova, è possibile eliminare la risorsa rete virtuale dalla matrice `resources`.</span><span class="sxs-lookup"><span data-stu-id="47751-112">Next, we can delete the virtual network resource from the `resources` array, since we are using an existing virtual network and don't need to deploy a new one.</span></span>

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

<span data-ttu-id="47751-113">La rete virtuale esiste già prima della distribuzione del modello, non è quindi necessario specificare una clausola dependsOn dal set di scalabilità alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="47751-113">The virtual network already exists before the template is deployed, so there is no need to specify a dependsOn clause from the scale set to the virtual network.</span></span> <span data-ttu-id="47751-114">Vengono quindi eliminate le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="47751-114">Thus, we delete these lines:</span></span>

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

<span data-ttu-id="47751-115">Infine, si passa il parametro `subnetId` impostato dall'utente, anziché usare `resourceId` per ottenere l'ID di una rete virtuale nella stessa distribuzione, perché questa operazione viene eseguita dal modello di set di scalabilità minimo valido.</span><span class="sxs-lookup"><span data-stu-id="47751-115">Finally, we pass in the `subnetId` parameter set by the user (instead of using `resourceId` to get the id of a vnet in the same deployment, which is what the minimum viable scale set template does).</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="47751-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47751-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
