---
title: esercitazione per il servizio contenitore aaaAzure - preparare ACR | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - Preparare il Registro contenitori di Azure
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Distribuire e usare il Registro contenitori di Azure

Il Registro contenitori di Azure è un registro privato basato su Azure per le immagini del contenitore Docker. Questa esercitazione, la seconda parte della sette, illustra la distribuzione di un'istanza del Registro di sistema di Azure contenitore e inserendo un tooit immagine contenitore. I passaggi completati comprendono:

> [!div class="checklist"]
> * Distribuzione di un'istanza di Registro contenitori di Azure
> * Assegnazione di tag a un'immagine del contenitore per Registro contenitori di Azure
> * Caricamento hello immagine tooACR

Nelle esercitazioni successive, questa istanza del registro contenitori di Azure viene integrata con un cluster Kubernetes del servizio contenitore di Azure, per eseguire in modo sicuro le immagini del contenitore. 

## <a name="before-you-begin"></a>Prima di iniziare

In hello [esercitazione precedente](./container-service-tutorial-kubernetes-prepare-app.md), un'immagine contenitore è stata creata per una semplice applicazione di Azure di voto. In questa esercitazione, questa immagine viene inserita tooan del Registro di sistema contenitore di Azure. Se non è stato creato immagine dell'app di Azure voto hello, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md). In alternativa, passaggi hello descritto in questo punto utilizzare qualsiasi immagine contenitore.

Questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Distribuire il Registro contenitori di Azure

Prima di distribuire un Registro contenitori di Azure, è necessario che esista un gruppo di risorse. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. In questo esempio, un gruppo di risorse denominato *myResourceGroup* viene creato in hello *westeurope* area.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Creare un registro di sistema del contenitore di Azure con hello [az acr creare](/cli/azure/acr#create) comando. nome di un contenitore del Registro di sistema di Hello **deve essere univoco**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

Tutta hello di questa esercitazione, utilizziamo "acrname" come segnaposto per nome del Registro di sistema del contenitore hello scelto.

## <a name="container-registry-login"></a>Accesso al registro contenitori

È necessario accedere in istanza ACR tooyour prima push tooit immagini. Hello utilizzare [accesso acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operazione hello toocomplete di comando. È necessario il nome univoco di tooprovide hello assegnato del Registro di sistema di toohello contenitore al momento della creazione.

```azurecli
az acr login --name <acrName>
```

comando Hello restituisce un messaggio 'Accesso riuscito' una volta completato.

## <a name="tag-container-images"></a>Assegnare tag alle immagini del contenitore

Ogni immagine di contenitore deve toobe contrassegnato con il nome loginServer hello del Registro di sistema hello. Questo tag viene usato per il routing quando push del Registro di sistema di contenitore immagini tooan immagine.

un elenco di immagini corrente, utilizzare hello toosee [immagini docker](https://docs.docker.com/engine/reference/commandline/images/) comando.

```bash
docker images
```

Output:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

tooget hello loginServer nome eseguire hello comando seguente.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

A questo punto, hello di tag *azure voto-anteriore* immagine con loginServer hello del Registro di sistema di hello contenitore. Inoltre, aggiungere `:redis-v1` toohello fine del nome dell'immagine hello. Questo tag indica una versione dell'immagine hello.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

Una volta contrassegnate, eseguire [immagini docker] operazione di hello tooverify (https://docs.docker.com/engine/reference/commandline/images/).

```bash
docker images
```

Output:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Push tooregistry immagini

Push hello *azure voto-anteriore* registro toohello di immagini. 

Utilizzando hello di esempio seguente, sostituire nome loginServer di hello ACR con loginServer hello dall'ambiente in uso.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Questa operazione richiede un paio di minuti toocomplete.

## <a name="list-images-in-registry"></a>Elencare le immagini nel registro

un elenco di immagini che sono stati inseriti tooyour Azure contenitore del Registro di sistema, hello utente tooreturn [elenco repository di az acr](/cli/azure/acr/repository#list) comando. Aggiornare il comando hello con il nome di istanza ACR hello.

```azurecli
az acr repository list --name <acrName> --output table
```

Output:

```azurecli
Result
----------------
azure-vote-front
```

Quindi tag hello toosee per un'immagine specifica, utilizzare hello [az acr repository Mostra-tag](/cli/azure/acr/repository#show-tags) comando.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Output:

```azurecli
Result
--------
redis-v1
```

Al termine dell'esercitazione, l'immagine contenitore hello è stato archiviato in un'istanza del Registro di sistema di Azure contenitore privata. Questa immagine viene distribuita dal cluster di record tooa Kubernetes nelle esercitazioni successive.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione un Registro contenitori di Azure è stato preparato per l'uso in un cluster Kubernetes del servizio contenitore di Azure. sono stata completata Hello alla procedura seguente:

> [!div class="checklist"]
> * Distribuzione di un'istanza di Registro contenitori di Azure
> * Assegnazione di tag a un'immagine del contenitore per Registro contenitori di Azure
> * TooACR immagine hello caricato

Spostare toohello Avanti toolearn esercitazione sulla distribuzione di un cluster Kubernetes in Azure.

> [!div class="nextstepaction"]
> [Distribuire un cluster Kubernetes](./container-service-tutorial-kubernetes-deploy-cluster.md).