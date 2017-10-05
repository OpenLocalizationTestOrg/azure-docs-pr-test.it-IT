---
title: Endpoint v2.0 di Azure Active Directory | Microsoft Docs
description: Introduzione alla compilazione di app con l'accesso sia per account Microsoft che per Azure Active Directory.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1e286044fb1a1b367fcac2dc14c47f68d5ed120d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="c297a-103">Accesso per account Microsoft e utenti di Azure AD nella stessa app</span><span class="sxs-lookup"><span data-stu-id="c297a-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="c297a-104">In passato, gli sviluppatori di app che intendevano supportare sia gli account personali che quelli aziendali di Microsoft da Azure Active Directory dovevano eseguire l'integrazione con due sistemi separati.</span><span class="sxs-lookup"><span data-stu-id="c297a-104">In the past, an app developer who wanted to support both personal Microsoft accounts and work accounts from Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="c297a-105">L'**endpoint v2.0 di Azure AD** introduce una nuova versione dell'API di autenticazione che consente agli utenti di accedere con entrambi i tipi di account usando una semplice integrazione.</span><span class="sxs-lookup"><span data-stu-id="c297a-105">The **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you to sign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="c297a-106">Le app che usano l'endpoint v2.0 possono anche usare le API REST da [Microsoft Graph](https://graph.microsoft.io) con entrambi i tipi di account.</span><span class="sxs-lookup"><span data-stu-id="c297a-106">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c297a-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="c297a-107">Getting Started</span></span>
<span data-ttu-id="c297a-108">Scegliere dall'elenco seguente la piattaforma preferita per compilare un'app usando le nostre librerie open source e i framework.</span><span class="sxs-lookup"><span data-stu-id="c297a-108">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="c297a-109">In alternativa, è possibile usare la documentazione relativa al protocollo OAuth 2.0 e OpenID Connect per inviare e ricevere i messaggi di protocollo direttamente senza usare una libreria di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c297a-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="c297a-110">Novità</span><span class="sxs-lookup"><span data-stu-id="c297a-110">What's New</span></span>
<span data-ttu-id="c297a-111">Le informazioni fornite di seguito saranno utili per individuare le operazioni che possono essere eseguite o meno con l'endpoint v2.0.</span><span class="sxs-lookup"><span data-stu-id="c297a-111">The information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="c297a-112">Informazioni sui [tipi di app che si possono creare con l'endpoint v2.0](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="c297a-112">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="c297a-113">Informazioni su [limitazioni, restrizioni e vincoli](active-directory-v2-limitations.md) dell'endpoint v2.0.</span><span class="sxs-lookup"><span data-stu-id="c297a-113">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="c297a-114">Leggere questa panoramica video per l'endpoint v 2.0:</span><span class="sxs-lookup"><span data-stu-id="c297a-114">Check out this overview video for the v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="c297a-115">riferimento</span><span class="sxs-lookup"><span data-stu-id="c297a-115">Reference</span></span>
<span data-ttu-id="c297a-116">I collegamenti seguenti sono utili per un'esplorazione più approfondita della piattaforma:</span><span class="sxs-lookup"><span data-stu-id="c297a-116">These links will be useful for exploring the platform in depth:</span></span>

* [<span data-ttu-id="c297a-117">Riferimento al protocollo v2.0</span><span class="sxs-lookup"><span data-stu-id="c297a-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="c297a-118">Riferimento al token v2.0</span><span class="sxs-lookup"><span data-stu-id="c297a-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="c297a-119">Informazioni di riferimento sulla libreria v2.0</span><span class="sxs-lookup"><span data-stu-id="c297a-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="c297a-120">Ambiti e consenso nell'endpoint v2.0</span><span class="sxs-lookup"><span data-stu-id="c297a-120">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="c297a-121">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c297a-121">The Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="c297a-122">Guida e supporto</span><span class="sxs-lookup"><span data-stu-id="c297a-122">Help & Support</span></span>
<span data-ttu-id="c297a-123">Il modo migliore per ottenere assistenza per lo sviluppo in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c297a-123">These are the best places to get help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="c297a-124">Tag `azure-active-directory` e `adal` di Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="c297a-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="c297a-125">Commenti e suggerimenti su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c297a-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="c297a-126">Se occorre effettuare l'accesso agli account di lavoro e dell'istituto di istruzione da Azure Active Directory, è consigliabile iniziare con la [guida per gli sviluppatori di Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c297a-126">If you only need to sign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="c297a-127">L'uso dell'endpoint v2.0 è destinato agli sviluppatori che devono eseguire l'accesso agli account personali di Microsoft in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="c297a-127">The v2.0 endpoint is intended for use by developers who explicitly need to sign in Microsoft personal accounts.</span></span>

