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
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Invio di notifiche push sicure con Hub di notifica di Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Panoramica
> [!IMPORTANT]
> toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Supporto di notifica push di Microsoft Azure consente tooaccess un'infrastruttura di messaggio push da usare, multipiattaforma e con scalabilità orizzontale, che semplifica notevolmente l'implementazione di hello delle notifiche push per applicazioni aziendali e per piattaforme per dispositivi mobili.

A causa di vincoli di sicurezza o tooregulatory, un'applicazione potrebbe talvolta tooinclude qualcosa nel notifica hello che non può essere trasmesso tramite l'infrastruttura di notifica push standard hello. In questa esercitazione viene descritto come tooachieve hello stessa esperienza inviando informazioni riservate tramite una connessione autenticata protetta tra i dispositivi Android di hello client e di back-end app hello.

In generale, il flusso di hello è il seguente:

1. Hello app back-end:
   * Archivia il payload sicuro nel database back-end.
   * Invia ID hello di questo dispositivo Android toohello notifica (viene inviata alcuna informazione protetta).
2. Hello app sul dispositivo hello, quando si riceve notifica hello:
   * dispositivo Android Hello contatta hello back-end richiedente hello sicura payload.
   * app Hello possono mostrare payload hello come una notifica sul dispositivo hello.

È importante in hello precedente del flusso e in questa esercitazione, si presuppone che il dispositivo hello toonote memorizza un token di autenticazione nel servizio di archiviazione locale, dopo hello utente effettua l'accesso. In questo modo si garantisce un'esperienza completamente trasparente, come dispositivo hello può recuperare i payload della notifica hello protetto con questo token. Se l'applicazione non archivia i token di autenticazione nel dispositivo hello o se i token possono scadere, hello dispositivo app, al momento della ricezione di notifiche push hello deve visualizzare una notifica generica richiesta hello utente toolaunch hello app. app Hello quindi esegue l'autenticazione utente hello e Mostra il payload di notifica di hello.

Questa esercitazione viene illustrato come le notifiche push toosend sicura. È basato su hello [notifica utenti](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) esercitazione, pertanto è necessario completare i passaggi di hello in tale esercitazione prima di tutto se hai già fatto.

> [!NOTE]
> In questa esercitazione si presuppone che l'utente abbia creato e configurato l'hub di notifica come descritto in [Introduzione ad Hub di notifica (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Modificare progetto Android hello
Ora che è stato modificato il hello solo toosend back-end di app *id* di una notifica push, aver toochange toohandle l'app Android di notifica e chiamare nuovamente il hello tooretrieve back-end protetta toobe messaggio visualizzato.
tooachieve questo obiettivo è verificare che l'app Android SA toomake come tooauthenticate stesso con il back-end quando riceve le notifiche push hello.

Si modificherà ora hello *accesso* flusso in ordine toosave hello autenticazione intestazione valore hello condivise le preferenze dell'app. Meccanismi analoghi possono essere utilizzati toostore qualsiasi token di autenticazione (ad esempio, i token OAuth) che hello app avrà toouse senza richiedere le credenziali dell'utente.

1. Nel progetto di app Android aggiungere hello seguenti costanti nella parte superiore di hello di hello **MainActivity** classe:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Ancora in hello **MainActivity** (classe), aggiornamento hello `getAuthorizationHeader()` hello toocontain metodo seguente codice:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Aggiungere il seguente hello `import` le istruzioni nella parte superiore di hello di hello **MainActivity** file:
   
        import android.content.SharedPreferences;

Verrà ora modificata gestore hello che viene chiamato quando viene ricevuta la notifica hello.

1. In hello **MyHandler** classe modificare hello `OnReceive()` toocontain metodo:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. Aggiungere quindi hello `retrieveNotification()` metodo, sostituendo il segnaposto hello `{back-end endpoint}` con endpoint di back-end hello ottenuto durante la distribuzione il back-end:
   
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

Questo metodo chiama la notifica hello tooretrieve back-end app contenuta utilizzando le credenziali di hello archiviate in hello condiviso preferenze e viene visualizzato sotto forma di una notifica normale. notifica Hello ricerca utente app toohello esattamente come qualsiasi altra notifica push.

Si noti che è preferibile toohandle casi di hello di proprietà di intestazione di autenticazione mancante o il rifiuto da hello back-end. gestione di specifica Hello di questi casi dipendono principalmente l'esperienza utente di destinazione. È una notifica con un messaggio generico per notifica effettivo di hello utente tooauthenticate tooretrieve hello toodisplay.

## <a name="run-hello-application"></a>Eseguire l'applicazione hello
toorun applicazione hello, hello seguenti:

1. Assicurarsi che il progetto **AppBackend** sia distribuito in Azure. Se si usa Visual Studio, eseguire hello **AppBackend** applicazione API Web. Verrà visualizzata una pagina Web ASP.NET.
2. In Eclipse, eseguire l'applicazione hello in un emulatore fisico hello o di dispositivi Android.
3. Nell'app Android hello dell'interfaccia utente, immettere un nome utente e password. Può trattarsi di qualsiasi stringa, ma devono essere hello stesso valore.
4. Nell'app Android hello dell'interfaccia utente, fare clic su **Accedi**. Fare clic su **Send push**.

