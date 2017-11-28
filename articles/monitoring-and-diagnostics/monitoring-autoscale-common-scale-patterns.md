---
title: "aaaOverview dei modelli di scalabilità automatica comuni | Documenti Microsoft"
description: Informazioni su che alcune delle tooauto modelli comuni hello ridimensionare la risorsa in Azure.
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
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="5a99b-103">Panoramica di modelli comuni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="5a99b-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="5a99b-104">In questo articolo vengono descritte alcune tooscale modelli comuni hello la risorsa in Azure.</span><span class="sxs-lookup"><span data-stu-id="5a99b-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="5a99b-105">Azure ridimensionamento automatico di monitoraggio si applica solo tooVirtual set di scalabilità macchina (VMSS), servizi cloud, piani di servizio app e gli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="5a99b-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="5a99b-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="5a99b-106">Lets get started</span></span>

<span data-ttu-id="5a99b-107">Questo articolo presuppone che l'utente abbia familiarità con la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="5a99b-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="5a99b-108">È possibile [ottenere avviata tooscale qui la risorsa][1].</span><span class="sxs-lookup"><span data-stu-id="5a99b-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="5a99b-109">di seguito Hello sono alcuni dei modelli di scala comune hello.</span><span class="sxs-lookup"><span data-stu-id="5a99b-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="5a99b-110">Scalabilità in base alla CPU</span><span class="sxs-lookup"><span data-stu-id="5a99b-110">Scale based on CPU</span></span>

<span data-ttu-id="5a99b-111">È presente un'app Web (VMSS/ruolo del servizio cloud) e</span><span class="sxs-lookup"><span data-stu-id="5a99b-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="5a99b-112">Si desidera tooscale out e della scala in base alle CPU.</span><span class="sxs-lookup"><span data-stu-id="5a99b-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="5a99b-113">Inoltre, si desidera tooensure è un numero minimo di istanze.</span><span class="sxs-lookup"><span data-stu-id="5a99b-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="5a99b-114">Inoltre, si desidera tooensure che si imposta un numero di toohello limite massimo di istanze che per cui è possibile scalare.</span><span class="sxs-lookup"><span data-stu-id="5a99b-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Scalabilità in base alla CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="5a99b-116">Scalabilità diversa per giorni feriali e fine settimana</span><span class="sxs-lookup"><span data-stu-id="5a99b-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="5a99b-117">È presente un'app Web (VMSS/ruolo del servizio cloud) e</span><span class="sxs-lookup"><span data-stu-id="5a99b-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="5a99b-118">Si vogliono 3 istanze per impostazione predefinita nei giorni feriali</span><span class="sxs-lookup"><span data-stu-id="5a99b-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="5a99b-119">Non si prevede che il traffico nei fine settimana e pertanto si desidera tooscale verso il basso too1 istanza nei fine settimana.</span><span class="sxs-lookup"><span data-stu-id="5a99b-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Scalabilità diversa per giorni feriali e fine settimana][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="5a99b-121">Scalabilità diversa durante le festività</span><span class="sxs-lookup"><span data-stu-id="5a99b-121">Scale differently during holidays</span></span>

<span data-ttu-id="5a99b-122">È presente un'app Web (VMSS/ruolo del servizio cloud) e</span><span class="sxs-lookup"><span data-stu-id="5a99b-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="5a99b-123">Si desidera tooscale su/giù in base all'utilizzo della CPU per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="5a99b-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="5a99b-124">Tuttavia, durante le feste natalizie (o i giorni specifici che sono importanti per l'azienda) desiderato toooverride hello predefinite che dispone di maggiore capacità.</span><span class="sxs-lookup"><span data-stu-id="5a99b-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Scalabilità diversa nelle festività][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="5a99b-126">Scalabilità in base a metriche personalizzate</span><span class="sxs-lookup"><span data-stu-id="5a99b-126">Scale based on custom metric</span></span>

<span data-ttu-id="5a99b-127">È necessario un front-end web e un livello di API che comunica con hello di back-end.</span><span class="sxs-lookup"><span data-stu-id="5a99b-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="5a99b-128">Si desidera il livello di API hello tooscale basato sugli eventi personalizzati nel front-end hello (esempio: si desidera tooscale il processo di estrazione in base al numero di hello di elementi nel carrello degli acquisti hello)</span><span class="sxs-lookup"><span data-stu-id="5a99b-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Scalabilità in base a metriche personalizzate][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png