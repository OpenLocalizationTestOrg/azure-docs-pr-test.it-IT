---
title: 'Introduzione a iOS con Azure AD v2: test | Microsoft Docs'
description: "Informazioni sulle modalità per le applicazioni iOS (Swift) per chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 4a88096d2b0a23708acdbc1798eac528599b4f71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
## <a name="test-querying-the-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="a73bf-103">Verificare l'esecuzione di query di API Graph di Microsoft dall'applicazione iOS</span><span class="sxs-lookup"><span data-stu-id="a73bf-103">Test querying the Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="a73bf-104">Premere `Command` + `R` per eseguire il codice nel simulatore.</span><span class="sxs-lookup"><span data-stu-id="a73bf-104">Press `Command` + `R` to run the code in the simulator.</span></span>

![Schermata di esempio](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="a73bf-106">Quando si è pronti per eseguire il test, toccare *"Call Microsoft Graph API"* (Chiamare l'API Graph di MIcrosoft) e verrà richiesto di digitare il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="a73bf-106">When you're ready to test, tap *‘Call Microsoft Graph API’* and you will be prompted to type your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="a73bf-107">Consenso</span><span class="sxs-lookup"><span data-stu-id="a73bf-107">Consent</span></span>
<span data-ttu-id="a73bf-108">La prima volta che si accede all'applicazione, viene visualizzata una schermata di consenso, simile alla figura seguente, in cui è necessario accettare in modo esplicito:</span><span class="sxs-lookup"><span data-stu-id="a73bf-108">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Schermata di consenso](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="a73bf-110">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="a73bf-110">Expected results</span></span>
<span data-ttu-id="a73bf-111">Si dovrebbero visualizzare le informazioni del profilo utente restituite dalla chiamata dell'API Microsoft Graph nella sezione *Registrazione*.</span><span class="sxs-lookup"><span data-stu-id="a73bf-111">You should see user profile information returned by the Microsoft Graph API call in the *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="a73bf-112">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="a73bf-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="a73bf-113">L'API di Microsoft Graph richiede l'ambito `user.read` per leggere il profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a73bf-113">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="a73bf-114">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="a73bf-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="a73bf-115">Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="a73bf-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="a73bf-116">Ad esempio, per Microsoft Graph, l'ambito `Calendars.Read` è necessario per elencare i calendari dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a73bf-116">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="a73bf-117">Per poter accedere al calendario dell'utente nel contesto di un'applicazione, è necessario aggiungere l'autorizzazione delegata `Calendars.Read` alle informazioni di registrazione dell'applicazione e quindi aggiungere l'ambito `Calendars.Read` alla chiamata `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="a73bf-117">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="a73bf-118">Con l'aumentare del numero di ambiti è possibile che all'utente venga chiesto di esprimere anche altri tipi di consenso.</span><span class="sxs-lookup"><span data-stu-id="a73bf-118">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



