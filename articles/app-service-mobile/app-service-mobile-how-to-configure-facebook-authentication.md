---
title: autenticazione di Facebook tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come tooconfigure l'autenticazione di Facebook per l'applicazione di servizi di App.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="54d34-103">Come tooconfigure l'account di accesso Facebook di toouse applicazione di servizio App</span><span class="sxs-lookup"><span data-stu-id="54d34-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="54d34-104">In questo argomento illustra come tooconfigure Azure App Service toouse Facebook come provider di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="54d34-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="54d34-105">toocomplete hello in questa procedura, è necessario disporre di un account Facebook che dispone di un indirizzo di posta elettronica verificati e un numero di telefono cellulare.</span><span class="sxs-lookup"><span data-stu-id="54d34-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="54d34-106">toocreate un nuovo account Facebook, andare troppo[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="54d34-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="54d34-107"><a name="register"></a>Registrare l'applicazione con Facebook</span><span class="sxs-lookup"><span data-stu-id="54d34-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="54d34-108">Accesso toohello [portale di Azure]e passare tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="54d34-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="54d34-109">Copiare l' **URL**.</span><span class="sxs-lookup"><span data-stu-id="54d34-109">Copy your **URL**.</span></span> <span data-ttu-id="54d34-110">Si utilizzerà questo tooconfigure app Facebook.</span><span class="sxs-lookup"><span data-stu-id="54d34-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="54d34-111">In un'altra finestra del browser, passare toohello [sviluppatori Facebook] sito Web e Accedi con il Facebook delle credenziali dell'account.</span><span class="sxs-lookup"><span data-stu-id="54d34-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="54d34-112">(Facoltativo) Se non è stata già registrata, fare clic su **app** > **registrare gli sviluppatori**quindi accettare criteri hello e attenersi alla procedura di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="54d34-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="54d34-113">Fare clic su **My Apps** (App personali)  > **Add a New App** (Aggiungi una nuova app)  > **Website** (Sito Web)  > **Skip and Create App ID** (Ignora e crea ID app).</span><span class="sxs-lookup"><span data-stu-id="54d34-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="54d34-114">In **nome visualizzato**, digitare un nome univoco per l'app, il tipo del **Contact Email**, scegliere un **categoria** per l'app, quindi fare clic su **creare ID App**e completare il controllo di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="54d34-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="54d34-115">Consente di procedere toohello dashboard dello sviluppatore per la nuova app Facebook.</span><span class="sxs-lookup"><span data-stu-id="54d34-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="54d34-116">In "Facebook Login" (Accesso a Facebook) fare clic su **Get Started**(Informazioni di base).</span><span class="sxs-lookup"><span data-stu-id="54d34-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="54d34-117">Aggiungere l'applicazione **URI di reindirizzamento** troppo**URI di reindirizzamento di OAuth valido**, quindi fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="54d34-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="54d34-118">L'URI di reindirizzamento URL hello dell'applicazione con il percorso di hello, */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="54d34-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="54d34-119">ad esempio `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="54d34-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="54d34-120">Assicurarsi che si sta utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="54d34-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="54d34-121">Navigazione a sinistra di hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="54d34-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="54d34-122">In hello **segreto dell'App** campo, fare clic su **Mostra**, fornire una password se richiesto, quindi prendere nota dei valori hello di **ID App** e **segreto dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="54d34-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="54d34-123">Usare questi tooconfigure successive l'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="54d34-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="54d34-124">segreto dell'applicazione Hello è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="54d34-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="54d34-125">Non condividere questo valore con altri e non distribuirlo all'interno di un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="54d34-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="54d34-126">Hello account Facebook è un'applicazione hello tooregister utilizzato sia un amministratore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="54d34-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="54d34-127">A questo punto, solo gli amministratori potranno effettuare l'accesso a questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="54d34-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="54d34-128">tooauthenticate altri account Facebook, fare clic su **revisione di App** e abilitare **pubblica assicurarsi < your-app-name >** accesso pubblico generale tooenable utilizzando l'autenticazione di Facebook.</span><span class="sxs-lookup"><span data-stu-id="54d34-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="54d34-129"><a name="secrets"></a>Applicazione tooyour aggiungere Facebook</span><span class="sxs-lookup"><span data-stu-id="54d34-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="54d34-130">In hello [portale di Azure], passare tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="54d34-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="54d34-131">Fare clic su **Impostazioni** > **Autenticazione/Autorizzazione**, quindi assicurarsi che l'opzione **Autenticazione servizio app** sia impostata su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="54d34-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="54d34-132">Fare clic su **Facebook**, incollare i valori ID dell'App e segreto dell'applicazione hello cui ottenuto in precedenza, se lo si desidera abilitare tutti gli ambiti richiesti dall'applicazione, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="54d34-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="54d34-133">Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API.</span><span class="sxs-lookup"><span data-stu-id="54d34-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="54d34-134">È necessario autorizzare gli utenti nel codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="54d34-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="54d34-135">(Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati da Facebook, impostare **tootake azione quando la richiesta non è autenticata** troppo**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="54d34-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="54d34-136">Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooFacebook per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="54d34-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="54d34-137">Al termine della configurazione dell'autenticazione, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="54d34-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="54d34-138">Si è ora pronto toouse Facebook per l'autenticazione nell'app.</span><span class="sxs-lookup"><span data-stu-id="54d34-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="54d34-139"><a name="related-content"></a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="54d34-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[sviluppatori Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portale di Azure]: https://portal.azure.com/
