---
title: aaaEnable sincronizzazione offline per l'app Universal Windows Platform (UWP) con App per dispositivi mobili | Documenti Microsoft
description: Informazioni su come toouse App Mobile Azure toocache e sincronizzazione dei dati nell'app della piattaforma UWP (Universal Windows).
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Abilitare la sincronizzazione offline per l'app di Windows
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come offline tooadd supportano app Universal Windows Platform (UWP) tooa utilizza un back-end dell'App Mobile di Azure. Sincronizzazione non in linea consente toointeract gli utenti finali con un'app per dispositivi mobili, visualizzazione, aggiunta o modifica dei dati, anche quando è presente alcuna connessione di rete. Le modifiche vengono archiviate in un database locale. Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con back-end remoto hello.

In questa esercitazione, si aggiorna progetto dell'app UWP hello dall'esercitazione hello [creare un'app di Windows] toosupport hello funzionalità offline di App mobili di Azure. Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere hello dati estensione pacchetti tooyour di Microsoft Access. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="requirements"></a>Requisiti
Questa esercitazione richiede hello seguenti prerequisiti:

* Visual Studio 2013 in esecuzione in Windows 8.1 o versioni successive
* Completamento dell'esercitazione [Creare un'app Windows][Creare un'app Windows].
* [Azure Mobile Services SQLite Store][sqlite store nuget]
* [SQLite for Universal Windows Platform](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Aggiornamento funzionalità offline toosupport hello client dell'applicazione
Le funzionalità non in linea di App Mobile Azure consentono di toointeract con un database locale quando si è in uno scenario non in linea. toouse queste funzionalità nell'applicazione, si inizializza un [SyncContext] [ synccontext] tooa di archivio locale. Fare riferimento la tabella tramite hello [IMobileServiceSyncTable][IMobileServiceSyncTable] interfaccia. SQLite viene utilizzato come archivio locale hello dispositivo hello.

1. Installare hello [runtime SQLite per hello Universal Windows Platform](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. In Visual Studio, aprire Gestione pacchetti NuGet di hello del progetto di app UWP hello completato nelle hello [creare un'app di Windows] esercitazione.
    Cercare e installare hello **Microsoft.Azure.Mobile.Client.SQLiteStore** pacchetto NuGet.
3. In Esplora soluzioni fare doppio clic su **Riferimenti** > **Aggiungi riferimento...** >**Universal Windows**>**Estensioni** e quindi abilitare sia **SQLite for Universal Windows Platform** che **Visual C++ 2015 Runtime for Universal Windows Platform apps**.

    ![Aggiungere un riferimento UWP SQLite][1]
4. Aprire il file MainPage.xaml.cs hello e rimuovere il commento hello `#define OFFLINE_SYNC_ENABLED` definizione.
5. In Visual Studio, premere hello **F5** chiave toorebuild e app client hello esecuzione. app Hello funziona esattamente come prima di attivare la sincronizzazione non in linea hello. Tuttavia, database locale hello viene popolato con dati che possono essere utilizzati in uno scenario non in linea.

## <a name="update-sync"></a>Aggiornare hello app toodisconnect dal back-end hello
In questa sezione si interrompe hello connessione tooyour App Mobile back-end toosimulate una situazione non in linea. Quando si aggiungono elementi di dati, il gestore di eccezioni indica che app hello è in modalità offline. In questo stato, i nuovi elementi aggiunti in locale hello archiviano e verranno sincronizzati per hello back-end dell'app mobile push quindi l'esecuzione in uno stato di connessione.

1. Modifica App.xaml.cs nel progetto condiviso hello. Impostare come commento l'inizializzazione di hello di hello **MobileServiceClient** e aggiungere hello successiva riga, che utilizza un URL dell'app mobile non valido:

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    È anche possibile illustrare comportamento offline disabilitando Wi-Fi e reti cellulari sul dispositivo hello o utilizzare modalità aereo.
2. Premere **F5** toobuild ed eseguire app hello. Si noti la sincronizzazione non riuscita in aggiornamento quando hello app avviata.
3. Immettere nuovi elementi. Si noti che il push ha esito negativo con stato [CancelledByNetworkError] ogni volta che si fa clic su **Salva**. Tuttavia, nuovi elementi di attività hello esistono nell'archivio locale hello fino a quando non può essere di back-end dell'app mobile toohello inseriti.  In un ambiente di produzione app, se si eliminano queste eccezioni hello client app si comporta come se fosse ancora connessa back-end dell'app mobile toohello.
4. Chiudere l'applicazione hello e riavviarlo tooverify che è stato creato in base ai nuovi elementi hello siano archivio locale toohello persistente.
5. (Facoltativo) In Visual Studio aprire **Esplora server**. Esplorare database tooyour **Azure**->**database SQL**. Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**. È possibile cercare tooyour tabella di database SQL e il relativo contenuto. Verificare che i dati di hello nel database back-end hello non sono stato modificato.
6. (Facoltativo) Utilizzare uno strumento REST come Fiddler o Postman tooquery back-end mobile, utilizzando una query GET nel formato `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Aggiornare hello app tooreconnect back-end App per dispositivi mobili
In questa sezione si riconnette hello app toohello app mobile back-end. Queste modifiche per simulare una riconnessione di rete nell'applicazione hello.

Quando si esegue innanzitutto un'applicazione hello, hello `OnNavigatedTo` chiamate del gestore dell'evento `InitLocalStoreAsync`. Questo metodo chiama a sua volta `SyncAsync` toosync archivio locale con database back-end hello. app Hello tenta toosync all'avvio.

1. Aprire App.xaml.cs nel progetto condiviso hello e rimuovere la precedente inizializzazione di `MobileServiceClient` URL dell'app mobile toouse hello hello corretto.
2. Hello premere **F5** chiave toorebuild e app hello esecuzione. Hello app esegue la sincronizzazione le modifiche locali con back-end App Mobile Azure hello utilizzando operazioni push e pull quando hello `OnNavigatedTo` gestore eventi viene eseguito.
3. (Facoltativo) Hello visualizzazione aggiornata dei dati utilizzando Esplora oggetti di SQL Server o uno strumento REST come Fiddler. Si noti hello dati sono stati sincronizzati tra database back-end di hello App per dispositivi mobili di Azure e l'archivio locale hello.
4. Nell'app hello, fare clic su verifica hello casella accanto a pochi elementi toocomplete li nell'archivio locale hello.

   `UpdateCheckedTodoItem`chiamate `SyncAsync` elemento toosync ogni completato con back-end di hello App per dispositivi mobili. `SyncAsync` chiama operazioni sia push che pull. Tuttavia, **ogni volta che si esegue un'operazione di pull in una tabella che il client hello è stato modificato da, un push viene sempre eseguito automaticamente**. Questo comportamento assicura che tutte le tabelle nell'archivio locale di hello insieme relazioni rimangono coerenti. e può determinare un'operazione push non prevista.  Per altre informazioni su questo comportamento, vedere [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="api-summary"></a>Riepilogo dell'API
toosupport hello offline le funzionalità dei servizi mobili, abbiamo utilizzato hello [IMobileServiceSyncTable] l'interfaccia e inizializzato [MobileServiceClient.SyncContext] [ synccontext] con un database locale di SQLite. Quando non in linea, hello normale le operazioni CRUD per App per dispositivi mobili funzioneranno come se app hello è ancora connesso mentre si verificano operazioni di hello sull'archivio locale hello. Hello dei seguenti metodi è archivio locale di hello toosynchronize utilizzato con server hello:

* **[PushAsync]**  poiché questo metodo è un membro di [IMobileServicesSyncContext], le modifiche su tutte le tabelle vengono inserite toohello di back-end. Solo i record con le modifiche locali vengono inviati toohello server.
* **[PullAsync]**. Viene avviato un pull da [IMobileServiceSyncTable]. Quando sono presenti modifiche rilevate nella tabella hello, un push implicito viene eseguito toomake assicurarsi che tutte le tabelle nell'archivio locale di hello insieme relazioni rimangono coerenti. Hello *pushOtherTables* parametro determina se altre tabelle nel contesto di hello vengono inseriti in un push implicito. Hello *query* parametro accetta un [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] o hello toofilter stringa query di OData ha restituito dati. Hello *queryId* parametro viene utilizzato toodefine la sincronizzazione incrementale. Per altre informazioni, vedere [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  l'app deve chiamare periodicamente dati obsoleti toopurge metodo dall'archivio locale hello. Hello utilizzare *forzare* parametro quando è necessario toopurge tutte le modifiche non sono ancora state sincronizzate.

Per altre informazioni su questi concetti, vedere [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>Altre informazioni
Hello argomenti seguenti vengono fornite ulteriori informazioni sulla funzionalità di sincronizzazione non in linea hello di App per dispositivi mobili:

* [sincronizzazione dati Offline nelle App mobili di Azure]
* [Procedura per .NET SDK di App per dispositivi mobili di Azure][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[sincronizzazione dati Offline nelle App mobili di Azure]: app-service-mobile-offline-data-sync.md
[Creare un'app Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
