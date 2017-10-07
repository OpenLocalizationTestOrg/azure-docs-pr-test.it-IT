---
title: esercitazione per il servizio contenitore aaaAzure - preparare App | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - App di preparazione
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="e5270-104">Crea contenitore immagini toobe utilizzato con il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="e5270-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="e5270-105">In questa esercitazione, parte uno di sette, si prepara un'applicazione multi-contenitore per l'uso in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e5270-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="e5270-106">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="e5270-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="e5270-107">Clonazione dell'origine applicazione da GitHub</span><span class="sxs-lookup"><span data-stu-id="e5270-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="e5270-108">Creazione di un'immagine contenitore dall'origine di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e5270-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="e5270-109">Test di un'applicazione hello in un ambiente locale in Docker</span><span class="sxs-lookup"><span data-stu-id="e5270-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="e5270-110">Una volta completato, dopo l'applicazione hello è accessibile in ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="e5270-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="e5270-112">Nelle esercitazioni successive, immagine contenitore hello è caricato tooan del Registro di sistema di Azure contenitore e quindi eseguiti in un Azure ospitati Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="e5270-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e5270-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e5270-113">Before you begin</span></span>

<span data-ttu-id="e5270-114">Questa esercitazione presuppone una conoscenza di base dei concetti principali di Docker, come contenitori, immagini dei contenitore e comandi essenziali.</span><span class="sxs-lookup"><span data-stu-id="e5270-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="e5270-115">Se necessario, vedere [Introduzione a Docker]( https://docs.docker.com/get-started/) per una panoramica sui concetti fondamentali relativi al contenitore.</span><span class="sxs-lookup"><span data-stu-id="e5270-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="e5270-116">toocomplete questa esercitazione, è necessario un ambiente di sviluppo di Docker.</span><span class="sxs-lookup"><span data-stu-id="e5270-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="e5270-117">Docker offre pacchetti che consentono di configurare facilmente Docker in qualsiasi sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="e5270-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="e5270-118">Ottenere il codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e5270-118">Get application code</span></span>

<span data-ttu-id="e5270-119">applicazione di esempio Hello utilizzata in questa esercitazione è un'app di voto base.</span><span class="sxs-lookup"><span data-stu-id="e5270-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="e5270-120">un'applicazione Hello è costituito da un componente front-end web e un'istanza di Redis back-end.</span><span class="sxs-lookup"><span data-stu-id="e5270-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="e5270-121">il componente web Hello viene compresso in un'immagine contenitore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e5270-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="e5270-122">istanza di Redis Hello utilizza un'immagine dall'Hub Docker non modificata.</span><span class="sxs-lookup"><span data-stu-id="e5270-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="e5270-123">Usare git toodownload una copia dell'ambiente di sviluppo tooyour applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="e5270-124">Un creato in precedenza Docker compose di file e un file manifesto Kubernetes interno hello clonato directory è codice sorgente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="e5270-125">Questi file sono utilizzati toocreate asset nel set di esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="e5270-126">Creare immagini del contenitore</span><span class="sxs-lookup"><span data-stu-id="e5270-126">Create container images</span></span>

<span data-ttu-id="e5270-127">[Docker Compose](https://docs.docker.com/compose/) può essere utilizzato tooautomate hello compilazione fuori immagini contenitore e la distribuzione di hello di applicazioni multi-contenitore.</span><span class="sxs-lookup"><span data-stu-id="e5270-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="e5270-128">Eseguire l'immagine di docker compose.yml file toocreate hello contenitore hello, hello download Redis immagine e avviare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="e5270-129">Al termine, utilizzare hello [immagini docker](https://docs.docker.com/engine/reference/commandline/images/) comando immagini hello creato toosee.</span><span class="sxs-lookup"><span data-stu-id="e5270-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="e5270-130">Si noti che sono state scaricate o create tre immagini.</span><span class="sxs-lookup"><span data-stu-id="e5270-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="e5270-131">Hello *azure voto-anteriore* immagine contiene un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="e5270-132">È stata derivata da hello *nginx pallone* immagine.</span><span class="sxs-lookup"><span data-stu-id="e5270-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="e5270-133">immagine di Redis Hello è stato scaricato dall'Hub Docker.</span><span class="sxs-lookup"><span data-stu-id="e5270-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="e5270-134">Eseguire hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) comando toosee hello contenitori in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e5270-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="e5270-135">Output:</span><span class="sxs-lookup"><span data-stu-id="e5270-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="e5270-136">Testare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="e5270-136">Test application locally</span></span>

<span data-ttu-id="e5270-137">Sfoglia toohttp://localhost:8080 toosee hello in esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5270-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="e5270-139">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="e5270-139">Clean up resources</span></span>

<span data-ttu-id="e5270-140">Ora che la funzionalità dell'applicazione è stata convalidata, hello contenitori in esecuzione può essere arrestato e rimosso.</span><span class="sxs-lookup"><span data-stu-id="e5270-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="e5270-141">Non eliminare le immagini contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-141">Do not delete hello container images.</span></span> <span data-ttu-id="e5270-142">Hello *azure voto-anteriore* immagine è l'istanza del Registro di sistema di Azure contenitore tooan caricato nella prossima esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="e5270-143">Eseguire hello seguente hello toostop contenitori in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e5270-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="e5270-144">Eliminare i contenitori di hello arrestato con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e5270-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="e5270-145">Al termine, si dispone di un'immagine contenitore che contiene un'applicazione hello Azure voto.</span><span class="sxs-lookup"><span data-stu-id="e5270-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5270-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5270-146">Next steps</span></span>

<span data-ttu-id="e5270-147">In questa esercitazione, un'applicazione è stata testata e le immagini contenitore creato per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5270-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="e5270-148">sono stata completata Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e5270-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e5270-149">La clonazione di origine dell'applicazione hello da GitHub</span><span class="sxs-lookup"><span data-stu-id="e5270-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="e5270-150">Creazione di un'immagine del contenitore dall'origine applicazione</span><span class="sxs-lookup"><span data-stu-id="e5270-150">Created a container image from application source</span></span>
> * <span data-ttu-id="e5270-151">Applicazione hello testata in un ambiente locale in Docker</span><span class="sxs-lookup"><span data-stu-id="e5270-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="e5270-152">Spostare toohello Avanti toolearn esercitazione sull'archiviazione di immagini contenitore in un registro di sistema di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5270-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5270-153">Push tooAzure immagini contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="e5270-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
