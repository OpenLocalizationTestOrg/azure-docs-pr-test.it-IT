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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Aggiungere che modello di set di tooan un'immagine personalizzata scalabilità di Azure

Questo articolo viene illustrato come hello toomodify [scala valida minima Imposta modello](./virtual-machine-scale-sets-mvss-start.md) toodeploy dall'immagine personalizzata.

## <a name="change-hello-template-definition"></a>Modificare la definizione di modello hello

Può essere visualizzato il modello di set di scala valida minima [qui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e il modello per la distribuzione di scala hello impostato da un'immagine personalizzata può essere visto [qui](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Questo modello si esamineranno hello diff utilizzato toocreate (`git diff minimum-viable-scale-set custom-image`), elemento per elemento:

### <a name="creating-a-managed-disk-image"></a>Creazione dell'immagine di un disco gestito

Se si dispone già di un'immagine di disco gestito personalizzata (una risorsa di tipo `Microsoft.Compute/images`), è possibile ignorare questa sezione.

In primo luogo, aggiungiamo un `sourceImageVhdUri` hello URI toohello generalizzato blob in archiviazione di Azure che contiene toodeploy immagine personalizzata hello dal parametro.


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

Successivamente si aggiungerà una risorsa di tipo `Microsoft.Compute/images`, quale immagine di disco gestito hello si basa sul blob hello generalizzato in URI `sourceImageVhdUri`. Questa immagine deve essere in hello stessa area come set di scalabilità hello che lo utilizza. Nelle proprietà dell'immagine di hello hello è specificare hello del sistema operativo, posizione di hello del blob hello (da hello `sourceImageVhdUri` parametro) e tipo di account di archiviazione hello:

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

In hello scala risorsa del set, viene aggiunta una `dependsOn` clausola toohello immagine personalizzata toomake immagine hello Ottiene creata prima di set di scalabilità hello tenta toodeploy da quell'immagine di riferimento:

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Modifica scala set immagine del disco gestito hello toouse proprietà

In hello `imageReference` della scala hello impostare `storageProfile`, anziché specificare un server di pubblicazione hello, offerta, sku e versione di un'immagine della piattaforma, specifichiamo hello `id` di hello `Microsoft.Compute/images` risorse:

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

In questo esempio, si usa hello `resourceId` ID risorsa della funzione tooget hello dell'immagine di hello creati in hello stesso modello. Se è stato creato immagine disco gestito hello in anticipo, è necessario fornire invece id hello dell'immagine. Questo id deve essere formato hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
