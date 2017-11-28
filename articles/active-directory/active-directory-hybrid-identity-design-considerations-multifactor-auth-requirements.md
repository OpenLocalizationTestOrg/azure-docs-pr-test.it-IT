---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di autenticazione a più fattori"
description: "Con il controllo di accesso condizionale, Azure Active Directory verifica specifiche condizioni hello selezionate per l'autenticazione utente hello e prima di consentire l'accesso toohello applicazione. Quando queste condizioni sono soddisfatte, l'utente di hello è autenticato e accesso toohello applicazione consentita."
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
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="96a75-104">Determinare i requisiti dell'autenticazione a più fattori per la soluzione di identità ibrida</span><span class="sxs-lookup"><span data-stu-id="96a75-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="96a75-105">In questo mondo di mobilità, con utenti che accedono ai dati e applicazioni nel cloud hello e da qualsiasi dispositivo, è diventato fondamentale proteggere queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="96a75-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="96a75-106">Ogni giorno viene data notizia di una nuova violazione della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="96a75-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="96a75-107">Tuttavia, non c'è garanzia contro tali violazioni della sicurezza, autenticazione a più fattori, offre un ulteriore livello di sicurezza toohelp evitare tali violazioni.</span><span class="sxs-lookup"><span data-stu-id="96a75-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="96a75-108">Avviare la valutazione dei requisiti delle organizzazioni hello multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="96a75-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="96a75-109">Che cos'è toosecure durante il tentativo di hello dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="96a75-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="96a75-110">Questa valutazione è requisiti tecnici di hello toodefine importanti per la configurazione e consentire agli utenti di organizzazioni hello multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="96a75-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="96a75-111">Se non si ha familiarità con l'autenticazione a più fattori e funzionalità, è consigliabile leggere l'articolo hello [che cos'è Azure multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) precedente toocontinue leggere questa sezione.</span><span class="sxs-lookup"><span data-stu-id="96a75-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="96a75-112">Verificare i seguenti hello tooanswer che:</span><span class="sxs-lookup"><span data-stu-id="96a75-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="96a75-113">L'azienda sta tentando toosecure Microsoft App?</span><span class="sxs-lookup"><span data-stu-id="96a75-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="96a75-114">Come sono state pubblicate queste app?</span><span class="sxs-lookup"><span data-stu-id="96a75-114">How these apps are published?</span></span>
* <span data-ttu-id="96a75-115">La società fornisce accesso remoto tooallow dipendenti tooaccess locale App?</span><span class="sxs-lookup"><span data-stu-id="96a75-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="96a75-116">In caso affermativo, il tipo di accesso remoto? È inoltre necessario tooevaluate in cui gli utenti di hello che accedono a tali applicazioni verranno memorizzati.</span><span class="sxs-lookup"><span data-stu-id="96a75-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="96a75-117">Questa valutazione è un'altra strategia di autenticazione a più fattori corretta hello di toodefine passaggio importante.</span><span class="sxs-lookup"><span data-stu-id="96a75-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="96a75-118">Verificare che hello tooanswer seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="96a75-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="96a75-119">Dove si trovano toobe utenti hello?</span><span class="sxs-lookup"><span data-stu-id="96a75-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="96a75-120">Potrebbero trovarsi ovunque?</span><span class="sxs-lookup"><span data-stu-id="96a75-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="96a75-121">L'azienda vuole tooestablish restrizioni in base della posizione dell'utente toohello?</span><span class="sxs-lookup"><span data-stu-id="96a75-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="96a75-122">Dopo aver appreso questi requisiti, è importante tooalso valutare i requisiti dell'utente hello multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="96a75-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="96a75-123">Questa valutazione è importante perché definirà i requisiti di hello per l'implementazione di multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="96a75-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="96a75-124">Verificare che hello tooanswer seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="96a75-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="96a75-125">Si ha familiarità con l'autenticazione a più fattori utenti hello?</span><span class="sxs-lookup"><span data-stu-id="96a75-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="96a75-126">Alcuni utilizzi sarà l'autenticazione aggiuntiva tooprovide necessarie?</span><span class="sxs-lookup"><span data-stu-id="96a75-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="96a75-127">In caso affermativo, tutti hello tempo, quando provenienti da reti esterne o accesso alle applicazioni specifiche o in altre condizioni?</span><span class="sxs-lookup"><span data-stu-id="96a75-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="96a75-128">Gli utenti di hello dovranno come toosetup e implementare l'autenticazione a più fattori?</span><span class="sxs-lookup"><span data-stu-id="96a75-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="96a75-129">Quali sono gli scenari principali di hello che la società decide tooenable multi-factor authentication per gli utenti?</span><span class="sxs-lookup"><span data-stu-id="96a75-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="96a75-130">Dopo aver rispondere alle domande precedenti hello, si sarà in grado di toounderstand se esistono già implementata l'autenticazione a più fattori locale.</span><span class="sxs-lookup"><span data-stu-id="96a75-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="96a75-131">Questa valutazione è requisiti tecnici di hello toodefine importanti per la configurazione e consentire agli utenti di organizzazioni hello multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="96a75-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="96a75-132">Verificare che hello tooanswer seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="96a75-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="96a75-133">L'azienda necessita di account con privilegi tooprotect con autenticazione a più fattori?</span><span class="sxs-lookup"><span data-stu-id="96a75-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="96a75-134">L'azienda necessita tooenable autenticazione a più fattori per alcune applicazioni per motivi di conformità?</span><span class="sxs-lookup"><span data-stu-id="96a75-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="96a75-135">L'azienda necessita tooenable autenticazione a più fattori per tutti gli utenti idonei di queste applicazioni o solo gli amministratori?</span><span class="sxs-lookup"><span data-stu-id="96a75-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="96a75-136">È necessario sono sempre abilitati con autenticazione a più fattori o solo quando sono connessi utenti hello all'esterno della rete aziendale?</span><span class="sxs-lookup"><span data-stu-id="96a75-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="96a75-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96a75-137">Next steps</span></span>
[<span data-ttu-id="96a75-138">Definire una strategia di adozione della soluzione ibrida di gestione delle identità</span><span class="sxs-lookup"><span data-stu-id="96a75-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="96a75-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="96a75-139">See also</span></span>
[<span data-ttu-id="96a75-140">Panoramica delle considerazioni di progettazione</span><span class="sxs-lookup"><span data-stu-id="96a75-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

