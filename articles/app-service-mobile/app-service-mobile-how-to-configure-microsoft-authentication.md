---
title: autenticazione dell'Account Microsoft tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come tooconfigure autenticazione dell'Account Microsoft per l'applicazione di servizi di App.
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
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="6c09a-103">Come tooconfigure l'account di accesso Account Microsoft di toouse applicazione di servizio App</span><span class="sxs-lookup"><span data-stu-id="6c09a-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="6c09a-104">In questo argomento illustra come tooconfigure Azure App Service toouse Account Microsoft come un provider di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6c09a-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="6c09a-105"><a name="register-microsoft-account"></a>Registrare l'app con l'account Microsoft</span><span class="sxs-lookup"><span data-stu-id="6c09a-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="6c09a-106">Accesso toohello [portale di Azure]e passare tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c09a-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="6c09a-107">Copia il **URL**, che in seguito utilizzare tooconfigure app con Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6c09a-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="6c09a-108">Passare toohello [applicazioni personali] pagina hello Microsoft Account Developer Center e accedere con l'account Microsoft, se necessario.</span><span class="sxs-lookup"><span data-stu-id="6c09a-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="6c09a-109">Fare clic su **Aggiungi un'app**, digitare un nome di applicazione e quindi fare clic su **Crea applicazione**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="6c09a-110">Prendere nota di hello **ID applicazione**, perché sarà necessaria in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6c09a-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="6c09a-111">In "Piattaforme" fare clic su **Aggiungi piattaforma** e quindi selezionare "Web".</span><span class="sxs-lookup"><span data-stu-id="6c09a-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="6c09a-112">In "Redirect URIs" alimentatore hello endpoint per l'applicazione, quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6c09a-113">L'URI di reindirizzamento URL hello dell'applicazione con il percorso di hello, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="6c09a-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="6c09a-114">ad esempio `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="6c09a-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="6c09a-115">Assicurarsi che si sta utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="6c09a-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="6c09a-116">In "Segreti applicazione" fare clic su **Genera nuova password**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="6c09a-117">Prendere nota del valore di hello che viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="6c09a-117">Make note of hello value that appears.</span></span> <span data-ttu-id="6c09a-118">Quando si esce hello pagina, non essere visualizzato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="6c09a-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6c09a-119">password di Hello è un'importante credenziale di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6c09a-119">hello password is an important security credential.</span></span> <span data-ttu-id="6c09a-120">Non condividere password hello con nessuno o distribuirlo in un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="6c09a-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="6c09a-121"><a name="secrets"></a>Aggiungere Account a Microsoft informazioni tooyour applicazione di servizio App</span><span class="sxs-lookup"><span data-stu-id="6c09a-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="6c09a-122">In hello [portale di Azure]passare tooyour applicazione, fare clic su **impostazioni** > **autenticazione / autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="6c09a-123">Se hello autenticazione / autorizzazione funzionalità non è abilitata, attivarla **su**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="6c09a-124">Fare clic su **Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="6c09a-125">Incollare i valori ID applicazione e la Password hello cui ottenuto in precedenza e facoltativamente abilitare tutti gli ambiti che richiede l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c09a-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="6c09a-126">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="6c09a-127">Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API.</span><span class="sxs-lookup"><span data-stu-id="6c09a-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="6c09a-128">È necessario autorizzare gli utenti nel codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="6c09a-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="6c09a-129">(Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati dall'account Microsoft, impostare **tootake azione quando la richiesta non è autenticata** troppo**Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="6c09a-130">Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooMicrosoft account per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6c09a-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="6c09a-131">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6c09a-131">Click **Save**.</span></span>

<span data-ttu-id="6c09a-132">Si è ora pronto toouse Account Microsoft per l'autenticazione nell'app.</span><span class="sxs-lookup"><span data-stu-id="6c09a-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="6c09a-133"><a name="related-content"></a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="6c09a-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[applicazioni personali]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portale di Azure]: https://portal.azure.com/
