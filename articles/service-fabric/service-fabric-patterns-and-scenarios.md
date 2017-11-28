---
title: aaaAzure Service Fabric modelli e gli scenari | Documenti Microsoft
description: Informazioni sulle procedure consigliate e dimostrato, toodesign modelli riutilizzabili, sviluppare e utilizzare il microservizi nell'infrastruttura del servizio.
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
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="f2374-103">Modelli e scenari per Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f2374-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="f2374-104">Se si sta consultando la creazione di microservizi su larga scala utilizzando Azure Service Fabric, imparare da hello esperti progettato e costruito questa piattaforma come servizio (PaaS).</span><span class="sxs-lookup"><span data-stu-id="f2374-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="f2374-105">Introduzione a architettura corretta e poi Scopri come toooptimize risorse per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2374-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="f2374-106">Hello [servizio Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) corso risposte hello domande spesso i clienti del mondo reale sugli scenari di Service Fabric e aree dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f2374-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="f2374-107">Scoprire come toodesign, sviluppare e utilizzare il microservizi nell'infrastruttura del servizio utilizza le procedure consigliate e modelli e riutilizzabili.</span><span class="sxs-lookup"><span data-stu-id="f2374-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="f2374-108">Si può iniziare da una panoramica di Service Fabric per poi procedere con vari argomenti di approfondimento come l'ottimizzazione e la sicurezza del cluster, la migrazione di applicazioni legacy, IoT su vasta scala, l'hosting di motori di gioco e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f2374-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="f2374-109">Esaminare la distribuzione continua per diversi carichi di lavoro e anche ottenere dettagli hello sul supporto di Linux e i contenitori.</span><span class="sxs-lookup"><span data-stu-id="f2374-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="f2374-110">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f2374-110">Introduction</span></span>
<span data-ttu-id="f2374-111">Esplorare le procedure consigliate e raccogliere informazioni per la scelta di una piattaforma distribuita come servizio (PaaS, Platform as a Service) o un'infrastruttura distribuita come servizio (IaaS, Infrastructure as a Service).</span><span class="sxs-lookup"><span data-stu-id="f2374-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="f2374-112">Recuperare i dettagli di hello sui principi di progettazione dell'applicazione si basa sulla collaudata seguenti.</span><span class="sxs-lookup"><span data-stu-id="f2374-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="f2374-113">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-113">Video</span></span></th><th><span data-ttu-id="f2374-114">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f2374-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduzione tooService dell'infrastruttura</a></span><span class="sxs-lookup"><span data-stu-id="f2374-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="f2374-116">Pianificazione e gestione del cluster</span><span class="sxs-lookup"><span data-stu-id="f2374-116">Cluster planning and management</span></span>
<span data-ttu-id="f2374-117">Questa presentazione di Azure Service Fabric include informazioni sulla pianificazione della capacità, l'ottimizzazione del cluster e la sicurezza del cluster.</span><span class="sxs-lookup"><span data-stu-id="f2374-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="f2374-118">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-118">Video</span></span></th><th><span data-ttu-id="f2374-119">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="f2374-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Pianificazione e gestione del cluster</a></span><span class="sxs-lookup"><span data-stu-id="f2374-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="f2374-121">Web con iperscalabilità</span><span class="sxs-lookup"><span data-stu-id="f2374-121">Hyper-scale web</span></span>
<span data-ttu-id="f2374-122">Una presentazione dei concetti relativi al Web con iperscalabilità, incluse disponibilità e affidabilità, iperscalabilità e gestione dello stato.</span><span class="sxs-lookup"><span data-stu-id="f2374-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="f2374-123">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-123">Video</span></span></th><th><span data-ttu-id="f2374-124">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f2374-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Web con iperscalabilità</a></span><span class="sxs-lookup"><span data-stu-id="f2374-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="f2374-126">IoT</span><span class="sxs-lookup"><span data-stu-id="f2374-126">IoT</span></span>
<span data-ttu-id="f2374-127">Esplorare hello Internet delle cose (IoT) nel contesto di hello di Azure Service Fabric, tra cui hello Azure IoT pipeline, multi-tenancy e IoT su larga scala.</span><span class="sxs-lookup"><span data-stu-id="f2374-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="f2374-128">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-128">Video</span></span></th><th><span data-ttu-id="f2374-129">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f2374-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="f2374-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="f2374-131">Giochi</span><span class="sxs-lookup"><span data-stu-id="f2374-131">Gaming</span></span>
<span data-ttu-id="f2374-132">Informazioni sui giochi a turni, i giochi interattivi e l'hosting di motori di gioco esistenti.</span><span class="sxs-lookup"><span data-stu-id="f2374-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="f2374-133">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-133">Video</span></span></th><th><span data-ttu-id="f2374-134">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f2374-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Giochi</a></span><span class="sxs-lookup"><span data-stu-id="f2374-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="f2374-136">Recapito continuo</span><span class="sxs-lookup"><span data-stu-id="f2374-136">Continuous delivery</span></span>
<span data-ttu-id="f2374-137">Presentazione dei concetti, tra i quali integrazione continua/recapito continuo con Visual Studio Team Services, flusso di lavoro di compilazione/creazione del pacchetto/pubblicazione, programma di installazione per più ambienti e pacchetto del servizio/condivisione.</span><span class="sxs-lookup"><span data-stu-id="f2374-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="f2374-138">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-138">Video</span></span></th><th><span data-ttu-id="f2374-139">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f2374-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Recapito continuo</a></span><span class="sxs-lookup"><span data-stu-id="f2374-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="f2374-141">Migrazione</span><span class="sxs-lookup"><span data-stu-id="f2374-141">Migration</span></span>
<span data-ttu-id="f2374-142">Informazioni sulla migrazione da un servizio cloud, inoltre toomigration delle applicazioni legacy.</span><span class="sxs-lookup"><span data-stu-id="f2374-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="f2374-143">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-143">Video</span></span></th><th><span data-ttu-id="f2374-144">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f2374-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migrazione</a></span><span class="sxs-lookup"><span data-stu-id="f2374-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="f2374-146">Contenitori e supporto di Linux</span><span class="sxs-lookup"><span data-stu-id="f2374-146">Containers and Linux support</span></span>
<span data-ttu-id="f2374-147">Ottenere una domanda a toohello risposta hello, "perché contenitori?"</span><span class="sxs-lookup"><span data-stu-id="f2374-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="f2374-148">Informazioni sull'anteprima hello per i contenitori di Windows, Linux supporta e orchestrazione di contenitori di Linux.</span><span class="sxs-lookup"><span data-stu-id="f2374-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="f2374-149">Inoltre, scoprire come toomigrate .NET Core App tooLinux.</span><span class="sxs-lookup"><span data-stu-id="f2374-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="f2374-150">Video</span><span class="sxs-lookup"><span data-stu-id="f2374-150">Video</span></span></th><th><span data-ttu-id="f2374-151">Presentazione di PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f2374-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="f2374-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Contenitori e supporto Linux</a></span><span class="sxs-lookup"><span data-stu-id="f2374-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="f2374-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2374-153">Next steps</span></span>
<span data-ttu-id="f2374-154">Ora che è stato sui modelli di Service Fabric e scenari, ulteriori informazioni su come troppo[creare e gestire cluster](service-fabric-deploy-anywhere.md), [eseguire la migrazione di servizi Cloud App tooService infrastruttura](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [impostare il recapito continuo](service-fabric-set-up-continuous-integration.md), e [distribuire contenitori](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2374-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
