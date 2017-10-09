---
title: aaaAzure AD v2 JS SPA impostazione guidata - Test | Documenti Microsoft
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
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testare il codice

> ### <a name="testing-with-visual-studio"></a>Test con Visual Studio
> Se si utilizza Visual Studio, premere `F5` toorun il progetto: hello browser verrà aperto e si indirizza troppo*http://localhost: {porta}* in cui si vedere hello *chiamare API di Microsoft Graph* pulsante.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Test con Python o un altro server Web
> Se non si utilizza Visual Studio, assicurarsi che il server web sia avviato e sia configurato in base hello cartella contenente la porta TCP tooa toolisten il *index.html* file. Per Python, è possibile avviare l'ascolto hello porta toohello eseguendo il comando hello dei messaggi di richiesta / terminal, dalla cartella dell'applicazione hello:
> 
> ```bash
> python -m http.server 8080
> ```
>  Quindi, aprire il browser hello e digitare *http://localhost:8080* o *http://localhost: {porta}* - hello *porta* corrisponde toohello porta che il server web in attesa di. È necessario visualizzare il contenuto di hello della pagina index. HTML con hello *chiamare API di Microsoft Graph* pulsante.

## <a name="test-your-application"></a>Testare l'applicazione

Dopo aver browser hello carica il *index.html*, fare clic su hello *chiamare API di Microsoft Graph* pulsante. Se si tratta hello prima volta, i reindirizzamenti browser hello è toohello v2 di Microsoft Azure Active Directory endpoint, in cui si è richiesto toosign in.
 
![Schermata di esempio](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Consenso
Hello prima volta che accedi tooyour applicazione, verranno visualizzate con un consenso schermata simili toohello riportato di seguito, in cui è necessario tooaccept:

 ![Schermata di consenso](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Risultati previsti
Si noterà che le informazioni sul profilo utente restituiti da hello risposta chiamata di API di Microsoft Graph.
 
 ![Risultati](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Inoltre visualizzare le informazioni di base sui token hello acquisito in hello *Token di accesso* e *le attestazioni nei Token ID* caselle.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Altre informazioni sugli ambiti e sulle autorizzazioni delegate

API di Microsoft Graph Hello richiede hello `user.read` ambito tooread hello del profilo utente. Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione. Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti. Ad esempio, per Microsoft Graph, hello ambito `Calendars.Read` è calendari dell'utente di hello toolist obbligatorio. In ordine tooaccess hello del calendario dell'utente nel contesto di hello di un'applicazione, è necessario hello tooadd `Calendars.Read` informazioni di registrazione applicazione toohello di autorizzazione di delega e quindi aggiungere hello `Calendars.Read` toohello ambito `acquireTokenSilent` chiamare. utente Hello potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.

Se un'API back-end non è necessario un ambito (non consigliato), è possibile utilizzare hello `clientId` come ambito hello in hello `acquireTokenSilent` e/o `acquireTokenRedirect` chiamate.

<!--end-collapse-->
