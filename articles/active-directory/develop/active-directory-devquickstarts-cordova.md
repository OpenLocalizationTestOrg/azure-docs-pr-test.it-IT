---
title: aaaAzure AD Cordova introduzione | Documenti Microsoft
description: Come toobuild un'applicazione Cordova che si integra con Azure AD per l'accesso e chiama le API di protetto AD Azure tramite OAuth.
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Integrare Azure AD con un'app Apache Cordova
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

È possibile utilizzare Apache Cordova toodevelop HTML5/JavaScript applicazioni eseguibili nei dispositivi mobili come applicazioni native complete. Con Azure Active Directory (Azure AD), è possibile aggiungere applicazioni di Cordova tooyour funzionalità autenticazione aziendale.

Un plug-in Cordova esegue il wrapping di SDK nativi di Azure AD in iOS, Android, Windows Store e Windows Phone. Utilizzando, plug-in, è possibile migliorare l'applicazione toosupport Accedi con account di Windows Server Active Directory degli utenti, ottenere accesso tooOffice 365 e API di Azure e anche proteggere chiamate tooyour proprio personalizzato API web.

In questa esercitazione si userà hello Apache Cordova plug-in per Active Directory Authentication Library (ADAL) tooimprove una semplice app aggiungendo hello seguenti caratteristiche:

* Sono sufficienti poche righe di codice per autenticare un utente e ottenere un token.
* Utilizzare tale tooquery di API Graph hello tooinvoke token tale directory e visualizzare i risultati di hello.  
* Utilizzare l'autenticazione ADAL cache dei token di hello toominimize richiesto per l'utente hello.

toomake questi miglioramenti, è necessario:

1. Registrare un'applicazione con Azure AD.
2. Aggiungere codice tooyour app toorequest token.
3. Aggiungere codice toouse hello token per l'esecuzione di query hello API Graph e visualizzare i risultati.
4. Crea progetto di distribuzione Cordova hello con tutte le piattaforme hello si desidera tootarget, hello Cordova ADAL plug-in aggiungere e testare soluzioni hello in emulatori.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario:

* Tenant di Azure AD nel quale è disponibile un account con diritti per lo sviluppo di app.
* Un ambiente di sviluppo configurato toouse Apache Cordova.  

Se si dispone sia già configurato, procedere direttamente toostep 1.

Se non si dispone di un tenant di Azure AD, usare hello [istruzioni su come tooget uno](active-directory-howto-tenant.md).

