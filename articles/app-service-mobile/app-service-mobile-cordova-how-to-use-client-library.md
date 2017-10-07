---
title: aaaHow tooUse plug-in Cordova Apache per App mobili di Azure
description: Come tooUse plug-in Cordova Apache per App mobili di Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>La libreria client di Apache Cordova toouse per App mobili di Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Questa guida illustra tooperform scenari comuni di utilizzo più recenti hello [plug-in Cordova Apache per App mobili di Azure]. Nel caso di nuove app per dispositivi mobili tooAzure, completare innanzitutto [avvio rapido di Azure Mobile app] toocreate un back-end, creare una tabella e scaricare un progetto di Apache Cordova preesistente. In questa Guida, focalizzata sul lato client hello plug-in Apache Cordova.

## <a name="supported-platforms"></a>Piattaforme supportate
Questo SDK supporta Apache Cordova v6.0.0 e versioni successive sui dispositivi iOS, Android e Windows.  supporto della piattaforma Hello è indicato di seguito:

* API Android 19-24 (KitKat tramite Nougat).
* iOS versioni 8.0 e successive.
* Windows Phone 8.1
* Piattaforma UWP (Universal Windows Platform).

## <a name="Setup"></a>Installazione e prerequisiti
In questa guida si presuppone che siano stati creati un backend e una tabella. Questa guida si presuppone che la tabella hello è hello stesso schema come tabelle hello in tali esercitazioni. Questa guida si presuppone inoltre che hello plug-in Apache Cordova tooyour codice sia stato aggiunto.  Se non si è connessi, è possibile aggiungere progetto tooyour plug-in Apache Cordova di hello nella riga di comando hello:

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Per altre informazioni sulla creazione della [prima app Apache Cordova], vedere la relativa documentazione.

## <a name="ionic"></a>Configurazione di un'app Ionic v2

tooproperly configurare un progetto Ionic v2, prima di tutto creare un'app di base e aggiungere plug-in Cordova hello:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Aggiungere hello seguenti righe troppo`app.component.ts` oggetto client di hello toocreate:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

È possibile compilare ed eseguire il progetto hello nel browser hello:

```
ionic platform add browser
ionic run browser
```

plug-in Cordova le app mobili di Azure Hello supporta entrambe le app di Ionic v1 e v2.  Solo app hello v2 Ionic richiedere che la dichiarazione aggiuntiva hello `WindowsAzure` oggetto.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Procedura: Autenticare gli utenti
Il servizio app di Azure supporta l'autenticazione e l'autorizzazione degli utenti di app usando diversi provider di identità esterni, a esempio Facebook, Google, account Microsoft e Twitter. È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users. È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione negli script del server. Per ulteriori informazioni, vedere hello [Introduzione all'autenticazione] esercitazione.

Quando si utilizza l'autenticazione in un'app di Apache Cordova, hello seguenti plug-in Cordova devono essere disponibile:

* [cordova-plugin-device]
* [cordova-plugin-inappbrowser]

Sono supportati due flussi di autenticazione, ovvero un flusso server e un flusso client.  flusso server Hello fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia di autenticazione web del provider di hello. Hello flusso client consente una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio single sign-on quanto si basa sulla SDK specifici del dispositivo specifico del provider.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Procedura: Configurare il servizio App per dispositivi mobili per URL di reindirizzamento esterni.
Diversi tipi di applicazioni Apache Cordova usano un toohandle funzionalità loopback che OAuth UI flussi.  Poiché il servizio di autenticazione hello riconosce solo problemi OAuth UI flussi su localhost come tooutilize il servizio per impostazione predefinita.  Alcuni esempi di flussi dell'interfaccia utente di OAuth problematici sono:

* emulatore Ripple Hello.
* Live Reload con Ionic.
* Esecuzione di back-end mobile hello in locale
* Back-end mobile hello è in esecuzione in Azure App Service diverso rispetto all'autenticazione che fornisce uno hello.

Seguire queste istruzioni tooadd configurazione toohello impostazioni locali:

1. Accedi toohello [portale di Azure]
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome dell'App Mobile.
3. Fare clic su **Strumenti**
4. Fare clic su **Esplora inventario risorse** nel menu NOTERÀ hello, quindi fare clic su **passare**.  Si apre una nuova finestra o una nuova scheda.
5. Espandere hello **config**, **authsettings** nodi per il sito di navigazione a sinistra di hello.
6. Fare clic su **Modifica**
7. Cercare l'elemento "allowedExternalRedirectUrls" hello.  Può essere impostata toonull o una matrice di valori.  Modificare hello valore toohello il valore seguente:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Sostituire gli URL di hello con hello URL del servizio.  Ad esempio "http://localhost:3000" (per hello servizio esempio Node. js), o "http://localhost:4400" (per il servizio Ripple hello).  Tuttavia, questi URL sono esempi - situazione attuale, tra cui servizi di hello indicati negli esempi di hello, potrebbero essere diversi.
8. Fare clic su hello **lettura/scrittura** pulsante nell'angolo superiore destro di hello della schermata di hello.
9. Fare clic su hello verde **inserire** pulsante.

impostazioni di Hello vengono salvate in questa fase.  Non chiudere finestra del browser hello fino a quando non vengono completate le impostazioni di hello salvataggio.
Aggiungere anche queste impostazioni di CORS loopback toohello gli URL per il servizio App:

1. Accedi toohello [portale di Azure]
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome dell'App Mobile.
3. pannello impostazioni Hello viene aperta automaticamente.  In caso contrario fare clic su **Tutte le impostazioni**.
4. Fare clic su **CORS** nel menu hello API.
5. Immettere l'URL di hello che si desidera tooadd nell'apposita casella hello e premere INVIO.
6. Immettere gli altri URL in base alle esigenze.
7. Fare clic su **salvare** impostazioni hello toosave.

Impiegato circa 10-15 secondi per effetto di tootake hello nuove impostazioni.

## <a name="register-for-push"></a>Procedura: Registrarsi per le notifiche push
Installare hello [phonegap-plug-in-push] toohandle le notifiche push.  Questo plug-in possono essere aggiunti facilmente mediante la `cordova plugin add` comando nella riga di comando hello o tramite installazione guidata di plug-in Git hello all'interno di Visual Studio.  Il codice seguente nell'app Apache Cordova registra il dispositivo per le notifiche push:

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

Usare le notifiche push di hello SDK hub di notifica toosend dal server hello.  Non inviare mai le notifiche push direttamente dai client. Procedere quindi potrebbe essere tootrigger usato un attacco denial of service contro gli hub di notifica o hello PNS.  Hello PNS Impossibile escludere il traffico in seguito a tali attacchi.

## <a name="more-information"></a>Altre informazioni

È possibile trovare informazioni dettagliate sulle API nella [documentazione sulle API](http://azure.github.io/azure-mobile-apps-js-client/).

<!-- URLs. -->
[portale di Azure]: https://portal.azure.com
[avvio rapido di Azure Mobile app]: app-service-mobile-cordova-get-started.md
[Introduzione all'autenticazione]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[plug-in Cordova Apache per App mobili di Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[prima app Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plug-in-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
