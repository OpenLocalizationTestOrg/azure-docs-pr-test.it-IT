---
title: aaaAzure AD v2 Android Getting Started - Test | Documenti Microsoft
description: "Informazioni sul modo in cui un'app di Android può ottenere un token di accesso e chiamare l'API o le API Graph Microsoft che richiedono token di acceso dall'endpoint di Azure Active Directory v2"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="ac7ff-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="ac7ff-103">Test your code</span></span>

1. <span data-ttu-id="ac7ff-104">Distribuire il codice tooyour/emulatore di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="ac7ff-105">Quando sarai pronto tootest, utilizzare Microsoft Azure Active Directory (account aziendale) o un toosign di account Account Microsoft (live.com, outlook.com) in.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="ac7ff-106">![Schermata di esempio](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="ac7ff-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="ac7ff-107">
![Accesso](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="ac7ff-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="ac7ff-108">Consenso</span><span class="sxs-lookup"><span data-stu-id="ac7ff-108">Consent</span></span>
<span data-ttu-id="ac7ff-109">Hello prima volta che un utente accede tooyour applicazione, viene visualizzata con un seguente toohello consenso simile dello schermo, in cui è necessario accettare tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="ac7ff-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Consenso](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="ac7ff-111">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="ac7ff-111">Expected results</span></span>
<span data-ttu-id="ac7ff-112">Dovrebbe essere risultati hello di tooMicrosoft una chiamata API Graph 'me' endpoint utilizzato profilo utente di hello tootooobtain - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="ac7ff-113">Per un elenco degli endpoint di Microsoft Graph comuni, consultare questo [articolo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="ac7ff-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="ac7ff-114">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="ac7ff-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="ac7ff-115">API di Microsoft Graph Hello richiede hello `user.read` ambito tooread hello del profilo utente.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="ac7ff-116">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="ac7ff-117">Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="ac7ff-118">Ad esempio, per Microsoft Graph, hello ambito `Calendars.Read` è calendari dell'utente di hello toolist obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="ac7ff-119">In ordine tooaccess hello del calendario dell'utente in un contesto di un'applicazione, è necessario hello tooadd `Calendars.Read` informazioni di registrazione applicazione toohello di autorizzazione di delega e quindi aggiungere hello `Calendars.Read` toohello ambito `acquireTokenSilentAsync` chiamare.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="ac7ff-120">utente Hello potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.</span><span class="sxs-lookup"><span data-stu-id="ac7ff-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
