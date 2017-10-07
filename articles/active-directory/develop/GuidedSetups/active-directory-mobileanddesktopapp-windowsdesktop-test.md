---
title: aaaAzure AD v2 Windows Desktop Getting Started - Test | Documenti Microsoft
description: Come applicazioni .NET per Windows Desktop (XAML) possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testare il codice

Ordinare tootest dell'applicazione, premere `F5` toorun il progetto in Visual Studio. Verrà visualizzata la finestra principale:

![Schermata di esempio](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Quando sarai pronto tootest, fare clic su *chiamare API di Microsoft Graph* e utilizzare Microsoft Azure Active Directory (account aziendale) o un toosign di account Account Microsoft (live.com, outlook.com) in. Si è hello prima volta, viene visualizzata una finestra toosign utente in:

![Accesso](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Consenso
Hello prima volta che accedi nell'applicazione tooyour, verrà visualizzata con un seguente toohello consenso simile dello schermo, in cui è necessario accettare tooexplicitly:

![Schermata di consenso](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Risultati previsti
Dovrebbe essere restituite dalla chiamata all'API Graph di Microsoft hello nella schermata di risultati di chiamare API hello informazioni del profilo utente.

Verrà visualizzato anche le informazioni di base token hello acquisito tramite `AcquireTokenAsync` o `AcquireTokenSilentAsync` nella casella di informazioni sul Token hello:

|Proprietà  |Format  |Descrizione |
|---------|---------|---------|
|Nome | {Nome utente completo} |utente Hello e del cognome|
|Username |<span>user@domain.com</span> |nome utente Hello utilizzato tooidentify hello|
|Token Expires (Scadenza token) |{DateTime}         |ora di Hello di quali hello scadenza del token. MSAL verrà esteso data di scadenza hello è Rinnovando il token hello quando necessario|
|Token di accesso |{Stringa}         |stringa di token hello inviati che riceverà le richieste di tooHTTP che richiedono un'intestazione di autorizzazione|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Altre informazioni sugli ambiti e sulle autorizzazioni delegate
API Graph richiede hello `user.read` profilo utente tooread di ambito. Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione. Altre API Graph e alcune API personalizzate per il server back-end richiedono anche altri ambiti. Ad esempio, per grafico, `Calendars.Read` è calendari dell'utente toolist obbligatorio. In ordine tooaccess hello del calendario dell'utente in un contesto di un'applicazione, è necessario tooadd `Calendars.Read` delegati informazioni di registrazione dell'applicazione e quindi aggiungere `Calendars.Read` toohello `AcquireTokenAsync` chiamare. Utente potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.

<!--end-collapse-->



