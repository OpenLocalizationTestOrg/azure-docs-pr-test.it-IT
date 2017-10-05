---
title: Delegare gli inviti per Collaborazione B2B di Azure Active Directory | Documentazione Microsoft
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="0742a-103">Delegare gli inviti per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0742a-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="0742a-104">Con Collaborazione B2B (Business-to-Business) di Azure Active Directory (Azure AD) non è necessario essere un amministratore globale per inviare inviti.</span><span class="sxs-lookup"><span data-stu-id="0742a-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="0742a-105">È possibile invece usare i criteri e delegare gli inviti agli utenti nei ruoli a cui è consentito inviare l'invito.</span><span class="sxs-lookup"><span data-stu-id="0742a-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="0742a-106">Un nuovo modo importante per delegare gli inviti di utenti guest consiste nell'usare il ruolo Mittente dell'invito guest.</span><span class="sxs-lookup"><span data-stu-id="0742a-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="0742a-107">Ruolo Mittente dell'invito guest</span><span class="sxs-lookup"><span data-stu-id="0742a-107">Guest Inviter role</span></span>
<span data-ttu-id="0742a-108">È possibile assegnare l'utente al ruolo Mittente dell'invito guest per inviare gli inviti.</span><span class="sxs-lookup"><span data-stu-id="0742a-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="0742a-109">Non è necessario essere membro del ruolo di amministratore globale per inviare gli inviti.</span><span class="sxs-lookup"><span data-stu-id="0742a-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="0742a-110">Per impostazione predefinita, i normali utenti possono anche richiamare l'API di invito, a meno che l'amministratore globale non abbia disabilitato gli inviti per i normali utenti.</span><span class="sxs-lookup"><span data-stu-id="0742a-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="0742a-111">Un utente può chiamare l'API anche usando il portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0742a-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="0742a-112">Ecco un esempio che illustra l'aggiunta di un utente al ruolo Mittente dell'invito guest con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0742a-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="0742a-113">Controllare i mittenti degli inviti</span><span class="sxs-lookup"><span data-stu-id="0742a-113">Control who can invite</span></span>

![Controllare come inviare un invito](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="0742a-115">Con Collaborazione B2B di Azure AD, un amministratore tenant può impostare i criteri di invito seguenti:</span><span class="sxs-lookup"><span data-stu-id="0742a-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="0742a-116">Disattivare gli inviti</span><span class="sxs-lookup"><span data-stu-id="0742a-116">Turn off invitations</span></span>
- <span data-ttu-id="0742a-117">Solo gli amministratori e gli utenti nel ruolo Mittente dell'invito guest possono inviare inviti</span><span class="sxs-lookup"><span data-stu-id="0742a-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="0742a-118">Gli amministratori, il ruolo Mittente dell'invito guest e i membri possono inviare inviti</span><span class="sxs-lookup"><span data-stu-id="0742a-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="0742a-119">Possono inviare inviti tutti gli utenti, inclusi gli utenti guest</span><span class="sxs-lookup"><span data-stu-id="0742a-119">All users, including guests, can invite</span></span>

<span data-ttu-id="0742a-120">Per impostazione predefinita, i tenant sono impostati su 4.</span><span class="sxs-lookup"><span data-stu-id="0742a-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="0742a-121">Tutti gli utenti, inclusi gli utenti guest, possono inviare inviti a utenti B2B.</span><span class="sxs-lookup"><span data-stu-id="0742a-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0742a-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0742a-122">Next steps</span></span>

<span data-ttu-id="0742a-123">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="0742a-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0742a-124">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="0742a-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="0742a-125">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0742a-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="0742a-126">Aggiunta di un utente di Collaborazione B2B a un ruolo</span><span class="sxs-lookup"><span data-stu-id="0742a-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="0742a-127">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0742a-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="0742a-128">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0742a-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="0742a-129">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0742a-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="0742a-130">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0742a-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="0742a-131">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0742a-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="0742a-132">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="0742a-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="0742a-133">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="0742a-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
