---
title: aaaHow tooenable SSO tra app in iOS usando ADAL | Documenti Microsoft
description: "Come funzionalità hello toouse di hello tooenable SDK ADAL Single Sign-On tra le applicazioni. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a>Come tooenable SSO tra app in iOS usando ADAL
Fornendo Single Sign-On (SSO) in modo che gli utenti solo tooenter le proprie credenziali una sola volta e le credenziali di lavoro automaticamente tutte le applicazioni è previsto dai clienti. immissione di nome utente e password su schermi di piccole dimensioni, spesso volte combinate con un fattore aggiuntivo (2FA), ad esempio una telefonata o un codice via SMS, la difficoltà di Hello risultati in rapida insoddisfazione dei clienti se un utente ha toodo più di una volta per il prodotto.

Inoltre, se si applica una piattaforma di identità che altre applicazioni possono utilizzare, ad esempio Accounts Microsoft o un account aziendale da Office 365, i clienti prevedere che toouse disponibili di toobe tali credenziali in tutte le proprie applicazioni indipendentemente dal fornitore hello.

Hello piattaforma Microsoft Identity, con il SDK di identità di Microsoft, funziona disco rigido per l'utente e fornisce capacità toodelight hello i clienti con SSO sia nel proprio gruppo di applicazioni o, come con le funzionalità di Service broker e un autenticatore applicazioni, attraverso intero dispositivo hello.

Questa procedura dettagliata verrà specificato come tooconfigure Windows SDK all'interno di tooprovide l'applicazione ai clienti tooyour questo vantaggio.

Questa procedura si applica a:

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Accesso condizionale di Azure Active Directory

documento Hello precedente presuppone che si conosca come troppo[provisioning delle applicazioni nel portale di hello legacy per Azure Active Directory](active-directory-how-to-integrate.md) e l'applicazione integrata con hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Concetti di SSO nella piattaforma delle identità Microsoft hello
### <a name="microsoft-identity-brokers"></a>Broker di Microsoft Identity
Microsoft fornisce le applicazioni per ogni piattaforma per dispositivi mobili che consentono il bridging delle credenziali tra le applicazioni di fornitori diversi hello e consente a particolari funzionalità avanzate che richiedono un'unica posizione sicura da cui toovalidate credenziali. Queste applicazioni sono dette **broker**. In iOS e Android tali gestori vengono forniti tramite applicazioni scaricabile che i clienti installare in modo indipendente o possono essere inseriti toohello dispositivo da una società che gestisce alcuni o tutti i dispositivi hello per i relativi dipendenti. Questi gestori supportano la sicurezza di gestione solo per alcune applicazioni o l'intero dispositivo hello in base a ciò che gli amministratori IT desiderano. In Windows, questa funzionalità è fornita dalla selezione account incorporato nel sistema operativo toohello, tecnicamente detto hello Broker di autenticazione Web.

Per ulteriori informazioni su come vengono utilizzati questi intermediari e come i clienti potrebbero visualizzarli nel flusso di accesso per piattaforma di Microsoft Identity hello leggere.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>Modelli di accesso dai dispositivi mobili
Accesso toocredentials nei dispositivi seguire due modelli di base per la piattaforma di Microsoft Identity hello:

* Accessi non assistiti da broker
* Accessi assistiti da broker

#### <a name="non-broker-assisted-logins"></a>Accessi non assistiti da broker
Account di accesso non broker assistito sono esperienze di accesso eseguite inline con un'applicazione hello e utilizzano l'archiviazione locale di hello sul dispositivo hello per tale applicazione. Questa risorsa di archiviazione può essere condivisi tra le applicazioni, ma le credenziali di hello sono strettamente associati toohello app o un gruppo di applicazioni utilizzando credenziali. Molto probabile che hai verificato in molte applicazioni per dispositivi mobili quando si immette un nome utente e una password all'interno di un'applicazione hello stesso.

Questi account hanno hello seguenti vantaggi:

* Esperienza utente esiste completamente all'interno di un'applicazione hello.
* Le credenziali possono essere condivise tra le applicazioni firmate da hello stesso certificato, che fornisce una suite di tooyour esperienza single sign-on di applicazioni.
* Controllo intorno esperienza hello della procedura di accesso viene fornito l'applicazione toohello prima e dopo l'accesso.

Questi account hanno hello seguenti svantaggi:

* L'utente non può eseguire il Single Sign-On per tutte le app che usano un'identità Microsoft, ma solo per le identità Microsoft configurate dall'applicazione.
* L'applicazione non può essere utilizzata con funzionalità più avanzate di business, ad esempio l'accesso condizionale o utilizzare hello InTune famiglia di prodotti.
* L'applicazione non supporta l'autenticazione basata su certificati per gli utenti aziendali.