Se non si dispone di Apache Cordova configurare nel computer, installare l'esempio hello:

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.JS](https://nodejs.org/download/)
* [Interfaccia della riga di comando di Cordova](https://cordova.apache.org/) (può essere installata facilmente tramite Gestione pacchetti NPM: `npm install -g cordova`)

Hello installazioni precedenti dovrebbe funzionare sia sui PC hello hello Mac.

Ogni piattaforma di destinazione ha prerequisiti diversi:

* toobuild ed eseguire un'app per PC o Tablet PC di Windows o Windows Phone:
  * Installare [Visual Studio 2013 per Windows con Update 2 o versione successiva](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express o altra versione) oppure [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild ed eseguire un'app per iOS:

  * Installare Xcode 6.x o versione successiva. Scaricarlo dal hello [sito per sviluppatori Apple](http://developer.apple.com/downloads) o hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Installare [ios-sim](https://www.npmjs.org/package/ios-sim). È possibile utilizzare le app iOS toostart nel simulatore iOS da riga di comando hello. (È possibile installare facilmente tramite terminal hello: `npm install -g ios-sim`.)
* toobuild ed eseguire un'app per Android:

  * Installare [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva. Assicurarsi che `JAVA_HOME` (variabile di ambiente) è impostato correttamente in base a percorso di installazione di JDK toohello (ad esempio, c:\Programmi\Microsoft Files\Java\jdk1.7.0_75).
  * Installare [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) e aggiungere hello `<android-sdk-location>\tools` tooyour percorso (ad esempio, C:\tools\Android\android-sdk\tools) `PATH` variabile di ambiente.
  * Apri Android SDK Manager (ad esempio, tramite terminal hello: `android`) e installare:
    * *Android 5.0.1 (API 21)* Platform SDK
    * *Android SDK Build Tools* 19.1.0 o versione successiva
    * *Android Support Repository* (funzionalità aggiuntive)

  Hello, Android SDK non fornisce a qualsiasi istanza dell'emulatore predefinito. Crearne una eseguendo `android avd` da terminal hello e quindi selezionando **crea**, se si desidera toorun app per Android hello in un emulatore. È consigliabile usare un' API di livello 19 o superiore. Per ulteriori informazioni sulle opzioni di creazione e l'emulatore Android hello, vedere [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) nel sito Android hello.

## <a name="step-1-register-an-application-with-azure-ad"></a>Passaggio 1: Registrare un'applicazione con Azure AD
Questo passaggio è facoltativo. In questa esercitazione vengono pre-provisioning di valori che è possibile utilizzare toosee hello esempio nell'azione senza effettuare alcun provisioning nel proprio tenant. Tuttavia, è consigliabile eseguire questo passaggio e acquisire familiarità con il processo di hello, perché sarà necessaria la creazione di applicazioni personalizzate.

Azure AD rilascia token tooonly noto di applicazioni. Prima di poter utilizzare Azure AD dall'app, è necessario toocreate una voce per tale nel tenant. tooregister una nuova applicazione nel tenant di:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra superiore hello, fare clic sull'account. In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.
3. Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.
4. Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.
5. Seguire le istruzioni di hello e creare un **applicazione Client nativa**. Benché le app Cordova siano basate su HTML, verrà creata un'applicazione client nativa. Hello **applicazione Client nativa** opzione deve essere selezionata o un'applicazione hello non funzionerà.)
  * **Nome** descrive toousers l'applicazione.
  * **URI di reindirizzamento** è hello URI utilizzato tooreturn token tooyour app. Immettere **http://MyDirectorySearcherApp**.

Dopo aver completato la registrazione, Azure AD le assegna un'app di tooyour ID applicazione univoco. È necessario che questo valore nelle sezioni successive di hello. È possibile trovarlo nella scheda applicazione hello di hello app appena creata.

toorun `DirSearchClient Sample`, concedere hello appena creato app autorizzazione tooquery hello Azure AD Graph API:

1. Da hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**.  
2. Per hello applicazione Azure Active Directory, selezionare **Microsoft Graph** come hello API e aggiungere hello **directory hello accesso come utente connesso di hello** autorizzazione in **delegati Autorizzazioni**.  In questo modo hello di tooquery l'applicazione API Graph per gli utenti.

## <a name="step-2-clone-hello-sample-app-repository"></a>Passaggio 2: Clonare il repository di app di esempio hello
La shell o la riga di comando, digitare hello comando seguente:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Passaggio 3: Creare app di Cordova hello
Esistono più modi toocreate Cordova applicazioni. In questa esercitazione verrà utilizzata l'interfaccia della riga di comando di Cordova hello (CLI).

1. La shell o la riga di comando, digitare hello comando seguente:

        cordova create DirSearchClient

   Tale comando Crea struttura di cartelle hello e lo scaffolding per progetto Cordova hello.

2. Spostare la nuova cartella di DirSearchClient toohello:

        cd .\DirSearchClient

3. Copiare il contenuto di hello del progetto di avvio hello nella sottocartella www hello tramite un gestore di file o hello comando nella shell seguente:

  * Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Aggiungere whitelist hello plug-in. Ciò è necessario per richiamare hello API Graph.

        cordova plugin add cordova-plugin-whitelist

5. Aggiungere tutte le piattaforme che si desidera toosupport hello. toohave un esempio funzionante, è necessario tooexecute almeno uno dei seguenti comandi hello. Si noti che non essere in grado di tooemulate iOS in Windows o di emulazione di Windows sul Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Aggiungere hello ADAL per progetto tooyour plug-in Cordova:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Passaggio 4: Aggiungere utenti tooauthenticate codice e ottenere i token da Azure AD
un'applicazione Hello sviluppata in questa esercitazione fornirà una funzionalità di ricerca di directory semplice. utente Hello, digitare l'alias di hello di qualsiasi utente nella directory hello e visualizzare alcuni attributi di base. progetto iniziale Hello contiene definizione hello dell'interfaccia utente di base hello dell'app di hello (in www/index.html) e lo scaffolding di hello che collega evento app di base di cicli, le associazioni dell'interfaccia utente e comporta la logica di visualizzazione (in www/js/index.js). Hello unica attività a sinistra per l'utente è tooadd hello logica che implementa l'attività di identità.

Hello innanzitutto, è necessario toodo nel codice è introdurre valori di protocollo hello Azure AD viene utilizzato per identificare l'app e hello risorse di destinazione. Questi valori sono le richieste di token hello tooconstruct utilizzati in un secondo momento. Inserire il seguente frammento di codice all'inizio di hello del file di index.js hello hello:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Hello `redirectUri` e `clientId` valori devono corrispondere i valori hello che descrivono l'app in Azure AD. È possibile trovarli da hello **configura** scheda hello portale di Azure, come descritto nel passaggio 1, più indietro in questa esercitazione.

> [!NOTE]
> Se si è scelto di non registra una nuova app nel proprio tenant, è possibile semplicemente incollare i valori hello preconfigurato come è. È quindi possibile visualizzare hello esempio in esecuzione, anche se è consigliabile creare sempre una voce personalizzata per le app che sono concepite per la produzione.

Successivamente, aggiungere il codice di richiesta di token hello. Inserisci hello seguente frammento di codice tra hello `search` e `renderData` definizioni:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Si esaminerà ora la funzione suddividendola nelle due parti principali.
In questo esempio è progettato toowork con un tenant, come toobeing anziché legata tooa uno. Usa hello endpoint "/ comuni", che consente a qualsiasi account hello utente tooenter al momento dell'autenticazione e indirizza il tenant di hello richiesta toohello cui appartiene.

La prima parte del metodo hello controlla hello cache ADAL toosee se un token è già archiviato. In questo caso, il metodo di hello Usa tenant hello token hello provenienza per reinizializzare ADAL. Ciò è necessario tooavoid prompt aggiuntivo, perché hello uso di "/ comuni" genera sempre porre hello utente tooenter un nuovo account.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
seconda parte di Hello del metodo hello esegue una richiesta di token corretto hello. Hello `acquireTokenSilentAsync` metodo chiede tooreturn ADAL un token specificato hello risorsa senza visualizzare alcun UX. Ciò può verificarsi se cache di hello dispone già di un token di accesso appropriato archiviato, o se un token di aggiornamento può essere utilizzato tooget un nuovo token di accesso senza che venga visualizzato un prompt dei comandi. Se il tentativo ha esito negativo, è il fallback `acquireTokenAsync`-che chiederà visibilmente tooauthenticate utente hello.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Ora che abbiamo token hello, è infine possibile richiamare l'API Graph hello e query di ricerca hello che si desidera eseguire. Inserisci hello seguente frammento di codice di sotto di hello `authenticate` definizione:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
file punto di partenza Hello fornire un'esperienza utente semplice per l'immissione di un alias utente in una casella di testo. Questo metodo utilizza tale valore tooconstruct una query, combinarla con il token di accesso di hello, inviarlo tooMicrosoft grafico e analizzare i risultati di hello. Hello `renderData` (metodo), già presente nel file di punto di partenza hello, si occupa della visualizzazione dei risultati di hello.

## <a name="step-5-run-hello-app"></a>Passaggio 5: Eseguire l'applicazione hello
L'app è toorun pronto. Il funzionamento è semplice: quando viene avviata l'applicazione hello, immettere l'alias dell'utente hello si desidera ripristinare toolook hello e quindi fare clic su pulsante hello. Viene richiesto di autenticarsi. Dopo l'autenticazione e la ricerca ha esito positivo, vengono visualizzati gli attributi di hello di hello ricercata utente.

Le esecuzioni successive verranno eseguite hello ricerca senza visualizzare alcun messaggio, grazie toohello presenza di hello precedentemente acquisito token nella cache.

Hello passaggi concreto per l'esecuzione di app hello variano a seconda della piattaforma.

### <a name="windows-10"></a>Windows 10
   Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`

   Dispositivi mobili (richiede un tooa di dispositivo connesso PC Windows 10 Mobile):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Durante la prima esecuzione di hello, potrebbe essere richiesto toosign in per una licenza per sviluppatori. Per altre informazioni, vedere [Licenza per sviluppatori](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Tablet/PC con Windows 8.1
   `cordova run windows`

   > [!NOTE]
   > Durante la prima esecuzione di hello, potrebbe essere richiesto toosign in per una licenza per sviluppatori. Per altre informazioni, vedere [Licenza per sviluppatori](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8.1
   toorun in un dispositivo collegato:`cordova run windows --device -- --phone`

   toorun sull'emulatore predefinito hello:`cordova emulate windows -- --phone`

   Utilizzare `cordova run windows --list -- --phone` toosee tutte le destinazioni disponibili e `cordova run windows --target=<target_name> -- --phone` toorun un'applicazione hello in un emulatore o un dispositivo specifico (ad esempio, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun in un dispositivo collegato:`cordova run android --device`

   toorun sull'emulatore predefinito hello:`cordova emulate android`

   Assicurarsi di che aver creato un'istanza dell'emulatore con AVD Manager, come descritto in precedenza nella sezione "Prerequisiti" hello.

   Utilizzare `cordova run android --list` toosee tutte le destinazioni disponibili e `cordova run android --target=<target_name>` toorun un'applicazione hello in un emulatore o un dispositivo specifico (ad esempio, `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun in un dispositivo collegato:`cordova run ios --device`

   toorun sull'emulatore predefinito hello:`cordova emulate ios`

   > [!NOTE]
   > Assicurarsi di avere hello `ios-sim` toorun pacchetto installato in un emulatore hello. Per ulteriori informazioni, vedere la sezione Prerequisiti"hello" sezione.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Passaggi successivi
Per riferimento, è disponibile in: esempio hello completata (senza i valori di configurazione) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

È possibile ora gli scenari di spostamento in toomore avanzate (e più interessante). Potrebbe essere necessario tootry: [proteggere un'API Web Node. js con Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
