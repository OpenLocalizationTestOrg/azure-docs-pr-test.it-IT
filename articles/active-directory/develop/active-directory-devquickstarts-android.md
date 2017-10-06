---
title: aaaAzure AD Android introduzione | Documenti Microsoft
description: Come un'applicazione Android che si integra con Azure AD per l'accesso e le chiamate AD Azure toobuild protetto API tramite OAuth.
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Integrare Azure AD in un'app per Android
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Provare l'anteprima di hello delle nuove [portale per sviluppatori](https://identity.microsoft.com/Docs/Android), che consente di sfruttare in esecuzione in Azure AD in pochi minuti. portale per sviluppatori Hello assiste l'utente attraverso il processo di hello di registrazione di un'app e l'integrazione di Azure AD nel codice. Al termine si ottiene una semplice applicazione in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida.
>
>

Se si sta sviluppando un'applicazione desktop, Azure Active Directory (Azure AD) rende semplice e diretto per si tooauthenticate gli utenti con gli account di Active Directory locale. Consente inoltre l'applicazione toosecurely utilizzare qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.

Per i client Android che necessitano di risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library (ADAL). Hello unico scopo della libreria ADAL è toomake è più facile per i token di accesso tooget app. toodemonstrate facilmente, verrà creata un'applicazione Android elenco di attività che:

* Ottiene i token per chiamare un'API di elenco attività da eseguire tramite hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Ottiene l'elenco attività (To-Do List) dell'utente.
* Disconnette gli utenti.

tooget avviato, è necessario un tenant di Azure Active Directory in cui è possibile creare utenti e registrare un'applicazione. Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Passaggio 1: Scaricare ed eseguire i server di esempio hello TODO API REST di Node.js
esempio Node.js REST API TODO Hello viene scritto in modo specifico toowork contro l'esempio esistente per la creazione di un tenant singolo API REST di attività da eseguire per Azure AD. Questo è un prerequisito per l'avvio rapido hello.

