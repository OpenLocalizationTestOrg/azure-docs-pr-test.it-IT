---
title: Panoramica di Istanze di contenitore di Azure | Azure Docs
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
ms.openlocfilehash: 3fb230c6b16a57e3650abf2000acdfe944cd633c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="6485e-103">Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6485e-103">Azure Container Instances</span></span>

<span data-ttu-id="6485e-104">I contenitori si stanno rapidamente affermando come soluzione preferita per creare pacchetti, distribuire e gestire le applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="6485e-104">Containers are quickly becoming the preferred way to package, deploy, and manage cloud applications.</span></span> <span data-ttu-id="6485e-105">Istanze di contenitore di Azure rappresenta il modo più semplice e rapido per eseguire un contenitore in Azure, senza dover effettuare il provisioning di macchine virtuali o adottare un servizio di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="6485e-105">Azure Container Instances offers the fastest and simplest way to run a container in Azure, without having to provision any virtual machines and without having to adopt a higher-level service.</span></span> 

<span data-ttu-id="6485e-106">Istanze di contenitore di Azure è un'ottima soluzione per qualsiasi scenario e funziona anche in contenitori isolati, inclusi i processi di compilazione, l'automazione di attività e le applicazioni semplici.</span><span class="sxs-lookup"><span data-stu-id="6485e-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="6485e-107">Per gli scenari in cui si rende necessaria l'orchestrazione completa dei contenitori, quali il rilevamento dei servizi tra più contenitori, la scalabilità automatica e gli aggiornamenti coordinati delle applicazioni, è consigliabile usare il [Servizio contenitore di Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="6485e-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="6485e-108">Tempi di avvio rapidi</span><span class="sxs-lookup"><span data-stu-id="6485e-108">Fast startup times</span></span>

<span data-ttu-id="6485e-109">I contenitori offrono notevoli vantaggi in termini di avvio rispetto alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6485e-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="6485e-110">Istanze di contenitore di Azure permette di avviare un contenitore in Azure in pochi secondi, senza dover gestire macchine virtuali o effettuarne il provisioning.</span><span class="sxs-lookup"><span data-stu-id="6485e-110">With Azure Container Instances, you can start a container in Azure in seconds without the need to provision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="6485e-111">Sicurezza a livello di hypervisor</span><span class="sxs-lookup"><span data-stu-id="6485e-111">Hypervisor-level security</span></span>

<span data-ttu-id="6485e-112">In passato i contenitori offrivano l'isolamento di dipendenze delle applicazioni e la governance delle risorse, ma non erano considerati sufficientemente protetti per l'uso di multi-tenant ostili.</span><span class="sxs-lookup"><span data-stu-id="6485e-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="6485e-113">Con Istanze di contenitore di Azure, l'applicazione è altrettanto isolata nel contenitore che in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6485e-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="6485e-114">Dimensioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="6485e-114">Custom sizes</span></span>

<span data-ttu-id="6485e-115">I contenitori sono in genere ottimizzati per l'esecuzione di un'applicazione singola, ma le esigenze specifiche di tale applicazione possono variare notevolmente.</span><span class="sxs-lookup"><span data-stu-id="6485e-115">Containers are typically optimized to run just a single application, but the exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="6485e-116">Con Istanze di contenitore di Azure è possibile specificare esattamente la richiesta in termini di memoria e di core CPU.</span><span class="sxs-lookup"><span data-stu-id="6485e-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="6485e-117">Si paga in base alla richiesta, fatturata al secondo. Questo permette di ottimizzare con precisione la spesa in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="6485e-117">You pay based on what you request, billed by the second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="6485e-118">Connettività tramite indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="6485e-118">Public IP connectivity</span></span>

<span data-ttu-id="6485e-119">Istanze di contenitore di Azure permette di esporre i contenitori direttamente a Internet con un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="6485e-119">With Azure Container Instances, you can expose your containers directly to the internet with a public IP address.</span></span> <span data-ttu-id="6485e-120">In futuro, le funzionalità di rete verranno estese all'integrazione con reti virtuali, servizi di bilanciamento del carico e altre componenti essenziali dell'infrastruttura di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="6485e-120">In the future, we will expand our networking capabilities to include integration with virtual networks, load balancers, and other core parts of the Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="6485e-121">Archiviazione permanente</span><span class="sxs-lookup"><span data-stu-id="6485e-121">Persistent storage</span></span>

<span data-ttu-id="6485e-122">Per recuperare e rendere persistente lo stato con Istanze di contenitore di Azure, è disponibile il montaggio diretto di condivisioni file di Azure.</span><span class="sxs-lookup"><span data-stu-id="6485e-122">To retrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="6485e-123">Contenitori Linux e Windows</span><span class="sxs-lookup"><span data-stu-id="6485e-123">Linux and Windows containers</span></span>

<span data-ttu-id="6485e-124">Istanze di contenitore di Azure permette di pianificare i contenitori Windows e Linux con la stessa API.</span><span class="sxs-lookup"><span data-stu-id="6485e-124">With Azure Container Instances, you can schedule both Windows and Linux containers with the same API.</span></span> <span data-ttu-id="6485e-125">È sufficiente indicare il tipo di sistema operativo di base. Tutti gli altri elementi sono identici.</span><span class="sxs-lookup"><span data-stu-id="6485e-125">Simply indicate the base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="6485e-126">Gruppi con pianificazione condivisa</span><span class="sxs-lookup"><span data-stu-id="6485e-126">Co-scheduled groups</span></span>

<span data-ttu-id="6485e-127">Istanze di contenitore di Azure supporta la pianificazione di gruppi multi-contenitore che condividono un computer host, una rete locale, un'archiviazione e un ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="6485e-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="6485e-128">Questo permette di combinare l'applicazione principale con altre che svolgono un ruolo di supporto, ad esempio la registrazione.</span><span class="sxs-lookup"><span data-stu-id="6485e-128">This enables you to combine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6485e-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6485e-129">Next steps</span></span>

<span data-ttu-id="6485e-130">Provare a distribuire un contenitore in Azure con un comando singolo, seguendo le indicazioni della [guida introduttiva](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="6485e-130">Try deploying a container to Azure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>