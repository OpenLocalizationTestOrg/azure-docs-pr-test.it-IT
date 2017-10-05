---
title: "Panoramica di modelli comuni di scalabilità automatica | Microsoft Docs"
description: "Informazioni su alcuni modelli comuni per la scalabilità automatica delle risorse in Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="ecc4e-103">Panoramica di modelli comuni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="ecc4e-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="ecc4e-104">Questo articolo descrive alcuni modelli comuni per la scalabilità delle risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="ecc4e-105">La scalabilità automatica di Monitoraggio di Azure si applica solo a set di scalabilità di macchine virtuali (VMSS), servizi cloud, piani di servizio app e ambienti di servizio app.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="ecc4e-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="ecc4e-106">Lets get started</span></span>

<span data-ttu-id="ecc4e-107">Questo articolo presuppone che l'utente abbia familiarità con la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="ecc4e-108">È disponibile un'[introduzione alla scalabilità della risorsa][1].</span><span class="sxs-lookup"><span data-stu-id="ecc4e-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="ecc4e-109">Di seguito sono indicati alcuni modelli comuni di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="ecc4e-110">Scalabilità in base alla CPU</span><span class="sxs-lookup"><span data-stu-id="ecc4e-110">Scale based on CPU</span></span>

<span data-ttu-id="ecc4e-111">È presente un'app Web (VMSS/ruolo del servizio cloud) e</span><span class="sxs-lookup"><span data-stu-id="ecc4e-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="ecc4e-112">Si vuole aumentare/ridurre il numero di istanze in base alla CPU.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="ecc4e-113">Si vuole anche verificare che sia presente un numero minimo di istanze.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="ecc4e-114">Si vuole anche impostare un limite massimo per il numero di istanze che è possibile aggiungere.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![Scalabilità in base alla CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="ecc4e-116">Scalabilità diversa per giorni feriali e fine settimana</span><span class="sxs-lookup"><span data-stu-id="ecc4e-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="ecc4e-117">È presente un'app Web (VMSS/ruolo del servizio cloud) e</span><span class="sxs-lookup"><span data-stu-id="ecc4e-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="ecc4e-118">Si vogliono 3 istanze per impostazione predefinita nei giorni feriali</span><span class="sxs-lookup"><span data-stu-id="ecc4e-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="ecc4e-119">Non si prevede traffico nei fine settimana e quindi si vuole ridurre il numero di istanze a 1 nei fine settimana.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Scalabilità diversa per giorni feriali e fine settimana][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="ecc4e-121">Scalabilità diversa durante le festività</span><span class="sxs-lookup"><span data-stu-id="ecc4e-121">Scale differently during holidays</span></span>

<span data-ttu-id="ecc4e-122">È presente un'app Web (VMSS/ruolo del servizio cloud) e</span><span class="sxs-lookup"><span data-stu-id="ecc4e-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="ecc4e-123">Si vogliono aumentare/ridurre le prestazioni in base all'utilizzo della CPU per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="ecc4e-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="ecc4e-124">Durante le festività o in giorni specifici importanti per l'azienda si vogliono tuttavia ignorare le impostazioni predefinite e avere a disposizione maggiore capacità.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Scalabilità diversa nelle festività][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="ecc4e-126">Scalabilità in base a metriche personalizzate</span><span class="sxs-lookup"><span data-stu-id="ecc4e-126">Scale based on custom metric</span></span>

<span data-ttu-id="ecc4e-127">Sono disponibili un front-end web e un livello API che comunica con il back-end.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="ecc4e-128">Si vuole ridimensionare il livello API in base a eventi personalizzati nel front-end, ad esempio si vuole ridimensionare il processo di completamento della transazione in base al numero di articoli contenuti nel carrello acquisti.</span><span class="sxs-lookup"><span data-stu-id="ecc4e-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Scalabilità in base a metriche personalizzate][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png