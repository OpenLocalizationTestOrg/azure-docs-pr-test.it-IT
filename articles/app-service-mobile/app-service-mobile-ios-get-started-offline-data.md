---
title: sincronizzazione non in linea aaaEnable con App per dispositivi mobili iOS | Documenti Microsoft
description: Informazioni su come toouse Azure App Service App per dispositivi mobili toocache e sincronizzazione dati offline nelle applicazioni iOS.
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Sincronizzare offline le app per dispositivi mobili iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione vengono illustrate la sincronizzazione non in linea con le funzionalità di App per dispositivi mobili hello di servizio App di Azure per iOS. Con gli utenti finali di sincronizzazione non in linea possono interagire con un tooview app per dispositivi mobili, aggiungere o modificare i dati, anche quando non dispongono di alcuna connessione di rete. Le modifiche vengono archiviate in un database locale. Dopo che il dispositivo di hello è online, le modifiche di hello vengono sincronizzate con hello remoto back-end.

Se questa è la prima esperienza con App per dispositivi mobili, è necessario completare prima esercitazione hello [crea un'App iOS]. Se non si utilizza il progetto di avvio rapido server hello scaricato, è necessario aggiungere il progetto tooyour pacchetti di hello accesso ai dati estensione. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere [sincronizzazione dati Offline nelle App per dispositivi mobili].

## <a name="review-sync"></a>Esaminare il codice di sincronizzazione client hello
progetto client Hello scaricati per hello [crea un'App iOS] esercitazione contiene già codice che supporta la sincronizzazione non in linea utilizzando un database locale basato su dati di base. Questa sezione vengono riepilogati gli elementi che è già inclusi nel codice dell'esercitazione hello. Per informazioni generali sulla funzionalità hello, vedere [sincronizzazione dati Offline nelle App per dispositivi mobili].

Tramite funzionalità di sincronizzazione di dati non in linea di hello di App per dispositivi mobili, gli utenti finali possono interagire con un database locale anche quando la rete hello è inaccessibile. toouse queste funzionalità nell'applicazione, inizializzare il contesto di sincronizzazione hello di `MSClient` e fare riferimento a un archivio locale. Quindi si fa riferimento la tabella tramite hello **MSSyncTable** interfaccia.

In **QSTodoService.m** (Objective-C) o **ToDoTableViewController.swift** (Agile), si noti che il tipo di membro hello hello **syncTable** è  **MSSyncTable**. La sincronizzazione offline usa questa interfaccia della tabella di sincronizzazione al posto di **MSTable**. Quando si utilizza una tabella di sincronizzazione, tutte le operazioni passare archivio locale toohello e vengono sincronizzate solo con hello remoto back-end con esplicita push e pull operazioni.

 tooget una tabella di riferimento tooa sincronizzazione, utilizzare hello **syncTableWithName** metodo `MSClient`. la funzionalità di sincronizzazione non in linea di tooremove, utilizzare **tableWithName** invece.

Prima di possono eseguire qualsiasi operazione di tabella, è necessario inizializzare l'archivio locale hello. Ecco il codice pertinente hello:

* **Objective-C**: In hello **QSTodoService.init** metodo:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Swift**: In hello **ToDoTableViewController.viewDidLoad** metodo:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Questo metodo crea un archivio locale tramite hello `MSCoreDataStore` fornisce l'interfaccia che hello Mobile App SDK. In alternativa, è possibile fornire un archivio locale diverso implementando hello `MSSyncContextDataSource` protocollo. Inoltre, hello primo parametro di **MSSyncContext** è toospecify utilizzato un gestore del conflitto. Perché è stato passato `nil`, si ottiene gestore di conflitti di hello predefinito, non riesce in eventuali conflitti.

A questo punto, consente un'operazione di sincronizzazione effettivo hello e ottenere dati dal back-end hello remoto:

* **Objective-C**: `syncData`Invia le nuove modifiche e quindi chiama **pullData** dati tooget dal back-end hello remoto. A sua volta, hello **pullData** metodo consente di ottenere nuovi dati che corrispondono a una query:

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* **Swift**:
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

Nella versione di hello Objective-C, in `syncData`, viene innanzitutto chiamato **pushWithCompletion** nel contesto di sincronizzazione hello. Questo metodo è un membro di `MSSyncContext` (e non hello sincronizzazione tabella) Poiché inserisce le modifiche apportate in tutte le tabelle. Solo i record che sono stati modificati in qualche modo localmente (tramite le operazioni CUD) vengono inviati toohello server. Quindi hello helper **pullData** viene chiamato, che chiama **MSSyncTable.pullWithQuery** dati remoti tooretrieve e archiviarla nel database locale hello.

Nella versione Swift hello, perché l'operazione di push hello non sia strettamente necessario, non vi è alcuna chiamata troppo**pushWithCompletion**. Se sono state apportate modifiche in sospeso nel contesto di sincronizzazione hello per tabella hello che esegue un'operazione push, pull genera sempre prima di push. Tuttavia, se si dispone di più di una tabella di sincronizzazione, è migliore tooexplicitly chiamata push tooensure che tutto sia coerenza tra le tabelle correlate.

In hello Objective-C e nelle versioni Swift, è possibile utilizzare hello **pullWithQuery** toospecify metodo toofilter una query hello record che si desidera tooretrieve. In questo esempio, query hello recupera tutti i record di hello remoto `TodoItem` tabella.

secondo parametro di Hello **pullWithQuery** è un ID di query che viene utilizzato per *sincronizzazione incrementale*. Sincronizzazione incrementale recupera solo i record che sono stati modificati dall'ultima sincronizzazione hello, utilizzo del record hello `UpdatedAt` timestamp (chiamato `updatedAt` nell'archivio locale di hello.) hello query ID deve essere una stringa descrittiva che è univoca per ogni query nella logica l'app. tooopt non sincronizzati incrementale, passare `nil` come hello ID di query. Questo approccio può potenzialmente non essere efficiente, perché recupera tutti i record ad ogni operazione pull.

app di Hello Objective-C esegue la sincronizzazione quando si modifica o aggiungere dati, quando un utente esegue l'azione di aggiornamento hello e all'avvio.

Consente di sincronizzare Hello Swift app quando l'utente hello esegue l'azione di aggiornamento hello e all'avvio.

Sincronizzazioni app ogni volta che i dati sono hello modificato (Objective-C) o ogni volta che l'applicazione hello all'avvio (Objective-C e Swift), applicazione hello presuppone che l'utente hello è online. In una sezione successiva, si aggiornerà app hello in modo che gli utenti possono modificare anche quando sono in linea.

## <a name="review-core-data"></a>Modello di dati principali hello revisione
Quando si utilizza l'archivio non in linea di hello dati principali, è necessario definire tabelle specifiche e i campi nel modello di dati. app di esempio Hello include già un modello di dati con formato corretto hello. In questa sezione vengono illustrate le tooshow tali tabelle le modalità di utilizzo.

Aprire **QSDataModel.xcdatamodeld**. Sono quattro tabelle definito tre utilizzati da hello SDK e uno che viene utilizzato per attività hello voci:
  * MS_TableOperations: Tracce hello elementi che richiedono toobe sincronizzati con il server di hello.
  * MS_TableOperationErrors: tiene traccia di eventuali errori che si verificano durante la sincronizzazione offline.
  * MS_TableConfig: Tracce hello ora dell'ultimo aggiornamento per l'operazione di sincronizzazione per tutte le operazioni pull ultimo hello.
  * TodoItem: Archivia gli elementi di attività da eseguire hello. le colonne di sistema di Hello **createdAt**, **updatedAt**, e **versione** sono proprietà di sistema facoltativo.

> [!NOTE]
> Hello Mobile App SDK riserva i nomi di colonna che iniziano con "**``**". Usare questo prefisso solo per le colonne di sistema. In caso contrario, i nomi di colonna vengono modificati quando si utilizza hello remoto back-end.
>
>

Quando si utilizza la funzionalità di sincronizzazione non in linea hello, definire tre tabelle di sistema hello e una tabella di dati hello.

### <a name="system-tables"></a>Tabelle di sistema

**MS_TableOperations**  

![Attributi della tabella MS_TableOperations][defining-core-data-tableoperations-entity]

| Attributo | Tipo |
| --- | --- |
| id | Valore integer 64 |
| itemId | String |
| properties | Dati binari |
| tabella | String |
| tableKind | Integer 16 |


**MS_TableOperationErrors**

 ![Attributi della tabella MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| Attributo | Tipo |
| --- | --- |
| id |String |
| operationId |Valore integer 64 |
| properties |Dati binari |
| tableKind |Integer 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Attributo | Tipo |
| --- | --- |
| id |String |
| key |String |
| keyType |Valore integer 64 |
| tabella |String |
| value |String |

### <a name="data-table"></a>Tabella dati

**TodoItem**

| Attributo | Tipo | Nota |
| --- | --- | --- |
| id | Stringa, contrassegnata come obbligatoria |chiave primaria nell'archivio remoto |
| complete | Boolean | campo elemento ToDo |
| text |String |campo elemento ToDo |
| createdAt | Date | (facoltativo) Esegue il mapping troppo**createdAt** proprietà di sistema |
| updatedAt | Date | (facoltativo) Esegue il mapping troppo**updatedAt** proprietà di sistema |
| version | String | (facoltativo) È in conflitto toodetect usato, tooversion mappe |

## <a name="setup-sync"></a>Modificare il comportamento di sincronizzazione hello di hello app
In questa sezione è modificare app hello in modo che non sincronizza avvio dell'app o quando si inserisce e aggiornare gli elementi. Viene eseguita la sincronizzazione solo quando viene eseguita pulsante di azione di aggiornamento hello.

**Objective-C**:

1. In **QSTodoListViewController.m**, modificare hello **viewDidLoad** tooremove metodo hello chiamata troppo`[self refresh]` alla fine di hello del metodo hello. Dati hello ora non è sincronizzati con il server di hello all'avvio dell'app. Invece viene sincronizzata con il contenuto di hello dell'archivio locale di hello.
2. In **QSTodoService.m**, modificare la definizione di hello `addItem` in modo che non sincronizzato dopo l'inserimento dell'elemento hello. Rimuovere hello `self syncData` blocco e sostituirlo con il seguente hello:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Modificare la definizione di hello `completeItem` come indicato in precedenza. Rimuovere il blocco di hello per `self syncData` e sostituirlo con il seguente hello:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**Swift**:

In `viewDidLoad`nella **ToDoTableViewController.swift**, impostare come commento le righe di due hello riportati di seguito, toostop la sincronizzazione all'avvio dell'app. In fase di hello della redazione del presente documento, app Todo Swift hello non aggiorna servizio hello quando un utente aggiunge o completato un elemento. Aggiorna servizio hello solo all'avvio di app.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Test hello app
In questa sezione è connettersi toosimulate URL non valido di tooan uno scenario non in linea. Quando si aggiungono elementi di dati, si è mantenuti in hello archivio locale dei dati di base, ma non è sincronizzati con hello app mobile back-end.

1. Modifica URL di app per dispositivi mobili hello in **QSTodoService.m** tooan URL non valido e nuovamente l'applicazione hello esecuzione:

   **Objective-C**: In QSTodoService.m:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Swift**: In ToDoTableViewController.swift:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Aggiungere alcuni elementi attività. Chiudere il simulatore hello (o app hello chiusura forzata) e quindi riavviarlo. Verificare che le modifiche siano state conservate.

3. Visualizzare il contenuto di hello di hello remoto **TodoItem** tabella:
   * Per un back-end di Node.js, visitare toohello [portale di Azure](https://portal.azure.com/) e il back-end di app per dispositivi mobili, fare clic su **tabelle facile** > **TodoItem**.  
   * Per il back-end .NET, usare uno strumento SQL, quale ad esempio SQL Server Management Studio, oppure un client REST, quale ad esempio Fiddler o Postman.  

4. Verificare che dispongano di nuovi elementi hello *non* stato sincronizzato con il server di hello.

5. Modifica hello URL nascosto toohello correggere uno in **QSTodoService.m**e app hello eseguire di nuovo.

6. Eseguire l'operazione di aggiornamento di hello trascinando verso il basso elenco hello degli elementi.  
Verrà visualizzato un indicatore di avanzamento.

7. Hello vista **TodoItem** nuovamente i dati. gli elementi di attività nuove e modificate di Hello dovrebbero essere ora visualizzati.

## <a name="summary"></a>Riepilogo
funzionalità di sincronizzazione non in linea toosupport hello, abbiamo utilizzato hello `MSSyncTable` l'interfaccia e inizializzato `MSClient.syncContext` con un archivio locale. In questo caso, archivio locale hello è un database basato su dati di base.

Quando si utilizza un archivio locale dei dati di base, è necessario definire più tabelle con hello [correggere le proprietà di sistema](#review-core-data).

normale Hello creare, leggere, aggiornare ed eliminazione (CRUD) per il lavoro App per dispositivi mobili, come se l'applicazione hello è ancora connesso, ma si verificano tutte le operazioni di hello sull'archivio locale hello.

Quando l'archivio locale hello è sincronizzato con server hello, abbiamo utilizzato hello **MSSyncTable.pullWithQuery** metodo.

## <a name="additional-resources"></a>Risorse aggiuntive
* [sincronizzazione dati Offline nelle App per dispositivi mobili]
* [Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure] \(hello video è servizi mobili, ma non in linea App per dispositivi mobili funziona la sincronizzazione in modo analogo.\)

<!-- URLs. -->


[crea un'App iOS]: app-service-mobile-ios-get-started.md
[sincronizzazione dati Offline nelle App per dispositivi mobili]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
