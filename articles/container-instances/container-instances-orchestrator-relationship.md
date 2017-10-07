---
title: Istanze di contenitori aaaAzure e orchestrazione contenitore
description: Informazioni sull'interazione tra Istanze di contenitore di Azure e gli agenti di orchestrazione dei contenitori
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
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="1e15c-103">Istanze di contenitore di Azure e agenti di orchestrazione dei contenitori</span><span class="sxs-lookup"><span data-stu-id="1e15c-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="1e15c-104">Grazie alle dimensioni ridotte e all'orientamento alle applicazioni, i contenitori sono particolarmente adatti per ambienti di recapito flessibili e architetture basate su microservizi.</span><span class="sxs-lookup"><span data-stu-id="1e15c-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="1e15c-105">Hello attività di automazione e gestione di un numero elevato di contenitori e l'interazione è detta *orchestrazione*.</span><span class="sxs-lookup"><span data-stu-id="1e15c-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="1e15c-106">Orchestrators contenitore più diffusi includono Kubernetes, controller di dominio/OS e Docker Swarm, ognuno dei quali sono disponibili in hello [servizio contenitore di Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="1e15c-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="1e15c-107">Istanze di contenitore di Azure fornisce alcune funzionalità delle piattaforme di orchestrazione di programmazione base hello, ma non copre servizi di valore più alto di hello forniscano tali piattaforme e possono infatti essere complementare con essi.</span><span class="sxs-lookup"><span data-stu-id="1e15c-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="1e15c-108">Questo articolo descrive l'ambito di hello di ciò che gestisce le istanze di contenitore di Azure e il livello di riempimento orchestrators contenitore potrebbe interagire con esso.</span><span class="sxs-lookup"><span data-stu-id="1e15c-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="1e15c-109">Orchestrazione tradizionale</span><span class="sxs-lookup"><span data-stu-id="1e15c-109">Traditional orchestration</span></span>

<span data-ttu-id="1e15c-110">definizione di standard Hello dell'orchestrazione include hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="1e15c-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="1e15c-111">**Pianificazione**: data una richiesta di risorse e di un'immagine contenitore, trovare una macchina adatta per il contenitore di hello toorun.</span><span class="sxs-lookup"><span data-stu-id="1e15c-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="1e15c-112">**Affinità/Antiaffinità**: specificare che i contenitori di un set devono essere eseguiti vicini tra loro (per le prestazioni) o sufficientemente distanti tra loro (disponibilità).</span><span class="sxs-lookup"><span data-stu-id="1e15c-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="1e15c-113">**Monitoraggio dell'integrità**: monitorare gli errori dei contenitori e modificare automaticamente la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1e15c-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="1e15c-114">**Failover**: tenere traccia dei quali è in esecuzione in ogni computer e riprogrammare i contenitori da nodi toohealthy macchine non riuscita.</span><span class="sxs-lookup"><span data-stu-id="1e15c-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="1e15c-115">**Scalabilità**: aggiungere o rimuovere richiesta toomatch istanze di contenitore, automaticamente o manualmente.</span><span class="sxs-lookup"><span data-stu-id="1e15c-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="1e15c-116">**Rete**: fornire una rete di sovrapposizione per il coordinamento di contenitori toocommunicate tra più computer host.</span><span class="sxs-lookup"><span data-stu-id="1e15c-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="1e15c-117">**Individuazione del servizio**: abilitare contenitori toolocate loro automaticamente anche come che si spostano tra computer host e modificare gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="1e15c-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="1e15c-118">**Coordinare gli aggiornamenti dell'applicazione**: gestire l'applicazione contenitore di tooavoid aggiornamenti tempi di inattività e abilitare il rollback in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="1e15c-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="1e15c-119">Orchestrazione con Istanze di contenitore di Azure: un approccio a più livelli</span><span class="sxs-lookup"><span data-stu-id="1e15c-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="1e15c-120">Istanze di contenitore di Azure fornisce tooorchestration un approccio a più livelli, tutta la programmazione hello e funzionalità di gestione richiesti toorun un singolo contenitore, consentendo allo stesso orchestrator attività di contenitore a più piattaforme toomanage su di esso.</span><span class="sxs-lookup"><span data-stu-id="1e15c-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="1e15c-121">Poiché tutti hello sottostante l'infrastruttura per le istanze del contenitore è gestito da Azure, una piattaforma di orchestrator non è necessario tooconcern stessa con la ricerca di una macchina host appropriato nel quale toorun un singolo contenitore.</span><span class="sxs-lookup"><span data-stu-id="1e15c-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="1e15c-122">l'elasticità del cloud hello Hello garantisce che uno è sempre disponibile.</span><span class="sxs-lookup"><span data-stu-id="1e15c-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="1e15c-123">Al contrario, orchestrator hello può concentrarsi sulle attività hello che semplificano lo sviluppo di hello di architetture multi-contenitore, tra cui l'adattamento e coordinare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="1e15c-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="1e15c-124">Potenziali scenari</span><span class="sxs-lookup"><span data-stu-id="1e15c-124">Potential scenarios</span></span>

