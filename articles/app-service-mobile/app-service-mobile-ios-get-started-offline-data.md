---
title: Abilitare la sincronizzazione offline con le app per dispositivi mobili per iOS | Documentazione Microsoft
description: Informazioni su come usare le app per dispositivi mobili del servizio app di Azure per memorizzare i dati nella cache e sincronizzarli offline nelle app iOS.
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
ms.openlocfilehash: 44c0d26b2d7d28322d436d4bda319d728c31a635
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="5f9d4-103">Sincronizzare offline le app per dispositivi mobili iOS</span><span class="sxs-lookup"><span data-stu-id="5f9d4-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="5f9d4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5f9d4-104">Overview</span></span>
<span data-ttu-id="5f9d4-105">Questa esercitazione illustra come eseguire la sincronizzazione offline con la funzionalità App per dispositivi mobili di Servizio app di Azure per iOS.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="5f9d4-106">La sincronizzazione offline consente agli utenti finali di usare un'app per dispositivi mobili per visualizzare, aggiungere o modificare dati anche in assenza di una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="5f9d4-107">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-107">Changes are stored in a local database.</span></span> <span data-ttu-id="5f9d4-108">Quando il dispositivo viene connesso nuovamente alla rete, le modifiche vengono sincronizzate con il back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="5f9d4-109">Se questa è la prima esperienza con la funzionalità App per dispositivi mobili, è consigliabile completare prima l'esercitazione [Creare un'app iOS].</span><span class="sxs-lookup"><span data-stu-id="5f9d4-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="5f9d4-110">Se non si usa il progetto server di avvio rapido scaricato, è necessario aggiungere al progetto i pacchetti di estensione per l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="5f9d4-111">Per altre informazioni sui pacchetti di estensione server, vedere l'articolo relativo all' [utilizzo dell'SDK del server back-end .NET per app per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5f9d4-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="5f9d4-112">Per altre informazioni sulla funzionalità di sincronizzazione offline, vedere l'argomento [Sincronizzazione di dati offline nelle app per dispositivi mobili].</span><span class="sxs-lookup"><span data-stu-id="5f9d4-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="5f9d4-113"><a name="review-sync"></a>Verificare il codice di sincronizzazione del client</span><span class="sxs-lookup"><span data-stu-id="5f9d4-113"><a name="review-sync"></a>Review the client sync code</span></span>
<span data-ttu-id="5f9d4-114">Il progetto client scaricato per l'esercitazione [Creare un'app iOS] contiene già il codice che supporta la sincronizzazione offline mediante un database basato sui dati principali locali.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="5f9d4-115">Questa sezione riepiloga gli elementi già inclusi nel codice dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="5f9d4-116">Per una panoramica concettuale della funzionalità, vedere [Sincronizzazione di dati offline nelle app per dispositivi mobili].</span><span class="sxs-lookup"><span data-stu-id="5f9d4-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="5f9d4-117">La funzionalità di sincronizzazione dei dati offline di App per dispositivi mobili consente agli utenti finali di interagire con un database locale quando la rete non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="5f9d4-118">Per usare queste funzionalità nell'app, è possibile inizializzare il contesto di sincronizzazione di `MSClient` e fare riferimento a un archivio locale.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="5f9d4-119">Fare quindi riferimento alla tabella tramite l'interfaccia **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="5f9d4-120">In **QSTodoService.m** (Objective-C) o **ToDoTableViewController.swift** (Swift) si noti che il tipo del membro **syncTable** è **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="5f9d4-121">La sincronizzazione offline usa questa interfaccia della tabella di sincronizzazione al posto di **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="5f9d4-122">Quando si usa una tabella di sincronizzazione, tutte le operazioni vengono inviate all'archivio locale e vengono sincronizzate con il back-end remoto solo mediante operazioni push e pull esplicite.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="5f9d4-123">Per ottenere un riferimento a una tabella di sincronizzazione, usare il metodo **syncTableWithName** su `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="5f9d4-124">Per rimuovere la funzionalità di sincronizzazione offline, usare invece **tableWithName**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="5f9d4-125">Prima di poter eseguire qualsiasi operazione su tabella, è necessario inizializzare l'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="5f9d4-126">Di seguito è riportato il codice pertinente.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-126">Here is the relevant code:</span></span>

