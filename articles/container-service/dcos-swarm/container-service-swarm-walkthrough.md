---
title: aaaQuickstart - cluster Azure Docker Swarm per Linux | Documenti Microsoft
description: Consente di capire velocemente toocreate un cluster di Docker Swarm per i contenitori di Linux nel servizio contenitore di Azure con hello CLI di Azure.
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a>Distribuire un cluster Docker Swarm

In questa Guida introduttiva viene distribuito un cluster di Docker Swarm utilizzando hello CLI di Azure. Un'applicazione multi-contenitore composta da front-end web e un'istanza di Redis viene quindi distribuita e in esecuzione nel cluster hello. Una volta completato, un'applicazione hello è accessibile tramite internet hello.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

Questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westus* percorso.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Output:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Creare un cluster Docker Swarm

Creare un cluster di Docker Swarm contenitore nel servizio di Azure con hello [az acs creare](/cli/azure/acs#create) comando. 

esempio Hello crea un cluster denominato *mySwarmCluster* con uno Linux master nodo e i tre nodi di agente di Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

Dopo alcuni minuti, il comando hello completa e restituisce informazioni in formato json sul cluster di hello.

## <a name="connect-toohello-cluster"></a>Connettere il cluster toohello

In tutta questa Guida introduttiva, è necessario l'indirizzo IP di hello del master Docker Swarm hello e pool di agenti di hello Docker. Comando che segue hello esecuzione tooreturn entrambi gli indirizzi IP.


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

Output:

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

Creare un SSH master sciame toohello di tunnel. Sostituire `IPAddress` con indirizzo IP hello master sciame hello.

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

Set hello `DOCKER_HOST` variabile di ambiente. Ciò consente di comandi di docker toorun su Docker Swarm hello senza nome hello toospecify dell'host hello.

```bash
export DOCKER_HOST=:2375
```

Sono ora pronti toorun Docker servizi hello Docker Swarm.


## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Creare un file denominato `docker-compose.yaml` e hello copia seguendo il contenuto al suo interno.

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Eseguire hello comando toocreate hello Azure voto servizio.

```bash
docker-compose up -d
```

Output:

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a>Testare l'applicazione hello

Individuare l'indirizzo IP toohello del hello sciame agente pool tootest all'applicazione Azure voto hello.

![Immagine di esplorazione tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Eliminare il cluster
Quando il cluster hello non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi gruppo di risorse hello tooremove, il servizio contenitore e tutte le relative risorse.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Ottenere il codice hello

In questa Guida introduttiva, le immagini contenitore creato in precedenza sono stati utilizzati toocreate un servizio Docker. Hello correlati codice dell'applicazione, Dockerfile e Scrivi file sono disponibili su GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Passaggi successivi

In questa Guida introduttiva è distribuito un cluster di Docker Swarm e distribuito un tooit applicazione multi-contenitore.

toolearn sull'integrazione di Docker warm con Visual Studio Team Services, continuare toohello CI/CD con Docker Swarm e Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Integrazione continua e distribuzione continua con Docker Swarm e VSTS](./container-service-docker-swarm-setup-ci-cd.md)