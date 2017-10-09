---
title: aaaAzure AD v2 JS SPA impostazione guidata - Test | Documenti Microsoft
description: Come le applicazioni SPA di Javascript possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="a6d9a-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="a6d9a-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="a6d9a-104">Test con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6d9a-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="a6d9a-105">Se si utilizza Visual Studio, premere `F5` toorun il progetto: hello browser verrà aperto e si indirizza troppo*http://localhost: {porta}* in cui si vedere hello *chiamare API di Microsoft Graph* pulsante.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="a6d9a-106">Test con Python o un altro server Web</span><span class="sxs-lookup"><span data-stu-id="a6d9a-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="a6d9a-107">Se non si utilizza Visual Studio, assicurarsi che il server web sia avviato e sia configurato in base hello cartella contenente la porta TCP tooa toolisten il *index.html* file.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="a6d9a-108">Per Python, è possibile avviare l'ascolto hello porta toohello eseguendo il comando hello dei messaggi di richiesta / terminal, dalla cartella dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="a6d9a-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="a6d9a-109">Quindi, aprire il browser hello e digitare *http://localhost:8080* o *http://localhost: {porta}* - hello *porta* corrisponde toohello porta che il server web in attesa di.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="a6d9a-110">È necessario visualizzare il contenuto di hello della pagina index. HTML con hello *chiamare API di Microsoft Graph* pulsante.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="a6d9a-111">Testare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="a6d9a-111">Test your application</span></span>

<span data-ttu-id="a6d9a-112">Dopo aver browser hello carica il *index.html*, fare clic su hello *chiamare API di Microsoft Graph* pulsante.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="a6d9a-113">Se si tratta hello prima volta, i reindirizzamenti browser hello è toohello v2 di Microsoft Azure Active Directory endpoint, in cui si è richiesto toosign in.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Schermata di esempio](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="a6d9a-115">Consenso</span><span class="sxs-lookup"><span data-stu-id="a6d9a-115">Consent</span></span>
<span data-ttu-id="a6d9a-116">Hello prima volta che accedi tooyour applicazione, verranno visualizzate con un consenso schermata simili toohello riportato di seguito, in cui è necessario tooaccept:</span><span class="sxs-lookup"><span data-stu-id="a6d9a-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Schermata di consenso](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="a6d9a-118">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="a6d9a-118">Expected results</span></span>
<span data-ttu-id="a6d9a-119">Si noterà che le informazioni sul profilo utente restituiti da hello risposta chiamata di API di Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Risultati](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="a6d9a-121">Inoltre visualizzare le informazioni di base sui token hello acquisito in hello *Token di accesso* e *le attestazioni nei Token ID* caselle.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="a6d9a-122">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="a6d9a-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="a6d9a-123">API di Microsoft Graph Hello richiede hello `user.read` ambito tooread hello del profilo utente.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="a6d9a-124">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="a6d9a-125">Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="a6d9a-126">Ad esempio, per Microsoft Graph, hello ambito `Calendars.Read` è calendari dell'utente di hello toolist obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="a6d9a-127">In ordine tooaccess hello del calendario dell'utente nel contesto di hello di un'applicazione, è necessario hello tooadd `Calendars.Read` informazioni di registrazione applicazione toohello di autorizzazione di delega e quindi aggiungere hello `Calendars.Read` toohello ambito `acquireTokenSilent` chiamare.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="a6d9a-128">utente Hello potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="a6d9a-129">Se un'API back-end non è necessario un ambito (non consigliato), è possibile utilizzare hello `clientId` come ambito hello in hello `acquireTokenSilent` e/o `acquireTokenRedirect` chiamate.</span><span class="sxs-lookup"><span data-stu-id="a6d9a-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