* <span data-ttu-id="5f9d4-127">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-127">**Objective-C**.</span></span> <span data-ttu-id="5f9d4-128">Nel metodo **QSTodoService.init**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="5f9d4-129">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-129">**Swift**.</span></span> <span data-ttu-id="5f9d4-130">Nel metodo **ToDoTableViewController.viewDidLoad**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="5f9d4-131">Questo metodo crea un archivio locale usando l'interfaccia `MSCoreDataStore`, disponibile in Mobile Apps SDK.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="5f9d4-132">È anche possibile fornire un archivio locale differente, implementando il protocollo `MSSyncContextDataSource`.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="5f9d4-133">Il primo parametro di **MSSyncContext** viene usato per specificare un gestore di conflitti.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="5f9d4-134">Poiché è stato passato `nil`, si otterrà il gestore di conflitti predefinito, che non consente l'esecuzione di operazioni in caso di conflitto.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="5f9d4-135">A questo punto, si esegue l'operazione effettiva di sincronizzazione e si ottengono i dati dal back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="5f9d4-136">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-136">**Objective-C**.</span></span> <span data-ttu-id="5f9d4-137">`syncData` effettua innanzitutto il push delle nuove modifiche e quindi chiama il metodo **pullData** per ottenere i dati dal back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="5f9d4-138">A sua volta, il metodo **pullData** ottiene nuovi dati che corrispondono a una query:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="5f9d4-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="5f9d4-140">Nella versione Objective-C, in `syncData`, viene innanzitutto chiamato il metodo **pushWithCompletion** nel contesto di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="5f9d4-141">Questo metodo fa parte di `MSSyncContext` (e non della tabella di sincronizzazione) perché effettua il push delle modifiche in tutte le tabelle.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="5f9d4-142">Solo i record che sono stati in qualche modo modificati localmente (tramite le operazioni CUD) vengono inviati al server.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="5f9d4-143">Viene quindi chiamato l'helper **pullData**, che chiama **MSSyncTable.pullWithQuery** per recuperare i dati remoti e memorizzarli nel database locale.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="5f9d4-144">Nella versione Swift, poiché l'operazione push non è strettamente necessaria, non vi è alcuna chiamata a **pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="5f9d4-145">Se nel contesto di sincronizzazione per la tabella che esegue un'operazione push sono presenti modifiche in sospeso, pull effettua sempre prima un'operazione push.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="5f9d4-146">Tuttavia, se sono presenti più tabelle di sincronizzazione, è preferibile chiamare in modo esplicito il push per garantire la coerenza tra le tabelle correlate.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="5f9d4-147">Sia nella versione Objective-C che nella versione Swift, è possibile usare il metodo **pullWithQuery** per specificare una query per filtrare i record da recuperare.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="5f9d4-148">In questo esempio, la query recupera tutti i record nella tabella `TodoItem` remota.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="5f9d4-149">Il secondo parametro di **pullWithQuery** è un ID di query che viene usato per la *sincronizzazione incrementale*.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*.</span></span> <span data-ttu-id="5f9d4-150">La sincronizzazione incrementale recupera solo i record che sono stati modificati dopo l'ultima sincronizzazione, usando il timestamp `UpdatedAt` del record denominato `updatedAt` nell'archivio locale. L'ID di query deve essere una stringa descrittiva univoca per ogni query logica presente nell'app.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-150">Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="5f9d4-151">Per rifiutare esplicitamente la sincronizzazione incrementale, passare `nil` come ID di query.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-151">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="5f9d4-152">Questo approccio può potenzialmente non essere efficiente, perché recupera tutti i record ad ogni operazione pull.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-152">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="5f9d4-153">L'app Objective-C esegue la sincronizzazione quando si modificano o si aggiungono dati, quando un utente esegue l'aggiornamento e all'avvio.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-153">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="5f9d4-154">L'app Swift esegue la sincronizzazione quando l'utente esegue l'aggiornamento e all'avvio.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-154">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="5f9d4-155">Poiché l'app esegue la sincronizzazione ogni volta che i dati vengono modificati (Objective-C) oppure a ogni avvio dell'applicazione (Objective-C e Swift), l'app presuppone che l'utente sia online.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-155">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="5f9d4-156">In un'altra sezione, l'app verrà aggiornata in modo che gli utenti possano apportare modifiche anche quando sono offline.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-156">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="5f9d4-157"><a name="review-core-data"></a>Esaminare il modello di Core Data</span><span class="sxs-lookup"><span data-stu-id="5f9d4-157"><a name="review-core-data"></a>Review the Core Data model</span></span>
<span data-ttu-id="5f9d4-158">Quando si usa l'archivio offline Core Data, è necessario definire particolari tabelle e campi all'interno del modello di dati.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-158">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="5f9d4-159">L'app di esempio include già un modello di dati nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-159">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="5f9d4-160">Questa sezione illustra le tabelle e il relativo uso.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-160">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="5f9d4-161">Aprire **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-161">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="5f9d4-162">Qui sono definite quattro tabelle, tre usate dall'SDK e una per gli elementi attività:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-162">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="5f9d4-163">MS_TableOperations: tiene traccia degli elementi da sincronizzare con il server.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-163">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="5f9d4-164">MS_TableOperationErrors: tiene traccia di eventuali errori che si verificano durante la sincronizzazione offline.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-164">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="5f9d4-165">MS_TableConfig: tiene traccia dell'ora dell'ultimo aggiornamento dell'ultima operazione di sincronizzazione per tutte le operazioni pull.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-165">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="5f9d4-166">TodoItem: archivia gli elementi attività.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-166">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="5f9d4-167">Le colonne di sistema **createdAt**, **updatedAt** e **version** sono proprietà di sistema facoltative.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-167">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="5f9d4-168">Mobile Apps SDK si riserva i nomi di colonna che iniziano con "**``**".</span><span class="sxs-lookup"><span data-stu-id="5f9d4-168">The Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="5f9d4-169">Usare questo prefisso solo per le colonne di sistema.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-169">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="5f9d4-170">In caso contrario, quando si usa il back-end remoto, i nomi di colonna vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-170">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="5f9d4-171">Quando si usa la funzionalità di sincronizzazione offline, definire le tre tabelle di sistema e la tabella dati.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-171">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="5f9d4-172">Tabelle di sistema</span><span class="sxs-lookup"><span data-stu-id="5f9d4-172">System tables</span></span>

