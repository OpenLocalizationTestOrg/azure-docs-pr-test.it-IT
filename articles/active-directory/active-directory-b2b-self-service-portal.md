---
title: portale di iscrizione aaaSelf-service per la collaborazione B2B di Azure Active Directory | Documenti Microsoft
description: "Collaborazione B2B di Active Directory di Azure supporta le relazioni tra società consentendo a partner commerciali tooselectively l'accesso alle applicazioni aziendali"
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
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="21e0a-103">Portale self-service per l'iscrizione a Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="21e0a-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="21e0a-104">I clienti possono eseguire molto con funzionalità incorporate di hello esposte tramite l'amministratore IT [portale di Azure](https://portal.azure.com) e nel [Pannello di accesso dell'applicazione](https://myapps.microsoft.com) per gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="21e0a-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="21e0a-105">Tuttavia anche le aziende necessario flusso di lavoro caricamento hello toocustomize per toofit utenti B2B esigenze della propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="21e0a-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="21e0a-106">È possibile farlo con la [nostra API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="21e0a-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="21e0a-107">Nel corso delle conversazioni intrattenute con i clienti, un'esigenza comune risulta più evidente rispetto a tutte le altre.</span><span class="sxs-lookup"><span data-stu-id="21e0a-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="21e0a-108">Hello si invitano organizzazione potrebbe non sapere anticipatamente che hello singoli collaboratori esterni sono che devono accedere alle risorse di tootheir.</span><span class="sxs-lookup"><span data-stu-id="21e0a-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="21e0a-109">Volevano un modo per gli utenti dei partner commerciali troppo iscriversi autonomamente con un set di criteri che hello si invitano i controlli dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="21e0a-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="21e0a-110">Questo scenario è possibile tramite le API ed è quindi stato pubblicato un [progetto Github di esempio](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="21e0a-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="21e0a-111">Il progetto Github viene illustrato come le organizzazioni possono usare le API e forniscono una funzionalità di sottoscrizione basata su criteri self-service per i relativi partner attendibili, con regole che determinano le app hello che possono accedere.</span><span class="sxs-lookup"><span data-stu-id="21e0a-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="21e0a-112">Gli utenti partner è possono ottenere accesso tooresources quando sono necessari, in modo sicuro, senza richiedere hello si invitano caricare toomanually organizzazione li.</span><span class="sxs-lookup"><span data-stu-id="21e0a-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="21e0a-113">È possibile distribuire facilmente progetto hello in una sottoscrizione di Azure di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="21e0a-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="21e0a-114">Codice cosi com’è</span><span class="sxs-lookup"><span data-stu-id="21e0a-114">As-is code</span></span>

<span data-ttu-id="21e0a-115">Tenere presente che questo codice viene fornito come un esempio di utilizzo di invito hello B2B di Azure Active Directory API toodemonstrate.</span><span class="sxs-lookup"><span data-stu-id="21e0a-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="21e0a-116">Deve essere preferibilmente personalizzato dal team di sviluppo o da un partner ed esaminato prima di essere distribuito in uno scenario di produzione.</span><span class="sxs-lookup"><span data-stu-id="21e0a-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e0a-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21e0a-117">Next steps</span></span>

<span data-ttu-id="21e0a-118">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="21e0a-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="21e0a-119">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="21e0a-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="21e0a-120">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="21e0a-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="21e0a-121">Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker</span><span class="sxs-lookup"><span data-stu-id="21e0a-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="21e0a-122">elementi Hello di posta elettronica di invito collaborazione B2B di hello</span><span class="sxs-lookup"><span data-stu-id="21e0a-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="21e0a-123">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="21e0a-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="21e0a-124">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="21e0a-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="21e0a-125">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21e0a-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="21e0a-126">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21e0a-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="21e0a-127">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="21e0a-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="21e0a-128">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="21e0a-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="21e0a-129">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21e0a-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)