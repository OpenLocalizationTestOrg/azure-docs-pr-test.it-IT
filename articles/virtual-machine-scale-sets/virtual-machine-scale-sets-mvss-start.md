---
title: "impostare i modelli di aaaLearn sulla scalabilità di macchine virtuali | Documenti Microsoft"
description: "Informazioni su una scala minima praticabile toocreate Imposta modello per il set di scalabilità di macchine virtuali"
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
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Informazioni sui modelli di set di scalabilità di macchine virtuali
[Modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) sono un ottimo modo toodeploy gruppi di risorse correlate. Questa serie di esercitazioni viene illustrato come modello di set di toocreate una scala minima valida e come toomodify toosuit questo modello vari scenari. Tutti gli esempi provengono da questo [archivio GitHub](https://github.com/gatneil/mvss). 

Questo modello è previsto toobe semplice. Per esempi più completi della scala impostare i modelli, vedere hello [repository GitHub modelli Guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates) e cercare le cartelle che contengono la stringa hello `vmss`.

Se si ha già familiarità con la creazione di modelli, è possibile ignorare toohello toosee di sezione "Passaggi successivi" come toomodify questo modello.

## <a name="review-hello-template"></a>Modello di hello revisione

Utilizzare GitHub tooreview modello, di impostare la scala minima valida [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

In questa esercitazione verranno esaminati hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimo possibili set di scalabilità di modello di elemento per elemento.

## <a name="define-schema-and-contentversion"></a>Definire $schema e contentVersion
In primo luogo, definiamo `$schema` e `contentVersion` nel modello di hello. Hello `$schema` elemento definisce una versione di hello hello della lingua del modello e viene utilizzato per l'evidenziazione della sintassi di Visual Studio e le funzionalità di convalida simile. Hello `contentVersion` elemento non viene usato da Azure. In alternativa, consente di tenere traccia di versione del modello di hello.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>Definire i parametri
Successivamente, si definiscono due parametri, `adminUsername` e `adminPassword`. I parametri sono i valori specificati in fase di hello della distribuzione. Hello `adminUsername` parametro è semplicemente un `string` tipo, ma poiché `adminPassword` è un segreto, abbiamo assegnarle tipo `securestring`. In un secondo momento, questi parametri vengono passati in configurazione di set di scalabilità hello.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Definire le variabili
Modelli di gestione risorse consentono inoltre di definire variabili toobe utilizzato in un secondo momento nel modello di hello. Questo esempio non utilizza tutte le variabili, in modo sono stati lasciati oggetto JSON hello vuoto.

```json
  "variables": {},
```

## <a name="define-resources"></a>Definire le risorse
Di seguito è la sezione relativa alle risorse hello del modello di hello. In questo caso, definire i dati effettivamente da toodeploy. A differenza di `parameters` e `variables` (che sono oggetti JSON), `resources` è un elenco JSON di oggetti JSON.

```json
   "resources": [
```

Tutte le risorse richiedono le proprietà `type`, `name`, `apiVersion` e `location`. La prima risorsa di questo esempio è di tipo `Microsft.Network/virtualNetwork`, nome `myVnet` e apiVersion `2016-03-30`. (toofind hello versione API più recente per un tipo di risorsa, vedere hello [documentazione dell'API REST di Azure](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Specificare il percorso
percorso di hello toospecify per la rete virtuale hello, utilizzare un [funzione di modello di gestione risorse](../azure-resource-manager/resource-group-template-functions.md). Questa funzione deve essere racchiusa tra virgolette e parentesi quadre, nel modo seguente: `"[<template-function>]"`. In questo caso, utilizziamo hello `resourceGroup` (funzione). Accetta alcun argomento e restituisce un oggetto JSON con metadati relativi al gruppo di risorse hello che viene distribuita per questa distribuzione. gruppo di risorse Hello viene impostata dall'utente hello in fase di hello della distribuzione. È quindi indice nell'oggetto JSON con `.location` percorso hello tooget da un oggetto JSON hello.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Specificare le proprietà di rete virtuale
Ogni risorsa di gestione risorse ha il proprio `properties` sezione per la risorsa toohello specifico di configurazioni. In questo caso, si specifica rete virtuale hello deve avere una subnet con intervallo di indirizzi IP privati hello `10.0.0.0/16`. Un set di scalabilità è sempre contenuto in una subnet. Non può estendersi a più subnet.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>Aggiungere un elenco dependsOn
È inoltre richiesto di toohello `type`, `name`, `apiVersion`, e `location` le proprietà, ogni risorsa possono avere un parametro facoltativo `dependsOn` elenco di stringhe. Questo elenco specifica le altre risorse di questa distribuzione che devono essere completate prima di distribuire la risorsa.

In questo caso, è presente un solo elemento nell'elenco di hello, rete virtuale di hello dall'esempio precedente hello. Si specifica questa dipendenza perché hello set di scalabilità è necessario hello rete tooexist prima di creare tutte le macchine virtuali. In questo modo, il set di scalabilità di hello può concedere a questi indirizzi IP privati di macchine virtuali dall'intervallo di indirizzi IP hello in precedenza specificato nelle proprietà di rete hello. formato Hello di ogni stringa nell'elenco di dependsOn hello è `<type>/<name>`. Utilizzare hello stesso `type` e `name` utilizzata in precedenza nella definizione di risorsa di rete virtuale hello.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Specificare le proprietà del set di scalabilità
Set di scalabilità hanno molte proprietà per la personalizzazione hello macchine virtuali nel set di scalabilità hello. Per un elenco completo di queste proprietà, vedere hello [set di scalabilità della documentazione dell'API REST](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). Per questa esercitazione, verranno impostate solo alcune proprietà usate di frequente.
### <a name="supply-vm-size-and-capacity"></a>Specificare capacità e dimensioni della macchina virtuale
scala Hello imposta tooknow esigenze le dimensioni della macchina virtuale toocreate ("nome sku") e quanti tali toocreate macchine virtuali ("capacità sku"). toosee le dimensioni delle macchine Virtuali sono disponibili, vedere hello [documentazione dimensioni delle macchine Virtuali](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Scegliere un tipo di aggiornamenti
set di scalabilità Hello deve inoltre tooknow modalità di aggiornamento nel set di scalabilità hello toohandle. Attualmente sono disponibili due opzioni, `Manual` e `Automatic`. Per ulteriori informazioni sulle differenze tra due hello la hello, vedere la documentazione di hello in [come tooupgrade un set di scalabilità](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>Scegliere il sistema operativo delle macchine virtuali
Hello set di scalabilità esigenze tooknow tooput il sistema operativo nelle macchine virtuali hello. In questo caso, creare macchine virtuali di hello con un'immagine di 16.04 LTS Ubuntu completamente con patch.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>Specificare computerNamePrefix
set di scalabilità Hello consente di distribuire più macchine virtuali. Anziché specificare il nome di ogni macchina virtuale, si specifica `computerNamePrefix`. Hello set di scalabilità aggiunge un prefisso toohello di indice per ogni macchina virtuale, in modo da dispongono di nomi di macchina virtuale modulo hello `<computerNamePrefix>_<auto-generated-index>`.

In hello seguente frammento di codice, utilizziamo parametri hello dalla prima tooset hello amministratore username e password per tutte le macchine virtuali nel set di scalabilità hello. Facciamo con hello `parameters` funzione di modello. Questa funzione accetta una stringa che specifica quali tooand toorefer parametro restituisce il valore di hello per tale parametro.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>Specificare la configurazione di rete delle macchine virtuali
Infine, è necessario toospecify configurazione di rete hello per le macchine virtuali hello in set di scalabilità hello. In questo caso, è necessario solo toospecify hello ID di subnet hello creato in precedenza. In questo modo hello set di scalabilità tooput interfacce di rete hello in questa subnet.

È possibile ottenere hello ID di rete virtuale di hello contenente subnet hello utilizzando hello `resourceId` funzione di modello. Questa funzione accetta il tipo di hello e il nome di una risorsa e restituisce hello identificatore completo della risorsa. Questo ID è hello:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

Tuttavia, identificatore hello della rete virtuale hello non è sufficiente. È necessario specificare una subnet specifica hello che hello set di scalabilità di in che macchine virtuali devono trovarsi. toodo, concatenare `/subnets/mySubnet` toohello ID di rete virtuale hello. il risultato di Hello è hello completo di ID di subnet hello. Eseguire questa concatenazione con hello `concat` funzione che accetta una serie di stringhe e restituisce la concatenazione.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
