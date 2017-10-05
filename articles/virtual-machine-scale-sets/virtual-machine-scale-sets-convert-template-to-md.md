---
title: "Convertire un modello di set di scalabilità di Azure Resource Manager per usare i dischi gestiti | Documentazione Microsoft"
description: "Convertire un modello di set di scalabilità in un modello di set di scalabilità per i dischi gestiti."
keywords: "set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="3dbac-104">Convertire un modello di set di scalabilità in un modello di set di scalabilità per i dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="3dbac-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="3dbac-105">I clienti con un modello di Resource Manager per la creazione di un set di scalabilità che non usa i dischi gestiti potrebbero volerlo modificare per usare i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="3dbac-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="3dbac-106">Questo articolo illustra come procedere, usando come esempio una richiesta pull dai [modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates), un repository gestito dalla community di modelli di Resource Manager di esempio.</span><span class="sxs-lookup"><span data-stu-id="3dbac-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="3dbac-107">La richiesta pull completa è disponibile all'indirizzo [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998). Le parti pertinenti del diff sono sotto, con le spiegazioni:</span><span class="sxs-lookup"><span data-stu-id="3dbac-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="3dbac-108">Impostazione dei dischi del sistema operativo come gestiti</span><span class="sxs-lookup"><span data-stu-id="3dbac-108">Making the OS disks managed</span></span>

<span data-ttu-id="3dbac-109">Nel diff seguente è possibile osservare che sono state rimosse diverse variabili correlate all'account di archiviazione e alle proprietà dei dischi.</span><span class="sxs-lookup"><span data-stu-id="3dbac-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="3dbac-110">Il tipo di account di archiviazione non è più necessario (Standard_LRS è il valore predefinito), ma è ugualmente possibile specificarlo, se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="3dbac-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="3dbac-111">Con il disco gestito sono supportati solo Standard_LRS e Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="3dbac-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="3dbac-112">Nel modello precedente, per generare i nomi degli account di archiviazione, vengono usati un nuovo suffisso dell'account di archiviazione, una matrice di stringhe univoca e il conteggio degli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3dbac-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="3dbac-113">Queste variabili non sono più necessarie nel nuovo modello perché il disco gestito crea automaticamente gli account di archiviazione per conto del cliente.</span><span class="sxs-lookup"><span data-stu-id="3dbac-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="3dbac-114">Allo stesso modo, non sono più necessari il nome contenitore del disco rigido virtuale e il nome del disco del sistema operativo perché il disco gestito denomina automaticamente i dischi e i contenitori BLOB di archiviazione sottostanti.</span><span class="sxs-lookup"><span data-stu-id="3dbac-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


<span data-ttu-id="3dbac-115">Nel diff seguente è possibile osservare che la versione dell'API di calcolo è stata aggiornata a 2016-04-30-preview, che è la versione necessaria più recente per il supporto per il disco gestito con i set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="3dbac-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="3dbac-116">Si noti che è ancora possibile usare dischi non gestiti nella nuova versione dell'API con la sintassi precedente, se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="3dbac-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="3dbac-117">In altre parole, se si aggiorna solo la versione dell'API di calcolo e non si modifica nient'altro, il modello continuerà a funzionare come prima.</span><span class="sxs-lookup"><span data-stu-id="3dbac-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

<span data-ttu-id="3dbac-118">Nel diff seguente si può osservare che la risorsa dell'account di archiviazione viene completamente rimossa dalla matrice di risorse.</span><span class="sxs-lookup"><span data-stu-id="3dbac-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="3dbac-119">Non è più necessaria perché il disco gestito la crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3dbac-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