Ecco una rappresentazione del funzionamento con archiviazione condivisa hello del tooenable applicazioni SSO hello identità SDK:

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>Accessi assistiti da broker
Gli account di accesso assistita da Service Broker sono esperienze di accesso che si verificano all'interno di un'applicazione hello broker e utilizzare hello archiviazione e la protezione delle credenziali di hello broker tooshare a tutte le applicazioni sul dispositivo hello applicabili alla piattaforma di Microsoft Identity hello. Ciò significa che le applicazioni utilizzano hello broker toosign gli utenti. In iOS e Android tali gestori vengono forniti tramite applicazioni scaricabile che i clienti installare in modo indipendente o possono essere inseriti toohello dispositivo da una società che gestisce il dispositivo di hello per utente. Un esempio di questo tipo di applicazione è un'applicazione Microsoft Authenticator hello in iOS. In Windows, questa funzionalità è fornita dalla selezione account incorporato nel sistema operativo toohello, tecnicamente detto hello Broker di autenticazione Web.
esperienza Hello varia in base alla piattaforma e a volte può risultare problematica toousers se non è gestita correttamente. Si è probabilmente più familiarità con questo modello se è installata l'applicazione di Facebook hello e si usa Facebook Connect da un'altra applicazione. Hello utilizza piattaforma Microsoft Identity hello stesso modello.

Per iOS in tal modo animazione "transizione" tooa in cui l'applicazione viene inviato background toohello mentre le applicazioni Microsoft Authenticator hello provengono in primo piano toohello per hello utente tooselect account con cui desiderano ricevere toosign con.  

Per Android e Windows account hello selezione viene visualizzato all'interno dell'applicazione dell'utente toohello meno problematica.

#### <a name="how-hello-broker-gets-invoked"></a>La modalità in cui viene richiamato il broker hello
Se è installato un broker compatibile hello dispositivo come applicazione di Microsoft Authenticator, hello identità SDK hello verrà automaticamente hello lavoro richiamare broker hello automaticamente quando un utente indica che desiderano toolog con qualsiasi account da piattaforma di Microsoft Identity Hello. Potrebbe trattarsi di un account Microsoft personale, di un account aziendale o dell'istituto di istruzione o di un account dato e ospitato in Azure con i prodotti B2C e B2B. 

 #### <a name="how-we-ensure-hello-application-is-valid"></a>Come è possibile garantire un'applicazione hello è valido
 
 identità del Hello necessità tooensure hello di broker di hello chiamata di un'applicazione è fondamentale toohello sicurezza che forniamo nell'account di accesso di Service broker assistito. IOS né Android applica gli identificatori univoci che sono validi solo per una determinata applicazione, in modo che applicazioni dannose potrebbero lo "spoofing" identificatore dell'applicazione legittimo e ricevere i token hello destinati a un'applicazione hello legittimi. tooensure che Microsoft segnala sempre con un'applicazione hello corretto in fase di esecuzione, chiediamo hello developer tooprovide un redirectURI personalizzato quando si registra l'applicazione con Microsoft. **Le modalità di creazione dell'URI di reindirizzamento da parte degli sviluppatori vengono trattate in dettaglio di seguito.** Questo valore di redirectURI personalizzato contiene hello ID Bundle dell'applicazione hello ed è garantita l'applicazione univoco toohello toobe da hello Apple App Store. Quando un gestore di hello chiamate applicazione broker hello richiede iOS hello tooprovide sistema operativo hello con ID di pacchetto che ha chiamato broker hello. broker Hello fornisce tooMicrosoft questo ID Bundle nel sistema di identità tooour chiamata hello. ID Bundle dell'applicazione hello hello non corrisponde a hello che ID Bundle fornito toous dallo sviluppatore hello durante la registrazione, si consentirà l'accesso toohello token per un'applicazione hello risorse hello richiede. Tale controllo garantisce che solo un'applicazione hello registrata dallo sviluppatore hello riceve i token.

**sviluppatore di Hello ha scelta hello del se hello Microsoft Identity SDK chiama broker hello o utilizza hello non broker assistito flusso.** Tuttavia se hello scelto non toouse hello assistito broker flusso perdono hello vantaggio derivante dall'utilizzo delle credenziali SSO utente hello potrà avere già aggiunto al dispositivo hello e impedisce loro applicazione in uso con le funzionalità di business Microsoft Fornisce i clienti, ad esempio l'accesso condizionale, funzionalità di gestione di Intune e l'autenticazione basata su certificato.

Questi account hanno hello seguenti vantaggi:

* Utente di cui si verifichi SSO per tutte le loro applicazioni indipendentemente dal fornitore hello.
* L'applicazione può utilizzare funzionalità più avanzate di business, ad esempio l'accesso condizionale o usare hello InTune suite di prodotti.
* L'applicazione può supportare l'autenticazione basata su certificati per gli utenti aziendali.
* Accedi molto più sicuro di riscontrare identità hello dell'applicazione hello e dell'utente hello vengono verificate dall'applicazione di Service broker hello con gli algoritmi di sicurezza aggiuntivo e la crittografia.

