---
title: Accesso con Azure MFA tramite verifica in due passaggi | Microsoft Docs
description: Questa pagina offre indicazioni su dove trovare le istruzioni per visualizzare i diversi metodi di accesso disponibili con Azure MFA.
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
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="2ea0a-104">Esperienza di accesso con Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2ea0a-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="2ea0a-105">Lo scopo di questo articolo è di illustrare un'esperienza di accesso tipico.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="2ea0a-106">Per informazioni sull’accesso o per la risoluzione dei problemi, vedere [Problemi con Multi-Factor Authentication di Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="2ea0a-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="2ea0a-107">Come sarà l'esperienza di accesso?</span><span class="sxs-lookup"><span data-stu-id="2ea0a-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="2ea0a-108">L'esperienza di accesso varia a seconda di ciò che si desidera usare come secondo fattore: una telefonata, un'app di autenticazione o un messaggio.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="2ea0a-109">Scegliere l'opzione che meglio descrive l'operazione:</span><span class="sxs-lookup"><span data-stu-id="2ea0a-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="2ea0a-110">Come si accede?</span><span class="sxs-lookup"><span data-stu-id="2ea0a-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="2ea0a-111">Con una telefonata al cellulare o al telefono dell'ufficio</span><span class="sxs-lookup"><span data-stu-id="2ea0a-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="2ea0a-112">Con un messaggio sul cellulare</span><span class="sxs-lookup"><span data-stu-id="2ea0a-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="2ea0a-113">Con le notifiche dell'app Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="2ea0a-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="2ea0a-114">Con i codici di verifica dell'app Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="2ea0a-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="2ea0a-115">Con un metodo alternativo, perché non è possibile usare subito il metodo preferito</span><span class="sxs-lookup"><span data-stu-id="2ea0a-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="2ea0a-116">Accesso tramite telefonata</span><span class="sxs-lookup"><span data-stu-id="2ea0a-116">Signing in with a phone call</span></span>
<span data-ttu-id="2ea0a-117">Le informazioni seguenti descrivono l'esperienza di verifica in due passaggi con una telefonata al cellulare o al telefono dell'ufficio.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="2ea0a-118">Accedere a un'applicazione o servizio come Office 365 usando nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="2ea0a-119">Microsoft telefona all'utente.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="2ea0a-120">Rispondere al telefono e premere il tasto #.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="2ea0a-121">Accesso tramite messaggio di testo</span><span class="sxs-lookup"><span data-stu-id="2ea0a-121">Signing in with a text message</span></span>
<span data-ttu-id="2ea0a-122">Le informazioni seguenti descrivono l'esperienza di verifica in due passaggi tramite messaggio di testo al telefono cellulare:</span><span class="sxs-lookup"><span data-stu-id="2ea0a-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="2ea0a-123">Accedere a un'applicazione o servizio come Office 365 usando nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="2ea0a-124">Microsoft invia un messaggio di testo che contiene un codice numerico.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="2ea0a-125">Immettere il codice nell'apposita casella sulla pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="2ea0a-126">Accesso con l'app Authenticator Microsoft</span><span class="sxs-lookup"><span data-stu-id="2ea0a-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="2ea0a-127">Le informazioni seguenti descrivono l'esperienza d'uso dell'app Microsoft Authenticator per le verifiche in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="2ea0a-128">Esistono due modi diversi di usare l'app.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-128">There are two different ways to use the app.</span></span> <span data-ttu-id="2ea0a-129">È possibile ricevere notifiche push sul dispositivo oppure aprire l'app per ottenere un codice di verifica.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="2ea0a-130">Per eseguire l'accesso con una notifica dell'app Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="2ea0a-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="2ea0a-131">Accedere a un'applicazione o servizio come Office 365 usando nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="2ea0a-132">Microsoft invia una notifica all'app Microsoft Authenticator sul dispositivo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Microsoft invia una notifica](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="2ea0a-134">Aprire la notifica sul telefono e quindi selezionare la chiave **Verifica**.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="2ea0a-135">Se la società richiede un PIN, immetterlo qui.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="2ea0a-136">Ora dovrebbe essere stato effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="2ea0a-137">Per effettuare l'accesso usando un codice di verifica con l'app Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="2ea0a-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="2ea0a-138">Se si usa l'app Microsoft Authenticator per ottenere i codici di verifica, quando si apre l'app viene visualizzato un numero nel nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="2ea0a-139">Questo numero cambia ogni trenta secondi, pertanto non è possibile usare lo stesso numero di due volte.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="2ea0a-140">Quando viene richiesto un codice di verifica, aprire l'app e utilizzare il numero attualmente visualizzato.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="2ea0a-141">Accedere a un'applicazione o servizio come Office 365 usando nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="2ea0a-142">Microsoft richiede un codice di verifica.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-142">Microsoft prompts you for a verification code.</span></span>

  ![Inserire il codice di verifica dell'app](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="2ea0a-144">Aprire l'app Microsoft Authenticator sul telefono e immettere il codice nella casella da cui si sta effettuando l'accesso.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="2ea0a-145">Accesso con un metodo alternativo</span><span class="sxs-lookup"><span data-stu-id="2ea0a-145">Signing in with an alternate method</span></span>
<span data-ttu-id="2ea0a-146">A volte non si dispone del telefono o del dispositivo configurato come metodo di verifica preferito.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="2ea0a-147">Per questo motivo è consigliabile configurare metodi di backup per l'account.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="2ea0a-148">Nella sezione seguente viene mostrato come effettuare l'accesso con un metodo alternativo quando il metodo principale può non essere disponibile.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="2ea0a-149">Accedere a un'applicazione o servizio come Office 365 usando nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="2ea0a-150">Selezionare **Usa un'opzione di verifica diversa**.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="2ea0a-151">Vengono visualizzate diverse opzioni di verifica in base al numero di opzioni configurate.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="2ea0a-152">Scegliere un metodo alternativo ed effettuare l’accesso.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-152">Choose an alternate method and sign in.</span></span>

  ![Utilizzare un metodo alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="2ea0a-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ea0a-154">Next steps</span></span>

<span data-ttu-id="2ea0a-155">In caso di problemi di accesso con la verifica in due passaggi, è possibile ottenere altre informazioni in [Problemi con Multi-Factor Authentication di Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="2ea0a-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="2ea0a-156">Informazioni su come [Gestire le impostazioni della verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="2ea0a-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="2ea0a-157">Altre informazioni sull'[introduzione all'app Microsoft Authenticator](microsoft-authenticator-app-how-to.md) per poter effettuare l'accesso tramite notifiche, invece che con messaggi e telefonate.</span><span class="sxs-lookup"><span data-stu-id="2ea0a-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 