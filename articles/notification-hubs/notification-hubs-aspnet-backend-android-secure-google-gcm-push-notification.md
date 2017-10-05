---
title: Invio di notifiche push sicure con Hub di notifica di Azure
description: Informazioni su come inviare notifiche push sicure a un'app per Android da Azure. Gli esempi di codice sono scritti in Java e C#.
documentationcenter: android
keywords: notifica push, notifiche push, push dei messaggi, notifiche push di android
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 29f8c516e611c13fb73c7edc15e7c52708c75bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="cd888-105">Invio di notifiche push sicure con Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="cd888-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd888-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="cd888-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="cd888-107">iOS</span><span class="sxs-lookup"><span data-stu-id="cd888-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="cd888-108">Android</span><span class="sxs-lookup"><span data-stu-id="cd888-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="cd888-109">Overview</span><span class="sxs-lookup"><span data-stu-id="cd888-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cd888-110">Per completare l'esercitazione, è necessario disporre di un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="cd888-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="cd888-111">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="cd888-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cd888-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="cd888-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="cd888-113">Il supporto per le notifiche push in Microsoft Azure consente di accedere a un'infrastruttura di messaggistica push di facile utilizzo, multipiattaforma con scalabilità orizzontale, che semplifica considerevolmente l'implementazione delle notifiche push sia per le applicazioni consumer sia per quelle aziendali per piattaforme mobili.</span><span class="sxs-lookup"><span data-stu-id="cd888-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="cd888-114">A causa di vincoli normativi o di sicurezza, un'applicazione potrebbe talvolta includere nella notifica informazioni che non è possibile trasmettere attraverso l'infrastruttura di notifiche push standard.</span><span class="sxs-lookup"><span data-stu-id="cd888-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="cd888-115">Questa esercitazione descrive come conseguire la stessa esperienza inviando informazioni sensibili attraverso una connessione autenticata e sicura tra il dispositivo client Android e il back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="cd888-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span></span>

<span data-ttu-id="cd888-116">A livello generale, il flusso è il seguente:</span><span class="sxs-lookup"><span data-stu-id="cd888-116">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="cd888-117">Il back-end dell'app:</span><span class="sxs-lookup"><span data-stu-id="cd888-117">The app back-end:</span></span>
   * <span data-ttu-id="cd888-118">Archivia il payload sicuro nel database back-end.</span><span class="sxs-lookup"><span data-stu-id="cd888-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="cd888-119">Invia l'ID di questa notifica al dispositivo Android (non vengono inviate informazioni sicure).</span><span class="sxs-lookup"><span data-stu-id="cd888-119">Sends the ID of this notification to the Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="cd888-120">L'app sul dispositivo, quando riceve la notifica:</span><span class="sxs-lookup"><span data-stu-id="cd888-120">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="cd888-121">Il dispositivo Android contatta il back-end richiedendo il payload sicuro.</span><span class="sxs-lookup"><span data-stu-id="cd888-121">The Android device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="cd888-122">L'app può indicare il payload come una notifica sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cd888-122">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="cd888-123">È importante notare che nel flusso precedente e in questa esercitazione si presuppone che il dispositivo archivi un token di autenticazione nella memoria locale, dopo l’accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cd888-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="cd888-124">Ciò garantisce un'esperienza completamente lineare, in quanto il dispositivo può recuperare il payload sicuro della notifica tramite questo token.</span><span class="sxs-lookup"><span data-stu-id="cd888-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="cd888-125">Se invece l'applicazione non archivia i token di autenticazione nel dispositivo o se questi hanno una scadenza, l'app per dispositivo, alla ricezione della notifica push, dovrà visualizzare una notifica generica in cui si richiede all'utente di avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="cd888-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="cd888-126">L'app autentica quindi l'utente e mostra il payload di notifica.</span><span class="sxs-lookup"><span data-stu-id="cd888-126">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="cd888-127">Questa esercitazione descrive come inviare notifiche push sicure.</span><span class="sxs-lookup"><span data-stu-id="cd888-127">This tutorial shows how to send secure push notifications.</span></span> <span data-ttu-id="cd888-128">Poiché i passaggi descritti in questa esercitazione si basano su quella relativa all' [invio di notifiche agli utenti](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) , sarà prima necessario completare i passaggi di quest'ultima.</span><span class="sxs-lookup"><span data-stu-id="cd888-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="cd888-129">In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cd888-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a><span data-ttu-id="cd888-130">Modificare il progetto Android</span><span class="sxs-lookup"><span data-stu-id="cd888-130">Modify the Android project</span></span>
