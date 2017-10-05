---
title: Aggiungere utenti di Collaborazione B2B ad Azure Active Directory senza invito | Microsoft Docs
description: "È possibile consentire a un utente guest di aggiungere altri utenti guest ad Azure Active Directory senza riscattare un invito in Collaborazione B2B di Azure Active Directory."
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
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="1a916-103">Aggiungere utenti guest di Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="1a916-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="1a916-104">È possibile consentire a un utente, ad esempio un rappresentante dei partner, di aggiungere utenti dal partner all'organizzazione senza la necessità di riscattare gli inviti.</span><span class="sxs-lookup"><span data-stu-id="1a916-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="1a916-105">È sufficiente concedere all'utente i privilegi di enumerazione nella directory in uso per l'organizzazione del partner.</span><span class="sxs-lookup"><span data-stu-id="1a916-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="1a916-106">Concedere i privilegi nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a916-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="1a916-107">Un utente dell'organizzazione host (ad esempio WoodGrove) invita un utente dell'organizzazione partner (ad esempio Sam@litware.com) come guest.</span><span class="sxs-lookup"><span data-stu-id="1a916-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="1a916-108">L'amministratore dell'organizzazione host configura criteri che consentono a Sam di identificare e aggiungere altri utenti dall'organizzazione partner (Litware).</span><span class="sxs-lookup"><span data-stu-id="1a916-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="1a916-109">Ora Sam può aggiungere altri utenti da Litware alla directory, ai gruppi o alle applicazioni di WoodGrove senza la necessità di riscattare gli inviti.</span><span class="sxs-lookup"><span data-stu-id="1a916-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="1a916-110">Se Sam dispone dei privilegi di enumerazione appropriati in Litware, l'operazione viene eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1a916-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="1a916-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a916-111">Next steps</span></span>

<span data-ttu-id="1a916-112">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="1a916-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1a916-113">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="1a916-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1a916-114">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="1a916-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="1a916-115">Procedura di aggiunta di utenti di Collaborazione B2B da parte di information worker</span><span class="sxs-lookup"><span data-stu-id="1a916-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="1a916-116">Elementi del messaggio di posta elettronica di invito per la Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="1a916-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="1a916-117">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="1a916-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="1a916-118">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a916-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="1a916-119">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a916-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="1a916-120">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a916-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="1a916-121">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a916-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="1a916-122">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="1a916-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="1a916-123">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a916-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)