---
title: aaaSubscription e gli account per le macchine virtuali Windows in Azure | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per le sottoscrizioni e account in Azure.
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
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="8a0ea-103">Linee guida per le sottoscrizioni e gli account Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="8a0ea-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="8a0ea-104">In questo articolo si incentra sulla comprensione di come si espande tooapproach sottoscrizione e account di gestione, come l'ambiente e un utente di base.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="8a0ea-105">Linee guida per l'implementazione di sottoscrizioni e account</span><span class="sxs-lookup"><span data-stu-id="8a0ea-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="8a0ea-106">Decisioni:</span><span class="sxs-lookup"><span data-stu-id="8a0ea-106">Decisions:</span></span>

* <span data-ttu-id="8a0ea-107">Il set di account e sottoscrizioni è necessario toohost l'infrastruttura o il carico di lavoro IT?</span><span class="sxs-lookup"><span data-stu-id="8a0ea-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="8a0ea-108">Come toobreak verso il basso hello gerarchia toofit organizzazione?</span><span class="sxs-lookup"><span data-stu-id="8a0ea-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="8a0ea-109">Attività:</span><span class="sxs-lookup"><span data-stu-id="8a0ea-109">Tasks:</span></span>

* <span data-ttu-id="8a0ea-110">Definire la gerarchia logica dell'organizzazione che si desidera toomanage dal livello di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="8a0ea-111">toomatch questa gerarchia logica, definire gli account di hello necessari e le sottoscrizioni con ogni account.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="8a0ea-112">Creare set di hello di sottoscrizioni e gli account utilizzando la convenzione di denominazione.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="8a0ea-113">Sottoscrizioni e account</span><span class="sxs-lookup"><span data-stu-id="8a0ea-113">Subscriptions and accounts</span></span>
<span data-ttu-id="8a0ea-114">toowork con Azure, è necessario uno o più sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="8a0ea-115">Nell'ambito di tali sottoscrizioni sono presenti risorse come le macchine virtuali o le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="8a0ea-116">I clienti aziendali hanno in genere un'iscrizione Enterprise, risorse di primo piano hello nella gerarchia di hello, e tooone associato o altri account.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="8a0ea-117">Per utenti e i clienti senza un'iscrizione Enterprise, risorse di primo piano hello sono account hello.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="8a0ea-118">Le sottoscrizioni sono associati tooaccounts e possono essere presenti uno o più sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="8a0ea-119">Azure record di informazioni a livello di sottoscrizione hello di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="8a0ea-120">A causa di limite toohello due di livelli della gerarchia in relazione tra Account o una sottoscrizione di hello, è importante tooalign convenzione di denominazione hello di account e sottoscrizioni toohello esigenze di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="8a0ea-121">Ad esempio, una società globale Usa Azure, possono scegliere account toohave uno per ogni area e avranno sottoscrizioni gestite a livello di area hello:</span><span class="sxs-lookup"><span data-stu-id="8a0ea-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="8a0ea-122">Ad esempio, è possibile utilizzare hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8a0ea-122">For instance, you might use hello following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="8a0ea-123">Se un'area decide toohave più gruppo specifico di una sottoscrizione associata tooa, convenzione di denominazione hello deve includere un tooencode modo hello dati aggiuntivi sul conto hello o nome della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="8a0ea-124">Questa organizzazione consente Ritocco dei fatturazione dati toogenerate hello nuovi livelli di gerarchia durante la fatturazione di report:</span><span class="sxs-lookup"><span data-stu-id="8a0ea-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="8a0ea-125">organizzazione Hello potrebbe essere simile hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8a0ea-125">hello organization could look like hello following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="8a0ea-126">Viene fornita la fatturazione dettagliata tramite un file scaricabile, per un singolo account o per tutti gli account di un contratto Enterprise.</span><span class="sxs-lookup"><span data-stu-id="8a0ea-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a0ea-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a0ea-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