<span data-ttu-id="5f9d4-173">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-173">**MS_TableOperations**</span></span>  

![Attributi della tabella MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="5f9d4-175">Attributo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-175">Attribute</span></span> | <span data-ttu-id="5f9d4-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-176">Type</span></span> |
| --- | --- |
| <span data-ttu-id="5f9d4-177">id</span><span class="sxs-lookup"><span data-stu-id="5f9d4-177">id</span></span> | <span data-ttu-id="5f9d4-178">Valore integer 64</span><span class="sxs-lookup"><span data-stu-id="5f9d4-178">Integer 64</span></span> |
| <span data-ttu-id="5f9d4-179">itemId</span><span class="sxs-lookup"><span data-stu-id="5f9d4-179">itemId</span></span> | <span data-ttu-id="5f9d4-180">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-180">String</span></span> |
| <span data-ttu-id="5f9d4-181">properties</span><span class="sxs-lookup"><span data-stu-id="5f9d4-181">properties</span></span> | <span data-ttu-id="5f9d4-182">Dati binari</span><span class="sxs-lookup"><span data-stu-id="5f9d4-182">Binary Data</span></span> |
| <span data-ttu-id="5f9d4-183">tabella</span><span class="sxs-lookup"><span data-stu-id="5f9d4-183">table</span></span> | <span data-ttu-id="5f9d4-184">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-184">String</span></span> |
| <span data-ttu-id="5f9d4-185">tableKind</span><span class="sxs-lookup"><span data-stu-id="5f9d4-185">tableKind</span></span> | <span data-ttu-id="5f9d4-186">Integer 16</span><span class="sxs-lookup"><span data-stu-id="5f9d4-186">Integer 16</span></span> |


<span data-ttu-id="5f9d4-187">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-187">**MS_TableOperationErrors**</span></span>

 ![Attributi della tabella MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="5f9d4-189">Attributo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-189">Attribute</span></span> | <span data-ttu-id="5f9d4-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-190">Type</span></span> |
| --- | --- |
| <span data-ttu-id="5f9d4-191">id</span><span class="sxs-lookup"><span data-stu-id="5f9d4-191">id</span></span> |<span data-ttu-id="5f9d4-192">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-192">String</span></span> |
| <span data-ttu-id="5f9d4-193">operationId</span><span class="sxs-lookup"><span data-stu-id="5f9d4-193">operationId</span></span> |<span data-ttu-id="5f9d4-194">Valore integer 64</span><span class="sxs-lookup"><span data-stu-id="5f9d4-194">Integer 64</span></span> |
| <span data-ttu-id="5f9d4-195">properties</span><span class="sxs-lookup"><span data-stu-id="5f9d4-195">properties</span></span> |<span data-ttu-id="5f9d4-196">Dati binari</span><span class="sxs-lookup"><span data-stu-id="5f9d4-196">Binary Data</span></span> |
| <span data-ttu-id="5f9d4-197">tableKind</span><span class="sxs-lookup"><span data-stu-id="5f9d4-197">tableKind</span></span> |<span data-ttu-id="5f9d4-198">Integer 16</span><span class="sxs-lookup"><span data-stu-id="5f9d4-198">Integer 16</span></span> |

 <span data-ttu-id="5f9d4-199">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-199">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="5f9d4-200">Attributo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-200">Attribute</span></span> | <span data-ttu-id="5f9d4-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-201">Type</span></span> |
| --- | --- |
| <span data-ttu-id="5f9d4-202">id</span><span class="sxs-lookup"><span data-stu-id="5f9d4-202">id</span></span> |<span data-ttu-id="5f9d4-203">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-203">String</span></span> |
| <span data-ttu-id="5f9d4-204">key</span><span class="sxs-lookup"><span data-stu-id="5f9d4-204">key</span></span> |<span data-ttu-id="5f9d4-205">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-205">String</span></span> |
| <span data-ttu-id="5f9d4-206">keyType</span><span class="sxs-lookup"><span data-stu-id="5f9d4-206">keyType</span></span> |<span data-ttu-id="5f9d4-207">Valore integer 64</span><span class="sxs-lookup"><span data-stu-id="5f9d4-207">Integer 64</span></span> |
| <span data-ttu-id="5f9d4-208">tabella</span><span class="sxs-lookup"><span data-stu-id="5f9d4-208">table</span></span> |<span data-ttu-id="5f9d4-209">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-209">String</span></span> |
| <span data-ttu-id="5f9d4-210">value</span><span class="sxs-lookup"><span data-stu-id="5f9d4-210">value</span></span> |<span data-ttu-id="5f9d4-211">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-211">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="5f9d4-212">Tabella dati</span><span class="sxs-lookup"><span data-stu-id="5f9d4-212">Data table</span></span>

<span data-ttu-id="5f9d4-213">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-213">**TodoItem**</span></span>

| <span data-ttu-id="5f9d4-214">Attributo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-214">Attribute</span></span> | <span data-ttu-id="5f9d4-215">Tipo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-215">Type</span></span> | <span data-ttu-id="5f9d4-216">Nota</span><span class="sxs-lookup"><span data-stu-id="5f9d4-216">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f9d4-217">id</span><span class="sxs-lookup"><span data-stu-id="5f9d4-217">id</span></span> | <span data-ttu-id="5f9d4-218">Stringa, contrassegnata come obbligatoria</span><span class="sxs-lookup"><span data-stu-id="5f9d4-218">String, marked required</span></span> |<span data-ttu-id="5f9d4-219">chiave primaria nell'archivio remoto</span><span class="sxs-lookup"><span data-stu-id="5f9d4-219">Primary key in remote store</span></span> |
| <span data-ttu-id="5f9d4-220">complete</span><span class="sxs-lookup"><span data-stu-id="5f9d4-220">complete</span></span> | <span data-ttu-id="5f9d4-221">Boolean</span><span class="sxs-lookup"><span data-stu-id="5f9d4-221">Boolean</span></span> | <span data-ttu-id="5f9d4-222">campo elemento ToDo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-222">To-do item field</span></span> |
| <span data-ttu-id="5f9d4-223">text</span><span class="sxs-lookup"><span data-stu-id="5f9d4-223">text</span></span> |<span data-ttu-id="5f9d4-224">String</span><span class="sxs-lookup"><span data-stu-id="5f9d4-224">String</span></span> |<span data-ttu-id="5f9d4-225">campo elemento ToDo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-225">To-do item field</span></span> |
| <span data-ttu-id="5f9d4-226">createdAt</span><span class="sxs-lookup"><span data-stu-id="5f9d4-226">createdAt</span></span> | <span data-ttu-id="5f9d4-227">Data</span><span class="sxs-lookup"><span data-stu-id="5f9d4-227">Date</span></span> | <span data-ttu-id="5f9d4-228">(facoltativo) viene mappato alla proprietà di sistema **createdAt**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-228">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="5f9d4-229">updatedAt</span><span class="sxs-lookup"><span data-stu-id="5f9d4-229">updatedAt</span></span> | <span data-ttu-id="5f9d4-230">Data</span><span class="sxs-lookup"><span data-stu-id="5f9d4-230">Date</span></span> | <span data-ttu-id="5f9d4-231">(facoltativo) viene mappato alla proprietà di sistema **updatedAt**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-231">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="5f9d4-232">version</span><span class="sxs-lookup"><span data-stu-id="5f9d4-232">version</span></span> | <span data-ttu-id="5f9d4-233">string</span><span class="sxs-lookup"><span data-stu-id="5f9d4-233">String</span></span> | <span data-ttu-id="5f9d4-234">(facoltativo) viene usato per il rilevamento dei conflitti, viene mappato a version</span><span class="sxs-lookup"><span data-stu-id="5f9d4-234">(optional) Used to detect conflicts, maps to version</span></span> |

## <span data-ttu-id="5f9d4-235"><a name="setup-sync"></a>Modificare il comportamento di sincronizzazione dell'app</span><span class="sxs-lookup"><span data-stu-id="5f9d4-235"><a name="setup-sync"></a>Change the sync behavior of the app</span></span>
<span data-ttu-id="5f9d4-236">In questa sezione si modifica l'app in modo che non esegua la sincronizzazione all'avvio o quando si inseriscono e si aggiornano elementi,</span><span class="sxs-lookup"><span data-stu-id="5f9d4-236">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="5f9d4-237">bensì solo quando si seleziona il pulsante di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-237">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="5f9d4-238">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-238">**Objective-C**:</span></span>

1. <span data-ttu-id="5f9d4-239">In **QSTodoListViewController.m** modificare il metodo **viewDidLoad** per rimuovere la chiamata a `[self refresh]` alla fine del metodo.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-239">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="5f9d4-240">A questo punto i dati non vengono sincronizzati con il server all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-240">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="5f9d4-241">Sono invece sincronizzati con il contenuto dell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-241">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="5f9d4-242">In **QSTodoService.m** modificare la definizione di `addItem` in modo che non esegua la sincronizzazione dopo l'inserimento dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-242">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="5f9d4-243">Rimuovere il blocco `self syncData` e sostituirlo con quanto segue:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-243">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="5f9d4-244">Modificare la definizione di `completeItem` come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-244">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="5f9d4-245">Rimuovere il blocco per `self syncData` e sostituirlo con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-245">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="5f9d4-246">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-246">**Swift**:</span></span>

<span data-ttu-id="5f9d4-247">In `viewDidLoad` in **ToDoTableViewController.swift** impostare un commento per queste due righe per interrompere la sincronizzazione all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-247">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="5f9d4-248">Al momento della stesura di questo articolo, l'app Swift Todo non aggiorna il servizio quando un utente aggiunge o completa un elemento.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-248">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="5f9d4-249">Aggiorna il servizio solo all'avvio.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-249">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="5f9d4-250"><a name="test-app"></a>Test dell'app</span><span class="sxs-lookup"><span data-stu-id="5f9d4-250"><a name="test-app"></a>Test the app</span></span>
<span data-ttu-id="5f9d4-251">In questa sezione, ci si collega a un URL non valido per simulare uno scenario offline.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-251">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="5f9d4-252">Quando si aggiungono elementi di dati, questi vengono conservati nell'archivio Core Data locale, ma non vengono sincronizzati con il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-252">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="5f9d4-253">Modificare l'URL dell'app per dispositivi mobili in **QSTodoService.m** con un URL non valido ed eseguire di nuovo l'app:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-253">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="5f9d4-254">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-254">**Objective-C**.</span></span> <span data-ttu-id="5f9d4-255">In QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-255">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="5f9d4-256">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-256">**Swift**.</span></span> <span data-ttu-id="5f9d4-257">In ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-257">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="5f9d4-258">Aggiungere alcuni elementi attività.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-258">Add some to-do items.</span></span> <span data-ttu-id="5f9d4-259">Uscire dal simulatore (o forzare la chiusura dell'app) e riavviare.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-259">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="5f9d4-260">Verificare che le modifiche siano state conservate.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-260">Verify that your changes persist.</span></span>

3. <span data-ttu-id="5f9d4-261">Visualizzare il contenuto della tabella **TodoItem** remota:</span><span class="sxs-lookup"><span data-stu-id="5f9d4-261">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="5f9d4-262">Per un back-end Node.js, passare al [portale di Azure](https://portal.azure.com/) e nel back-end dell'app per dispositivi mobili fare clic su **Tabelle semplici** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-262">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="5f9d4-263">Per il back-end .NET, usare uno strumento SQL, quale ad esempio SQL Server Management Studio, oppure un client REST, quale ad esempio Fiddler o Postman.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-263">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="5f9d4-264">Verificare che i nuovi elementi *non* siano stati sincronizzati con il server.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-264">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="5f9d4-265">Ripristinare l'URL corretto in **QSTodoService.m** ed eseguire di nuovo l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-265">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="5f9d4-266">Eseguire il movimento di aggiornamento spostando verso il basso l'elenco di elementi.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-266">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="5f9d4-267">Verrà visualizzato un indicatore di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-267">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="5f9d4-268">Visualizzare nuovamente i dati di **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-268">View the **TodoItem** data again.</span></span> <span data-ttu-id="5f9d4-269">Gli elementi attività nuovi e modificati dovrebbero essere a questo punto visualizzati.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-269">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="5f9d4-270">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5f9d4-270">Summary</span></span>
<span data-ttu-id="5f9d4-271">Per supportare la funzionalità di sincronizzazione offline è stata usata l'interfaccia `MSSyncTable` ed è stato inizializzato `MSClient.syncContext` con un archivio locale.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-271">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="5f9d4-272">In questo caso l'archivio locale era un database basato su Core Data.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-272">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="5f9d4-273">Quando si usa un archivio locale Core Data, è necessario definire varie tabelle con le [proprietà di sistema corrette](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="5f9d4-273">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="5f9d4-274">Le normali operazioni CRUD (create, read, update, delete) per le app per dispositivi mobili funzionano come se l'app fosse connessa alla rete, ma tutte le operazioni si verificano nell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-274">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="5f9d4-275">Quando l'archivio locale è stato sincronizzato con il server, è stato usato il metodo **MSSyncTable.pullWithQuery**.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-275">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f9d4-276">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5f9d4-276">Additional resources</span></span>
* <span data-ttu-id="5f9d4-277">[Sincronizzazione di dati offline nelle app per dispositivi mobili]</span><span class="sxs-lookup"><span data-stu-id="5f9d4-277">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="5f9d4-278">[Cloud Cover: Sincronizzazione offline in Servizi mobili di Azure] \(Il video è relativo a Servizi mobili, ma la sincronizzazione offline delle app per dispositivi mobili funziona in modo analogo.\)</span><span class="sxs-lookup"><span data-stu-id="5f9d4-278">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


<span data-ttu-id="5f9d4-279">[Creare un'app iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="5f9d4-279">[Create an iOS App]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="5f9d4-280">[Sincronizzazione di dati offline nelle app per dispositivi mobili]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="5f9d4-280">[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

<span data-ttu-id="5f9d4-281">[Cloud Cover: Sincronizzazione offline in Servizi mobili di Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="5f9d4-281">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
