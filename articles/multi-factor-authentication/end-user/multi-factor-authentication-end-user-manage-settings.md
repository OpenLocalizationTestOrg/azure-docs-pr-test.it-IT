---
title: Gestire le impostazioni della verifica in due passaggi | Documentazione Microsoft
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
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="27a9f-104">Gestire le impostazioni per la verifica in due passaggi</span><span class="sxs-lookup"><span data-stu-id="27a9f-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="27a9f-105">Questo articolo risponde a domande su come aggiornare le impostazioni della verifica in due passaggi o della Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="27a9f-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="27a9f-106">Se si sono verificati problemi di accesso all'account, vedere le informazioni relative ai [problemi con la verifica in due passaggi](multi-factor-authentication-end-user-troubleshoot.md) che potrebbero essere utili.</span><span class="sxs-lookup"><span data-stu-id="27a9f-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="27a9f-107">Dove trovare la pagina delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="27a9f-107">Where to find the settings page</span></span>
<span data-ttu-id="27a9f-108">In base al modo in cui l'azienda ha configurato Azure Multi-Factor Authentication, le impostazioni come il numero di telefono possono essere modificate in diverse posizioni.</span><span class="sxs-lookup"><span data-stu-id="27a9f-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="27a9f-109">Se l'amministratore IT ha fornito un URL o passaggi specifici per la gestione della verifica in due passaggi, seguire tali istruzioni.</span><span class="sxs-lookup"><span data-stu-id="27a9f-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="27a9f-110">In caso contrario, le istruzioni seguenti dovrebbero funzionare per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="27a9f-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="27a9f-111">Se si esegue questa procedura ma non vengono visualizzate le stesse opzioni, significa che l'azienda o l'istituto di istruzione ha personalizzato il proprio portale.</span><span class="sxs-lookup"><span data-stu-id="27a9f-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="27a9f-112">Chiedere all'amministratore il collegamento al portale di Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="27a9f-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="27a9f-113">Effettuare l'accesso ad [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="27a9f-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="27a9f-114">Selezionare il nome dell'account in alto a destra, quindi selezionare **profilo**.</span><span class="sxs-lookup"><span data-stu-id="27a9f-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="27a9f-115">Selezionare **Verifica aggiuntiva di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="27a9f-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="27a9f-117">La pagina Verifica aggiuntiva di sicurezza viene caricata e mostra le impostazioni attive.</span><span class="sxs-lookup"><span data-stu-id="27a9f-117">The Additional security verification page loads with your settings.</span></span>

    ![Verifica](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="27a9f-119">Si desidera modificare il numero di telefono o aggiungere un numero secondario</span><span class="sxs-lookup"><span data-stu-id="27a9f-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="27a9f-120">È importante configurare un numero di telefono di autenticazione secondario.</span><span class="sxs-lookup"><span data-stu-id="27a9f-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="27a9f-121">Poiché il numero di telefono primario e l'app per dispositivi mobili si trovano probabilmente sullo stesso telefono, il numero di telefono secondario è l'unico modo che consente di accedere di nuovo all'account in caso di perdita o furto del telefono.</span><span class="sxs-lookup"><span data-stu-id="27a9f-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="27a9f-122">Se non si ha accesso al proprio numero di telefono principale e si ha bisogno di assistenza per l'accesso al proprio account, vedere le informazioni relative ai [problemi con la verifica in due passaggi](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="27a9f-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="27a9f-123">**Per modificare il numero di telefono principale:**</span><span class="sxs-lookup"><span data-stu-id="27a9f-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="27a9f-124">Nella pagina Verifica aggiuntiva di sicurezza selezionare la casella di testo con il numero di telefono attuale e modificarla con il nuovo numero di telefono.</span><span class="sxs-lookup"><span data-stu-id="27a9f-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="27a9f-125">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="27a9f-125">Select **Save**.</span></span>  
3. <span data-ttu-id="27a9f-126">Se questo è il numero che si usa per l'opzione di verifica preferita, è necessario verificare il nuovo numero prima di poterlo salvare.</span><span class="sxs-lookup"><span data-stu-id="27a9f-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="27a9f-127">**Per aggiungere un numero di telefono secondario:**</span><span class="sxs-lookup"><span data-stu-id="27a9f-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="27a9f-128">Nella pagina Verifica aggiuntiva di sicurezza selezionare la casella di controllo accanto a **Telefono per l'autenticazione alternativo**.</span><span class="sxs-lookup"><span data-stu-id="27a9f-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="27a9f-129">Immettere il numero di telefono secondario nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="27a9f-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="27a9f-130">Selezionare **Salva** e le modifiche sono terminate.</span><span class="sxs-lookup"><span data-stu-id="27a9f-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="27a9f-131">Richiedere di nuovo la verifica in due passaggi in un dispositivo che è stato contrassegnato come attendibile</span><span class="sxs-lookup"><span data-stu-id="27a9f-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="27a9f-132">A seconda delle impostazioni dell'organizzazione si potrebbe avere una casella di controllo del tipo "Non mostrare più la richiesta per **X** giorni" quando si esegue la verifica in due passaggi nel browser.</span><span class="sxs-lookup"><span data-stu-id="27a9f-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="27a9f-133">Se si seleziona la casella di controllo e poi si perde il dispositivo o si ritiene che l'account sia stato violato, si deve ripristinare la verifica in due passaggi per tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="27a9f-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="27a9f-134">Nella pagina Verifica aggiuntiva di sicurezza selezionare **Ripristina Multi-Factor Authentication nei dispositivi precedentemente attendibili**.</span><span class="sxs-lookup"><span data-stu-id="27a9f-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="27a9f-135">Al successivo accesso da qualsiasi dispositivo verrà richiesto di eseguire la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="27a9f-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="27a9f-136">Come si rimuove Microsoft Authenticator dal dispositivo precedente per passare a un nuovo dispositivo?</span><span class="sxs-lookup"><span data-stu-id="27a9f-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="27a9f-137">Quando si disinstalla l'app dal dispositivo o si ripristina il dispositivo, l'attivazione sul back-end non verrà rimossa.</span><span class="sxs-lookup"><span data-stu-id="27a9f-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="27a9f-138">Per altre informazioni, vedere [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="27a9f-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27a9f-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27a9f-139">Next steps</span></span>
* <span data-ttu-id="27a9f-140">Leggere le informazioni di guida relative ai [problemi con la verifica in due passaggi](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="27a9f-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="27a9f-141">Impostare [password di app](multi-factor-authentication-end-user-app-passwords.md) per tutte le applicazioni che non supportano la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="27a9f-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
