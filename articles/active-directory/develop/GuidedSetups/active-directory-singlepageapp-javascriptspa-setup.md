---
title: aaaAzure AD v2 JS SPA interattiva installazione - installazione | Documenti Microsoft
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="6c9e9-103">Impostazione del server Web o del progetto</span><span class="sxs-lookup"><span data-stu-id="6c9e9-103">Setting up your web server or project</span></span>

> <span data-ttu-id="6c9e9-104">Se si preferisce toodownload progetto questo esempio invece,</span><span class="sxs-lookup"><span data-stu-id="6c9e9-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="6c9e9-105">Scaricare il progetto di Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="6c9e9-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="6c9e9-106">oppure</span><span class="sxs-lookup"><span data-stu-id="6c9e9-106">or</span></span>
> - <span data-ttu-id="6c9e9-107">[Scaricare il file di progetto hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) per un server web locale, ad esempio Python</span><span class="sxs-lookup"><span data-stu-id="6c9e9-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="6c9e9-108">E quindi ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6c9e9-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c9e9-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6c9e9-109">Prerequisites</span></span>
<span data-ttu-id="6c9e9-110">Un server web locale, ad esempio [Python http.server](https://www.python.org/downloads/), [server http](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), o l'integrazione di IIS Express con [Visual Studio 2017](https://www.visualstudio.com/downloads/) è necessario toorun il programma di installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="6c9e9-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="6c9e9-111">Istruzioni di questa guida sono basate su Python sia Visual Studio 2017, ma sono disponibile toouse qualsiasi altro ambiente di sviluppo o un Server Web.</span><span class="sxs-lookup"><span data-stu-id="6c9e9-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="6c9e9-112">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="6c9e9-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="6c9e9-113">Opzione 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6c9e9-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="6c9e9-114">Se si utilizza Visual Studio e si sta creando un nuovo progetto, attenersi alla procedura hello seguente toocreate una nuova soluzione di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6c9e9-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="6c9e9-115">In Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="6c9e9-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="6c9e9-116">In `Visual C#\Web` selezionare `ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="6c9e9-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="6c9e9-117">Assegnare un nome all'applicazione e fare clic su *OK*</span><span class="sxs-lookup"><span data-stu-id="6c9e9-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="6c9e9-118">In `New ASP.NET Web Application` selezionare `Empty`</span><span class="sxs-lookup"><span data-stu-id="6c9e9-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="6c9e9-119">Opzione 2: Python/altri server Web</span><span class="sxs-lookup"><span data-stu-id="6c9e9-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="6c9e9-120">Verificare di avere installato [Python](https://www.python.org/downloads/), quindi eseguire il passaggio di hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6c9e9-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="6c9e9-121">Creare una cartella toohost l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c9e9-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="6c9e9-122">Creare l'interfaccia utente dell'applicazione a singola pagina</span><span class="sxs-lookup"><span data-stu-id="6c9e9-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="6c9e9-123">Creare un file *index.html* per la SPA di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6c9e9-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="6c9e9-124">Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), fare clic e selezionare: `Add`  >  `New Item`  >  `HTML page` e denominarlo index.html</span><span class="sxs-lookup"><span data-stu-id="6c9e9-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="6c9e9-125">Aggiungere i seguenti codici tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="6c9e9-125">Add hello following code tooyour page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
