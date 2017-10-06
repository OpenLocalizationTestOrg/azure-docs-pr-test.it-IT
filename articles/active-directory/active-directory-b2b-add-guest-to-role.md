---
title: ruolo di tooa aaaAdd un B2B di Azure Active Directory collaborazione utente | Documenti Microsoft
description: Aggiungere un ruolo di tooa utente guest in Azure Active Directory
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
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="821bd-103">Concedere le autorizzazioni toousers di organizzazioni partner nel tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="821bd-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="821bd-104">Gli utenti di collaborazione B2B di Active Directory (Azure AD) Azure vengono aggiunti come directory di toohello utenti guest e le autorizzazioni guest nella directory hello sono limitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="821bd-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="821bd-105">L'azienda potrebbe essere necessario alcuni ruoli del privilegio superiore toofill utenti guest all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="821bd-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="821bd-106">toosupport definizione dei ruoli di privilegio superiore, gli utenti guest possono essere aggiunto tooany ruoli desiderati, in base alle esigenze dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="821bd-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="821bd-107">Ruolo predefinito</span><span class="sxs-lookup"><span data-stu-id="821bd-107">Default role</span></span>

![ruolo predefinito](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="821bd-109">Ruolo Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="821bd-109">Global Administrator Role</span></span>

![ruolo Amministratore globale](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="821bd-111">Ruolo Amministratore con limitazioni</span><span class="sxs-lookup"><span data-stu-id="821bd-111">Limited Administrator Role</span></span>

![ruolo Amministratore con limitazioni](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="821bd-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="821bd-113">Next steps</span></span>

<span data-ttu-id="821bd-114">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="821bd-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="821bd-115">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="821bd-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="821bd-116">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="821bd-117">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="821bd-118">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="821bd-119">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="821bd-120">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="821bd-121">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="821bd-122">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="821bd-123">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="821bd-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="821bd-124">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="821bd-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
