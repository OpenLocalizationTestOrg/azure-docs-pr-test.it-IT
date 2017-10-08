---
title: esercitazione per istanze di contenitori aaaAzure - preparare Registro di sistema contenitore di Azure | Documenti Microsoft
description: Esercitazione di Istanze di contenitore di Azure - Preparare Registro contenitori di Azure
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Distribuire e usare il Registro contenitori di Azure

Questa è la parte due di un'esercitazione in tre parti. In hello [passaggio precedente](./container-instances-tutorial-prepare-app.md), un'immagine contenitore è stata creata per un'applicazione web semplice scritta in [Node.js](http://nodejs.org). In questa esercitazione, questa immagine viene inserita tooan del Registro di sistema contenitore di Azure. Se non è stato creato immagine contenitore hello, restituire troppo[esercitazione 1: immagine contenitore crea](./container-instances-tutorial-prepare-app.md). 

Hello del Registro di sistema di Azure contenitore è un registro basato su Azure e privato, per le immagini contenitore Docker. In questa esercitazione vengono illustrati l'implementazione di un'istanza del Registro di sistema di Azure contenitore e inserendo un tooit immagine contenitore. I passaggi completati comprendono:

> [!div class="checklist"]
> * Distribuzione di un'istanza del Registro contenitori di Azure
> * Assegnazione di un tag all'immagine del contenitore per Registro contenitori di Azure
> * Caricamento tooAzure immagine contenitore del Registro di sistema

Nelle esercitazioni successive, distribuire contenitore hello dal tooAzure del Registro di sistema privata istanze di contenitori.

## <a name="before-you-begin"></a>Prima di iniziare

Questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Distribuire il Registro contenitori di Azure

Prima di distribuire un Registro contenitori di Azure, è necessario che esista un gruppo di risorse. Un gruppo di risorse di Azure è una raccolta logica in cui le risorse di Azure vengono distribuite e gestite.

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. In questo esempio, un gruppo di risorse denominato *myResourceGroup* viene creato in hello *eastus* area.

```azurecli
az group create --name myResourceGroup --location eastus
```

Creare un registro di sistema del contenitore di Azure con hello [az acr creare](/cli/azure/acr#create) comando. nome di un contenitore del Registro di sistema di Hello **deve essere univoco**. Nel seguente esempio di hello, utilizziamo nome hello *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

Tutta hello di questa esercitazione, utilizziamo `<acrname>` come segnaposto per nome del Registro di sistema del contenitore hello scelto.

## <a name="container-registry-login"></a>Accesso al registro contenitori

È necessario accedere in istanza ACR tooyour prima push tooit immagini. Hello utilizzare [accesso acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operazione hello toocomplete di comando. È necessario il nome univoco di tooprovide hello assegnato del Registro di sistema di toohello contenitore al momento della creazione.

```azurecli
az acr login --name <acrName>
```

comando Hello restituisce un messaggio 'Accesso riuscito' una volta completato.

## <a name="tag-container-image"></a>Assegnare tag all'immagine del contenitore

toodeploy un'immagine contenitore da un registro di sistema privato, l'immagine di hello deve essere contrassegnato con hello toobe `loginServer` nome del Registro di sistema hello.

un elenco di immagini corrente, utilizzare hello toosee `docker images` comando.

```bash
docker images
```

Output:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

tooget hello loginServer nome eseguire hello comando seguente.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Hello tag *aci-esercitazione-app* immagine con loginServer hello del Registro di sistema di hello contenitore. Inoltre, aggiungere `:v1` toohello fine del nome dell'immagine hello. Questo tag indica numero di versione di hello immagine.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

Una volta contrassegnate, eseguire `docker images` operazione hello tooverify.

```bash
docker images
```

Output:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Push tooAzure immagine contenitore del Registro di sistema

Push hello *aci-esercitazione-app* registro toohello di immagini.

Utilizza hello di esempio seguente, sostituire hello contenitore del Registro di sistema loginServer name con loginServer hello dall'ambiente in uso.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Elencare le immagini in Registro contenitori di Azure

un elenco di immagini che sono stati inseriti tooyour Azure contenitore del Registro di sistema, hello utente tooreturn [elenco repository di az acr](/cli/azure/acr/repository#list) comando. Aggiornare il comando hello con il nome del Registro di sistema di hello contenitore.

```azurecli
az acr repository list --name <acrName> --output table
```

Output:

```azurecli
Result
----------------
aci-tutorial-app
```

Quindi tag hello toosee per un'immagine specifica, utilizzare hello [az acr repository Mostra-tag](/cli/azure/acr/repository#show-tags) comando.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Output:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, un registro di sistema di contenitore di Azure è stata preparata per l'uso con istanze di contenitori di Azure e immagine contenitore hello è stato inserito. sono stata completata Hello alla procedura seguente:

> [!div class="checklist"]
> * Distribuzione di un'istanza del Registro contenitori di Azure
> * Assegnazione di un tag all'immagine del contenitore per Registro contenitori di Azure
> * Caricamento tooAzure immagine contenitore del Registro di sistema

Spostare toohello Avanti toolearn esercitazione sulla distribuzione di hello contenitore tooAzure utilizzando istanze di contenitori di Azure.

> [!div class="nextstepaction"]
> [Distribuire i contenitori tooAzure istanze di contenitori](./container-instances-tutorial-deploy-app.md)
