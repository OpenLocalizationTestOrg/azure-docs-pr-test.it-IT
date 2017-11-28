---
title: autenticazione aaaAdd in Android con App per dispositivi mobili | Documenti Microsoft
description: "Informazioni su come toouse hello funzionalità delle App per dispositivi mobili degli utenti di tooauthenticate di servizio App di Azure di app Android tramite un'ampia varietà di provider di identità, tra cui Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="acfa3-103">Aggiungere app per Android tooyour autenticazione</span><span class="sxs-lookup"><span data-stu-id="acfa3-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="acfa3-104">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="acfa3-104">Summary</span></span>
<span data-ttu-id="acfa3-105">In questa esercitazione, aggiungere progetto di avvio rapido di autenticazione toohello todolist in Android tramite un provider di identità supportati.</span><span class="sxs-lookup"><span data-stu-id="acfa3-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="acfa3-106">In questa esercitazione si basa sull'hello [Introduzione a Mobile app] esercitazione, è necessario completare prima.</span><span class="sxs-lookup"><span data-stu-id="acfa3-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="acfa3-107"><a name="register"></a>Registrare l'app per l'autenticazione e configurare Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="acfa3-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="acfa3-108"><a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app</span><span class="sxs-lookup"><span data-stu-id="acfa3-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="acfa3-109">L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app.</span><span class="sxs-lookup"><span data-stu-id="acfa3-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="acfa3-110">App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="acfa3-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="acfa3-111">In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto.</span><span class="sxs-lookup"><span data-stu-id="acfa3-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="acfa3-112">È tuttavia possibile usare QUALSIASI schema URL.</span><span class="sxs-lookup"><span data-stu-id="acfa3-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="acfa3-113">Deve essere univoco tooyour applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="acfa3-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="acfa3-114">reindirizzamento di hello tooenable sul lato server hello:</span><span class="sxs-lookup"><span data-stu-id="acfa3-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="acfa3-115">In hello [portale], selezionare il servizio App.</span><span class="sxs-lookup"><span data-stu-id="acfa3-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="acfa3-116">Fare clic su hello **autenticazione / autorizzazione** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="acfa3-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="acfa3-117">In hello **consentito URL di reindirizzamento esterno**, immettere `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="acfa3-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="acfa3-118">Hello _appname_ in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="acfa3-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="acfa3-119">Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.</span><span class="sxs-lookup"><span data-stu-id="acfa3-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="acfa3-120">È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.</span><span class="sxs-lookup"><span data-stu-id="acfa3-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="acfa3-121">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="acfa3-121">Click **OK**.</span></span>

5. <span data-ttu-id="acfa3-122">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="acfa3-122">Click **Save**.</span></span>

## <span data-ttu-id="acfa3-123"><a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti</span><span class="sxs-lookup"><span data-stu-id="acfa3-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="acfa3-124">In Android Studio, aprire il progetto di hello è stata completata con l'esercitazione hello [Introduzione a Mobile app].</span><span class="sxs-lookup"><span data-stu-id="acfa3-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="acfa3-125">Da hello **eseguire** menu, fare clic su **eseguire app**e verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato).</span><span class="sxs-lookup"><span data-stu-id="acfa3-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="acfa3-126">Questa eccezione si verifica perché i tentativi di applicazione hello tooaccess hello nuovamente terminano come un utente non autenticato, ma hello *TodoItem* tabella richiede ora l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="acfa3-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="acfa3-127">Aggiornare quindi gli utenti di hello app tooauthenticate prima di richiedere risorse di hello che terminare nuovamente App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="acfa3-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="acfa3-128">Aggiungere app toohello authentication</span><span class="sxs-lookup"><span data-stu-id="acfa3-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="acfa3-129"><a name="cache-tokens"></a>Token di autenticazione nella cache sul client hello</span><span class="sxs-lookup"><span data-stu-id="acfa3-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="acfa3-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acfa3-130">Next steps</span></span>
<span data-ttu-id="acfa3-131">Ora che è stata completata questa esercitazione l'autenticazione di base, è consigliabile continuare su tooone di hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="acfa3-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="acfa3-132">[Aggiungere app per Android tooyour le notifiche push](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="acfa3-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="acfa3-133">Informazioni su come eseguire il backup delle applicazioni mobili tooconfigure terminare notifiche di push toosend hub notifica di Azure toouse.</span><span class="sxs-lookup"><span data-stu-id="acfa3-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="acfa3-134">[Attivare la sincronizzazione offline per l'app Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="acfa3-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="acfa3-135">Informazioni su come offline tooadd supportano tooyour app con un back-end App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="acfa3-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="acfa3-136">Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche quando non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="acfa3-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[Introduzione a Mobile app]: app-service-mobile-android-get-started.md
