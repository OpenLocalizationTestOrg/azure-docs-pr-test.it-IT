---
title: aaaAzure AD v2 Android Getting Started - Test | Documenti Microsoft
description: "Informazioni sul modo in cui un'app di Android può ottenere un token di accesso e chiamare l'API o le API Graph Microsoft che richiedono token di acceso dall'endpoint di Azure Active Directory v2"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testare il codice

1. Distribuire il codice tooyour/emulatore di dispositivo.
2. Quando sarai pronto tootest, utilizzare Microsoft Azure Active Directory (account aziendale) o un toosign di account Account Microsoft (live.com, outlook.com) in. 

![Schermata di esempio](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Accesso](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Consenso
Hello prima volta che un utente accede tooyour applicazione, viene visualizzata con un seguente toohello consenso simile dello schermo, in cui è necessario accettare tooexplicitly: 

![Consenso](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Risultati previsti
Dovrebbe essere risultati hello di tooMicrosoft una chiamata API Graph 'me' endpoint utilizzato profilo utente di hello tootooobtain - https://graph.microsoft.com/v1.0/me. Per un elenco degli endpoint di Microsoft Graph comuni, consultare questo [articolo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Altre informazioni sugli ambiti e sulle autorizzazioni delegate

API di Microsoft Graph Hello richiede hello `user.read` ambito tooread hello del profilo utente. Per impostazione predefinita, questo ambito viene aggiunto automaticamente in ogni applicazione registrata nel portale di registrazione. Altre API per Microsoft Graph e le API personalizzate per il server di back-end potrebbero richiedere anche altri ambiti. Ad esempio, per Microsoft Graph, hello ambito `Calendars.Read` è calendari dell'utente di hello toolist obbligatorio. In ordine tooaccess hello del calendario dell'utente in un contesto di un'applicazione, è necessario hello tooadd `Calendars.Read` informazioni di registrazione applicazione toohello di autorizzazione di delega e quindi aggiungere hello `Calendars.Read` toohello ambito `acquireTokenSilentAsync` chiamare. utente Hello potrebbe essere richieste autorizzazioni aggiuntive quando si aumenta il numero di hello degli ambiti.

<!--end-collapse-->
