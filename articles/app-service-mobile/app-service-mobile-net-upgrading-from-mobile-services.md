---
title: aaaUpgrade da servizi mobili tooAzure servizio App
description: Informazioni su come tooeasily l'aggiornamento del tooan di applicazione di servizi mobili App del servizio Mobile App
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Aggiornare il tooApp servizio Mobile di Azure .NET esistenti del servizio
Servizio App per dispositivi mobili sono un nuovo modo toobuild applicazioni per dispositivi mobili con Microsoft Azure. vedere, più toolearn [quali sono App per dispositivi mobili?].

Questo argomento viene descritto come un'applicazione back-end .NET esistente da servizi mobili di Azure tooa tooupgrade nuova App per dispositivi mobili del servizio App. Durante l'esecuzione di questo aggiornamento, l'applicazione di servizi mobili esistente possa continuare toooperate.   Se è necessario tooupgrade un'applicazione back-end di Node.js, vedere troppo[l'aggiornamento dei servizi mobili di Node.js](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Quando un back-end mobile è aggiornato tooAzure servizio App, ha accesso tooall le funzionalità del servizio App e vengono fatturate in base troppo[servizio App prezzi], non sui prezzi di servizi mobili.

## <a name="migrate-vs-upgrade"></a>Eseguire la migrazione o aggiornare
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Prima di procedere a un aggiornamento, è consigliabile [eseguire una migrazione](app-service-mobile-migrating-from-mobile-services.md) . In questo modo, è possibile inserire entrambe le versioni dell'applicazione hello piano di servizio App stesso e non comportare senza alcun costo aggiuntivo.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Miglioramenti dell’SDK del server .NET di App per dispositivi mobili
L'aggiornamento toohello nuova [Mobile App SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) fornisce hello seguenti vantaggi:

* Maggiore flessibilità alle dipendenze di NuGet. Hello ambiente di hosting non fornisce le versioni dei pacchetti NuGet, pertanto è possibile utilizzare le versioni compatibili alternative. Tuttavia, se sono presenti nuovi bugfixes critici o toohello gli aggiornamenti di sicurezza Mobile Server SDK o le dipendenze, è necessario aggiornare il servizio manualmente.
* Una maggiore flessibilità nella hello SDK per dispositivi mobili. È possibile controllare in modo esplicito le funzioni e le route vengono impostate, ad esempio l'autenticazione, tabella, API e hello push endpoint di registrazione. vedere, più toolearn [come toouse hello server .NET SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Supporto per altri tipi di progetto ASP.NET e route. È ora possibile ospitare controller MVC e Web API hello stesso progetto come progetto di back-end per dispositivi mobili.
* Supporto per le nuove funzionalità di autenticazione del servizio App, che consentono una configurazione di autenticazione comune toouse attraverso il web e App per dispositivi mobili.

## <a name="overview"></a>Panoramica sull'aggiornamento di base
In molti casi, l'aggiornamento sarà semplice come cambio toohello nuova App per dispositivi mobili SDK server e la ripubblicazione, il codice in una nuova istanza di App per dispositivi mobili. Esistono, tuttavia, alcuni scenari che richiedono alcune configurazioni aggiuntive, ad esempio l'autenticazione avanzata e l'uso dei processi pianificati. Ognuno di questi è illustrato in hello sezioni in un secondo momento.

> [!TIP]
> Si consiglia di leggere e comprendere completamente rest hello di questo argomento prima di avviare un aggiornamento. Prendere nota delle funzionalità usate che sono indicate di seguito.
>
>

il client di servizi mobili di Hello SDK sono **non** compatibile con il server di App per dispositivi mobili nuovi hello SDK. In ordine tooprovide la continuità del servizio per l'app, non è possibile pubblicare il sito di tooa modifiche attualmente rispondendo alle richieste client pubblicato. È invece necessario creare una nuova app per dispositivi mobili che agisce da duplicato. È possibile inserire l'applicazione hello stesso servizio App piano tooavoid incorrere in costi finanziari aggiuntivi.

Sarà quindi possibile due versioni di un'applicazione hello: uno che rimane hello stesso e serve le app pubblicate in hello wild e hello altro che è quindi possibile eseguire l'aggiornamento e destinazione con una nuova versione di client. È possibile spostare e testare il codice le esigenze, ma è necessario assicurarsi che tutte le correzioni di bug apportate ottenere tooboth applicato. Quando si ritiene che un numero desiderato di App client in hello wild have aggiornato la versione più recente di toohello, è possibile eliminare l'applicazione migrata originale hello se lo si desidera.

Hello completo per il processo di aggiornamento hello è come segue:

1. Creare una nuova app per dispositivi mobili
2. Aggiornamento hello progetto toouse hello nuovi Server SDK
3. Rilasciare una nuova versione dell'applicazione client
4. (Facoltativo) Eliminare l'istanza migrata originale

## <a name="mobile-app-version"></a>Creazione di una seconda istanza dell'applicazione
Hello innanzitutto l'aggiornamento è toocreate hello App Mobile risorsa che ospiterà una nuova versione di hello dell'applicazione. Se si è già eseguita la migrazione di un servizio mobile esistente, è opportuno toocreate questa versione di hello stesso piano di hosting. Aprire hello [portale di Azure] e passare tooyour eseguita la migrazione dell'applicazione. Prendere nota del piano di servizio App è in esecuzione su hello.

Successivamente, creare seconda istanza di applicazione hello hello seguente [istruzioni di creazione di back-end .NET](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Quando richiesto tooselect piano di servizio App "piano di hosting" sceglie hello piano dell'applicazione migrata.

Probabilmente si desidererà toouse hello stesso database e Hub di notifica come è stato in servizi mobili. È possibile copiare questi valori aprendo [portale di Azure] navigazione toohello di applicazione originale, quindi fare clic su **impostazioni** > **le impostazioni dell'applicazione**. In **Stringhe di connessione** copiare `MS_NotificationHubConnectionString` e `MS_TableConnectionString`. Passare tooyour nuovo aggiornamento del sito e li incolliamo in, sovrascrivendo i valori esistenti. Ripetere questo processo per tutte le altre impostazioni dell'applicazione necessarie per l'app. Se non si utilizza un servizio migrato, è possibile leggere le stringhe di connessione e le impostazioni dell'app da hello **configura** scheda della sezione Servizi mobili di hello hello [portale di Azure classico].

Creare una copia del progetto ASP.NET hello per l'applicazione e pubblicarlo tooyour nuovo sito. Utilizzando una copia dell'applicazione client aggiornata con nuovo URL hello, verificare che tutto funzioni come previsto.

## <a name="updating-hello-server-project"></a>Aggiornamento di project server hello
Fornisce una nuova App per dispositivi mobili [Mobile App Server SDK] che fornisce gran parte di hello stessa funzionalità di runtime di servizi mobili hello. In primo luogo, è necessario rimuovere tutti i pacchetti di servizi mobili toohello riferimenti. In Gestione pacchetti NuGet di hello, cercare `WindowsAzure.MobileServices.Backend`. Per la maggior parte delle app saranno presenti diversi pacchetti, tra cui `WindowsAzure.MobileServices.Backend.Tables` e `WindowsAzure.MobileServices.Backend.Entity`. In tal caso, iniziare con il pacchetto più basso di hello nell'albero delle dipendenze di hello, ad esempio `Entity`e rimuoverlo. Quando richiesto, non rimuovere tutti i pacchetti dipendenti. Ripetere questo processo finché non è stato rimosso `WindowsAzure.MobileServices.Backend` stesso.

A questo punto si avrà un progetto che non fa più riferimento agli SDK di Servizi mobili.

Si aggiungeranno quindi riferimenti hello Mobile App SDK. Per questo aggiornamento, la maggior parte degli sviluppatori verranno toodownload e installare hello `Microsoft.Azure.Mobile.Server.Quickstart` del pacchetto, come si effettuerà il pull nel set necessarie intera hello.

Saranno presenti alcuni errori del compilatore derivanti dalle differenze esistenti tra hello SDK, ma questi sono tooaddress semplice e vengono trattati nel resto di hello di questa sezione.

### <a name="base-configuration"></a>Configurazione di base
In WebApiConfig.cs è quindi possibile sostituire:

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

con

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Se si desidera toolearn ulteriori informazioni su hello nuovo .NET SDK e come tooadd/Rimuovi funzionalità server dall'app, vedere hello [come toouse hello server .NET SDK] argomento.
>
>

Se l'app Usa le funzionalità di autenticazione hello, sarà anche necessario tooregister un middleware OWIN. In questo caso, è necessario spostare hello sopra il codice di configurazione in una nuova classe di avvio di OWIN.

1. Aggiungere il pacchetto NuGet hello `Microsoft.Owin.Host.SystemWeb` se non è già incluso nel progetto.
2. In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi** -> **Nuovo elemento**. Selezionare **Web** -> **Generale** -> **Classe di avvio di OWIN**.
3. Spostare hello di sopra di codice per MobileAppConfiguration da `WebApiConfig.Register()` toohello `Configuration()` metodo per la nuova classe di avvio.

Verificare che hello `Configuration()` metodo termina con:

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

Esistono tooauthentication correlati di altre modifiche che sono descritte nella sezione autenticazione completa hello riportato di seguito.

### <a name="working-with-data"></a>Uso dei dati
Nei servizi mobili, il nome di app per dispositivi mobili hello utilizzato come nome dello schema predefinito di hello nel programma di installazione di hello Entity Framework.

tooensure che è necessario hello stesso schema a cui fa riferimento come prima, hello utilizzare schema hello tooset hello DbContext per l'applicazione seguente:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Verificare di che aver MS_MobileServiceName impostare se hello sopra. È anche possibile fornire un altro nome di schema se l'applicazione lo ha personalizzato in precedenza.

### <a name="system-properties"></a>Proprietà di sistema
#### <a name="naming"></a>Denominazione
Nel server di servizi mobili di Azure hello SDK, le proprietà di sistema contengono sempre un doppio carattere di sottolineatura (`__`) prefisso per le proprietà di hello:

* __createdAt
* __updatedAt
* __deleted
* __version

il client di servizi mobili Hello SDK hanno una logica speciale per l'analisi delle proprietà del sistema in questo formato.

In App mobili di Azure, le proprietà di sistema non sono una speciale formattare e avere hello i nomi seguenti:

* createdAt
* updatedAt
* deleted
* version

Hello App per dispositivi mobili client SDK utilizzare hello nuovo sistema proprietà, in modo da modifiche non sono necessari nomi tooclient codice. Tuttavia, se si è direttamente effettua REST chiama servizio tooyour quindi è necessario modificare di conseguenza le query.

#### <a name="local-store"></a>Archivio locale
Hello modifiche toohello nomi di proprietà di sistema indicano che un database locale di sincronizzazione non in linea per i servizi mobili non è compatibile con App per dispositivi mobili. Se possibile, è consigliabile evitare l'aggiornamento di applicazioni client da servizi mobili tooMobile che App fino a dopo le modifiche in sospeso sono state inviate toohello server. Quindi, hello aggiornato app deve utilizzare un nuovo nome di database.

Se un'applicazione client viene aggiornata da servizi mobili tooMobile App mentre sono presenti modifiche non in linea in sospeso nella coda di operazione hello, database di sistema hello deve essere aggiornato toouse hello nomi di colonna nuova. In iOS, è possibile usare nomi di colonna hello toochange migrazioni lightweight. In Android e hello gestito client .NET, è consigliabile scrivere toorename SQL personalizzata colonne hello per le tabelle di dati oggetto.

In iOS, è necessario modificare lo schema dei dati di base per i dati entità toomatch hello successivi. Si noti che le proprietà di hello `createdAt`, `updatedAt` e `version` non hanno più un `ms_` prefisso:

| Attributo | Tipo | Nota |
| --- | --- | --- |
| id |Stringa, contrassegnata come obbligatoria |chiave primaria nell'archivio remoto |
| createdAt |Date |proprietà di sistema toocreatedAt mappe (facoltativo) |
| updatedAt |Date |proprietà di sistema tooupdatedAt mappe (facoltativo) |
| version |String |è in conflitto toodetect utilizzato (facoltativo), mappe tooversion |

#### <a name="querying-system-properties"></a>Query delle proprietà di sistema
Servizi mobili di Azure, le proprietà di sistema non vengono inviate per impostazione predefinita, ma solo quando vengono richiesti utilizzando la stringa di query hello `__systemProperties`. Al contrario, nel sistema di App mobili di Azure sono proprietà **sempre selezionato** poiché sono parte del modello a oggetti hello server SDK.

Questa modifica influisce principalmente sulle implementazioni personalizzate di gestori di dominio, come le estensioni di `MappedEntityDomainManager`. In servizi mobili, se un client non richiede mai le proprietà del sistema, è possibile toouse un `MappedEntityDomainManager` che non effettivamente eseguire il mapping di tutte le proprietà. Tuttavia, in App per dispositivi mobili di Azure, queste proprietà non mappate genereranno un errore nelle query GET.

problema di hello tooresolve modo più semplice di Hello è toomodify il DTO in modo che ereditano da `ITableData` anziché `EntityData`. Aggiungere quindi hello `[NotMapped]` attributo campi toohello che devono essere omessa.

Ad esempio, il seguente hello definisce `TodoItem` senza proprietà di sistema:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Nota: se si verifica un errore `NotMapped`, aggiungere un assembly di riferimento toohello `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Servizi mobili è incluso il supporto per CORS eseguendo il wrapping di hello soluzione ASP.NET CORS. Questo livello di ritorno a capo è stato rimosso toogive per sviluppatori di hello maggiore controllo, è possibile utilizzare direttamente [supporto ASP.NET CORS](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

le aree principali problematiche se tramite condivisione CORS Hello sono tale hello `eTag` e `Location` intestazioni devono essere consentite affinché hello client SDK toowork correttamente.

### <a name="push-notifications"></a>Notifiche push
Affinché il push, hello principale che potrebbero risultare mancanti dal Server SDK hello è classe PushRegistrationHandler hello. Le registrazioni vengono gestite in modo leggermente diverso nelle app per dispositivi mobili e le registrazioni prive di tag sono abilitate per impostazione predefinita. La gestione dei tag può essere eseguita usando API personalizzate. Vedere hello [la registrazione per i tag](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) le istruzioni per ulteriori informazioni.

### <a name="scheduled-jobs"></a>Processi pianificati
I processi pianificati non vengono compilati in App per dispositivi mobili, pertanto tutti i processi esistenti presenti nel back-end .NET necessario toobe aggiornato singolarmente. Un'opzione è pianificato toocreate [processo Web] nel sito di codice hello App per dispositivi mobili. È anche possibile configurare un controller che contiene il codice di processo e configurare hello [dell'utilità di pianificazione di Azure] toohit quell'endpoint su pianificazione hello previsto.

### <a name="miscellaneous-changes"></a>Modifiche varie
Tutti i ApiControllers che verranno utilizzati da un client mobile devono disporre di hello `[MobileAppController]` attributo. Non è più incluso per impostazione predefinita, in modo che altri toogo ApiControllers influenzato hello formattatori per dispositivi mobili.

Hello `ApiServices` oggetto non fa parte di hello SDK. tooaccess le impostazioni dell'App Mobile, è possibile utilizzare l'esempio hello:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

Analogamente, la registrazione viene ora eseguita mediante scrittura di traccia ASP.NET standard hello:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Considerazioni sull'autenticazione
componenti di autenticazione Hello dei servizi mobili sono stati spostati nella funzionalità di autenticazione/autorizzazione del servizio App hello. È possibile acquisire informazioni se si abilita questa per il sito per la lettura hello [Aggiungi app per dispositivi mobili tooyour autenticazione](app-service-mobile-ios-get-started-users.md) argomento.

Per alcuni provider, ad esempio, Google, Facebook e AAD dovrebbe essere in grado di tooleverage registrazione hello dall'applicazione di copia. Semplicemente necessario portale toonavigate toohello del provider e aggiungere una nuova registrazione toohello URL di reindirizzamento. Quindi configurare l'autenticazione/autorizzazione del servizio App con hello client ID e il segreto.

### <a name="controller-action-authorization"></a>Autorizzazione dell'azione del controller
Tutte le istanze di hello `[AuthorizeLevel(AuthorizationLevel.User)]` attributo deve essere modificate toouse hello ASP.NET standard `[Authorize]` attributo. Inoltre, i controller ora sono anonimi per impostazione predefinita, come nelle altre applicazioni ASP.NET.
Se si utilizza uno di hello altre opzioni di AuthorizeLevel, ad esempio Admin o un'applicazione, tenere presente che questi sono stati eliminati. È invece possibile impostare AuthorizationFilters per i segreti condivisi o configurare in modo sicuro un chiamate service to service tooenable dell'entità servizio AAD.

### <a name="getting-additional-user-information"></a>Recupero di informazioni aggiuntive sull'utente
È possibile ottenere informazioni utente aggiuntive, tra cui i token di accesso tramite hello `GetAppServiceIdentityAsync()` metodo:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

Inoltre, se l'applicazione accetta le dipendenze su ID utente, ad esempio conservarli in un database, è importante toonote che hello tra servizi mobili e App per dispositivi mobili del servizio App ID utente sono diversi. È comunque possibile ottenere hello ID utente di servizi mobili, tuttavia. Le sottoclassi ProviderCredentials hello dispone di una proprietà ID utente. Pertanto, proseguendo dallo esempio hello prima:

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Se l'app esegue tutte le dipendenze su ID utente, è importante utilizzare hello stessa registrazione con un provider di identità, se possibile. Gli ID utente sono in genere con ambito toohello registrazione dell'applicazione che è stata usata, quindi introdurre una nuova registrazione potrebbero provocare problemi con i corrispondenti dati tootheir gli utenti.

### <a name="custom-authentication"></a>Autenticazione personalizzata
Se l'app Usa una soluzione di autenticazione personalizzato, è possibile che tale sito aggiornato hello disponga di accesso toohello sistema toomake. Seguire le istruzioni di nuovo hello per l'autenticazione personalizzata in hello [Panoramica di .NET server SDK] toointegrate la soluzione. Si noti che i componenti di autenticazione personalizzata hello siano ancora in anteprima.

## <a name="updating-clients"></a>Aggiornamento dei client
Dopo aver reso operativo un back-end dell'app per dispositivi mobili, è possibile lavorare su una nuova versione dell'applicazione client che ne faccia uso. App per dispositivi mobili include anche una nuova versione del client hello SDK e aggiornamento del server toohello simile precedente, sarà necessario tooremove tutti i riferimenti toohello Mobile Services SDK prima di installare le versioni di App per dispositivi mobili hello.

Una delle modifiche principali di hello tra le versioni di hello è che i costruttori di hello non richiedono una chiave applicazione. È ora semplicemente passare hello URL dell'App Mobile. Ad esempio, nei client .NET hello, hello `MobileServiceClient` costruttore è:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

È possibile leggere informazioni sull'installazione hello nuovi SDK e con nuova struttura di hello tramite collegamenti hello riportati di seguito:

* [iOS versione 3.0.0 o successiva](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versione 2.0.0 o successiva](app-service-mobile-dotnet-how-to-use-client-library.md)

Se in un'applicazione si usano le notifiche push, prendere nota di hello istruzioni di registrazione specifica per ogni piattaforma, come sono state apportate alcune modifiche sono anche.

Dopo aver hello nuova versione del client pronta, eseguire la verifica per il progetto server aggiornato in. Dopo aver verificato il corretto funzionamento, è possibile rilasciare una nuova versione di toocustomers l'applicazione. Infine, dopo i clienti hanno una probabilità tooreceive questi aggiornamenti, è possibile eliminare versione di servizi mobili hello dell'app. A questo punto, avere completamente aggiornato tooan App del servizio Mobile App utilizzando il server di App per dispositivi mobili più recente hello SDK.

<!-- URLs. -->

[portale di Azure]: https://portal.azure.com/
[portale di Azure classico]: https://manage.windowsazure.com/
[quali sono App per dispositivi mobili?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[dell'utilità di pianificazione di Azure]: /en-us/documentation/services/scheduler/
[processo Web]: ../app-service-web/websites-webjobs-resources.md
[come toouse hello server .NET SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[servizio App prezzi]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Panoramica di .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
