---
title: iOS v2 aaaAzure AD Getting Started - Test | Documenti Microsoft
description: "Informazioni sulle modalità per le applicazioni iOS (Swift) per chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Test query hello API di Microsoft Graph dall'applicazione iOS

Premere `Command`  +  `R` codice hello toorun nel simulatore hello.

![Schermata di esempio](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Quando sarai pronto tootest, toccare *'Chiamare l'API di Microsoft Graph'* ed è il nome utente e password, sarà richiesta tootype.

### <a name="consent"></a>Consenso
Hello prima volta che accedi nell'applicazione tooyour, verrà visualizzata con un seguente toohello consenso simile dello schermo, in cui è necessario accettare tooexplicitly:

![Schermata di consenso](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Risultati previsti
Informazioni sul profilo utente restituiti dalla chiamata all'API di Microsoft Graph hello in hello dovrebbe *registrazione* sezione.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Altre informazioni sugli ambiti e sulle autorizzazioni delegate

API di Microsoft Graph Hello richiede hello `user.read` ambito tooread hello del profilo utente. Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione. Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti. Ad esempio, per Microsoft Graph, hello ambito `Calendars.Read` è calendari dell'utente di hello toolist obbligatorio. In ordine tooaccess hello del calendario dell'utente in un contesto di un'applicazione, è necessario hello tooadd `Calendars.Read` informazioni di registrazione applicazione toohello di autorizzazione di delega e quindi aggiungere hello `Calendars.Read` toohello ambito `acquireTokenSilent` chiamare. utente Hello potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.

<!--end-collapse-->



