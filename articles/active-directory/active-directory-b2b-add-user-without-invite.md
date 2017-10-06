---
title: gli utenti per la collaborazione B2B aaaAdd tooAzure Active Directory senza un invito | Documenti Microsoft
description: "È possibile consentire a un utente guest di aggiungere altri tooyour utenti guest Azure AD senza Riscatta un invito in collaborazione B2B di Azure Active Directory."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="45dac-103">Aggiungere utenti guest di Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="45dac-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="45dac-104">È possibile consentire a un utente, ad esempio un partner rappresentativo, tooadd gli utenti dell'organizzazione di tooyour hello partner senza la necessità di inviti toobe riscattato.</span><span class="sxs-lookup"><span data-stu-id="45dac-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="45dac-105">È necessario eseguire è concedere privilegi di enumerazione nella directory hello in uso per dell'organizzazione partner hello di tale utente</span><span class="sxs-lookup"><span data-stu-id="45dac-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="45dac-106">Concedere i privilegi nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="45dac-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="45dac-107">Un utente nell'organizzazione di hello host (ad esempio WoodGrove) invita un utente dall'organizzazione partner hello (ad esempio, Sam@litware.com) come Guest.</span><span class="sxs-lookup"><span data-stu-id="45dac-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="45dac-108">salve organizzazione host hello imposta i criteri che consentono di Sam tooidentify e aggiungere altri utenti dell'organizzazione partner hello (Litware).</span><span class="sxs-lookup"><span data-stu-id="45dac-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="45dac-109">Sam ora possibile aggiungere altri utenti dalla directory di Litware toohello WoodGrove, gruppi o le applicazioni senza la necessità di inviti toobe riscattato.</span><span class="sxs-lookup"><span data-stu-id="45dac-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="45dac-110">Se Sam disponga dei privilegi di enumerazione appropriata hello Litware, avviene automaticamente.</span><span class="sxs-lookup"><span data-stu-id="45dac-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="45dac-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45dac-111">Next steps</span></span>

<span data-ttu-id="45dac-112">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="45dac-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="45dac-113">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="45dac-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="45dac-114">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="45dac-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="45dac-115">Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker</span><span class="sxs-lookup"><span data-stu-id="45dac-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="45dac-116">elementi Hello di posta elettronica di invito collaborazione B2B di hello</span><span class="sxs-lookup"><span data-stu-id="45dac-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="45dac-117">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="45dac-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="45dac-118">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="45dac-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="45dac-119">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45dac-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="45dac-120">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45dac-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="45dac-121">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45dac-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="45dac-122">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="45dac-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="45dac-123">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45dac-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)