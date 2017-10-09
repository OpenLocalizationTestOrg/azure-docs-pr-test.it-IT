---
title: un'applicazione con endpoint v 2.0 hello Azure AD tramite il portale di hello aaaRegister | Documenti Microsoft
description: "La modalità di servizi utilizzando hello v 2.0 endpoint tooregister un'app con Microsoft per l'attivazione di accesso e l'accesso a Microsoft"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="d1057-103">Come un'app con endpoint v 2.0 hello tooregister</span><span class="sxs-lookup"><span data-stu-id="d1057-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="d1057-104">un'applicazione che accetta sia MSA & Azure AD toobuild sign-in, è prima necessario tooregister un'app con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d1057-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="d1057-105">A questo punto, è non essere in grado di toouse qualsiasi App esistenti con Azure Active Directory o account del servizio gestito, è necessario toocreate una marca di uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="d1057-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="d1057-106">Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="d1057-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="d1057-107">toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d1057-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="d1057-108">Visitare il portale di registrazione app Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="d1057-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="d1057-109">Innanzitutto, passa troppo[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="d1057-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="d1057-110">Il nuovo portale di registrazione delle app consente di gestire le app Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d1057-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="d1057-111">Accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="d1057-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="d1057-112">Se non si dispone di alcun account, iscriversi per creare un nuovo account personale.</span><span class="sxs-lookup"><span data-stu-id="d1057-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="d1057-113">La procedura richiederà pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d1057-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="d1057-114">Dopo aver completato l'operazione,</span><span class="sxs-lookup"><span data-stu-id="d1057-114">Done?</span></span> <span data-ttu-id="d1057-115">è possibile esaminare l'elenco delle app Microsoft, che probabilmente sarà vuoto.</span><span class="sxs-lookup"><span data-stu-id="d1057-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="d1057-116">A tale scopo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="d1057-116">Let's change that.</span></span>

<span data-ttu-id="d1057-117">Fare clic sul pulsante per **aggiungere un'app**e attribuirle un nome.</span><span class="sxs-lookup"><span data-stu-id="d1057-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="d1057-118">portale Hello assegnerà app Id univoco globale dell'applicazione che verrà utilizzato successivamente nel codice.</span><span class="sxs-lookup"><span data-stu-id="d1057-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="d1057-119">Se l'applicazione include un componente sul lato server che necessita di token di accesso per chiamare le API (pensare: Office, Azure o API web proprie), è opportuno toocreate un **segreto dell'applicazione** anche qui.</span><span class="sxs-lookup"><span data-stu-id="d1057-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="d1057-120">Successivamente, aggiungere hello piattaforme che verrà utilizzati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d1057-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="d1057-121">Per le applicazioni basate sul Web, specificare un **URI di reindirizzamento** dove possono essere inviati messaggi di accesso.</span><span class="sxs-lookup"><span data-stu-id="d1057-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="d1057-122">App per dispositivi mobili, copia verso il valore predefinito di hello reindirizzare l'uri creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d1057-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="d1057-123">Facoltativamente, è possibile personalizzare hello aspetto della pagina di accesso nel profilo hello.</span><span class="sxs-lookup"><span data-stu-id="d1057-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="d1057-124">Verificare che tooclick **salvare** prima di proseguire.</span><span class="sxs-lookup"><span data-stu-id="d1057-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="d1057-125">Quando si crea un'applicazione utilizzando [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), un'applicazione hello verrà registrata nel tenant di home hello di hello che l'account utilizzato toosign portale hello.</span><span class="sxs-lookup"><span data-stu-id="d1057-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="d1057-126">Ciò significa che non è possibile registrare un'applicazione nel tenant di Azure AD usando un account Microsoft personale.</span><span class="sxs-lookup"><span data-stu-id="d1057-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="d1057-127">Se in modo esplicito desidera tooregister un'applicazione in un particolare tenant, accedere con un account creato in origine in tale tenant.</span><span class="sxs-lookup"><span data-stu-id="d1057-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="d1057-128">Creare un'app di avvio rapido</span><span class="sxs-lookup"><span data-stu-id="d1057-128">Build a quick start app</span></span>
<span data-ttu-id="d1057-129">Dopo aver creato un'app Microsoft, è possibile completare una delle esercitazioni rapide v2.0.</span><span class="sxs-lookup"><span data-stu-id="d1057-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="d1057-130">Di seguito sono elencati alcuni suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d1057-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

