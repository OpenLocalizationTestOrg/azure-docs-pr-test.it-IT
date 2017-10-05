---
title: Come configurare l'autenticazione Google per un'applicazione dei servizi app
description: Informazioni su come configurare l'autenticazione Google per un'applicazione dei servizi app.
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
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="57beb-103">Come configurare l'applicazione del servizio app per usare l'account di accesso di Google</span><span class="sxs-lookup"><span data-stu-id="57beb-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="57beb-104">Questo argomento descrive come configurare il servizio app di Azure per usare Google come provider di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="57beb-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="57beb-105">Per completare la procedura descritta in questo argomento, è necessario avere un account Google con un indirizzo di posta elettronica verificato.</span><span class="sxs-lookup"><span data-stu-id="57beb-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="57beb-106">Per creare un nuovo account Google, visitare il sito Web all'indirizzo [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="57beb-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="57beb-107"><a name="register"> </a>Registrare l'applicazione con Google</span><span class="sxs-lookup"><span data-stu-id="57beb-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="57beb-108">Accedere al [portale di Azure], e passare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57beb-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="57beb-109">Copiare l' **URL**, che verrà usato in seguito per configurare l'app Google.</span><span class="sxs-lookup"><span data-stu-id="57beb-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="57beb-110">Passare al sito Web delle [API di Google](http://go.microsoft.com/fwlink/p/?LinkId=268303)accedere con le credenziali dell'account Google, fare clic su **Crea progetto**, specificare un valore in **Nome progetto**, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="57beb-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="57beb-111">In **API Social** fare clic **Google+ API** e quindi su **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="57beb-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="57beb-112">Nel riquadro di spostamento a sinistra scegliere **Credenziali** > **Schermata consenso OAuth**, quindi selezionare il proprio **Indirizzo email**, immettere un **Nome del prodotto** e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="57beb-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="57beb-113">Nella scheda **Credenziali** fare clic su **Crea credenziali**  > **ID client OAuth**, quindi selezionare **Applicazione web**.</span><span class="sxs-lookup"><span data-stu-id="57beb-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="57beb-114">Incollare l'**URL** del servizio app copiato in precedenza in **Origini JavaScript autorizzate** e quindi incollare l'URI di reindirizzamento in **URI di reindirizzamento autorizzati**.</span><span class="sxs-lookup"><span data-stu-id="57beb-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="57beb-115">L'URI di reindirizzamento corrisponde all'URL dell'applicazione con l'aggiunta del percorso */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="57beb-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="57beb-116">Ad esempio: `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="57beb-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="57beb-117">Assicurarsi che sia in uso lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="57beb-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="57beb-118">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="57beb-118">Then click **Create**.</span></span>
7. <span data-ttu-id="57beb-119">Fare clic sulla schermata successiva e annotare i valori di ID client e Segreto client.</span><span class="sxs-lookup"><span data-stu-id="57beb-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="57beb-120">Il segreto client è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="57beb-120">The client secret is an important security credential.</span></span> <span data-ttu-id="57beb-121">Non condividere questo valore con altri e non distribuirlo all'interno di un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="57beb-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="57beb-122"><a name="secrets"> </a>Aggiungere le informazioni di Google all'applicazione</span><span class="sxs-lookup"><span data-stu-id="57beb-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="57beb-123">Nel [portale di Azure], passare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57beb-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="57beb-124">Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="57beb-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="57beb-125">Se la funzionalità di autenticazione/autorizzazione non è abilitata, impostare l'opzione in modo da **abilitarla**.</span><span class="sxs-lookup"><span data-stu-id="57beb-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="57beb-126">Fare clic su **Google**.</span><span class="sxs-lookup"><span data-stu-id="57beb-126">Click **Google**.</span></span> <span data-ttu-id="57beb-127">Incollare i valori ID App e Segreto app ottenuti in precedenza e facoltativamente abilitare tutti gli ambiti richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="57beb-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="57beb-128">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="57beb-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="57beb-129">Per impostazione predefinita, il servizio app fornisce l'autenticazione ma non limita l'accesso alle API e al contenuto del sito solo agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="57beb-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="57beb-130">È necessario autorizzare gli utenti nel codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="57beb-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="57beb-131">(Facoltativo) Per consentire l'accesso al sito solo agli utenti autenticati da Google, impostare il parametro **Azione da eseguire quando la richiesta non è autenticata** su **Google**.</span><span class="sxs-lookup"><span data-stu-id="57beb-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="57beb-132">Per poter utilizzare questa funzione, tuttavia, è necessario che tutte le richieste vengano autenticate e che le richieste non autenticate vengano reindirizzate a Google per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="57beb-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="57beb-133">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="57beb-133">Click **Save**.</span></span>

<span data-ttu-id="57beb-134">È ora possibile usare un account Google per l'autenticazione nell'app.</span><span class="sxs-lookup"><span data-stu-id="57beb-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="57beb-135"><a name="related-content"> </a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="57beb-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portale di Azure]: https://portal.azure.com/

