---
title: aaaSend App tooChrome le notifiche di push con hub di notifica di Azure | Documenti Microsoft
description: Informazioni su come toouse gli hub di notifica di Azure toosend push notifiche tooa App Chrome.
services: notification-hubs
keywords: notifiche push per dispositivi mobili,notifiche push,notifica push, notifiche push per chrome
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Invia push notifiche tooChrome App con gli hub di notifica di Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Questo argomento viene illustrato come toouse gli hub di notifica di Azure toosend push notifiche tooa App Chrome, che verrà visualizzato in contesto hello di hello browser Google Chrome. In questa esercitazione si creerà un'app Chrome che riceve notifiche push tramite [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

esercitazione Hello illustra queste notifiche di push tooenable passaggi di base:

* [Abilitare Google Cloud Messaging](#register)
* [Configurare l'hub di notifica](#configure-hub)
* [Connettere l'hub di notifica toohello App Chrome](#connect-app)
* [Inviare un tooyour di notifica push App Chrome](#send)
* [Altre funzionalità e capacità](#next-steps)

> [!NOTE]
> Chrome app le notifiche push non sono di tipo generiche notifiche nel browser, sono toohello specifico modello di estendibilità del browser (vedere [Chrome App Panoramica] per informazioni dettagliate). Inoltre toohello desktop browser Chrome App eseguite su dispositivi mobili (Android e iOS) tramite Apache Cordova. Vedere [Chrome App Mobile] toolearn altre.
> 
> 

Configurazione GCM e hub di notifica di Azure è identica tooconfiguring per Android, poiché [Google Cloud Messaging per Chrome] è stato deprecato e hello GCM stesso supporta ora i dispositivi Android sia le istanze di Chrome.

## <a id="register"></a>Abilitare Google Cloud Messaging
1. Passare toohello [Google Cloud Console] sito Web, accedere con le credenziali dell'account Google e quindi fare clic su hello **Crea progetto** pulsante. Fornire un oggetto appropriato **nome progetto**, quindi fare clic su hello **crea** pulsante.
   
       ![Google Cloud Console - Create Project][1]
2. Prendere nota di hello **numero progetto** su hello **progetti** pagina hello progetto appena creato. Si utilizzerà questo come hello **ID mittente GCM** in hello Chrome App tooregister con GCM.
   
       ![Google Cloud Console - Project Number][2]
3. Nel riquadro di sinistra hello, fare clic su **API & auth**e quindi scorrere verso il basso e fare clic su hello attiva/disattiva tooenable **Google Cloud Messaging per Android**. Non è tooenable **Google Cloud Messaging per Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. Nel riquadro di sinistra hello, fare clic su **credenziali** > **Crea nuova chiave** > **chiave Server** > **crea**.
   
       ![Google Cloud Console - Credentials][4]
5. Prendere nota del server hello **chiave API**. Questo sarà configurato nell'hub di notifica successiva, tooenable è tooGCM di notifiche push toosend.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Configurare l'hub di notifica
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   In hello **impostazioni** pannello seleziona **Notification Services** e quindi **Google (GCM)**. Immettere la chiave API hello e salvare.

&emsp;&emsp;![Hub di notifica di Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Connettere l'hub di notifica toohello App Chrome
Hub di notifica è ora configurato toowork con GCM, e si dispone di hello tooregister stringhe di connessione tooboth l'app di ricevere e inviare notifiche push. LK

### <a name="create-a-new-chrome-app"></a>Creare una nuova app Chrome
esempio Hello seguente è basato sull'hello [esempio GCM di Chrome App] e utilizza hello consigliato toocreate modo un'App di Chrome. Verranno evidenziati hello passaggi correlati in modo specifico tooAzure gli hub di notifica. 

> [!NOTE]
> Si consiglia di scaricare origine hello per questa App Chrome da [esempio Hub di notifica App Chrome].
> 
> 

è possibile utilizzare uno qualsiasi di editor la preferenza per la creazione, Hello Chrome App viene creato tramite JavaScript. L'app Chrome avrà un aspetto simile al seguente.

![App Google Chrome][15]

1. Creare una cartella e denominarla `ChromePushApp`. Naturalmente, nome hello è arbitrario, se è il nome qualcosa di diverso, assicurarsi che sostituire il percorso di hello in segmenti di codice hello necessario.
2. Scaricare hello [crittografia js libreria] nella cartella hello creato nel passaggio secondo hello. Questa cartella della libreria contiene due sottocartelle: `components` e `rollups`.
3. Creare un file `manifest.json` . Tutte le app di Chrome sono supportate da un file manifesto che contiene i metadati di app hello e, più importante, tutte le autorizzazioni vengono concesse app toohello quando installa utente hello.
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    Hello preavviso `permissions` elemento che specifica che questa App Chrome sarà in grado di tooreceive le notifiche push da GCM. È necessario specificare anche hello URI di hub di notifica di Azure dove hello App Chrome renderà un tooregister chiamata REST.
    L'app di esempio Usa anche un file di icona, `gcm_128.png`, sono disponibili nell'origine hello che viene riutilizzata da esempio GCM di hello originale. È possibile sostituirlo per qualsiasi immagine che si adatta a hello [criteri icona](https://developer.chrome.com/apps/manifest/icons).
4. Creare un file denominato `background.js` con hello seguente codice:
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    Si tratta di file hello che viene visualizzata una finestra dell'App Chrome hello HTML (**register.html**) e definisce anche il gestore di hello **messageReceived** notifica push di toohandle hello in arrivo.
5. Creare un file denominato `register.html` -definisce hello dell'interfaccia utente di hello App Chrome. 
   
   > [!NOTE]
   > Questo esempio usa **CryptoJS v3.1.2**. Se hai scaricato un'altra versione della libreria di hello, assicurarsi che si sostitutiva correttamente versione hello in hello `src` percorso.
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. Creare un file denominato `register.js` con codice hello riportato di seguito. Specifica di questo file script hello dietro `register.html`. App Chrome non consentono l'esecuzione inline, in modo che sia toocreate uno script di backup separato per l'interfaccia utente.
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    Hello sopra script ha hello seguenti parametri chiavi:
   
   * **Window. OnLoad** definisce eventi click hello dei pulsanti hello due su hello dell'interfaccia utente. Uno registra con GCM, e altri hello utilizza ID registrazione hello restituito dopo la registrazione con GCM tooregister con gli hub di notifica di Azure.
   * **Registro aggiornamento** funzione hello che consente di elaborare toohandle funzionalità di registrazione semplice.
   * **registerWithGCM** hello primo clic sul pulsante gestore, rendendo hello `chrome.gcm.register` chiamata tooGCM tooregister hello Chrome App istanza corrente.
   * **registerCallback** è hello funzione di callback che viene chiamato quando viene restituito hello chiamata di registrazione GCM.
   * **registerWithNH** è hello secondo gestore clic del pulsante, che registra con gli hub di notifica. Ottiene `hubName` e `connectionString` (l'utente che ha hello è specificato) e presenta hello chiamata all'API REST registrazione hub di notifica.
   * **splitConnectionString** e **generateSaSToken** helper che rappresentano l'implementazione JavaScript hello di un processo di creazione del token di firma di accesso condiviso, che deve essere usato in tutte le chiamate API REST. Per altre informazioni, vedere [Concetti comuni](http://msdn.microsoft.com/library/dn495627.aspx).
   * **sendNHRegistrationRequest** è chiamata di funzione hello che rende un HTTP REST tooAzure gli hub di notifica.
   * **registrationPayload** definisce payload XML di registrazione hello. Per altre informazioni, vedere [Creare una registrazione dell'API REST per l'Hub di notifica]. ID registrazione hello in esso viene aggiornato con ciò che è stato ricevuto da GCM.
   * **client** è un'istanza di **XMLHttpRequest** che viene usata una richiesta HTTP POST toomake hello. Si noti che è aggiornare hello `Authorization` intestazione con `sasToken`. Il corretto completamento di questa chiamata registra questa istanza dell'app Chrome in Hub di notifica di Azure.

Hello generale struttura di cartelle per questo progetto deve essere analogo al seguente: ![Google Chrome App - struttura di cartelle][21]

### <a name="set-up-and-test-your-chrome-app"></a>Configurare e testare l'app Chrome
1. Aprire il browser Chrome. Aprire le **estensioni Chrome** e abilitare la **Modalità sviluppatore**.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Fare clic su **caricare l'estensione decompressi** e passare toohello cartella in cui è stato creato il file hello. È inoltre possibile utilizzare hello **Chrome app & strumento per sviluppatori di estensioni**. Questo strumento è un'App di Chrome in sé (installato da hello archivio Web Chrome) e fornisce funzionalità di debug avanzate per lo sviluppo delle App Chrome.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Se hello Chrome App viene creata senza errori, quindi verrà visualizzato l'App Chrome visualizzati.
   
       ![Google Chrome - Chrome App Display][18]
4. Immettere hello **numero progetto** che è stato creato in precedenza da hello **Google Cloud Console** come ID mittente hello, fare clic su **registrare con GCM**. È necessario visualizzare il messaggio hello **registrazione con GCM ha avuto esito positivo.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Immettere il **nome Hub di notifica** hello e **DefaultListenSharedAccessSignature** ottenuto dal portale di hello in precedenza e fare clic su **registrare con l'Hub di notifica di Azure**. È necessario visualizzare il messaggio hello **registrazione Hub di notifica completata.** e i dettagli di hello della risposta di registrazione hello, che contiene la registrazione di hub di notifica di Azure hello all'ID.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Inviare un tooyour notifica App Chrome
A scopo di test, verranno inviate notifiche push a Chrome usando un'applicazione console .NET. 

> [!NOTE]
> È possibile inviare notifiche push con Hub di notifica da qualsiasi back-end tramite l'<a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaccia REST</a> pubblica. Consultare il [portale di documentazione](https://azure.microsoft.com/documentation/services/notification-hubs/) per altri esempi multipiattaforma.
> 
> 

1. In Visual Studio, hello **File** dal menu **New** e quindi **progetto**. In **Visual C#** fare clic su **Windows** e **Applicazione console**, quindi selezionare **OK**.  Verrà creato un nuovo progetto di applicazione console.
2. Da hello **strumenti** menu, fare clic su **Gestione pacchetti libreria** e quindi **Package Manager Console**. Consente di visualizzare hello Console di gestione pacchetti.
3. Nella finestra della console hello, eseguire hello comando seguente:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Aprire `Program.cs` e aggiungere il seguente hello `using` istruzione:
   
        using Microsoft.Azure.NotificationHubs;
5. In hello `Program` classe, aggiungere al metodo hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Assicurarsi di utilizzare la stringa di connessione hello con **completo** non accedere **ascolto** accesso. Hello **ascolto** stringa di connessione di accesso non concede autorizzazioni toosend le notifiche push.
   > 
   > 
6. Aggiungere il seguente hello chiamate in hello `Main` metodo:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Verificare che Chrome sia in esecuzione ed eseguire un'applicazione console hello.
8. Si dovrebbe visualizzare hello segue notifica popup sul desktop.
   
       ![Google Chrome - Notification][13]
9. È inoltre possibile visualizzare tutte le notifiche utilizzando finestra notifiche Chrome hello hello sulla barra delle applicazioni (Windows) quando è in esecuzione Chrome.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> Non è necessario toohave hello Chrome App in esecuzione o Apri nel browser hello (anche se i browser Chrome hello stesso deve essere in esecuzione). È inoltre possibile ottenere una visualizzazione consolidata di tutte le notifiche nella finestra di notifiche di Chrome hello.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sugli hub di notifica, vedere [Panoramica dell'Hub di notifica].

tootarget utenti specifici, vedere toohello [Azure notifica hub di notifica utenti] esercitazione. 

Se si desidera che gli utenti dai gruppi di interesse toosegment, è possibile seguire hello [gli hub di notifica di Azure le ultime notizie] esercitazione.

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[esempio Hub di notifica App Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Panoramica dell'Hub di notifica]: notification-hubs-push-notification-overview.md
[Chrome App Panoramica]: https://developer.chrome.com/apps/about_apps
[esempio GCM di Chrome App]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Chrome App Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Creare una registrazione dell'API REST per l'Hub di notifica]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crittografia js libreria]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging per Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure notifica hub di notifica utenti]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[gli hub di notifica di Azure le ultime notizie]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