Per informazioni su come tooset, vedere gli esempi esistenti in [servizio Microsoft Azure Active Directory esempio REST API per Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Passaggio 2: Registrare l'API Web con il tenant di Azure AD
Active Directory supporta l'aggiunta di due tipi di applicazioni:

- API che offrono servizi toousers Web
- Le API di applicazioni (in esecuzione sul web hello o in un dispositivo) che quelli di accesso web

In questo passaggio, si sta registrando l'API web hello in esecuzione in locale per test di questo esempio. L'API web è in genere, un servizio REST che è una funzionalità offerta che si desidera tooaccess un'app. Azure AD contribuisce alla protezione di qualsiasi endpoint.

Si presuppone che si sta registrando hello API REST di attività a cui fa riferimento in precedenza. Ma questo procedimento funziona per qualsiasi API web che si desidera proteggere toohelp Azure Active Directory.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account. In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. Immettere un nome descrittivo per l'applicazione hello (ad esempio, **TodoListService**), selezionare **applicazione Web e/o API Web**, fare clic su **Avanti**.
6. Per hello sign-on URL, immettere l'URL di base hello per esempio hello. Per impostazione predefinita, tale valore è `https://localhost:8080`.
7. Fare clic su **OK** registrazione hello toocomplete.
8. In hello portale di Azure, visitare tooyour pagina dell'applicazione, trovare il valore dell'ID applicazione hello e copiarlo. Servirà in un secondo momento durante la configurazione dell'applicazione.
9. Da hello **impostazioni** -> **proprietà** pagina, aggiornare l'URI ID app hello - immettere `https://<your_tenant_name>/TodoListService`. Sostituire `<your_tenant_name>` con nome hello del tenant di Azure AD.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Passaggio 3: Registrare un'applicazione hello esempio Android Native Client
È necessario registrare l'applicazione Web in questo esempio. In questo modo toocommunicate l'applicazione con l'API web appena registrato hello. Azure AD rifiuterà tooeven consentire tooask l'applicazione per l'accesso a meno che non è registrato. Che fa parte di sicurezza hello del modello di hello.

Si presuppone che si sta registrando l'applicazione di esempio hello citata in precedenza. ma questa procedura è applicabile a qualsiasi app in fase di sviluppo.

> [!NOTE]
> Si procede all'inserimento di un'applicazione e di un'API Web in un tenant, perché è possibile compilare un'app che accede a un'API esterna registrata in Azure AD da un altro tenant. In questo caso, i clienti sarà richiesto di utilizzare toohello tooconsent di hello API in un'applicazione hello. Active Directory Authentication Library per iOS gestisce automaticamente la richiesta di consenso. Esplorare le funzionalità più avanzate, si noterà che si tratta di una parte importante della suite di hello lavoro tooaccess necessari hello di APIs di Microsoft Azure e Office, nonché qualsiasi altro provider di servizio. Per il momento, perché è stato registrato l'API web sia l'applicazione sottoposta a hello stesso tenant, non verrà visualizzata alcuna richiesta di consenso dell'utente. Ciò avviene in genere hello se si sta sviluppando un'applicazione solo per toouse la propria società.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account. In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. Immettere un nome descrittivo per l'applicazione hello (ad esempio, **TodoListClient Android**), selezionare **applicazione Client nativa**, fare clic su **Avanti**.
6. URI di reindirizzamento hello, immettere `http://TodoListClient`. Fare clic su **Finish**.
7. Dalla pagina dell'applicazione hello, trovare il valore dell'ID applicazione hello e copiarlo. Servirà in un secondo momento durante la configurazione dell'applicazione.
8. Da hello **impostazioni** selezionare **autorizzazioni obbligatorie** e selezionare **Aggiungi**.  Individuare e selezionare TodoListService, aggiungere hello **accesso TodoListService** autorizzazione in **autorizzazioni delegate**, fare clic su **eseguita**.

toobuild con Maven, è possibile utilizzare pom.xml al primo livello hello:

1. Clonare il repository in una directory di propria scelta:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Seguire i passaggi hello hello [tooset prerequisiti dell'ambiente di Maven per Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Configurare l'emulatore hello con SDK 19.
4. Passare cartella radice toohello in cui è stato clonato repository hello.
5. Eseguire questo comando: `mvn clean install`
6. Modificare hello directory toohello avvio rapido-esempio:`cd samples\hello`
7. Eseguire questo comando: `mvn android:deploy android:run`

   Avvio dell'applicazione hello dovrebbe.
8. Immettere tootry le credenziali utente di test.

Verranno inviati pacchetti JAR accanto pacchetto AAR hello.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Passaggio 4: Scaricare Android ADAL hello e aggiungerlo come area di lavoro Eclipse tooyour
È stata semplificata per si toohave più opzioni toouse ADAL nel progetto Android:

* È possibile utilizzare questa libreria tooimport di codice sorgente hello in applicazione tooyour Eclipse e collegamento.
* Se si usa Android Studio, è possibile utilizzare hello AAR pacchetto formato e riferimento hello i file binari.

### <a name="option-1-source-zip"></a>Opzione 1: Zip del codice sorgente
Fare clic su una copia del codice sorgente hello, toodownload **ZIP di Download** hello destra della pagina hello. In alternativa, [eseguire il download da GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Opzione 2: Codice sorgente tramite Git
codice sorgente di hello tooget di hello SDK tramite Git, digitare:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Opzione 3: File binari tramite Gradle
È possibile ottenere i file binari hello dal repository centrale di Maven hello. pacchetto AAR Hello può essere inclusi come indicato di seguito nel progetto in Android Studio:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Opzione 4: AAR tramite Maven
Se si usa hello M2Eclipse plug-in, è possibile specificare una dipendenza hello nel file pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Opzione 5: Pacchetto JAR cartella di librerie hello
È possibile ottenere i file JAR hello dal repository di Maven hello e rilasciarlo hello **librerie** cartella nel progetto. Progetto tooyour di toocopy hello risorse necessarie, è necessario perché i pacchetti hello JAR non li includono.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Passaggio 5: Aggiungere progetti tooyour ADAL tooAndroid di riferimenti
1. Aggiungere un progetto di riferimento tooyour e specificarlo come una libreria Android. Se non si è sicuri come toodo, è possibile ottenere ulteriori informazioni su hello [sito Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Aggiungere una dipendenza di progetto hello per il debug nelle impostazioni del progetto.
3. Aggiornare tooinclude di file AndroidManifest.xml del progetto:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Creare un'istanza di AuthenticationContext nell'attività principale. Dettagli Hello di questa chiamata esulano dall'ambito di hello di questo argomento, ma è possibile ottenere un buon inizio esaminando hello [esempio Android Native Client](https://github.com/AzureADSamples/NativeClient-Android). Nell'esempio seguente di hello, SharedPreferences è cache predefinita hello e autorità è nel formato hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Copiare questo codice blocco toohandle hello fine AuthenticationActivity utente hello immette le credenziali e riceve un codice di autorizzazione:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask per un token, definire un callback:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Infine, richiedere il token usando il callback:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Di seguito è riportata una spiegazione dei parametri di hello:

* *risorsa* è obbligatorio e si sta tentando di tooaccess di risorse hello.
* *clientid* è obbligatorio e viene fornito da Azure AD.
* *RedirectUri* non è necessario toobe fornito per chiamata acquireToken hello. È possibile configurarlo come nome del pacchetto.
* *PromptBehavior* consente tooask per cache di hello tooskip credenziali e i cookie.
* *callback* viene chiamato dopo che il codice di autorizzazione hello verrà scambiato per un token. Ha un oggetto AuthenticationResult, che include un token di accesso, la data di scadenza e le informazioni sul token ID.
* *acquireTokenSilent* è facoltativo. È possibile chiamarlo toohandle la memorizzazione nella cache e l'aggiornamento del token. Fornisce inoltre la versione di sincronizzazione hello. Accetta *userId* come parametro.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Tramite questa procedura dettagliata, è necessario quali è necessario integrare con Azure Active Directory toosuccessfully. Per ulteriori esempi di questo utilizzo, visitare hello AzureADSamples / repository in GitHub.

## <a name="important-information"></a>Informazioni importanti
### <a name="customization"></a>Personalizzazione
Le risorse dell'applicazione possono sovrascrivere le risorse del progetto di libreria. Ciò si verifica durante la compilazione dell'app. Per questo motivo, è possibile personalizzare l'autenticazione attività layout hello desiderato. ID di hello tookeep assicurarsi di controlli hello che ADAL Usa (WebView).

### <a name="broker"></a>Gestore
app portale aziendale di Microsoft Intune Hello fornisce il componente di Service broker hello. Hello account viene creato in ad AccountManager. tipo di account di Hello è "workaccount". AccountManager consente solo un singolo account Single Sign-On (SSO). Crea un cookie SSO per utente hello dopo aver completato una sfida di dispositivo hello per una delle App hello.

Libreria ADAL Usa account di Service broker hello se viene creato un account utente in questo autenticatore e si sceglie di non tooskip è. È possibile ignorare l'utente di Service broker hello con:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

È necessario tooregister un RedirectUri speciali per l'utilizzo di Service broker. Valore di RedirectUri è nel formato hello `msauth://packagename/Base64UrlencodedSignature`. È possibile ottenere il valore di RedirectUri dell'App tramite brokerRedirectPrint.ps1 script hello o hello API chiamata mContext.getBrokerRedirectUri. firma di Hello è tooyour correlati i certificati di firma.

modello broker corrente Hello è per un utente. AuthenticationContext consente hello API metodo tooget hello broker.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

Il manifesto dell'applicazione deve avere autorizzazioni toouse ad AccountManager account seguente hello. Per informazioni dettagliate, vedere hello [ad AccountManager informazioni sul sito Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>URL dell'autorità e AD FS
Active Directory Federation Services (ADFS) non è riconosciuto come servizio token di sicurezza, di produzione, pertanto è necessario tooturn di individuazione di istanza e passare false nel costruttore AuthenticationContext hello.

URL dell'autorità Hello richiede un'istanza del servizio token di sicurezza e un [nome tenant](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Esecuzione di query sugli elementi della cache
ADAL fornisce una cache predefinita in SharedPrefrecens con alcune semplici funzioni di query nella cache. È possibile ottenere corrente cache di hello da AuthenticationContext utilizzando:

    ITokenCacheStore cache = mContext.getCache();

È anche possibile fornire l'implementazione della cache, se si desidera toocustomize è.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Comportamento della richiesta
ADAL fornisce un comportamento dell'opzione toospecify prompt dei comandi. Se non è valido il token di aggiornamento hello e sono necessarie le credenziali utente, PromptBehavior.Auto visualizzerà hello dell'interfaccia utente. PromptBehavior.Always ignorerà l'utilizzo della cache di hello e Mostra sempre hello dell'interfaccia utente.

### <a name="silent-token-request-from-cache-and-refresh"></a>Richiesta invisibile all'utente dei token dalla cache e aggiornamento
Una richiesta di token invisibile all'utente non usa hello popup dell'interfaccia utente e non richiede un'attività. Restituisce un token dalla cache di hello, se disponibile. Se il token di hello è scaduto, questo metodo tenta toorefresh è. Se il token di aggiornamento hello è scaduto o non è riuscito, viene restituito AuthenticationException.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Con questo metodo è anche possibile effettuare una chiamata di sincronizzazione. È possibile impostare toocallback null o usare acquireTokenSilentSync.

### <a name="diagnostics"></a>Diagnostica
Si tratta di fonti principali di hello di informazioni per la diagnosi dei problemi:

* Eccezioni
* Log
* Tracce di rete

Si noti che gli ID di correlazione sono diagnostica toohello centrale nella libreria hello. Se si desidera toocorrelate un ADAL richiesta con altre operazioni nel codice, è possibile impostare l'ID di correlazione in base a una richiesta. Se non si imposta un ID di correlazione, ADAL genererà un valore casuale. Tutti i messaggi di log e chiamate di rete verranno quindi contrassegnate con l'ID di correlazione hello. modifiche ID generate automaticamente Hello in ciascuna richiesta.

#### <a name="exceptions"></a>Eccezioni
Le eccezioni sono hello innanzitutto diagnostica. Si tenta di tooprovide utili messaggi di errore. ma se qualcuno non dovesse esserlo, registrare il problema e segnalarlo. Includere le informazioni relative al dispositivo, ad esempio modello e numero di SDK.

#### <a name="logs"></a>Log
È possibile configurare hello libreria toogenerate messaggi di log che è possibile utilizzare toohelp diagnosticare i problemi. Per configurare la registrazione, chiamata seguente hello tooconfigure un callback che ADAL utilizzerà toohand off ogni messaggio del log appena generato.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

I messaggi possono essere scritti tooa file di log personalizzato, come illustrato nel seguente codice hello. Non esiste purtroppo un metodo standard per ottenere i log da un dispositivo. A questo scopo, sono disponibili alcuni servizi che possono risultare utili. È anche possibile inventare personalizzati, ad esempio l'invio server tooa di file hello.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Questi sono i livelli di registrazione hello:
* Errore (eccezioni)
* Avviso (avviso)
* Info (a scopo informativo)
* Dettagliato (altri dettagli)

Impostare il livello di registrazione hello simile al seguente:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Tutti i messaggi di log vengono inviati toologcat, nei callback di log personalizzato tooany aggiunta.
È possibile ottenere un file di log tooa da logcat come indicato di seguito:

    adb logcat > "C:\logmsg\logfile.txt"

 Per informazioni dettagliate sui comandi adb, vedere hello [logcat informazioni sul sito Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Tracce di rete
È possibile utilizzare vari strumenti toocapture hello il traffico HTTP che genera l'errore ADAL.  Questo è particolarmente utile se si ha familiarità con il protocollo OAuth hello o se è necessario tooprovide informazioni di diagnostica tooMicrosoft o altri canali di supporto.

Fiddler è uno strumento traccia HTTP estremamente semplice hello. Seguente hello utilizzare collegamenti tooset, configurarlo toocorrectly record ADAL traffico di rete. Per uno strumento di traccia come Fiddler o Charles toobe utile, è necessario configurare il traffico SSL toorecord non crittografato.  

> [!NOTE]
> Le tracce generate in questo modo possono contenere informazioni con privilegi elevati, ad esempio token di accesso, nomi utente e password. Se si usano account di produzione, non condividere queste tracce con terze parti. Se è necessario toosupply toosomeone una traccia in supporto tooget ordine, riprodurre il problema di hello utilizzando un account temporaneo con nomi utente e password che si desidera condividere.

* Dal sito Web di Telerik hello: [impostazione backup Fiddler per Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* Vedere [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler) (Configurare le regole di Fiddler per ADAL) in GitHub

### <a name="dialog-mode"></a>Modalità della finestra di dialogo
metodo acquireToken Hello senza attività supporta un prompt dei comandi di finestra di dialogo.

### <a name="encryption"></a>Crittografia
ADAL crittografa i token hello e memorizzarlo in SharedPreferences per impostazione predefinita. È possibile esaminare i dettagli di hello toosee di hello StorageHelper classe. Android ha introdotto Android Keystore 4.3 (API 18) per l'archiviazione protetta delle chiavi private. ADAL lo usa per API 18 e versioni successive. Se si desidera toouse ADAL per le versioni precedenti di SDK, è necessario tooprovide una chiave segreta in AuthenticationSettings.INSTANCE.setSecretKey.

### <a name="oauth2-bearer-challenge"></a>Richiesta di connessione di OAuth2
classe AuthenticationParameters Hello fornisce funzionalità tooget authorization_uri da hello OAuth2 richiesta di connessione.

### <a name="session-cookies-in-webview"></a>Cookie di sessione in WebView
Android WebView non cancella i cookie di sessione si chiude l'applicazione hello. È possibile gestire questa operazione usando questo codice di esempio:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Per informazioni dettagliate sui cookie, vedere hello [CookieSyncManager informazioni sul sito Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Override delle risorse
libreria ADAL Hello include stringhe in inglese per i messaggi ProgressDialog. L'applicazione deve sovrascriverle, se si vogliono usare stringhe localizzate.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Finestra di dialogo NTLM
Versione di ADAL 1.1.0 supporta una finestra di dialogo NTLM che viene elaborata tramite l'evento onReceivedHttpAuthRequest hello da WebViewClient. È possibile personalizzare il layout di hello e stringhe per la finestra di dialogo hello.

### <a name="cross-app-sso"></a>Accesso Single Sign-On tra app
Informazioni su [come tooenable SSO tra app in Android tramite ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
