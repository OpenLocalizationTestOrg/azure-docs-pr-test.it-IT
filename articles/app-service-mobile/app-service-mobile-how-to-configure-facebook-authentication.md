---
title: autenticazione di Facebook tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come tooconfigure l'autenticazione di Facebook per l'applicazione di servizi di App.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Come tooconfigure l'account di accesso Facebook di toouse applicazione di servizio App
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

In questo argomento illustra come tooconfigure Azure App Service toouse Facebook come provider di autenticazione.

toocomplete hello in questa procedura, è necessario disporre di un account Facebook che dispone di un indirizzo di posta elettronica verificati e un numero di telefono cellulare. toocreate un nuovo account Facebook, andare troppo[facebook.com].

## <a name="register"></a>Registrare l'applicazione con Facebook
1. Accesso toohello [portale di Azure]e passare tooyour applicazione. Copiare l' **URL**. Si utilizzerà questo tooconfigure app Facebook.
2. In un'altra finestra del browser, passare toohello [sviluppatori Facebook] sito Web e Accedi con il Facebook delle credenziali dell'account.
3. (Facoltativo) Se non è stata già registrata, fare clic su **app** > **registrare gli sviluppatori**quindi accettare criteri hello e attenersi alla procedura di registrazione hello.
4. Fare clic su **My Apps** (App personali)  > **Add a New App** (Aggiungi una nuova app)  > **Website** (Sito Web)  > **Skip and Create App ID** (Ignora e crea ID app). 
5. In **nome visualizzato**, digitare un nome univoco per l'app, il tipo del **Contact Email**, scegliere un **categoria** per l'app, quindi fare clic su **creare ID App**e completare il controllo di sicurezza hello. Consente di procedere toohello dashboard dello sviluppatore per la nuova app Facebook.
6. In "Facebook Login" (Accesso a Facebook) fare clic su **Get Started**(Informazioni di base). Aggiungere l'applicazione **URI di reindirizzamento** troppo**URI di reindirizzamento di OAuth valido**, quindi fare clic su **Salva modifiche**. 
   
   > [!NOTE]
   > L'URI di reindirizzamento URL hello dell'applicazione con il percorso di hello, */.auth/login/facebook/callback*. ad esempio `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Assicurarsi che si sta utilizzando lo schema HTTPS hello.
   > 
   > 
7. Navigazione a sinistra di hello, fare clic su **impostazioni**. In hello **segreto dell'App** campo, fare clic su **Mostra**, fornire una password se richiesto, quindi prendere nota dei valori hello di **ID App** e **segreto dell'applicazione**. Usare questi tooconfigure successive l'applicazione in Azure.
   
   > [!IMPORTANT]
   > segreto dell'applicazione Hello è un'importante credenziale di sicurezza. Non condividere questo valore con altri e non distribuirlo all'interno di un'applicazione client.
   > 
   > 
8. Hello account Facebook è un'applicazione hello tooregister utilizzato sia un amministratore dell'applicazione hello. A questo punto, solo gli amministratori potranno effettuare l'accesso a questa applicazione. tooauthenticate altri account Facebook, fare clic su **revisione di App** e abilitare **pubblica assicurarsi < your-app-name >** accesso pubblico generale tooenable utilizzando l'autenticazione di Facebook.

## <a name="secrets"></a>Applicazione tooyour aggiungere Facebook
1. In hello [portale di Azure], passare tooyour applicazione. Fare clic su **Impostazioni** > **Autenticazione/Autorizzazione**, quindi assicurarsi che l'opzione **Autenticazione servizio app** sia impostata su **Sì**.
2. Fare clic su **Facebook**, incollare i valori ID dell'App e segreto dell'applicazione hello cui ottenuto in precedenza, se lo si desidera abilitare tutti gli ambiti richiesti dall'applicazione, quindi fare clic su **OK**.
   
    ![][0]
   
    Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API. È necessario autorizzare gli utenti nel codice dell'app.
3. (Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati da Facebook, impostare **tootake azione quando la richiesta non è autenticata** troppo**Facebook**. Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooFacebook per l'autenticazione.
4. Al termine della configurazione dell'autenticazione, fare clic su **Salva**.

Si è ora pronto toouse Facebook per l'autenticazione nell'app.

## <a name="related-content"></a>Contenuti correlati
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[sviluppatori Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portale di Azure]: https://portal.azure.com/
