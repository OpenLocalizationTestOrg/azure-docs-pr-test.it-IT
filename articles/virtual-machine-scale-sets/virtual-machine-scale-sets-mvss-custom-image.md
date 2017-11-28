---
title: "Fare riferimento a un'immagine personalizzata in un modello di set di scalabilità di Azure | Microsoft Docs"
description: "Informazioni su come tooadd personalizzato immagine modello di Set di scalabilità della macchina virtuale Azure esistente tooan"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="fcdfe-103">Aggiungere che modello di set di tooan un'immagine personalizzata scalabilità di Azure</span><span class="sxs-lookup"><span data-stu-id="fcdfe-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="fcdfe-104">Questo articolo viene illustrato come hello toomodify [scala valida minima Imposta modello](./virtual-machine-scale-sets-mvss-start.md) toodeploy dall'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="fcdfe-105">Modificare la definizione di modello hello</span><span class="sxs-lookup"><span data-stu-id="fcdfe-105">Change hello template definition</span></span>

<span data-ttu-id="fcdfe-106">Può essere visualizzato il modello di set di scala valida minima [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e il modello per la distribuzione di scala hello impostato da un'immagine personalizzata può essere visto [qui](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="fcdfe-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="fcdfe-107">Questo modello si esamineranno hello diff utilizzato toocreate (`git diff minimum-viable-scale-set custom-image`), elemento per elemento:</span><span class="sxs-lookup"><span data-stu-id="fcdfe-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="fcdfe-108">Creazione dell'immagine di un disco gestito</span><span class="sxs-lookup"><span data-stu-id="fcdfe-108">Creating a managed disk image</span></span>

<span data-ttu-id="fcdfe-109">Se si dispone già di un'immagine di disco gestito personalizzata (una risorsa di tipo `Microsoft.Compute/images`), è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="fcdfe-110">In primo luogo, aggiungiamo un `sourceImageVhdUri` hello URI toohello generalizzato blob in archiviazione di Azure che contiene toodeploy immagine personalizzata hello dal parametro.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

<span data-ttu-id="fcdfe-111">Successivamente si aggiungerà una risorsa di tipo `Microsoft.Compute/images`, quale immagine di disco gestito hello si basa sul blob hello generalizzato in URI `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="fcdfe-112">Questa immagine deve essere in hello stessa area come set di scalabilità hello che lo utilizza.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="fcdfe-113">Nelle proprietà dell'immagine di hello hello è specificare hello del sistema operativo, posizione di hello del blob hello (da hello `sourceImageVhdUri` parametro) e tipo di account di archiviazione hello:</span><span class="sxs-lookup"><span data-stu-id="fcdfe-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

<span data-ttu-id="fcdfe-114">In hello scala risorsa del set, viene aggiunta una `dependsOn` clausola toohello immagine personalizzata toomake immagine hello Ottiene creata prima di set di scalabilità hello tenta toodeploy da quell'immagine di riferimento:</span><span class="sxs-lookup"><span data-stu-id="fcdfe-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="fcdfe-115">Modifica scala set immagine del disco gestito hello toouse proprietà</span><span class="sxs-lookup"><span data-stu-id="fcdfe-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="fcdfe-116">In hello `imageReference` della scala hello impostare `storageProfile`, anziché specificare un server di pubblicazione hello, offerta, sku e versione di un'immagine della piattaforma, specifichiamo hello `id` di hello `Microsoft.Compute/images` risorse:</span><span class="sxs-lookup"><span data-stu-id="fcdfe-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

<span data-ttu-id="fcdfe-117">In questo esempio, si usa hello `resourceId` ID risorsa della funzione tooget hello dell'immagine di hello creati in hello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="fcdfe-118">Se è stato creato immagine disco gestito hello in anticipo, è necessario fornire invece id hello dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="fcdfe-119">Questo id deve essere formato hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="fcdfe-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fcdfe-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fcdfe-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
