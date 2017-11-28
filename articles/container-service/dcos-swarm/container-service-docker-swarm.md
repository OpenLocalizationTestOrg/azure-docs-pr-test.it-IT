---
title: Azure Swarm aaaManage cluster con l'API di Docker | Documenti Microsoft
description: Distribuire cluster contenitori Docker Swarm tooa contenitore nel servizio di Azure
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
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="9fb71-104">Gestione dei contenitori con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="9fb71-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="9fb71-105">Docker Swarm offre un ambiente per la distribuzione di carichi di lavoro in contenitori in un set di host Docker in pool.</span><span class="sxs-lookup"><span data-stu-id="9fb71-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="9fb71-106">Docker sciame utilizza API di Docker native hello.</span><span class="sxs-lookup"><span data-stu-id="9fb71-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="9fb71-107">flusso di lavoro di Hello per la gestione dei contenitori in un Docker Swarm è quasi identica toowhat che sarebbe in un singolo host contenitore.</span><span class="sxs-lookup"><span data-stu-id="9fb71-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="9fb71-108">Questo documento fornisce semplici esempi di distribuzione di carichi di lavoro in contenitori, in un'istanza del servizio contenitore di Azure di Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="9fb71-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="9fb71-109">Per una documentazione più dettagliata su Docker Swarm, vedere [Docker Swarm in Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="9fb71-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="9fb71-110">Prerequisiti toohello gli esercizi di questo documento:</span><span class="sxs-lookup"><span data-stu-id="9fb71-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="9fb71-111">Creare un cluster Swarm nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="9fb71-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="9fb71-112">Connettersi con cluster sciame hello contenitore nel servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="9fb71-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="9fb71-113">Distribuire un nuovo contenitore</span><span class="sxs-lookup"><span data-stu-id="9fb71-113">Deploy a new container</span></span>
<span data-ttu-id="9fb71-114">un nuovo contenitore di hello Docker Swarm, toocreate utilizzare hello `docker run` comando (assicurandosi che è stato aperto un master di toohello tunnel SSH in base ai prerequisiti hello sopra).</span><span class="sxs-lookup"><span data-stu-id="9fb71-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="9fb71-115">In questo esempio crea un contenitore da hello `yeasy/simple-web` immagine:</span><span class="sxs-lookup"><span data-stu-id="9fb71-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="9fb71-116">Dopo aver creato il contenitore di hello, utilizzare `docker ps` tooreturn informazioni contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="9fb71-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="9fb71-117">Notare che l'agente sciame hello host contenitore hello è elencato:</span><span class="sxs-lookup"><span data-stu-id="9fb71-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="9fb71-118">È ora possibile accedere a un'applicazione hello che è in esecuzione in questo contenitore tramite nome DNS pubblico hello di bilanciamento del carico di hello sciame agente.</span><span class="sxs-lookup"><span data-stu-id="9fb71-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="9fb71-119">È possibile trovare queste informazioni nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="9fb71-119">You can find this information in hello Azure portal:</span></span>  

![Risultati della visita reali](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="9fb71-121">Per impostazione predefinita hello bilanciamento del carico con porte 80, aperta 8080 e 443.</span><span class="sxs-lookup"><span data-stu-id="9fb71-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="9fb71-122">Se si desidera tooconnect su un'altra porta occorre tooopen tale porta in hello bilanciamento del carico di Azure per hello Pool di agenti.</span><span class="sxs-lookup"><span data-stu-id="9fb71-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="9fb71-123">Distribuire più contenitori</span><span class="sxs-lookup"><span data-stu-id="9fb71-123">Deploy multiple containers</span></span>
<span data-ttu-id="9fb71-124">Più contenitori vengono avviati, tramite l'esecuzione di 'docker run' più volte, è possibile utilizzare hello `docker ps` toosee comando che ospita i contenitori di hello eseguono.</span><span class="sxs-lookup"><span data-stu-id="9fb71-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="9fb71-125">Nell'esempio hello seguente, tre contenitori vengono distribuiti uniformemente tra tre agenti di sciame hello:</span><span class="sxs-lookup"><span data-stu-id="9fb71-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="9fb71-126">Distribuire contenitori con Docker Compose</span><span class="sxs-lookup"><span data-stu-id="9fb71-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="9fb71-127">È possibile utilizzare Docker Compose tooautomate hello distribuzione e configurazione di più contenitori.</span><span class="sxs-lookup"><span data-stu-id="9fb71-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="9fb71-128">toodo in tal caso, verificare che è stato creato un tunnel SSH (Secure Shell) e che è stata impostata la variabile DOCKER_HOST hello (vedere hello i prerequisiti sopra).</span><span class="sxs-lookup"><span data-stu-id="9fb71-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="9fb71-129">Creare un file docker-compose.yml nel sistema locale.</span><span class="sxs-lookup"><span data-stu-id="9fb71-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="9fb71-130">toodo, utilizzare questo [esempio](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="9fb71-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

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

<span data-ttu-id="9fb71-131">Eseguire `docker-compose up -d` toostart le distribuzioni di contenitori hello:</span><span class="sxs-lookup"><span data-stu-id="9fb71-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

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

<span data-ttu-id="9fb71-132">Infine, verrà restituito hello elenco di contenitori in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9fb71-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="9fb71-133">Questo elenco contiene contenitori hello che sono stati distribuiti tramite Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="9fb71-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="9fb71-134">Naturalmente, è possibile utilizzare `docker-compose ps` tooexamine hello solo contenitori definiti nel `compose.yml` file.</span><span class="sxs-lookup"><span data-stu-id="9fb71-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fb71-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9fb71-135">Next steps</span></span>
[<span data-ttu-id="9fb71-136">Altre informazioni su Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="9fb71-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

