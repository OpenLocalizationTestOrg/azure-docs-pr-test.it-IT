---
title: Uso di un gruppo per gestire l'accesso ad applicazioni SaaS| Documentazione Microsoft
description: Come usare i gruppi in Azure Active Directory Premium o Basic per assegnare l'accesso ad applicazioni SaaS integrate in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="c3089-103">Uso di un gruppo per gestire l'accesso ad applicazioni SaaS</span><span class="sxs-lookup"><span data-stu-id="c3089-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="c3089-104">Con Azure Active Directory (Azure AD) con licenza Azure AD Premium o Azure AD Basic, è possibile usare i gruppi per assegnare l'accesso a un'applicazione SaaS integrata in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3089-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="c3089-105">Ad esempio, se si desidera assegnare al reparto marketing l'accesso per l'uso di cinque applicazioni SaaS diverse, è possibile creare un gruppo contenente gli utenti del reparto marketing e quindi assegnare a tale gruppo le cinque applicazioni SaaS necessarie.</span><span class="sxs-lookup"><span data-stu-id="c3089-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="c3089-106">In questo modo è possibile velocizzare le operazioni grazie alla gestione dei membri del reparto marketing in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="c3089-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="c3089-107">Gli utenti vengono quindi assegnati all'applicazione quando vengono aggiunti come membri del gruppo marketing. In modo analogo, le relative assegnazioni vengono rimosse dall'applicazione quando gli utenti vengono rimossi dal gruppo marketing.</span><span class="sxs-lookup"><span data-stu-id="c3089-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3089-108">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="c3089-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="c3089-109">Questa funzionalità può essere usata con centinaia di applicazioni che è possibile aggiungere dalla raccolta di applicazioni Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3089-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="c3089-110">**Per assegnare a un gruppo l'accesso a un'applicazione SaaS**</span><span class="sxs-lookup"><span data-stu-id="c3089-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="c3089-111">Nel [portale di Azure classico](https://manage.windowsazure.com), selezionare trovare **Active Directory** nella barra di spostamento sulla sinistra.</span><span class="sxs-lookup"><span data-stu-id="c3089-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="c3089-112">Selezionare la scheda **Directory** e aprire la directory in cui si desidera assegnare a un gruppo l'accesso a un'applicazione Saas.</span><span class="sxs-lookup"><span data-stu-id="c3089-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="c3089-113">Selezionare la scheda **Applicazioni** . Selezionare un'applicazione aggiunta dalla raccolta di applicazioni e quindi fare clic sulla scheda **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c3089-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="c3089-114">Nella scheda **Utenti e gruppi**, nel campo **Inizia con** immettere il nome del gruppo a cui si desidera assegnare l'accesso e selezionare il segno di spunta in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="c3089-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="c3089-115">È sufficiente digitare la prima parte del nome di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="c3089-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="c3089-116">Selezionare il gruppo, quindi scegliere il pulsante **Assegna accesso** .</span><span class="sxs-lookup"><span data-stu-id="c3089-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="c3089-117">Selezionare **Sì** quando viene visualizzato il messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="c3089-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="c3089-118">In questo momento, le appartenenze ai gruppi annidati non sono supportate per l'assegnazione alle applicazioni in base al gruppo.</span><span class="sxs-lookup"><span data-stu-id="c3089-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="c3089-119">È inoltre possibile visualizzare quali utenti sono assegnati all'applicazione direttamente o in base all'appartenenza a un gruppo.</span><span class="sxs-lookup"><span data-stu-id="c3089-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="c3089-120">Per farlo, A tale scopo, impostare **Mostra elenco a discesa da "Gruppi"** su **"Tutti gli utenti"**.</span><span class="sxs-lookup"><span data-stu-id="c3089-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="c3089-121">Nell'elenco sono visualizzati gli utenti nella directory ed è indicato se ogni utente è assegnato o meno all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c3089-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="c3089-122">Nell'elenco è inoltre indicato se gli utenti sono assegnati direttamente all'applicazione (il tipo di assegnazione è indicato come 'Diretto') oppure in base all'appartenenza al gruppo (il tipo di assegnazione è indicato come 'Ereditato').</span><span class="sxs-lookup"><span data-stu-id="c3089-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="c3089-123">La scheda Utenti e gruppi è visibile solo dopo aver abilitato Azure AD Premium o Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="c3089-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="c3089-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3089-124">Next steps</span></span>
<span data-ttu-id="c3089-125">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3089-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c3089-126">Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3089-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="c3089-127">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3089-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c3089-128">Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo</span><span class="sxs-lookup"><span data-stu-id="c3089-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="c3089-129">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3089-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="c3089-130">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3089-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
