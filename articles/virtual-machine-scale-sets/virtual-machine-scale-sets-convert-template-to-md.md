---
title: una scala di Azure Resource Manager aaaConvert impostare modello toouse gestito disco | Documenti Microsoft
description: "Convertire un modello di set di scalabilità set modello tooa disco gestito scala."
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
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="b98d3-104">Convertire un modello di set di scalabilità set modello tooa disco gestito scala</span><span class="sxs-lookup"><span data-stu-id="b98d3-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="b98d3-105">I clienti con un modello di gestione risorse per la creazione di un set non utilizza disco gestito di scalabilità può essere utile toomodify è toouse gestiti disco.</span><span class="sxs-lookup"><span data-stu-id="b98d3-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="b98d3-106">Questo articolo viene illustrato come toodo questo, utilizzando ad esempio una richiesta di pull da hello [modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates), un repository basato sulla community per i modelli di gestione risorse di esempio.</span><span class="sxs-lookup"><span data-stu-id="b98d3-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="b98d3-107">richiesta di pull completo Hello sono consultabili qui: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), e parti inerenti hello hello diff sono di sotto, insieme a una spiegazione:</span><span class="sxs-lookup"><span data-stu-id="b98d3-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="b98d3-108">Rendere i dischi del sistema operativo hello gestiti</span><span class="sxs-lookup"><span data-stu-id="b98d3-108">Making hello OS disks managed</span></span>

<span data-ttu-id="b98d3-109">Nel diff hello riportato di seguito, si noterà che è stata rimossa diverse variabili correlate toostorage account e disco proprietà.</span><span class="sxs-lookup"><span data-stu-id="b98d3-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="b98d3-110">Tipo di account di archiviazione non è più necessario (Standard_LRS è predefinito hello), ma è possibile specificare comunque Se si desidera.</span><span class="sxs-lookup"><span data-stu-id="b98d3-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="b98d3-111">Con il disco gestito sono supportati solo Standard_LRS e Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="b98d3-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="b98d3-112">Nuovo suffisso di account di archiviazione, matrice di stringhe univoche e il numero di sa utilizzati nei nomi di archiviazione hello vecchio modello toogenerate account.</span><span class="sxs-lookup"><span data-stu-id="b98d3-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="b98d3-113">Queste variabili non sono più necessari nel nuovo modello di hello perché disco gestito crea automaticamente gli account di archiviazione per conto del cliente hello.</span><span class="sxs-lookup"><span data-stu-id="b98d3-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="b98d3-114">Analogamente, il nome di contenitore vhd e il nome del disco del sistema operativo non sono più necessarie poiché disco gestito nomi automaticamente i dischi e i contenitori blob di archiviazione sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="b98d3-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="b98d3-115">In hello diff seguito, è possibile vedere che abbiamo aggiornato hello calcolare versione too2016-04-30-l'anteprima dell'api, ovvero hello versione meno recente necessario per il supporto di dischi gestiti con set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b98d3-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="b98d3-116">Si noti che è possibile usare ancora i dischi non gestiti in hello nuova versione dell'api con sintassi precedente hello se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="b98d3-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="b98d3-117">In altre parole, se si aggiorna solo hello versione dell'api di calcolo e di non modificare nemmeno altri elementi, il modello di hello deve continuare toowork come prima.</span><span class="sxs-lookup"><span data-stu-id="b98d3-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

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

