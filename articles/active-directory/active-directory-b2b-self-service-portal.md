---
title: Portale di iscrizione self-service per Collaborazione B2B di Azure Active Directory | Microsoft Docs
description: "La collaborazione B2B di Azure Active Directory supporta le relazioni tra società abilitando i partner commerciali ad accedere in modo selettivo alle applicazioni aziendali"
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
ms.openlocfilehash: 307373c75bbb87cec683f7a3097f8f159c9d5e61
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="20e62-103">Portale self-service per l'iscrizione a Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e62-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="20e62-104">I clienti possono eseguire molte operazioni con le funzionalità predefinite esposte tramite il [portale di Azure](https://portal.azure.com) per gli amministratori IT e il [pannello di accesso alle applicazioni](https://myapps.microsoft.com) per gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="20e62-104">Customers can do a lot with the built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="20e62-105">Le aziende hanno tuttavia bisogno di personalizzare il flusso di lavoro di onboarding per gli utenti B2B in base alle esigenze della propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="20e62-105">But we are also aware that businesses need to customize the onboarding workflow for B2B users to fit their organization’s needs.</span></span> <span data-ttu-id="20e62-106">È possibile farlo con la [nostra API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="20e62-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="20e62-107">Nel corso delle conversazioni intrattenute con i clienti, un'esigenza comune risulta più evidente rispetto a tutte le altre.</span><span class="sxs-lookup"><span data-stu-id="20e62-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="20e62-108">L'organizzazione che emette inviti potrebbe non sapere in anticipo quali singoli collaboratori esterni avranno bisogno di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="20e62-108">The inviting organization may not know ahead of time who the individual external collaborators are who need access to their resources.</span></span> <span data-ttu-id="20e62-109">È quindi necessario un modo che consenta agli utenti delle aziende partner di effettuare l'iscrizione con un set di criteri controllati dall'organizzazione che emette gli inviti.</span><span class="sxs-lookup"><span data-stu-id="20e62-109">They wanted a way for users from partner companies to  sign themselves up with a set of policies that the inviting organization controls.</span></span> <span data-ttu-id="20e62-110">Questo scenario è possibile tramite le API ed è quindi stato pubblicato un [progetto Github di esempio](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="20e62-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="20e62-111">Il progetto Github illustra come le organizzazioni possono usare le API e offrire ai partner attendibili una funzionalità di iscrizione self-service basata su criteri, con regole che determinano le app a cui potranno accedere.</span><span class="sxs-lookup"><span data-stu-id="20e62-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine the apps they can access.</span></span> <span data-ttu-id="20e62-112">Gli utenti partner possono ottenere l'accesso alle risorse quando necessario, in modo sicuro, senza che l'organizzazione che emette l'invito debba eseguirne manualmente l'onboarding.</span><span class="sxs-lookup"><span data-stu-id="20e62-112">Partner users can get access to resources when they need them, securely, without requiring the inviting organization to manually onboard them.</span></span> <span data-ttu-id="20e62-113">È possibile distribuire facilmente il progetto in una sottoscrizione di Azure di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="20e62-113">You can easily deploy the project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="20e62-114">Codice cosi com’è</span><span class="sxs-lookup"><span data-stu-id="20e62-114">As-is code</span></span>

<span data-ttu-id="20e62-115">Tenere presente che questo codice viene reso disponibile come esempio per illustrare l'utilizzo dell'API di invito B2B di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="20e62-115">Remember that this code is made available as a sample to demonstrate usage of the Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="20e62-116">Deve essere preferibilmente personalizzato dal team di sviluppo o da un partner ed esaminato prima di essere distribuito in uno scenario di produzione.</span><span class="sxs-lookup"><span data-stu-id="20e62-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20e62-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20e62-117">Next steps</span></span>

<span data-ttu-id="20e62-118">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="20e62-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="20e62-119">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="20e62-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="20e62-120">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="20e62-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="20e62-121">Procedura di aggiunta di utenti di Collaborazione B2B da parte di information worker</span><span class="sxs-lookup"><span data-stu-id="20e62-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="20e62-122">Elementi del messaggio di posta elettronica di invito per la Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="20e62-122">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="20e62-123">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="20e62-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="20e62-124">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="20e62-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="20e62-125">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20e62-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="20e62-126">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20e62-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="20e62-127">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="20e62-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="20e62-128">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="20e62-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="20e62-129">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20e62-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)