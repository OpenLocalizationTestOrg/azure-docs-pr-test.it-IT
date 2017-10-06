---
title: aaaSending proteggere le notifiche Push con hub di notifica di Azure
description: Informazioni su come toosend sicura push app Android di notifiche tooan da Azure. Gli esempi di codice sono scritti in Java e C#.
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
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="a5764-105">Invio di notifiche push sicure con Hub di notifica di Azure</span><span class="sxs-lookup"><span data-stu-id="a5764-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5764-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a5764-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="a5764-107">iOS</span><span class="sxs-lookup"><span data-stu-id="a5764-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="a5764-108">Android</span><span class="sxs-lookup"><span data-stu-id="a5764-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a5764-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a5764-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a5764-110">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a5764-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a5764-111">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a5764-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a5764-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="a5764-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="a5764-113">Supporto di notifica push di Microsoft Azure consente tooaccess un'infrastruttura di messaggio push da usare, multipiattaforma e con scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per applicazioni aziendali e per piattaforme per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a5764-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="a5764-114">A causa di vincoli di sicurezza o tooregulatory, un'applicazione potrebbe talvolta tooinclude qualcosa nel notifica hello che non può essere trasmesso tramite l'infrastruttura di notifica push standard hello.</span><span class="sxs-lookup"><span data-stu-id="a5764-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="a5764-115">In questa esercitazione viene descritto come tooachieve hello stessa esperienza inviando informazioni riservate tramite una connessione autenticata protetta tra i dispositivi Android di hello client e di back-end app hello.</span><span class="sxs-lookup"><span data-stu-id="a5764-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="a5764-116">In generale, il flusso di hello è il seguente:</span><span class="sxs-lookup"><span data-stu-id="a5764-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="a5764-117">Hello app back-end:</span><span class="sxs-lookup"><span data-stu-id="a5764-117">hello app back-end:</span></span>
   * <span data-ttu-id="a5764-118">Archivia il payload sicuro nel database back-end.</span><span class="sxs-lookup"><span data-stu-id="a5764-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="a5764-119">Invia ID hello di questo dispositivo Android toohello notifica (viene inviata alcuna informazione protetta).</span><span class="sxs-lookup"><span data-stu-id="a5764-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="a5764-120">Hello app sul dispositivo hello, quando si riceve notifica hello:</span><span class="sxs-lookup"><span data-stu-id="a5764-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="a5764-121">dispositivo Android Hello contatta hello back-end richiedente hello sicura payload.</span><span class="sxs-lookup"><span data-stu-id="a5764-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="a5764-122">app Hello possono mostrare payload hello come una notifica sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a5764-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="a5764-123">È importante in hello precedente del flusso e in questa esercitazione, si presuppone che il dispositivo hello toonote memorizza un token di autenticazione nel servizio di archiviazione locale, dopo hello utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a5764-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="a5764-124">In questo modo si garantisce un'esperienza completamente trasparente, come dispositivo hello può recuperare i payload della notifica hello protetto con questo token.</span><span class="sxs-lookup"><span data-stu-id="a5764-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="a5764-125">Se l'applicazione non archivia i token di autenticazione nel dispositivo hello o se i token possono scadere, hello dispositivo app, al momento della ricezione di notifiche push hello deve visualizzare una notifica generica richiesta hello utente toolaunch hello app.</span><span class="sxs-lookup"><span data-stu-id="a5764-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="a5764-126">app Hello quindi esegue l'autenticazione utente hello e Mostra il payload di notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="a5764-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="a5764-127">Questa esercitazione viene illustrato come le notifiche push toosend sicura.</span><span class="sxs-lookup"><span data-stu-id="a5764-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="a5764-128">È basato su hello [notifica utenti](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) esercitazione, pertanto è necessario completare i passaggi di hello in tale esercitazione prima di tutto se hai già fatto.</span><span class="sxs-lookup"><span data-stu-id="a5764-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="a5764-129">In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a5764-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="a5764-130">Modificare progetto Android hello</span><span class="sxs-lookup"><span data-stu-id="a5764-130">Modify hello Android project</span></span>
