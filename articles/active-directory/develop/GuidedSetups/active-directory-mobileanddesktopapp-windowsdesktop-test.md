---
title: Introduzione a Windows Desktop per Azure AD v2 - Test | Microsoft Docs
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="bca98-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="bca98-103">Test your code</span></span>

<span data-ttu-id="bca98-104">Per testare l'applicazione, premere `F5` per eseguire il progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bca98-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="bca98-105">Verrà visualizzata la finestra principale:</span><span class="sxs-lookup"><span data-stu-id="bca98-105">Your Main Window should appear:</span></span>

![Schermata di esempio](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="bca98-107">Quando si è pronti per eseguire il test, fare clic su *Call Microsoft Graph API* (Chiama API Microsoft Graph) e usare un account Microsoft Azure Active Directory (account aziendale) o un account Microsoft (live.com, outlook.com) per accedere.</span><span class="sxs-lookup"><span data-stu-id="bca98-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="bca98-108">Se è la prima volta, verrà visualizzata una finestra in cui si chiede all'utente di eseguire l'accesso:</span><span class="sxs-lookup"><span data-stu-id="bca98-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![Accesso](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="bca98-110">Consenso</span><span class="sxs-lookup"><span data-stu-id="bca98-110">Consent</span></span>
<span data-ttu-id="bca98-111">La prima volta che si accede all'applicazione, viene visualizzata una schermata di consenso, simile alla figura seguente, in cui è necessario accettare in modo esplicito:</span><span class="sxs-lookup"><span data-stu-id="bca98-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Schermata di consenso](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="bca98-113">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="bca98-113">Expected results</span></span>
<span data-ttu-id="bca98-114">Nella schermata API Call Results (Risultati chiamata API) vengono visualizzate le informazioni sul profilo utente restituite dalla chiamata all'API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="bca98-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="bca98-115">Nella casella Token Info (Informazioni sul token) vengono visualizzate anche informazioni di base sul token acquisite tramite `AcquireTokenAsync` o `AcquireTokenSilentAsync`:</span><span class="sxs-lookup"><span data-stu-id="bca98-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="bca98-116">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bca98-116">Property</span></span>  |<span data-ttu-id="bca98-117">Format</span><span class="sxs-lookup"><span data-stu-id="bca98-117">Format</span></span>  |<span data-ttu-id="bca98-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bca98-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="bca98-119">Nome</span><span class="sxs-lookup"><span data-stu-id="bca98-119">Name</span></span> | <span data-ttu-id="bca98-120">{Nome utente completo}</span><span class="sxs-lookup"><span data-stu-id="bca98-120">{User Full name}</span></span> |<span data-ttu-id="bca98-121">Nome e cognome dell'utente</span><span class="sxs-lookup"><span data-stu-id="bca98-121">The user’s first and last name</span></span>|
|<span data-ttu-id="bca98-122">Username</span><span class="sxs-lookup"><span data-stu-id="bca98-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="bca98-123">Nome utente usato per identificare l'utente</span><span class="sxs-lookup"><span data-stu-id="bca98-123">The username used to identify the user</span></span>|
|<span data-ttu-id="bca98-124">Token Expires (Scadenza token)</span><span class="sxs-lookup"><span data-stu-id="bca98-124">Token Expires</span></span> |<span data-ttu-id="bca98-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="bca98-125">{DateTime}</span></span>         |<span data-ttu-id="bca98-126">Ora in cui scadrà il token.</span><span class="sxs-lookup"><span data-stu-id="bca98-126">The time on which the token expires.</span></span> <span data-ttu-id="bca98-127">MSAL estende automaticamente la data di scadenza rinnovando il token ogni volta che è necessario</span><span class="sxs-lookup"><span data-stu-id="bca98-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="bca98-128">Token di accesso</span><span class="sxs-lookup"><span data-stu-id="bca98-128">Access token</span></span> |<span data-ttu-id="bca98-129">{Stringa}</span><span class="sxs-lookup"><span data-stu-id="bca98-129">{String}</span></span>         |<span data-ttu-id="bca98-130">Stringa di token che verrà inviata alle richieste HTTP che richiedono un'intestazione di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="bca98-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="bca98-131">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="bca98-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="bca98-132">L'API Graph richiede l'ambito `user.read` per leggere il profilo utente.</span><span class="sxs-lookup"><span data-stu-id="bca98-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="bca98-133">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="bca98-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="bca98-134">Altre API Graph e alcune API personalizzate per il server back-end richiedono anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="bca98-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="bca98-135">Graph, ad esempio, richiede l'ambito `Calendars.Read` per elencare i calendari degli utenti.</span><span class="sxs-lookup"><span data-stu-id="bca98-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="bca98-136">Per poter accedere al calendario dell'utente nel contesto di un'applicazione, è necessario aggiungere le informazioni di registrazione dell'applicazione delegata `Calendars.Read` e aggiungere `Calendars.Read` alla chiamata `AcquireTokenAsync`.</span><span class="sxs-lookup"><span data-stu-id="bca98-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="bca98-137">Con l'aumentare del numero di ambiti è possibile che all'utente venga chiesto di esprimere anche altri tipi di consenso.</span><span class="sxs-lookup"><span data-stu-id="bca98-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



