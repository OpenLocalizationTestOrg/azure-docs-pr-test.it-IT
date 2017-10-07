---
title: aaaEnable sincronizzazione offline per l'App Mobile di Azure (Android di Xamarin)
description: Informazioni su come toouse App del servizio Mobile App toocache e sincronizzazione dati offline nell'applicazione Android di Xamarin
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a>Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione introduce funzionalità di sincronizzazione non in linea hello di App mobili di Azure per xamarin. Sincronizzazione non in linea consente toointeract gli utenti finali con un'app per dispositivi mobili, visualizzazione, aggiunta o modifica dei dati, anche quando è presente alcuna connessione di rete. Le modifiche vengono archiviate in un database locale.
Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con servizio remoto hello.

In questa esercitazione, si aggiorna il progetto client hello dall'esercitazione hello [creare un'app Android di Xamarin] toosupport hello funzionalità offline di App mobili di Azure. Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere hello dati estensione pacchetti tooyour di Microsoft Access. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Aggiornamento funzionalità offline toosupport hello client dell'applicazione
Le funzionalità non in linea di App Mobile Azure consentono di toointeract con un database locale quando si è in uno scenario non in linea. toouse queste funzionalità nell'applicazione, si inizializza un [SyncContext] tooa di archivio locale. Fare riferimento la tabella tramite hello [IMobileServiceSyncTable] [IMobileServiceSyncTable] interfaccia. SQLite viene utilizzato come archivio locale hello dispositivo hello.

