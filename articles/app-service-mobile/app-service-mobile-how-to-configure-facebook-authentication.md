---
title: Come configurare l'autenticazione Facebook per un'applicazione dei servizi app
description: Informazioni su come configurare l'autenticazione Facebook per un'applicazione dei servizi app.
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
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="18406-103">Come configurare un'applicazione del servizio App per usare l'account di accesso di Facebook</span><span class="sxs-lookup"><span data-stu-id="18406-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="18406-104">Questo argomento descrive come configurare il servizio app di Azure per usare Facebook come provider di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="18406-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="18406-105">Per completare la procedura descritta in questo argomento, è necessario disporre di un account di Facebook con un indirizzo di posta elettronica verificato e un numero di cellulare.</span><span class="sxs-lookup"><span data-stu-id="18406-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="18406-106">Per creare un nuovo account di Facebook, visitare il sito [facebook.com].</span><span class="sxs-lookup"><span data-stu-id="18406-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="18406-107"><a name="register"> </a>Registrare l'applicazione con Facebook</span><span class="sxs-lookup"><span data-stu-id="18406-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="18406-108">Accedere al [portale di Azure], e passare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="18406-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="18406-109">Copiare l' **URL**.</span><span class="sxs-lookup"><span data-stu-id="18406-109">Copy your **URL**.</span></span> <span data-ttu-id="18406-110">Verrà usato per configurare l'app Facebook.</span><span class="sxs-lookup"><span data-stu-id="18406-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="18406-111">In un'altra finestra del browser passare al sito Web [Facebook Developers] e accedere con le credenziali dell'account Facebook.</span><span class="sxs-lookup"><span data-stu-id="18406-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="18406-112">(Facoltativo) Se non è ancora stata effettuata la registrazione, fare clic su **Apps** (App)  > **Register as a Developer** (Registrarsi come sviluppatore), quindi accettare le condizioni e seguire la procedura di registrazione.</span><span class="sxs-lookup"><span data-stu-id="18406-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="18406-113">Fare clic su **My Apps** (App personali)  > **Add a New App** (Aggiungi una nuova app)  > **Website** (Sito Web)  > **Skip and Create App ID** (Ignora e crea ID app).</span><span class="sxs-lookup"><span data-stu-id="18406-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="18406-114">In **Display Name** (Nome visualizzato) digitare un nome univoco per l'app, digitare un indirizzo in **Contact Email** (Indirizzo di posta elettronica di contatto), scegliere una categoria per l'app in **Category** (Categoria), quindi fare clic su **Create App ID** (Crea ID app) e completare il controllo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="18406-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="18406-115">Si passerà al dashboard dello sviluppatore per la nuova app di Facebook.</span><span class="sxs-lookup"><span data-stu-id="18406-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="18406-116">In "Facebook Login" (Accesso a Facebook) fare clic su **Get Started**(Informazioni di base).</span><span class="sxs-lookup"><span data-stu-id="18406-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="18406-117">Aggiungere l'URI di **Redirect URI** (URI di reindirizzamento) dell'applicazione in **Valid OAuth redirect URIs** (URI di reindirizzamento OAuth validi) e quindi fare clic su **Save Changes** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="18406-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="18406-118">L'URI di reindirizzamento corrisponde all'URL dell'applicazione con l'aggiunta del percorso */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="18406-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="18406-119">Ad esempio: `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="18406-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="18406-120">Assicurarsi che sia in uso lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="18406-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="18406-121">Nel riquadro di spostamento a sinistra fare clic su **Settings**(Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="18406-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="18406-122">Nel campo **App Secret** (Segreto app) fare clic su **Show** (Mostra), fornire la password se richiesto, quindi prendere nota dei valori di **App ID** (ID app) e **App Secret** (Segreto app).</span><span class="sxs-lookup"><span data-stu-id="18406-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="18406-123">Verranno usati più avanti per configurare l'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="18406-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="18406-124">Il segreto dell'app è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="18406-124">The app secret is an important security credential.</span></span> <span data-ttu-id="18406-125">Non condividere questo valore con altri e non distribuirlo all'interno di un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="18406-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="18406-126">L'account di Facebook usato per registrare l'applicazione sarà un account di amministratore dell'app.</span><span class="sxs-lookup"><span data-stu-id="18406-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="18406-127">A questo punto, solo gli amministratori potranno effettuare l'accesso a questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="18406-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="18406-128">Per eseguire l'autenticazione di altri account di Facebook, fare clic su **App Review** (Controllo app) e abilitare l'opzione **Make <nome-app> public** (Rendi pubblica) e consentire così l'accesso pubblico generale con l'autenticazione di Facebook.</span><span class="sxs-lookup"><span data-stu-id="18406-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="18406-129"><a name="secrets"> </a>Aggiungere le informazioni di Facebook all'applicazione</span><span class="sxs-lookup"><span data-stu-id="18406-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="18406-130">Nel [portale di Azure], passare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="18406-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="18406-131">Fare clic su **Impostazioni** > **Autenticazione/Autorizzazione**, quindi assicurarsi che l'opzione **Autenticazione servizio app** sia impostata su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="18406-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="18406-132">Fare clic su **Facebook**, incollare i valori di ID app e segreto app i valori ottenuti in precedenza e abilitare facoltativamente tutti gli ambiti richiesti dall'applicazione, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="18406-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="18406-133">Per impostazione predefinita, il servizio app fornisce l'autenticazione ma non limita l'accesso alle API e al contenuto del sito solo agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="18406-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="18406-134">È necessario autorizzare gli utenti nel codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="18406-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="18406-135">(Facoltativo) Per consentire l'accesso al sito solo agli utenti autenticati da Facebook, impostare il parametro **Azione da eseguire quando la richiesta non è autenticata** su **Facebook**.</span><span class="sxs-lookup"><span data-stu-id="18406-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="18406-136">Per poter utilizzare questa funzione, tuttavia, è necessario che tutte le richieste vengano autenticate e che le richieste non autenticate vengano reindirizzate a Facebook per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="18406-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="18406-137">Al termine della configurazione dell'autenticazione, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="18406-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="18406-138">È ora possibile usare un account di Facebook per l'autenticazione nell'app.</span><span class="sxs-lookup"><span data-stu-id="18406-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="18406-139"><a name="related-content"> </a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="18406-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="18406-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="18406-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="18406-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="18406-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="18406-142">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="18406-142">[Azure portal]: https://portal.azure.com/</span></span>
