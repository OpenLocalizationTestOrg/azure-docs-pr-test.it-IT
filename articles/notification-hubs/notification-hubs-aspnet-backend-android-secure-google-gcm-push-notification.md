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
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Invio di notifiche push sicure con Hub di notifica di Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
> [!IMPORTANT]
> Per completare l'esercitazione, è necessario disporre di un account Azure attivo. Se non si dispone di un account Azure, è possibile creare un account di valutazione gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Il supporto per le notifiche push in Microsoft Azure consente di accedere a un'infrastruttura di messaggistica push di facile utilizzo, multipiattaforma con scalabilità orizzontale, che semplifica considerevolmente l'implementazione delle notifiche push sia per le applicazioni consumer sia per quelle aziendali per piattaforme mobili.

A causa di vincoli normativi o di sicurezza, un'applicazione potrebbe talvolta includere nella notifica informazioni che non è possibile trasmettere attraverso l'infrastruttura di notifiche push standard. Questa esercitazione descrive come conseguire la stessa esperienza inviando informazioni sensibili attraverso una connessione autenticata e sicura tra il dispositivo client Android e il back-end dell'app.

A livello generale, il flusso è il seguente:

1. Il back-end dell'app:
   * Archivia il payload sicuro nel database back-end.
   * Invia l'ID di questa notifica al dispositivo Android (non vengono inviate informazioni sicure).
2. L'app sul dispositivo, quando riceve la notifica:
   * Il dispositivo Android contatta il back-end richiedendo il payload sicuro.
   * L'app può indicare il payload come una notifica sul dispositivo.

È importante notare che nel flusso precedente e in questa esercitazione si presuppone che il dispositivo archivi un token di autenticazione nella memoria locale, dopo l’accesso dell'utente. Ciò garantisce un'esperienza completamente lineare, in quanto il dispositivo può recuperare il payload sicuro della notifica tramite questo token. Se invece l'applicazione non archivia i token di autenticazione nel dispositivo o se questi hanno una scadenza, l'app per dispositivo, alla ricezione della notifica push, dovrà visualizzare una notifica generica in cui si richiede all'utente di avviare l'app. L'app autentica quindi l'utente e mostra il payload di notifica.

Questa esercitazione descrive come inviare notifiche push sicure. Poiché i passaggi descritti in questa esercitazione si basano su quella relativa all' [invio di notifiche agli utenti](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) , sarà prima necessario completare i passaggi di quest'ultima.

> [!NOTE]
> In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a>Modificare il progetto Android
Ora che è stato modificato il back-end dell'app in modo da inviare solo l' *ID* di una notifica push, è necessario modificare l'app per Android in modo da gestire tale notifica e richiamare il back-end per recuperare il messaggio sicuro da visualizzare.
Per conseguire questo obiettivo, è necessario assicurarsi che l'app per Android sia in grado di eseguire l'autenticazione con il back-end quando riceve le notifiche push.

Ora si modificherà il flusso di *accesso* per salvare il valore dell'intestazione di autenticazione nelle preferenze condivise dell'app. Un meccanismo analogo può essere usato per archiviare eventuali token di autenticazione (ad esempio token OAuth) che l'app dovrà usare senza richiedere le credenziali dell'utente.

1. Nel progetto di app per Android, aggiungere le costanti seguenti all'inizio della classe **MainActivity** :
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Sempre nella classe **MainActivity** aggiornare il metodo `getAuthorizationHeader()` per includere il codice seguente:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Aggiungere le seguenti istruzioni `import` all'inizio del file **MainActivity** :
   
        import android.content.SharedPreferences;

A questo punto, modificare il gestore chiamato quando si riceve la notifica.

1. Nella classe **MyHandler** modificare il metodo `OnReceive()` in modo che contenga:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Aggiungere quindi il metodo `retrieveNotification()`, sostituendo il segnaposto `{back-end endpoint}` con l'endpoint del back-end ottenuto durante la distribuzione del back-end:
   
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

Questo metodo chiama il back-end dell'app per recuperare il contenuto della notifica usando le credenziali memorizzate nelle preferenze condivise e lo visualizza come una normale notifica. L'utente dell'app vedrà la notifica esattamente come qualsiasi altra notifica push.

Notare che è preferibile gestire i casi in cui manca la proprietà dell'intestazione di autenticazione o di rifiuto da parte del back-end. La gestione specifica di questi casi dipende in larga misura dall'esperienza dell'utente di destinazione. Una delle opzioni consiste nel visualizzare una notifica con un prompt generico affinché l'utente possa autenticarsi per recuperare la notifica effettiva.

## <a name="run-the-application"></a>Eseguire l'applicazione
Per eseguire l'applicazione, eseguire le operazioni seguenti:

1. Assicurarsi che il progetto **AppBackend** sia distribuito in Azure. Se si usa Visual Studio, eseguire l'applicazione API Web **AppBackend** . Verrà visualizzata una pagina Web ASP.NET.
2. In Eclipse eseguire l'app su un dispositivo Android fisico o sull'emulatore.
3. Nell'interfaccia utente dell'app per Android immettere un nome utente e una password. Può trattarsi di qualsiasi stringa, ma devono avere lo stesso valore.
4. Nell'interfaccia utente dell'app per Android fare clic su **Log in**. Fare clic su **Send push**.