<span data-ttu-id="b98d3-118">Nel diff hello riportato di seguito, si noterà che viene rimossa risorsa account di archiviazione hello dalla matrice di risorse hello completamente.</span><span class="sxs-lookup"><span data-stu-id="b98d3-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="b98d3-119">Non è più necessaria perché il disco gestito la crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b98d3-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="b98d3-120">In hello diff seguito, è possibile vedere che viene rimossa hello dipende clausola che fa riferimento la ciclo hello scala set toohello che la creazione di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b98d3-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="b98d3-121">Nel modello precedente hello, questo è stato verificato che siano stati creati gli account di archiviazione hello prima che il set di scalabilità di hello è iniziata la creazione, ma questa clausola non è più necessaria con disco gestito.</span><span class="sxs-lookup"><span data-stu-id="b98d3-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="b98d3-122">È inoltre rimuovere proprietà di contenitori vhd hello e hello proprietà del nome del disco del sistema operativo come queste proprietà vengono gestite automaticamente quinte hello dal disco gestito.</span><span class="sxs-lookup"><span data-stu-id="b98d3-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="b98d3-123">Se si intende, è possibile aggiungere `"managedDisk": { "storageAccountType": "Premium_LRS" }` nella configurazione di "osDisk" hello se si volevano i dischi del sistema operativo premium.</span><span class="sxs-lookup"><span data-stu-id="b98d3-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="b98d3-124">Solo le macchine virtuali con una maiuscola o del minuscola ' nella macchina virtuale hello sku è possibile utilizzare i dischi premium.</span><span class="sxs-lookup"><span data-stu-id="b98d3-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

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

<span data-ttu-id="b98d3-125">Non è nessuna proprietà esplicita nella configurazione di set di scalabilità di hello per se toouse gestito o un disco non gestito.</span><span class="sxs-lookup"><span data-stu-id="b98d3-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="b98d3-126">set di scalabilità Hello sa quale toouse in base alle proprietà hello presenti nel profilo di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="b98d3-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="b98d3-127">Di conseguenza, è importante quando si modifica tooensure modello hello che sono proprietà diritti hello nel profilo di archiviazione hello del set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="b98d3-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="b98d3-128">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="b98d3-128">Data disks</span></span>

<span data-ttu-id="b98d3-129">Con le modifiche hello sopra, hello scala set utilizza gestito per hello del sistema operativo dischi, ma sui dischi dati? i dischi dati tooadd, aggiungere della proprietà "dataDisks" hello "storageProfile" in hello stesso livello come "osDisk".</span><span class="sxs-lookup"><span data-stu-id="b98d3-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="b98d3-130">valore della proprietà hello Hello è un elenco JSON di oggetti, ognuno dei quali dispone di proprietà "lun" (che deve essere univoco per ogni disco dati in una macchina virtuale), "createOption" ("empty" è attualmente hello opzione supportata solo) e "diskSizeGB" (dimensioni del disco hello in gigabyte hello; deve essere maggiore di 0 e minore di 1024) come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b98d3-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="b98d3-131">Se si specifica `n` dischi in questa matrice, ogni macchina virtuale nella scala hello impostato Ottiene `n` dischi dati.</span><span class="sxs-lookup"><span data-stu-id="b98d3-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="b98d3-132">Si noti tuttavia che questi dischi dati sono dispositivi RAW.</span><span class="sxs-lookup"><span data-stu-id="b98d3-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="b98d3-133">Non sono formattati.</span><span class="sxs-lookup"><span data-stu-id="b98d3-133">They are not formatted.</span></span> <span data-ttu-id="b98d3-134">È di toohello cliente tooattach, Partition e dischi in formato hello prima di usarli.</span><span class="sxs-lookup"><span data-stu-id="b98d3-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="b98d3-135">Facoltativamente, è inoltre possibile specificare `"managedDisk": { "storageAccountType": "Premium_LRS" }` in ogni toospecify di oggetto disco dati che deve essere un disco dati premium.</span><span class="sxs-lookup"><span data-stu-id="b98d3-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="b98d3-136">Solo le macchine virtuali con una maiuscola o del minuscola ' nella macchina virtuale hello sku è possibile utilizzare i dischi premium.</span><span class="sxs-lookup"><span data-stu-id="b98d3-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="b98d3-137">toolearn ulteriori informazioni sull'utilizzo di dischi di dati con il set di scalabilità, vedere [questo articolo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="b98d3-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b98d3-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b98d3-138">Next steps</span></span>
<span data-ttu-id="b98d3-139">Ad esempio utilizzando set di scalabilità di modelli di gestione risorse di ricerca per "vmss" hello [repository github dei modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="b98d3-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="b98d3-140">Per informazioni generali, vedere hello [pagina principale per set di scalabilità](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="b98d3-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

