---
title: "autenticazione a più fattori aaaAzure Accedi con verifica in due passaggi | Documenti Microsoft"
description: Questa pagina forniranno per indicazioni su dove toogo toosee hello vari metodi di accesso disponibili con Azure MFA.
keywords: autenticazione utente, esperienza di accesso con telefono cellulare, accesso con telefono dell'ufficio
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="9c2f0-104">Hello esperienza di accesso con Azure multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9c2f0-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="9c2f0-105">Hello in questo articolo mira toowalk tramite un'esperienza di accesso tipico.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="9c2f0-106">Per informazioni sull'accesso o tootroubleshoot problemi, vedere [problemi con Azure multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="9c2f0-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="9c2f0-107">Come sarà l'esperienza di accesso?</span><span class="sxs-lookup"><span data-stu-id="9c2f0-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="9c2f0-108">L'esperienza di accesso varia a seconda della scelta effettuata toouse come il secondo fattore: una chiamata telefonica, un'app di autenticazione o testi.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="9c2f0-109">Scegliere l'opzione hello che meglio descrive le operazioni:</span><span class="sxs-lookup"><span data-stu-id="9c2f0-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="9c2f0-110">Come si accede?</span><span class="sxs-lookup"><span data-stu-id="9c2f0-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="9c2f0-111">Con un telefono cellulare o dell'ufficio toomy telefonata</span><span class="sxs-lookup"><span data-stu-id="9c2f0-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="9c2f0-112">Con un telefono cellulare toomy testo</span><span class="sxs-lookup"><span data-stu-id="9c2f0-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="9c2f0-113">Le notifiche da app Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="9c2f0-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="9c2f0-114">Con i codici di verifica dall'app Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="9c2f0-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="9c2f0-115">Con un metodo alternativo, perché non è possibile usare subito il metodo preferito</span><span class="sxs-lookup"><span data-stu-id="9c2f0-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="9c2f0-116">Accesso tramite telefonata</span><span class="sxs-lookup"><span data-stu-id="9c2f0-116">Signing in with a phone call</span></span>
<span data-ttu-id="9c2f0-117">le seguenti informazioni Hello descrive telefono dell'ufficio o dell'esperienza di verifica in due passaggi hello mobili tooyour chiamata.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="9c2f0-118">Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="9c2f0-119">Microsoft telefona all'utente.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="9c2f0-120">Rispondere hello telefono e premere il tasto di # hello.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="9c2f0-121">Accesso tramite messaggio di testo</span><span class="sxs-lookup"><span data-stu-id="9c2f0-121">Signing in with a text message</span></span>
<span data-ttu-id="9c2f0-122">le seguenti informazioni Hello descrive hello esperienza di verifica in due passaggi con un telefono cellulare tooyour messaggio testo:</span><span class="sxs-lookup"><span data-stu-id="9c2f0-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="9c2f0-123">Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="9c2f0-124">Microsoft invia un messaggio di testo che contiene un codice numerico.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="9c2f0-125">Immettere il codice hello in hello apposita casella sulla pagina di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="9c2f0-126">Accedere con l'app Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="9c2f0-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="9c2f0-127">Hello informazioni riportate di seguito viene descritta hello esperienza di uso dell'app di Microsoft Authenticator hello per le verifiche in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="9c2f0-128">Esistono due modi diversi toouse hello app.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="9c2f0-129">È possibile ricevere notifiche push sul dispositivo, oppure è possibile aprire hello app tooget un codice di verifica.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="9c2f0-130">toosign con una notifica dall'app Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="9c2f0-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="9c2f0-131">Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="9c2f0-132">Microsoft invia un'app di Microsoft Authenticator toohello notifica sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft invia una notifica](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="9c2f0-134">Notifica di hello aperto sul telefono e seleziona hello **verificare** chiave.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="9c2f0-135">Se la società richiede un PIN, immetterlo qui.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="9c2f0-136">Ora dovrebbe essere stato effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="9c2f0-137">toosign utilizzando un codice di verifica con app Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="9c2f0-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="9c2f0-138">Se si utilizzano i codici di verifica tooget app Authenticator Microsoft hello, quando si apre l'applicazione hello visibili un numero con il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="9c2f0-139">Questo valore cambia ogni 30 secondi in modo che non si utilizza hello stesso numero di due volte.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="9c2f0-140">Quando viene richiesto un codice di verifica, aprire l'applicazione hello e utilizzare il numero è attualmente visualizzato.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="9c2f0-141">Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="9c2f0-142">Microsoft richiede un codice di verifica.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-142">Microsoft prompts you for a verification code.</span></span>

  ![Inserire il codice di verifica dell'app](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="9c2f0-144">Aprire l'app Microsoft Authenticator hello sul telefono e immettere il codice hello nella casella di hello in cui si accede.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="9c2f0-145">Accesso con un metodo alternativo</span><span class="sxs-lookup"><span data-stu-id="9c2f0-145">Signing in with an alternate method</span></span>
<span data-ttu-id="9c2f0-146">Non è a volte hello telefono o un dispositivo che è configurato come metodo di verifica preferita.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="9c2f0-147">Per questo motivo è consigliabile configurare metodi di backup per l'account.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="9c2f0-148">Hello nella sezione seguente illustra come toosign con un metodo alternativo quando il metodo principale potrebbe non essere disponibile.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="9c2f0-149">Accedi tooan applicazione o servizio, ad esempio Office 365 usando il nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="9c2f0-150">Selezionare **Usa un'opzione di verifica diversa**.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="9c2f0-151">Vengono visualizzate diverse opzioni di verifica in base al numero di opzioni configurate.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="9c2f0-152">Scegliere un metodo alternativo ed effettuare l’accesso.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-152">Choose an alternate method and sign in.</span></span>

  ![Utilizzare un metodo alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="9c2f0-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c2f0-154">Next steps</span></span>

<span data-ttu-id="9c2f0-155">In caso di problemi di accesso con la verifica in due passaggi, è possibile ottenere altre informazioni in [Problemi con Multi-Factor Authentication di Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="9c2f0-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="9c2f0-156">Informazioni su come troppo[gestire le impostazioni di verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="9c2f0-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="9c2f0-157">Scoprire come troppo[introduzione app Microsoft Authenticator hello](microsoft-authenticator-app-how-to.md) in modo che è possibile utilizzare le notifiche toosign in, invece di testi e chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="9c2f0-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
