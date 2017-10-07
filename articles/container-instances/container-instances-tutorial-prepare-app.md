---
title: esercitazione per istanze di contenitori - aaaAzure preparazione dell'app | Documenti di Azure
description: Preparare un'applicazione per la distribuzione tooAzure istanze di contenitori
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="88e21-103">Creare il contenitore per la distribuzione tooAzure istanze di contenitori</span><span class="sxs-lookup"><span data-stu-id="88e21-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="88e21-104">Istanze di contenitore di Azure consente la distribuzione di contenitori Docker nell'infrastruttura di Azure senza effettuare il provisioning di macchine virtuali o adottare servizi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="88e21-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="88e21-105">In questa esercitazione si compilerà una semplice applicazione Web in Node.js e si creerà un pacchetto in un contenitore che può essere eseguito usando Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="88e21-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="88e21-106">Verranno illustrati gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="88e21-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88e21-107">Clonazione dell'origine applicazione da GitHub</span><span class="sxs-lookup"><span data-stu-id="88e21-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="88e21-108">Creazione di immagini del contenitore dall'origine applicazione</span><span class="sxs-lookup"><span data-stu-id="88e21-108">Creating container images from application source</span></span>
> * <span data-ttu-id="88e21-109">Test delle immagini di hello in un ambiente locale in Docker</span><span class="sxs-lookup"><span data-stu-id="88e21-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="88e21-110">Nelle esercitazioni successive, è caricare il tooan immagine del Registro di sistema di Azure contenitore e quindi distribuirli tooAzure istanze di contenitori.</span><span class="sxs-lookup"><span data-stu-id="88e21-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="88e21-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="88e21-111">Before you begin</span></span>

<span data-ttu-id="88e21-112">Questa esercitazione presuppone una conoscenza di base dei concetti principali di Docker, come contenitori, immagini dei contenitore e comandi essenziali.</span><span class="sxs-lookup"><span data-stu-id="88e21-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="88e21-113">Se necessario, vedere [Introduzione a Docker]( https://docs.docker.com/get-started/) per una panoramica sui concetti fondamentali relativi al contenitore.</span><span class="sxs-lookup"><span data-stu-id="88e21-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="88e21-114">toocomplete questa esercitazione, è necessario un ambiente di sviluppo di Docker.</span><span class="sxs-lookup"><span data-stu-id="88e21-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="88e21-115">Docker offre pacchetti che consentono di configurare facilmente Docker in qualsiasi sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="88e21-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="88e21-116">Ottenere il codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="88e21-116">Get application code</span></span>

<span data-ttu-id="88e21-117">esempio Hello in questa esercitazione include una semplice applicazione web incorporata [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="88e21-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="88e21-118">applicazione Hello serve di una pagina HTML statica e simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="88e21-118">hello app serves a static HTML page and looks like this:</span></span>

![App dell'esercitazione visualizzata in un browser][aci-tutorial-app]

<span data-ttu-id="88e21-120">Usare git toodownload hello-esempio:</span><span class="sxs-lookup"><span data-stu-id="88e21-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="88e21-121">Crea immagine del contenitore hello</span><span class="sxs-lookup"><span data-stu-id="88e21-121">Build hello container image</span></span>

<span data-ttu-id="88e21-122">Hello Dockerfile fornito nel repository di esempio hello viene illustrata la modalità di compilazione contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="88e21-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="88e21-123">Viene avviato da un [ufficiale immagine Node.js] [ dockerhub-nodeimage] in base a [Linux Alpine](https://alpinelinux.org/), una distribuzione di piccole dimensioni che è adatto toouse con i contenitori.</span><span class="sxs-lookup"><span data-stu-id="88e21-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="88e21-124">Viene quindi copia i file dell'applicazione hello in un contenitore di hello, installa le dipendenze tramite Gestione pacchetti di nodi hello e infine viene avviata un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="88e21-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="88e21-125">Hello utilizzare `docker build` comando toocreate hello immagine contenitore come tag *aci-esercitazione-app*:</span><span class="sxs-lookup"><span data-stu-id="88e21-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="88e21-126">Hello utilizzare `docker images` immagine hello compilato toosee:</span><span class="sxs-lookup"><span data-stu-id="88e21-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="88e21-127">Output:</span><span class="sxs-lookup"><span data-stu-id="88e21-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="88e21-128">Eseguire il contenitore di hello in locale</span><span class="sxs-lookup"><span data-stu-id="88e21-128">Run hello container locally</span></span>

<span data-ttu-id="88e21-129">Prima di tentare la distribuzione di hello contenitore tooAzure istanze di contenitori, eseguirla localmente tooconfirm del corretto funzionamento.</span><span class="sxs-lookup"><span data-stu-id="88e21-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="88e21-130">Hello `-d` switch consente contenitore hello eseguito in background hello, mentre `-p` consente toomap una porta arbitraria del tooport calcolo 80 nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="88e21-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="88e21-131">Aprire hello browser toohttp://localhost:8080 tooconfirm che hello contenitore è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="88e21-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![App di hello in esecuzione in locale nel browser hello][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="88e21-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88e21-133">Next steps</span></span>

<span data-ttu-id="88e21-134">In questa esercitazione, è stato creato un'immagine contenitore che può essere distribuito tooAzure istanze di contenitori.</span><span class="sxs-lookup"><span data-stu-id="88e21-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="88e21-135">sono stata completata Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="88e21-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88e21-136">La clonazione di origine dell'applicazione hello da GitHub</span><span class="sxs-lookup"><span data-stu-id="88e21-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="88e21-137">Creazione di immagini del contenitore dall'origine applicazione</span><span class="sxs-lookup"><span data-stu-id="88e21-137">Creating container images from application source</span></span>
> * <span data-ttu-id="88e21-138">Contenitore di hello di test in locale</span><span class="sxs-lookup"><span data-stu-id="88e21-138">Testing hello container locally</span></span>

<span data-ttu-id="88e21-139">Spostare toohello Avanti toolearn esercitazione sull'archiviazione di immagini contenitore in un registro di sistema di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="88e21-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="88e21-140">Push tooAzure immagini contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="88e21-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png