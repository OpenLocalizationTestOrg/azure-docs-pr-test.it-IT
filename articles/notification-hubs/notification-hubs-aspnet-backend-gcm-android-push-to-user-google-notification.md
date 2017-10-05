---
title: Uso di Hub di notifica di Azure per inviare notifiche agli utenti per Android con back-end .NET
description: Informazioni su come inviare notifiche push agli utenti in Azure. Esempi di codice scritti in Java per Android
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 418a4b638dfaa3fee33a7a7242433699205c79f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="bd923-104">Uso di Hub di notifica di Azure per inviare notifiche agli utenti per Android con back-end .NET</span><span class="sxs-lookup"><span data-stu-id="bd923-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="bd923-105">Overview</span><span class="sxs-lookup"><span data-stu-id="bd923-105">Overview</span></span>
<span data-ttu-id="bd923-106">Il supporto per le notifiche push in Azure consente di accedere a un'infrastruttura push facile da usare, multipiattaforma e con scalabilità orizzontale, che semplifica considerevolmente l'implementazione delle notifiche push sia per le applicazioni consumer sia per quelle aziendali per piattaforme mobili.</span><span class="sxs-lookup"><span data-stu-id="bd923-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="bd923-107">In questa esercitazione viene illustrato come usare Hub di notifica di Azure per inviare notifiche push a un utente specifico dell'app su un dispositivo specifico.</span><span class="sxs-lookup"><span data-stu-id="bd923-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="bd923-108">Per autenticare i client e generare le notifiche viene usato un back-end di API Web ASP.NET, come illustrato nell'argomento [Registrazione dal back-end dell'app](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="bd923-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="bd923-109">Questa esercitazione si basa sull'hub di notifica creato nell'esercitazione [Introduzione ad Hub di notifica (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="bd923-109">This tutorial builds on the notification hub that you created in the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="bd923-110">In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bd923-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-the-android-project"></a><span data-ttu-id="bd923-111">Creare il progetto Android</span><span class="sxs-lookup"><span data-stu-id="bd923-111">Create the Android Project</span></span>
<span data-ttu-id="bd923-112">Il passaggio successivo consiste nella creazione dell'applicazione per Android.</span><span class="sxs-lookup"><span data-stu-id="bd923-112">The next step is to create the Android application.</span></span>

1. <span data-ttu-id="bd923-113">Seguire l'esercitazione [Introduzione ad Hub di notifica (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) per creare e configurare l'app per la ricezione di notifiche push da GCM.</span><span class="sxs-lookup"><span data-stu-id="bd923-113">Follow the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial to create and configure your app to receive push notifications from GCM.</span></span>
2. <span data-ttu-id="bd923-114">Aprire il file **res/layout/activity_main.xml** e sostituire il contenuto con le definizioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="bd923-114">Open your **res/layout/activity_main.xml** file, replace the with the following content definitions.</span></span>
   
    <span data-ttu-id="bd923-115">Verranno aggiunti nuovi controlli EditText per l'accesso come utente.</span><span class="sxs-lookup"><span data-stu-id="bd923-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="bd923-116">Viene aggiunto anche un campo per un tag username che farà parte delle notifiche inviate:</span><span class="sxs-lookup"><span data-stu-id="bd923-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. <span data-ttu-id="bd923-117">Aprire il file **res/values/strings.xml** e sostituire la definizione `send_button` con le righe seguenti per ridefinire la stringa per `send_button` e aggiungere stringhe per gli altri controlli:</span><span class="sxs-lookup"><span data-stu-id="bd923-117">Open your **res/values/strings.xml** file and replace the `send_button` definition with the following lines that redefine the string for the `send_button` and add strings for the other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="bd923-118">A questo punto il layout grafico del file main_activity.xml dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="bd923-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="bd923-119">Creare una nuova classe denominata **RegisterClient** nello stesso pacchetto della classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="bd923-119">Create a new class named **RegisterClient** in the same package as your `MainActivity` class.</span></span> <span data-ttu-id="bd923-120">Usare il codice seguente per il nuovo file di classe.</span><span class="sxs-lookup"><span data-stu-id="bd923-120">Use the code below for the new class file.</span></span>
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    <span data-ttu-id="bd923-121">Questo componente implementa le chiamate REST necessarie per contattare il back-end dell'app allo scopo di effettuare la registrazione per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="bd923-121">This component implements the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="bd923-122">Archivia inoltre in locale i *registrationId* creati dall'hub di notifica, come illustrato in [Registrazione dal back-end dell'app](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="bd923-122">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="bd923-123">Si noti che usa un token di autorizzazione memorizzato nell'archivio locale quando si fa clic sul pulsante **Log in** .</span><span class="sxs-lookup"><span data-stu-id="bd923-123">Note that it uses an authorization token stored in local storage when you click the **Log in** button.</span></span>
5. <span data-ttu-id="bd923-124">Nella classe `MainActivity` rimuovere o impostare come commento il campo privato per `NotificationHub` e aggiungere un campo per la classe `RegisterClient` e una stringa per l'endpoint del back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bd923-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for the `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="bd923-125">Assicurarsi di sostituire `<Enter Your Backend Endpoint>` con l'endpoint back-end effettivo ottenuto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="bd923-125">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="bd923-126">Ad esempio: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="bd923-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="bd923-127">Nella classe `MainActivity`, all'interno del metodo `onCreate`, rimuovere o impostare come commento l'inizializzazione del campo `hub` e la chiamata al metodo `registerWithNotificationHubs`.</span><span class="sxs-lookup"><span data-stu-id="bd923-127">In your `MainActivity` class, in the `onCreate` method, remove or comment out the initialization of the `hub` field and the call to the `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="bd923-128">Aggiungere quindi il codice per inizializzare un'istanza della classe `RegisterClient` .</span><span class="sxs-lookup"><span data-stu-id="bd923-128">Then add code to initialize an instance of the `RegisterClient` class.</span></span> <span data-ttu-id="bd923-129">Il metodo deve contenere le seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="bd923-129">The method should contain the following lines:</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. <span data-ttu-id="bd923-130">Nella classe `MainActivity` eliminare o impostare come commento tutto il metodo `registerWithNotificationHubs`.</span><span class="sxs-lookup"><span data-stu-id="bd923-130">In your `MainActivity` class, delete or comment out the entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="bd923-131">Non verrà usato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bd923-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="bd923-132">Aggiungere le istruzioni `import` seguenti al file **MainActivity.java** .</span><span class="sxs-lookup"><span data-stu-id="bd923-132">Add the following `import` statements to your **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="bd923-133">Aggiungere quindi i metodi seguenti per gestire l'evento clic del pulsante **Log in** e inviare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="bd923-133">Then, add the following methods to handle the **Log in** button click event and sending push notifications.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed to register", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls the ASP.NET WebAPI backend to send the notification message
         * to the platform notification service based on the pns parameter.
         *
         * @param pns     The platform notification service to send the notification message to. Must
         *                be one of the following ("wns", "gcm", "apns").
         * @param userTag The tag for the user who will receive the notification message. This string
         *                must not contain spaces or special characters.
         * @param message The notification message string. This string must include the double quotes
         *                to be used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed to send " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="bd923-134">Il gestore `login` per il pulsante **Log in`RegisterClient` genera un token di autenticazione di base usando il nome utente e la password di input. Si noti che rappresenta qualsiasi token usato dallo schema di autenticazione, quindi usa**  per chiamare il back-end per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="bd923-134">The `login` handler for the **Log in** button generates a basic authentication token using on the input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` to call the backend for registration.</span></span>

    <span data-ttu-id="bd923-135">Il metodo `sendPush` chiama il back-end per attivare una notifica sicura per l'utente in base al tag user.</span><span class="sxs-lookup"><span data-stu-id="bd923-135">The `sendPush` method calls the backend to trigger a secure notification to the user based on the user tag.</span></span> <span data-ttu-id="bd923-136">Il servizio di notifica della piattaforma a cui è destinato `sendPush` dipende dalla stringa `pns` passata.</span><span class="sxs-lookup"><span data-stu-id="bd923-136">The platform notification service that `sendPush` targets depends on the `pns` string passed in.</span></span>

1. <span data-ttu-id="bd923-137">Nella classe `MainActivity` aggiornare il metodo`sendNotificationButtonOnClick` per chiamare il metodo `sendPush` con i servizi di notifica della piattaforma selezionati dell'utente, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bd923-137">In your `MainActivity` class, update the `sendNotificationButtonOnClick` method to call the `sendPush` method with the user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends the push notification
        * message to each platform selected.
        *
        * @param v The view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-the-application"></a><span data-ttu-id="bd923-138">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="bd923-138">Run the Application</span></span>
1. <span data-ttu-id="bd923-139">Eseguire l'applicazione su un dispositivo o un emulatore tramite Android Studio.</span><span class="sxs-lookup"><span data-stu-id="bd923-139">Run the application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="bd923-140">Nell'app per Android immettere un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="bd923-140">In the Android app, enter a username and password.</span></span> <span data-ttu-id="bd923-141">Devono avere lo stesso valore di stringa e non devono contenere spazi o caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="bd923-141">They must both be the same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="bd923-142">Nell'app per Android fare clic su **Log in**.</span><span class="sxs-lookup"><span data-stu-id="bd923-142">In the Android app, click **Log in**.</span></span> <span data-ttu-id="bd923-143">Attendere un avviso popup che indica **Logged in and registered**.</span><span class="sxs-lookup"><span data-stu-id="bd923-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="bd923-144">Verrà abilitato il pulsante **Send Notification** .</span><span class="sxs-lookup"><span data-stu-id="bd923-144">This will enable the **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="bd923-145">Fare clic sugli interruttori per abilitare tutte le piattaforme in cui è stata eseguita l'app ed è stato registrato un utente.</span><span class="sxs-lookup"><span data-stu-id="bd923-145">Click the toggle buttons to enable all platforms where you have ran the app and registered a user.</span></span>
5. <span data-ttu-id="bd923-146">Immettere il nome dell'utente che riceverà il messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="bd923-146">Enter the user's name that will receive the notification message.</span></span> <span data-ttu-id="bd923-147">L'utente dovrà essere registrato per le notifiche nei dispositivi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bd923-147">That user must be registered for notifications on the target devices.</span></span>
6. <span data-ttu-id="bd923-148">Immettere un messaggio che l'utente riceverà come messaggio di notifica push.</span><span class="sxs-lookup"><span data-stu-id="bd923-148">Enter a message for the user to receive as a push notification message.</span></span>
7. <span data-ttu-id="bd923-149">Fare clic su **Send Notification**.</span><span class="sxs-lookup"><span data-stu-id="bd923-149">Click **Send Notification**.</span></span>  <span data-ttu-id="bd923-150">Ogni dispositivo che ha una registrazione con il tag username corrispondente riceverà la notifica push.</span><span class="sxs-lookup"><span data-stu-id="bd923-150">Each device that has a registration with the matching username tag will receive the push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
