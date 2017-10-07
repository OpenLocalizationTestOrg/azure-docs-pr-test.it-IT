---
title: autenticazione di Google tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come l'autenticazione di Google tooconfigure per l'applicazione di servizi di App.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="4cef6-103">Come tooconfigure l'account di Google accesso toouse di applicazione di servizio App</span><span class="sxs-lookup"><span data-stu-id="4cef6-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="4cef6-104">In questo argomento illustra come tooconfigure Azure App Service toouse Google come provider di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4cef6-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="4cef6-105">toocomplete hello in questa procedura, è necessario disporre di un account di Google che dispone di un indirizzo di posta elettronica verificato.</span><span class="sxs-lookup"><span data-stu-id="4cef6-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="4cef6-106">toocreate un nuovo account di Google, andare troppo[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="4cef6-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="4cef6-107"><a name="register"></a>Registrare l'applicazione con Google</span><span class="sxs-lookup"><span data-stu-id="4cef6-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="4cef6-108">Accesso toohello [portale di Azure]e passare tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="4cef6-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="4cef6-109">Copia il **URL**, che si utilizza tooconfigure successive dell'app di Google.</span><span class="sxs-lookup"><span data-stu-id="4cef6-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="4cef6-110">Passare toohello [API Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) sito Web, accedere con le credenziali dell'account Google, fare clic su **Crea progetto**, fornire un **nome progetto**, quindi fare clic su  **Creare**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="4cef6-111">In **API Social** fare clic **Google+ API** e quindi su **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="4cef6-112">Nel riquadro di spostamento, sinistro hello **credenziali** > **schermata consenso OAuth**, quindi selezionare il **indirizzo di posta elettronica**, immettere un **Product Name**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="4cef6-113">In hello **credenziali** scheda, fare clic su **creare credenziali** > **ID client OAuth**, quindi selezionare **applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="4cef6-114">Incolla hello servizio App **URL** è copiato in precedenza in **Authorized JavaScript Origins**, quindi incollare il reindirizzamento URI in **autorizzato l'URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="4cef6-115">URI di reindirizzamento URL hello dell'applicazione con il percorso di hello, Hello */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="4cef6-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="4cef6-116">ad esempio `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="4cef6-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="4cef6-117">Assicurarsi che si sta utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="4cef6-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="4cef6-118">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-118">Then click **Create**.</span></span>
7. <span data-ttu-id="4cef6-119">Nella schermata successiva hello, prendere nota dei valori di hello del client hello segreto ID e client.</span><span class="sxs-lookup"><span data-stu-id="4cef6-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4cef6-120">segreto client hello è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4cef6-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="4cef6-121">Non condividere questo valore con altri e non distribuirlo all'interno di un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="4cef6-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="4cef6-122"><a name="secrets"></a>Tooyour Google Aggiungi applicazione</span><span class="sxs-lookup"><span data-stu-id="4cef6-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="4cef6-123">In hello [portale di Azure], passare tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="4cef6-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="4cef6-124">Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="4cef6-125">Se l'autenticazione di hello / non è abilitata la funzionalità di autorizzazione, l'opzione di hello troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="4cef6-126">Fare clic su **Google**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-126">Click **Google**.</span></span> <span data-ttu-id="4cef6-127">Incollare i valori ID dell'App e segreto dell'applicazione hello cui ottenuto in precedenza e facoltativamente abilitare tutti gli ambiti che richiede l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4cef6-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="4cef6-128">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="4cef6-129">Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API.</span><span class="sxs-lookup"><span data-stu-id="4cef6-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="4cef6-130">È necessario autorizzare gli utenti nel codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="4cef6-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="4cef6-131">(Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati da Google, impostare **tootake azione quando la richiesta non è autenticata** troppo**Google**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="4cef6-132">Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooGoogle per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4cef6-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="4cef6-133">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4cef6-133">Click **Save**.</span></span>

<span data-ttu-id="4cef6-134">Si è ora pronto toouse Google per l'autenticazione nell'app.</span><span class="sxs-lookup"><span data-stu-id="4cef6-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="4cef6-135"><a name="related-content"></a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="4cef6-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portale di Azure]: https://portal.azure.com/

