---
title: 'Guida introduttiva: cluster Docker Swarm di Azure per Linux | Microsoft Docs'
description: Informazioni per creare rapidamente un cluster Docker Swarm per contenitori Linux nel servizio contenitore di Azure con l'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: 1d10c347795227ed056a95d1bcd4aff82af7b876
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="8ff54-103">Distribuire un cluster Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="8ff54-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="8ff54-104">In questa guida introduttiva viene distribuito un cluster Docker Swarm usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ff54-104">In this quick start, a Docker Swarm cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="8ff54-105">Un'applicazione multicontenitore costituita dal front-end Web e da un'istanza di Redis viene quindi distribuita ed eseguita nel cluster.</span><span class="sxs-lookup"><span data-stu-id="8ff54-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="8ff54-106">Al termine, l'applicazione è accessibile tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="8ff54-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="8ff54-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="8ff54-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="8ff54-108">Questa guida introduttiva richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8ff54-108">This quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8ff54-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="8ff54-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="8ff54-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8ff54-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="8ff54-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8ff54-111">Create a resource group</span></span>

<span data-ttu-id="8ff54-112">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8ff54-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8ff54-113">Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="8ff54-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="8ff54-114">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *westus*.</span><span class="sxs-lookup"><span data-stu-id="8ff54-114">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="8ff54-115">Output:</span><span class="sxs-lookup"><span data-stu-id="8ff54-115">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="8ff54-116">Creare un cluster Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="8ff54-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="8ff54-117">Creare un cluster Docker Swarm nel servizio contenitore di Azure con il comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="8ff54-117">Create a Docker Swarm cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="8ff54-118">L'esempio seguente crea un cluster denominato *mySwarmCluster* con un nodo master Linux e tre nodi agente Linux.</span><span class="sxs-lookup"><span data-stu-id="8ff54-118">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="8ff54-119">Dopo alcuni minuti, il comando viene completato e restituisce le informazioni in formato json sul cluster.</span><span class="sxs-lookup"><span data-stu-id="8ff54-119">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="8ff54-120">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="8ff54-120">Connect to the cluster</span></span>

<span data-ttu-id="8ff54-121">Nel corso di questa guida introduttiva è necessario l'indirizzo IP sia del master Docker Swarm che del pool di agenti Docker.</span><span class="sxs-lookup"><span data-stu-id="8ff54-121">Throughout this quick start, you need the IP address of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="8ff54-122">Usare il comando seguente per restituire entrambi gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="8ff54-122">Run the following command to return both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="8ff54-123">Output:</span><span class="sxs-lookup"><span data-stu-id="8ff54-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="8ff54-124">Creare un tunnel SSH per il master Swarm.</span><span class="sxs-lookup"><span data-stu-id="8ff54-124">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="8ff54-125">Sostituire `IPAddress` con l'indirizzo IP del master Swarm.</span><span class="sxs-lookup"><span data-stu-id="8ff54-125">Replace `IPAddress` with the IP address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="8ff54-126">Impostare la variabile di ambiente `DOCKER_HOST`.</span><span class="sxs-lookup"><span data-stu-id="8ff54-126">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="8ff54-127">In questo modo è possibile eseguire comandi di Docker su Docker Swarm senza dover specificare il nome dell'host.</span><span class="sxs-lookup"><span data-stu-id="8ff54-127">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="8ff54-128">È ora possibile eseguire servizi Docker in Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="8ff54-128">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="8ff54-129">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8ff54-129">Run the application</span></span>

<span data-ttu-id="8ff54-130">Creare un file denominato `docker-compose.yaml` e copiarvi il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="8ff54-130">Create a file named `docker-compose.yaml` and copy the following content into it.</span></span>

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

<span data-ttu-id="8ff54-131">Eseguire il comando seguente per creare il servizio Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="8ff54-131">Run the following command to create the Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="8ff54-132">Output:</span><span class="sxs-lookup"><span data-stu-id="8ff54-132">Output:</span></span>

```bash
Creating network "user_default" with the default driver
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

## <a name="test-the-application"></a><span data-ttu-id="8ff54-133">Test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8ff54-133">Test the application</span></span>

<span data-ttu-id="8ff54-134">Passare all'indirizzo IP del pool di agenti Swarm per testare l'applicazione Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="8ff54-134">Browse to the IP address of the Swarm agent pool to test out the Azure Vote application.</span></span>

![Immagine del passaggio ad Azure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="8ff54-136">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="8ff54-136">Delete cluster</span></span>
<span data-ttu-id="8ff54-137">Quando il cluster non è più necessario, è possibile usare il comando [az group delete](/cli/azure/group#delete) per rimuovere il gruppo di risorse, il servizio contenitore e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="8ff54-137">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="8ff54-138">Ottenere il codice</span><span class="sxs-lookup"><span data-stu-id="8ff54-138">Get the code</span></span>

<span data-ttu-id="8ff54-139">In questa guida introduttiva sono state usate immagini del contenitore già create per creare un servizio Docker.</span><span class="sxs-lookup"><span data-stu-id="8ff54-139">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="8ff54-140">Il codice dell'applicazione correlato, Dockerfile, e il file Compose sono disponibili in GitHub.</span><span class="sxs-lookup"><span data-stu-id="8ff54-140">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="8ff54-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="8ff54-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="8ff54-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ff54-142">Next steps</span></span>

<span data-ttu-id="8ff54-143">In questa guida introduttiva è stato distribuito un cluster Docker Swarm in cui è stata quindi distribuita un'applicazione multicontenitore.</span><span class="sxs-lookup"><span data-stu-id="8ff54-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="8ff54-144">Per informazioni sull'integrazione di Docker Swarm con Visual Studio Team Services, vedere l'articolo relativo a integrazione e distribuzione continua con Docker Swarm e VSTS.</span><span class="sxs-lookup"><span data-stu-id="8ff54-144">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ff54-145">Integrazione continua e distribuzione continua con Docker Swarm e VSTS</span><span class="sxs-lookup"><span data-stu-id="8ff54-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)