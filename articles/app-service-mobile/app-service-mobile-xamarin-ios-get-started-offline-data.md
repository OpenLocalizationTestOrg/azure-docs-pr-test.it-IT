---
title: aaaEnable sincronizzazione offline per l'App Mobile di Azure (Xamarin. iOS)
description: Informazioni su come toouse App del servizio Mobile App toocache e sincronizzazione dati offline nell'applicazione Xamarin iOS
documentationcenter: xamarin
author: ggailey777
manager: cfowler
editor: 
services: app-service\mobile
ms.assetid: 828a287c-5d58-4540-9527-1309ebb0f32b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5243f2d292377d8de103a40f45d649394f11b97c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a>Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione introduce funzionalità di sincronizzazione non in linea hello di App mobili di Azure per xamarin. IOS. Sincronizzazione non in linea consente toointeract gli utenti finali con un'app per dispositivi mobili, visualizzazione, aggiunta o modifica dei dati, anche quando è presente alcuna connessione di rete. Le modifiche vengono archiviate in un database locale. Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con servizio remoto hello.

In questa esercitazione, aggiornare il progetto di app xamarin hello da [creare un'app iOS Xamarin] toosupport hello funzionalità offline di App mobili di Azure. Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere i pacchetti di estensione di accesso ai dati hello al progetto. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Aggiornamento funzionalità offline toosupport hello client dell'applicazione
Le funzionalità non in linea di App Mobile Azure consentono di toointeract con un database locale quando si è in uno scenario non in linea. toouse queste funzionalità nell'app, inizializzare un [SyncContext] tooa di archivio locale. Fare riferimento a tabella tramite l'interfaccia hello [IMobileServiceSyncTable]. SQLite viene utilizzato come archivio locale hello dispositivo hello.

1. Gestione pacchetti NuGet di hello Apri progetto hello completato nelle hello [creare un'app iOS Xamarin] esercitazione, quindi cercare e installare hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet pacchetto.
2. Aprire il file QSTodoService.cs hello e rimuovere il commento hello `#define OFFLINE_SYNC_ENABLED` definizione.
3. Ricompilare ed eseguire l'applicazione client hello. app Hello funziona esattamente come prima di attivare la sincronizzazione non in linea hello. Tuttavia, database locale hello viene popolato con dati che possono essere utilizzati in uno scenario non in linea.

## <a name="update-sync"></a>Aggiornare hello app toodisconnect dal back-end hello
In questa sezione si interrompe hello connessione tooyour App Mobile back-end toosimulate una situazione non in linea. Quando si aggiungono elementi di dati, il gestore di eccezioni indica che app hello è in modalità offline. In questo stato, i nuovi elementi aggiunti in locale hello archiviano e verranno sincronizzati per hello back-end dell'app mobile push quindi l'esecuzione in uno stato di connessione.

1. Modifica QSToDoService.cs nel progetto condiviso hello. Hello modifica **applicationURL** URL non valido di toopoint tooan:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Disabilitazione Wi-Fi e reti cellulari sul dispositivo hello o utilizzando modalità aereo, è anche possibile illustrare il comportamento non in linea.
2. Compilare ed eseguire l'applicazione hello. Si noti la sincronizzazione non riuscita in aggiornamento quando hello app avviata.
3. Immettere nuovi elementi. Si noti che il push ha esito negativo con stato [CancelledByNetworkError] ogni volta che si fa clic su **Salva**. Tuttavia, nuovi elementi di attività hello esistono nell'archivio locale hello fino a quando non può essere di back-end dell'app mobile toohello inseriti.  In un ambiente di produzione app, se si eliminano queste eccezioni hello client app si comporta come se fosse ancora connessa back-end dell'app mobile toohello.
4. Chiudere l'applicazione hello e riavviarlo tooverify che è stato creato in base ai nuovi elementi hello siano archivio locale toohello persistente.
5. (Facoltativo) Se Visual Studio è installato in un computer, aprire **Esplora server**. Esplorare database tooyour **Azure**-> **database SQL**. Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**. È possibile cercare tooyour tabella di database SQL e il relativo contenuto. Verificare che i dati di hello nel database back-end hello non sono stato modificato.
6. (Facoltativo) Utilizzare uno strumento REST come Fiddler o Postman tooquery back-end mobile, utilizzando una query GET nel formato `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Aggiornare hello app tooreconnect back-end App per dispositivi mobili
In questa sezione, ristabilire la connessione back-end di hello app toohello app per dispositivi mobili. In questo modo si simulano app hello lo spostamento da uno stato online tooan di stato non in linea con back-end dell'app mobile hello.   Se si simulato rottura rete hello disattivando la connettività di rete, non è necessari alcuna modifica del codice.
Attivare nuovamente rete hello.  Quando si esegue innanzitutto un'applicazione hello, hello `RefreshDataAsync` metodo viene chiamato. A sua volta chiama `SyncAsync` toosync archivio locale con database back-end hello.

1. Aprire QSToDoService.cs nel progetto condiviso hello e annullare la modifica di hello **applicationURL** proprietà.
2. Ricompilare ed eseguire l'applicazione hello. Hello app esegue la sincronizzazione le modifiche locali con back-end App Mobile Azure hello utilizzando operazioni push e pull quando hello `OnRefreshItemsSelected` esecuzione del metodo.
3. (Facoltativo) Hello visualizzazione aggiornata dei dati utilizzando Esplora oggetti di SQL Server o uno strumento REST come Fiddler. Si noti hello dati sono stati sincronizzati tra database back-end di hello App per dispositivi mobili di Azure e l'archivio locale hello.
4. Nell'app hello, fare clic su verifica hello casella accanto a pochi elementi toocomplete li nell'archivio locale hello.

   `CompleteItemAsync`chiamate `SyncAsync` elemento toosync ogni completato con back-end di hello App per dispositivi mobili. `SyncAsync` chiama operazioni sia push che pull.
   **Ogni volta che si esegue un'operazione di pull in una tabella client hello è stato modificato da, un comando nel contesto di sincronizzazione client hello viene sempre eseguita per prima automaticamente**. push implicita Hello assicura che tutte le tabelle nell'archivio locale di hello insieme relazioni rimangono coerenti. Per altre informazioni su questo comportamento, vedere [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="review-hello-client-sync-code"></a>Esaminare il codice di sincronizzazione client hello
progetto di client Xamarin Hello scaricato dopo avere completato l'esercitazione hello [creare un'app iOS Xamarin] già contiene il codice che supporta la sincronizzazione non in linea utilizzando un database locale di SQLite. Di seguito è riportata una breve panoramica degli elementi già inclusi nel codice dell'esercitazione hello. Per informazioni generali sulla funzionalità hello, vedere [sincronizzazione dati Offline nelle App mobili di Azure].

* Prima di possono eseguire qualsiasi operazione di tabella, è necessario inizializzare l'archivio locale hello. Hello database dell'archivio locale viene inizializzato quando `QSTodoListViewController.ViewDidLoad()` esegue `QSTodoService.InitializeStoreAsync()`. Questo metodo crea un nuovo database SQLite locale utilizzando hello `MobileServiceSQLiteStore` classe fornita dai client di hello App per dispositivi mobili di Azure SDK.

    Hello `DefineTable` metodo crea una tabella nell'archivio locale hello corrispondente hello campi tipo hello fornito, `ToDoItem` in questo caso. tipo di Hello privo di tooinclude tutte le colonne di hello presenti nel database remoto hello. È possibile toostore solo un subset di colonne.

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* Hello `todoTable` membro di `QSTodoService` di hello `IMobileServiceSyncTable` digitare anziché `IMobileServiceTable`. Hello IMobileServiceSyncTable indirizza tutti creare, leggere, aggiornare ed eliminare database dell'archivio locale toohello operazioni tabella (CRUD).

    Si decide quando tali modifiche vengono inserite back-end App Mobile Azure toohello chiamando `IMobileServiceSyncContext.PushAsync()`. Hello contesto di sincronizzazione consente di mantenere le relazioni tra tabelle e di rilevamento e il push delle modifiche in tutte le tabelle modificato quando un'app client `PushAsync` viene chiamato.

    chiamate di codice Hello fornito `QSTodoService.SyncAsync()` toosync ogni volta che viene aggiornato l'elenco todoitem hello o un oggetto todoitem viene aggiunto o completato. L'app viene sincronizzata dopo ogni modifica locale. Se un'operazione di pull viene eseguita su una tabella in cui è in attesa di aggiornamenti locali registrati dal contesto hello, tale operazione pull attiverà automaticamente un push di contesto prima.

    Nel codice hello fornito, tutti i record in remoto hello `TodoItem` vengono eseguite query sulle tabella, ma è anche possibile toofilter record passando un id di query e una query troppo`PushAsync`. Per ulteriori informazioni, vedere la sezione hello *sincronizzazione incrementale* in [sincronizzazione dati Offline nelle App mobili di Azure].

        // QSTodoService.cs
        public async Task SyncAsync()
        {
            try
            {
                await client.SyncContext.PushAsync();
                await todoTable.PullAsync("allTodoItems", todoTable.CreateQuery()); // query ID is used for incremental sync
            }

            catch (MobileServiceInvalidOperationException e)
            {
                Console.Error.WriteLine(@"Sync Failed: {0}", e.Message);
            }
        }

## <a name="additional-resources"></a>Risorse aggiuntive
* [sincronizzazione dati Offline nelle App mobili di Azure]
* [Procedura per .NET SDK di App per dispositivi mobili di Azure][8]

<!-- Images -->

<!-- URLs. -->
[creare un'app iOS Xamarin]: app-service-mobile-xamarin-ios-get-started.md
[sincronizzazione dati Offline nelle App mobili di Azure]: app-service-mobile-offline-data-sync.md
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
