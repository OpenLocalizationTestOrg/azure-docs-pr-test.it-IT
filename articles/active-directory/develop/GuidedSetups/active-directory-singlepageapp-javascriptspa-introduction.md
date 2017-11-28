---
title: 'Configurazione guidata di JS SPA per Azure AD v2: introduzione | Microsoft Docs'
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
ms.openlocfilehash: 3d195d0d67f8f82c9450ffd93767917698addee3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="29603-103">Chiamare l'API di Microsoft Graph da un'applicazione a singola pagina (SPA) di JavaScript</span><span class="sxs-lookup"><span data-stu-id="29603-103">Call the Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="29603-104">Questa guida dimostra come un'applicazione a pagina singola JavaScript possa accedere ad account personali, aziendali e dell'istituto di istruzione, ottenere un token di accesso e chiamare l'API Microsoft Graph o altre API che richiedono token di accesso dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="29603-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API or other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="29603-105">Come interpretare questa guida</span><span class="sxs-lookup"><span data-stu-id="29603-105">How this guide works</span></span>

![Funzionamento dell'app di esempio generata da questa guida](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="29603-107">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="29603-107">More Information</span></span>

<span data-ttu-id="29603-108">L'applicazione di esempio creata in questa guida consente a una SPA di Javascript di eseguire query nell'API di Microsoft Graph o in un'API Web che accetta token dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="29603-108">The sample application created by this guide enables a JavaScript SPA to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="29603-109">Per questo scenario, dopo l'accesso di un utente, viene richiesto e aggiunto un token di accesso a richieste HTTP tramite l'intestazione dell'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="29603-109">For this scenario, after a user signs-in, an access token is requested and added to HTTP requests via the authorization header.</span></span> <span data-ttu-id="29603-110">L'acquisizione e il rinnovo del token vengono gestiti da Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="29603-110">Token acquisition and renewal are handled by the Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="29603-111">Librerie</span><span class="sxs-lookup"><span data-stu-id="29603-111">Libraries</span></span>

<span data-ttu-id="29603-112">Questa guida usa la libreria seguente:</span><span class="sxs-lookup"><span data-stu-id="29603-112">This guide uses the following library:</span></span>

|<span data-ttu-id="29603-113">Libreria</span><span class="sxs-lookup"><span data-stu-id="29603-113">Library</span></span>|<span data-ttu-id="29603-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="29603-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="29603-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="29603-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="29603-116">Authentication Library di Microsoft per l'anteprima di JavaScript</span><span class="sxs-lookup"><span data-stu-id="29603-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="29603-117">*msal.js* specifica come destinazione l'*endpoint di Azure Active Directory v2*, che consente agli account personali, aziendali e dell'istituto di istruzione di eseguire l'accesso e di acquisire i token.</span><span class="sxs-lookup"><span data-stu-id="29603-117">*msal.js* targets the *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts to sign in and acquire tokens.</span></span> <span data-ttu-id="29603-118">L'*endpoint di Azure Active Directory v2* ha [alcune limitazioni](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="29603-118">The *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="29603-119">Se si è interessati solo ad account aziendali e dell'istituto di istruzione, usare *adal.js* e l'*endpoint V1*.</span><span class="sxs-lookup"><span data-stu-id="29603-119">If you are interested only in school and work accounts, use *adal.js* and the *V1 endpoint*.</span></span> <span data-ttu-id="29603-120">Per conoscere le differenze tra gli endpoint v1 e v2, vedere il [confronto tra v1 e v2](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="29603-120">To understand differences between the v1 and v2 endpoints read the [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
