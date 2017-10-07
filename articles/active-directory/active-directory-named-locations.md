---
title: percorsi aaaNamed in Azure Active Directory | Documenti Microsoft
description: "Configurando denominato percorsi, è possibile evitare IP indirizzi che appartengono a organizzazione generano falsi positivi per il tipo di evento di rischio di hello impossibili tooatypical corsa."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="4ced8-103">Località denominate in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ced8-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="4ced8-104">Con hello denominato percorsi funzionalità di Azure Active Directory, è possibile etichettare gli intervalli di indirizzi IP attendibili nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4ced8-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="4ced8-105">Nell'ambiente in uso, è possibile utilizzare posizioni denominate contesto hello di rilevamento hello di [gli eventi di rischio](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="4ced8-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="4ced8-106">funzionalità Hello consente di ridurre il numero di hello di segnalati falsi positivi per hello *percorsi di comunicazione Impossibile tooatypical* il tipo di evento di rischio.</span><span class="sxs-lookup"><span data-stu-id="4ced8-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="4ced8-107">Configurazione</span><span class="sxs-lookup"><span data-stu-id="4ced8-107">Configuration</span></span>

<span data-ttu-id="4ced8-108">posizione denominata tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="4ced8-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="4ced8-109">Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="4ced8-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="4ced8-110">Nel riquadro di sinistra hello, fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ced8-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![collegamento di Azure Active Directory Hello nel riquadro di sinistra hello](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="4ced8-112">In hello **Azure Active Directory** pannello in hello **sicurezza** fare clic su **accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="4ced8-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![il comando di accesso condizionale Hello](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="4ced8-114">In hello **accesso condizionale** pannello in hello **Gestisci** fare clic su **posizioni denominate**.</span><span class="sxs-lookup"><span data-stu-id="4ced8-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![comando percorsi denominato Hello](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="4ced8-116">In hello **denominato percorsi** pannello, fare clic su **nuova posizione**.</span><span class="sxs-lookup"><span data-stu-id="4ced8-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Hello nuovo comando di percorso](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="4ced8-118">In hello **New** pannello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ced8-118">On hello **New** blade, do hello following:</span></span>

    ![Nuovo pannello Hello](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="4ced8-120">a.</span><span class="sxs-lookup"><span data-stu-id="4ced8-120">a.</span></span> <span data-ttu-id="4ced8-121">In hello **nome** , digitare un nome per il percorso denominato.</span><span class="sxs-lookup"><span data-stu-id="4ced8-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="4ced8-122">b.</span><span class="sxs-lookup"><span data-stu-id="4ced8-122">b.</span></span> <span data-ttu-id="4ced8-123">In hello **intervalli IP** , digitare un intervallo di IP.</span><span class="sxs-lookup"><span data-stu-id="4ced8-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="4ced8-124">intervallo IP Hello deve toobe in hello *Classless Interdomain Routing* formato (CIDR).</span><span class="sxs-lookup"><span data-stu-id="4ced8-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="4ced8-125">c.</span><span class="sxs-lookup"><span data-stu-id="4ced8-125">c.</span></span> <span data-ttu-id="4ced8-126">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4ced8-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="4ced8-127">Informazioni utili</span><span class="sxs-lookup"><span data-stu-id="4ced8-127">What you should know</span></span>

<span data-ttu-id="4ced8-128">**Aggiornamenti bulk**: quando si crea o Aggiorna ubicazioni denominate, per gli aggiornamenti bulk, è possibile caricare o scaricare un file CSV con intervalli IP hello.</span><span class="sxs-lookup"><span data-stu-id="4ced8-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="4ced8-129">Un'operazione di caricamento consente di aggiungere intervalli IP hello nell'elenco di toohello hello file anziché sovrascrivere l'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="4ced8-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Hello caricare e scaricare i collegamenti](./media/active-directory-named-locations/09.png)


<span data-ttu-id="4ced8-131">**Limitazioni**: È possibile definire un massimo di 60 posizioni denominate, con tooeach di intervallo assegnato IP uno di essi.</span><span class="sxs-lookup"><span data-stu-id="4ced8-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="4ced8-132">Se si dispone di una sola posizione denominata configurata, è possibile definire degli intervalli IP too500 appositamente.</span><span class="sxs-lookup"><span data-stu-id="4ced8-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4ced8-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ced8-133">Next steps</span></span>

<span data-ttu-id="4ced8-134">toolearn più sugli eventi di rischio, vedere [gli eventi di rischio di Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="4ced8-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

