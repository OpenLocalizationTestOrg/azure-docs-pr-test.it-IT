---
title: aaaCreate il primo contenitore di istanze di contenitori di Azure | Documenti di Azure
description: Distribuire e iniziare a usare Istanze di contenitore di Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Creare il primo contenitore in Istanze di contenitore di Azure

Istanze di contenitori Azure rende facile toocreate e gestire i contenitori in Azure. In questa Guida introduttiva, verrà creato un contenitore in Azure ed esporlo toohello internet con un indirizzo IP pubblico. Per completare questa operazione, è sufficiente un solo comando. In pochi secondi, nel browser verrà visualizzato quanto segue:

![App distribuita usando Istanze di contenitore di Azure visualizzata nel browser][aci-app-browser]

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.12 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Le istanze di contenitore di Azure sono risorse di Azure e devono essere inserite in un gruppo di risorse di Azure, una raccolta logica in cui le risorse di Azure vengono distribuite e gestite.

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Creare un contenitore

Per creare un contenitore, specificare un nome, un'immagine Docker e un gruppo di risorse di Azure. Facoltativamente è possibile esporre hello contenitore toohello internet con un indirizzo IP pubblico. In questo caso, verrà usato un contenitore che ospita un'app Web molto semplice scritta in [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Entro pochi secondi, è necessario ottenere una richiesta di tooyour di risposta. Inizialmente, il contenitore di hello verrà incluso un **creazione** stato, ma deve iniziare in pochi secondi. È possibile controllare lo stato di hello utilizzando hello `show` comando:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

Nella parte inferiore di hello dell'output di hello, verrà visualizzato lo stato del provisioning del contenitore hello e l'indirizzo IP:

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Una volta contenitore hello Sposta toohello **Succeeded** stato, è possibile raggiungerli nel browser hello utilizzando l'indirizzo IP hello fornito. 

![App distribuita usando Istanze di contenitore di Azure visualizzata nel browser][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Pull hello contenitore log

È possibile effettuare il pull nei registri hello contenitore hello è stato creato mediante hello `logs` comando:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Output:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Eliminare il contenitore di hello

Al termine con contenitore hello, è possibile rimuoverla utilizzando hello `delete` comando:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

Tutti di hello del codice per il contenitore di hello utilizzato in questa Guida introduttiva è disponibile [su GitHub][app-github-repo], insieme ai relativi Dockerfile. Se si desidera tootry compilazione manualmente e la distribuzione di istanze di contenitori tooAzure utilizzando hello del Registro di sistema contenitore di Azure, è possibile continuare toohello esercitazione di istanze di contenitori di Azure.

> [!div class="nextstepaction"]
> [Esercitazioni su Istanze di contenitore di Azure](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png