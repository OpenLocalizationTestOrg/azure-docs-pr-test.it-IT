---
title: endpoint v 2.0 di Active Directory aaaAzure | Documenti Microsoft
description: Un'app di toobuilding introduzione con sign-in sia Account Microsoft e Azure Active Directory.
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
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="5c07e-103">Accesso per account Microsoft e utenti di Azure AD nella stessa app</span><span class="sxs-lookup"><span data-stu-id="5c07e-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="5c07e-104">In hello precedenti, uno sviluppatore di app che volevano toosupport entrambi gli account Microsoft personali e gli account di lavoro da Azure Active Directory è stato richiesto toointegrate con due sistemi separati.</span><span class="sxs-lookup"><span data-stu-id="5c07e-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="5c07e-105">Hello **endpoint v 2.0 di Azure AD** introduce una nuova versione di API di autenticazione che consente di toosign in entrambi i tipi di account con una facile integrazione.</span><span class="sxs-lookup"><span data-stu-id="5c07e-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="5c07e-106">Applicazioni che utilizzano endpoint v 2.0 hello possono usare anche le API REST da hello [Microsoft Graph](https://graph.microsoft.io) utilizzando dei tipi di account.</span><span class="sxs-lookup"><span data-stu-id="5c07e-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5c07e-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="5c07e-107">Getting Started</span></span>
<span data-ttu-id="5c07e-108">Scegliere la piattaforma preferita dal seguente elenco toobuild hello un'app usando il nostro librerie open source e Framework.</span><span class="sxs-lookup"><span data-stu-id="5c07e-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="5c07e-109">In alternativa, è possibile utilizzare il protocollo documentazione toosend di OAuth 2.0 e OpenID Connect e ricevere messaggi di protocollo direttamente senza usare una libreria di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="5c07e-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="5c07e-110">Novità</span><span class="sxs-lookup"><span data-stu-id="5c07e-110">What's New</span></span>
<span data-ttu-id="5c07e-111">informazioni di Hello qui saranno utili per comprendere cosa è & ciò che è possibile con endpoint v 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="5c07e-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="5c07e-112">Informazioni su hello [tipi di App, è possibile compilare con endpoint v 2.0 hello](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="5c07e-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="5c07e-113">Comprendere hello [vincoli, restrizioni e limitazioni](active-directory-v2-limitations.md) con endpoint v 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="5c07e-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="5c07e-114">Questa panoramica video per l'endpoint di hello v 2.0, consultare:</span><span class="sxs-lookup"><span data-stu-id="5c07e-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="5c07e-115">riferimento</span><span class="sxs-lookup"><span data-stu-id="5c07e-115">Reference</span></span>
<span data-ttu-id="5c07e-116">Questi collegamenti sono utili per l'esplorazione della piattaforma hello in modo approfondito:</span><span class="sxs-lookup"><span data-stu-id="5c07e-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="5c07e-117">Riferimento al protocollo v2.0</span><span class="sxs-lookup"><span data-stu-id="5c07e-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="5c07e-118">Riferimento al token v2.0</span><span class="sxs-lookup"><span data-stu-id="5c07e-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="5c07e-119">Informazioni di riferimento sulla libreria v2.0</span><span class="sxs-lookup"><span data-stu-id="5c07e-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="5c07e-120">Gli ambiti e consenso nell'endpoint di hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="5c07e-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="5c07e-121">Hello Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="5c07e-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="5c07e-122">Guida e supporto</span><span class="sxs-lookup"><span data-stu-id="5c07e-122">Help & Support</span></span>
<span data-ttu-id="5c07e-123">Si tratta di hello migliore posizioni tooget assistenza per lo sviluppo di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c07e-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="5c07e-124">Tag `azure-active-directory` e `adal` di Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="5c07e-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="5c07e-125">Commenti e suggerimenti su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c07e-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="5c07e-126">Se è necessario solo toosign gli account di lavoro e dell'istituto di istruzione da Azure Active Directory, è consigliabile iniziare con il nostro [Guida per gli sviluppatori di Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5c07e-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="5c07e-127">endpoint di Hello v 2.0 deve essere utilizzato dagli sviluppatori che necessitano di toosign negli account personale di Microsoft in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="5c07e-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