1. In Visual Studio, aprire Gestione pacchetti NuGet di hello nel progetto hello completato nelle hello [creare un'app Android di Xamarin] esercitazione.  Cercare e installare hello **Microsoft.Azure.Mobile.Client.SQLiteStore** pacchetto NuGet.
2. Aprire il file ToDoActivity.cs hello e rimuovere il commento hello `#define OFFLINE_SYNC_ENABLED` definizione.
3. In Visual Studio, premere hello **F5** chiave toorebuild e app client hello esecuzione. app Hello funziona esattamente come prima di attivare la sincronizzazione non in linea hello. Tuttavia, database locale hello viene popolato con dati che possono essere utilizzati in uno scenario non in linea.

## <a name="update-sync"></a>Aggiornare hello app toodisconnect dal back-end hello
In questa sezione si interrompe hello connessione tooyour App Mobile back-end toosimulate una situazione non in linea. Quando si aggiungono elementi di dati, il gestore di eccezioni indica che app hello è in modalità offline. In questo stato, nuovi elementi aggiunti in locale hello archiviano e sincronizzati in back-end dell'app mobile hello quando viene eseguito un push in uno stato connesso.

1. Modifica ToDoActivity.cs nel progetto condiviso hello. Hello modifica **applicationURL** URL non valido di toopoint tooan:

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Disabilitazione Wi-Fi e reti cellulari sul dispositivo hello o utilizzando modalità aereo, è anche possibile illustrare il comportamento non in linea.
2. Premere **F5** toobuild ed eseguire app hello. Si noti la sincronizzazione non riuscita in aggiornamento quando hello app avviata.
3. Immettere nuovi elementi. Si noti che il push ha esito negativo con stato [CancelledByNetworkError] ogni volta che si fa clic su **Salva**. Tuttavia, nuovi elementi di attività hello esistono nell'archivio locale hello fino a quando non può essere di back-end dell'app mobile toohello inseriti.  In un ambiente di produzione app, se si eliminano queste eccezioni hello client app si comporta come se fosse ancora connessa back-end dell'app mobile toohello.
4. Chiudere l'applicazione hello e riavviarlo tooverify che è stato creato in base ai nuovi elementi hello siano archivio locale toohello persistente.
5. (Facoltativo) In Visual Studio aprire **Esplora server**. Esplorare database tooyour **Azure**->**database SQL**. Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**. È possibile cercare tooyour tabella di database SQL e il relativo contenuto. Verificare che i dati di hello nel database back-end hello non sono stato modificato.
6. (Facoltativo) Utilizzare uno strumento REST come Fiddler o Postman tooquery back-end mobile, utilizzando una query GET nel formato `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Aggiornare hello app tooreconnect back-end App per dispositivi mobili
In questa sezione, ristabilire la connessione back-end di hello app toohello app per dispositivi mobili. Quando si esegue innanzitutto un'applicazione hello, hello `OnCreate` chiamate del gestore dell'evento `OnRefreshItemsSelected`. Questo metodo chiama `SyncAsync` toosync archivio locale con database back-end hello.

1. Aprire ToDoActivity.cs nel progetto condiviso hello e annullare la modifica di hello **applicationURL** proprietà.
2. Hello premere **F5** chiave toorebuild e app hello esecuzione. Hello app esegue la sincronizzazione le modifiche locali con back-end App Mobile Azure hello utilizzando operazioni push e pull quando hello `OnRefreshItemsSelected` esecuzione del metodo.
3. (Facoltativo) Hello visualizzazione aggiornata dei dati utilizzando Esplora oggetti di SQL Server o uno strumento REST come Fiddler. Si noti hello dati sono stati sincronizzati tra database back-end di hello App per dispositivi mobili di Azure e l'archivio locale hello.
4. Nell'app hello, fare clic su verifica hello casella accanto a pochi elementi toocomplete li nell'archivio locale hello.

   `CheckItem`chiamate `SyncAsync` elemento toosync ogni completato con back-end di hello App per dispositivi mobili. `SyncAsync` chiama operazioni sia push che pull. **Ogni volta che si esegue un'operazione di pull in una tabella che il client hello è stato modificato da, un push viene sempre eseguito automaticamente**. Ciò assicura che tutte le tabelle nell'archivio locale e le relazioni restino coerenti e può determinare un'operazione push non prevista. Per altre informazioni su questo comportamento, vedere [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="review-hello-client-sync-code"></a>Esaminare il codice di sincronizzazione client hello
progetto di client Xamarin Hello scaricato dopo avere completato l'esercitazione hello [creare un'app Android di Xamarin] già contiene il codice che supporta la sincronizzazione non in linea utilizzando un database locale di SQLite. Di seguito è riportata una breve panoramica degli elementi già inclusi nel codice dell'esercitazione hello. Per informazioni generali sulla funzionalità hello, vedere [sincronizzazione dati Offline nelle App mobili di Azure].

* Prima di possono eseguire qualsiasi operazione di tabella, è necessario inizializzare l'archivio locale hello. Hello database dell'archivio locale viene inizializzato quando `ToDoActivity.OnCreate()` esegue `ToDoActivity.InitLocalStoreAsync()`. Questo metodo crea un database locale di SQLite utilizzando hello `MobileServiceSQLiteStore` classe fornita dai client di hello App mobili di Azure SDK.

    Hello `DefineTable` metodo crea una tabella nell'archivio locale hello corrispondente hello campi tipo hello fornito, `ToDoItem` in questo caso. tipo di Hello privo di tooinclude tutte le colonne di hello presenti nel database remoto hello. È possibile toostore solo un subset di colonne.

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* Hello `toDoTable` membro di `ToDoActivity` di hello `IMobileServiceSyncTable` digitare anziché `IMobileServiceTable`. Hello IMobileServiceSyncTable indirizza tutti creare, leggere, aggiornare ed eliminare database dell'archivio locale toohello operazioni tabella (CRUD).

    Si decide quando le modifiche vengono inserite back-end App Mobile Azure toohello chiamando `IMobileServiceSyncContext.PushAsync()`. Hello contesto di sincronizzazione consente di mantenere le relazioni tra tabelle e di rilevamento e il push delle modifiche in tutte le tabelle modificato quando un'app client `PushAsync` viene chiamato.

    chiamate di codice Hello fornito `ToDoActivity.SyncAsync()` toosync ogni volta che viene aggiornato l'elenco todoitem hello o un oggetto todoitem viene aggiunto o completato. Hello codice esegue la sincronizzazione dopo ogni modifica locale.

    Nel codice hello fornito, tutti i record in remoto hello `TodoItem` vengono eseguite query sulle tabella, ma è anche possibile toofilter record passando un id di query e una query troppo`PushAsync`. Per ulteriori informazioni, vedere la sezione hello *sincronizzazione incrementale* in [sincronizzazione dati Offline nelle App mobili di Azure].

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a>Risorse aggiuntive
* [sincronizzazione dati Offline nelle App mobili di Azure]
* [Procedura per .NET SDK di App per dispositivi mobili di Azure][8]

<!-- URLs. -->
[creare un'app Android di Xamarin]: ../app-service-mobile-xamarin-android-get-started.md
[sincronizzazione dati Offline nelle App mobili di Azure]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Creare un'app Xamarin Android]: app-service-mobile-xamarin-android-get-started.md
[Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
