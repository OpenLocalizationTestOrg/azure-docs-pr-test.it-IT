---
title: aaaIntroduction tooAzure servizio contenitore per Kubernetes | Documenti Microsoft
description: Servizio di contenitore di Azure per Kubernetes rende semplice toodeploy e gestire applicazioni basate sul contenitore in Azure.
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
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="00d56-104">Introduzione tooAzure servizio contenitore per Kubernetes</span><span class="sxs-lookup"><span data-stu-id="00d56-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="00d56-105">Servizio di contenitore di Azure per Kubernetes rende semplice toocreate, configurare e gestire un cluster di macchine virtuali che sono preconfigurati toorun contenitore applicazioni.</span><span class="sxs-lookup"><span data-stu-id="00d56-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="00d56-106">Questo consente di toouse le competenze esistenti, o disegnare su un corpo di grandi dimensioni e in continua crescito di esperienza della community, toodeploy e gestire le applicazioni basate sul contenitore in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="00d56-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="00d56-107">Tramite il servizio contenitore di Azure, è possibile sfruttare i vantaggi di hello funzionalità aziendale di Azure, mantenendo al tempo stesso la portabilità dell'applicazione tramite Kubernetes e hello formato immagine Docker.</span><span class="sxs-lookup"><span data-stu-id="00d56-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="00d56-108">Uso del servizio contenitore di Azure per Kubernetes</span><span class="sxs-lookup"><span data-stu-id="00d56-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="00d56-109">L'obiettivo di Microsoft con il servizio contenitore di Azure è tooprovide un ambiente host del contenitore tramite strumenti open source e tecnologie che sono comuni tra i clienti oggi.</span><span class="sxs-lookup"><span data-stu-id="00d56-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="00d56-110">toothis fine, è necessario esporre gli endpoint dell'API di Kubernetes standard hello.</span><span class="sxs-lookup"><span data-stu-id="00d56-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="00d56-111">Tramite questi endpoint standard, è possibile utilizzare qualsiasi software che è in grado di comunicare tooa Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="00d56-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="00d56-112">È ad esempio possibile scegliere [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) o [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="00d56-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="00d56-113">Creazione di un cluster Kubernetes con il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="00d56-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="00d56-114">toobegin utilizzando servizio contenitore di Azure, distribuire un cluster il servizio contenitore di Azure con hello [CLI di Azure 2.0](container-service-kubernetes-walkthrough.md) o tramite il portale di hello (hello ricerca Marketplace per **servizio contenitore di Azure**).</span><span class="sxs-lookup"><span data-stu-id="00d56-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="00d56-115">Nel caso di un utente avanzato che necessita di maggiore controllo sui modelli di hello Azure Resource Manager, è possibile utilizzare open source di hello [acs motore](https://github.com/Azure/acs-engine) toobuild di progetto personalizzati Kubernetes personalizzato del cluster e distribuirlo tramite hello `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="00d56-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="00d56-116">Uso di Kubernetes</span><span class="sxs-lookup"><span data-stu-id="00d56-116">Using Kubernetes</span></span>
<span data-ttu-id="00d56-117">Kubernetes automatizza la distribuzione, il ridimensionamento e la gestione delle applicazioni nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="00d56-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="00d56-118">Dispone di un set completo di funzionalità tra cui:</span><span class="sxs-lookup"><span data-stu-id="00d56-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="00d56-119">Bin packing automatico</span><span class="sxs-lookup"><span data-stu-id="00d56-119">Automatic binpacking</span></span>
* <span data-ttu-id="00d56-120">Riparazione automatica</span><span class="sxs-lookup"><span data-stu-id="00d56-120">Self-healing</span></span>
* <span data-ttu-id="00d56-121">Scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="00d56-121">Horizontal scaling</span></span>
* <span data-ttu-id="00d56-122">Bilanciamento del carico e rilevamento del servizio</span><span class="sxs-lookup"><span data-stu-id="00d56-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="00d56-123">Implementazioni e ripristini dello stato precedente automatizzati</span><span class="sxs-lookup"><span data-stu-id="00d56-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="00d56-124">Gestione della configurazione e dei segreti</span><span class="sxs-lookup"><span data-stu-id="00d56-124">Secret and configuration management</span></span>
* <span data-ttu-id="00d56-125">Orchestrazione dell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="00d56-125">Storage orchestration</span></span>
* <span data-ttu-id="00d56-126">Esecuzione batch</span><span class="sxs-lookup"><span data-stu-id="00d56-126">Batch execution</span></span>

<span data-ttu-id="00d56-127">Diagramma dell'architettura di Kubernetes distribuito tramite il servizio contenitore di Azure:</span><span class="sxs-lookup"><span data-stu-id="00d56-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Il servizio contenitore di Azure configurato toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="00d56-129">Video</span><span class="sxs-lookup"><span data-stu-id="00d56-129">Videos</span></span>

<span data-ttu-id="00d56-130">Il supporto per Kubernetes nei servizi contenitore di Azure (Azure Friday, gennaio 2017):</span><span class="sxs-lookup"><span data-stu-id="00d56-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="00d56-131">Strumenti per lo sviluppo e la distribuzione di applicazioni in Kubernetes (Azure OpenDev, giugno 2017):</span><span class="sxs-lookup"><span data-stu-id="00d56-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="00d56-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00d56-132">Next steps</span></span>

<span data-ttu-id="00d56-133">Esplorare hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin esplorazione oggi servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="00d56-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
