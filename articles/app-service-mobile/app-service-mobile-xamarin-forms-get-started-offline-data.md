---
title: aaaEnable sincronizzazione offline per l'App Mobile di Azure (xamarin. Forms) | Documenti Microsoft
description: Informazioni su come toouse App del servizio Mobile App toocache e sincronizzazione dati offline nell'applicazione xamarin. Forms
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione introduce funzionalità di sincronizzazione non in linea hello di App mobili di Azure per xamarin. Forms. La sincronizzazione offline consente agli utenti finali di interagire con un'app, visualizzando, aggiungendo e modificando i dati, anche se non è disponibile una connessione di rete. Le modifiche vengono archiviate in un database locale. Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con servizio remoto hello.

In questa esercitazione si basa sulla soluzione di avvio rapido di xamarin. Forms hello per App per dispositivi mobili che si crea una volta completata l'esercitazione [creare un'app di iOS Xamarin]. soluzione di avvio rapido Hello per xamarin. Forms contiene hello codice toosupport sincronizzazione offline, che è necessario impostare solo toobe abilitato. In questa esercitazione è aggiornare hello delle Guide rapide soluzione tooturn sulle funzionalità offline di hello di App mobili di Azure. È inoltre evidenziati codice specifico per la linea hello in app hello. Se non si utilizza hello scaricato soluzione di avvio rapido, è necessario aggiungere hello dati estensione pacchetti tooyour di Microsoft Access. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][1].

toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Abilitare la funzionalità di sincronizzazione non in linea nella soluzione di avvio rapido hello
codice di sincronizzazione non in linea Hello è incluso nel progetto hello mediante le direttive del preprocessore c#. Quando hello **OFFLINE\_sincronizzazione\_abilitato** simbolo è definito, questi percorsi di codice sono inclusi nella compilazione hello. Per le app di Windows, è necessario installare anche piattaforma SQLite hello.

1. In Visual Studio, fare doppio clic hello soluzione > **Gestisci pacchetti NuGet per la soluzione...** , quindi cercare e installare il **Microsoft.Azure.Mobile.Client.SQLiteStore** pacchetto NuGet per tutti i progetti nella soluzione hello.
2. In Esplora soluzioni hello, aprire il file di TodoItemManager.cs hello dal progetto di hello con **portabile** nel nome hello, che è il progetto libreria di classi portabile, quindi rimuovere il commento hello dopo la direttiva del preprocessore:

        #define OFFLINE_SYNC_ENABLED
3. I dispositivi Windows toosupport (facoltativo), installare uno dei seguenti pacchetti runtime SQLite hello:

   * **Windows 8.1 Runtime:** installare [SQLite per Windows 8.1][3].
   * **Windows Phone 8.1:** installare [SQLite per Windows Phone 8.1][4].
   * **Piattaforma UWP** installare [SQLite per hello universali di Windows universale][5].

     Anche se la Guida introduttiva hello non contiene un progetto Windows universale, piattaforma Windows universale hello è supportata con Xamarin Forms.
4. (Facoltativo) In ogni progetto di app di Windows, fare clic sul **riferimenti** > **Aggiungi riferimento...** , espandere hello **Windows** cartella > **estensioni**.
    Abilitare hello appropriato **SQLite per Windows** SDK insieme hello **Visual C++ 2013 Runtime per Windows** SDK.
    Hello nomi SQLite SDK variano leggermente in ogni piattaforma di Windows.

## <a name="review-hello-client-sync-code"></a>Esaminare il codice di sincronizzazione client hello
Ecco una breve panoramica degli elementi già inclusi nel codice dell'esercitazione di hello all'interno di hello `#if OFFLINE_SYNC_ENABLED` direttive. La funzionalità di sincronizzazione non in linea è nel file di progetto hello TodoItemManager.cs nel progetto libreria di classi portabile hello. Per informazioni generali sulla funzionalità hello, vedere [non in linea sincronizzazione di dati in App mobili di Azure][2].

* Prima di possono eseguire qualsiasi operazione di tabella, è necessario inizializzare l'archivio locale hello. Hello database dell'archivio locale viene inizializzato in hello **TodoItemManager** costruttore della classe utilizzando hello seguente codice:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Questo codice crea un nuovo database SQLite locale utilizzando hello **MobileServiceSQLiteStore** classe.

    Hello **DefineTable** metodo crea una tabella nell'archivio locale hello corrispondente hello campi tipo hello fornito.  tipo di Hello privo di tooinclude tutte le colonne di hello presenti nel database remoto hello. È possibile toostore un subset di colonne.
* Hello **todoTable** campo **TodoItemManager** è un **IMobileServiceSyncTable** digitare anziché **IMobileServiceTable**. Il database locale di hello utilizza classe per tutti creare, leggere, aggiornare ed eliminazione (CRUD) nella tabella. Si decide quando tali modifiche vengono inserite back-end App Mobile toohello chiamando **PushAsync** su hello **IMobileServiceSyncContext**. Hello contesto di sincronizzazione consente di mantenere le relazioni tra tabelle e di rilevamento e il push delle modifiche in tutte le tabelle modificato quando un'app client **PushAsync** viene chiamato.

    esempio Hello **SyncAsync** toosync con back-end App Mobile hello viene chiamato:

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    Questo esempio utilizza una semplice gestione degli errori con gestore di sincronizzazione predefinito hello. Un'applicazione reale si gestisce hello diversi errori, ad esempio le condizioni della rete e server è in conflitto con un oggetto personalizzato **IMobileServiceSyncHandler** implementazione.

