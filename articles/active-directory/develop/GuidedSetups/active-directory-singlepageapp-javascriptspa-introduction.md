---
title: aaaAzure AD v2 JS SPA interattiva installazione - Introduzione | Documenti Microsoft
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
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="1e675-103">Hello chiamata API di Microsoft Graph dall'applicazione di pagina singola (SPA) un JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e675-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="1e675-104">Questa guida illustra come lavoro personale, può accedere un JavaScript singola pagina applicazione (SPA) e account scuola, ottenere un token di accesso e chiamare l'API di Microsoft Graph hello o altre API che richiedono token di accesso di hello endpoint v2 Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e675-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="1e675-105">Come interpretare questa guida</span><span class="sxs-lookup"><span data-stu-id="1e675-105">How this guide works</span></span>

![Funzionamento delle app di esempio hello generati da questa Guida](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="1e675-107">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="1e675-107">More Information</span></span>

<span data-ttu-id="1e675-108">applicazione di esempio Hello creata da questa Guida consente un hello tooquery SPA JavaScript Microsoft Graph API o un'API Web che accetta i token dall'endpoint di Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="1e675-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="1e675-109">Per questo scenario, dopo che un utente firma in un token di accesso è richieste tooHTTP richiesto e aggiunti tramite l'intestazione di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e675-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="1e675-110">Acquisizione del token e il rinnovo vengono gestiti da hello libreria di autenticazione di Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="1e675-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="1e675-111">Librerie</span><span class="sxs-lookup"><span data-stu-id="1e675-111">Libraries</span></span>

<span data-ttu-id="1e675-112">Questa Guida Usa hello seguente libreria:</span><span class="sxs-lookup"><span data-stu-id="1e675-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="1e675-113">Libreria</span><span class="sxs-lookup"><span data-stu-id="1e675-113">Library</span></span>|<span data-ttu-id="1e675-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1e675-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="1e675-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="1e675-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="1e675-116">Authentication Library di Microsoft per l'anteprima di JavaScript</span><span class="sxs-lookup"><span data-stu-id="1e675-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="1e675-117">*msal.js* hello destinazioni *endpoint di Azure Active Directory v2* -che abilita toosign account personali, dell'istituto di istruzione e aziendali in e acquisire i token.</span><span class="sxs-lookup"><span data-stu-id="1e675-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="1e675-118">Hello *endpoint di Azure Active Directory v2* è [alcune limitazioni](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="1e675-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="1e675-119">Se si è interessati solo gli account di lavoro e dell'istituto di istruzione, utilizzare *adal.js* hello e *V1 endpoint*.</span><span class="sxs-lookup"><span data-stu-id="1e675-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="1e675-120">toounderstand differenze tra gli endpoint v1 e v2 hello leggere hello [v1, v2 confronto](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="1e675-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
