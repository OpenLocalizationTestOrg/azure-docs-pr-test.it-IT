---
title: aaaOffice 365 condivisione esterna e la collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: Informazioni sul mapping delle attestazioni per Collaborazione B2B in Azure Active Directory
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="d3f67-103">Condivisione esterna di Office 365 e Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3f67-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="d3f67-104">Condivisione in Office 365 (OneDrive, SharePoint Online, gruppi unificati, e così via) e B2B di Azure Active Directory (Azure AD) sono tecnicamente di collaborazione esterna hello stessa cosa.</span><span class="sxs-lookup"><span data-stu-id="d3f67-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="d3f67-105">Condivisione tutti esterna (ad eccezione di OneDrive/SharePoint Online), inclusi gli utenti guest in gruppi di Office 365, Usa già l'invito di collaborazione Azure AD B2B hello API per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="d3f67-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="d3f67-106">La gestione degli inviti di OneDrive/SharePoint Online è separata.</span><span class="sxs-lookup"><span data-stu-id="d3f67-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="d3f67-107">Il supporto per la condivisione esterna in OneDrive/SharePoint Online è iniziato prima dello sviluppo del supporto di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3f67-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="d3f67-108">Nel tempo, la condivisione esterna OneDrive/SharePoint Online sono accumulati diverse funzionalità e diversi milioni di utenti che utilizzano prodotto hello del incorporati modello di condivisione.</span><span class="sxs-lookup"><span data-stu-id="d3f67-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="d3f67-109">Rimangono tuttavia alcune sottili differenze di funzionamento tra la condivisione esterna di OneDrive/SharePoint Online e quella di Collaborazione B2B di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d3f67-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="d3f67-110">OneDrive o SharePoint Online l'aggiunta di utenti toohello directory dopo che gli utenti hanno riscattati gli inviti.</span><span class="sxs-lookup"><span data-stu-id="d3f67-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="d3f67-111">Prima di rimborso, pertanto, non viene visualizzato utente hello nel portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3f67-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="d3f67-112">Se un utente in hello frattempo invita a un altro sito, viene generato un nuovo invito.</span><span class="sxs-lookup"><span data-stu-id="d3f67-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="d3f67-113">Quando invece si usa Collaborazione B2B di Azure AD, gli utenti vengono aggiunti immediatamente all'invito e sono quindi visibili ovunque.</span><span class="sxs-lookup"><span data-stu-id="d3f67-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="d3f67-114">esperienza di riscatto Hello in OneDrive o SharePoint Online è diverso dall'esperienza hello in collaborazione B2B di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d3f67-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="d3f67-115">Dopo che un utente Riscatta un invito, hello esperienze simili.</span><span class="sxs-lookup"><span data-stu-id="d3f67-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="d3f67-116">Gli utenti invitati di Collaborazione B2B di Azure AD possono essere selezionati nelle finestre di dialogo di condivisione di OneDrive/SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d3f67-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="d3f67-117">Dopo avere riscattato gli inviti, gli utenti invitati di OneDrive/SharePoint Online vengono visualizzati anche in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3f67-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="d3f67-118">toomanage esterno condivisione in OneDrive o SharePoint Online con la collaborazione B2B di Azure Active Directory, imposta hello OneDrive/SharePoint Online esterne condivisione impostazione troppo**solo consentire la condivisione con utenti esterni già nella directory hello**.</span><span class="sxs-lookup"><span data-stu-id="d3f67-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="d3f67-119">Gli utenti possono accedere a siti tooexternally condivisi e prelievo da collaboratori esterni che hello amministratore è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="d3f67-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="d3f67-120">salve aggiungere collaboratori esterni di hello tramite hello invito di collaborazione B2B API.</span><span class="sxs-lookup"><span data-stu-id="d3f67-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![Hello OneDrive/SharePoint Online esterni di impostazione di condivisione](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="d3f67-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3f67-122">Next steps</span></span>

<span data-ttu-id="d3f67-123">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="d3f67-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d3f67-124">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="d3f67-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d3f67-125">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d3f67-126">Aggiunta di un ruolo di tooa utente collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="d3f67-127">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="d3f67-128">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="d3f67-129">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d3f67-130">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d3f67-131">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d3f67-132">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d3f67-133">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="d3f67-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
