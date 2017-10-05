---
title: Come configurare l'autenticazione dell'account Microsoft per un'applicazione dei servizi app
description: Informazioni su come configurare l'autenticazione dell'account Microsoft per un'applicazione dei servizi app.
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 67386b03ae4cc683fe00e11e8dad19d1442eff09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="e533f-103">Come configurare l’applicazione del servizio app per usare l'account di accesso Microsoft</span><span class="sxs-lookup"><span data-stu-id="e533f-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="e533f-104">Questo argomento descrive come configurare il servizio app di Azure per usare l'account Microsoft come provider di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e533f-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="e533f-105"><a name="register-microsoft-account"> </a>Registrare l'app con l'account Microsoft</span><span class="sxs-lookup"><span data-stu-id="e533f-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="e533f-106">Accedere al [portale di Azure], e passare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e533f-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="e533f-107">Copiare l' **URL**, che verrà usato in un secondo momento per configurare l'app con Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e533f-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="e533f-108">Passare alla pagina [My Applications] di Microsoft Account Developer Center e, se necessario, accedere con il proprio account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e533f-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="e533f-109">Fare clic su **Aggiungi un'app**, digitare un nome di applicazione e quindi fare clic su **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="e533f-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="e533f-110">Prendere nota dell' **ID applicazione**perché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e533f-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="e533f-111">In "Piattaforme" fare clic su **Aggiungi piattaforma** e quindi selezionare "Web".</span><span class="sxs-lookup"><span data-stu-id="e533f-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="e533f-112">In "URI di reindirizzamento" specificare l'endpoint dell'applicazione e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e533f-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e533f-113">L'URI di reindirizzamento corrisponde all'URL dell'applicazione con l'aggiunta del percorso */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="e533f-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="e533f-114">Ad esempio: `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="e533f-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="e533f-115">Assicurarsi che sia in uso lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e533f-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="e533f-116">In "Segreti applicazione" fare clic su **Genera nuova password**.</span><span class="sxs-lookup"><span data-stu-id="e533f-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="e533f-117">Prendere nota del valore visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e533f-117">Make note of the value that appears.</span></span> <span data-ttu-id="e533f-118">Una volta chiusa la pagina, il valore non verrà più mostrato.</span><span class="sxs-lookup"><span data-stu-id="e533f-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e533f-119">La password è una credenziale di sicurezza importante.</span><span class="sxs-lookup"><span data-stu-id="e533f-119">The password is an important security credential.</span></span> <span data-ttu-id="e533f-120">Non condividerla con altri e non distribuirla all'interno di un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="e533f-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="e533f-121"><a name="secrets"> </a>Aggiungere le informazioni dell'account Microsoft all'applicazione del servizio app</span><span class="sxs-lookup"><span data-stu-id="e533f-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="e533f-122">Nel [portale di Azure] passare all'applicazione e fare clic su **Impostazioni** > **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="e533f-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="e533f-123">Se la funzionalità Autenticazione/Autorizzazione non è abilitata, impostare l'opzione su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="e533f-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="e533f-124">Fare clic su **Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e533f-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="e533f-125">Incollare i valori di ID applicazione e Password ottenuti in precedenza ed eventualmente abilitare gli ambiti richiesti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e533f-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="e533f-126">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e533f-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="e533f-127">Per impostazione predefinita, il servizio app fornisce l'autenticazione ma non limita l'accesso alle API e al contenuto del sito solo agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="e533f-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="e533f-128">È necessario autorizzare gli utenti nel codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="e533f-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="e533f-129">(Facoltativo) Per consentire l'accesso al sito solo agli utenti autenticati dall'account Microsoft, impostare il parametro **Azione da eseguire quando la richiesta non è autenticata** su **Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e533f-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="e533f-130">Per poter utilizzare questa funzione, tuttavia, è necessario che tutte le richieste vengano autenticate e che le richieste non autenticate vengano reindirizzate all’account Microsoft per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e533f-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="e533f-131">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e533f-131">Click **Save**.</span></span>

<span data-ttu-id="e533f-132">È ora possibile usare l'account Microsoft per l'autenticazione nell'app.</span><span class="sxs-lookup"><span data-stu-id="e533f-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="e533f-133"><a name="related-content"> </a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="e533f-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portale di Azure]: https://portal.azure.com/
