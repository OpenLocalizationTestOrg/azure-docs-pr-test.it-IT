---
title: Sottoscrizione e account per le macchine virtuali Windows in Azure | Documentazione Microsoft
description: Informazioni sulle principali linee guida di progettazione e implementazione per le sottoscrizioni e gli account in Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b54e18ed6ecef26a059a6ce742bca03a6434183
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="a00ea-103">Linee guida per le sottoscrizioni e gli account Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="a00ea-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="a00ea-104">Questo articolo è incentrato sulla comprensione delle modalità di gestione delle sottoscrizioni e degli account mano a mano che si amplia l'ambiente e la base utenti.</span><span class="sxs-lookup"><span data-stu-id="a00ea-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="a00ea-105">Linee guida per l'implementazione di sottoscrizioni e account</span><span class="sxs-lookup"><span data-stu-id="a00ea-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="a00ea-106">Decisioni:</span><span class="sxs-lookup"><span data-stu-id="a00ea-106">Decisions:</span></span>

* <span data-ttu-id="a00ea-107">Quali sono i set di sottoscrizioni e account necessari per l'hosting dell'infrastruttura o del carico di lavoro IT?</span><span class="sxs-lookup"><span data-stu-id="a00ea-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="a00ea-108">Come deve essere suddivisa la gerarchia in modo da adattarsi all'organizzazione?</span><span class="sxs-lookup"><span data-stu-id="a00ea-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="a00ea-109">Attività:</span><span class="sxs-lookup"><span data-stu-id="a00ea-109">Tasks:</span></span>

* <span data-ttu-id="a00ea-110">Definire la gerarchia logica dell'organizzazione in base a come si intende gestirla a livello di sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="a00ea-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="a00ea-111">Per soddisfare questa gerarchia logica, definire gli account necessari e le sottoscrizioni per ogni account.</span><span class="sxs-lookup"><span data-stu-id="a00ea-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="a00ea-112">Creare il set di sottoscrizioni e account usando la convenzione di denominazione scelta.</span><span class="sxs-lookup"><span data-stu-id="a00ea-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="a00ea-113">Sottoscrizioni e account</span><span class="sxs-lookup"><span data-stu-id="a00ea-113">Subscriptions and accounts</span></span>
<span data-ttu-id="a00ea-114">Per usare Azure sono necessarie una o più sottoscrizioni ad Azure.</span><span class="sxs-lookup"><span data-stu-id="a00ea-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="a00ea-115">Nell'ambito di tali sottoscrizioni sono presenti risorse come le macchine virtuali o le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="a00ea-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="a00ea-116">I clienti aziendali dispongono in genere di una registrazione Enterprise, che è la risorsa più in alto nella gerarchia ed è associata a uno o più account.</span><span class="sxs-lookup"><span data-stu-id="a00ea-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="a00ea-117">Per utenti e clienti senza una registrazione Enterprise, la risorsa di livello superiore è l'Account.</span><span class="sxs-lookup"><span data-stu-id="a00ea-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="a00ea-118">Le sottoscrizioni sono associate agli account ed è possibile associare una o più sottoscrizioni a ogni account.</span><span class="sxs-lookup"><span data-stu-id="a00ea-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="a00ea-119">In Azure le informazioni relative alla fatturazione vengono registrate a livello di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a00ea-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="a00ea-120">A causa del limite di due livelli gerarchici nella relazione di account/sottoscrizione è importante allineare la convenzione di denominazione degli account e delle sottoscrizioni alle esigenze di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="a00ea-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="a00ea-121">Se ad esempio un'azienda globale usa Azure, può scegliere di disporre di un account per ogni area e fare in modo che le sottoscrizioni vengano gestite a livello di area:</span><span class="sxs-lookup"><span data-stu-id="a00ea-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="a00ea-122">È ad esempio possibile usare la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="a00ea-122">For instance, you might use the following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="a00ea-123">Se in un'area si decide di associare più sottoscrizioni a un determinato gruppo, la convenzione di denominazione deve incorporare un modo per codificare i dati aggiuntivi sia nel nome account che nel nome della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a00ea-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="a00ea-124">Questa organizzazione consente di elaborare i dati di fatturazione per generare nuovi livelli di gerarchia durante la fatturazione dei report:</span><span class="sxs-lookup"><span data-stu-id="a00ea-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="a00ea-125">L'organizzazione potrebbe essere simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a00ea-125">The organization could look like the following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="a00ea-126">Viene fornita la fatturazione dettagliata tramite un file scaricabile, per un singolo account o per tutti gli account di un contratto Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a00ea-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a00ea-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a00ea-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

