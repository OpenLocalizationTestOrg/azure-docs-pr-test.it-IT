---
title: Gruppi di contenitori in Istanze di contenitore di Azure
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
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="d81a9-103">Gruppi di contenitori in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="d81a9-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="d81a9-104">La risorsa di livello principale in Istanze di contenitore di Azure consiste in un gruppo di contenitori.</span><span class="sxs-lookup"><span data-stu-id="d81a9-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="d81a9-105">Questo articolo descrive le caratteristiche dei gruppi di contenitori e i tipi di scenari possibili.</span><span class="sxs-lookup"><span data-stu-id="d81a9-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="d81a9-106">Come funziona un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="d81a9-106">How a container group works</span></span>

<span data-ttu-id="d81a9-107">Un gruppo di contenitori è una raccolta di contenitori che vengono pianificati nello stesso computer host e condividono un ciclo di vita, una rete locale e i volumi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d81a9-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="d81a9-108">Il concetto è simile a quello di *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) e [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="d81a9-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="d81a9-109">Il diagramma seguente mostra un esempio di un gruppo che include più contenitori.</span><span class="sxs-lookup"><span data-stu-id="d81a9-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![Esempio di un gruppo di contenitori][container-groups-example]

<span data-ttu-id="d81a9-111">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="d81a9-111">Note that:</span></span>

- <span data-ttu-id="d81a9-112">Il gruppo è pianificato su un singolo computer host.</span><span class="sxs-lookup"><span data-stu-id="d81a9-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="d81a9-113">Il gruppo espone un singolo indirizzo IP pubblico, con una sola porta esposta.</span><span class="sxs-lookup"><span data-stu-id="d81a9-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="d81a9-114">Il gruppo è costituito da due contenitori.</span><span class="sxs-lookup"><span data-stu-id="d81a9-114">The group is made up of two containers.</span></span> <span data-ttu-id="d81a9-115">Un contenitore è in ascolto sulla porta 80, mentre l'altro è in ascolto sulla porta 5000.</span><span class="sxs-lookup"><span data-stu-id="d81a9-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="d81a9-116">Il gruppo include due condivisioni file di Azure come punti di montaggio di volume e ogni contenitore monta una delle due condivisioni in locale.</span><span class="sxs-lookup"><span data-stu-id="d81a9-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="d81a9-117">Rete</span><span class="sxs-lookup"><span data-stu-id="d81a9-117">Networking</span></span>

<span data-ttu-id="d81a9-118">I gruppi di contenitori condividono un indirizzo IP e uno spazio dei nomi di porta su tale indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="d81a9-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="d81a9-119">Per consentire a client esterni di raggiungere un contenitore all'interno del gruppo, è necessario esporre la porta sull'indirizzo IP e dal contenitore.</span><span class="sxs-lookup"><span data-stu-id="d81a9-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="d81a9-120">Poiché i contenitori all'interno del gruppo condividono uno spazio dei nomi di porta, il mapping delle porte non è supportato.</span><span class="sxs-lookup"><span data-stu-id="d81a9-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="d81a9-121">I contenitori all'interno di un gruppo possono raggiungersi tramite localhost sulle porte che hanno esposto, anche se queste porte non sono esposte esternamente sull'indirizzo IP del gruppo.</span><span class="sxs-lookup"><span data-stu-id="d81a9-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="d81a9-122">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="d81a9-122">Storage</span></span>

<span data-ttu-id="d81a9-123">È possibile impostare il montaggio di volumi esterni all'interno di un gruppo di contenitori</span><span class="sxs-lookup"><span data-stu-id="d81a9-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="d81a9-124">ed eseguire il mapping di tali volumi in percorsi specifici all'interno dei singoli contenitori di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="d81a9-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="d81a9-125">Scenari comuni</span><span class="sxs-lookup"><span data-stu-id="d81a9-125">Common scenarios</span></span>

<span data-ttu-id="d81a9-126">I gruppi di più contenitori sono utili nei casi in cui si vuole dividere una singola attività funzionale in un numero ridotto di immagini di contenitore, che possono essere distribuite da team diversi e hanno requisiti separati in termini di risorse.</span><span class="sxs-lookup"><span data-stu-id="d81a9-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="d81a9-127">Un esempio di utilizzo può includere gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d81a9-127">Example usage could include:</span></span>

- <span data-ttu-id="d81a9-128">Un contenitore di applicazione e un contenitore di registrazione.</span><span class="sxs-lookup"><span data-stu-id="d81a9-128">An application container and a logging container.</span></span> <span data-ttu-id="d81a9-129">Il contenitore di registrazione raccoglie l'output dei log e delle metriche generato dall'applicazione principale e lo scrive in una risorsa di archiviazione a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="d81a9-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="d81a9-130">Un contenitore di applicazione e uno di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="d81a9-130">An application and a monitoring container.</span></span> <span data-ttu-id="d81a9-131">Il contenitore di monitoraggio invia periodicamente una richiesta all'applicazione per verificare che sia in esecuzione e risponda correttamente e genera un avviso nel caso in cui la verifica abbia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d81a9-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="d81a9-132">Un contenitore che serve un'applicazione Web e un altro che esegue il pull del contenuto più recente dal controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="d81a9-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d81a9-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d81a9-133">Next steps</span></span>

<span data-ttu-id="d81a9-134">Informazioni su come [distribuire un gruppo di più contenitori](container-instances-multi-container-group.md) con un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d81a9-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png