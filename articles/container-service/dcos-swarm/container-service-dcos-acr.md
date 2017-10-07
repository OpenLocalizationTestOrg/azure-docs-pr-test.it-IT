---
title: aaaUsing record con un cluster di controller di dominio o sistema operativo di Azure | Documenti Microsoft
description: Usare Registro contenitori di Azure con un cluster DC/OS nel servizio contenitore di Azure
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, contenitori, micro-servizi, Mesos, Azure, FileShare, CIFS
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>Usare ACR con toodeploy di cluster un controller di dominio o del sistema operativo, l'applicazione

In questo articolo esamineremo come toouse del Registro di sistema di Azure contenitore con un cluster di controller di dominio o del sistema operativo. Utilizzando ACR consente tooprivately store e gestire le immagini contenitore. Questa esercitazione sono trattati hello seguenti attività:

> [!div class="checklist"]
> * Distribuire il Registro contenitori di Azure (se necessario)
> * Configurare l'autenticazione del record di controllo di accesso in un cluster del controller di dominio/sistema operativo
> * Caricare un toohello immagine del Registro di sistema contenitore di Azure
> * Eseguire un'immagine contenitore da hello del Registro di sistema contenitore di Azure

È necessario un ACS controller di dominio o sistema operativo hello toocomplete cluster i passaggi in questa esercitazione. Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.

Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Distribuire il Registro contenitori di Azure

Se necessario, creare un registro di sistema del contenitore di Azure con hello [az acr creare](/cli/azure/acr#create) comando. 

esempio Hello crea un registro di sistema con un nome di generare in modo casuale. Registro di sistema Hello viene inoltre configurato con un account di amministratore utilizzando hello `--admin-enabled` argomento.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Dopo aver creato il registro hello, hello CLI di Azure genera dati simili toohello successivi. Prendere nota di hello `name` e `loginServer`, questi vengono utilizzati nei passaggi successivi.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Ottenere le credenziali del Registro di sistema di contenitore hello utilizzando hello [Mostra credenziale di az acr](/cli/azure/acr/credential) comando. Hello Substitute `--name` con hello uno indicato nell'ultimo passaggio hello. Prendere nota di una password, che sarà necessaria in un passaggio successivo.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Per ulteriori informazioni sul Registro di sistema contenitore di Azure, vedere [registri contenitore Docker di introduzione tooprivate](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>Gestire l'autenticazione del record di controllo di accesso

metodo convenzionale per Hello immagine toopush e pull da un registro di sistema privato è toofirst l'autenticazione con il Registro di sistema hello. toodo, è necessario utilizzare hello `docker login` comando in qualsiasi client necessarie del Registro di sistema di tooaccess hello privata. Poiché un cluster di controller di dominio o del sistema operativo può contenere molti nodi, ognuno dei quali è necessario toobe autenticato con hello ACR, è utile tooautomate questo processo in ciascun nodo. 

### <a name="create-shared-storage"></a>Creare uno spazio di archiviazione condiviso

Questo processo usa una condivisione di file di Azure che è stata montata in ogni nodo cluster hello. Se non è già stato impostato lo spazio di archiviazione condiviso, vedere [Creare e montare una condivisione di file per un cluster DC/OS](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>Configurare l'autenticazione del record di controllo di accesso

Innanzitutto, ottenere hello FQDN di hello DC/OS master e archiviarlo in una variabile.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Creare una connessione SSH con hello master (o master prima di hello) del cluster basato su controller di dominio/OS. Aggiornare il nome utente hello se è stato utilizzato un valore non predefinito durante la creazione di cluster hello.

```azurecli-interactive
ssh azureuser@$FQDN
```

Comando che segue di esecuzione hello toologin toohello del Registro di sistema contenitore di Azure. Sostituire hello `--username` con nome hello del Registro di sistema contenitore hello e hello `--password` con una delle password hello fornito. Sostituire l'ultimo argomento hello *mycontainerregistry.azurecr.io* nell'esempio hello con nome loginServer hello del Registro di sistema di hello contenitore. 

Questo comando Archivia i valori di autenticazione hello localmente in hello `~/.docker` percorso.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Creare un file compresso che contiene i valori di autenticazione hello contenitore del Registro di sistema.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Copiare questa risorsa di archiviazione di file toohello condiviso del cluster. Questo passaggio rende disponibili in tutti i nodi del cluster di controller di dominio/OS hello file hello.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Caricare l'immagine tooACR

Ora da un computer di sviluppo, o qualsiasi altro sistema con Docker installato, creare un'immagine e caricarlo toohello del Registro di sistema contenitore di Azure.

Creare un contenitore dall'immagine Ubuntu hello.

```azurecli-interactive
docker run ubunut --name base-image
```

Ora l'acquisizione hello contenitore in una nuova immagine. nome dell'immagine Hello deve hello tooinclude `loginServer` nome di hello contenitore registrywith un formato di `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Account di accesso in hello del Registro di sistema contenitore di Azure. Sostituire hello con nome loginServer hello, hello - nome utente con nome hello del Registro di sistema contenitore hello e hello - password con una delle password hello fornito.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Infine, caricare del Registro di sistema di hello immagine toohello record. In questo esempio si carica un'immagine denominata dcos-demo.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Eseguire un'immagine dal record di controllo di accesso

toouse un'immagine dal Registro di sistema ACR hello, creare un file di nomi *acrDemo.json* e hello copia seguente testo al suo interno. Sostituire il nome di immagine hello con hello contenitore del Registro di sistema loginServer nome e il nome dell'immagine, ad esempio `loginServer/imageName`. Prendere nota di hello `uris` proprietà. Questa proprietà contiene hello percorso file hello contenitore del Registro di sistema l'autenticazione, ovvero in questo caso condivisione di file di Azure hello montato in ogni nodo nel cluster di controller di dominio/OS hello.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Distribuire un'applicazione hello con hello CLI DC / ° c.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono configuri toouse controller di dominio o del sistema operativo Azure contenitore Registro di sistema inclusi hello seguenti attività:

> [!div class="checklist"]
> * Distribuire il Registro contenitori di Azure (se necessario)
> * Configurare l'autenticazione del record di controllo di accesso in un cluster del controller di dominio/sistema operativo
> * Caricare un toohello immagine del Registro di sistema contenitore di Azure
> * Eseguire un'immagine contenitore da hello del Registro di sistema contenitore di Azure
