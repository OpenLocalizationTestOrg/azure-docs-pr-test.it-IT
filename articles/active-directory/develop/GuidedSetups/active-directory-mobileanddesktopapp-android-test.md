---
title: Introduzione ad Android per Azure AD v2 - Test | Microsoft Docs
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="43069-103">Testare il codice</span><span class="sxs-lookup"><span data-stu-id="43069-103">Test your code</span></span>

1. <span data-ttu-id="43069-104">Distribuire il codice nel dispositivo/emulatore.</span><span class="sxs-lookup"><span data-stu-id="43069-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="43069-105">Quando si è pronti per eseguire il test, usare un account Microsoft Azure Active Directory (account aziendale) o un account Microsoft (live.com, outlook.com) per accedere.</span><span class="sxs-lookup"><span data-stu-id="43069-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="43069-106">![Schermata di esempio](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="43069-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="43069-107">
![Accesso](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="43069-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="43069-108">Consenso</span><span class="sxs-lookup"><span data-stu-id="43069-108">Consent</span></span>
<span data-ttu-id="43069-109">La prima volta che un utente accede all'applicazione, viene visualizzata una schermata di consenso, simile alla figura seguente, in cui è necessario accettare in modo esplicito:</span><span class="sxs-lookup"><span data-stu-id="43069-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Consenso](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="43069-111">Risultati previsti</span><span class="sxs-lookup"><span data-stu-id="43069-111">Expected results</span></span>
<span data-ttu-id="43069-112">Dovrebbero essere visualizzati i risultati di una chiamata all'endpoint 'me' dell'API Microsoft Graph usato per ottenere il profilo utente: https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="43069-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="43069-113">Per un elenco degli endpoint di Microsoft Graph comuni, consultare questo [articolo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="43069-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="43069-114">Altre informazioni sugli ambiti e sulle autorizzazioni delegate</span><span class="sxs-lookup"><span data-stu-id="43069-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="43069-115">L'API di Microsoft Graph richiede l'ambito `user.read` per leggere il profilo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="43069-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="43069-116">Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione.</span><span class="sxs-lookup"><span data-stu-id="43069-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="43069-117">Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="43069-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="43069-118">Ad esempio, per Microsoft Graph, l'ambito `Calendars.Read` è necessario per elencare i calendari dell'utente.</span><span class="sxs-lookup"><span data-stu-id="43069-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="43069-119">Per poter accedere al calendario dell'utente nel contesto di un'applicazione, è necessario aggiungere l'autorizzazione delegata `Calendars.Read` alle informazioni di registrazione dell'applicazione e quindi aggiungere l'ambito `Calendars.Read` alla chiamata `acquireTokenSilentAsync`.</span><span class="sxs-lookup"><span data-stu-id="43069-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="43069-120">Con l'aumentare del numero di ambiti è possibile che all'utente venga chiesto di esprimere anche altri tipi di consenso.</span><span class="sxs-lookup"><span data-stu-id="43069-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
