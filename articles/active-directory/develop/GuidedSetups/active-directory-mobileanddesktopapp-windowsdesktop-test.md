---
title: aaaAzure AD v2 Windows Desktop Getting Started - Test | Documenti Microsoft
description: Come applicazioni .NET per Windows Desktop (XAML) possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="3c7a3-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="3c7a3-103">Test your code</span></span>

<span data-ttu-id="3c7a3-104">Ordinare tootest dell'applicazione, premere `F5` toorun il progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="3c7a3-105">Verrà visualizzata la finestra principale:</span><span class="sxs-lookup"><span data-stu-id="3c7a3-105">Your Main Window should appear:</span></span>

![Schermata di esempio](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="3c7a3-107">Quando sarai pronto tootest, fare clic su *chiamare API di Microsoft Graph* e utilizzare Microsoft Azure Active Directory (account aziendale) o un toosign di account Account Microsoft (live.com, outlook.com) in.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="3c7a3-108">Si è hello prima volta, viene visualizzata una finestra toosign utente in:</span><span class="sxs-lookup"><span data-stu-id="3c7a3-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![Accesso](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="3c7a3-110">Consenso</span><span class="sxs-lookup"><span data-stu-id="3c7a3-110">Consent</span></span>
<span data-ttu-id="3c7a3-111">Hello prima volta che accedi nell'applicazione tooyour, verrà visualizzata con un seguente toohello consenso simile dello schermo, in cui è necessario accettare tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="3c7a3-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Schermata di consenso](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="3c7a3-113">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="3c7a3-113">Expected results</span></span>
<span data-ttu-id="3c7a3-114">Dovrebbe essere restituite dalla chiamata all'API Graph di Microsoft hello nella schermata di risultati di chiamare API hello informazioni del profilo utente.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="3c7a3-115">Verrà visualizzato anche le informazioni di base token hello acquisito tramite `AcquireTokenAsync` o `AcquireTokenSilentAsync` nella casella di informazioni sul Token hello:</span><span class="sxs-lookup"><span data-stu-id="3c7a3-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="3c7a3-116">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3c7a3-116">Property</span></span>  |<span data-ttu-id="3c7a3-117">Format</span><span class="sxs-lookup"><span data-stu-id="3c7a3-117">Format</span></span>  |<span data-ttu-id="3c7a3-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3c7a3-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="3c7a3-119">Nome</span><span class="sxs-lookup"><span data-stu-id="3c7a3-119">Name</span></span> | <span data-ttu-id="3c7a3-120">{Nome utente completo}</span><span class="sxs-lookup"><span data-stu-id="3c7a3-120">{User Full name}</span></span> |<span data-ttu-id="3c7a3-121">utente Hello e del cognome</span><span class="sxs-lookup"><span data-stu-id="3c7a3-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="3c7a3-122">Username</span><span class="sxs-lookup"><span data-stu-id="3c7a3-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="3c7a3-123">nome utente Hello utilizzato tooidentify hello</span><span class="sxs-lookup"><span data-stu-id="3c7a3-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="3c7a3-124">Token Expires (Scadenza token)</span><span class="sxs-lookup"><span data-stu-id="3c7a3-124">Token Expires</span></span> |<span data-ttu-id="3c7a3-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="3c7a3-125">{DateTime}</span></span>         |<span data-ttu-id="3c7a3-126">ora di Hello di quali hello scadenza del token.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-126">hello time on which hello token expires.</span></span> <span data-ttu-id="3c7a3-127">MSAL verrà esteso data di scadenza hello è Rinnovando il token hello quando necessario</span><span class="sxs-lookup"><span data-stu-id="3c7a3-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="3c7a3-128">Token di accesso</span><span class="sxs-lookup"><span data-stu-id="3c7a3-128">Access token</span></span> |<span data-ttu-id="3c7a3-129">{Stringa}</span><span class="sxs-lookup"><span data-stu-id="3c7a3-129">{String}</span></span>         |<span data-ttu-id="3c7a3-130">stringa di token hello inviati che riceverà le richieste di tooHTTP che richiedono un'intestazione di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="3c7a3-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="3c7a3-131">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="3c7a3-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="3c7a3-132">API Graph richiede hello `user.read` profilo utente tooread di ambito.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="3c7a3-133">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="3c7a3-134">Altre API Graph e alcune API personalizzate per il server back-end richiedono anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="3c7a3-135">Ad esempio, per grafico, `Calendars.Read` è calendari dell'utente toolist obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="3c7a3-136">In ordine tooaccess hello del calendario dell'utente in un contesto di un'applicazione, è necessario tooadd `Calendars.Read` delegati informazioni di registrazione dell'applicazione e quindi aggiungere `Calendars.Read` toohello `AcquireTokenAsync` chiamare.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="3c7a3-137">Utente potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.</span><span class="sxs-lookup"><span data-stu-id="3c7a3-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



