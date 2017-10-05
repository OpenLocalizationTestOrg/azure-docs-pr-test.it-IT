---
title: App Microsoft Authenticator per telefoni cellulari | Documentazione Microsoft
description: "Informazioni su come effettuare l'aggiornamento alla versione più recente di Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="518d8-103">Introduzione all'app Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="518d8-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="518d8-104">L'app Microsoft Authenticator offre un livello di sicurezza aggiuntivo in un account aziendale o dell'istituto di istruzione, ad esempio bsimon@contoso.com, o un account Microsoft, ad esempio bsimon@outlook.com.</span><span class="sxs-lookup"><span data-stu-id="518d8-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="518d8-105">L'app può essere usata in uno dei due modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="518d8-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="518d8-106">**Notifica**.</span><span class="sxs-lookup"><span data-stu-id="518d8-106">**Notification**.</span></span> <span data-ttu-id="518d8-107">L'app consente di impedire l'accesso non autorizzato agli account e arrestare le transazioni illecite effettuando il push di una notifica allo smartphone o al tablet dell'utente.</span><span class="sxs-lookup"><span data-stu-id="518d8-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="518d8-108">È sufficiente visualizzare la notifica e, se legittima, selezionare **Verifica**.</span><span class="sxs-lookup"><span data-stu-id="518d8-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="518d8-109">In caso contrario, è possibile selezionare **Nega**.</span><span class="sxs-lookup"><span data-stu-id="518d8-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="518d8-110">**Codice di verifica**.</span><span class="sxs-lookup"><span data-stu-id="518d8-110">**Verification code**.</span></span> <span data-ttu-id="518d8-111">L'app può essere usata come token software per generare un codice di verifica OAuth.</span><span class="sxs-lookup"><span data-stu-id="518d8-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="518d8-112">Dopo aver inserito il nome utente e la password, si immette il codice fornito dall'app nella schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="518d8-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="518d8-113">Il codice di verifica offre una seconda forma di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="518d8-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="518d8-114">L'app Microsoft Authenticator sostituisce l'app Azure Authenticator.</span><span class="sxs-lookup"><span data-stu-id="518d8-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="518d8-115">L'app Azure Authenticator continua a funzionare, ma questo articolo offre informazioni utili nel caso in cui si decida di passare alla nuova app Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="518d8-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="518d8-116">Fornire il consenso esplicito per la verifica in due passaggi</span><span class="sxs-lookup"><span data-stu-id="518d8-116">Opt in for two-step verification</span></span>