<span data-ttu-id="3dbac-120">Nel diff seguente è possibile osservare che viene rimossa la clausola depends on che crea un riferimento dal set di scalabilità al ciclo che crea gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3dbac-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="3dbac-121">Nel modello precedente ciò assicura che gli account di archiviazione vengano creati prima che il set di scalabilità inizi la creazione, ma questa clausola non è più necessaria con i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="3dbac-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="3dbac-122">Vengono rimosse anche la proprietà dei contenitori dei dischi rigidi virtuali e la proprietà del nome del disco del sistema operativo perché queste proprietà vengono gestite automaticamente in background dal disco gestito.</span><span class="sxs-lookup"><span data-stu-id="3dbac-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="3dbac-123">Se necessario, è possibile aggiungere `"managedDisk": { "storageAccountType": "Premium_LRS" }` nella configurazione di "osDisk" se si preferiscono dischi di sistema operativo Premium.</span><span class="sxs-lookup"><span data-stu-id="3dbac-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="3dbac-124">Solo le VM con una "s" maiuscola o minuscola nell'unità SKU possono usare dischi Premium.</span><span class="sxs-lookup"><span data-stu-id="3dbac-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

<span data-ttu-id="3dbac-125">Non esistono proprietà esplicite nella configurazione del set di scalabilità che indichino se usare dischi gestiti o non gestiti.</span><span class="sxs-lookup"><span data-stu-id="3dbac-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="3dbac-126">Il set di scalabilità determina quale usare in base alle proprietà presenti nel profilo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3dbac-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="3dbac-127">È quindi importante, quando si modifica il modello, assicurarsi che nel profilo di archiviazione del set di scalabilità siano presenti le proprietà corrette.</span><span class="sxs-lookup"><span data-stu-id="3dbac-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="3dbac-128">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="3dbac-128">Data disks</span></span>

<span data-ttu-id="3dbac-129">Con le modifiche precedenti, il set di scalabilità usa dischi gestiti per il disco del sistema operativo. Non si è però parlato dei dischi dati.</span><span class="sxs-lookup"><span data-stu-id="3dbac-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="3dbac-130">Per aggiungere dischi dati, aggiungere la proprietà "dataDisks" in "storageProfile" allo stesso livello di "osDisk".</span><span class="sxs-lookup"><span data-stu-id="3dbac-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="3dbac-131">Il valore della proprietà è un elenco JSON di oggetti, ognuno dei quali ha proprietà "lun" (che devono essere univoche per ogni disco dati in una VM), "createOption" ("empty" è attualmente la sola opzione supportata) e "diskSizeGB" (le dimensioni del disco in gigabyte, che devono essere maggiori di 0 e minori di 1024), come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3dbac-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="3dbac-132">Se si specificano `n` dischi in questa matrice, ogni VM nel set di scalabilità ottiene `n` dischi dati.</span><span class="sxs-lookup"><span data-stu-id="3dbac-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="3dbac-133">Si noti tuttavia che questi dischi dati sono dispositivi RAW.</span><span class="sxs-lookup"><span data-stu-id="3dbac-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="3dbac-134">Non sono formattati.</span><span class="sxs-lookup"><span data-stu-id="3dbac-134">They are not formatted.</span></span> <span data-ttu-id="3dbac-135">È responsabilità del cliente collegare, partizionare e formattare i dischi prima di usarli.</span><span class="sxs-lookup"><span data-stu-id="3dbac-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="3dbac-136">Volendo, è possibile specificare `"managedDisk": { "storageAccountType": "Premium_LRS" }` in ogni oggetto disco dati per specificare che deve essere un disco dati Premium.</span><span class="sxs-lookup"><span data-stu-id="3dbac-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="3dbac-137">Solo le VM con una "s" maiuscola o minuscola nell'unità SKU possono usare dischi Premium.</span><span class="sxs-lookup"><span data-stu-id="3dbac-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="3dbac-138">Per altre informazioni sull'uso dei dischi dati con i set di scalabilità, vedere [questo articolo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="3dbac-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="3dbac-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3dbac-139">Next steps</span></span>
<span data-ttu-id="3dbac-140">Ad esempio, per i modelli di Resource Manager con set di scalabilità, cercare "vmss" nel [repository di GitHub dei modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="3dbac-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="3dbac-141">Per informazioni generali, vedere la [pagina di destinazione principale per i set di scalabilità](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="3dbac-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

