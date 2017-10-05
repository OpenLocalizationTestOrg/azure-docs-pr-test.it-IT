---
title: Inviare notifiche push alle app Chrome con Hub di notifica di Azure | Documentazione di Microsoft
description: Informazioni su come usare Hub di notifica di Azure per inviare notifiche push a un'app Chrome.
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
ms.openlocfilehash: 600b1b7e5f3987c9a0acc33b7049f7118442b931
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="4b822-104">Inviare notifiche push alle app Chrome con Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="4b822-104">Send push notifications to Chrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="4b822-105">Questo argomento illustra come usare Hub di notifica per inviare notifiche push a un'app Chrome, che saranno visualizzate nel contesto del browser Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span></span> <span data-ttu-id="4b822-106">In questa esercitazione si creerà un'app Chrome che riceve notifiche push tramite [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="4b822-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="4b822-107">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4b822-107">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="4b822-108">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4b822-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4b822-109">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="4b822-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="4b822-110">Questa esercitazione descrive le operazioni di base per abilitare le notifiche push:</span><span class="sxs-lookup"><span data-stu-id="4b822-110">The tutorial walks you through these basic steps to enable push notifications:</span></span>

* [<span data-ttu-id="4b822-111">Abilitare Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="4b822-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="4b822-112">Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="4b822-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="4b822-113">Connettere l'app Chrome all'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="4b822-113">Connect your Chrome App to the notification hub</span></span>](#connect-app)
* [<span data-ttu-id="4b822-114">Inviare una notifica push all'app Chrome</span><span class="sxs-lookup"><span data-stu-id="4b822-114">Send a push notification to your Chrome App</span></span>](#send)
* [<span data-ttu-id="4b822-115">Altre funzionalità e capacità</span><span class="sxs-lookup"><span data-stu-id="4b822-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="4b822-116">Le notifiche push alle app Chrome non sono notifiche generiche all'interno del browser, ma sono specifiche del modello di estendibilità del browser. Per informazioni dettagliate, vedere l'articolo che fornisce una [panoramica delle app Chrome].</span><span class="sxs-lookup"><span data-stu-id="4b822-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="4b822-117">Oltre che in browser desktop, le app Chrome vengono eseguite su dispositivi mobili (iOS e Android) tramite Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="4b822-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="4b822-118">Per altre informazioni, vedere [App Chrome su dispositivi mobili].</span><span class="sxs-lookup"><span data-stu-id="4b822-118">See [Chrome Apps on Mobile] to learn more.</span></span>
> 
> 

<span data-ttu-id="4b822-119">La configurazione di GCM e di Hub di notifica di Azure è identica alla configurazione per Android, perché [Google Cloud Messaging per Chrome] è stato ritirato e lo stesso GCM ora supporta sia dispositivi Android che istanze di Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="4b822-120"><a id="register"></a>Abilitare Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="4b822-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="4b822-121">Passare al sito Web [Google Cloud Console] , accedere con le credenziali dell'account Google e fare clic su **Create Project** .</span><span class="sxs-lookup"><span data-stu-id="4b822-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span></span> <span data-ttu-id="4b822-122">Inserire un valore appropriato nel campo **Nome progetto** e fare clic sul pulsante **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4b822-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="4b822-123">Annotare il valore di **Numero progetto** nella pagina **Progetti** per il progetto appena creato.</span><span class="sxs-lookup"><span data-stu-id="4b822-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span></span> <span data-ttu-id="4b822-124">Verrà usato come **GCM Sender ID** nell'app Chrome per la registrazione con GCM.</span><span class="sxs-lookup"><span data-stu-id="4b822-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="4b822-125">Nel riquadro sinistro fare clic su **APIs & auth** (API e autenticazione), quindi scorrere verso il basso e fare clic sull'interruttore per abilitare **Google Cloud Messaging per Android**.</span><span class="sxs-lookup"><span data-stu-id="4b822-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="4b822-126">Non è necessario abilitare **Google Cloud Messaging for Chrome**.</span><span class="sxs-lookup"><span data-stu-id="4b822-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="4b822-127">Nel riquadro a sinistra fare clic su **Credenziali** > **Crea nuova chiave** > **Chiave server** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4b822-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="4b822-128">Prendere nota del valore **API Key**per il server.</span><span class="sxs-lookup"><span data-stu-id="4b822-128">Make a note of the server **API Key**.</span></span> <span data-ttu-id="4b822-129">La chiave verrà successivamente configurata nell'hub di notifica, in modo che possa inviare notifiche push a GCM.</span><span class="sxs-lookup"><span data-stu-id="4b822-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="4b822-130"><a id="configure-hub"></a>Configurare l'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="4b822-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="4b822-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="4b822-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="4b822-132">Nel pannello **Impostazioni** selezionare **Servizi di notifica**, quindi **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="4b822-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="4b822-133">Immettere la chiave API e salvare.</span><span class="sxs-lookup"><span data-stu-id="4b822-133">Enter the API key and save.</span></span>

&emsp;&emsp;![Hub di notifica di Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="4b822-135"><a id="connect-app"></a>Connettere l'app Chrome all'hub di notifica</span><span class="sxs-lookup"><span data-stu-id="4b822-135"><a id="connect-app"></a>Connect your Chrome App to the notification hub</span></span>
<span data-ttu-id="4b822-136">A questo punto,l'hub di notifica è configurato per l'uso con GCM e sono disponibili le stringhe di connessione per registrare l'app per l'invio e la ricezione di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="4b822-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span></span> <span data-ttu-id="4b822-137">LK</span><span class="sxs-lookup"><span data-stu-id="4b822-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="4b822-138">Creare una nuova app Chrome</span><span class="sxs-lookup"><span data-stu-id="4b822-138">Create a new Chrome App</span></span>
<span data-ttu-id="4b822-139">L'esempio seguente è basato sull' [esempio GCM per app Chrome] e usa il metodo consigliato per creare un'app Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span></span> <span data-ttu-id="4b822-140">Le sezioni seguenti evidenziano i passaggi relativi all'Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b822-140">We will highlight the steps specifically related to Azure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4b822-141">È consigliabile scaricare l'origine dell'app Chrome dall' [esempio di hub di notifica per l'app Chrome].</span><span class="sxs-lookup"><span data-stu-id="4b822-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="4b822-142">L'app Chrome viene creata tramite JavaScript ed è possibile usare il proprio editor di testo preferito a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="4b822-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="4b822-143">L'app Chrome avrà un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="4b822-143">Below is what this Chrome App will look like.</span></span>

![App Google Chrome][15]

1. <span data-ttu-id="4b822-145">Creare una cartella e denominarla `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="4b822-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="4b822-146">Naturalmente, il nome è arbitrario. Se si assegnano nomi diversi, assicurarsi di sostituire il percorso nei segmenti di codice necessari.</span><span class="sxs-lookup"><span data-stu-id="4b822-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span></span>
2. <span data-ttu-id="4b822-147">Scaricare la [libreria crypto-js] nella cartella creata nel secondo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4b822-147">Download the [crypto-js library] in the folder you created in the second step.</span></span> <span data-ttu-id="4b822-148">Questa cartella della libreria contiene due sottocartelle: `components` e `rollups`.</span><span class="sxs-lookup"><span data-stu-id="4b822-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="4b822-149">Creare un file `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="4b822-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="4b822-150">Tutte le app Chrome sono accompagnate da un file manifesto che contiene i metadati dell'app e, più importante, tutte le autorizzazioni concesse all'applicazione quando viene installata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="4b822-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span></span>
   
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
   
    <span data-ttu-id="4b822-151">Si noti l'elemento `permissions` , che specifica che l'app Chrome può ricevere notifiche push da GCM.</span><span class="sxs-lookup"><span data-stu-id="4b822-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span></span> <span data-ttu-id="4b822-152">È anche necessario specificare l'URI di Hub di notifica di Azure in cui l'app Chrome eseguirà una chiamata REST per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="4b822-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span></span>
    <span data-ttu-id="4b822-153">L'esempio usa anche un file di icona, `gcm_128.png`, disponibile nell'origine riutilizzata dall'esempio GCM originale.</span><span class="sxs-lookup"><span data-stu-id="4b822-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span></span> <span data-ttu-id="4b822-154">È possibile sostituirlo con qualsiasi immagine che soddisfa i [criteri relativi alle icone](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="4b822-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="4b822-155">Creare un file denominato `background.js` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="4b822-155">Create a file called `background.js` with the following code:</span></span>
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
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
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="4b822-156">Si tratta del file che visualizza il codice HTML della finestra dell'app Chrome (**register.html**) e che definisce anche il gestore **messageReceived** per la gestione della notifica push in arrivo.</span><span class="sxs-lookup"><span data-stu-id="4b822-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span></span>
5. <span data-ttu-id="4b822-157">Creare un file denominato `register.html` che definisce l'interfaccia utente dell'app Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4b822-158">Questo esempio usa **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="4b822-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="4b822-159">Se è stata scaricata un'altra versione della libreria, assicurarsi di sostituire correttamente la versione nel percorso `src` .</span><span class="sxs-lookup"><span data-stu-id="4b822-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span></span>
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
6. <span data-ttu-id="4b822-160">Creare un file denominato `register.js` con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="4b822-160">Create a file called `register.js` with the code below.</span></span> <span data-ttu-id="4b822-161">Questo file specifica lo script di base di `register.html`.</span><span class="sxs-lookup"><span data-stu-id="4b822-161">This file specifies the script behind `register.html`.</span></span> <span data-ttu-id="4b822-162">Le app Chrome non consentono l'esecuzione in linea, quindi è necessario creare uno script separato per l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4b822-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span></span>
   
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
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
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
   
          // Update the payload with the registration ID obtained earlier.
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
   
    <span data-ttu-id="4b822-163">Lo script precedente include i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b822-163">The above script has the following key parameters:</span></span>
   
   * <span data-ttu-id="4b822-164">**window.onload** definisce gli eventi clic dei due pulsanti nell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4b822-164">**window.onload** defines the button-click events of the two buttons on the UI.</span></span> <span data-ttu-id="4b822-165">Uno effettua la registrazione con GCM e l'altro usa l'ID della registrazione restituito dopo la registrazione con GCM per effettuare la registrazione all'Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b822-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="4b822-166">**updateLog** è la funzione che consente di gestire semplici funzionalità di registrazione.</span><span class="sxs-lookup"><span data-stu-id="4b822-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span></span>
   * <span data-ttu-id="4b822-167">**registerWithGCM** è il primo gestore di eventi clic del pulsante che esegue la chiamata `chrome.gcm.register` a GCM per registrare questa istanza corrente dell'app Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span></span>
   * <span data-ttu-id="4b822-168">**registerCallback** è la funzione di callback che riceve la chiamata quando viene restituita la chiamata di registrazione GCM.</span><span class="sxs-lookup"><span data-stu-id="4b822-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span></span>
   * <span data-ttu-id="4b822-169">**registerWithNH** è il secondo gestore di eventi clic del pulsante che esegue la registrazione con Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="4b822-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="4b822-170">Ottiene `hubName` e `connectionString` specificati dall'utente e crea la chiamata all'API REST per la registrazione con Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="4b822-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="4b822-171">**splitConnectionString** e **generateSaSToken** sono helper che rappresentano l'implementazione JavaScript del processo di creazione di un token di firma di accesso condiviso da usare in tutte le chiamate all'API REST.</span><span class="sxs-lookup"><span data-stu-id="4b822-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="4b822-172">Per altre informazioni, vedere [Concetti comuni](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b822-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="4b822-173">**sendNHRegistrationRequest** è la funzione che esegue una chiamata REST HTTP ad Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b822-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span></span>
   * <span data-ttu-id="4b822-174">**registrationPayload** definisce il payload XML di registrazione.</span><span class="sxs-lookup"><span data-stu-id="4b822-174">**registrationPayload** defines the registration XML payload.</span></span> <span data-ttu-id="4b822-175">Per altre informazioni, vedere [Creare una registrazione dell'API REST per l'Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="4b822-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="4b822-176">L'ID della registrazione viene aggiornato con i dati ricevuti da GCM.</span><span class="sxs-lookup"><span data-stu-id="4b822-176">We update the registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="4b822-177">**client** è un'istanza di **XMLHttpRequest** usata per eseguire la richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="4b822-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span></span> <span data-ttu-id="4b822-178">L'intestazione `Authorization` viene aggiornata con `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="4b822-178">Note that we update the `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="4b822-179">Il corretto completamento di questa chiamata registra questa istanza dell'app Chrome in Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b822-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="4b822-180">La struttura di cartelle complessiva per questo progetto sarà analoga alla seguente: ![App di Google Chrome - Struttura cartelle][21]</span><span class="sxs-lookup"><span data-stu-id="4b822-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="4b822-181">Configurare e testare l'app Chrome</span><span class="sxs-lookup"><span data-stu-id="4b822-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="4b822-182">Aprire il browser Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-182">Open your Chrome browser.</span></span> <span data-ttu-id="4b822-183">Aprire le **estensioni Chrome** e abilitare la **Modalità sviluppatore**.</span><span class="sxs-lookup"><span data-stu-id="4b822-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="4b822-184">Fare clic su **Load unpacked extension** e selezionare la cartella in cui sono stati creati i file.</span><span class="sxs-lookup"><span data-stu-id="4b822-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span></span> <span data-ttu-id="4b822-185">È facoltativamente possibile usare anche lo **strumento per sviluppatori di estensioni e app Chrome**.</span><span class="sxs-lookup"><span data-stu-id="4b822-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="4b822-186">Questo strumento è a sua volta un'app Chrome (installata da Chrome Web Store) e fornisce capacità di debug avanzate per lo sviluppo di app Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="4b822-187">Se l'app Chrome viene creata senza errori, verrà visualizzata.</span><span class="sxs-lookup"><span data-stu-id="4b822-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="4b822-188">Immettere il valore **Nome progetto** ottenuto in precedenza da **Google Cloud Console** come ID del mittente e fare clic su **Register with GCM** (Registra con GCM).</span><span class="sxs-lookup"><span data-stu-id="4b822-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="4b822-189">Verrà visualizzato un messaggio **Registration with GCM succeeded**</span><span class="sxs-lookup"><span data-stu-id="4b822-189">You must see the message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="4b822-190">Immettere i valori **Nome hub di notifica** e **DefaultListenSharedAccessSignature** ottenuti in precedenza dal portale, quindi fare clic su **Register with Azure Notification Hub** (Registra con l'hub di notifica di Azure).</span><span class="sxs-lookup"><span data-stu-id="4b822-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="4b822-191">Verrà visualizzato un messaggio **Notification Hub Registration successful!**</span><span class="sxs-lookup"><span data-stu-id="4b822-191">You must see the message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="4b822-192">e i dettagli della risposta della registrazione, che contiene l'ID di registrazione di Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b822-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="4b822-193"><a name="send"></a>Inviare una notifica all'app Chrome</span><span class="sxs-lookup"><span data-stu-id="4b822-193"><a name="send"></a>Send a notification to your Chrome App</span></span>
<span data-ttu-id="4b822-194">A scopo di test, verranno inviate notifiche push a Chrome usando un'applicazione console .NET.</span><span class="sxs-lookup"><span data-stu-id="4b822-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="4b822-195">È possibile inviare notifiche push con Hub di notifica da qualsiasi back-end tramite l'<a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaccia REST</a> pubblica.</span><span class="sxs-lookup"><span data-stu-id="4b822-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="4b822-196">Consultare il [portale di documentazione](https://azure.microsoft.com/documentation/services/notification-hubs/) per altri esempi multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="4b822-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="4b822-197">In Visual Studio scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="4b822-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="4b822-198">In **Visual C#** fare clic su **Windows** e **Applicazione console**, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b822-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="4b822-199">Verrà creato un nuovo progetto di applicazione console.</span><span class="sxs-lookup"><span data-stu-id="4b822-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="4b822-200">Scegliere **Gestione pacchetti libreria** dal menu **Strumenti**, quindi fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="4b822-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="4b822-201">Verrà visualizzata la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4b822-201">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="4b822-202">Nella finestra della console eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4b822-202">In the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="4b822-203">Aprire `Program.cs` e aggiungere l'istruzione `using`:</span><span class="sxs-lookup"><span data-stu-id="4b822-203">Open `Program.cs` and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="4b822-204">Nella classe `Program` aggiungere il metodo seguente.</span><span class="sxs-lookup"><span data-stu-id="4b822-204">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="4b822-205">Assicurarsi di usare la stringa di connessione con accesso **Full**, non con accesso **Listen**.</span><span class="sxs-lookup"><span data-stu-id="4b822-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="4b822-206">La stringa di connessione di accesso di tipo **Listen** non ha le autorizzazioni per l'invio di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="4b822-206">The **Listen** access connection string does not grant permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="4b822-207">Aggiungere le chiamate seguenti al metodo `Main` :</span><span class="sxs-lookup"><span data-stu-id="4b822-207">Add the following calls in the `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="4b822-208">Assicurarsi che Chrome sia in esecuzione ed eseguire l'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="4b822-208">Make sure that Chrome is running, and run the console application.</span></span>
8. <span data-ttu-id="4b822-209">Verrà visualizzato il seguente popup di notifica sul desktop.</span><span class="sxs-lookup"><span data-stu-id="4b822-209">You should see the following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="4b822-210">È anche possibile visualizzare tutte le notifiche tramite la finestra delle notifiche di Chrome sulla barra delle applicazioni (in Windows) quando Chrome è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4b822-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="4b822-211">Non è necessario che l'app Chrome sia in esecuzione o aperta nel browser, anche se il browser Chrome deve essere in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4b822-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span></span> <span data-ttu-id="4b822-212">È inoltre possibile ottenere una vista consolidata di tutte le notifiche nella finestra delle notifiche di Chrome.</span><span class="sxs-lookup"><span data-stu-id="4b822-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="4b822-213"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b822-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="4b822-214">Per altre informazioni sugli hub di notifica, vedere [Panoramica dell'Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="4b822-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="4b822-215">Per rivolgersi a utenti specifici, vedere l'esercitazione [Uso di Hub di notifica di Azure per inviare notifiche agli utenti] .</span><span class="sxs-lookup"><span data-stu-id="4b822-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="4b822-216">Per segmentare gli utenti in base ai gruppi di interesse, eseguire l'esercitazione [Uso di Hub di notifica per inviare le ultime notizie] .</span><span class="sxs-lookup"><span data-stu-id="4b822-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span></span>

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
<span data-ttu-id="4b822-217">[esempio di hub di notifica per l'app Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span><span class="sxs-lookup"><span data-stu-id="4b822-217">[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span></span>
<span data-ttu-id="4b822-218">[Google Cloud Console]: http://cloud.google.com/console</span><span class="sxs-lookup"><span data-stu-id="4b822-218">[Google Cloud Console]: http://cloud.google.com/console</span></span>
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="4b822-219">[Panoramica dell'Hub di notifica]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="4b822-219">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="4b822-220">[panoramica delle app Chrome]: https://developer.chrome.com/apps/about_apps</span><span class="sxs-lookup"><span data-stu-id="4b822-220">[Chrome Apps Overview]: https://developer.chrome.com/apps/about_apps</span></span>
<span data-ttu-id="4b822-221">[esempio GCM per app Chrome]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span><span class="sxs-lookup"><span data-stu-id="4b822-221">[Chrome App GCM Sample]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span></span>
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
<span data-ttu-id="4b822-222">[App Chrome su dispositivi mobili]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span><span class="sxs-lookup"><span data-stu-id="4b822-222">[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span></span>
<span data-ttu-id="4b822-223">[Creare una registrazione dell'API REST per l'Hub di notifica]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span><span class="sxs-lookup"><span data-stu-id="4b822-223">[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span></span>
<span data-ttu-id="4b822-224">[libreria crypto-js]: http://code.google.com/p/crypto-js/</span><span class="sxs-lookup"><span data-stu-id="4b822-224">[crypto-js library]: http://code.google.com/p/crypto-js/</span></span>
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
<span data-ttu-id="4b822-225">[Google Cloud Messaging per Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span><span class="sxs-lookup"><span data-stu-id="4b822-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span></span>
<span data-ttu-id="4b822-226">[Uso di Hub di notifica di Azure per inviare notifiche agli utenti]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="4b822-226">[Azure Notification Hubs Notify Users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="4b822-227">[Uso di Hub di notifica per inviare le ultime notizie]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="4b822-227">[Azure Notification Hubs breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