<span data-ttu-id="518d8-117">L'app Microsoft Authenticator non funziona in modo autonomo.</span><span class="sxs-lookup"><span data-stu-id="518d8-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="518d8-118">Configurare ogni account in modo da richiedere un secondo metodo di verifica dopo l'accesso con il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="518d8-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="518d8-119">Per un account aziendale o dell'istituto di istruzione, non è possibile scegliere questa funzionalità in autonomia,</span><span class="sxs-lookup"><span data-stu-id="518d8-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="518d8-120">ma sarà necessario che un amministratore della sicurezza fornisca il consenso esplicito per conto dell'utente e lo inviti a registrare i metodi di verifica per il proprio account.</span><span class="sxs-lookup"><span data-stu-id="518d8-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="518d8-121">Per altre informazioni relative a questo scenario, vedere [Quali sono i vantaggi di Azure Multi-Factor Authentication?](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="518d8-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="518d8-122">Per un account personale, è necessario configurare manualmente la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="518d8-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="518d8-123">Per un account Microsoft, questi passaggi sono disponibili in [Informazioni sulla verifica in due passaggi](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="518d8-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="518d8-124">È possibile usare l'app Microsoft Authenticator anche con account non Microsoft.</span><span class="sxs-lookup"><span data-stu-id="518d8-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="518d8-125">La funzionalità potrebbe avere un nome diverso, ma dovrebbe essere facile da individuare tra le impostazioni di sicurezza o di accesso.</span><span class="sxs-lookup"><span data-stu-id="518d8-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="518d8-126">Installare l'app</span><span class="sxs-lookup"><span data-stu-id="518d8-126">Install the app</span></span>
<span data-ttu-id="518d8-127">L'app Microsoft Authenticator è disponibile per [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072) e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="518d8-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="518d8-128">Aggiungere account all'app</span><span class="sxs-lookup"><span data-stu-id="518d8-128">Add accounts to the app</span></span>
<span data-ttu-id="518d8-129">Per ogni account che si vuole aggiungere all'app Microsoft Authenticator, seguire una delle procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="518d8-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="518d8-130">Aggiungere un account Microsoft personale all'app</span><span class="sxs-lookup"><span data-stu-id="518d8-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="518d8-131">Per un account Microsoft personale (che consente di accedere ad Outlook.com, Xbox, Skype e così via), è sufficiente accedere al proprio account nell'app Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="518d8-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="518d8-132">Aggiungere un account aziendale o dell'istituto di istruzione all'app usando il lettore di codici QR</span><span class="sxs-lookup"><span data-stu-id="518d8-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="518d8-133">Accedere alla schermata delle impostazioni di verifica della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="518d8-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="518d8-134">Per informazioni su come accedere a questa schermata, vedere la sezione relativa alla [modifica delle impostazioni di sicurezza](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="518d8-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="518d8-135">Selezionare la casella accanto ad **App Authenticator** quindi selezionare **Configura**.</span><span class="sxs-lookup"><span data-stu-id="518d8-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![Pulsante Configura nella schermata delle impostazioni di verifica della sicurezza](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="518d8-137">Verrà visualizzata una schermata contenente un codice a matrice.</span><span class="sxs-lookup"><span data-stu-id="518d8-137">This brings up a screen with a QR code on it.</span></span>

    ![Schermata contenente il codice a matrice](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="518d8-139">Aprire l'app Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="518d8-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="518d8-140">Nella schermata **account** selezionare **+** e quindi specificare che si vuole aggiungere un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="518d8-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="518d8-141">Usare la fotocamera per effettuare la scansione del codice a matrice e quindi selezionare **Operazione completata** per chiudere la relativa schermata.</span><span class="sxs-lookup"><span data-stu-id="518d8-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="518d8-142">Se la fotocamera non funziona correttamente è possibile [immettere manualmente il codice a matrice e l'URL](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="518d8-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="518d8-143">Quando l'app mostra il nome dell'account con un codice di sei cifre riportato sotto il nome, la procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="518d8-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Schermata Account](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="518d8-145">Aggiungere manualmente un account all'app</span><span class="sxs-lookup"><span data-stu-id="518d8-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="518d8-146">Accedere alla schermata delle impostazioni di verifica della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="518d8-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="518d8-147">Per informazioni su come accedere a questa schermata, vedere la sezione relativa alla [modifica delle impostazioni di sicurezza](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="518d8-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="518d8-148">Selezionare **Configura**.</span><span class="sxs-lookup"><span data-stu-id="518d8-148">Select **Configure**.</span></span>

    ![Pulsante Configura nella schermata delle impostazioni di verifica della sicurezza](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="518d8-150">Verrà visualizzata una schermata contenente un codice a matrice.</span><span class="sxs-lookup"><span data-stu-id="518d8-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="518d8-151">Prendere nota del codice e dell'URL.</span><span class="sxs-lookup"><span data-stu-id="518d8-151">Note the code and URL.</span></span>

    ![Schermata contenente il codice a matrice e l'URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="518d8-153">Aprire l'app Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="518d8-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="518d8-154">Nella schermata **account** selezionare **+** e quindi specificare che si vuole aggiungere un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="518d8-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="518d8-155">Nello scanner selezionare **In alternativa, immettere il codice manualmente**.</span><span class="sxs-lookup"><span data-stu-id="518d8-155">In the scanner, select **enter code manually**.</span></span>

    ![Schermata per la scansione di un codice a matrice](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="518d8-157">Immettere il codice e l'URL nelle caselle appropriate nell'app, quindi selezionare **Fine**.</span><span class="sxs-lookup"><span data-stu-id="518d8-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![Schermata per l'immissione del codice e dell'URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="518d8-159">Quando l'app mostra il nome dell'account con un codice di sei cifre riportato sotto il nome, la procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="518d8-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Schermata Account](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="518d8-161">Aggiungere un account all'app mediante Touch ID</span><span class="sxs-lookup"><span data-stu-id="518d8-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="518d8-162">In iOS, l'app Microsoft Authenticator supporta Touch ID.</span><span class="sxs-lookup"><span data-stu-id="518d8-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="518d8-163">Azure Multi-Factor Authentication consente alle organizzazioni di richiedere un PIN per i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="518d8-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="518d8-164">Con Touch ID, non è necessario che gli utenti iOS immettano un PIN.</span><span class="sxs-lookup"><span data-stu-id="518d8-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="518d8-165">Possono invece effettuare la scansione della propria impronta digitale e selezionare **Approva**.</span><span class="sxs-lookup"><span data-stu-id="518d8-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="518d8-166">Configurare Touch ID con Microsoft Authenticator è semplice.</span><span class="sxs-lookup"><span data-stu-id="518d8-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="518d8-167">Si completa una normale richiesta di verifica con un PIN.</span><span class="sxs-lookup"><span data-stu-id="518d8-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="518d8-168">Se il dispositivo supporta Touch ID, viene automaticamente configurato per l'account da Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="518d8-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Verifica della configurazione di Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="518d8-170">Successivamente, ogni volta che verrà richiesto di verificare le informazioni di accesso sarà sufficiente selezionare la notifica push ricevuta ed effettuare la scansione della propria impronta digitale anziché immettere il PIN.</span><span class="sxs-lookup"><span data-stu-id="518d8-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Notifica push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="518d8-172">Usare l'app durante l'accesso</span><span class="sxs-lookup"><span data-stu-id="518d8-172">Use the app when you sign in</span></span>

<span data-ttu-id="518d8-173">Dopo che l'account è stato aggiunto all'app, potrebbe essere chiesto di eseguire una verifica di prova per assicurarsi che la configurazione sia corretta.</span><span class="sxs-lookup"><span data-stu-id="518d8-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="518d8-174">Dopo questa verifica, la procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="518d8-174">After that, you're done!</span></span> <span data-ttu-id="518d8-175">Non è necessario fare altro fino al successivo accesso.</span><span class="sxs-lookup"><span data-stu-id="518d8-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="518d8-176">Se si sceglie di usare codici di verifica nell'app, vengono prima visualizzati nella home page.</span><span class="sxs-lookup"><span data-stu-id="518d8-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="518d8-177">Questi codici cambiano ogni 30 secondi in modo da riceverne sempre uno nuovo ogni volta che è necessario.</span><span class="sxs-lookup"><span data-stu-id="518d8-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="518d8-178">Tuttavia, non è necessario fare altro finché non si accede e non viene chiesto di immettere un codice di verifica.</span><span class="sxs-lookup"><span data-stu-id="518d8-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  