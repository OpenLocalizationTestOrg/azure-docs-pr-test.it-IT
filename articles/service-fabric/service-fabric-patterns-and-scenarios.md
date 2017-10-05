---
title: Modelli e scenari per Azure Service Fabric | Documentazione Microsoft
description: Informazioni sulle procedure consigliate e collaudate, sui modelli riutilizzabili per progettare, sviluppare e gestire i microservizi in Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: fb2fa495758433e357722427b1c162420935955d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="f07c4-103">Modelli e scenari per Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f07c4-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="f07c4-104">Se si vogliono sviluppare microservizi su larga scala con Azure Service Fabric, può essere utile imparare dagli esperti che hanno progettato questa piattaforma distribuita come servizio (PaaS, Platform as a Service).</span><span class="sxs-lookup"><span data-stu-id="f07c4-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="f07c4-105">Per iniziare occorre scegliere l'architettura appropriata, per poi imparare le procedure per ottimizzare le risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f07c4-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="f07c4-106">Il corso [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) (Modelli e procedure consigliate per Service Fabric) offre le risposte alle domande più frequenti dei clienti reali sugli scenari di utilizzo e le aree applicative di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f07c4-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="f07c4-107">È possibile scoprire come progettare, sviluppare e gestire i microservizi in Service Fabric usando procedure consigliate e modelli collaudati riutilizzabili.</span><span class="sxs-lookup"><span data-stu-id="f07c4-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="f07c4-108">Si può iniziare da una panoramica di Service Fabric per poi procedere con vari argomenti di approfondimento come l'ottimizzazione e la sicurezza del cluster, la migrazione di applicazioni legacy, IoT su vasta scala, l'hosting di motori di gioco e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f07c4-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="f07c4-109">Sono anche disponibili informazioni su come controllare il recapito continuo per diversi carichi di lavoro e dettagli sul supporto di Linux e i contenitori.</span><span class="sxs-lookup"><span data-stu-id="f07c4-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="f07c4-110">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f07c4-110">Introduction</span></span>
<span data-ttu-id="f07c4-111">Esplorare le procedure consigliate e raccogliere informazioni per la scelta di una piattaforma distribuita come servizio (PaaS, Platform as a Service) o un'infrastruttura distribuita come servizio (IaaS, Infrastructure as a Service).</span><span class="sxs-lookup"><span data-stu-id="f07c4-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="f07c4-112">Informazioni dettagliate sui principi di progettazione delle applicazioni collaudati.</span><span class="sxs-lookup"><span data-stu-id="f07c4-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="f07c4-113">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-113">Video</span></span></th><th><span data-ttu-id="f07c4-114">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f07c4-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduzione a Service Fabric</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="f07c4-116">Pianificazione e gestione del cluster</span><span class="sxs-lookup"><span data-stu-id="f07c4-116">Cluster planning and management</span></span>
<span data-ttu-id="f07c4-117">Questa presentazione di Azure Service Fabric include informazioni sulla pianificazione della capacità, l'ottimizzazione del cluster e la sicurezza del cluster.</span><span class="sxs-lookup"><span data-stu-id="f07c4-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="f07c4-118">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-118">Video</span></span></th><th><span data-ttu-id="f07c4-119">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="f07c4-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Pianificazione e gestione del cluster</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="f07c4-121">Web con iperscalabilità</span><span class="sxs-lookup"><span data-stu-id="f07c4-121">Hyper-scale web</span></span>
<span data-ttu-id="f07c4-122">Una presentazione dei concetti relativi al Web con iperscalabilità, incluse disponibilità e affidabilità, iperscalabilità e gestione dello stato.</span><span class="sxs-lookup"><span data-stu-id="f07c4-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="f07c4-123">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-123">Video</span></span></th><th><span data-ttu-id="f07c4-124">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f07c4-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Web con iperscalabilità</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="f07c4-126">IoT</span><span class="sxs-lookup"><span data-stu-id="f07c4-126">IoT</span></span>
<span data-ttu-id="f07c4-127">Esplorare Internet delle cose (IoT) nel contesto di Azure Service Fabric, inclusi pipeline IoT di Azure, multitenancy e IoT su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="f07c4-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="f07c4-128">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-128">Video</span></span></th><th><span data-ttu-id="f07c4-129">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f07c4-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="f07c4-131">Giochi</span><span class="sxs-lookup"><span data-stu-id="f07c4-131">Gaming</span></span>
<span data-ttu-id="f07c4-132">Informazioni sui giochi a turni, i giochi interattivi e l'hosting di motori di gioco esistenti.</span><span class="sxs-lookup"><span data-stu-id="f07c4-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="f07c4-133">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-133">Video</span></span></th><th><span data-ttu-id="f07c4-134">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f07c4-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Giochi</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="f07c4-136">Recapito continuo</span><span class="sxs-lookup"><span data-stu-id="f07c4-136">Continuous delivery</span></span>
<span data-ttu-id="f07c4-137">Presentazione dei concetti, tra i quali integrazione continua/recapito continuo con Visual Studio Team Services, flusso di lavoro di compilazione/creazione del pacchetto/pubblicazione, programma di installazione per più ambienti e pacchetto del servizio/condivisione.</span><span class="sxs-lookup"><span data-stu-id="f07c4-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="f07c4-138">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-138">Video</span></span></th><th><span data-ttu-id="f07c4-139">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f07c4-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Recapito continuo</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="f07c4-141">Migrazione</span><span class="sxs-lookup"><span data-stu-id="f07c4-141">Migration</span></span>
<span data-ttu-id="f07c4-142">Informazioni sulla migrazione da un servizio cloud, oltre alla migrazione di app legacy.</span><span class="sxs-lookup"><span data-stu-id="f07c4-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="f07c4-143">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-143">Video</span></span></th><th><span data-ttu-id="f07c4-144">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f07c4-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migrazione</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="f07c4-146">Contenitori e supporto di Linux</span><span class="sxs-lookup"><span data-stu-id="f07c4-146">Containers and Linux support</span></span>
<span data-ttu-id="f07c4-147">Ottenere la risposta alla domanda "Perché usare i contenitori?"</span><span class="sxs-lookup"><span data-stu-id="f07c4-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="f07c4-148">Informazioni sull'anteprima per i contenitori di Windows, il supporto di Linux e l'orchestrazione dei contenitori Linux.</span><span class="sxs-lookup"><span data-stu-id="f07c4-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="f07c4-149">Sono disponibili anche indicazioni pratiche per la migrazione di app .NET Core a Linux.</span><span class="sxs-lookup"><span data-stu-id="f07c4-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="f07c4-150">Video</span><span class="sxs-lookup"><span data-stu-id="f07c4-150">Video</span></span></th><th><span data-ttu-id="f07c4-151">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f07c4-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f07c4-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Contenitori e supporto Linux</a></span><span class="sxs-lookup"><span data-stu-id="f07c4-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="f07c4-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f07c4-153">Next steps</span></span>
<span data-ttu-id="f07c4-154">Dopo aver raccolto informazioni dettagliate sui modelli e gli scenari di utilizzo di Service Fabric, è possibile procedere con la lettura e scoprire come [creare e gestire i cluster](service-fabric-deploy-anywhere.md), [eseguire la migrazione delle app di Servizi cloud a Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [configurare il recapito continuo](service-fabric-set-up-continuous-integration.md) e [distribuire i contenitori](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f07c4-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
