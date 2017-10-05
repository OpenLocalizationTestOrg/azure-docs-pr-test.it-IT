---
title: Registrare un'applicazione con l'endpoint 2.0 di Azure AD usando il portale | Documentazione Microsoft
description: Come registrare un'app in Microsoft per abilitare l'accesso ai servizi Microsoft tramite l'endpoint v2.0
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
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="dac30-103">Come registrare un'app con l'endpoint v2.0</span><span class="sxs-lookup"><span data-stu-id="dac30-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="dac30-104">Per creare un'app che consente di accedere tramite account Microsoft e Azure AD, è innanzitutto necessario registrare un'app con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dac30-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="dac30-105">Con gli account Azure AD o Microsoft non sarà possibile usare un'app esistente, ma è necessario crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="dac30-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="dac30-106">Non tutti gli scenari e le funzionalità di Azure Active Directory sono supportati dall'endpoint 2.0.</span><span class="sxs-lookup"><span data-stu-id="dac30-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="dac30-107">Per determinare se è necessario usare l'endpoint v2.0, leggere le informazioni sulle [limitazioni v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="dac30-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="dac30-108">Visitare il portale di registrazione delle app Microsoft</span><span class="sxs-lookup"><span data-stu-id="dac30-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="dac30-109">Per prima cosa, passare a [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="dac30-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="dac30-110">Il nuovo portale di registrazione delle app consente di gestire le app Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dac30-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="dac30-111">Accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="dac30-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="dac30-112">Se non si dispone di alcun account, iscriversi per creare un nuovo account personale.</span><span class="sxs-lookup"><span data-stu-id="dac30-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="dac30-113">La procedura richiederà pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="dac30-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="dac30-114">Dopo aver completato l'operazione,</span><span class="sxs-lookup"><span data-stu-id="dac30-114">Done?</span></span> <span data-ttu-id="dac30-115">è possibile esaminare l'elenco delle app Microsoft, che probabilmente sarà vuoto.</span><span class="sxs-lookup"><span data-stu-id="dac30-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="dac30-116">A tale scopo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="dac30-116">Let's change that.</span></span>

<span data-ttu-id="dac30-117">Fare clic sul pulsante per **aggiungere un'app**e attribuirle un nome.</span><span class="sxs-lookup"><span data-stu-id="dac30-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="dac30-118">Il portale assegnerà all'app un ID applicazione univoco globale che verrà usato successivamente nel codice.</span><span class="sxs-lookup"><span data-stu-id="dac30-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="dac30-119">Se l’app include un componente sul lato server che necessità di token di accesso per chiamare le API (ad esempio, Office, Azure o un’API Web), è opportuno creare anche un **segreto dell’applicazione** .</span><span class="sxs-lookup"><span data-stu-id="dac30-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="dac30-120">Successivamente, aggiungere le piattaforme usate dall'app.</span><span class="sxs-lookup"><span data-stu-id="dac30-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="dac30-121">Per le applicazioni basate sul Web, specificare un **URI di reindirizzamento** dove possono essere inviati messaggi di accesso.</span><span class="sxs-lookup"><span data-stu-id="dac30-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="dac30-122">Per le app per dispositivi mobili, copiare l'URI di reindirizzamento predefinito creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dac30-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="dac30-123">Facoltativamente, è possibile personalizzare l'aspetto della pagina di accesso nella sezione del profilo.</span><span class="sxs-lookup"><span data-stu-id="dac30-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="dac30-124">Assicurarsi di **salvare** prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="dac30-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="dac30-125">Quando si crea un'applicazione usando [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), l'applicazione verrà registrata nel tenant home dell'account usato per accedere al portale.</span><span class="sxs-lookup"><span data-stu-id="dac30-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="dac30-126">Ciò significa che non è possibile registrare un'applicazione nel tenant di Azure AD usando un account Microsoft personale.</span><span class="sxs-lookup"><span data-stu-id="dac30-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="dac30-127">Se si desidera registrare  in modo esplicito un'applicazione in un particolare tenant, accedere con un account creato nel tenant.</span><span class="sxs-lookup"><span data-stu-id="dac30-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="dac30-128">Creare un'app di avvio rapido</span><span class="sxs-lookup"><span data-stu-id="dac30-128">Build a quick start app</span></span>
<span data-ttu-id="dac30-129">Dopo aver creato un'app Microsoft, è possibile completare una delle esercitazioni rapide v2.0.</span><span class="sxs-lookup"><span data-stu-id="dac30-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="dac30-130">Di seguito sono elencati alcuni suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="dac30-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

