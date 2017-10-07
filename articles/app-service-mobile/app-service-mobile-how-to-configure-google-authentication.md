---
title: autenticazione di Google tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come l'autenticazione di Google tooconfigure per l'applicazione di servizi di App.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Come tooconfigure l'account di Google accesso toouse di applicazione di servizio App
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

In questo argomento illustra come tooconfigure Azure App Service toouse Google come provider di autenticazione.

toocomplete hello in questa procedura, è necessario disporre di un account di Google che dispone di un indirizzo di posta elettronica verificato. toocreate un nuovo account di Google, andare troppo[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"></a>Registrare l'applicazione con Google
1. Accesso toohello [portale di Azure]e passare tooyour applicazione. Copia il **URL**, che si utilizza tooconfigure successive dell'app di Google.
2. Passare toohello [API Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) sito Web, accedere con le credenziali dell'account Google, fare clic su **Crea progetto**, fornire un **nome progetto**, quindi fare clic su  **Creare**.
3. In **API Social** fare clic **Google+ API** e quindi su **Abilita**.
4. Nel riquadro di spostamento, sinistro hello **credenziali** > **schermata consenso OAuth**, quindi selezionare il **indirizzo di posta elettronica**, immettere un **Product Name**, fare clic su **salvare**.
5. In hello **credenziali** scheda, fare clic su **creare credenziali** > **ID client OAuth**, quindi selezionare **applicazione Web**.
6. Incolla hello servizio App **URL** è copiato in precedenza in **Authorized JavaScript Origins**, quindi incollare il reindirizzamento URI in **autorizzato l'URI di reindirizzamento**. URI di reindirizzamento URL hello dell'applicazione con il percorso di hello, Hello */.auth/login/google/callback*. ad esempio `https://contoso.azurewebsites.net/.auth/login/google/callback`. Assicurarsi che si sta utilizzando lo schema HTTPS hello. Fare quindi clic su **Crea**.
7. Nella schermata successiva hello, prendere nota dei valori di hello del client hello segreto ID e client.

    > [!IMPORTANT]
    > segreto client hello è un'importante credenziale di sicurezza. Non condividere questo valore con altri e non distribuirlo all'interno di un'applicazione client.


## <a name="secrets"></a>Tooyour Google Aggiungi applicazione
1. In hello [portale di Azure], passare tooyour applicazione. Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.
2. Se l'autenticazione di hello / non è abilitata la funzionalità di autorizzazione, l'opzione di hello troppo**su**.
3. Fare clic su **Google**. Incollare i valori ID dell'App e segreto dell'applicazione hello cui ottenuto in precedenza e facoltativamente abilitare tutti gli ambiti che richiede l'applicazione. Fare quindi clic su **OK**.
   
   ![][1]
   
   Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API. È necessario autorizzare gli utenti nel codice dell'app.
4. (Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati da Google, impostare **tootake azione quando la richiesta non è autenticata** troppo**Google**. Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooGoogle per l'autenticazione.
5. Fare clic su **Salva**.

Si è ora pronto toouse Google per l'autenticazione nell'app.

## <a name="related-content"></a>Contenuti correlati
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portale di Azure]: https://portal.azure.com/

