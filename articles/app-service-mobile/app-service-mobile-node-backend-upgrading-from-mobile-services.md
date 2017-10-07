---
title: aaaUpgrade da servizi mobili tooAzure servizio App - Node. js
description: Informazioni su come tooeasily l'aggiornamento del tooan di applicazione di servizi mobili App del servizio Mobile App
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Aggiornare il tooApp servizio Mobile di Azure Node.js esistente del servizio
Servizio App per dispositivi mobili sono un nuovo modo toobuild applicazioni per dispositivi mobili con Microsoft Azure. vedere, più toolearn [quali sono App per dispositivi mobili?].

Questo argomento viene descritto come un'applicazione back-end Node.js esistente da servizi mobili di Azure tooa tooupgrade nuova App per dispositivi mobili del servizio App. Durante l'esecuzione di questo aggiornamento, l'applicazione di servizi mobili esistente possa continuare toooperate.  Se è necessario tooupgrade un'applicazione back-end di Node.js, vedere troppo[l'aggiornamento di servizi mobili .NET](app-service-mobile-net-upgrading-from-mobile-services.md).

Quando un back-end mobile è aggiornato tooAzure servizio App, ha accesso tooall le funzionalità del servizio App e vengono fatturate in base troppo[servizio App prezzi], non sui prezzi di servizi mobili.

## <a name="migrate-vs-upgrade"></a>Eseguire la migrazione o aggiornare
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Prima di procedere a un aggiornamento, è consigliabile [eseguire una migrazione](app-service-mobile-migrating-from-mobile-services.md) . In questo modo, è possibile inserire entrambe le versioni dell'applicazione hello piano di servizio App stesso e non comportare senza alcun costo aggiuntivo.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Miglioramenti apportati all'SDK del server Node.js di App per dispositivi mobili
L'aggiornamento toohello nuova [Mobile App SDK](https://www.npmjs.com/package/azure-mobile-apps) fornisce numerosi miglioramenti, tra cui:

* In base a hello [Express framework](http://expressjs.com/en/index.html), il nuovo nodo SDK hello è leggero e progettato tookeep con le nuove versioni nodo man mano che arrivano. È possibile personalizzare il comportamento dell'applicazione hello con Express middleware.
* Miglioramenti significativi delle prestazioni rispetto toohello Mobile Services SDK.
* È ora possibile ospitare un sito Web con il back-end mobile; allo stesso modo, è facile tooadd hello Azure Mobile SDK tooany express.v4 applicazione esistente.
* Compilato per lo sviluppo multipiattaforma e locale, hello Mobile App SDK può essere sviluppata ed eseguire localmente su piattaforme Windows, Linux e OS x. Ora è facile toouse comuni nodo tecniche di sviluppo come esecuzione [Mocha](https://mochajs.org/) verifica toodeployment precedente.

## <a name="overview"></a>Panoramica sull'aggiornamento di base
tooaid durante l'aggiornamento di un back-end Node.js, Azure App Service ha fornito un pacchetto di compatibilità.  Dopo l'aggiornamento, sarà necessario un sito niew che può essere distribuito tooa nuovo sito di servizio App.

il client di servizi mobili di Hello SDK sono **non** compatibile con il server di App per dispositivi mobili nuovi hello SDK. In ordine tooprovide la continuità del servizio per l'app, non è possibile pubblicare il sito di tooa modifiche attualmente rispondendo alle richieste client pubblicato. È invece necessario creare una nuova app per dispositivi mobili che agisce da duplicato. È possibile inserire l'applicazione hello stesso servizio App piano tooavoid incorrere in costi finanziari aggiuntivi.

Sarà quindi possibile due versioni di un'applicazione hello: uno che rimane hello stesso e funge da app pubblicate in circostanze normali hello e rilasciare l'altro che è quindi possibile eseguire l'aggiornamento e la destinazione con un nuovo client. È possibile spostare e testare il codice le esigenze, ma è necessario assicurarsi che tutte le correzioni di bug apportate ottenere tooboth applicato. Quando si ritiene che un numero desiderato di App client in circostanze normali è aggiornati toohello più recente, è possibile eliminare l'applicazione migrata originale hello se lo si desidera. Non comportano costi aggiuntivi monetari, se ospitato in hello stesso servizio App piano dell'App Mobile.

Hello completo per il processo di aggiornamento hello è come segue:

1. Scaricare il servizio mobile di Azure esistente (migrato).
2. Convertire hello progetto tooan App per dispositivi mobili di Azure usando il pacchetto di compatibilità hello.
3. Correggere le eventuali differenze (ad esempio nelle impostazioni di autenticazione).
4. Distribuire il convertito tooa di progetto di App per dispositivi mobili di Azure nuovo servizio App.
5. Rilasciare una nuova versione dell'applicazione client che usa hello nuova App per dispositivi mobili.
6. (Facoltativo) Eliminare l'app del servizio mobile originale migrata.

L'eliminazione può essere eseguita quando non è presente traffico nel servizio mobile originale migrato.

## <a name="install-npm-package"></a>Installare i prerequisiti hello
È consigliabile installare Node nel computer locale.  È inoltre necessario installare il pacchetto di compatibilità hello.  Dopo l'installazione di nodo, è possibile eseguire hello comando seguente da un nuovo cmd o un prompt dei comandi PowerShell:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> Ottenere gli script di Servizi mobili di Azure
* Accedi toohello [portale Azure].
* Usare **Tutte le risorse** o **Servizi app** per trovare il sito di Servizi mobili.
* All'interno del sito hello, fare clic su **strumenti** -> **Kudu** -> **passare** sito Kudu di tooopen hello.
* Fare clic su **Debug Console** -> **PowerShell** console di Debug tooopen hello.
* Passare troppo`site/wwwroot/App_Data/config` facendo clic su ogni directory a sua volta
* Fare clic su Avanti toohello di hello download icona `scripts` directory.

Questo script hello in formato ZIP eseguirà il download.  Creare una nuova directory sul computer locale e decomprimere hello `scripts.ZIP` file all'interno di directory hello.  Verrà così creata una directory `scripts` .

## <a name="scaffold-app"></a>Lo scaffolding hello nuovo back-end App mobili di Azure
Eseguire hello comando seguente dalla directory hello contenente la directory di script hello:

```scaffold-mobile-app scripts out```

Verrà creato un back-end scaffolding di App mobili di Azure in hello `out` directory.  Sebbene non obbligatorio, è un hello toocheck buona `out` directory in un repository di codice sorgente di propria scelta.

## <a name="deploy-ama-app"></a> Distribuire il back-end delle app per dispositivi mobili
Durante la distribuzione, è necessario seguente hello toodo:

1. Creare una nuova App per dispositivi mobili in hello [portale Azure].
2. Eseguire hello `createViews.sql` script sul database connesso.
3. Collegamento hello database tooyour collegato del servizio Mobile tooyour nuovo servizio App.
4. Collegamento di qualsiasi altro toohello risorse (ad esempio gli hub di notifica) nuovo servizio App.
5. Distribuire hello generato codice tooyour nuovo sito.

### <a name="create-a-new-mobile-app"></a>Creare una nuova app per dispositivi mobili
1. Accedere all'indirizzo hello [portale Azure].
2. Fare clic su **+NUOVO** > **Web e dispositivi mobili** > **App per dispositivi mobili** e quindi specificare un nome per il back-end dell'app per dispositivi mobili.
3. Per hello **gruppo di risorse**, selezionare un gruppo di risorse esistente o crearne uno nuovo (utilizzando hello stesso nome dell'app).

    È possibile selezionare un altro piano del servizio app o crearne uno nuovo. Per ulteriori informazioni sui piani di servizi App e come toocreate un nuovo piano di un prezzo diversi livelli e nella propria posizione desiderata, vedere [piani di servizio App di Azure ad approfondimenti su](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Per hello **piano di servizio App**, il piano predefinito hello (in hello [livello Standard](https://azure.microsoft.com/pricing/details/app-service/)) sia selezionata. È anche possibile selezionare un piano diverso oppure [crearne uno nuovo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). le impostazioni del piano di servizio App Hello determinano hello [posizione, funzionalità, costo e le risorse di calcolo](https://azure.microsoft.com/pricing/details/app-service/) associati all'app.

    Dopo avere stabilito il piano di hello, fare clic su **crea**. Crea back-end di hello App per dispositivi mobili.

### <a name="run-createviewssql"></a>Eseguire CreateViews.SQL
Hello scaffolding app contiene un file denominato `createViews.sql`.  Questo script deve essere eseguito sul database di destinazione.  stringa di connessione Hello hello database di destinazione può essere ottenuto nel servizio mobile migrato da hello **impostazioni** pannello **le stringhe di connessione**.  È denominata `MS_TableConnectionString`.

È possibile eseguire lo script da SQL Server Management Studio o Visual Studio.

### <a name="link-hello-database-tooyour-app-service"></a>Collegamento hello Database tooyour servizio App
Collegamento hello esistente database tooyour servizio App:

* In hello [portale Azure], aprire il servizio App.
* Selezionare **Tutte le impostazioni** -> **Connessioni dati**.
* Fare clic su **+ Aggiungi**.
* Nell'elenco a discesa hello, selezionare **Database SQL**
* In **Database SQL** selezionare il database esistente e quindi fare clic su **Seleziona**.
* In **stringa di connessione**, immettere nome utente hello e una password per il database di hello, quindi fare clic su **OK**.
* In hello **aggiungere connessioni dati** pannello, fare clic su **OK**.

la password e il nome utente hello è reperibile visualizzando hello stringa di connessione per il database di destinazione hello nel servizio Mobile migrati.

### <a name="set-up-authentication"></a>Configurare l'autenticazione
App per dispositivi mobili Azure consente l'autenticazione di Azure Active Directory, Facebook, Google, Microsoft e Twitter tooconfigure all'interno del servizio hello.  Autenticazione personalizzata sarà necessario toobe sviluppato separatamente.  Fare riferimento a messaggi hello [concetti di autenticazione] documentazione e [delle Guide rapide di autenticazione] documentazione per ulteriori informazioni.  

## <a name="updating-clients"></a>Aggiornare i client per dispositivi mobili
Dopo aver reso operativo un back-end dell'app per dispositivi mobili, è possibile lavorare su una nuova versione dell'applicazione client che ne faccia uso. App per dispositivi mobili include anche una nuova versione del client hello SDK e aggiornamento del server toohello simile precedente, sarà necessario tooremove tutti i riferimenti toohello Mobile Services SDK prima di installare le versioni di App per dispositivi mobili.

Una delle modifiche principali di hello tra le versioni di hello è che i costruttori di hello non richiedono una chiave applicazione.
È ora semplicemente passare hello URL dell'App Mobile. Ad esempio, nei client .NET hello, hello `MobileServiceClient` costruttore è:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

È possibile leggere informazioni sull'installazione hello nuovi SDK e con nuova struttura di hello tramite collegamenti hello riportati di seguito:

* [Android versione 2.2 o successiva](app-service-mobile-android-how-to-use-client-library.md)
* [iOS versione 3.0.0 o successiva](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versione 2.0.0 o successiva](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova versione 2.0 o successiva](app-service-mobile-cordova-how-to-use-client-library.md)

Se in un'applicazione si usano le notifiche push, prendere nota di hello istruzioni di registrazione specifica per ogni piattaforma, come sono state apportate alcune modifiche sono anche.

Dopo aver hello nuova versione del client pronta, eseguire la verifica per il progetto server aggiornato in. Dopo aver verificato il corretto funzionamento, è possibile rilasciare una nuova versione di toocustomers l'applicazione. Infine, dopo i clienti hanno una probabilità tooreceive questi aggiornamenti, è possibile eliminare versione di servizi mobili hello dell'app. A questo punto, avere completamente aggiornato tooan App del servizio Mobile App utilizzando il server di App per dispositivi mobili più recente hello SDK.

<!-- URLs. -->

[Portale di Azure]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[quali sono App per dispositivi mobili?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[servizio App prezzi]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[concetti di autenticazione]: ../app-service/app-service-authentication-overview.md
[delle Guide rapide di autenticazione]: app-service-mobile-auth.md

[portale Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
