---
title: "Considerazioni di progettazione dell'identità ibrida di Azure Active Directory - Determinare i requisiti di Multi-factor Authentication"
description: Il controllo di accesso condizionale consente ad Azure Active Directory di controllare le condizioni specifiche definite durante l'autenticazione dell'utente e prima di consentire l'accesso all'applicazione. Se tali condizioni vengono soddisfatte, l'utente viene autenticato e gli viene consentito l'accesso all'applicazione.
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5b3a8ce6e4203dfb3700f324e32687dd910118af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="9757a-104">Determinare i requisiti dell'autenticazione a più fattori per la soluzione di identità ibrida</span><span class="sxs-lookup"><span data-stu-id="9757a-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="9757a-105">Nell'era della mobilità, in cui gli utenti accedono a dati e applicazioni nel cloud con qualsiasi dispositivo, proteggere queste informazioni è diventata un'esigenza assoluta.</span><span class="sxs-lookup"><span data-stu-id="9757a-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="9757a-106">Ogni giorno viene data notizia di una nuova violazione della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9757a-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="9757a-107">Sebbene non esista una soluzione in grado di fornire una protezione assoluta contro tali violazioni, l'autenticazione a più fattori fornisce un livello aggiuntivo di sicurezza nel tentativo di contrastarle.</span><span class="sxs-lookup"><span data-stu-id="9757a-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="9757a-108">In primo luogo, quindi, è opportuno valutare i requisiti aziendali per l'autenticazione a più fattori,</span><span class="sxs-lookup"><span data-stu-id="9757a-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="9757a-109">ovvero stabilire gli elementi che l'azienda desidera proteggere.</span><span class="sxs-lookup"><span data-stu-id="9757a-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="9757a-110">Questa valutazione è importante per definire i requisiti tecnici a cui attenersi per configurare e abilitare gli utenti aziendali per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="9757a-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="9757a-111">Se non si ha familiarità con l'autenticazione a più fattori, è consigliabile leggere l'articolo [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) prima di andare avanti.</span><span class="sxs-lookup"><span data-stu-id="9757a-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="9757a-112">Accertarsi che venga fornita una risposta alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="9757a-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="9757a-113">L'azienda desidera proteggere anche app Microsoft?</span><span class="sxs-lookup"><span data-stu-id="9757a-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="9757a-114">Come sono state pubblicate queste app?</span><span class="sxs-lookup"><span data-stu-id="9757a-114">How these apps are published?</span></span>
* <span data-ttu-id="9757a-115">L'azienda consente ai dipendenti di accedere alle app locali anche in remoto?</span><span class="sxs-lookup"><span data-stu-id="9757a-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="9757a-116">In caso affermativo, che tipo di accesso remoto offre? È necessario stabilire, infatti, dove si trovano gli utenti che eseguono l'accesso a tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9757a-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="9757a-117">Questa valutazione costituisce un altro elemento di grande importanza per definire una strategia di autenticazione a più fattori appropriata.</span><span class="sxs-lookup"><span data-stu-id="9757a-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="9757a-118">Rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="9757a-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="9757a-119">Dove si troveranno gli utenti?</span><span class="sxs-lookup"><span data-stu-id="9757a-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="9757a-120">Potrebbero trovarsi ovunque?</span><span class="sxs-lookup"><span data-stu-id="9757a-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="9757a-121">L'azienda desidera imporre delle limitazioni in base alla posizione degli utenti?</span><span class="sxs-lookup"><span data-stu-id="9757a-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="9757a-122">Dopo aver identificato questi requisiti, è importante valutare anche i requisiti degli utenti relativamente all'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="9757a-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="9757a-123">Questa valutazione è importante poiché consente di definire i requisiti da soddisfare per implementare l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="9757a-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="9757a-124">Rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="9757a-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="9757a-125">Gli utenti hanno già familiarità con l'autenticazione a più fattori?</span><span class="sxs-lookup"><span data-stu-id="9757a-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="9757a-126">Per alcuni utilizzi verrà prevista una procedura di autenticazione aggiuntiva?</span><span class="sxs-lookup"><span data-stu-id="9757a-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="9757a-127">In caso affermativo, verrà prevista in tutti i casi, solo se provenienti da reti esterne, se accedono ad applicazioni specifiche o in quali altre condizioni?</span><span class="sxs-lookup"><span data-stu-id="9757a-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="9757a-128">Sarà necessario prevedere sessioni di formazione degli utenti sulle modalità per impostare e implementare l'autenticazione a più fattori?</span><span class="sxs-lookup"><span data-stu-id="9757a-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="9757a-129">Quali sono gli scenari principali in cui l'azienda desidera abilitare l'autenticazione a più fattori per gli utenti?</span><span class="sxs-lookup"><span data-stu-id="9757a-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="9757a-130">Dopo aver risposto a queste domande, sarà possibile capire se l'autenticazione a più fattori è già stata implementata in locale.</span><span class="sxs-lookup"><span data-stu-id="9757a-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="9757a-131">Questa valutazione è importante per definire i requisiti tecnici a cui attenersi per configurare e abilitare gli utenti aziendali per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="9757a-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="9757a-132">Rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="9757a-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="9757a-133">L'azienda desidera proteggere account privilegiati con l'autenticazione a più fattori?</span><span class="sxs-lookup"><span data-stu-id="9757a-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="9757a-134">L'azienda intende abilitare l'autenticazione a più fattori in alcune applicazioni per motivi di conformità?</span><span class="sxs-lookup"><span data-stu-id="9757a-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="9757a-135">L'azienda prevede di abilitare l'autenticazione a più fattori per tutti gli utenti di queste applicazioni o solo per gli amministratori?</span><span class="sxs-lookup"><span data-stu-id="9757a-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="9757a-136">È necessario che l'autenticazione a più fattori sia costantemente abilitata o solo quando gli utenti sono collegati da una posizione esterna alla rete aziendale?</span><span class="sxs-lookup"><span data-stu-id="9757a-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="9757a-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9757a-137">Next steps</span></span>
[<span data-ttu-id="9757a-138">Definire una strategia di adozione della soluzione ibrida di gestione delle identità</span><span class="sxs-lookup"><span data-stu-id="9757a-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="9757a-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9757a-139">See also</span></span>
[<span data-ttu-id="9757a-140">Panoramica delle considerazioni di progettazione</span><span class="sxs-lookup"><span data-stu-id="9757a-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

