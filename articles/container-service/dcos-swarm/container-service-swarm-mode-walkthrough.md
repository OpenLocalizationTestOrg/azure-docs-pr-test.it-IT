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
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="764cd-103">Distribuire un cluster Docker CE</span><span class="sxs-lookup"><span data-stu-id="764cd-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="764cd-104">In questa Guida introduttiva viene distribuito un cluster di Docker CE usando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="764cd-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="764cd-105">Un'applicazione multi-contenitore composta da front-end web e un'istanza di Redis viene quindi distribuita e in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="764cd-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="764cd-106">Una volta completato, un'applicazione hello è accessibile tramite internet hello.</span><span class="sxs-lookup"><span data-stu-id="764cd-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="764cd-107">Docker CE nel servizio contenitore di Azure è in anteprima e **non deve essere usato per carichi di lavoro di produzione**.</span><span class="sxs-lookup"><span data-stu-id="764cd-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="764cd-108">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="764cd-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="764cd-109">Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="764cd-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="764cd-110">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="764cd-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="764cd-111">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="764cd-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="764cd-112">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="764cd-112">Create a resource group</span></span>

<span data-ttu-id="764cd-113">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="764cd-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="764cd-114">Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="764cd-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="764cd-115">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *ukwest* percorso.</span><span class="sxs-lookup"><span data-stu-id="764cd-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="764cd-116">Output:</span><span class="sxs-lookup"><span data-stu-id="764cd-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="764cd-117">Creare un cluster Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="764cd-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="764cd-118">Creare un cluster di Docker CE contenitore nel servizio di Azure con hello [az acs creare](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="764cd-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="764cd-119">esempio Hello crea un cluster denominato *mySwarmCluster* con uno Linux master nodo e i tre nodi di agente di Linux.</span><span class="sxs-lookup"><span data-stu-id="764cd-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="764cd-120">Dopo alcuni minuti, il comando hello completa e restituisce informazioni in formato json sul cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="764cd-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="764cd-121">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="764cd-121">Connect toohello cluster</span></span>

<span data-ttu-id="764cd-122">In questa Guida introduttiva, è necessario hello FQDN del master Docker Swarm hello e pool di agenti di hello Docker.</span><span class="sxs-lookup"><span data-stu-id="764cd-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="764cd-123">Eseguire hello tooreturn entrambi hello FQDN master e l'agente di comando seguente.</span><span class="sxs-lookup"><span data-stu-id="764cd-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="764cd-124">Output:</span><span class="sxs-lookup"><span data-stu-id="764cd-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="764cd-125">Creare un SSH master sciame toohello di tunnel.</span><span class="sxs-lookup"><span data-stu-id="764cd-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="764cd-126">Sostituire `MasterFQDN` con l'indirizzo FQDN hello master sciame hello.</span><span class="sxs-lookup"><span data-stu-id="764cd-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="764cd-127">Set hello `DOCKER_HOST` variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="764cd-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="764cd-128">Ciò consente di comandi di docker toorun su Docker Swarm hello senza nome hello toospecify dell'host hello.</span><span class="sxs-lookup"><span data-stu-id="764cd-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="764cd-129">Sono ora pronti toorun Docker servizi hello Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="764cd-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="764cd-130">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="764cd-130">Run hello application</span></span>

<span data-ttu-id="764cd-131">Creare un file denominato `azure-vote.yaml` e hello copia seguendo il contenuto al suo interno.</span><span class="sxs-lookup"><span data-stu-id="764cd-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


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

<span data-ttu-id="764cd-132">Eseguire hello [distribuire stack docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) comando del servizio di Azure voto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="764cd-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="764cd-133">Output:</span><span class="sxs-lookup"><span data-stu-id="764cd-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="764cd-134">Hello utilizzare [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) comando tooreturn hello stato di distribuzione hello applicazione.</span><span class="sxs-lookup"><span data-stu-id="764cd-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="764cd-135">Una volta hello `CURRENT STATE` di ogni servizio è `Running`, un'applicazione hello è pronta.</span><span class="sxs-lookup"><span data-stu-id="764cd-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="764cd-136">Testare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="764cd-136">Test hello application</span></span>

<span data-ttu-id="764cd-137">Sfoglia toohello FQDN di hello sciame agente pool tootest out hello applicazione Azure voto.</span><span class="sxs-lookup"><span data-stu-id="764cd-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Immagine di esplorazione tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="764cd-139">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="764cd-139">Delete cluster</span></span>
<span data-ttu-id="764cd-140">Quando il cluster hello non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi gruppo di risorse hello tooremove, il servizio contenitore e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="764cd-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="764cd-141">Ottenere il codice hello</span><span class="sxs-lookup"><span data-stu-id="764cd-141">Get hello code</span></span>

<span data-ttu-id="764cd-142">In questa Guida introduttiva, le immagini contenitore creato in precedenza sono stati utilizzati toocreate un servizio Docker.</span><span class="sxs-lookup"><span data-stu-id="764cd-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="764cd-143">Hello correlati codice dell'applicazione, Dockerfile e Scrivi file sono disponibili su GitHub.</span><span class="sxs-lookup"><span data-stu-id="764cd-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="764cd-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="764cd-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="764cd-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="764cd-145">Next steps</span></span>

<span data-ttu-id="764cd-146">In questa Guida introduttiva è distribuito un cluster di Docker Swarm e distribuito un tooit applicazione multi-contenitore.</span><span class="sxs-lookup"><span data-stu-id="764cd-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="764cd-147">toolearn sull'integrazione di Docker warm con Visual Studio Team Services, continuare toohello CI/CD con Docker Swarm e Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="764cd-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="764cd-148">Integrazione continua e distribuzione continua con Docker Swarm e VSTS</span><span class="sxs-lookup"><span data-stu-id="764cd-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)