Questi account hanno hello seguenti svantaggi:

* In iOS utente hello viene eseguita la transizione dall'esperienza dell'applicazione mentre si scelgono le credenziali.
* Perdita di account di accesso di hello possibilità toomanage hello esperienza per i clienti all'interno dell'applicazione.

Ecco una rappresentazione di come utilizzare Microsoft Identity SDK hello hello broker tooenable applicazioni SSO:

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+
```

Grazie a queste informazioni di base deve essere toobetter in grado di comprendere e implementare SSO all'interno dell'applicazione utilizzando una piattaforma di Microsoft Identity hello e SDK.

## <a name="enabling-cross-app-sso-using-adal"></a>Abilitazione di SSO tra app tramite ADAL
In questo caso si usa hello ADAL iOS SDK per:

* Attivare SSO non assistito da broker per la suite di app
* Attivare il supporto per SSO assistito da broker

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Attivazione dell'SSO per l'SSO non assistito da broker
Per tutte le applicazioni di accesso non broker SSO assistito hello identità SDK gestisce gran parte delle complessità hello di SSO. Ciò include l'individuazione utente hello nella cache di hello e la gestione di un elenco di utenti ha effettuato l'accesso è tooquery.

tooenable SSO tutte le applicazioni che si è proprietari che è necessario hello toodo seguenti:

1. Verificare che tutte le hello di utente le applicazioni stesso Client o applicazione ID.
2. Verificare che tutti i hello condivisione applicazioni la stessa firma del certificato di Apple in modo da poter condividere portachiavi
3. Richiesta hello stesso diritto keychain per ognuna delle applicazioni.
4. Informare hello identità SDK keychain condiviso hello che desideri toouse.

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Utilizzando lo stesso ID Client di hello / applicazione ID per tutte le applicazioni nel gruppo di applicazioni di hello
Per consentire tooknow piattaforma di Microsoft Identity hello che ne sia consentita tooshare token tra le applicazioni, ognuna delle applicazioni sarà necessario tooshare hello stesso Client o applicazione ID. Questo è l'identificatore hello tooyou fornito al momento della prima applicazione è stato registrato nel portale di hello.

Per comprendere come identificare diverse App toohello servizio Microsoft Identity se utilizza hello stesso ID applicazione. risposte Hello sono con hello **Redirect URIs**. Ogni applicazione può avere più URI di reindirizzamento registrato nel portale di onboarding hello. Ogni app della suite avrà un URI di reindirizzamento diverso. La situazione potrebbe essere simile alla seguente:

URI di reindirizzamento dell'app 1: `x-msauth-mytestiosapp://com.myapp.mytestapp`

URI di reindirizzamento dell'app 2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`

URI di reindirizzamento dell'app 3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`

....

Questi vengono nidificati sotto lo stesso ID client hello / ID dell'applicazione e ricercata hello in base a URI è restituire toous nella configurazione del SDK di reindirizzamento.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*Si noti che hello formato degli URI di reindirizzamento vengono spiegate di seguito. È possibile utilizzare qualsiasi URI di reindirizzamento a meno che non si desidera broker hello toosupport, nel qual caso è necessario simile hello precedente*

#### <a name="create-keychain-sharing-between-applications"></a>Creare la condivisione dei portachiavi tra le applicazioni
Abilitazione della condivisione di portachiavi esula hello in questo documento e coperto da Apple nel proprio documento [aggiunta di funzionalità](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html). È importante soprattutto di stabilire il toobe portachiavi chiamato desiderato e aggiungere tale funzionalità in tutte le applicazioni.

Quando si dispone dei diritti impostare correttamente la dovrebbe essere un file nella directory del progetto intitolata `entitlements.plist` che contiene un elemento che sembra hello seguenti:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

Dopo aver diritto portachiavi hello abilitato in ognuna delle applicazioni e si è pronti toouse SSO, informare hello Microsoft Identity SDK portachiavi utilizzando hello impostazione in seguito il `ADAuthenticationSettings` con hello seguente impostazione:

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> Quando si condivide un portachiavi tra le applicazioni qualsiasi applicazione può eliminare utenti o peggio eliminare tutti i token hello in tutta l'applicazione. Questo è particolarmente disastroso se si hanno applicazioni che si basano su hello token toodo operazioni in background. La condivisione a un portachiavi significa che è necessario prestare particolare attenzione in tutte le rimuove operazioni tramite hello identità SDK.
> 
> 

