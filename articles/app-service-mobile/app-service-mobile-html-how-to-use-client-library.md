---
title: aaaHow tooUse hello SDK JavaScript per App mobili di Azure
description: Come v tooUse per App mobili di Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Come tooUse hello libreria client JavaScript per App mobili di Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Questa guida illustra tooperform scenari comuni di utilizzo più recenti hello [SDK JavaScript per App mobili di Azure]. Nel caso di nuove app per dispositivi mobili tooAzure, completare innanzitutto [avvio rapido di Azure Mobile app] toocreate un back-end e creare una tabella. In questa Guida, l'attenzione sull'utilizzo di back-end mobile hello in applicazioni Web HTML/JavaScript.

## <a name="supported-platforms"></a>Piattaforme supportate
È limitare browser supporto toohello corrente e l'ultimo versioni di hello i browser principali: Google Chrome, Microsoft Edge, Microsoft Internet Explorer e Mozilla Firefox.  Prevediamo hello SDK toofunction con qualsiasi browser moderno relativamente.

pacchetto di Hello viene distribuito come modulo JavaScript universale, in modo che supporta funzioni globali, AMD, CommonJS i formati e.

## <a name="Setup"></a>Installazione e prerequisiti
In questa guida si presuppone che siano stati creati un backend e una tabella. Questa guida si presuppone che la tabella hello è hello stesso schema come tabelle hello in tali esercitazioni.

L'installazione di hello Azure Mobile App JavaScript SDK possono essere eseguita tramite hello `npm` comando:

```
npm install azure-mobile-apps-client --save
```

libreria di Hello può essere utilizzata anche come un modulo ES2015, all'interno di ambienti CommonJS come Browserify e Webpack e come una libreria AMD.  ad esempio:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

È anche possibile utilizzare una versione preesistente di hello SDK scaricando direttamente dal nostro CDN:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Procedura: Autenticare gli utenti
Il servizio app di Azure supporta l'autenticazione e l'autorizzazione degli utenti di app usando diversi provider di identità esterni, a esempio Facebook, Google, account Microsoft e Twitter. È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users. È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione negli script del server. Per ulteriori informazioni, vedere hello [Introduzione all'autenticazione] esercitazione.

Sono supportati due flussi di autenticazione, ovvero un flusso server e un flusso client.  flusso server Hello fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia di autenticazione web del provider di hello. Hello flusso client consente una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio single sign-on quanto si basa sulla SDK specifici del provider.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Procedura: Configurare il servizio App per dispositivi mobili per URL di reindirizzamento esterni.
Diversi tipi di applicazioni JavaScript di utilizzare un toohandle funzionalità loopback che OAuth UI flussi.  Queste funzionalità includono:

* Esecuzione del servizio in locale
* Utilizzo di ricaricamento in tempo reale con hello Framework Ionic
* Reindirizzamento tooApp servizio per l'autenticazione.

In esecuzione in locale può causare problemi in quanto, per impostazione predefinita, il servizio App è solo l'autenticazione configurato l'accesso tooallow dal back-end App per dispositivi mobili. Utilizzare i seguenti passaggi toochange hello autenticazione tooenable le impostazioni di servizio App in esecuzione in locale server hello hello:

1. Accedi toohello [portale di Azure]
2. Passare back-end di tooyour App per dispositivi mobili.
3. Selezionare **Esplora inventario risorse** in hello **gli strumenti di sviluppo** menu.
4. Fare clic su **passare** Esplora inventario risorse di hello tooopen per il back-end di App per dispositivi mobili in una nuova scheda o finestra.
5. Espandere hello **config** > **authsettings** nodo per l'app.
6. Fare clic su hello **modifica** pulsante tooenable la modifica della risorsa hello.
7. Trovare hello **allowedExternalRedirectUrls** elemento che deve essere null. Aggiungere gli URL in una matrice:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Sostituire gli URL di hello nella matrice hello con hello URL del servizio, che in questo esempio è `http://localhost:3000` per il servizio di esempio hello locale Node.js. È anche possibile usare `http://localhost:4400` per il servizio di Ripple hello o altri URL, a seconda della configurazione dell'app.
8. Nella parte superiore di hello della pagina hello, fare clic su **lettura/scrittura**, quindi fare clic su **inserire** toosave gli aggiornamenti.

È inoltre necessario tooadd hello stesso loopback URL toohello whitelist delle impostazioni CORS:

1. Spostarsi indietro toohello [portale di Azure].
2. Passare back-end di tooyour App per dispositivi mobili.
3. Fare clic su **CORS** in hello **API** menu.
4. Immettere ogni URL in hello vuoto **le origini consentite** casella di testo.  Viene creata una nuova casella di testo.
5. Fare clic su **SALVA**

Dopo l'aggiornamento di back-end hello, sarà in grado di toouse hello nuovi loopback URL nell'app.

<!-- URLs. -->
[avvio rapido di Azure Mobile app]: app-service-mobile-cordova-get-started.md
[Introduzione all'autenticazione]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portale di Azure]: https://portal.azure.com/
[SDK JavaScript per App mobili di Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
