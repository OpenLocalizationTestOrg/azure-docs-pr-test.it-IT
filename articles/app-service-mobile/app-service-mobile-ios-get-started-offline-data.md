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
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="a05a4-103">Sincronizzare offline le app per dispositivi mobili iOS</span><span class="sxs-lookup"><span data-stu-id="a05a4-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="a05a4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a05a4-104">Overview</span></span>
<span data-ttu-id="a05a4-105">In questa esercitazione vengono illustrate la sincronizzazione non in linea con le funzionalità di App per dispositivi mobili hello di servizio App di Azure per iOS.</span><span class="sxs-lookup"><span data-stu-id="a05a4-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="a05a4-106">Con gli utenti finali di sincronizzazione non in linea possono interagire con un tooview app per dispositivi mobili, aggiungere o modificare i dati, anche quando non dispongono di alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="a05a4-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="a05a4-107">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="a05a4-107">Changes are stored in a local database.</span></span> <span data-ttu-id="a05a4-108">Dopo che il dispositivo di hello è online, le modifiche di hello vengono sincronizzate con hello remoto back-end.</span><span class="sxs-lookup"><span data-stu-id="a05a4-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="a05a4-109">Se questa è la prima esperienza con App per dispositivi mobili, è necessario completare prima esercitazione hello [crea un'App iOS].</span><span class="sxs-lookup"><span data-stu-id="a05a4-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="a05a4-110">Se non si utilizza il progetto di avvio rapido server hello scaricato, è necessario aggiungere il progetto tooyour pacchetti di hello accesso ai dati estensione.</span><span class="sxs-lookup"><span data-stu-id="a05a4-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="a05a4-111">Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a05a4-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="a05a4-112">toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere [sincronizzazione dati Offline nelle App per dispositivi mobili].</span><span class="sxs-lookup"><span data-stu-id="a05a4-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="a05a4-113"><a name="review-sync"></a>Esaminare il codice di sincronizzazione client hello</span><span class="sxs-lookup"><span data-stu-id="a05a4-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="a05a4-114">progetto client Hello scaricati per hello [crea un'App iOS] esercitazione contiene già codice che supporta la sincronizzazione non in linea utilizzando un database locale basato su dati di base.</span><span class="sxs-lookup"><span data-stu-id="a05a4-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="a05a4-115">Questa sezione vengono riepilogati gli elementi che è già inclusi nel codice dell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="a05a4-116">Per informazioni generali sulla funzionalità hello, vedere [sincronizzazione dati Offline nelle App per dispositivi mobili].</span><span class="sxs-lookup"><span data-stu-id="a05a4-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="a05a4-117">Tramite funzionalità di sincronizzazione di dati non in linea di hello di App per dispositivi mobili, gli utenti finali possono interagire con un database locale anche quando la rete hello è inaccessibile.</span><span class="sxs-lookup"><span data-stu-id="a05a4-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="a05a4-118">toouse queste funzionalità nell'applicazione, inizializzare il contesto di sincronizzazione hello di `MSClient` e fare riferimento a un archivio locale.</span><span class="sxs-lookup"><span data-stu-id="a05a4-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="a05a4-119">Quindi si fa riferimento la tabella tramite hello **MSSyncTable** interfaccia.</span><span class="sxs-lookup"><span data-stu-id="a05a4-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="a05a4-120">In **QSTodoService.m** (Objective-C) o **ToDoTableViewController.swift** (Agile), si noti che il tipo di membro hello hello **syncTable** è  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="a05a4-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="a05a4-121">La sincronizzazione offline usa questa interfaccia della tabella di sincronizzazione al posto di **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="a05a4-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="a05a4-122">Quando si utilizza una tabella di sincronizzazione, tutte le operazioni passare archivio locale toohello e vengono sincronizzate solo con hello remoto back-end con esplicita push e pull operazioni.</span><span class="sxs-lookup"><span data-stu-id="a05a4-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="a05a4-123">tooget una tabella di riferimento tooa sincronizzazione, utilizzare hello **syncTableWithName** metodo `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="a05a4-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="a05a4-124">la funzionalità di sincronizzazione non in linea di tooremove, utilizzare **tableWithName** invece.</span><span class="sxs-lookup"><span data-stu-id="a05a4-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="a05a4-125">Prima di possono eseguire qualsiasi operazione di tabella, è necessario inizializzare l'archivio locale hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="a05a4-126">Ecco il codice pertinente hello:</span><span class="sxs-lookup"><span data-stu-id="a05a4-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="a05a4-127">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-127">**Objective-C**.</span></span> <span data-ttu-id="a05a4-128">In hello **QSTodoService.init** metodo:</span><span class="sxs-lookup"><span data-stu-id="a05a4-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="a05a4-129">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-129">**Swift**.</span></span> <span data-ttu-id="a05a4-130">In hello **ToDoTableViewController.viewDidLoad** metodo:</span><span class="sxs-lookup"><span data-stu-id="a05a4-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="a05a4-131">Questo metodo crea un archivio locale tramite hello `MSCoreDataStore` fornisce l'interfaccia che hello Mobile App SDK.</span><span class="sxs-lookup"><span data-stu-id="a05a4-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="a05a4-132">In alternativa, è possibile fornire un archivio locale diverso implementando hello `MSSyncContextDataSource` protocollo.</span><span class="sxs-lookup"><span data-stu-id="a05a4-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="a05a4-133">Inoltre, hello primo parametro di **MSSyncContext** è toospecify utilizzato un gestore del conflitto.</span><span class="sxs-lookup"><span data-stu-id="a05a4-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="a05a4-134">Perché è stato passato `nil`, si ottiene gestore di conflitti di hello predefinito, non riesce in eventuali conflitti.</span><span class="sxs-lookup"><span data-stu-id="a05a4-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="a05a4-135">A questo punto, consente un'operazione di sincronizzazione effettivo hello e ottenere dati dal back-end hello remoto:</span><span class="sxs-lookup"><span data-stu-id="a05a4-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="a05a4-136">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-136">**Objective-C**.</span></span> <span data-ttu-id="a05a4-137">`syncData`Invia le nuove modifiche e quindi chiama **pullData** dati tooget dal back-end hello remoto.</span><span class="sxs-lookup"><span data-stu-id="a05a4-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="a05a4-138">A sua volta, hello **pullData** metodo consente di ottenere nuovi dati che corrispondono a una query:</span><span class="sxs-lookup"><span data-stu-id="a05a4-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

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
* <span data-ttu-id="a05a4-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-139">**Swift**:</span></span>
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

