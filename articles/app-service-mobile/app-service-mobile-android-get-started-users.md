---
title: autenticazione aaaAdd in Android con App per dispositivi mobili | Documenti Microsoft
description: "Informazioni su come toouse hello funzionalità delle App per dispositivi mobili degli utenti di tooauthenticate di servizio App di Azure di app Android tramite un'ampia varietà di provider di identità, tra cui Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>Aggiungere app per Android tooyour autenticazione
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Riepilogo
In questa esercitazione, aggiungere progetto di avvio rapido di autenticazione toohello todolist in Android tramite un provider di identità supportati. In questa esercitazione si basa sull'hello [Introduzione a Mobile app] esercitazione, è necessario completare prima.

## <a name="register"></a>Registrare l'app per l'autenticazione e configurare Servizio app di Azure
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Aggiungere gli URL di reindirizzamento esterno consentito toohello app

L'autenticazione sicura richiede la definizione di un nuovo schema URL per l'app. App di hello authentication sistema tooredirect tooyour indietro in questo modo una volta completato il processo di autenticazione hello. In questa esercitazione, si usa lo schema dell'URL hello _appname_ in tutto. È tuttavia possibile usare QUALSIASI schema URL. Deve essere univoco tooyour applicazioni per dispositivi mobili. reindirizzamento di hello tooenable sul lato server hello:

1. In hello [portale], selezionare il servizio App.

2. Fare clic su hello **autenticazione / autorizzazione** opzione di menu.

3. In hello **consentito URL di reindirizzamento esterno**, immettere `appname://easyauth.callback`.  Hello _appname_ in questa stringa è hello lo schema dell'URL per l'applicazione per dispositivi mobili.  Deve seguire le normale specifica URL per un protocollo, ovvero usare solo lettere e numeri e iniziare con una lettera.  È opportuno prendere nota della stringa hello scelte in quanto è necessario tooadjust il codice dell'applicazione per dispositivi mobili con lo schema dell'URL in diverse posizioni hello.

4. Fare clic su **OK**.

5. Fare clic su **Salva**.

## <a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* In Android Studio, aprire il progetto di hello è stata completata con l'esercitazione hello [Introduzione a Mobile app]. Da hello **eseguire** menu, fare clic su **eseguire app**e verificare che, dopo l'avvio dell'applicazione hello, viene generata un'eccezione non gestita con un codice di stato di 401 (non autorizzato).

     Questa eccezione si verifica perché i tentativi di applicazione hello tooaccess hello nuovamente terminano come un utente non autenticato, ma hello *TodoItem* tabella richiede ora l'autenticazione.

Aggiornare quindi gli utenti di hello app tooauthenticate prima di richiedere risorse di hello che terminare nuovamente App per dispositivi mobili. 

## <a name="add-authentication-toohello-app"></a>Aggiungere app toohello authentication
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Token di autenticazione nella cache sul client hello
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Passaggi successivi
Ora che è stata completata questa esercitazione l'autenticazione di base, è consigliabile continuare su tooone di hello seguenti esercitazioni:

* [Aggiungere app per Android tooyour le notifiche push](app-service-mobile-android-get-started-push.md).
  Informazioni su come eseguire il backup delle applicazioni mobili tooconfigure terminare notifiche di push toosend hub notifica di Azure toouse.
* [Attivare la sincronizzazione offline per l'app Android](app-service-mobile-android-get-started-offline-data.md).
  Informazioni su come offline tooadd supportano tooyour app con un back-end App per dispositivi mobili. Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche quando non è disponibile una connessione di rete.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[Introduzione a Mobile app]: app-service-mobile-android-get-started.md
