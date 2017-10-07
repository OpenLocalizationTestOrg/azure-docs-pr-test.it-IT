---
title: esercitazione per il servizio contenitore aaaAzure - l'applicazione di aggiornamento | Documenti Microsoft
description: Esercitazione per il servizio contenitore di Azure - Aggiornare un'applicazione
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Aggiornare un'applicazione in Kubernetes

Dopo aver distribuito un'applicazione in Kubernetes, è possibile aggiornarla specificando una nuova immagine del contenitore o una nuova versione dell'immagine. Quando si aggiorna un'applicazione, implementazione di update hello viene gestita in modo che solo una parte della distribuzione hello verrà aggiornata contemporaneamente. Questo aggiornamento per la gestione temporanea consente tookeep applicazione hello in esecuzione durante l'aggiornamento di hello e fornisce un meccanismo di rollback se si verifica un errore di distribuzione. 

In questa esercitazione, parte 6 di sette, app di Azure voto esempio hello viene aggiornato. Le attività da completare comprendono:

> [!div class="checklist"]
> * Aggiornamento del codice dell'applicazione front-end hello
> * Creazione di un'immagine del contenitore aggiornata
> * Push hello contenitore immagine tooAzure contenitore del Registro di sistema
> * Distribuzione immagine contenitore aggiornato hello

Nelle esercitazioni successive, Operations Management Suite è cluster Kubernetes di hello toomonitor configurato.

## <a name="before-you-begin"></a>Prima di iniziare

Nelle esercitazioni precedenti, un'applicazione è stata distribuita in un'immagine contenitore, immagine hello caricato tooAzure contenitore del Registro di sistema e un cluster Kubernetes creato. un'applicazione Hello quindi è stata eseguita nel cluster Kubernetes hello. 

Se non sono state completate le operazioni di toofollow lungo, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Aggiornare l'applicazione

passaggi di hello toocomplete in questa esercitazione, deve avere una copia clonata di hello applicazione Azure voto. Se necessario, creare la copia clonata con hello comando seguente:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Aprire hello `config_file.cfg` file con qualsiasi editor di testo o codice. È possibile trovare questo file nella seguente directory di repository clonato hello hello.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Modificare i valori hello per `VOTE1VALUE` e `VOTE2VALUE`e quindi salvare il file hello.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Utilizzare [comporre docker](https://docs.docker.com/compose/) toore-creare immagine front-end hello e un'applicazione hello esecuzione aggiornato.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Testare l'applicazione in locale

Sfoglia troppo`http://localhost:8080` toosee hello applicazione aggiornata.

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Applicare tag ed eseguire il push delle immagini

Hello tag *azure voto-anteriore* immagine con loginServer hello del Registro di sistema di hello contenitore.

Se si usa Azure del Registro di sistema contenitore, ottenere il nome di server di accesso di hello con hello [elenco acr az](/cli/azure/acr#list) comando.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Utilizzare [tag docker](https://docs.docker.com/engine/reference/commandline/tag/) immagine hello tootag. Sostituire `<acrLoginServer>` con il nome di accesso del server del Registro contenitori di Azure o un nome host di un registro pubblico.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Utilizzare [push di docker](https://docs.docker.com/engine/reference/commandline/push/) Registro di sistema tooupload hello immagine tooyour. Sostituire `<acrLoginServer>` con il nome di accesso del server del Registro contenitori di Azure o un nome host di un registro pubblico.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Distribuire l'aggiornamento dell'applicazione

tempi tooensure più istanze di pod applicazione hello devono essere in esecuzione. Verificare la configurazione con hello [kubectl ottenere pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```bash
kubectl get pod
```

Output:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Se non si dispone di più POD che esegue l'immagine di azure-anteriore voto hello, applicare la scalabilità hello *azure voto-anteriore* distribuzione.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

un'applicazione hello tooupdate, utilizzare hello [set kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) comando. Aggiornamento `<acrLoginServer>` con hello account di accesso server o il nome host contenitore del Registro di sistema.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

distribuzione di hello toomonitor, utilizzare hello [kubectl ottenere pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando. Come un'applicazione hello aggiornato viene distribuita, le unità vengono terminate e ricreato con nuova immagine contenitore di hello.

```azurecli-interactive
kubectl get pod
```

Output:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Testare l'applicazione aggiornata

Ottenere l'indirizzo IP esterno hello di hello *azure voto-anteriore* servizio.

```azurecli-interactive
kubectl get service azure-vote-front
```

Sfoglia toohello IP indirizzo toosee hello applicazione aggiornata.

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, si aggiornata un'applicazione e il cluster di aggiornamento tooa Kubernetes di implementazione. sono stata completata Hello seguenti attività:

> [!div class="checklist"]
> * Codice dell'applicazione front-end hello aggiornato
> * Creazione di un'immagine del contenitore aggiornata
> * Inserito hello contenitore immagine tooAzure contenitore del Registro di sistema
> * Applicazione distribuita hello aggiornato

Toohello Avanti toolearn esercitazione su come spostare toomonitor Kubernetes con Operations Management Suite.

> [!div class="nextstepaction"]
> [Monitorare Kubernetes con OMS](./container-service-tutorial-kubernetes-monitor.md)