<span data-ttu-id="a05a4-140">Nella versione di hello Objective-C, in `syncData`, viene innanzitutto chiamato **pushWithCompletion** nel contesto di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="a05a4-141">Questo metodo è un membro di `MSSyncContext` (e non hello sincronizzazione tabella) Poiché inserisce le modifiche apportate in tutte le tabelle.</span><span class="sxs-lookup"><span data-stu-id="a05a4-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="a05a4-142">Solo i record che sono stati modificati in qualche modo localmente (tramite le operazioni CUD) vengono inviati toohello server.</span><span class="sxs-lookup"><span data-stu-id="a05a4-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="a05a4-143">Quindi hello helper **pullData** viene chiamato, che chiama **MSSyncTable.pullWithQuery** dati remoti tooretrieve e archiviarla nel database locale hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="a05a4-144">Nella versione Swift hello, perché l'operazione di push hello non sia strettamente necessario, non vi è alcuna chiamata troppo**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="a05a4-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="a05a4-145">Se sono state apportate modifiche in sospeso nel contesto di sincronizzazione hello per tabella hello che esegue un'operazione push, pull genera sempre prima di push.</span><span class="sxs-lookup"><span data-stu-id="a05a4-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="a05a4-146">Tuttavia, se si dispone di più di una tabella di sincronizzazione, è migliore tooexplicitly chiamata push tooensure che tutto sia coerenza tra le tabelle correlate.</span><span class="sxs-lookup"><span data-stu-id="a05a4-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="a05a4-147">In hello Objective-C e nelle versioni Swift, è possibile utilizzare hello **pullWithQuery** toospecify metodo toofilter una query hello record che si desidera tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="a05a4-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="a05a4-148">In questo esempio, query hello recupera tutti i record di hello remoto `TodoItem` tabella.</span><span class="sxs-lookup"><span data-stu-id="a05a4-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="a05a4-149">secondo parametro di Hello **pullWithQuery** è un ID di query che viene utilizzato per *sincronizzazione incrementale*. Sincronizzazione incrementale recupera solo i record che sono stati modificati dall'ultima sincronizzazione hello, utilizzo del record hello `UpdatedAt` timestamp (chiamato `updatedAt` nell'archivio locale di hello.) hello query ID deve essere una stringa descrittiva che è univoca per ogni query nella logica l'app.</span><span class="sxs-lookup"><span data-stu-id="a05a4-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="a05a4-150">tooopt non sincronizzati incrementale, passare `nil` come hello ID di query.</span><span class="sxs-lookup"><span data-stu-id="a05a4-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="a05a4-151">Questo approccio può potenzialmente non essere efficiente, perché recupera tutti i record ad ogni operazione pull.</span><span class="sxs-lookup"><span data-stu-id="a05a4-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="a05a4-152">app di Hello Objective-C esegue la sincronizzazione quando si modifica o aggiungere dati, quando un utente esegue l'azione di aggiornamento hello e all'avvio.</span><span class="sxs-lookup"><span data-stu-id="a05a4-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="a05a4-153">Consente di sincronizzare Hello Swift app quando l'utente hello esegue l'azione di aggiornamento hello e all'avvio.</span><span class="sxs-lookup"><span data-stu-id="a05a4-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="a05a4-154">Sincronizzazioni app ogni volta che i dati sono hello modificato (Objective-C) o ogni volta che l'applicazione hello all'avvio (Objective-C e Swift), applicazione hello presuppone che l'utente hello è online.</span><span class="sxs-lookup"><span data-stu-id="a05a4-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="a05a4-155">In una sezione successiva, si aggiornerà app hello in modo che gli utenti possono modificare anche quando sono in linea.</span><span class="sxs-lookup"><span data-stu-id="a05a4-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="a05a4-156"><a name="review-core-data"></a>Modello di dati principali hello revisione</span><span class="sxs-lookup"><span data-stu-id="a05a4-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="a05a4-157">Quando si utilizza l'archivio non in linea di hello dati principali, è necessario definire tabelle specifiche e i campi nel modello di dati.</span><span class="sxs-lookup"><span data-stu-id="a05a4-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="a05a4-158">app di esempio Hello include già un modello di dati con formato corretto hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="a05a4-159">In questa sezione vengono illustrate le tooshow tali tabelle le modalità di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="a05a4-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="a05a4-160">Aprire **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="a05a4-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="a05a4-161">Sono quattro tabelle definito tre utilizzati da hello SDK e uno che viene utilizzato per attività hello voci:</span><span class="sxs-lookup"><span data-stu-id="a05a4-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="a05a4-162">MS_TableOperations: Tracce hello elementi che richiedono toobe sincronizzati con il server di hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="a05a4-163">MS_TableOperationErrors: tiene traccia di eventuali errori che si verificano durante la sincronizzazione offline.</span><span class="sxs-lookup"><span data-stu-id="a05a4-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="a05a4-164">MS_TableConfig: Tracce hello ora dell'ultimo aggiornamento per l'operazione di sincronizzazione per tutte le operazioni pull ultimo hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="a05a4-165">TodoItem: Archivia gli elementi di attività da eseguire hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="a05a4-166">le colonne di sistema di Hello **createdAt**, **updatedAt**, e **versione** sono proprietà di sistema facoltativo.</span><span class="sxs-lookup"><span data-stu-id="a05a4-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="a05a4-167">Hello Mobile App SDK riserva i nomi di colonna che iniziano con "**``**".</span><span class="sxs-lookup"><span data-stu-id="a05a4-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="a05a4-168">Usare questo prefisso solo per le colonne di sistema.</span><span class="sxs-lookup"><span data-stu-id="a05a4-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="a05a4-169">In caso contrario, i nomi di colonna vengono modificati quando si utilizza hello remoto back-end.</span><span class="sxs-lookup"><span data-stu-id="a05a4-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="a05a4-170">Quando si utilizza la funzionalità di sincronizzazione non in linea hello, definire tre tabelle di sistema hello e una tabella di dati hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="a05a4-171">Tabelle di sistema</span><span class="sxs-lookup"><span data-stu-id="a05a4-171">System tables</span></span>

