---
title: 'Azure Active Directory B2C: disabilitare la verifica tramite posta elettronica durante l''iscrizione dell''utente | Documentazione Microsoft'
description: Un argomento che illustra come toodisable posta elettronica di verifica durante l'iscrizione in Azure Active Directory B2C consumer
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="3596f-103">Azure Active Directory B2C: disabilitare la verifica tramite posta elettronica durante l'iscrizione dell'utente</span><span class="sxs-lookup"><span data-stu-id="3596f-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="3596f-104">Quando abilitata, B2C Azure Active Directory (Azure AD) offre un consumer hello toosign possibilità per applicazioni fornendo un indirizzo di posta elettronica e la creazione di un account locale.</span><span class="sxs-lookup"><span data-stu-id="3596f-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="3596f-105">Azure Active Directory B2C assicura gli indirizzi di posta elettronica valido richiedendo consumer tooverify loro durante il processo di iscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="3596f-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="3596f-106">Impedisce inoltre un processo automatizzato dannoso la generazione di un account fittizio per le applicazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="3596f-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="3596f-107">Alcuni sviluppatori di applicazioni preferiscono tooskip verifica della posta elettronica durante il processo di iscrizione hello e invece che disponga di consumer verifica indirizzo di posta elettronica hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="3596f-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="3596f-108">toosupport, Azure AD B2C può essere configurato toodisable verifica della posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="3596f-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="3596f-109">In questo modo viene creato un processo di iscrizione più uniforme e offre agli sviluppatori hello flessibilità toodifferentiate hello i consumer accertato l'indirizzo di posta elettronica da tali utenti che non siano.</span><span class="sxs-lookup"><span data-stu-id="3596f-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="3596f-110">Per impostazione predefinita, nei criteri di iscrizione la verifica tramite posta elettronica è abilitata.</span><span class="sxs-lookup"><span data-stu-id="3596f-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="3596f-111">Utilizzare hello seguendo i passaggi tooturn disattivata:</span><span class="sxs-lookup"><span data-stu-id="3596f-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="3596f-112">[Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="3596f-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="3596f-113">Fare clic su **Criteri di iscrizione** o su **Criteri di iscrizione o di accesso**, a seconda della configurazione usata per l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="3596f-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="3596f-114">Fare clic su tooopen i criteri (ad esempio, "B2C_1_SiUp") è.</span><span class="sxs-lookup"><span data-stu-id="3596f-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="3596f-115">Fare clic su **modifica** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="3596f-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="3596f-116">Fare clic su **Personalizzazione dell'interfaccia utente della pagina**.</span><span class="sxs-lookup"><span data-stu-id="3596f-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="3596f-117">Fare clic su **Pagina di iscrizione dell'account locale**.</span><span class="sxs-lookup"><span data-stu-id="3596f-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="3596f-118">Fare clic su **indirizzo di posta elettronica** in hello **nome** colonna sotto hello **attributi iscrizione** sezione.</span><span class="sxs-lookup"><span data-stu-id="3596f-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="3596f-119">Hello attiva/disattiva **Richiedi verifica** opzione troppo**n**.</span><span class="sxs-lookup"><span data-stu-id="3596f-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="3596f-120">Fare clic su **OK** nella parte inferiore di hello fino a raggiungere hello **Modifica criterio** blade.</span><span class="sxs-lookup"><span data-stu-id="3596f-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="3596f-121">Fare clic su **salvare** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="3596f-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="3596f-122">L'operazione è completata.</span><span class="sxs-lookup"><span data-stu-id="3596f-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="3596f-123">Disabilitare la verifica tramite posta elettronica nel processo di iscrizione hello può causare toospam.</span><span class="sxs-lookup"><span data-stu-id="3596f-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="3596f-124">Se si disabilita predefinito hello, è consigliabile aggiungere il sistema di verifica.</span><span class="sxs-lookup"><span data-stu-id="3596f-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="3596f-125">Ci sono sempre toofeedback aperti e i suggerimenti!</span><span class="sxs-lookup"><span data-stu-id="3596f-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="3596f-126">Se si hanno difficoltà a questo argomento o avere indicazioni per migliorare il contenuto, Gradiremmo commenti e suggerimenti nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3596f-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="3596f-127">Per le richieste di funzionalità, aggiungerli troppo[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="3596f-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
