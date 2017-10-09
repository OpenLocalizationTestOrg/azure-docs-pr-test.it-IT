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
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="37d27-103">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="37d27-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="37d27-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="37d27-104">Overview</span></span>
<span data-ttu-id="37d27-105">In questa esercitazione introduce funzionalità di sincronizzazione non in linea hello di App mobili di Azure per xamarin. Forms.</span><span class="sxs-lookup"><span data-stu-id="37d27-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="37d27-106">La sincronizzazione offline consente agli utenti finali di interagire con un'app, visualizzando, aggiungendo e modificando i dati, anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="37d27-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="37d27-107">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="37d27-107">Changes are stored in a local database.</span></span> <span data-ttu-id="37d27-108">Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con servizio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="37d27-109">In questa esercitazione si basa sulla soluzione di avvio rapido di xamarin. Forms hello per App per dispositivi mobili che si crea una volta completata l'esercitazione [creare un'app di iOS Xamarin].</span><span class="sxs-lookup"><span data-stu-id="37d27-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="37d27-110">soluzione di avvio rapido Hello per xamarin. Forms contiene hello codice toosupport sincronizzazione offline, che è necessario impostare solo toobe abilitato.</span><span class="sxs-lookup"><span data-stu-id="37d27-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="37d27-111">In questa esercitazione è aggiornare hello delle Guide rapide soluzione tooturn sulle funzionalità offline di hello di App mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="37d27-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="37d27-112">È inoltre evidenziati codice specifico per la linea hello in app hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="37d27-113">Se non si utilizza hello scaricato soluzione di avvio rapido, è necessario aggiungere hello dati estensione pacchetti tooyour di Microsoft Access.</span><span class="sxs-lookup"><span data-stu-id="37d27-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="37d27-114">Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="37d27-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="37d27-115">toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="37d27-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="37d27-116">Abilitare la funzionalità di sincronizzazione non in linea nella soluzione di avvio rapido hello</span><span class="sxs-lookup"><span data-stu-id="37d27-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="37d27-117">codice di sincronizzazione non in linea Hello è incluso nel progetto hello mediante le direttive del preprocessore c#.</span><span class="sxs-lookup"><span data-stu-id="37d27-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="37d27-118">Quando hello **OFFLINE\_sincronizzazione\_abilitato** simbolo è definito, questi percorsi di codice sono inclusi nella compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="37d27-119">Per le app di Windows, è necessario installare anche piattaforma SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="37d27-120">In Visual Studio, fare doppio clic hello soluzione > **Gestisci pacchetti NuGet per la soluzione...** , quindi cercare e installare il **Microsoft.Azure.Mobile.Client.SQLiteStore** pacchetto NuGet per tutti i progetti nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="37d27-121">In Esplora soluzioni hello, aprire il file di TodoItemManager.cs hello dal progetto di hello con **portabile** nel nome hello, che è il progetto libreria di classi portabile, quindi rimuovere il commento hello dopo la direttiva del preprocessore:</span><span class="sxs-lookup"><span data-stu-id="37d27-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="37d27-122">I dispositivi Windows toosupport (facoltativo), installare uno dei seguenti pacchetti runtime SQLite hello:</span><span class="sxs-lookup"><span data-stu-id="37d27-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="37d27-123">**Windows 8.1 Runtime:** installare [SQLite per Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="37d27-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="37d27-124">**Windows Phone 8.1:** installare [SQLite per Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="37d27-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="37d27-125">**Piattaforma UWP** installare [SQLite per hello universali di Windows universale][5].</span><span class="sxs-lookup"><span data-stu-id="37d27-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="37d27-126">Anche se la Guida introduttiva hello non contiene un progetto Windows universale, piattaforma Windows universale hello è supportata con Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="37d27-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="37d27-127">(Facoltativo) In ogni progetto di app di Windows, fare clic sul **riferimenti** > **Aggiungi riferimento...** , espandere hello **Windows** cartella > **estensioni**.</span><span class="sxs-lookup"><span data-stu-id="37d27-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="37d27-128">Abilitare hello appropriato **SQLite per Windows** SDK insieme hello **Visual C++ 2013 Runtime per Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="37d27-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="37d27-129">Hello nomi SQLite SDK variano leggermente in ogni piattaforma di Windows.</span><span class="sxs-lookup"><span data-stu-id="37d27-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="37d27-130">Esaminare il codice di sincronizzazione client hello</span><span class="sxs-lookup"><span data-stu-id="37d27-130">Review hello client sync code</span></span>
<span data-ttu-id="37d27-131">Ecco una breve panoramica degli elementi già inclusi nel codice dell'esercitazione di hello all'interno di hello `#if OFFLINE_SYNC_ENABLED` direttive.</span><span class="sxs-lookup"><span data-stu-id="37d27-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="37d27-132">La funzionalità di sincronizzazione non in linea è nel file di progetto hello TodoItemManager.cs nel progetto libreria di classi portabile hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="37d27-133">Per informazioni generali sulla funzionalità hello, vedere [non in linea sincronizzazione di dati in App mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="37d27-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="37d27-134">Prima di possono eseguire qualsiasi operazione di tabella, è necessario inizializzare l'archivio locale hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="37d27-135">Hello database dell'archivio locale viene inizializzato in hello **TodoItemManager** costruttore della classe utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="37d27-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="37d27-136">Questo codice crea un nuovo database SQLite locale utilizzando hello **MobileServiceSQLiteStore** classe.</span><span class="sxs-lookup"><span data-stu-id="37d27-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="37d27-137">Hello **DefineTable** metodo crea una tabella nell'archivio locale hello corrispondente hello campi tipo hello fornito.</span><span class="sxs-lookup"><span data-stu-id="37d27-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="37d27-138">tipo di Hello privo di tooinclude tutte le colonne di hello presenti nel database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="37d27-139">È possibile toostore un subset di colonne.</span><span class="sxs-lookup"><span data-stu-id="37d27-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="37d27-140">Hello **todoTable** campo **TodoItemManager** è un **IMobileServiceSyncTable** digitare anziché **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="37d27-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="37d27-141">Il database locale di hello utilizza classe per tutti creare, leggere, aggiornare ed eliminazione (CRUD) nella tabella.</span><span class="sxs-lookup"><span data-stu-id="37d27-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="37d27-142">Si decide quando tali modifiche vengono inserite back-end App Mobile toohello chiamando **PushAsync** su hello **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="37d27-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="37d27-143">Hello contesto di sincronizzazione consente di mantenere le relazioni tra tabelle e di rilevamento e il push delle modifiche in tutte le tabelle modificato quando un'app client **PushAsync** viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="37d27-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="37d27-144">esempio Hello **SyncAsync** toosync con back-end App Mobile hello viene chiamato:</span><span class="sxs-lookup"><span data-stu-id="37d27-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

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

    <span data-ttu-id="37d27-145">Questo esempio utilizza una semplice gestione degli errori con gestore di sincronizzazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="37d27-146">Un'applicazione reale si gestisce hello diversi errori, ad esempio le condizioni della rete e server è in conflitto con un oggetto personalizzato **IMobileServiceSyncHandler** implementazione.</span><span class="sxs-lookup"><span data-stu-id="37d27-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="37d27-147">Considerazioni sulla sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="37d27-147">Offline sync considerations</span></span>
<span data-ttu-id="37d27-148">Nell'esempio hello hello **SyncAsync** metodo viene chiamato solo sull'avvio e quando è richiesta una sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="37d27-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="37d27-149">tooinitiate una sincronizzazione in un'app Android o iOS, pull verso il basso nell'elenco degli elementi hello; per Windows, utilizzare hello **sincronizzazione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="37d27-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="37d27-150">In un'applicazione reale, è possibile creare trigger di sincronizzazione hello quando cambia lo stato di rete hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="37d27-151">Quando viene eseguita un'operazione di pull in una tabella che è in sospeso aggiornamenti locali registrati dal contesto hello, che pull operazione automaticamente i trigger di push contesto precedente.</span><span class="sxs-lookup"><span data-stu-id="37d27-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="37d27-152">Quando l'aggiornamento, l'aggiunta e il completamento di elementi in questo esempio, è possibile omettere hello esplicita **PushAsync** chiamare.</span><span class="sxs-lookup"><span data-stu-id="37d27-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="37d27-153">Nel codice hello fornito, tutti i record nella tabella TodoItem remoto hello esecuzione di query, ma è anche possibile toofilter record passando un id di query e una query troppo**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="37d27-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="37d27-154">Per ulteriori informazioni, vedere la sezione hello *sincronizzazione incrementale* in [non in linea sincronizzazione di dati in App mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="37d27-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="37d27-155">Eseguire app di hello client</span><span class="sxs-lookup"><span data-stu-id="37d27-155">Run hello client app</span></span>
<span data-ttu-id="37d27-156">Con ora abilitata la sincronizzazione non in linea, eseguire un'applicazione hello client almeno una volta su ogni database dell'archivio locale hello toopopulate piattaforma.</span><span class="sxs-lookup"><span data-stu-id="37d27-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="37d27-157">In un secondo momento, simulare uno scenario offline e modificare i dati di hello nell'archivio locale hello mentre l'applicazione hello è offline.</span><span class="sxs-lookup"><span data-stu-id="37d27-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="37d27-158">Aggiornare il comportamento di sincronizzazione hello di app client hello</span><span class="sxs-lookup"><span data-stu-id="37d27-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="37d27-159">In questa sezione, modificare hello client progetto toosimulate uno scenario offline tramite un URL dell'applicazione non valido per il back-end.</span><span class="sxs-lookup"><span data-stu-id="37d27-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="37d27-160">In alternativa, è possibile disattivare le connessioni di rete spostando il dispositivo troppo "Modalità aereo".</span><span class="sxs-lookup"><span data-stu-id="37d27-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="37d27-161">Quando si aggiunge o modifica gli elementi di dati, queste modifiche sono contenute nell'archivio locale hello, ma non sincronizzate i dati di back-end toohello archiviano fino a quando non viene ristabilita la connessione di hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="37d27-162">In hello Esplora soluzioni, aprire il file di progetto di hello Constants.cs da hello **portabile** del progetto e modificare il valore di hello di `ApplicationURL` URL non valido di toopoint tooan:</span><span class="sxs-lookup"><span data-stu-id="37d27-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="37d27-163">File TodoItemManager.cs hello aperto da hello **portabile** del progetto, quindi aggiungere un **catch** per hello base **eccezione** toohello classe **try … catch** blocco **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="37d27-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="37d27-164">Questo **catch** blocco scrive console toohello di messaggio eccezione di hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="37d27-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="37d27-165">Compilare ed eseguire l'applicazione client hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-165">Build and run hello client app.</span></span>  <span data-ttu-id="37d27-166">Aggiungere nuovi elementi.</span><span class="sxs-lookup"><span data-stu-id="37d27-166">Add some new items.</span></span> <span data-ttu-id="37d27-167">Si noti che un'eccezione viene registrata nella console di hello per ogni tentativo di toosync con hello di back-end.</span><span class="sxs-lookup"><span data-stu-id="37d27-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="37d27-168">Questi nuovi elementi esistono solo nell'archivio locale di hello fino a quando non può essere di back-end mobile toohello inseriti.</span><span class="sxs-lookup"><span data-stu-id="37d27-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="37d27-169">app client Hello si comporta come se fosse back-end connesso toohello, supporto che tutte di creazione, lettura, aggiornamento, le operazioni di eliminazione (CRUD).</span><span class="sxs-lookup"><span data-stu-id="37d27-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="37d27-170">Chiudere l'applicazione hello e riavviarlo tooverify che è stato creato in base ai nuovi elementi hello siano archivio locale toohello persistente.</span><span class="sxs-lookup"><span data-stu-id="37d27-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="37d27-171">(Facoltativo) Utilizzare Visual Studio tooview toosee di tabella del Database SQL di Azure che hello dati nel database back-end hello non vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="37d27-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="37d27-172">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="37d27-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="37d27-173">Esplorare database tooyour **Azure**->**database SQL**.</span><span class="sxs-lookup"><span data-stu-id="37d27-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="37d27-174">Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="37d27-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="37d27-175">È possibile cercare tooyour tabella di database SQL e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="37d27-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="37d27-176">Aggiornare hello client app tooreconnect back-end per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="37d27-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="37d27-177">In questa sezione, riconnettersi hello app toohello mobile back-end, che simula l'applicazione hello confermata tooan di stato online.</span><span class="sxs-lookup"><span data-stu-id="37d27-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="37d27-178">Quando si esegue l'azione di aggiornamento hello, i dati sono back-end mobile tooyour sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="37d27-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="37d27-179">Riaprire il file Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="37d27-179">Reopen Constants.cs.</span></span> <span data-ttu-id="37d27-180">Hello corretto `applicationURL` toopoint toohello correggere URL.</span><span class="sxs-lookup"><span data-stu-id="37d27-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="37d27-181">Ricompilare ed eseguire l'applicazione client hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="37d27-182">app Hello tenta toosync con back-end dell'app mobile hello dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="37d27-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="37d27-183">Verificare che nessuna eccezione vengono registrata nella console di debug hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="37d27-184">(Facoltativo) Hello visualizzazione aggiornata dei dati utilizzando Esplora oggetti di SQL Server o uno strumento REST come Fiddler o [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="37d27-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="37d27-185">Si noti hello dati sono stati sincronizzati tra i database di back-end hello e archivio locale hello.</span><span class="sxs-lookup"><span data-stu-id="37d27-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="37d27-186">Avviso hello dati sincronizzati tra database hello e archivio locale hello e contiene elementi hello che aggiunti mentre l'app è stata disconnessa.</span><span class="sxs-lookup"><span data-stu-id="37d27-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37d27-187">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="37d27-187">Additional Resources</span></span>
* <span data-ttu-id="37d27-188">[Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure][2]</span><span class="sxs-lookup"><span data-stu-id="37d27-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="37d27-189">[Procedura per .NET SDK di App per dispositivi mobili di Azure][8]</span><span class="sxs-lookup"><span data-stu-id="37d27-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
