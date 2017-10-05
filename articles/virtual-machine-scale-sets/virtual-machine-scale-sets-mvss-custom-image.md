---
title: "Fare riferimento a un'immagine personalizzata in un modello di set di scalabilità di Azure | Microsoft Docs"
description: "Informazioni su come aggiungere un'immagine personalizzata in un modello di set di scalabilità di macchine virtuali di Azure esistente"
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
ms.openlocfilehash: cf52fc9e95267c4bc5c0106aadf626685ddd5c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-custom-image-to-an-azure-scale-set-template"></a><span data-ttu-id="99c92-103">Aggiungere un'immagine personalizzata in un modello di set di scalabilità di Azure</span><span class="sxs-lookup"><span data-stu-id="99c92-103">Add a custom image to an Azure scale set template</span></span>

<span data-ttu-id="99c92-104">Questo articolo illustra come modificare il [modello di set di scalabilità a validità minima](./virtual-machine-scale-sets-mvss-start.md) per la distribuzione da un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="99c92-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy from custom image.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="99c92-105">Modificare la definizione del modello</span><span class="sxs-lookup"><span data-stu-id="99c92-105">Change the template definition</span></span>

<span data-ttu-id="99c92-106">Il modello di set di scalabilità a validità minima è disponibile [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), mentre il modello per la distribuzione del set di scalabilità da un'immagine personalizzata è disponibile [qui](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="99c92-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="99c92-107">Viene ora esaminato il diff usato per creare questo modello, `git diff minimum-viable-scale-set custom-image`, passo per passo:</span><span class="sxs-lookup"><span data-stu-id="99c92-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="99c92-108">Creazione dell'immagine di un disco gestito</span><span class="sxs-lookup"><span data-stu-id="99c92-108">Creating a managed disk image</span></span>

<span data-ttu-id="99c92-109">Se si dispone già di un'immagine di disco gestito personalizzata (una risorsa di tipo `Microsoft.Compute/images`), è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="99c92-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="99c92-110">Prima di tutto si aggiunge un parametro `sourceImageVhdUri`, ovvero l'URI del BLOB generalizzato in Archiviazione di Azure contenente l'immagine personalizzata da usare per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="99c92-110">First, we add a `sourceImageVhdUri` parameter, which is the URI to the generalized blob in Azure Storage that contains the custom image to deploy from.</span></span>


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "The source of the generalized blob containing the custom image"
+      }
     }
   },
   "variables": {},
```

<span data-ttu-id="99c92-111">Poi si aggiunge una risorsa di tipo `Microsoft.Compute/images`, ovvero l'immagine del disco gestito basata sul BLOB generalizzato presente nell'URI `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="99c92-111">Next, we add a resource of type `Microsoft.Compute/images`, which is the managed disk image based on the generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="99c92-112">Questa immagine deve trovarsi nella stessa area del set di scalabilità da cui viene usata.</span><span class="sxs-lookup"><span data-stu-id="99c92-112">This image must be in the same region as the scale set that uses it.</span></span> <span data-ttu-id="99c92-113">Nelle proprietà dell'immagine, si specifica il tipo di sistema operativo, la posizione del BLOB (ottenuta dal parametro `sourceImageVhdUri`) e il tipo di account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="99c92-113">In the properties of the image, we specify the OS type, the location of the blob (from the `sourceImageVhdUri` parameter), and the storage account type:</span></span>

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

<span data-ttu-id="99c92-114">Nella risorsa del set di scalabilità, si aggiunge una clausola `dependsOn` che fa riferimento all'immagine personalizzata, in modo da essere certi che l'immagine venga creata prima che il set di scalabilità tenti la distribuzione da tale immagine:</span><span class="sxs-lookup"><span data-stu-id="99c92-114">In the scale set resource, we add a `dependsOn` clause referring to the custom image to make sure the image gets created before the scale set tries to deploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-to-use-the-managed-disk-image"></a><span data-ttu-id="99c92-115">Modifica delle proprietà del set di scalabilità per usare l'immagine del disco gestito</span><span class="sxs-lookup"><span data-stu-id="99c92-115">Changing scale set properties to use the managed disk image</span></span>

<span data-ttu-id="99c92-116">In `imageReference` del set di scalabilità `storageProfile`, anziché specificare entità di pubblicazione, offerta, SKU e versione di un'immagine della piattaforma, si specifica l'`id` della risorsa `Microsoft.Compute/images`:</span><span class="sxs-lookup"><span data-stu-id="99c92-116">In the `imageReference` of the scale set `storageProfile`, instead of specifying the publisher, offer, sku, and version of a platform image, we specify the `id` of the `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="99c92-117">In questo esempio, viene usata la funzione `resourceId` per ottenere l'ID dell'immagine creata nello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="99c92-117">In this example, we use the `resourceId` function to get the resource ID of the image created in the same template.</span></span> <span data-ttu-id="99c92-118">Se l'immagine del disco gestito è stata creata in precedenza, è necessario fornire invece l'ID di tale immagine.</span><span class="sxs-lookup"><span data-stu-id="99c92-118">If you have created the managed disk image beforehand, you should provide the id of that image instead.</span></span> <span data-ttu-id="99c92-119">L'ID deve essere nel formato seguente: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="99c92-119">This id must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="99c92-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99c92-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
