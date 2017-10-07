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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Convertire un modello di set di scalabilità set modello tooa disco gestito scala

I clienti con un modello di gestione risorse per la creazione di un set non utilizza disco gestito di scalabilità può essere utile toomodify è toouse gestiti disco. Questo articolo viene illustrato come toodo questo, utilizzando ad esempio una richiesta di pull da hello [modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates), un repository basato sulla community per i modelli di gestione risorse di esempio. richiesta di pull completo Hello sono consultabili qui: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), e parti inerenti hello hello diff sono di sotto, insieme a una spiegazione:

## <a name="making-hello-os-disks-managed"></a>Rendere i dischi del sistema operativo hello gestiti

Nel diff hello riportato di seguito, si noterà che è stata rimossa diverse variabili correlate toostorage account e disco proprietà. Tipo di account di archiviazione non è più necessario (Standard_LRS è predefinito hello), ma è possibile specificare comunque Se si desidera. Con il disco gestito sono supportati solo Standard_LRS e Premium_LRS. Nuovo suffisso di account di archiviazione, matrice di stringhe univoche e il numero di sa utilizzati nei nomi di archiviazione hello vecchio modello toogenerate account. Queste variabili non sono più necessari nel nuovo modello di hello perché disco gestito crea automaticamente gli account di archiviazione per conto del cliente hello. Analogamente, il nome di contenitore vhd e il nome del disco del sistema operativo non sono più necessarie poiché disco gestito nomi automaticamente i dischi e i contenitori blob di archiviazione sottostante hello.

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


In hello diff seguito, è possibile vedere che abbiamo aggiornato hello calcolare versione too2016-04-30-l'anteprima dell'api, ovvero hello versione meno recente necessario per il supporto di dischi gestiti con set di scalabilità. Si noti che è possibile usare ancora i dischi non gestiti in hello nuova versione dell'api con sintassi precedente hello se lo si desidera. In altre parole, se si aggiorna solo hello versione dell'api di calcolo e di non modificare nemmeno altri elementi, il modello di hello deve continuare toowork come prima.

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

Nel diff hello riportato di seguito, si noterà che viene rimossa risorsa account di archiviazione hello dalla matrice di risorse hello completamente. Non è più necessaria perché il disco gestito la crea automaticamente.

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

In hello diff seguito, è possibile vedere che viene rimossa hello dipende clausola che fa riferimento la ciclo hello scala set toohello che la creazione di account di archiviazione. Nel modello precedente hello, questo è stato verificato che siano stati creati gli account di archiviazione hello prima che il set di scalabilità di hello è iniziata la creazione, ma questa clausola non è più necessaria con disco gestito. È inoltre rimuovere proprietà di contenitori vhd hello e hello proprietà del nome del disco del sistema operativo come queste proprietà vengono gestite automaticamente quinte hello dal disco gestito. Se si intende, è possibile aggiungere `"managedDisk": { "storageAccountType": "Premium_LRS" }` nella configurazione di "osDisk" hello se si volevano i dischi del sistema operativo premium. Solo le macchine virtuali con una maiuscola o del minuscola ' nella macchina virtuale hello sku è possibile utilizzare i dischi premium.

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

Non è nessuna proprietà esplicita nella configurazione di set di scalabilità di hello per se toouse gestito o un disco non gestito. set di scalabilità Hello sa quale toouse in base alle proprietà hello presenti nel profilo di archiviazione hello. Di conseguenza, è importante quando si modifica tooensure modello hello che sono proprietà diritti hello nel profilo di archiviazione hello del set di scalabilità hello.


## <a name="data-disks"></a>Dischi dati

Con le modifiche hello sopra, hello scala set utilizza gestito per hello del sistema operativo dischi, ma sui dischi dati? i dischi dati tooadd, aggiungere della proprietà "dataDisks" hello "storageProfile" in hello stesso livello come "osDisk". valore della proprietà hello Hello è un elenco JSON di oggetti, ognuno dei quali dispone di proprietà "lun" (che deve essere univoco per ogni disco dati in una macchina virtuale), "createOption" ("empty" è attualmente hello opzione supportata solo) e "diskSizeGB" (dimensioni del disco hello in gigabyte hello; deve essere maggiore di 0 e minore di 1024) come illustrato nell'esempio seguente hello: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Se si specifica `n` dischi in questa matrice, ogni macchina virtuale nella scala hello impostato Ottiene `n` dischi dati. Si noti tuttavia che questi dischi dati sono dispositivi RAW. Non sono formattati. È di toohello cliente tooattach, Partition e dischi in formato hello prima di usarli. Facoltativamente, è inoltre possibile specificare `"managedDisk": { "storageAccountType": "Premium_LRS" }` in ogni toospecify di oggetto disco dati che deve essere un disco dati premium. Solo le macchine virtuali con una maiuscola o del minuscola ' nella macchina virtuale hello sku è possibile utilizzare i dischi premium.

toolearn ulteriori informazioni sull'utilizzo di dischi di dati con il set di scalabilità, vedere [questo articolo](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Passaggi successivi
Ad esempio utilizzando set di scalabilità di modelli di gestione risorse di ricerca per "vmss" hello [repository github dei modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).

Per informazioni generali, vedere hello [pagina principale per set di scalabilità](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