<span data-ttu-id="a5764-131">Ora che è stato modificato il hello solo toosend back-end di app *id* di una notifica push, aver toochange toohandle l'app Android di notifica e chiamare nuovamente il hello tooretrieve back-end protetta toobe messaggio visualizzato.</span><span class="sxs-lookup"><span data-stu-id="a5764-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="a5764-132">tooachieve questo obiettivo è verificare che l'app Android SA toomake come tooauthenticate stesso con il back-end quando riceve le notifiche push hello.</span><span class="sxs-lookup"><span data-stu-id="a5764-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="a5764-133">Si modificherà ora hello *accesso* flusso in ordine toosave hello autenticazione intestazione valore hello condivise le preferenze dell'app.</span><span class="sxs-lookup"><span data-stu-id="a5764-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="a5764-134">Meccanismi analoghi possono essere utilizzati toostore qualsiasi token di autenticazione (ad esempio, i token OAuth) che hello app avrà toouse senza richiedere le credenziali dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a5764-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="a5764-135">Nel progetto di app Android aggiungere hello seguenti costanti nella parte superiore di hello di hello **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="a5764-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="a5764-136">Ancora in hello **MainActivity** (classe), aggiornamento hello `getAuthorizationHeader()` hello toocontain metodo seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a5764-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="a5764-137">Aggiungere il seguente hello `import` le istruzioni nella parte superiore di hello di hello **MainActivity** file:</span><span class="sxs-lookup"><span data-stu-id="a5764-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="a5764-138">Verrà ora modificata gestore hello che viene chiamato quando viene ricevuta la notifica hello.</span><span class="sxs-lookup"><span data-stu-id="a5764-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="a5764-139">In hello **MyHandler** classe modificare hello `OnReceive()` toocontain metodo:</span><span class="sxs-lookup"><span data-stu-id="a5764-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="a5764-140">Aggiungere quindi hello `retrieveNotification()` metodo, sostituendo il segnaposto hello `{back-end endpoint}` con endpoint di back-end hello ottenuto durante la distribuzione il back-end:</span><span class="sxs-lookup"><span data-stu-id="a5764-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="a5764-141">Questo metodo chiama la notifica hello tooretrieve back-end app contenuta utilizzando le credenziali di hello archiviate in hello condiviso preferenze e viene visualizzato sotto forma di una notifica normale.</span><span class="sxs-lookup"><span data-stu-id="a5764-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="a5764-142">notifica Hello ricerca utente app toohello esattamente come qualsiasi altra notifica push.</span><span class="sxs-lookup"><span data-stu-id="a5764-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="a5764-143">Si noti che è preferibile toohandle casi di hello di proprietà di intestazione di autenticazione mancante o il rifiuto da hello back-end.</span><span class="sxs-lookup"><span data-stu-id="a5764-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="a5764-144">gestione di specifica Hello di questi casi dipendono principalmente l'esperienza utente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a5764-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="a5764-145">È una notifica con un messaggio generico per notifica effettivo di hello utente tooauthenticate tooretrieve hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="a5764-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="a5764-146">Eseguire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a5764-146">Run hello Application</span></span>
<span data-ttu-id="a5764-147">toorun applicazione hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a5764-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="a5764-148">Assicurarsi che il progetto **AppBackend** sia distribuito in Azure.</span><span class="sxs-lookup"><span data-stu-id="a5764-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="a5764-149">Se si usa Visual Studio, eseguire hello **AppBackend** applicazione API Web.</span><span class="sxs-lookup"><span data-stu-id="a5764-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="a5764-150">Verrà visualizzata una pagina Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a5764-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="a5764-151">In Eclipse, eseguire l'applicazione hello in un emulatore fisico hello o di dispositivi Android.</span><span class="sxs-lookup"><span data-stu-id="a5764-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="a5764-152">Nell'app Android hello dell'interfaccia utente, immettere un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="a5764-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="a5764-153">Può trattarsi di qualsiasi stringa, ma devono essere hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="a5764-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="a5764-154">Nell'app Android hello dell'interfaccia utente, fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="a5764-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="a5764-155">Fare clic su **Send push**.</span><span class="sxs-lookup"><span data-stu-id="a5764-155">Then click **Send push**.</span></span>

