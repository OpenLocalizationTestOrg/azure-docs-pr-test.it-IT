---
title: aaaDelegate inviti per la collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: "Le proprietà di un utente di Collaborazione B2B di Azure Active Directory sono configurabili"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="33eae-103">Delegare gli inviti per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33eae-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="33eae-104">Con la collaborazione business-to-business (B2B) di Azure Active Directory (Azure AD), non si dispone toobe gli inviti toosend un amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="33eae-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="33eae-105">Al contrario, è possibile usare i criteri e delegare toousers inviti con ruoli consentono inviti toosend.</span><span class="sxs-lookup"><span data-stu-id="33eae-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="33eae-106">Un importante nuovo modo toodelegate guest utente inviti è tramite il ruolo di mittente dell'invito Guest hello.</span><span class="sxs-lookup"><span data-stu-id="33eae-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="33eae-107">Ruolo Mittente dell'invito guest</span><span class="sxs-lookup"><span data-stu-id="33eae-107">Guest Inviter role</span></span>
<span data-ttu-id="33eae-108">È possibile assegnare hello utente tooGuest inviti toosend ruolo di mittente dell'invito.</span><span class="sxs-lookup"><span data-stu-id="33eae-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="33eae-109">Non è membro toobe inviti toosend ruolo amministratore globale di hello.</span><span class="sxs-lookup"><span data-stu-id="33eae-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="33eae-110">Per impostazione predefinita, gli utenti standard possono anche richiamare hello invito API a meno che un amministratore globale disabilitata inviti per gli utenti standard.</span><span class="sxs-lookup"><span data-stu-id="33eae-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="33eae-111">Un utente può anche richiamare API hello con hello portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33eae-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="33eae-112">Di seguito è riportato un esempio che illustra come toouse PowerShell tooadd un ruolo di mittente dell'invito Guest toohello utente:</span><span class="sxs-lookup"><span data-stu-id="33eae-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="33eae-113">Controllare i mittenti degli inviti</span><span class="sxs-lookup"><span data-stu-id="33eae-113">Control who can invite</span></span>

![Controllo modalità tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="33eae-115">Con la collaborazione B2B di Azure AD, un amministratore tenant possibile impostare hello base invito ai criteri:</span><span class="sxs-lookup"><span data-stu-id="33eae-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="33eae-116">Disattivare gli inviti</span><span class="sxs-lookup"><span data-stu-id="33eae-116">Turn off invitations</span></span>
- <span data-ttu-id="33eae-117">Solo gli amministratori e gli utenti nel ruolo di mittente dell'invito Guest hello è possono invitare</span><span class="sxs-lookup"><span data-stu-id="33eae-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="33eae-118">Membri, il ruolo di mittente dell'invito Guest hello e amministratori possono invitare</span><span class="sxs-lookup"><span data-stu-id="33eae-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="33eae-119">Possono inviare inviti tutti gli utenti, inclusi gli utenti guest</span><span class="sxs-lookup"><span data-stu-id="33eae-119">All users, including guests, can invite</span></span>

<span data-ttu-id="33eae-120">Per impostazione predefinita, i tenant sono troppo n. 4.</span><span class="sxs-lookup"><span data-stu-id="33eae-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="33eae-121">Tutti gli utenti, inclusi gli utenti guest, possono inviare inviti a utenti B2B.</span><span class="sxs-lookup"><span data-stu-id="33eae-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="33eae-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33eae-122">Next steps</span></span>

<span data-ttu-id="33eae-123">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="33eae-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="33eae-124">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="33eae-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="33eae-125">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="33eae-126">Aggiunta di un ruolo di tooa utente collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="33eae-127">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="33eae-128">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="33eae-129">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="33eae-130">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="33eae-131">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="33eae-132">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="33eae-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="33eae-133">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="33eae-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
