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
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="0fad6-104">Invia push notifiche tooChrome App con gli hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="0fad6-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="0fad6-105">Questo argomento viene illustrato come toouse gli hub di notifica di Azure toosend push notifiche tooa App Chrome, che verrà visualizzato in contesto hello di hello browser Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="0fad6-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="0fad6-106">In questa esercitazione si creerà un'app Chrome che riceve notifiche push tramite [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="0fad6-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="0fad6-107">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="0fad6-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="0fad6-108">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0fad6-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0fad6-109">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="0fad6-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="0fad6-110">esercitazione Hello illustra queste notifiche di push tooenable passaggi di base:</span><span class="sxs-lookup"><span data-stu-id="0fad6-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="0fad6-111">Abilitare Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="0fad6-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="0fad6-112">Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="0fad6-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="0fad6-113">Connettere l'hub di notifica toohello App Chrome</span><span class="sxs-lookup"><span data-stu-id="0fad6-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="0fad6-114">Inviare un tooyour di notifica push App Chrome</span><span class="sxs-lookup"><span data-stu-id="0fad6-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="0fad6-115">Altre funzionalità e capacità</span><span class="sxs-lookup"><span data-stu-id="0fad6-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="0fad6-116">Chrome app le notifiche push non sono di tipo generiche notifiche nel browser, sono toohello specifico modello di estendibilità del browser (vedere [Chrome App Panoramica] per informazioni dettagliate).</span><span class="sxs-lookup"><span data-stu-id="0fad6-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="0fad6-117">Inoltre toohello desktop browser Chrome App eseguite su dispositivi mobili (Android e iOS) tramite Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="0fad6-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="0fad6-118">Vedere [Chrome App Mobile] toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="0fad6-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="0fad6-119">Configurazione GCM e hub di notifica di Azure è identica tooconfiguring per Android, poiché [Google Cloud Messaging per Chrome] è stato deprecato e hello GCM stesso supporta ora i dispositivi Android sia le istanze di Chrome.</span><span class="sxs-lookup"><span data-stu-id="0fad6-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="0fad6-120"><a id="register"></a>Abilitare Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="0fad6-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="0fad6-121">Passare toohello [Google Cloud Console] sito Web, accedere con le credenziali dell'account Google e quindi fare clic su hello **Crea progetto** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0fad6-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="0fad6-122">Fornire un oggetto appropriato **nome progetto**, quindi fare clic su hello **crea** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0fad6-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="0fad6-123">Prendere nota di hello **numero progetto** su hello **progetti** pagina hello progetto appena creato.</span><span class="sxs-lookup"><span data-stu-id="0fad6-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="0fad6-124">Si utilizzerà questo come hello **ID mittente GCM** in hello Chrome App tooregister con GCM.</span><span class="sxs-lookup"><span data-stu-id="0fad6-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="0fad6-125">Nel riquadro di sinistra hello, fare clic su **API & auth**e quindi scorrere verso il basso e fare clic su hello attiva/disattiva tooenable **Google Cloud Messaging per Android**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="0fad6-126">Non è tooenable **Google Cloud Messaging per Chrome**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="0fad6-127">Nel riquadro di sinistra hello, fare clic su **credenziali** > **Crea nuova chiave** > **chiave Server** > **crea**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="0fad6-128">Prendere nota del server hello **chiave API**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="0fad6-129">Questo sarà configurato nell'hub di notifica successiva, tooenable è tooGCM di notifiche push toosend.</span><span class="sxs-lookup"><span data-stu-id="0fad6-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="0fad6-130"><a id="configure-hub"></a>Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="0fad6-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="0fad6-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="0fad6-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="0fad6-132">In hello **impostazioni** pannello seleziona **Notification Services** e quindi **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="0fad6-133">Immettere la chiave API hello e salvare.</span><span class="sxs-lookup"><span data-stu-id="0fad6-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Hub di notifica di Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="0fad6-135"><a id="connect-app"></a>Connettere l'hub di notifica toohello App Chrome</span><span class="sxs-lookup"><span data-stu-id="0fad6-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="0fad6-136">Hub di notifica è ora configurato toowork con GCM, e si dispone di hello tooregister stringhe di connessione tooboth l'app di ricevere e inviare notifiche push.</span><span class="sxs-lookup"><span data-stu-id="0fad6-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="0fad6-137">LK</span><span class="sxs-lookup"><span data-stu-id="0fad6-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="0fad6-138">Creare una nuova app Chrome</span><span class="sxs-lookup"><span data-stu-id="0fad6-138">Create a new Chrome App</span></span>
<span data-ttu-id="0fad6-139">esempio Hello seguente è basato sull'hello [esempio GCM di Chrome App] e utilizza hello consigliato toocreate modo un'App di Chrome.</span><span class="sxs-lookup"><span data-stu-id="0fad6-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="0fad6-140">Verranno evidenziati hello passaggi correlati in modo specifico tooAzure gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="0fad6-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="0fad6-141">Si consiglia di scaricare origine hello per questa App Chrome da [esempio Hub di notifica App Chrome].</span><span class="sxs-lookup"><span data-stu-id="0fad6-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="0fad6-142">è possibile utilizzare uno qualsiasi di editor la preferenza per la creazione, Hello Chrome App viene creato tramite JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0fad6-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="0fad6-143">L'app Chrome avrà un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="0fad6-143">Below is what this Chrome App will look like.</span></span>