<span data-ttu-id="cd888-131">Ora che è stato modificato il back-end dell'app in modo da inviare solo l' *ID* di una notifica push, è necessario modificare l'app per Android in modo da gestire tale notifica e richiamare il back-end per recuperare il messaggio sicuro da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="cd888-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>
<span data-ttu-id="cd888-132">Per conseguire questo obiettivo, è necessario assicurarsi che l'app per Android sia in grado di eseguire l'autenticazione con il back-end quando riceve le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="cd888-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span></span>

<span data-ttu-id="cd888-133">Ora si modificherà il flusso di *accesso* per salvare il valore dell'intestazione di autenticazione nelle preferenze condivise dell'app.</span><span class="sxs-lookup"><span data-stu-id="cd888-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span></span> <span data-ttu-id="cd888-134">Un meccanismo analogo può essere usato per archiviare eventuali token di autenticazione (ad esempio token OAuth) che l'app dovrà usare senza richiedere le credenziali dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cd888-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span></span>

1. <span data-ttu-id="cd888-135">Nel progetto di app per Android, aggiungere le costanti seguenti all'inizio della classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="cd888-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="cd888-136">Sempre nella classe **MainActivity** aggiornare il metodo `getAuthorizationHeader()` per includere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="cd888-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="cd888-137">Aggiungere le seguenti istruzioni `import` all'inizio del file **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="cd888-137">Add the following `import` statements at the top of the **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="cd888-138">A questo punto, modificare il gestore chiamato quando si riceve la notifica.</span><span class="sxs-lookup"><span data-stu-id="cd888-138">Now we will change the handler that is called when the notification is received.</span></span>

1. <span data-ttu-id="cd888-139">Nella classe **MyHandler** modificare il metodo `OnReceive()` in modo che contenga:</span><span class="sxs-lookup"><span data-stu-id="cd888-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="cd888-140">Aggiungere quindi il metodo `retrieveNotification()`, sostituendo il segnaposto `{back-end endpoint}` con l'endpoint del back-end ottenuto durante la distribuzione del back-end:</span><span class="sxs-lookup"><span data-stu-id="cd888-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed to retrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="cd888-141">Questo metodo chiama il back-end dell'app per recuperare il contenuto della notifica usando le credenziali memorizzate nelle preferenze condivise e lo visualizza come una normale notifica.</span><span class="sxs-lookup"><span data-stu-id="cd888-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="cd888-142">L'utente dell'app vedrà la notifica esattamente come qualsiasi altra notifica push.</span><span class="sxs-lookup"><span data-stu-id="cd888-142">The notification looks to the app user exactly like any other push notification.</span></span>

<span data-ttu-id="cd888-143">Notare che è preferibile gestire i casi in cui manca la proprietà dell'intestazione di autenticazione o di rifiuto da parte del back-end.</span><span class="sxs-lookup"><span data-stu-id="cd888-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="cd888-144">La gestione specifica di questi casi dipende in larga misura dall'esperienza dell'utente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="cd888-144">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="cd888-145">Una delle opzioni consiste nel visualizzare una notifica con un prompt generico affinché l'utente possa autenticarsi per recuperare la notifica effettiva.</span><span class="sxs-lookup"><span data-stu-id="cd888-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="cd888-146">Esecuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="cd888-146">Run the Application</span></span>
<span data-ttu-id="cd888-147">Per eseguire l'applicazione, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd888-147">To run the application, do the following:</span></span>

1. <span data-ttu-id="cd888-148">Assicurarsi che il progetto **AppBackend** sia distribuito in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd888-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="cd888-149">Se si usa Visual Studio, eseguire l'applicazione API Web **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="cd888-149">If using Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="cd888-150">Verrà visualizzata una pagina Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cd888-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="cd888-151">In Eclipse eseguire l'app su un dispositivo Android fisico o sull'emulatore.</span><span class="sxs-lookup"><span data-stu-id="cd888-151">In Eclipse, run the app on a physical Android device or the emulator.</span></span>
3. <span data-ttu-id="cd888-152">Nell'interfaccia utente dell'app per Android immettere un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="cd888-152">In the Android app UI, enter a username and password.</span></span> <span data-ttu-id="cd888-153">Può trattarsi di qualsiasi stringa, ma devono avere lo stesso valore.</span><span class="sxs-lookup"><span data-stu-id="cd888-153">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="cd888-154">Nell'interfaccia utente dell'app per Android fare clic su **Log in**.</span><span class="sxs-lookup"><span data-stu-id="cd888-154">In the Android app UI, click **Log in**.</span></span> <span data-ttu-id="cd888-155">Fare clic su **Send push**.</span><span class="sxs-lookup"><span data-stu-id="cd888-155">Then click **Send push**.</span></span>

