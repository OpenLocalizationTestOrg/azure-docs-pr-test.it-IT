---
title: autenticazione aaaAdd in Apache Cordova con App per dispositivi mobili | Documenti Microsoft
description: "Informazioni su come toouse App per dispositivi mobili degli utenti di Azure App Service tooauthenticate dell'app Apache Cordova tramite un'ampia varietà di provider di identità, tra cui Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Aggiungere app Apache Cordova tooyour di autenticazione
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Riepilogo
In questa esercitazione è aggiungere progetto di avvio rapido di autenticazione toohello todolist in Apache Cordova tramite un provider di identità supportati. In questa esercitazione si basa sull'hello [Introduzione a Mobile app] esercitazione, è necessario completare prima.

## <a name="register"></a>Registrare l'app per l'autenticazione e configurare hello servizio App
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Guardare un video che illustra una procedura simile](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Limitare le autorizzazioni tooauthenticated utenti
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

A questo punto, è possibile verificare che tale back-end tooyour l'accesso anonimo è stato disabilitato. In Visual Studio:

* Progetto aperto hello creato dopo avere completato l'esercitazione hello [Introduzione a Mobile app].
* Eseguire l'applicazione in hello **emulatore Android di Google**.
* Verificare che sia visualizzato un errore di connessione imprevisto dopo l'avvio dell'applicazione hello.

Aggiornare quindi gli utenti di hello app tooauthenticate prima di richiedere risorse di back-end di hello App per dispositivi mobili.

## <a name="add-authentication"></a>Aggiungere app toohello authentication
1. Aprire il progetto in **Visual Studio**, quindi aprire hello `www/index.html` file per la modifica.
2. Individuare hello `Content-Security-Policy` metatag nella sezione di intestazione hello.  Aggiungere hello OAuth host toohello elenco di origini consentite.

   | Provider | Nome del provider SDK | Host OAuth |
   |:--- |:--- |:--- |
   | Azure Active Directory | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://accounts.google.com |
   | Microsoft | microsoftaccount | https://login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    Ecco un esempio di Content-Security-Policy implementato per Azure Active Directory:

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Sostituire `https://login.microsoftonline.com` con host OAuth hello hello tabella precedente.  Per ulteriori informazioni sui tag meta di criteri di sicurezza contenuto hello, vedere hello [documentazione di criteri di sicurezza contenuto].

    Alcuni provider di autenticazione non richiedono modifiche a Content-Security-Policy quando viene usato in dispositivi mobili appropriati.  Ad esempio, non sono richieste modifiche a Content-Security-Policy quando si usa l'autenticazione di Google in un dispositivo Android.

3. Aprire hello `www/js/index.js` per la modifica del file, individuare hello `onDeviceReady()` (metodo), e creazione di client hello in codice aggiungere hello seguente codice:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Questo codice sostituisce il codice esistente hello Crea riferimento a tabella hello e aggiorna hello dell'interfaccia utente.

    metodo di Login () Hello avvia l'autenticazione con il provider di hello. Hello Login () è una funzione asincrona che restituisce una promessa di JavaScript.  rest Hello di inizializzazione hello viene inserito in risposta promessa hello in modo che non viene eseguita fino al completamento di metodo di hello Login ().

4. Nel codice hello appena aggiunto, sostituire `SDK_Provider_Name` con nome hello del provider di accesso. Ad esempio, per Azure Active Directory usare `client.login('aad')`.
5. Eseguire il progetto.  Al termine dell'inizializzazione progetto hello, l'applicazione Mostra pagina di accesso OAuth hello per hello provider di autenticazione scelto.

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni, vedere [Autenticazione e autorizzazione] con il servizio app di Azure.
* Continuare l'esercitazione hello aggiungendo [le notifiche Push] tooyour app di Apache Cordova.

Informazioni su come toouse hello SDK.

* [Apache Cordova SDK]
* [ASP.NET Server SDK]
* [Node.js Server SDK]

<!-- URLs. -->
[Introduzione a Mobile app]: app-service-mobile-cordova-get-started.md
[documentazione di criteri di sicurezza contenuto]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[le notifiche Push]: app-service-mobile-cordova-get-started-push.md
[Autenticazione e autorizzazione]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
