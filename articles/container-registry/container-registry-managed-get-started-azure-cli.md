---
title: aaaCreate registro contenitore privato Docker - CLI di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Creare un registro di sistema di contenitore gestito mediante hello CLI di Azure

Registro contenitori di Azure è un servizio gestito di registri contenitori Docker usato per l'archiviazione di immagini di un contenitore Docker privato. Questa guida descrive la creazione di un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello CLI di Azure.

I registri contenitori di Azure gestiti sono in anteprima e non disponibili in tutte le aree di Azure.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westcentralus* percorso.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Creare un registro di contenitori

Creare un'istanza di record con hello [az acr creare](/cli/azure/acr#create) comando.

> [!NOTE]
> Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri.

 nome del Registro di sistema Hello nell'esempio hello è *myContainerRegistry1*, sostituire con un nome univoco del proprio.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Quando viene creato il registro hello, l'output di hello è simile toohello seguenti:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>Accedi tooACR istanza

Prima di push e pull immagini contenitore, è necessario accedere nell'istanza di record toohello. toodo in tal caso, utilizzare hello [accesso acr az](/cli/azure/acr#login) comando.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

comando Hello restituisce un messaggio 'Accesso riuscito' una volta completato.

## <a name="use-azure-container-registry"></a>Usare Registro contenitori di Azure

### <a name="list-container-images"></a>Elencare le immagini del contenitore

Hello utilizzare `az acr` contiene i comandi CLI immagini hello tooquery e tag in un repository.

> [!NOTE]
> Registro di sistema di contenitore non supporta attualmente hello `docker search` comando tooquery per immagini e i tag.

### <a name="list-repositories"></a>Elencare repository

Hello esempio seguente vengono elencati i repository hello nel Registro di sistema, in formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Elencare tag

Hello esempio seguente vengono elencati i tag hello in hello **esempi/nginx** repository, in formato JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Passaggi successivi

In questa Guida introduttiva è stata creata un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello CLI di Azure.

> [!div class="nextstepaction"]
> [La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md)
