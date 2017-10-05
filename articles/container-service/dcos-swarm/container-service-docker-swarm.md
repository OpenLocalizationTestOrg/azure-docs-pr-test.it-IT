---
title: Gestire un cluster Azure Swarm con l'API Docker | Documentazione Microsoft
description: Distribuire contenitori in un cluster Docker Swarm nel servizio contenitore di Azure
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 6ca2d2e49c4b7f5eb0580e7091b09209f8b73a7c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="983da-104">Gestione dei contenitori con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="983da-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="983da-105">Docker Swarm offre un ambiente per la distribuzione di carichi di lavoro in contenitori in un set di host Docker in pool.</span><span class="sxs-lookup"><span data-stu-id="983da-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="983da-106">Docker Swarm usa l'API Docker nativa.</span><span class="sxs-lookup"><span data-stu-id="983da-106">Docker Swarm uses the native Docker API.</span></span> <span data-ttu-id="983da-107">Il flusso di lavoro per la gestione dei contenitori in Docker Swarm è quasi identico a quello di un host con un singolo contenitore.</span><span class="sxs-lookup"><span data-stu-id="983da-107">The workflow for managing containers on a Docker Swarm is almost identical to what it would be on a single container host.</span></span> <span data-ttu-id="983da-108">Questo documento fornisce semplici esempi di distribuzione di carichi di lavoro in contenitori, in un'istanza del servizio contenitore di Azure di Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="983da-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="983da-109">Per una documentazione più dettagliata su Docker Swarm, vedere [Docker Swarm in Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="983da-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="983da-110">Prerequisiti per gli esercizi in questo documento:</span><span class="sxs-lookup"><span data-stu-id="983da-110">Prerequisites to the exercises in this document:</span></span>

[<span data-ttu-id="983da-111">Creare un cluster Swarm nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="983da-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="983da-112">Connettersi a un cluster Swarm nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="983da-112">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="983da-113">Distribuire un nuovo contenitore</span><span class="sxs-lookup"><span data-stu-id="983da-113">Deploy a new container</span></span>
<span data-ttu-id="983da-114">Per creare un nuovo contenitore in Docker Swarm, usare il comando `docker run` , assicurandosi di avere aperto un tunnel SSH per i master, in base ai prerequisiti riportati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="983da-114">To create a new container in the Docker Swarm, use the `docker run` command (ensuring that you have opened an SSH tunnel to the masters as per the prerequisites above).</span></span> <span data-ttu-id="983da-115">Questo esempio consente di creare un contenitore dall'immagine `yeasy/simple-web` :</span><span class="sxs-lookup"><span data-stu-id="983da-115">This example creates a container from the `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="983da-116">Dopo aver creato il contenitore, usare `docker ps` per restituire informazioni sul contenitore.</span><span class="sxs-lookup"><span data-stu-id="983da-116">After the container has been created, use `docker ps` to return information about the container.</span></span> <span data-ttu-id="983da-117">Viene elencato l'agente Swarm che ospita il contenitore:</span><span class="sxs-lookup"><span data-stu-id="983da-117">Notice here that the Swarm agent that is hosting the container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="983da-118">Ora è possibile accedere all'applicazione in esecuzione in questo contenitore tramite il nome DNS pubblico del servizio di bilanciamento del carico dell'agente Swarm.</span><span class="sxs-lookup"><span data-stu-id="983da-118">You can now access the application that is running in this container through the public DNS name of the Swarm agent load balancer.</span></span> <span data-ttu-id="983da-119">Queste informazioni sono disponibili nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="983da-119">You can find this information in the Azure portal:</span></span>  

![Risultati della visita reali](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="983da-121">Per impostazione predefinita, le porte 80, 8080 e 443 sono aperte per il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="983da-121">By default the Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="983da-122">Se ci si vuole connettere su un'altra porta, sarà necessario aprire la porta in Azure Load Balancer per il pool di agenti.</span><span class="sxs-lookup"><span data-stu-id="983da-122">If you want to connect on another port you will need to open that port on the Azure Load Balancer for the Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="983da-123">Distribuire più contenitori</span><span class="sxs-lookup"><span data-stu-id="983da-123">Deploy multiple containers</span></span>
<span data-ttu-id="983da-124">Poiché vengono avviati più contenitori, eseguendo più volte il comando 'docker run', è possibile usare il comando `docker ps` per visualizzare gli host in cui sono in esecuzione i contenitori.</span><span class="sxs-lookup"><span data-stu-id="983da-124">As multiple containers are started, by executing 'docker run' multiple times, you can use the `docker ps` command to see which hosts the containers are running on.</span></span> <span data-ttu-id="983da-125">Nell'esempio seguente tre contenitori sono distribuiti uniformemente nei tre agenti Swarm:</span><span class="sxs-lookup"><span data-stu-id="983da-125">In the example below, three containers are spread evenly across the three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="983da-126">Distribuire contenitori con Docker Compose</span><span class="sxs-lookup"><span data-stu-id="983da-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="983da-127">È possibile usare Docker Compose per l'automazione della distribuzione e la configurazione di più contenitori.</span><span class="sxs-lookup"><span data-stu-id="983da-127">You can use Docker Compose to automate the deployment and configuration of multiple containers.</span></span> <span data-ttu-id="983da-128">A questo scopo, assicurarsi che sia stato creato un tunnel SSH (Secure Shell) e che sia stata impostata la variabile DOCKER_HOST (vedere i prerequisiti riportati in precedenza).</span><span class="sxs-lookup"><span data-stu-id="983da-128">To do so, ensure that a Secure Shell (SSH) tunnel has been created and that the DOCKER_HOST variable has been set (see the pre-requisites above).</span></span>

<span data-ttu-id="983da-129">Creare un file docker-compose.yml nel sistema locale.</span><span class="sxs-lookup"><span data-stu-id="983da-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="983da-130">A questo scopo, usare questo [esempio](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="983da-130">To do this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="983da-131">Eseguire `docker-compose up -d` per avviare le distribuzioni dei contenitori:</span><span class="sxs-lookup"><span data-stu-id="983da-131">Run `docker-compose up -d` to start the container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="983da-132">Infine, verrà restituito l'elenco dei contenitori in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="983da-132">Finally, the list of running containers will be returned.</span></span> <span data-ttu-id="983da-133">Questo elenco riflette i contenitori distribuiti con Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="983da-133">This list reflects the containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="983da-134">È ovviamente possibile usare `docker-compose ps` per esaminare solo i contenitori definiti nel file `compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="983da-134">Naturally, you can use `docker-compose ps` to examine only the containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="983da-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="983da-135">Next steps</span></span>
[<span data-ttu-id="983da-136">Altre informazioni su Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="983da-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

