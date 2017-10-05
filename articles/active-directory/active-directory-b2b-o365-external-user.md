---
title: Condivisione esterna di Office 365 e Collaborazione B2B di Azure Active Directory | Documentazione Microsoft
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
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="838cc-103">Condivisione esterna di Office 365 e Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="838cc-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="838cc-104">La condivisione esterna in Office 365, con OneDrive, SharePoint Online, gruppi unificati e così via, e quella tramite Collaborazione B2B di Azure Active Directory (Azure AD) tecnicamente si equivalgono.</span><span class="sxs-lookup"><span data-stu-id="838cc-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="838cc-105">Tutti i tipi di condivisione esterna, ad eccezione di OneDrive/SharePoint Online, inclusi gli utenti guest nei gruppi di Office 365, fanno già uso delle API di invito di Collaborazione B2B di Azure AD per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="838cc-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="838cc-106">La gestione degli inviti di OneDrive/SharePoint Online è separata.</span><span class="sxs-lookup"><span data-stu-id="838cc-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="838cc-107">Il supporto per la condivisione esterna in OneDrive/SharePoint Online è iniziato prima dello sviluppo del supporto di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="838cc-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="838cc-108">Nel tempo la condivisione esterna di OneDrive/SharePoint Online ha accumulato diverse funzionalità e milioni di utenti, che fanno uso del modello di condivisione incorporato nel prodotto.</span><span class="sxs-lookup"><span data-stu-id="838cc-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="838cc-109">Rimangono tuttavia alcune sottili differenze di funzionamento tra la condivisione esterna di OneDrive/SharePoint Online e quella di Collaborazione B2B di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="838cc-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="838cc-110">OneDrive/SharePoint consente di aggiungere utenti alla directory dopo che gli utenti hanno riscattato gli inviti.</span><span class="sxs-lookup"><span data-stu-id="838cc-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="838cc-111">Prima del riscatto l'utente non è quindi visibile nel portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="838cc-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="838cc-112">Se nel frattempo un altro sito invita un utente, viene generato un nuovo invito.</span><span class="sxs-lookup"><span data-stu-id="838cc-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="838cc-113">Quando invece si usa Collaborazione B2B di Azure AD, gli utenti vengono aggiunti immediatamente all'invito e sono quindi visibili ovunque.</span><span class="sxs-lookup"><span data-stu-id="838cc-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="838cc-114">L'esperienza di riscatto in OneDrive/SharePoint Online è diversa da quella in Collaborazione B2B di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="838cc-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="838cc-115">Dopo che un utente ha riscattato un invito, le esperienze sono simili.</span><span class="sxs-lookup"><span data-stu-id="838cc-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="838cc-116">Gli utenti invitati di Collaborazione B2B di Azure AD possono essere selezionati nelle finestre di dialogo di condivisione di OneDrive/SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="838cc-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="838cc-117">Dopo avere riscattato gli inviti, gli utenti invitati di OneDrive/SharePoint Online vengono visualizzati anche in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="838cc-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="838cc-118">Per gestire la condivisione esterna in OneDrive/SharePoint Online con Collaborazione B2B di Azure AD, configurare l'impostazione relativa alla condivisione esterna in OneDrive/SharePoint Online su **Only allow sharing with external users already in the directory** (Consenti la condivisione solo con gli utenti esterni già nella directory).</span><span class="sxs-lookup"><span data-stu-id="838cc-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="838cc-119">Gli utenti possono accedere a siti condivisi esternamente e scegliere tra i collaboratori esterni che l'amministratore ha aggiunto.</span><span class="sxs-lookup"><span data-stu-id="838cc-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="838cc-120">L'amministratore può aggiungere i collaboratori esterni tramite le API di invito di Collaborazione B2B.</span><span class="sxs-lookup"><span data-stu-id="838cc-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![Impostazione relativa alla condivisione esterna di Online OneDrive/SharePoint](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="838cc-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="838cc-122">Next steps</span></span>

<span data-ttu-id="838cc-123">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="838cc-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="838cc-124">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="838cc-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="838cc-125">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="838cc-126">Aggiunta di un utente di Collaborazione B2B a un ruolo</span><span class="sxs-lookup"><span data-stu-id="838cc-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="838cc-127">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="838cc-128">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="838cc-129">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="838cc-130">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="838cc-131">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="838cc-132">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="838cc-133">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="838cc-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
