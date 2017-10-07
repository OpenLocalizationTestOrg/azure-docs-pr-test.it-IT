---
title: aaaGet avviato con Azure Mobile Engagement per Cordova/Phonegap
description: Informazioni su come toouse Azure Mobile Engagement con Analitica e le notifiche Push per le app Cordova/Phonegap.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Introduzione ad Azure Mobile Engagement per Cordova/Phonegap
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

In questo argomento illustra come toouse Azure Mobile Engagement toounderstand app informazioni sull'utilizzo e trasmissione push notifiche toosegmented utenti per un'applicazione per dispositivi mobili sviluppati con Cordova.

In questa esercitazione verrà creata un'app Cordova vuota mediante Mac e quindi verrà eseguita l'integrazione di Mobile Engagement SDK. L'app raccoglierà dati analitici di base e riceverà notifiche push tramite Apple Push Notification System (APNS) per iOS e Google Cloud Messaging (GCM) per Android. Si distribuirà questo tooan dispositivo iOS o Android per il test. 

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).
> 
> 

Questa esercitazione richiede il seguente hello:

* XCode, che è possibile installare Mac App Store (per la distribuzione tooiOS)
* [Android SDK & emulatore](http://developer.android.com/sdk/installing/index.html) (per la distribuzione tooAndroid)
* Certificato per notifiche push (con estensione p12) che è possibile ottenere nell'Apple Dev Center per APNS
* Numero di progetto GCM, che è possibile ottenere da Google Developer Console per GCM
* [Plug-in di Cordova per Mobile Engagement](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> È possibile trovare il codice sorgente hello e hello file Leggimi per plug-in Cordova hello in [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Configurare Mobile Engagement per l'app Cordova
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app
Questa esercitazione viene illustrato un "integrazione di base" hello minimo imposta dati toocollect necessarie e invia una notifica push. 

Verrà creata un'applicazione di base con l'integrazione di hello toodemonstrate Cordova:

### <a name="create-a-new-cordova-project"></a>Creare un nuovo progetto Cordova
1. Avviare *Terminal* finestra il hello macchina e tipo Mac successivo che verrà creato un nuovo progetto Cordova dal modello predefinito hello. Assicurarsi che la pubblicazione di hello profilo è alla fine toodeploy di usare l'app iOS Usa 'com.mycompany.myapp' come hello ID App. 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Eseguire hello seguente tooconfigure il progetto per **iOS** ed eseguirlo nel simulatore iOS hello:
   
        $ cordova platform add ios 
        $ cordova run ios
3. Eseguire hello seguente tooconfigure il progetto per **Android** ed eseguirlo nell'emulatore Android hello. Assicurarsi che le impostazioni dell'emulatore di Android SDK dispongano la destinazione come Google APIs (Google Inc.) con hello CPU / ABI come Google APIs ARM.  
   
        $ cordova platform add android
        $ cordova run android
4. Aggiungi plug-in Cordova Console hello. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>La connessione back-end Engagement tooMobile app
1. Installazione di plug-in Cordova di Azure Mobile Engagement hello fornendo hello i valori delle variabili tooconfigure hello plug-in:
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Icona di raggiungere Android* : deve essere hello nome della risorsa hello senza qualsiasi estensione né drawable prefisso (ad esempio: mynotificationicon), e i file di icona hello devono essere copiati nel progetto android (piattaforme/android/res/drawable)

*Icona raggiungere iOS* : deve essere hello nome della risorsa hello con l'estensione (ad esempio: mynotificationicon.png), e file di icona hello devono essere aggiunti al progetto iOS con XCode (tramite hello Aggiungi file Menu)

## <a id="monitor"></a>Abilitazione del monitoraggio in tempo reale
1. Nel progetto Cordova hello - modifica **www/js/index.js** chiamata hello tooadd tooMobile Engagement toodeclare una nuova attività una volta hello *deviceReady* viene ricevuto l'evento.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Eseguire un'applicazione hello:
   
   * **Per iOS**
     
       In `Terminal` finestra Avvia l'app in una nuova istanza di simulatore eseguendo hello seguente:
     
           cordova run ios
   * **Per Android**
     
       In `Terminal` finestra Avvia l'app in una nuova istanza dell'emulatore eseguendo hello seguente:
     
           cordova run android
3. È possibile visualizzare i seguenti hello in hello registri della console:
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>Connettere l'app con monitoraggio in tempo reale
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Abilitazione delle notifiche push e della messaggistica in-app
Engagement mobile permette di toointeract con gli utenti utilizzando le notifiche Push e nel contesto di hello delle campagne di messaggistica in-app. Questo modulo viene chiamato REACH nel portale Mobile Engagement hello.
Hello nelle sezioni seguenti installerà il tooreceive app li.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Configurare le credenziali push per Mobile Engagement
tooallow Mobile Engagement toosend le notifiche Push per conto dell'utente, è necessario accedere a tooyour del certificato per Apple iOS o la chiave API Server GCM toogrant. 

1. Passare portale Mobile Engagement tooyour. Verificare le app hello è in uso per questo progetto e quindi fare clic su hello **attirare** pulsante nella parte inferiore di hello:
   
    ![][1]
2. Viene visualizzata nella pagina Impostazioni hello nel portale del progetto. Da scegliere è hello **Push nativo** sezione:
   
    ![][2]
3. Configurare il certificato iOS o la chiave dell'API del server GCM
   
    **[iOS]**
   
    a. Selezionare il certificato con estensione p12, caricarlo e digitare la password:
   
    ![][3]
   
    **[Android]**
   
    a. Fare clic sull'icona di modifica hello in primo piano **chiave API** nella sezione Impostazioni GCM hello e nella finestra popup di hello che viene visualizzato, incollare hello chiave Server GCM, quindi fare clic su **OK**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Abilitare le notifiche push in app di Cordova hello
Modifica **www/js/index.js** tooadd hello chiamata tooMobile Engagement toorequest notifiche push e dichiarare un gestore:

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Eseguire app hello
**[iOS]**

1. Verrà utilizzare toobuild XCode e distribuire app hello in notifiche di push tootest dispositivo hello poiché iOS consente solo dispositivo effettivo tooan di notifiche push. Passare toohello percorso in cui è stato creato il progetto Cordova e passare troppo**...\platforms\ios** percorso. Aprire il file con estensione xcodeproj nativo hello in XCode. 
2. Compilare e distribuire i dispositivi iOS hello Cordova app toohello utilizzando account hello è hello contenente il certificato di hello che appena caricato portale Mobile Engagement toohello e hello App Id che trova la corrispondenza hello uno fornita durante la creazione di profilo di provisioning app Cordova Hello. È possibile estrarre hello *identificatore Bundle* nel **risorse\*-Info. plist** file in XCode toomatch il backup. 
3. Si noterà popup iOS standard hello sul dispositivo che informa che app hello richiede notifiche toosend di autorizzazione. Concedere l'autorizzazione di hello. 

**[Android]**

È possibile utilizzare l'applicazione Android hello hello emulatore toorun semplicemente come le notifiche GCM sono supportate nell'emulatore Android hello. 

    cordova run android

## <a id="send"></a>Invia un'app tooyour notifica
Verrà ora creata una semplice campagna di notifica Push che invierà un'app tooyour push in esecuzione sul dispositivo hello:

1. Passare toohello **raggiungere** scheda nel portale Mobile Engagement
2. Fare clic su **nuovo annuncio** toocreate la campagna push
   
    ![][6]
3. Fornire input toocreate campagna **[Android]**
   
   * Fornire un **Nome** per la campagna. 
   * Seleziona hello **tipo di recapito** come *notifica di sistema* *semplice*
   * Seleziona hello **l'ora di recapito** come *"Any ora"*
   * Fornire un **titolo** per la notifica che sarà hello nella prima riga push hello.
   * Fornire un **messaggio** per la notifica che verrà utilizzata come corpo del messaggio hello. 
     
     ![][11]
4. Fornire input toocreate campagna **[iOS]**
   
   * Fornire un **Nome** per la campagna. 
   * Seleziona hello **l'ora di recapito** come *"da solo app"*
   * Fornire un **titolo** per la notifica che sarà hello nella prima riga push hello.
   * Fornire un **messaggio** per la notifica che verrà utilizzata come corpo del messaggio hello. 
     
     ![][12]
5. Scorrere verso il basso e in hello sezione di contenuto selezionare **sola notifica**
   
    ![][8]
6. [Facoltativo] È anche possibile specificare un URL di azione. Assicurarsi che utilizza uno schema URL fornito durante la configurazione del plug-in di hello **AZME\_REINDIRIZZARE\_URL** variabile, ad esempio *myapp://test*.  
7. Possibili campagna più elementare di impostazione hello completato. Ora nuovamente a scorrere verso il basso e fare clic su hello **crea** pulsante toosave la campagna.
8. Fare infine clic su **Attiva** per la campagna.
   
    ![][10]
9. Una notifica push dovrebbe essere visualizzata nel dispositivo o nell'emulatore come parte di questa campagna. 

## <a id="next-steps"></a>Passaggi successivi
[Panoramica di tutti i metodi disponibili con Cordova Mobile Engagement SDK](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