## <a name="offline-sync-considerations"></a>Considerazioni sulla sincronizzazione offline
Nell'esempio hello hello **SyncAsync** metodo viene chiamato solo sull'avvio e quando è richiesta una sincronizzazione.  tooinitiate una sincronizzazione in un'app Android o iOS, pull verso il basso nell'elenco degli elementi hello; per Windows, utilizzare hello **sincronizzazione** pulsante. In un'applicazione reale, è possibile creare trigger di sincronizzazione hello quando cambia lo stato di rete hello.

Quando viene eseguita un'operazione di pull in una tabella che è in sospeso aggiornamenti locali registrati dal contesto hello, che pull operazione automaticamente i trigger di push contesto precedente. Quando l'aggiornamento, l'aggiunta e il completamento di elementi in questo esempio, è possibile omettere hello esplicita **PushAsync** chiamare.

Nel codice hello fornito, tutti i record nella tabella TodoItem remoto hello esecuzione di query, ma è anche possibile toofilter record passando un id di query e una query troppo**PushAsync**. Per ulteriori informazioni, vedere la sezione hello *sincronizzazione incrementale* in [non in linea sincronizzazione di dati in App mobili di Azure][2].

## <a name="run-hello-client-app"></a>Eseguire app di hello client
Con ora abilitata la sincronizzazione non in linea, eseguire un'applicazione hello client almeno una volta su ogni database dell'archivio locale hello toopopulate piattaforma. In un secondo momento, simulare uno scenario offline e modificare i dati di hello nell'archivio locale hello mentre l'applicazione hello è offline.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Aggiornare il comportamento di sincronizzazione hello di app client hello
In questa sezione, modificare hello client progetto toosimulate uno scenario offline tramite un URL dell'applicazione non valido per il back-end. In alternativa, è possibile disattivare le connessioni di rete spostando il dispositivo troppo "Modalità aereo".  Quando si aggiunge o modifica gli elementi di dati, queste modifiche sono contenute nell'archivio locale hello, ma non sincronizzate i dati di back-end toohello archiviano fino a quando non viene ristabilita la connessione di hello.

1. In hello Esplora soluzioni, aprire il file di progetto di hello Constants.cs da hello **portabile** del progetto e modificare il valore di hello di `ApplicationURL` URL non valido di toopoint tooan:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. File TodoItemManager.cs hello aperto da hello **portabile** del progetto, quindi aggiungere un **catch** per hello base **eccezione** toohello classe **try … catch** blocco **SyncAsync**. Questo **catch** blocco scrive console toohello di messaggio eccezione di hello, come indicato di seguito:

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Compilare ed eseguire l'applicazione client hello.  Aggiungere nuovi elementi. Si noti che un'eccezione viene registrata nella console di hello per ogni tentativo di toosync con hello di back-end. Questi nuovi elementi esistono solo nell'archivio locale di hello fino a quando non può essere di back-end mobile toohello inseriti. app client Hello si comporta come se fosse back-end connesso toohello, supporto che tutte di creazione, lettura, aggiornamento, le operazioni di eliminazione (CRUD).
4. Chiudere l'applicazione hello e riavviarlo tooverify che è stato creato in base ai nuovi elementi hello siano archivio locale toohello persistente.
5. (Facoltativo) Utilizzare Visual Studio tooview toosee di tabella del Database SQL di Azure che hello dati nel database back-end hello non vengono modificati.

    In Visual Studio aprire **Esplora server**. Esplorare database tooyour **Azure**->**database SQL**. Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**. È possibile cercare tooyour tabella di database SQL e il relativo contenuto.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Aggiornare hello client app tooreconnect back-end per dispositivi mobili
In questa sezione, riconnettersi hello app toohello mobile back-end, che simula l'applicazione hello confermata tooan di stato online. Quando si esegue l'azione di aggiornamento hello, i dati sono back-end mobile tooyour sincronizzati.

1. Riaprire il file Constants.cs. Hello corretto `applicationURL` toopoint toohello correggere URL.
2. Ricompilare ed eseguire l'applicazione client hello. app Hello tenta toosync con back-end dell'app mobile hello dopo l'avvio. Verificare che nessuna eccezione vengono registrata nella console di debug hello.
3. (Facoltativo) Hello visualizzazione aggiornata dei dati utilizzando Esplora oggetti di SQL Server o uno strumento REST come Fiddler o [Postman][6]. Si noti hello dati sono stati sincronizzati tra i database di back-end hello e archivio locale hello.

    Avviso hello dati sincronizzati tra database hello e archivio locale hello e contiene elementi hello che aggiunti mentre l'app è stata disconnessa.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure][2]
* [Procedura per .NET SDK di App per dispositivi mobili di Azure][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
