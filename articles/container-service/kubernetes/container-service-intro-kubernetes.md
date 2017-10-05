---
title: Introduzione al servizio contenitore di Azure per Kubernetes | Microsoft Docs
description: Il servizio contenitore di Azure per Kubernetes semplifica la distribuzione e la gestione delle applicazioni basate su contenitori in Azure.
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, contenitori, microservizi, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: 92cdbe20e7a2974a734dfed5294c547866050290
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-azure-container-service-for-kubernetes"></a><span data-ttu-id="55cc7-104">Introduzione al servizio contenitore di Azure per Kubernetes</span><span class="sxs-lookup"><span data-stu-id="55cc7-104">Introduction to Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="55cc7-105">Il servizio contenitore di Azure per Kubernetes semplifica la creazione, la configurazione e la gestione di un cluster di macchine virtuali preconfigurate per eseguire le applicazioni nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="55cc7-105">Azure Container Service for Kubernetes makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="55cc7-106">Ciò consente di usare le competenze già acquisite o di attingere da un consistente e crescente bagaglio di competenze a livello di community per distribuire e gestire applicazioni basate sul contenitore in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="55cc7-106">This enables you to use your existing skills, or draw upon a large and growing body of community expertise, to deploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="55cc7-107">Il servizio contenitore di Azure consente di sfruttare i vantaggi delle funzionalità di livello aziendale di Azure mantenendo al tempo stesso la portabilità delle applicazioni tramite Kubernetes e il formato immagine Docker.</span><span class="sxs-lookup"><span data-stu-id="55cc7-107">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and the Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="55cc7-108">Uso del servizio contenitore di Azure per Kubernetes</span><span class="sxs-lookup"><span data-stu-id="55cc7-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="55cc7-109">L'obiettivo del servizio contenitore di Azure è fornire un ambiente host contenitore tramite tecnologie e strumenti open source, che sono attualmente diffusi fra i nostri clienti.</span><span class="sxs-lookup"><span data-stu-id="55cc7-109">Our goal with Azure Container Service is to provide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="55cc7-110">A questo scopo vengono esposti gli endpoint API di Kubernetes standard.</span><span class="sxs-lookup"><span data-stu-id="55cc7-110">To this end, we expose the standard Kubernetes API endpoints.</span></span> <span data-ttu-id="55cc7-111">Usando questi endpoint standard è possibile usare qualsiasi software riesca a comunicare con un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="55cc7-111">By using these standard endpoints, you can leverage any software that is capable of talking to a Kubernetes cluster.</span></span> <span data-ttu-id="55cc7-112">È ad esempio possibile scegliere [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) o [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="55cc7-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="55cc7-113">Creazione di un cluster Kubernetes con il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="55cc7-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="55cc7-114">Per iniziare a usare il servizio contenitore di Azure, distribuire un cluster del servizio contenitore di Azure con l'[interfaccia della riga di comando di Azure 2.0](container-service-kubernetes-walkthrough.md) o tramite il portale (cercare **Servizio contenitore di Azure** nel Marketplace).</span><span class="sxs-lookup"><span data-stu-id="55cc7-114">To begin using Azure Container Service, deploy an Azure Container Service cluster with the [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via the portal (search the Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="55cc7-115">Gli utenti avanzati che hanno bisogno di un maggiore controllo sui modelli di Azure Resource Manager possono usare il progetto open source [acs-engine](https://github.com/Azure/acs-engine) per compilare un cluster Kubernetes personalizzato e distribuirlo tramite l'interfaccia della riga di comando `az`.</span><span class="sxs-lookup"><span data-stu-id="55cc7-115">If you are an advanced user who needs more control over the Azure Resource Manager templates, you can use the open source [acs-engine](https://github.com/Azure/acs-engine) project to build your own custom Kubernetes cluster and deploy it via the `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="55cc7-116">Uso di Kubernetes</span><span class="sxs-lookup"><span data-stu-id="55cc7-116">Using Kubernetes</span></span>
<span data-ttu-id="55cc7-117">Kubernetes automatizza la distribuzione, il ridimensionamento e la gestione delle applicazioni nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="55cc7-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="55cc7-118">Dispone di un set completo di funzionalità tra cui:</span><span class="sxs-lookup"><span data-stu-id="55cc7-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="55cc7-119">Bin packing automatico</span><span class="sxs-lookup"><span data-stu-id="55cc7-119">Automatic binpacking</span></span>
* <span data-ttu-id="55cc7-120">Riparazione automatica</span><span class="sxs-lookup"><span data-stu-id="55cc7-120">Self-healing</span></span>
* <span data-ttu-id="55cc7-121">Scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="55cc7-121">Horizontal scaling</span></span>
* <span data-ttu-id="55cc7-122">Bilanciamento del carico e rilevamento del servizio</span><span class="sxs-lookup"><span data-stu-id="55cc7-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="55cc7-123">Implementazioni e ripristini dello stato precedente automatizzati</span><span class="sxs-lookup"><span data-stu-id="55cc7-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="55cc7-124">Gestione della configurazione e dei segreti</span><span class="sxs-lookup"><span data-stu-id="55cc7-124">Secret and configuration management</span></span>
* <span data-ttu-id="55cc7-125">Orchestrazione dell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="55cc7-125">Storage orchestration</span></span>
* <span data-ttu-id="55cc7-126">Esecuzione batch</span><span class="sxs-lookup"><span data-stu-id="55cc7-126">Batch execution</span></span>

<span data-ttu-id="55cc7-127">Diagramma dell'architettura di Kubernetes distribuito tramite il servizio contenitore di Azure:</span><span class="sxs-lookup"><span data-stu-id="55cc7-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Servizio contenitore di Azure configurato per l'uso di Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="55cc7-129">Video</span><span class="sxs-lookup"><span data-stu-id="55cc7-129">Videos</span></span>

<span data-ttu-id="55cc7-130">Il supporto per Kubernetes nei servizi contenitore di Azure (Azure Friday, gennaio 2017):</span><span class="sxs-lookup"><span data-stu-id="55cc7-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="55cc7-131">Strumenti per lo sviluppo e la distribuzione di applicazioni in Kubernetes (Azure OpenDev, giugno 2017):</span><span class="sxs-lookup"><span data-stu-id="55cc7-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="55cc7-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55cc7-132">Next steps</span></span>

<span data-ttu-id="55cc7-133">Vedere la [guida introduttiva a Kubernetes](container-service-kubernetes-walkthrough.md) per iniziare a conoscere oggi stesso il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="55cc7-133">Explore the [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) to begin exploring Azure Container Service today.</span></span>