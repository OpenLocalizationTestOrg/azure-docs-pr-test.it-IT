---
title: Gruppi dinamici e Collaborazione B2B di Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="0153b-103">Gruppi dinamici e Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0153b-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="0153b-104">Che cosa sono i gruppi dinamici</span><span class="sxs-lookup"><span data-stu-id="0153b-104">What are dynamic groups?</span></span>
<span data-ttu-id="0153b-105">La configurazione dinamica dell'appartenenza a gruppi di sicurezza per Azure Active Directory (Azure AD) è disponibile nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0153b-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0153b-106">Gli amministratori possono impostare regole per popolare i gruppi creati in Azure Active Directory in base agli attributi utente, ad esempio tipo di utente, reparto o paese.</span><span class="sxs-lookup"><span data-stu-id="0153b-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="0153b-107">I membri possono essere automaticamente aggiunti o rimossi in un gruppo di sicurezza in base agli attributi.</span><span class="sxs-lookup"><span data-stu-id="0153b-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="0153b-108">Questi gruppi possono fornire accesso ad applicazioni o a risorse cloud, (documenti, siti di SharePoint) e per assegnare licenze ai membri.</span><span class="sxs-lookup"><span data-stu-id="0153b-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="0153b-109">Per altre informazioni sui gruppi dinamici, vedere [Gruppi dedicati in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="0153b-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="0153b-110">La [licenza di Azure AD Premium P1 o P2](https://azure.microsoft.com/pricing/details/active-directory/) appropriata è necessaria per creare e usare gruppi dinamici.</span><span class="sxs-lookup"><span data-stu-id="0153b-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="0153b-111">Maggiori informazioni sono riportate nell’articolo [Creare regole basate su attributi per l'appartenenza dinamica ai gruppi in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0153b-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="0153b-112">Che cosa sono i gruppi dinamici predefiniti</span><span class="sxs-lookup"><span data-stu-id="0153b-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="0153b-113">Il gruppo dinamico **Tutti gli utenti** consente agli amministratori tenant di creare un gruppo contenente tutti gli utenti nel tenant con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="0153b-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="0153b-114">Per impostazione predefinita, il gruppo **Tutti gli utenti** include tutti gli utenti della directory, compresi guest e membri.</span><span class="sxs-lookup"><span data-stu-id="0153b-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="0153b-115">Nel nuovo portale di amministrazione di Azure Active Directory è possibile scegliere di abilitare il gruppo **Tutti gli utenti** nella visualizzazione Impostazioni gruppo.</span><span class="sxs-lookup"><span data-stu-id="0153b-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![Gruppi predefiniti](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="0153b-117">Applicando la protezione avanzata al gruppo dinamico Tutti gli utenti</span><span class="sxs-lookup"><span data-stu-id="0153b-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="0153b-118">Per impostazione predefinita, il gruppo **Tutti gli utenti** contiene anche gli utenti (guest) di Collaborazione B2B.</span><span class="sxs-lookup"><span data-stu-id="0153b-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="0153b-119">È possibile proteggere ulteriormente il gruppo **Tutti gli utenti** tramite una regola di rimozione degli utenti guest.</span><span class="sxs-lookup"><span data-stu-id="0153b-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="0153b-120">La figura seguente illustra il gruppo **Tutti gli utenti** modificato per escludere i guest.</span><span class="sxs-lookup"><span data-stu-id="0153b-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![Abilitare il gruppo Tutti gli utenti](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="0153b-122">Potrebbe inoltre essere utile creare un nuovo gruppo dinamico che contiene solo gli utenti guest, in modo che sia possibile applicare a essi criteri quali, ad esempio, criteri di accesso condizionale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0153b-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="0153b-123">Un gruppo può avere questo aspetto:</span><span class="sxs-lookup"><span data-stu-id="0153b-123">What such a group might look like:</span></span>

![Escludere gli utenti guest](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="0153b-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0153b-125">Next steps</span></span>

<span data-ttu-id="0153b-126">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="0153b-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0153b-127">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="0153b-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="0153b-128">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0153b-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="0153b-129">Aggiunta di un utente di Collaborazione B2B a un ruolo</span><span class="sxs-lookup"><span data-stu-id="0153b-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="0153b-130">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0153b-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="0153b-131">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0153b-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="0153b-132">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0153b-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="0153b-133">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0153b-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="0153b-134">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0153b-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="0153b-135">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="0153b-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="0153b-136">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0153b-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
