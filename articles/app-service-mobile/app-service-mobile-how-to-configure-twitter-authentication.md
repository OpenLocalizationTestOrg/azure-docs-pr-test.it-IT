---
title: autenticazione di Twitter tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come l'autenticazione di Twitter tooconfigure per l'applicazione di servizi di App.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Come tooconfigure l'account di accesso Twitter di toouse applicazione di servizio App
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

In questo argomento illustra come tooconfigure Azure App Service toouse Twitter come provider di autenticazione.

toocomplete hello in questa procedura, è necessario disporre di un account Twitter con un messaggio di posta elettronica verificato indirizzo e numero di telefono. toocreate un nuovo account Twitter, andare troppo<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"></a>Registrare l'applicazione con Twitter
1. Accesso toohello [portale di Azure]e passare tooyour applicazione. Copiare l' **URL**. Si utilizzerà questo tooconfigure app Twitter.
2. Passare toohello [agli sviluppatori di Twitter] sito Web, accedere con le credenziali dell'account Twitter e fare clic su **Create New App**.
3. Tipo di hello **nome** e **descrizione** per la nuova app. Incolla in un'applicazione **URL** per hello **sito Web** valore. Quindi, per hello **URL Callback**, incollare hello **URL Callback** copiato in precedenza. Questo è il gateway di App per dispositivi mobili con il percorso di hello, */.auth/login/twitter/callback*. ad esempio `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Assicurarsi che si sta utilizzando lo schema HTTPS hello.
4. Nella pagina di hello inferiore hello, leggere e accettare i termini di hello. Fare clic su **Create your Twitter application**. Questa app hello registri consente di visualizzare i dettagli dell'applicazione hello.
5. Fare clic su hello **impostazioni** scheda **consentire questa toosign toobe utilizzato applicazione con Twitter**, quindi fare clic su **le impostazioni di aggiornamento**.
6. Seleziona hello **chiavi e i token di accesso** scheda. Prendere nota dei valori hello di **Consumer tasto (API)** e **segreto del cliente (chiave privata API)**.
   
   > [!NOTE]
   > segreto del cliente Hello è un'importante credenziale di sicurezza. Non condividere questo valore con altri né distribuirlo con l'app.
   > 
   > 

## <a name="secrets"></a>Applicazione tooyour aggiungere Twitter
1. In hello [portale di Azure], passare tooyour applicazione. Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.
2. Se l'autenticazione di hello / non è abilitata la funzionalità di autorizzazione, l'opzione di hello troppo**su**.
3. Fare clic su **Twitter**. Incollare hello App ID e segreto dell'applicazione i valori che è stato ottenuto in precedenza. Fare quindi clic su **OK**.
   
   ![][1]
   
   Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API. È necessario autorizzare gli utenti nel codice dell'app.
4. (Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati tramite Twitter, impostare **tootake azione quando la richiesta non è autenticata** troppo**Twitter**. Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooTwitter per l'autenticazione.
5. Fare clic su **Salva**.

Si è ora pronto toouse Twitter per l'autenticazione nell'app.

## <a name="related-content"></a>Contenuti correlati
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[agli sviluppatori di Twitter]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portale di Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
