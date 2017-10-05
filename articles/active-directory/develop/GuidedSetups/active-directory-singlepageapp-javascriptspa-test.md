---
title: Configurazione guidata di JS SPA per Azure AD v2 - Test | Microsoft Docs
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
ms.openlocfilehash: c888760ab311e8ac08b1e625bb837f91047db645
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
## <a name="test-your-code"></a><span data-ttu-id="2771b-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="2771b-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="2771b-104">Test con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2771b-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="2771b-105">Se si usa Visual Studio, premere `F5` per eseguire il progetto: verrà aperto il browser e l'utente verrà indirizzato a *http://localhost:{port}*, in cui verrà visualizzato il pulsante *Call Microsoft Graph API* (Chiama API Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="2771b-105">If you are using Visual Studio, press `F5` to run your project: the browser opens and directs you to *http://localhost:{port}* where you see the *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="2771b-106">Test con Python o un altro server Web</span><span class="sxs-lookup"><span data-stu-id="2771b-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="2771b-107">Se non si usa Visual Studio, assicurarsi che il server Web sia avviato e configurato per ascoltare una porta TCP in base alla cartella contenente il file *index.html*.</span><span class="sxs-lookup"><span data-stu-id="2771b-107">If you are not using Visual Studio, make sure your web server is started and it is configured to listen to a TCP port based on the folder containing your *index.html* file.</span></span> <span data-ttu-id="2771b-108">Per Python, è possibile avviare l'ascolto della porta mediante l'esecuzione di nel prompt dei comandi/terminale dalla cartella dell'app:</span><span class="sxs-lookup"><span data-stu-id="2771b-108">For Python, you can start listening to the port by running the in the command prompt/ terminal, from the app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="2771b-109">Aprire quindi il browser e digitare *http://localhost:8080* o *http://localhost:{port}* in cui *port* corrisponde alla porta che il server Web sta ascoltando.</span><span class="sxs-lookup"><span data-stu-id="2771b-109">Then, open the browser and type *http://localhost:8080* or *http://localhost:{port}* - where the *port* corresponds to the port that your web server is listening to.</span></span> <span data-ttu-id="2771b-110">È necessario visualizzare i contenuti della pagina index.html con il pulsante *Call Microsoft Graph API* (Chiama API Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="2771b-110">You should see the contents of your index.html page with the *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="2771b-111">Testare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="2771b-111">Test your application</span></span>

<span data-ttu-id="2771b-112">Dopo che il browser ha caricato *index.html*, fare clic sul pulsante *Call Microsoft Graph API*.</span><span class="sxs-lookup"><span data-stu-id="2771b-112">After the browser loads your *index.html*, click the *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="2771b-113">Se questa è la prima volta, il browser reindirizza all'endpoint v2 di Microsoft Azure Active Directory, a cui viene chiesto di accedere.</span><span class="sxs-lookup"><span data-stu-id="2771b-113">If this is the first time, the browser redirects you to the Microsoft Azure Active Directory v2 endpoint, where you are  prompted to sign in.</span></span>
 
![Schermata di esempio](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="2771b-115">Consenso</span><span class="sxs-lookup"><span data-stu-id="2771b-115">Consent</span></span>
<span data-ttu-id="2771b-116">La prima volta che si accede all'applicazione, viene visualizzata una schermata di consenso, simile alla seguente, in cui è necessario accettare:</span><span class="sxs-lookup"><span data-stu-id="2771b-116">The very first time you sign in to your application, you are presented with a consent screen similar to the following, where you need to accept:</span></span>

 ![Schermata di consenso](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="2771b-118">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="2771b-118">Expected results</span></span>
<span data-ttu-id="2771b-119">Si dovrebbero visualizzare le informazioni del profilo utente restituite dalla risposta alla chiamata all'API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2771b-119">You should see user profile information returned by the Microsoft Graph API call response.</span></span>
 
 ![Risultati](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="2771b-121">Sono anche visualizzate le informazioni di base sul token acquisite nelle caselle *Access Token* e *ID Token Claims*.</span><span class="sxs-lookup"><span data-stu-id="2771b-121">You also see basic information about the token acquired in the *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="2771b-122">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="2771b-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="2771b-123">L'API di Microsoft Graph richiede l'ambito `user.read` per leggere il profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2771b-123">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="2771b-124">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="2771b-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="2771b-125">Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="2771b-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="2771b-126">Ad esempio, per Microsoft Graph, l'ambito `Calendars.Read` è necessario per elencare i calendari dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2771b-126">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="2771b-127">Per poter accedere al calendario dell'utente nel contesto di un'applicazione, è necessario aggiungere l'autorizzazione delegata `Calendars.Read` alle informazioni di registrazione dell'applicazione e quindi aggiungere l'ambito `Calendars.Read` alla chiamata `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="2771b-127">In order to access the user’s calendar in the context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="2771b-128">Con l'aumentare del numero di ambiti è possibile che all'utente venga chiesto di esprimere anche altri tipi di consenso.</span><span class="sxs-lookup"><span data-stu-id="2771b-128">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<span data-ttu-id="2771b-129">Se per un'API back-end non è richiesto alcun ambito (non consigliabile), è possibile usare `clientId` come ambito nelle chiamate `acquireTokenSilent` e/o `acquireTokenRedirect`.</span><span class="sxs-lookup"><span data-stu-id="2771b-129">If a backend API does not require a scope (not recommended), you can use the `clientId` as the scope in the `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