<span data-ttu-id="1e15c-125">Anche se l'integrazione degli agenti di orchestrazione con Istanze di contenitore di Azure è ancora agli inizi, si prevede che possano emergere alcuni ambienti diversi:</span><span class="sxs-lookup"><span data-stu-id="1e15c-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="1e15c-126">Orchestrazione di Istanze di contenitore in modo esclusivo</span><span class="sxs-lookup"><span data-stu-id="1e15c-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="1e15c-127">Poiché l'avvio rapido e fatturare da hello in secondo luogo, un ambiente basato esclusivamente su istanze di contenitori di Azure offre avviato tooget modo più rapido hello e toodeal con carichi di lavoro estremamente variabile.</span><span class="sxs-lookup"><span data-stu-id="1e15c-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="1e15c-128">Combinazione di Istanze di contenitore e contenitori in macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1e15c-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="1e15c-129">Per l'esecuzione prolungata, carichi di lavoro stabile, l'orchestrazione di contenitori in un cluster di macchine virtuali dedicate corrisponderà in genere più economiche rispetto all'esecuzione hello stessi contenitori con istanze di contenitori.</span><span class="sxs-lookup"><span data-stu-id="1e15c-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="1e15c-130">Tuttavia, istanze di contenitori offrono un'ottima soluzione per rapidamente espansione e la toodeal capacità globale con imprevisti o di breve durati picchi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="1e15c-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="1e15c-131">Invece di scalabilità orizzontale numero hello di macchine virtuali del cluster, quindi la distribuzione di altri contenitori in tali computer, orchestrator hello può semplicemente pianificare altri contenitori hello utilizzando istanze di contenitori ed eliminarli quando non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="1e15c-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="1e15c-132">Implementazione di esempio: connettore di Istanze di contenitore di Azure per Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1e15c-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="1e15c-133">toodemonstrate come piattaforme di orchestrazione contenitore è possono integrare con istanze di contenitori di Azure, abbiamo iniziato compilazione un [connettore di esempio per Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="1e15c-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="1e15c-134">Hello connettore per Kubernetes riproduce hello [kubelet] [ kubelet-doc] registrando come nodo con capacità di un numero illimitata e invio di creazione di hello di [POD] [ pod-doc] come gruppi contenitore in istanze di contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e15c-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="1e15c-135">I connettori per altri orchestrators può essere implementati in modo analogo è integrato con piattaforma primitive toocombine hello potenza orchestrator hello API con velocità hello e semplicità di gestione dei contenitori di istanze di contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e15c-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="1e15c-136">Hello connettore ACI per Kubernetes è *sperimentale* e non deve essere utilizzato nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1e15c-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e15c-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e15c-137">Next steps</span></span>

<span data-ttu-id="1e15c-138">Creare il primo contenitore con le istanze di contenitore di Azure utilizzando hello [Guida introduttiva](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="1e15c-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/