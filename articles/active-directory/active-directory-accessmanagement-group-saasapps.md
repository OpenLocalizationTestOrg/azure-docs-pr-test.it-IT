---
title: aaaUsing un tooSaaS di accesso di gruppo toomanage applicazioni | Documenti Microsoft
description: Come toouse gruppi in Azure Active Directory Premium o Basic tooassign accedere tooSaaS applicazioni integrate con Azure Active Directory.
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
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="cd65d-103">Utilizzo di applicazioni di tooSaaS un gruppo toomanage accesso</span><span class="sxs-lookup"><span data-stu-id="cd65d-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="cd65d-104">Azure Active Directory (Azure AD) con una licenza Azure AD Premium o Azure AD Basic, è possibile utilizzare gruppi tooassign accesso tooa applicazione SaaS integrata con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd65d-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="cd65d-105">Ad esempio, se si desidera accedere tooassign per hello marketing reparto toouse cinque applicazioni SaaS diverse, è possibile creare un gruppo che contiene gli utenti di hello reparto marketing hello e quindi assegnare tale gruppo toothese cinque applicazioni SaaS che sono richiesta in base al reparto marketing hello.</span><span class="sxs-lookup"><span data-stu-id="cd65d-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="cd65d-106">In questo modo è possibile risparmiare tempo mediante la gestione di appartenenza hello di hello marketing reparto in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="cd65d-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="cd65d-107">Gli utenti quindi assegnati toohello applicazione quando vengono aggiunti come membri del gruppo marketing hello e sono le relative assegnazioni rimosse da un'applicazione hello quando vengono rimossi dal gruppo marketing hello.</span><span class="sxs-lookup"><span data-stu-id="cd65d-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd65d-108">Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cd65d-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="cd65d-109">Questa funzionalità è utilizzabile con centinaia di applicazioni che è possibile aggiungere all'interno di hello raccolta di applicazioni Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd65d-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="cd65d-110">**accesso tooassign per un'applicazione SaaS di tooa gruppo**</span><span class="sxs-lookup"><span data-stu-id="cd65d-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="cd65d-111">In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory** sulla barra di spostamento hello sul lato sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="cd65d-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="cd65d-112">Seleziona hello **Directory** scheda e quindi aprire hello directory in cui si desidera l'accesso tooassign per un'applicazione SaaS di tooa gruppo.</span><span class="sxs-lookup"><span data-stu-id="cd65d-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="cd65d-113">Seleziona hello **applicazioni** scheda. Selezionare un'applicazione aggiunta dalla raccolta di applicazioni hello e quindi fare clic su hello **utenti e gruppi** scheda.</span><span class="sxs-lookup"><span data-stu-id="cd65d-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="cd65d-114">In hello **utenti e gruppi** scheda hello **a partire da** immettere nome hello di hello gruppo toowhich si desidera tooassign accesso e quindi selezionare hello segno di spunta in alto a destra hello.</span><span class="sxs-lookup"><span data-stu-id="cd65d-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="cd65d-115">È necessario solo la prima parte hello tootype del nome di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="cd65d-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="cd65d-116">Selezionare il gruppo di hello, quindi scegliere hello **assegna accesso** pulsante.</span><span class="sxs-lookup"><span data-stu-id="cd65d-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="cd65d-117">Selezionare **Sì** quando viene visualizzato il messaggio di conferma hello.</span><span class="sxs-lookup"><span data-stu-id="cd65d-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="cd65d-118">Appartenenze a gruppi nidificati non sono supportate per l'assegnazione basata su gruppo tooapplications in questo momento.</span><span class="sxs-lookup"><span data-stu-id="cd65d-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="cd65d-119">È inoltre possibile visualizzare quali utenti vengono assegnati applicazione toohello, direttamente o tramite l'appartenenza a un gruppo.</span><span class="sxs-lookup"><span data-stu-id="cd65d-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="cd65d-120">toodo hello, questa modifica **Mostra l'elenco a discesa da "Gruppi"** troppo**'Tutti gli utenti'**.</span><span class="sxs-lookup"><span data-stu-id="cd65d-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="cd65d-121">Hello sono elencati gli utenti nella directory di hello e se ogni utente è assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="cd65d-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="cd65d-122">elenco di Hello Mostra anche se gli utenti assegnato hello assegnati direttamente applicazione toohello (tipo di assegnazione visualizzato come "Diretta") oppure in base l'appartenenza al gruppo (tipo di assegnazione visualizzato come "Ereditata")</span><span class="sxs-lookup"><span data-stu-id="cd65d-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="cd65d-123">È possibile visualizzare scheda gruppi e utenti hello solo dopo avere abilitato Azure AD Premium o Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="cd65d-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="cd65d-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd65d-124">Next steps</span></span>
<span data-ttu-id="cd65d-125">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd65d-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="cd65d-126">Gestione di accesso tooresources con gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd65d-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="cd65d-127">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd65d-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="cd65d-128">Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo</span><span class="sxs-lookup"><span data-stu-id="cd65d-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="cd65d-129">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd65d-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="cd65d-130">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd65d-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
