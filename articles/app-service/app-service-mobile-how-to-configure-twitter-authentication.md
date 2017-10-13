---
title: Come configurare l'autenticazione Twitter per un'applicazione dei servizi app
description: Informazioni su come configurare l'autenticazione Twitter per un'applicazione dei servizi app.
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
ms.openlocfilehash: afde020b7817dc58ecea24eb4a09cf93d0986eb2
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a>Come configurare un'applicazione del servizio app per usare l'account di accesso di Twitter
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Questo argomento descrive come configurare il servizio app di Azure per usare Twitter come provider di autenticazione.

Per completare la procedura descritta in questo argomento è necessario avere un account Twitter con un indirizzo di posta elettronica e un numero di telefono verificati. Per creare un nuovo account Twitter, visitare il sito Web all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"></a>Registrare l'applicazione con Twitter
1. Accedere al [portale di Azure], e passare all'applicazione. Copiare l' **URL**. Verrà usato per configurare l'app Twitter.
2. Passare al sito Web [Twitter Developers] , accedere con le credenziali dell'account Twitter e quindi fare clic su **Create New App**(Crea nuova app).
3. Digitare i valori per **Name** (Nome) e **Description** (Descrizione) per la nuova app. Incollare l'**URL** dell'applicazione per il valore **Website** (Sito Web). Nella casella **Callback URL** (URL callback) incollare quindi il valore di **URL callback** copiato prima. Si tratta del gateway dell'app per dispositivi mobili con il percorso */.auth/login/twitter/callback* come suffisso. Ad esempio `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Assicurarsi che sia in uso lo schema HTTPS.
4. Nella parte inferiore della pagina, leggere e accettare le condizioni di utilizzo. Fare clic su **Create your Twitter application**. L'app verrà registrata e verranno visualizzati i dettagli dell'applicazione.
5. Fare clic sulla scheda **Settings** (Impostazioni), selezionare **Allow this application to be used to sign in with Twitter** (Consenti l'uso dell'applicazione per l'accesso con Twitter) e quindi fare clic su **Update Settings** (Aggiorna impostazioni).
6. Selezionare la scheda **Keys and Access Tokens** . Prendere nota dei valori di **Consumer Key (API Key)** (Chiave utente (chiave API)) e **Consumer secret (API Secret)** (Segreto utente (chiave privata API)).
   
   > [!NOTE]
   > Il segreto consumer è un'importante credenziale di sicurezza. Non condividere questo valore con altri né distribuirlo con l'app.
   > 
   > 

## <a name="secrets"></a>Aggiungere informazioni di Twitter all'applicazione
1. Nel [portale di Azure], passare all'applicazione. Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.
2. Se la funzionalità di autenticazione/autorizzazione non è abilitata, impostare l'opzione in modo da **abilitarla**.
3. Fare clic su **Twitter**. Incollare i valori relativi all'ID dell'app e al segreto dell'app ottenuti in precedenza. Fare quindi clic su **OK**.
   
   ![][1]
   
   Per impostazione predefinita, il servizio app fornisce l'autenticazione ma non limita l'accesso alle API e al contenuto del sito solo agli utenti autorizzati. È necessario autorizzare gli utenti nel codice dell'app.
4. (Facoltativo) Per consentire l'accesso al sito solo agli utenti autenticati da Twitter, impostare il parametro **Azione da eseguire quando la richiesta non è autenticata** su **Twitter**. Per poter utilizzare questa funzione, tuttavia, è necessario che tutte le richieste vengano autenticate e che le richieste non autenticate vengano reindirizzate a Twitter per l'autenticazione.
5. Fare clic su **Save**.

È ora possibile usare un account Twitter per l'autenticazione nell'app.

## <a name="related-content"></a>Contenuti correlati
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portale di Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