<span data-ttu-id="a05a4-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="a05a4-172">**MS_TableOperations**</span></span>  

![Attributi della tabella MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="a05a4-174">Attributo</span><span class="sxs-lookup"><span data-stu-id="a05a4-174">Attribute</span></span> | <span data-ttu-id="a05a4-175">Tipo</span><span class="sxs-lookup"><span data-stu-id="a05a4-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="a05a4-176">id</span><span class="sxs-lookup"><span data-stu-id="a05a4-176">id</span></span> | <span data-ttu-id="a05a4-177">Valore integer 64</span><span class="sxs-lookup"><span data-stu-id="a05a4-177">Integer 64</span></span> |
| <span data-ttu-id="a05a4-178">itemId</span><span class="sxs-lookup"><span data-stu-id="a05a4-178">itemId</span></span> | <span data-ttu-id="a05a4-179">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-179">String</span></span> |
| <span data-ttu-id="a05a4-180">properties</span><span class="sxs-lookup"><span data-stu-id="a05a4-180">properties</span></span> | <span data-ttu-id="a05a4-181">Dati binari</span><span class="sxs-lookup"><span data-stu-id="a05a4-181">Binary Data</span></span> |
| <span data-ttu-id="a05a4-182">tabella</span><span class="sxs-lookup"><span data-stu-id="a05a4-182">table</span></span> | <span data-ttu-id="a05a4-183">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-183">String</span></span> |
| <span data-ttu-id="a05a4-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="a05a4-184">tableKind</span></span> | <span data-ttu-id="a05a4-185">Integer 16</span><span class="sxs-lookup"><span data-stu-id="a05a4-185">Integer 16</span></span> |


<span data-ttu-id="a05a4-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="a05a4-186">**MS_TableOperationErrors**</span></span>

 ![Attributi della tabella MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="a05a4-188">Attributo</span><span class="sxs-lookup"><span data-stu-id="a05a4-188">Attribute</span></span> | <span data-ttu-id="a05a4-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="a05a4-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="a05a4-190">id</span><span class="sxs-lookup"><span data-stu-id="a05a4-190">id</span></span> |<span data-ttu-id="a05a4-191">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-191">String</span></span> |
| <span data-ttu-id="a05a4-192">operationId</span><span class="sxs-lookup"><span data-stu-id="a05a4-192">operationId</span></span> |<span data-ttu-id="a05a4-193">Valore integer 64</span><span class="sxs-lookup"><span data-stu-id="a05a4-193">Integer 64</span></span> |
| <span data-ttu-id="a05a4-194">properties</span><span class="sxs-lookup"><span data-stu-id="a05a4-194">properties</span></span> |<span data-ttu-id="a05a4-195">Dati binari</span><span class="sxs-lookup"><span data-stu-id="a05a4-195">Binary Data</span></span> |
| <span data-ttu-id="a05a4-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="a05a4-196">tableKind</span></span> |<span data-ttu-id="a05a4-197">Integer 16</span><span class="sxs-lookup"><span data-stu-id="a05a4-197">Integer 16</span></span> |

 <span data-ttu-id="a05a4-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="a05a4-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="a05a4-199">Attributo</span><span class="sxs-lookup"><span data-stu-id="a05a4-199">Attribute</span></span> | <span data-ttu-id="a05a4-200">Tipo</span><span class="sxs-lookup"><span data-stu-id="a05a4-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="a05a4-201">id</span><span class="sxs-lookup"><span data-stu-id="a05a4-201">id</span></span> |<span data-ttu-id="a05a4-202">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-202">String</span></span> |
| <span data-ttu-id="a05a4-203">key</span><span class="sxs-lookup"><span data-stu-id="a05a4-203">key</span></span> |<span data-ttu-id="a05a4-204">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-204">String</span></span> |
| <span data-ttu-id="a05a4-205">keyType</span><span class="sxs-lookup"><span data-stu-id="a05a4-205">keyType</span></span> |<span data-ttu-id="a05a4-206">Valore integer 64</span><span class="sxs-lookup"><span data-stu-id="a05a4-206">Integer 64</span></span> |
| <span data-ttu-id="a05a4-207">tabella</span><span class="sxs-lookup"><span data-stu-id="a05a4-207">table</span></span> |<span data-ttu-id="a05a4-208">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-208">String</span></span> |
| <span data-ttu-id="a05a4-209">value</span><span class="sxs-lookup"><span data-stu-id="a05a4-209">value</span></span> |<span data-ttu-id="a05a4-210">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="a05a4-211">Tabella dati</span><span class="sxs-lookup"><span data-stu-id="a05a4-211">Data table</span></span>

<span data-ttu-id="a05a4-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="a05a4-212">**TodoItem**</span></span>

| <span data-ttu-id="a05a4-213">Attributo</span><span class="sxs-lookup"><span data-stu-id="a05a4-213">Attribute</span></span> | <span data-ttu-id="a05a4-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="a05a4-214">Type</span></span> | <span data-ttu-id="a05a4-215">Nota</span><span class="sxs-lookup"><span data-stu-id="a05a4-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a05a4-216">id</span><span class="sxs-lookup"><span data-stu-id="a05a4-216">id</span></span> | <span data-ttu-id="a05a4-217">Stringa, contrassegnata come obbligatoria</span><span class="sxs-lookup"><span data-stu-id="a05a4-217">String, marked required</span></span> |<span data-ttu-id="a05a4-218">chiave primaria nell'archivio remoto</span><span class="sxs-lookup"><span data-stu-id="a05a4-218">Primary key in remote store</span></span> |
| <span data-ttu-id="a05a4-219">complete</span><span class="sxs-lookup"><span data-stu-id="a05a4-219">complete</span></span> | <span data-ttu-id="a05a4-220">Boolean</span><span class="sxs-lookup"><span data-stu-id="a05a4-220">Boolean</span></span> | <span data-ttu-id="a05a4-221">campo elemento ToDo</span><span class="sxs-lookup"><span data-stu-id="a05a4-221">To-do item field</span></span> |
| <span data-ttu-id="a05a4-222">text</span><span class="sxs-lookup"><span data-stu-id="a05a4-222">text</span></span> |<span data-ttu-id="a05a4-223">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-223">String</span></span> |<span data-ttu-id="a05a4-224">campo elemento ToDo</span><span class="sxs-lookup"><span data-stu-id="a05a4-224">To-do item field</span></span> |
| <span data-ttu-id="a05a4-225">createdAt</span><span class="sxs-lookup"><span data-stu-id="a05a4-225">createdAt</span></span> | <span data-ttu-id="a05a4-226">Date</span><span class="sxs-lookup"><span data-stu-id="a05a4-226">Date</span></span> | <span data-ttu-id="a05a4-227">(facoltativo) Esegue il mapping troppo**createdAt** proprietà di sistema</span><span class="sxs-lookup"><span data-stu-id="a05a4-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="a05a4-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="a05a4-228">updatedAt</span></span> | <span data-ttu-id="a05a4-229">Date</span><span class="sxs-lookup"><span data-stu-id="a05a4-229">Date</span></span> | <span data-ttu-id="a05a4-230">(facoltativo) Esegue il mapping troppo**updatedAt** proprietà di sistema</span><span class="sxs-lookup"><span data-stu-id="a05a4-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="a05a4-231">version</span><span class="sxs-lookup"><span data-stu-id="a05a4-231">version</span></span> | <span data-ttu-id="a05a4-232">String</span><span class="sxs-lookup"><span data-stu-id="a05a4-232">String</span></span> | <span data-ttu-id="a05a4-233">(facoltativo) È in conflitto toodetect usato, tooversion mappe</span><span class="sxs-lookup"><span data-stu-id="a05a4-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="a05a4-234"><a name="setup-sync"></a>Modificare il comportamento di sincronizzazione hello di hello app</span><span class="sxs-lookup"><span data-stu-id="a05a4-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="a05a4-235">In questa sezione è modificare app hello in modo che non sincronizza avvio dell'app o quando si inserisce e aggiornare gli elementi.</span><span class="sxs-lookup"><span data-stu-id="a05a4-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="a05a4-236">Viene eseguita la sincronizzazione solo quando viene eseguita pulsante di azione di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="a05a4-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-237">**Objective-C**:</span></span>

1. <span data-ttu-id="a05a4-238">In **QSTodoListViewController.m**, modificare hello **viewDidLoad** tooremove metodo hello chiamata troppo`[self refresh]` alla fine di hello del metodo hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="a05a4-239">Dati hello ora non è sincronizzati con il server di hello all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="a05a4-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="a05a4-240">Invece viene sincronizzata con il contenuto di hello dell'archivio locale di hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="a05a4-241">In **QSTodoService.m**, modificare la definizione di hello `addItem` in modo che non sincronizzato dopo l'inserimento dell'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="a05a4-242">Rimuovere hello `self syncData` blocco e sostituirlo con il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="a05a4-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="a05a4-243">Modificare la definizione di hello `completeItem` come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a05a4-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="a05a4-244">Rimuovere il blocco di hello per `self syncData` e sostituirlo con il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="a05a4-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="a05a4-245">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-245">**Swift**:</span></span>

<span data-ttu-id="a05a4-246">In `viewDidLoad`nella **ToDoTableViewController.swift**, impostare come commento le righe di due hello riportati di seguito, toostop la sincronizzazione all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="a05a4-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="a05a4-247">In fase di hello della redazione del presente documento, app Todo Swift hello non aggiorna servizio hello quando un utente aggiunge o completato un elemento.</span><span class="sxs-lookup"><span data-stu-id="a05a4-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="a05a4-248">Aggiorna servizio hello solo all'avvio di app.</span><span class="sxs-lookup"><span data-stu-id="a05a4-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="a05a4-249"><a name="test-app"></a>Test hello app</span><span class="sxs-lookup"><span data-stu-id="a05a4-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="a05a4-250">In questa sezione è connettersi toosimulate URL non valido di tooan uno scenario non in linea.</span><span class="sxs-lookup"><span data-stu-id="a05a4-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="a05a4-251">Quando si aggiungono elementi di dati, si è mantenuti in hello archivio locale dei dati di base, ma non è sincronizzati con hello app mobile back-end.</span><span class="sxs-lookup"><span data-stu-id="a05a4-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="a05a4-252">Modifica URL di app per dispositivi mobili hello in **QSTodoService.m** tooan URL non valido e nuovamente l'applicazione hello esecuzione:</span><span class="sxs-lookup"><span data-stu-id="a05a4-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="a05a4-253">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-253">**Objective-C**.</span></span> <span data-ttu-id="a05a4-254">In QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="a05a4-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="a05a4-255">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a05a4-255">**Swift**.</span></span> <span data-ttu-id="a05a4-256">In ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="a05a4-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="a05a4-257">Aggiungere alcuni elementi attività.</span><span class="sxs-lookup"><span data-stu-id="a05a4-257">Add some to-do items.</span></span> <span data-ttu-id="a05a4-258">Chiudere il simulatore hello (o app hello chiusura forzata) e quindi riavviarlo.</span><span class="sxs-lookup"><span data-stu-id="a05a4-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="a05a4-259">Verificare che le modifiche siano state conservate.</span><span class="sxs-lookup"><span data-stu-id="a05a4-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="a05a4-260">Visualizzare il contenuto di hello di hello remoto **TodoItem** tabella:</span><span class="sxs-lookup"><span data-stu-id="a05a4-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="a05a4-261">Per un back-end di Node.js, visitare toohello [portale di Azure](https://portal.azure.com/) e il back-end di app per dispositivi mobili, fare clic su **tabelle facile** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="a05a4-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="a05a4-262">Per il back-end .NET, usare uno strumento SQL, quale ad esempio SQL Server Management Studio, oppure un client REST, quale ad esempio Fiddler o Postman.</span><span class="sxs-lookup"><span data-stu-id="a05a4-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="a05a4-263">Verificare che dispongano di nuovi elementi hello *non* stato sincronizzato con il server di hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="a05a4-264">Modifica hello URL nascosto toohello correggere uno in **QSTodoService.m**e app hello eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="a05a4-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="a05a4-265">Eseguire l'operazione di aggiornamento di hello trascinando verso il basso elenco hello degli elementi.</span><span class="sxs-lookup"><span data-stu-id="a05a4-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="a05a4-266">Verrà visualizzato un indicatore di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="a05a4-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="a05a4-267">Hello vista **TodoItem** nuovamente i dati.</span><span class="sxs-lookup"><span data-stu-id="a05a4-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="a05a4-268">gli elementi di attività nuove e modificate di Hello dovrebbero essere ora visualizzati.</span><span class="sxs-lookup"><span data-stu-id="a05a4-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="a05a4-269">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="a05a4-269">Summary</span></span>
<span data-ttu-id="a05a4-270">funzionalità di sincronizzazione non in linea toosupport hello, abbiamo utilizzato hello `MSSyncTable` l'interfaccia e inizializzato `MSClient.syncContext` con un archivio locale.</span><span class="sxs-lookup"><span data-stu-id="a05a4-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="a05a4-271">In questo caso, archivio locale hello è un database basato su dati di base.</span><span class="sxs-lookup"><span data-stu-id="a05a4-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="a05a4-272">Quando si utilizza un archivio locale dei dati di base, è necessario definire più tabelle con hello [correggere le proprietà di sistema](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="a05a4-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="a05a4-273">normale Hello creare, leggere, aggiornare ed eliminazione (CRUD) per il lavoro App per dispositivi mobili, come se l'applicazione hello è ancora connesso, ma si verificano tutte le operazioni di hello sull'archivio locale hello.</span><span class="sxs-lookup"><span data-stu-id="a05a4-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="a05a4-274">Quando l'archivio locale hello è sincronizzato con server hello, abbiamo utilizzato hello **MSSyncTable.pullWithQuery** metodo.</span><span class="sxs-lookup"><span data-stu-id="a05a4-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a05a4-275">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a05a4-275">Additional resources</span></span>
* <span data-ttu-id="a05a4-276">[sincronizzazione dati Offline nelle App per dispositivi mobili]</span><span class="sxs-lookup"><span data-stu-id="a05a4-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="a05a4-277">[Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure] \(hello video è servizi mobili, ma non in linea App per dispositivi mobili funziona la sincronizzazione in modo analogo.\)</span><span class="sxs-lookup"><span data-stu-id="a05a4-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[crea un'App iOS]: app-service-mobile-ios-get-started.md
[sincronizzazione dati Offline nelle App per dispositivi mobili]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
