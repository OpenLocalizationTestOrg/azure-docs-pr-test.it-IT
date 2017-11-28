---
title: Panoramica di istanze di contenitore aaaAzure | Documenti di Azure
description: Informazioni su Istanze di contenitore di Azure
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="5e41f-103">Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="5e41f-103">Azure Container Instances</span></span>

<span data-ttu-id="5e41f-104">Contenitori stanno diventando toopackage modo hello preferito, distribuire e gestire le applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="5e41f-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="5e41f-105">Istanze di contenitore di Azure offre hello più veloce e più semplice modo toorun un contenitore in Azure, senza dovere tooprovision tutte le macchine virtuali e senza doverlo tooadopt un servizio di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="5e41f-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="5e41f-106">Istanze di contenitore di Azure è un'ottima soluzione per qualsiasi scenario e funziona anche in contenitori isolati, inclusi i processi di compilazione, l'automazione di attività e le applicazioni semplici.</span><span class="sxs-lookup"><span data-stu-id="5e41f-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="5e41f-107">Per gli scenari in cui è necessario disporre di tutte orchestrazione contenitore, incluso l'individuazione del servizio tra più contenitori di scalabilità automatica e gli aggiornamenti dell'applicazione coordinato, si consiglia di hello [servizio contenitore di Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="5e41f-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="5e41f-108">Tempi di avvio rapidi</span><span class="sxs-lookup"><span data-stu-id="5e41f-108">Fast startup times</span></span>

<span data-ttu-id="5e41f-109">I contenitori offrono notevoli vantaggi in termini di avvio rispetto alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5e41f-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="5e41f-110">Con le istanze di contenitore di Azure, è possibile avviare un contenitore in Azure in pochi secondi senza tooprovision necessità hello e gestire macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5e41f-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="5e41f-111">Sicurezza a livello di hypervisor</span><span class="sxs-lookup"><span data-stu-id="5e41f-111">Hypervisor-level security</span></span>

<span data-ttu-id="5e41f-112">In passato i contenitori offrivano l'isolamento di dipendenze delle applicazioni e la governance delle risorse, ma non erano considerati sufficientemente protetti per l'uso di multi-tenant ostili.</span><span class="sxs-lookup"><span data-stu-id="5e41f-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="5e41f-113">Con Istanze di contenitore di Azure, l'applicazione è altrettanto isolata nel contenitore che in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e41f-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="5e41f-114">Dimensioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="5e41f-114">Custom sizes</span></span>

<span data-ttu-id="5e41f-115">I contenitori sono in genere ottimizzato toorun solo una singola applicazione, ma esigenze hello di tali applicazioni possono variare notevolmente.</span><span class="sxs-lookup"><span data-stu-id="5e41f-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="5e41f-116">Con Istanze di contenitore di Azure è possibile specificare esattamente la richiesta in termini di memoria e di core CPU.</span><span class="sxs-lookup"><span data-stu-id="5e41f-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="5e41f-117">Verranno addebitati i costi in base alle quali richiesta fatturato da hello in secondo luogo, in modo da ottimizzare più preciso la spesa in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="5e41f-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="5e41f-118">Connettività tramite indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="5e41f-118">Public IP connectivity</span></span>

<span data-ttu-id="5e41f-119">Con le istanze di contenitore di Azure, è possibile esporre ai contenitori direttamente toohello internet con un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="5e41f-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="5e41f-120">In hello future, si verrà espandere la rete integrazione tooinclude di funzionalità con le reti virtuali, caricare bilanciamento del carico e altre parti principali di hello infrastruttura di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e41f-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="5e41f-121">Archiviazione permanente</span><span class="sxs-lookup"><span data-stu-id="5e41f-121">Persistent storage</span></span>

<span data-ttu-id="5e41f-122">tooretrieve e rendere persistente lo stato con istanze di contenitori di Azure, offriamo condivisioni di file montaggio diretto di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e41f-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="5e41f-123">Contenitori Linux e Windows</span><span class="sxs-lookup"><span data-stu-id="5e41f-123">Linux and Windows containers</span></span>

<span data-ttu-id="5e41f-124">Con istanze di contenitori di Azure, è possibile pianificare entrambe le finestre e i contenitori di Linux con hello stessa API.</span><span class="sxs-lookup"><span data-stu-id="5e41f-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="5e41f-125">È sufficiente indicare il tipo di sistema operativo base hello e tutto il resto è identico.</span><span class="sxs-lookup"><span data-stu-id="5e41f-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="5e41f-126">Gruppi con pianificazione condivisa</span><span class="sxs-lookup"><span data-stu-id="5e41f-126">Co-scheduled groups</span></span>

<span data-ttu-id="5e41f-127">Istanze di contenitore di Azure supporta la pianificazione di gruppi multi-contenitore che condividono un computer host, una rete locale, un'archiviazione e un ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="5e41f-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="5e41f-128">In questo modo si toocombine dell'applicazione principale con altri utenti che svolge un ruolo di supporto, ad esempio la registrazione.</span><span class="sxs-lookup"><span data-stu-id="5e41f-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e41f-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e41f-129">Next steps</span></span>

<span data-ttu-id="5e41f-130">Provare a distribuire tooAzure un contenitore con un singolo comando con il nostro [Guida rapida](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="5e41f-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
