---
title: aaaAzure gruppi contenitore di istanze di contenitori
description: Informazioni sul funzionamento di gruppi di contenitori in Istanze di contenitore di Azure
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="0782a-103">Gruppi di contenitori in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="0782a-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="0782a-104">risorsa di primo livello Hello in istanze di contenitori di Azure è un gruppo contenitore.</span><span class="sxs-lookup"><span data-stu-id="0782a-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="0782a-105">Questo articolo descrive le caratteristiche dei gruppi di contenitori e i tipi di scenari possibili.</span><span class="sxs-lookup"><span data-stu-id="0782a-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="0782a-106">Come funziona un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="0782a-106">How a container group works</span></span>

<span data-ttu-id="0782a-107">Un gruppo contenitore è una raccolta di contenitori che ottengano pianificati su hello stesso ospitare macchina e condividere un ciclo di vita, rete locale e i volumi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0782a-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="0782a-108">È simile toohello concetto di un *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) e [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="0782a-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="0782a-109">Hello diagramma seguente viene illustrato un esempio di un gruppo contenitore che include più contenitori.</span><span class="sxs-lookup"><span data-stu-id="0782a-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Esempio di un gruppo di contenitori][container-groups-example]

<span data-ttu-id="0782a-111">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="0782a-111">Note that:</span></span>

- <span data-ttu-id="0782a-112">gruppo Hello viene pianificata su un computer singolo host.</span><span class="sxs-lookup"><span data-stu-id="0782a-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="0782a-113">gruppo Hello espone un singolo indirizzo IP pubblico, con una porta esposto.</span><span class="sxs-lookup"><span data-stu-id="0782a-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="0782a-114">gruppo Hello è costituito da due contenitori.</span><span class="sxs-lookup"><span data-stu-id="0782a-114">hello group is made up of two containers.</span></span> <span data-ttu-id="0782a-115">Un contenitore è in ascolto sulla porta 80, mentre altri hello in ascolto sulla porta 5000.</span><span class="sxs-lookup"><span data-stu-id="0782a-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="0782a-116">gruppo Hello include due condivisioni di file di Azure come volume mount e ogni contenitore Monta una delle condivisioni hello in locale.</span><span class="sxs-lookup"><span data-stu-id="0782a-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="0782a-117">Rete</span><span class="sxs-lookup"><span data-stu-id="0782a-117">Networking</span></span>

<span data-ttu-id="0782a-118">I gruppi di contenitori condividono un indirizzo IP e uno spazio dei nomi di porta su tale indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="0782a-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="0782a-119">tooenable client esterni tooreach un contenitore all'interno di gruppo hello, è necessario esporre la porta hello sull'indirizzo IP hello e dal contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="0782a-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="0782a-120">Poiché i contenitori all'interno di gruppo hello condividono uno spazio dei nomi di porta, il mapping della porta non è supportato.</span><span class="sxs-lookup"><span data-stu-id="0782a-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="0782a-121">Contenitori all'interno di un gruppo possono raggiungere tra loro tramite localhost sul hello le porte che è stata esposta, anche se queste porte non sono esposte esternamente sull'indirizzo IP del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="0782a-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="0782a-122">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="0782a-122">Storage</span></span>

<span data-ttu-id="0782a-123">È possibile specificare toomount volumi esterni all'interno di un gruppo contenitore.</span><span class="sxs-lookup"><span data-stu-id="0782a-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="0782a-124">È possibile eseguire il mapping di tali volumi in percorsi specifici all'interno di contenitori di singoli hello in un gruppo.</span><span class="sxs-lookup"><span data-stu-id="0782a-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="0782a-125">Scenari comuni</span><span class="sxs-lookup"><span data-stu-id="0782a-125">Common scenarios</span></span>

<span data-ttu-id="0782a-126">Contenitori a più gruppi sono utili nei casi in cui si desidera toodivide di una singola attività funzionale in un numero ridotto di immagini contenitore, che possono essere recapitati da team diversi e hanno requisiti di risorse separato.</span><span class="sxs-lookup"><span data-stu-id="0782a-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="0782a-127">Un esempio di utilizzo può includere gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0782a-127">Example usage could include:</span></span>

- <span data-ttu-id="0782a-128">Un contenitore di applicazione e un contenitore di registrazione.</span><span class="sxs-lookup"><span data-stu-id="0782a-128">An application container and a logging container.</span></span> <span data-ttu-id="0782a-129">contenitore di registrazione Hello raccoglie i log di hello e output metriche da principale dell'applicazione hello e li scrive archiviazione toolong termine.</span><span class="sxs-lookup"><span data-stu-id="0782a-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="0782a-130">Un contenitore di applicazione e uno di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="0782a-130">An application and a monitoring container.</span></span> <span data-ttu-id="0782a-131">monitoraggio contenitore periodicamente Hello rende un tooensure applicazione toohello richiesta che è in esecuzione e risponde correttamente e genera un avviso in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="0782a-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="0782a-132">Un contenitore per un'applicazione web e un contenitore di estrarre contenuto più recente di hello dal controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="0782a-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0782a-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0782a-133">Next steps</span></span>

<span data-ttu-id="0782a-134">Informazioni su come troppo[distribuire un gruppo multi-contenitore](container-instances-multi-container-group.md) con un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0782a-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png