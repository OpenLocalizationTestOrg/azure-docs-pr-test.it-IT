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
## <a name="setting-up-your-web-server-or-project"></a>Impostazione del server Web o del progetto

> Se si preferisce toodownload progetto questo esempio invece, 
> - [Scaricare il progetto di Visual Studio hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> oppure
> - [Scaricare il file di progetto hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) per un server web locale, ad esempio Python
>
> E quindi ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.

## <a name="prerequisites"></a>Prerequisiti
Un server web locale, ad esempio [Python http.server](https://www.python.org/downloads/), [server http](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), o l'integrazione di IIS Express con [Visual Studio 2017](https://www.visualstudio.com/downloads/) è necessario toorun il programma di installazione guidata. 

Istruzioni di questa guida sono basate su Python sia Visual Studio 2017, ma sono disponibile toouse qualsiasi altro ambiente di sviluppo o un Server Web.

## <a name="create-your-project"></a>Creare il progetto 

> ### <a name="option-1-visual-studio"></a>Opzione 1: Visual Studio 
> Se si utilizza Visual Studio e si sta creando un nuovo progetto, attenersi alla procedura hello seguente toocreate una nuova soluzione di Visual Studio:
> 1.    In Visual Studio: `File` > `New` > `Project`
> 2.    In `Visual C#\Web` selezionare `ASP.NET Web Application (.NET Framework)`
> 3.    Assegnare un nome all'applicazione e fare clic su *OK*
> 4.    In `New ASP.NET Web Application` selezionare `Empty`

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Opzione 2: Python/altri server Web
> Verificare di avere installato [Python](https://www.python.org/downloads/), quindi eseguire il passaggio di hello riportato di seguito:
> - Creare una cartella toohost l'applicazione.


## <a name="create-your-single-page-applications-ui"></a>Creare l'interfaccia utente dell'applicazione a singola pagina
1.  Creare un file *index.html* per la SPA di JavaScript. Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), fare clic e selezionare: `Add`  >  `New Item`  >  `HTML page` e denominarlo index.html
2.  Aggiungere i seguenti codici tooyour hello:
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
