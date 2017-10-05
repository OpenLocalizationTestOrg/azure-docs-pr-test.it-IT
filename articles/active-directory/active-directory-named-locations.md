---
title: "Località denominate in Azure Active Directory | Microsoft Docs"
description: "Configurando località denominate, è possibile evitare che indirizzi IP di proprietà dell'organizzazione generino falsi positivi per eventi di rischio di tipo Trasferimento impossibile a posizioni atipiche."
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
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="d6d46-103">Località denominate in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6d46-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="d6d46-104">La funzionalità delle località denominate di Azure Active Directory consente di etichettare intervalli di indirizzi IP attendibili nelle organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="d6d46-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="d6d46-105">Nell'ambiente in uso si possono usare le località denominate nel contesto del rilevamento degli [eventi di rischio](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="d6d46-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="d6d46-106">Questa funzionalità consente di ridurre il numero di falsi positivi segnalati per gli eventi di rischio di tipo *Trasferimento impossibile a posizioni atipiche*.</span><span class="sxs-lookup"><span data-stu-id="d6d46-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="d6d46-107">Configurazione</span><span class="sxs-lookup"><span data-stu-id="d6d46-107">Configuration</span></span>

<span data-ttu-id="d6d46-108">Per configurare una località denominata:</span><span class="sxs-lookup"><span data-stu-id="d6d46-108">To configure a named location:</span></span>

1. <span data-ttu-id="d6d46-109">Accedere al [portale di Azure](https://portal.azure.com) come amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="d6d46-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="d6d46-110">Nel riquadro sinistro fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6d46-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![Collegamento ad Azure Active Directory nel riquadro sinistro](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="d6d46-112">Nella sezione **Sicurezza** del pannello **Azure Active Directory** fare clic su **Accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="d6d46-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![Comando Accesso condizionale](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="d6d46-114">Nella sezione **Gestisci** del pannello **Accesso condizionale** fare clic su **Località denominate**.</span><span class="sxs-lookup"><span data-stu-id="d6d46-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![Comando Località denominate](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="d6d46-116">Nel pannello **Località denominate** fare clic su **Nuovo percorso**.</span><span class="sxs-lookup"><span data-stu-id="d6d46-116">On the **Named locations** blade, click **New location**.</span></span>

    ![Comando Nuovo percorso](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="d6d46-118">Nel pannello **Nuovo** eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="d6d46-118">On the **New** blade, do the following:</span></span>

    ![Pannello Nuovo](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="d6d46-120">a.</span><span class="sxs-lookup"><span data-stu-id="d6d46-120">a.</span></span> <span data-ttu-id="d6d46-121">Nella casella **Nome** digitare un nome per la località denominata.</span><span class="sxs-lookup"><span data-stu-id="d6d46-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="d6d46-122">b.</span><span class="sxs-lookup"><span data-stu-id="d6d46-122">b.</span></span> <span data-ttu-id="d6d46-123">Nella casella **Intervalli IP** digitare un intervallo IP.</span><span class="sxs-lookup"><span data-stu-id="d6d46-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="d6d46-124">L'intervallo IP deve essere in formato *CIDR (Classless Inter-Domain Routing)*.</span><span class="sxs-lookup"><span data-stu-id="d6d46-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="d6d46-125">c.</span><span class="sxs-lookup"><span data-stu-id="d6d46-125">c.</span></span> <span data-ttu-id="d6d46-126">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d6d46-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="d6d46-127">Informazioni utili</span><span class="sxs-lookup"><span data-stu-id="d6d46-127">What you should know</span></span>

<span data-ttu-id="d6d46-128">**Aggiornamenti in blocco**: quando si creano o si aggiornano le località denominate, per aggiornamenti in blocco è possibile caricare o scaricare un file CSV con gli intervalli IP.</span><span class="sxs-lookup"><span data-stu-id="d6d46-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="d6d46-129">Un caricamento aggiunge gli intervalli IP nel file all'elenco invece di sovrascrivere l'elenco.</span><span class="sxs-lookup"><span data-stu-id="d6d46-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![Collegamenti Carica e Scarica](./media/active-directory-named-locations/09.png)


<span data-ttu-id="d6d46-131">**Limitazioni**: è possibile definire un massimo di 60 località denominate, ognuna con un intervallo IP assegnato.</span><span class="sxs-lookup"><span data-stu-id="d6d46-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="d6d46-132">Se si configura una sola località denominata, è possibile definire fino a 500 intervalli IP per tale località.</span><span class="sxs-lookup"><span data-stu-id="d6d46-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d6d46-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6d46-133">Next steps</span></span>

<span data-ttu-id="d6d46-134">Per altre informazioni sugli eventi di rischio, vedere [Eventi di rischio di Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="d6d46-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

