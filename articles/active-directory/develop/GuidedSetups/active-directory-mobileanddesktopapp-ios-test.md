---
title: iOS v2 aaaAzure AD Getting Started - Test | Documenti Microsoft
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="a7bea-103">Test query hello API di Microsoft Graph dall'applicazione iOS</span><span class="sxs-lookup"><span data-stu-id="a7bea-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="a7bea-104">Premere `Command`  +  `R` codice hello toorun nel simulatore hello.</span><span class="sxs-lookup"><span data-stu-id="a7bea-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Schermata di esempio](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="a7bea-106">Quando sarai pronto tootest, toccare *'Chiamare l'API di Microsoft Graph'* ed è il nome utente e password, sarà richiesta tootype.</span><span class="sxs-lookup"><span data-stu-id="a7bea-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="a7bea-107">Consenso</span><span class="sxs-lookup"><span data-stu-id="a7bea-107">Consent</span></span>
<span data-ttu-id="a7bea-108">Hello prima volta che accedi nell'applicazione tooyour, verrà visualizzata con un seguente toohello consenso simile dello schermo, in cui è necessario accettare tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="a7bea-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Schermata di consenso](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="a7bea-110">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="a7bea-110">Expected results</span></span>
<span data-ttu-id="a7bea-111">Informazioni sul profilo utente restituiti dalla chiamata all'API di Microsoft Graph hello in hello dovrebbe *registrazione* sezione.</span><span class="sxs-lookup"><span data-stu-id="a7bea-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="a7bea-112">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="a7bea-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="a7bea-113">API di Microsoft Graph Hello richiede hello `user.read` ambito tooread hello del profilo utente.</span><span class="sxs-lookup"><span data-stu-id="a7bea-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="a7bea-114">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="a7bea-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="a7bea-115">Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="a7bea-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="a7bea-116">Ad esempio, per Microsoft Graph, hello ambito `Calendars.Read` è calendari dell'utente di hello toolist obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="a7bea-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="a7bea-117">In ordine tooaccess hello del calendario dell'utente in un contesto di un'applicazione, è necessario hello tooadd `Calendars.Read` informazioni di registrazione applicazione toohello di autorizzazione di delega e quindi aggiungere hello `Calendars.Read` toohello ambito `acquireTokenSilent` chiamare.</span><span class="sxs-lookup"><span data-stu-id="a7bea-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="a7bea-118">utente Hello potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.</span><span class="sxs-lookup"><span data-stu-id="a7bea-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



