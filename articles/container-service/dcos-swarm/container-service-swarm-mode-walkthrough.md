---
title: aaaQuickstart - cluster CE Docker di Azure per Linux | Documenti Microsoft
description: Consente di capire velocemente toocreate un cluster di Docker CE per i contenitori di Linux nel servizio contenitore di Azure con hello CLI di Azure.
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Distribuire un cluster Docker CE

In questa Guida introduttiva viene distribuito un cluster di Docker CE usando hello CLI di Azure. Un'applicazione multi-contenitore composta da front-end web e un'istanza di Redis viene quindi distribuita e in esecuzione nel cluster hello. Una volta completato, un'applicazione hello è accessibile tramite internet hello.

Docker CE nel servizio contenitore di Azure è in anteprima e **non deve essere usato per carichi di lavoro di produzione**.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *ukwest* percorso.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
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

Creare un cluster di Docker CE contenitore nel servizio di Azure con hello [az acs creare](/cli/azure/acs#create) comando. 

esempio Hello crea un cluster denominato *mySwarmCluster* con uno Linux master nodo e i tre nodi di agente di Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Dopo alcuni minuti, il comando hello completa e restituisce informazioni in formato json sul cluster di hello.

## <a name="connect-toohello-cluster"></a>Connettere il cluster toohello

In questa Guida introduttiva, è necessario hello FQDN del master Docker Swarm hello e pool di agenti di hello Docker. Eseguire hello tooreturn entrambi hello FQDN master e l'agente di comando seguente.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Output:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Creare un SSH master sciame toohello di tunnel. Sostituire `MasterFQDN` con l'indirizzo FQDN hello master sciame hello.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Set hello `DOCKER_HOST` variabile di ambiente. Ciò consente di comandi di docker toorun su Docker Swarm hello senza nome hello toospecify dell'host hello.

```bash
export DOCKER_HOST=localhost:2374
```

Sono ora pronti toorun Docker servizi hello Docker Swarm.


## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Creare un file denominato `azure-vote.yaml` e hello copia seguendo il contenuto al suo interno.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Eseguire hello [distribuire stack docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) comando del servizio di Azure voto hello toocreate.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Output:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Hello utilizzare [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) comando tooreturn hello stato di distribuzione hello applicazione.

```bash
docker stack ps azure-vote
```

Una volta hello `CURRENT STATE` di ogni servizio è `Running`, un'applicazione hello è pronta.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Testare l'applicazione hello

Sfoglia toohello FQDN di hello sciame agente pool tootest out hello applicazione Azure voto.

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