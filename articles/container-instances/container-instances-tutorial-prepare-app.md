---
title: Esercitazione su Istanze di contenitore di Azure - Preparare l'app | Azure Docs
description: Preparare un'app per la distribuzione in Istanze di contenitore di Azure
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
ms.openlocfilehash: 167297e10eed11833623ff797e676ad43c65f9ad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-container-for-deployment-to-azure-container-instances"></a><span data-ttu-id="28f1f-103">Creare un contenitore per la distribuzione in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="28f1f-103">Create container for deployment to Azure Container Instances</span></span>

<span data-ttu-id="28f1f-104">Istanze di contenitore di Azure consente la distribuzione di contenitori Docker nell'infrastruttura di Azure senza effettuare il provisioning di macchine virtuali o adottare servizi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="28f1f-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="28f1f-105">In questa esercitazione si compilerà una semplice applicazione Web in Node.js e si creerà un pacchetto in un contenitore che può essere eseguito usando Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="28f1f-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="28f1f-106">Verranno illustrati gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="28f1f-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28f1f-107">Clonazione dell'origine applicazione da GitHub</span><span class="sxs-lookup"><span data-stu-id="28f1f-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="28f1f-108">Creazione di immagini del contenitore dall'origine applicazione</span><span class="sxs-lookup"><span data-stu-id="28f1f-108">Creating container images from application source</span></span>
> * <span data-ttu-id="28f1f-109">Test delle immagini in un ambiente Docker locale</span><span class="sxs-lookup"><span data-stu-id="28f1f-109">Testing the images in a local Docker environment</span></span>

<span data-ttu-id="28f1f-110">Nelle esercitazioni successive si caricherà l'immagine in un Registro contenitori di Azure e quindi la si distribuirà in Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="28f1f-110">In subsequent tutorials, you will upload your image to an Azure Container Registry, and then deploy them to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28f1f-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="28f1f-111">Before you begin</span></span>

<span data-ttu-id="28f1f-112">Questa esercitazione presuppone una conoscenza di base dei concetti principali di Docker, come contenitori, immagini dei contenitore e comandi essenziali.</span><span class="sxs-lookup"><span data-stu-id="28f1f-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="28f1f-113">Se necessario, vedere [Introduzione a Docker]( https://docs.docker.com/get-started/) per una panoramica sui concetti fondamentali relativi al contenitore.</span><span class="sxs-lookup"><span data-stu-id="28f1f-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="28f1f-114">Per completare questa esercitazione è necessario un ambiente di sviluppo Docker.</span><span class="sxs-lookup"><span data-stu-id="28f1f-114">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="28f1f-115">Docker offre pacchetti che consentono di configurare facilmente Docker in qualsiasi sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) o [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="28f1f-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="28f1f-116">Ottenere il codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="28f1f-116">Get application code</span></span>

<span data-ttu-id="28f1f-117">L'esempio in questa esercitazione include una semplice applicazione Web compilata in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="28f1f-117">The sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="28f1f-118">L'app gestisce una pagina HTML statica ed è simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="28f1f-118">The app serves a static HTML page and looks like this:</span></span>

![App dell'esercitazione visualizzata in un browser][aci-tutorial-app]

<span data-ttu-id="28f1f-120">Usare Git per scaricare l'esempio:</span><span class="sxs-lookup"><span data-stu-id="28f1f-120">Use git to download the sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-the-container-image"></a><span data-ttu-id="28f1f-121">Compilare l'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="28f1f-121">Build the container image</span></span>

<span data-ttu-id="28f1f-122">Il documento Dockerfile fornito nel repository di esempio illustra come viene compilato il contenitore.</span><span class="sxs-lookup"><span data-stu-id="28f1f-122">The Dockerfile provided in the sample repo shows how the container is built.</span></span> <span data-ttu-id="28f1f-123">Viene avviato da un'[immagine Node.js ufficiale][dockerhub-nodeimage] basata su [Alpine Linux](https://alpinelinux.org/), una distribuzione di piccole dimensioni particolarmente adatta per l'uso con i contenitori.</span><span class="sxs-lookup"><span data-stu-id="28f1f-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited to use with containers.</span></span> <span data-ttu-id="28f1f-124">Copia quindi i file dell'applicazione nel contenitore, installa le dipendenze usando Gestione pacchetti del nodo e infine avvia l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="28f1f-124">It then copies the application files into the container, installs dependencies using the Node Package Manager, and finally starts the application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="28f1f-125">Usare il comando `docker build` per creare l'immagine del contenitore, assegnandole il tag *aci-tutorial-app*:</span><span class="sxs-lookup"><span data-stu-id="28f1f-125">Use the `docker build` command to create the container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="28f1f-126">Usare `docker images` per visualizzare l'immagine compilata:</span><span class="sxs-lookup"><span data-stu-id="28f1f-126">Use the `docker images` to see the built image:</span></span>

```bash
docker images
```

<span data-ttu-id="28f1f-127">Output:</span><span class="sxs-lookup"><span data-stu-id="28f1f-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-the-container-locally"></a><span data-ttu-id="28f1f-128">Eseguire il contenitore in locale</span><span class="sxs-lookup"><span data-stu-id="28f1f-128">Run the container locally</span></span>

<span data-ttu-id="28f1f-129">Prima di provare a distribuire il contenitore in Istanze di contenitore di Azure, eseguirlo in locale per verificarne il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="28f1f-129">Before you try deploying the container to Azure Container Instances, run it locally to confirm that it works.</span></span> <span data-ttu-id="28f1f-130">L'opzione `-d` consente di eseguire il contenitore in background, mentre `-p` consente di eseguire il mapping di una porta arbitraria del computer alla porta 80 del contenitore.</span><span class="sxs-lookup"><span data-stu-id="28f1f-130">The `-d` switch lets the container run in the background, while `-p` allows you to map an arbitrary port on your compute to port 80 in the container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="28f1f-131">Aprire il browser all'indirizzo http://localhost:8080 per verificare che il contenitore sia un esecuzione.</span><span class="sxs-lookup"><span data-stu-id="28f1f-131">Open the browser to http://localhost:8080 to confirm that the container is running.</span></span>

![Esecuzione locale dell'app nel browser][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="28f1f-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28f1f-133">Next steps</span></span>

<span data-ttu-id="28f1f-134">In questa esercitazione è stata creata un'immagine del contenitore che può essere distribuita in Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="28f1f-134">In this tutorial, you created a container image that can be deployed to Azure Container Instances.</span></span> <span data-ttu-id="28f1f-135">Sono stati completati i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="28f1f-135">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28f1f-136">Clonazione dell'origine applicazione da GitHub</span><span class="sxs-lookup"><span data-stu-id="28f1f-136">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="28f1f-137">Creazione di immagini del contenitore dall'origine applicazione</span><span class="sxs-lookup"><span data-stu-id="28f1f-137">Creating container images from application source</span></span>
> * <span data-ttu-id="28f1f-138">Test del contenitore in locale</span><span class="sxs-lookup"><span data-stu-id="28f1f-138">Testing the container locally</span></span>

<span data-ttu-id="28f1f-139">Passare alla prossima esercitazione per apprendere informazioni sull'archiviazione delle immagini del contenitore in un Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="28f1f-139">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="28f1f-140">Eseguire il push delle immagini nel Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="28f1f-140">Push images to Azure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png