L'operazione è terminata. Hello Microsoft Identity SDK ora condividono le credenziali in tutte le applicazioni. elenco di utenti Hello verrà inoltre essere condivisi tra le istanze dell'applicazione.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>Attivazione di SSO per SSO assistito da broker
consente a un'applicazione di toouse qualsiasi broker da cui è installato nel dispositivo hello è Hello **disattivata per impostazione predefinita**. Ordinare toouse l'applicazione con broker hello è necessario apportare alcune modifiche alla configurazione e aggiungere un'applicazione tooyour di codice.

Hello passaggi toofollow sono:

1. Abilitare la modalità di Service broker in toohello di chiamata del codice dell'applicazione SDK MS.
2. Stabilire un nuovo URI di reindirizzamento e fornire tooboth hello app e la registrazione dell'app.
3. Registrazione di uno schema URL.
4. Supporto iOS9: aggiungere un file Info. plist tooyour di autorizzazione.

#### <a name="step-1-enable-broker-mode-in-your-application"></a>Passaggio 1: Abilitare la modalità broker nell'applicazione
possibilità di Hello per il broker di hello toouse applicazione è attivata quando si crea la configurazione iniziale dell'oggetto di autenticazione o contesto"hello". A tal fine, impostare il tipo delle credenziali nel codice:

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
Hello `AD_CREDENTIALS_AUTO` impostazione consentirà hello Microsoft Identity SDK tootry toocall out broker toohello, `AD_CREDENTIALS_EMBEDDED` impedirà hello Microsoft Identity SDK dalla chiamata toohello broker.

#### <a name="step-2-registering-a-url-scheme"></a>Passaggio 2: Registrazione di uno schema URL
piattaforma di Microsoft Identity Hello Usa broker hello tooinvoke di URL e dell'applicazione tooyour indietro quindi la restituzione di controllo. toofinish di andata e ritorno è necessario uno schema URL registrato per l'applicazione che hello Microsoft Identity conoscenza della piattaforma. Questo può essere inoltre tooany altri schemi app potrebbe aver precedentemente registrato con l'applicazione.

> [!WARNING]
> È consigliabile apportare hello URL schema toominimize piuttosto univoco hello possibilità che un'altra app hello utilizzando lo stesso schema dell'URL. Apple non garantisce l'univocità hello degli schemi di URL registrati nell'archivio di app hello.
> 
> 

Ecco un esempio di come appare nella configurazione del progetto. È anche possibile usare XCode:

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a>Passaggio 3: Stabilire un nuovo URI di reindirizzamento con lo schema URL
In ordine tooensure che è sempre restituire credenziali hello token toohello corretta applicazione, è necessario toomake che è richiamata tooyour applicazione in modo da hello del sistema operativo iOS è possibile verificare. applicazioni di Service broker di Hello iOS del sistema operativo report toohello Microsoft hello ID Bundle dell'applicazione hello chiamata. di cui un'applicazione non autorizzata non può effettuare lo spoofing. Pertanto, è usato insieme a hello URI del nostro tooensure applicazione Service broker token hello vengono restituiti toohello corretta applicazione. È necessario è tooestablish questo reindirizzamento univoco sia nell'applicazione e set URI come URI di reindirizzamento nel nostro portale per sviluppatori.

L'URI di reindirizzamento deve essere nel formato corretto di hello di:

`<app-scheme>://<your.bundle.id>`

Ad esempio: *x-msauth-mytestiosapp://com.myapp.mytestapp*

Questo URI di reindirizzamento deve toobe specificato con la registrazione di app utilizzando hello [portale di Azure](https://portal.azure.com/). Per altre informazioni sulla registrazione di app Azure AD, vedere [Integrazione con Azure Active Directory](active-directory-how-to-integrate.md).

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a>Passaggio 3a: aggiungere un URI di reindirizzamento nell'autenticazione basata su certificati di portale toosupport app e sviluppo
autenticazione basata sul certificato toosupport secondo "msauth" deve toobe registrato nell'applicazione e hello [portale di Azure](https://portal.azure.com/) toohandle l'autenticazione del certificato se lo si desidera tooadd che supportano l'applicazione.

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

Ad esempio: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a>Passaggio 4: iOS9: aggiungere un'app tooyour parametro di configurazione
Libreria ADAL Usa – canOpenURL: toocheck se broker hello è installato nel dispositivo hello. In iOS 9 Apple ha bloccato gli schemi di cui un'applicazione può effettuare una query. Sarà necessario tooadd "msauth" toohello LSApplicationQueriesSchemes sezione il `info.plist file`.

<key>LSApplicationQueriesSchemes</key>

<array><string>msauth</string>
</array>

### <a name="youve-configured-sso"></a>L'SSO è stato configurato!
Ora hello SDK identità Microsoft verrà automaticamente sia condivide le credenziali tra le applicazioni e richiamare broker hello se è presente sul dispositivo.