![App Google Chrome][15]

1. <span data-ttu-id="0fad6-145">Creare una cartella e denominarla `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="0fad6-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="0fad6-146">Naturalmente, nome hello è arbitrario, se è il nome qualcosa di diverso, assicurarsi che sostituire il percorso di hello in segmenti di codice hello necessario.</span><span class="sxs-lookup"><span data-stu-id="0fad6-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="0fad6-147">Scaricare hello [crittografia js libreria] nella cartella hello creato nel passaggio secondo hello.</span><span class="sxs-lookup"><span data-stu-id="0fad6-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="0fad6-148">Questa cartella della libreria contiene due sottocartelle: `components` e `rollups`.</span><span class="sxs-lookup"><span data-stu-id="0fad6-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="0fad6-149">Creare un file `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="0fad6-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="0fad6-150">Tutte le app di Chrome sono supportate da un file manifesto che contiene i metadati di app hello e, più importante, tutte le autorizzazioni vengono concesse app toohello quando installa utente hello.</span><span class="sxs-lookup"><span data-stu-id="0fad6-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
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
   
    <span data-ttu-id="0fad6-151">Hello preavviso `permissions` elemento che specifica che questa App Chrome sarà in grado di tooreceive le notifiche push da GCM.</span><span class="sxs-lookup"><span data-stu-id="0fad6-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="0fad6-152">È necessario specificare anche hello URI di hub di notifica di Azure dove hello App Chrome renderà un tooregister chiamata REST.</span><span class="sxs-lookup"><span data-stu-id="0fad6-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="0fad6-153">L'app di esempio Usa anche un file di icona, `gcm_128.png`, sono disponibili nell'origine hello che viene riutilizzata da esempio GCM di hello originale.</span><span class="sxs-lookup"><span data-stu-id="0fad6-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="0fad6-154">È possibile sostituirlo per qualsiasi immagine che si adatta a hello [criteri icona](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="0fad6-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="0fad6-155">Creare un file denominato `background.js` con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="0fad6-155">Create a file called `background.js` with hello following code:</span></span>
   
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
   
    <span data-ttu-id="0fad6-156">Si tratta di file hello che viene visualizzata una finestra dell'App Chrome hello HTML (**register.html**) e definisce anche il gestore di hello **messageReceived** notifica push di toohandle hello in arrivo.</span><span class="sxs-lookup"><span data-stu-id="0fad6-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="0fad6-157">Creare un file denominato `register.html` -definisce hello dell'interfaccia utente di hello App Chrome.</span><span class="sxs-lookup"><span data-stu-id="0fad6-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0fad6-158">Questo esempio usa **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="0fad6-159">Se hai scaricato un'altra versione della libreria di hello, assicurarsi che si sostitutiva correttamente versione hello in hello `src` percorso.</span><span class="sxs-lookup"><span data-stu-id="0fad6-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
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
6. <span data-ttu-id="0fad6-160">Creare un file denominato `register.js` con codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0fad6-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="0fad6-161">Specifica di questo file script hello dietro `register.html`.</span><span class="sxs-lookup"><span data-stu-id="0fad6-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="0fad6-162">App Chrome non consentono l'esecuzione inline, in modo che sia toocreate uno script di backup separato per l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="0fad6-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
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
   
    <span data-ttu-id="0fad6-163">Hello sopra script ha hello seguenti parametri chiavi:</span><span class="sxs-lookup"><span data-stu-id="0fad6-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="0fad6-164">**Window. OnLoad** definisce eventi click hello dei pulsanti hello due su hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="0fad6-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="0fad6-165">Uno registra con GCM, e altri hello utilizza ID registrazione hello restituito dopo la registrazione con GCM tooregister con gli hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fad6-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="0fad6-166">**Registro aggiornamento** funzione hello che consente di elaborare toohandle funzionalità di registrazione semplice.</span><span class="sxs-lookup"><span data-stu-id="0fad6-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="0fad6-167">**registerWithGCM** hello primo clic sul pulsante gestore, rendendo hello `chrome.gcm.register` chiamata tooGCM tooregister hello Chrome App istanza corrente.</span><span class="sxs-lookup"><span data-stu-id="0fad6-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="0fad6-168">**registerCallback** è hello funzione di callback che viene chiamato quando viene restituito hello chiamata di registrazione GCM.</span><span class="sxs-lookup"><span data-stu-id="0fad6-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="0fad6-169">**registerWithNH** è hello secondo gestore clic del pulsante, che registra con gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="0fad6-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="0fad6-170">Ottiene `hubName` e `connectionString` (l'utente che ha hello è specificato) e presenta hello chiamata all'API REST registrazione hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="0fad6-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="0fad6-171">**splitConnectionString** e **generateSaSToken** helper che rappresentano l'implementazione JavaScript hello di un processo di creazione del token di firma di accesso condiviso, che deve essere usato in tutte le chiamate API REST.</span><span class="sxs-lookup"><span data-stu-id="0fad6-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="0fad6-172">Per altre informazioni, vedere [Concetti comuni](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fad6-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="0fad6-173">**sendNHRegistrationRequest** è chiamata di funzione hello che rende un HTTP REST tooAzure gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="0fad6-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="0fad6-174">**registrationPayload** definisce payload XML di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="0fad6-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="0fad6-175">Per altre informazioni, vedere [Creare una registrazione dell'API REST per l'Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="0fad6-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="0fad6-176">ID registrazione hello in esso viene aggiornato con ciò che è stato ricevuto da GCM.</span><span class="sxs-lookup"><span data-stu-id="0fad6-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="0fad6-177">**client** è un'istanza di **XMLHttpRequest** che viene usata una richiesta HTTP POST toomake hello.</span><span class="sxs-lookup"><span data-stu-id="0fad6-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="0fad6-178">Si noti che è aggiornare hello `Authorization` intestazione con `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="0fad6-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="0fad6-179">Il corretto completamento di questa chiamata registra questa istanza dell'app Chrome in Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fad6-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="0fad6-180">Hello generale struttura di cartelle per questo progetto deve essere analogo al seguente: ![Google Chrome App - struttura di cartelle][21]</span><span class="sxs-lookup"><span data-stu-id="0fad6-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="0fad6-181">Configurare e testare l'app Chrome</span><span class="sxs-lookup"><span data-stu-id="0fad6-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="0fad6-182">Aprire il browser Chrome.</span><span class="sxs-lookup"><span data-stu-id="0fad6-182">Open your Chrome browser.</span></span> <span data-ttu-id="0fad6-183">Aprire le **estensioni Chrome** e abilitare la **Modalità sviluppatore**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="0fad6-184">Fare clic su **caricare l'estensione decompressi** e passare toohello cartella in cui è stato creato il file hello.</span><span class="sxs-lookup"><span data-stu-id="0fad6-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="0fad6-185">È inoltre possibile utilizzare hello **Chrome app & strumento per sviluppatori di estensioni**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="0fad6-186">Questo strumento è un'App di Chrome in sé (installato da hello archivio Web Chrome) e fornisce funzionalità di debug avanzate per lo sviluppo delle App Chrome.</span><span class="sxs-lookup"><span data-stu-id="0fad6-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="0fad6-187">Se hello Chrome App viene creata senza errori, quindi verrà visualizzato l'App Chrome visualizzati.</span><span class="sxs-lookup"><span data-stu-id="0fad6-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="0fad6-188">Immettere hello **numero progetto** che è stato creato in precedenza da hello **Google Cloud Console** come ID mittente hello, fare clic su **registrare con GCM**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="0fad6-189">È necessario visualizzare il messaggio hello **registrazione con GCM ha avuto esito positivo.**</span><span class="sxs-lookup"><span data-stu-id="0fad6-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="0fad6-190">Immettere il **nome Hub di notifica** hello e **DefaultListenSharedAccessSignature** ottenuto dal portale di hello in precedenza e fare clic su **registrare con l'Hub di notifica di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="0fad6-191">È necessario visualizzare il messaggio hello **registrazione Hub di notifica completata.**</span><span class="sxs-lookup"><span data-stu-id="0fad6-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="0fad6-192">e i dettagli di hello della risposta di registrazione hello, che contiene la registrazione di hub di notifica di Azure hello all'ID.</span><span class="sxs-lookup"><span data-stu-id="0fad6-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="0fad6-193"><a name="send"></a>Inviare un tooyour notifica App Chrome</span><span class="sxs-lookup"><span data-stu-id="0fad6-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="0fad6-194">A scopo di test, verranno inviate notifiche push a Chrome usando un'applicazione console .NET.</span><span class="sxs-lookup"><span data-stu-id="0fad6-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="0fad6-195">È possibile inviare notifiche push con Hub di notifica da qualsiasi back-end tramite l'<a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaccia REST</a> pubblica.</span><span class="sxs-lookup"><span data-stu-id="0fad6-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="0fad6-196">Consultare il [portale di documentazione](https://azure.microsoft.com/documentation/services/notification-hubs/) per altri esempi multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="0fad6-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="0fad6-197">In Visual Studio, hello **File** dal menu **New** e quindi **progetto**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="0fad6-198">In **Visual C#** fare clic su **Windows** e **Applicazione console**, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="0fad6-199">Verrà creato un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="0fad6-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="0fad6-200">Da hello **strumenti** menu, fare clic su **Gestione pacchetti libreria** e quindi **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="0fad6-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="0fad6-201">Consente di visualizzare hello Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="0fad6-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="0fad6-202">Nella finestra della console hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0fad6-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="0fad6-203">Aprire `Program.cs` e aggiungere il seguente hello `using` istruzione:</span><span class="sxs-lookup"><span data-stu-id="0fad6-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="0fad6-204">In hello `Program` classe, aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="0fad6-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="0fad6-205">Assicurarsi di utilizzare la stringa di connessione hello con **completo** non accedere **ascolto** accesso.</span><span class="sxs-lookup"><span data-stu-id="0fad6-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="0fad6-206">Hello **ascolto** stringa di connessione di accesso non concede autorizzazioni toosend le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="0fad6-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="0fad6-207">Aggiungere il seguente hello chiamate in hello `Main` metodo:</span><span class="sxs-lookup"><span data-stu-id="0fad6-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="0fad6-208">Verificare che Chrome sia in esecuzione ed eseguire un'applicazione console hello.</span><span class="sxs-lookup"><span data-stu-id="0fad6-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="0fad6-209">Si dovrebbe visualizzare hello segue notifica popup sul desktop.</span><span class="sxs-lookup"><span data-stu-id="0fad6-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="0fad6-210">È inoltre possibile visualizzare tutte le notifiche utilizzando finestra notifiche Chrome hello hello sulla barra delle applicazioni (Windows) quando è in esecuzione Chrome.</span><span class="sxs-lookup"><span data-stu-id="0fad6-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="0fad6-211">Non è necessario toohave hello Chrome App in esecuzione o Apri nel browser hello (anche se i browser Chrome hello stesso deve essere in esecuzione).</span><span class="sxs-lookup"><span data-stu-id="0fad6-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="0fad6-212">È inoltre possibile ottenere una visualizzazione consolidata di tutte le notifiche nella finestra di notifiche di Chrome hello.</span><span class="sxs-lookup"><span data-stu-id="0fad6-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="0fad6-213"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0fad6-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="0fad6-214">Per altre informazioni sugli hub di notifica, vedere [Panoramica dell'Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="0fad6-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="0fad6-215">tootarget utenti specifici, vedere toohello [Azure notifica hub di notifica utenti] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0fad6-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="0fad6-216">Se si desidera che gli utenti dai gruppi di interesse toosegment, è possibile seguire hello [gli hub di notifica di Azure le ultime notizie] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0fad6-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

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
