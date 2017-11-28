---
title: aaaManage le impostazioni di verifica in due passaggi | Documenti Microsoft
description: Gestire l'utilizzo di Azure Multi-Factor Authentication, inclusa la modifica delle informazioni di contatto e la configurazione dei dispositivi.
services: multi-factor-authentication
keywords: client di multi-factor authentication, problema di autenticazione, ID di correlazione
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="1b787-104">Gestire le impostazioni per la verifica in due passaggi</span><span class="sxs-lookup"><span data-stu-id="1b787-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="1b787-105">In questo articolo risponde alle domande sul tooupdate impostazioni per l'autenticazione a più fattori o di verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="1b787-105">This article answers questions about how tooupdate settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="1b787-106">Se si sono verificati problemi di accesso account tooyour, fare riferimento troppo[problemi con la verifica](multi-factor-authentication-end-user-troubleshoot.md) per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="1b787-106">If you are having issues signing in tooyour account, refer too[Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-toofind-hello-settings-page"></a><span data-ttu-id="1b787-107">Dove toofind hello pagina Impostazioni</span><span class="sxs-lookup"><span data-stu-id="1b787-107">Where toofind hello settings page</span></span>
<span data-ttu-id="1b787-108">In base al modo in cui l'azienda ha configurato Azure Multi-Factor Authentication, le impostazioni come il numero di telefono possono essere modificate in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="1b787-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="1b787-109">Se l'amministratore IT inviato un URL specifico o di verifica in due passaggi toomanage di passaggi, seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="1b787-109">If your IT admin sent out a specific URL or steps toomanage two-step verification, follow those instructions.</span></span> <span data-ttu-id="1b787-110">In caso contrario, hello attenendosi alle istruzioni dovrebbe funzionare per qualsiasi altro utente.</span><span class="sxs-lookup"><span data-stu-id="1b787-110">Otherwise, hello following instructions should work for everybody else.</span></span> <span data-ttu-id="1b787-111">Se questa procedura, ma non viene visualizzato hello stesse opzioni, che significa che l'azienda o dell'istituto di istruzione proprio portale personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1b787-111">If you follow these steps but don't see hello same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="1b787-112">Chiedere all'amministratore per il portale di Azure multi-Factor Authentication tooyour collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1b787-112">Ask your admin for hello link tooyour Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="1b787-113">Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="1b787-113">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="1b787-114">Selezionare il nome dell'account in hello in alto a destra, quindi selezionare **profilo**.</span><span class="sxs-lookup"><span data-stu-id="1b787-114">Select your account name in hello top right, then select **profile**.</span></span>  
3. <span data-ttu-id="1b787-115">Selezionare **Verifica aggiuntiva di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="1b787-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="1b787-117">pagina verifica aggiuntiva di sicurezza di Hello carica le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1b787-117">hello Additional security verification page loads with your settings.</span></span>

    ![Verifica](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="1b787-119">Si desidera toochange numero di telefono o aggiungere un numero secondario</span><span class="sxs-lookup"><span data-stu-id="1b787-119">I want toochange my phone number, or add a secondary number</span></span>
<span data-ttu-id="1b787-120">È importante tooconfigure un numero di telefono di autenticazione secondaria.</span><span class="sxs-lookup"><span data-stu-id="1b787-120">It is important tooconfigure a secondary authentication phone number.</span></span>  <span data-ttu-id="1b787-121">Poiché primario phone numero e app per dispositivi mobili sono probabilmente in hello stesso telefono, il numero di telefono secondario di hello è unico modo hello sarà in grado di tooget nuovamente al tuo account se il telefono viene smarrito o rubato.</span><span class="sxs-lookup"><span data-stu-id="1b787-121">Because your primary phone number and your mobile app are probably on hello same phone, hello secondary phone number is hello only way you will be able tooget back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="1b787-122">Se non hanno accesso tooyour numero di telefono principale e assistenza durante il recupero dell'account tooyour, vedere la Guida in [problemi con la verifica](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="1b787-122">If you don't have access tooyour primary phone number, and need help getting in tooyour account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="1b787-123">**toochange numero di telefono primario:**</span><span class="sxs-lookup"><span data-stu-id="1b787-123">**toochange your primary phone number:**</span></span>  

1. <span data-ttu-id="1b787-124">Nella pagina verifica aggiuntiva di sicurezza di hello, selezionare la casella di testo hello con il numero di telefono corrente e modificarla con il nuovo numero di telefono.</span><span class="sxs-lookup"><span data-stu-id="1b787-124">On hello Additional security verification page, select hello text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="1b787-125">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1b787-125">Select **Save**.</span></span>  
3. <span data-ttu-id="1b787-126">Se si tratta numero hello che verrà usata per l'opzione di verifica preferita, è necessario nuovo numero di tooverify hello prima di poter salvare.</span><span class="sxs-lookup"><span data-stu-id="1b787-126">If this is hello number that you use for your preferred verification option, you have tooverify hello new number before you can save it.</span></span>  

<span data-ttu-id="1b787-127">**tooadd un numero di telefono secondario:**</span><span class="sxs-lookup"><span data-stu-id="1b787-127">**tooadd a secondary phone number:**</span></span>  

1. <span data-ttu-id="1b787-128">Nella pagina verifica aggiuntiva di sicurezza di hello, casella di controllo hello accanto troppo**telefono per l'autenticazione alternativo.**</span><span class="sxs-lookup"><span data-stu-id="1b787-128">On hello Additional security verification page, check hello box next too**Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="1b787-129">Immettere il numero di telefono secondario nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="1b787-129">Enter your secondary phone number in hello text box.</span></span>  
3. <span data-ttu-id="1b787-130">Selezionare **Salva** e le modifiche sono terminate.</span><span class="sxs-lookup"><span data-stu-id="1b787-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="1b787-131">Richiedere di nuovo la verifica in due passaggi in un dispositivo che è stato contrassegnato come attendibile</span><span class="sxs-lookup"><span data-stu-id="1b787-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="1b787-132">A seconda delle impostazioni dell'organizzazione si potrebbe avere una casella di controllo del tipo "Non mostrare più la richiesta per **X** giorni" quando si esegue la verifica in due passaggi nel browser.</span><span class="sxs-lookup"><span data-stu-id="1b787-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="1b787-133">Se questa casella di controllo e quindi perde il dispositivo o ritiene che l'account è compromessa, è necessario ripristinare i dispositivi tooall verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="1b787-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification tooall your devices.</span></span> 

1. <span data-ttu-id="1b787-134">Nella pagina verifica aggiuntiva di sicurezza hello selezionare **ripristino multi-factor authentication per dispositivi precedentemente attendibili**.</span><span class="sxs-lookup"><span data-stu-id="1b787-134">On hello Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="1b787-135">Hello successivo che si accede in qualsiasi dispositivo, sarà richiesta tooperform la verifica.</span><span class="sxs-lookup"><span data-stu-id="1b787-135">hello next time you sign in on any device, you'll be prompted tooperform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a><span data-ttu-id="1b787-136">Come pulire Microsoft Authenticator dalla periferica precedente e spostare tooa uno nuovo?</span><span class="sxs-lookup"><span data-stu-id="1b787-136">How do I clean up Microsoft Authenticator from my old device and move tooa new one?</span></span>
<span data-ttu-id="1b787-137">Quando si disinstalla l'applicazione hello dal dispositivo o la reimpostazione hello dispositivo, ma non attivazione hello back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1b787-137">When you uninstall hello app from your device or reset hello device, it does not remove hello activation on hello back end.</span></span> <span data-ttu-id="1b787-138">Per altre informazioni, vedere [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="1b787-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b787-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b787-139">Next steps</span></span>
* <span data-ttu-id="1b787-140">Leggere le informazioni di guida relative ai [problemi con la verifica in due passaggi](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="1b787-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="1b787-141">Impostare [password di app](multi-factor-authentication-end-user-app-passwords.md) per tutte le applicazioni che non supportano la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="1b787-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
