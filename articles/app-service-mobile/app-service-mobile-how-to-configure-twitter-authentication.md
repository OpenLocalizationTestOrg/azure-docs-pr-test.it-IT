---
title: autenticazione di Twitter tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come l'autenticazione di Twitter tooconfigure per l'applicazione di servizi di App.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="4f5e0-103">Come tooconfigure l'account di accesso Twitter di toouse applicazione di servizio App</span><span class="sxs-lookup"><span data-stu-id="4f5e0-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="4f5e0-104">In questo argomento illustra come tooconfigure Azure App Service toouse Twitter come provider di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="4f5e0-105">toocomplete hello in questa procedura, è necessario disporre di un account Twitter con un messaggio di posta elettronica verificato indirizzo e numero di telefono.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="4f5e0-106">toocreate un nuovo account Twitter, andare troppo<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="4f5e0-107"><a name="register"></a>Registrare l'applicazione con Twitter</span><span class="sxs-lookup"><span data-stu-id="4f5e0-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="4f5e0-108">Accesso toohello [portale di Azure]e passare tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="4f5e0-109">Copiare l' **URL**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-109">Copy your **URL**.</span></span> <span data-ttu-id="4f5e0-110">Si utilizzerà questo tooconfigure app Twitter.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="4f5e0-111">Passare toohello [agli sviluppatori di Twitter] sito Web, accedere con le credenziali dell'account Twitter e fare clic su **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="4f5e0-112">Tipo di hello **nome** e **descrizione** per la nuova app.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="4f5e0-113">Incolla in un'applicazione **URL** per hello **sito Web** valore.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="4f5e0-114">Quindi, per hello **URL Callback**, incollare hello **URL Callback** copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="4f5e0-115">Questo è il gateway di App per dispositivi mobili con il percorso di hello, */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="4f5e0-116">ad esempio `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="4f5e0-117">Assicurarsi che si sta utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="4f5e0-118">Nella pagina di hello inferiore hello, leggere e accettare i termini di hello.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="4f5e0-119">Fare clic su **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="4f5e0-120">Questa app hello registri consente di visualizzare i dettagli dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="4f5e0-121">Fare clic su hello **impostazioni** scheda **consentire questa toosign toobe utilizzato applicazione con Twitter**, quindi fare clic su **le impostazioni di aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="4f5e0-122">Seleziona hello **chiavi e i token di accesso** scheda. Prendere nota dei valori hello di **Consumer tasto (API)** e **segreto del cliente (chiave privata API)**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4f5e0-123">segreto del cliente Hello è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="4f5e0-124">Non condividere questo valore con altri né distribuirlo con l'app.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="4f5e0-125"><a name="secrets"></a>Applicazione tooyour aggiungere Twitter</span><span class="sxs-lookup"><span data-stu-id="4f5e0-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="4f5e0-126">In hello [portale di Azure], passare tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="4f5e0-127">Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="4f5e0-128">Se l'autenticazione di hello / non è abilitata la funzionalità di autorizzazione, l'opzione di hello troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="4f5e0-129">Fare clic su **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-129">Click **Twitter**.</span></span> <span data-ttu-id="4f5e0-130">Incollare hello App ID e segreto dell'applicazione i valori che è stato ottenuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="4f5e0-131">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="4f5e0-132">Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="4f5e0-133">È necessario autorizzare gli utenti nel codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="4f5e0-134">(Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati tramite Twitter, impostare **tootake azione quando la richiesta non è autenticata** troppo**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="4f5e0-135">Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooTwitter per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="4f5e0-136">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-136">Click **Save**.</span></span>

<span data-ttu-id="4f5e0-137">Si è ora pronto toouse Twitter per l'autenticazione nell'app.</span><span class="sxs-lookup"><span data-stu-id="4f5e0-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="4f5e0-138"><a name="related-content"></a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="4f5e0-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[agli sviluppatori di Twitter]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portale di Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
