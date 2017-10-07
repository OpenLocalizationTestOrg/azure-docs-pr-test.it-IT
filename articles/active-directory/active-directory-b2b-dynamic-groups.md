---
title: aaaDynamic gruppi e collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: "Collaborazione B2B di Azure Active Directory può essere usato con i gruppi dinamici di Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="f7c83-103">Gruppi dinamici e Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7c83-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="f7c83-104">Che cosa sono i gruppi dinamici</span><span class="sxs-lookup"><span data-stu-id="f7c83-104">What are dynamic groups?</span></span>
<span data-ttu-id="f7c83-105">Configurazione dinamica dell'appartenenza al gruppo di sicurezza per Azure Active Directory (Azure AD) è disponibile in [hello Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f7c83-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f7c83-106">Gli amministratori possono impostare regole toopopulate gruppi creati in Azure Active Directory in base agli attributi utente (ad esempio userType, reparto o paese).</span><span class="sxs-lookup"><span data-stu-id="f7c83-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="f7c83-107">I membri possono essere aggiunti automaticamente tooor rimossi da un gruppo di sicurezza in base ai relativi attributi.</span><span class="sxs-lookup"><span data-stu-id="f7c83-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="f7c83-108">Questi gruppi è possono accedere alle risorse tooapplications o cloud (siti di SharePoint, documenti) e tooassign toomembers le licenze.</span><span class="sxs-lookup"><span data-stu-id="f7c83-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="f7c83-109">Per altre informazioni sui gruppi dinamici, vedere [Gruppi dedicati in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="f7c83-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="f7c83-110">Hello appropriato [licenze di Azure AD Premium P1 or P2](https://azure.microsoft.com/pricing/details/active-directory/) è gruppi dinamici toocreate e l'utilizzo richiesti.</span><span class="sxs-lookup"><span data-stu-id="f7c83-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="f7c83-111">Altre informazioni nell'articolo hello [creare regole basate su attributi per l'appartenenza dinamica ai gruppi in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f7c83-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="f7c83-112">Quali sono gruppi dinamici incorporato hello?</span><span class="sxs-lookup"><span data-stu-id="f7c83-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="f7c83-113">Hello **tutti gli utenti** gruppo dinamico consente toocreate amministratori tenant fare clic su un gruppo contenente tutti gli utenti nel tenant di hello con un singolo.</span><span class="sxs-lookup"><span data-stu-id="f7c83-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="f7c83-114">Per impostazione predefinita, hello **tutti gli utenti** gruppo include tutti gli utenti nella directory di hello, inclusi i membri e Guest.</span><span class="sxs-lookup"><span data-stu-id="f7c83-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="f7c83-115">All'interno di hello nuovo Azure Active Directory portale di amministrazione, è possibile scegliere hello tooenable **tutti gli utenti** gruppo hello consente di visualizzare le impostazioni di gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7c83-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![Gruppi predefiniti](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="f7c83-117">Protezione avanzata hello gruppo dinamico di tutti gli utenti</span><span class="sxs-lookup"><span data-stu-id="f7c83-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="f7c83-118">Per impostazione predefinita, hello **tutti gli utenti** gruppo contiene anche gli utenti di collaborazione (guest) B2B.</span><span class="sxs-lookup"><span data-stu-id="f7c83-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="f7c83-119">È possibile proteggere ulteriormente i **tutti gli utenti** gruppo tramite una regola di tooremove utenti guest.</span><span class="sxs-lookup"><span data-stu-id="f7c83-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="f7c83-120">Hello illustrazione che segue hello **tutti gli utenti** modifica del gruppo guests tooexclude.</span><span class="sxs-lookup"><span data-stu-id="f7c83-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![Abilitare il gruppo Tutti gli utenti](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="f7c83-122">Può inoltre risultare utile toocreate un nuovo gruppo dinamico che contiene solo gli utenti guest, in modo che sia possibile applicare toothem criteri (ad esempio criteri di accesso condizionale di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7c83-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="f7c83-123">Un gruppo può avere questo aspetto:</span><span class="sxs-lookup"><span data-stu-id="f7c83-123">What such a group might look like:</span></span>

![Escludere gli utenti guest](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="f7c83-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7c83-125">Next steps</span></span>

<span data-ttu-id="f7c83-126">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="f7c83-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f7c83-127">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="f7c83-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f7c83-128">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="f7c83-129">Aggiunta di un ruolo di tooa utente collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="f7c83-130">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="f7c83-131">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="f7c83-132">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="f7c83-133">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="f7c83-134">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="f7c83-135">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="f7c83-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="f7c83-136">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f7c83-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
