---
title: Abilitare la sincronizzazione offline per l'app per dispositivi mobili di Azure (Xamarin.Forms) | Documentazione Microsoft
description: Informazioni su come usare le app per dispositivi mobili del servizio app per memorizzare nella cache e sincronizzare i dati offline in un'applicazione Xamarin.Forms
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
ms.openlocfilehash: f2bed0a7124517319cc82405c4ab6b4d79aacfe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="d1b83-103">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="d1b83-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="d1b83-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d1b83-104">Overview</span></span>
<span data-ttu-id="d1b83-105">Questa esercitazione descrive la funzionalità di sincronizzazione offline di App per dispositivi mobili di Azure per Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="d1b83-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="d1b83-106">La sincronizzazione offline consente agli utenti finali di interagire con un'app, visualizzando, aggiungendo e modificando i dati, anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="d1b83-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="d1b83-107">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="d1b83-107">Changes are stored in a local database.</span></span> <span data-ttu-id="d1b83-108">Quando il dispositivo torna online, vengono sincronizzate con il servizio remoto.</span><span class="sxs-lookup"><span data-stu-id="d1b83-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="d1b83-109">Questa esercitazione si basa sulla soluzione di avvio rapido per Xamarin.Forms per le app per dispositivi mobili create quando si completa l'esercitazione [Creare un'app per Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="d1b83-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="d1b83-110">La soluzione di avvio rapido per Xamarin.Forms contiene il codice per supportare la sincronizzazione offline, che deve solo essere abilitata.</span><span class="sxs-lookup"><span data-stu-id="d1b83-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span></span> <span data-ttu-id="d1b83-111">In questa esercitazione viene aggiornata la soluzione di avvio rapido per attivare le funzionalità offline delle app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="d1b83-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="d1b83-112">Viene anche evidenziato il codice specifico per le funzionalità offline nell'app.</span><span class="sxs-lookup"><span data-stu-id="d1b83-112">We also highlight the offline-specific code in the app.</span></span> <span data-ttu-id="d1b83-113">Se non si usa la soluzione di avvio rapido scaricata, è necessario aggiungere al progetto il pacchetto di estensione per l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="d1b83-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="d1b83-114">Per altre informazioni sui pacchetti di estensione server, vedere l'articolo [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="d1b83-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="d1b83-115">Per altre informazioni sulla funzionalità di sincronizzazione offline, vedere l'argomento [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="d1b83-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-the-quickstart-solution"></a><span data-ttu-id="d1b83-116">Abilitare la funzionalità di sincronizzazione offline nella soluzione di avvio rapido</span><span class="sxs-lookup"><span data-stu-id="d1b83-116">Enable offline sync functionality in the quickstart solution</span></span>
<span data-ttu-id="d1b83-117">Il codice per la sincronizzazione offline viene incluso nel progetto usando le direttive del preprocessore C#.</span><span class="sxs-lookup"><span data-stu-id="d1b83-117">The offline sync code is included in the project by using C# preprocessor directives.</span></span> <span data-ttu-id="d1b83-118">Quando il simbolo **OFFLINE\_SYNC\_ENABLED** viene definito, questi percorsi di codice vengono inclusi nella build.</span><span class="sxs-lookup"><span data-stu-id="d1b83-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span></span> <span data-ttu-id="d1b83-119">Per le app di Windows, è anche necessario installare la piattaforma SQLite.</span><span class="sxs-lookup"><span data-stu-id="d1b83-119">For Windows apps, you must also install the SQLite platform.</span></span>

1. <span data-ttu-id="d1b83-120">In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione > **Gestisci pacchetti NuGet per la soluzione**, quindi cercare e installare il pacchetto NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** per tutti i progetti della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d1b83-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="d1b83-121">In Esplora soluzioni aprire il file TodoItemManager.cs dal progetto con **portabile** nel nome, ovvero il progetto Libreria di classi portabile, quindi rimuovere il commento dalla direttiva del preprocessore seguente:</span><span class="sxs-lookup"><span data-stu-id="d1b83-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="d1b83-122">(Facoltativo) Per supportare i dispositivi Windows, installare uno dei pacchetti di runtime SQLite seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1b83-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="d1b83-123">**Windows 8.1 Runtime:** installare [SQLite per Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="d1b83-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="d1b83-124">**Windows Phone 8.1:** installare [SQLite per Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="d1b83-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="d1b83-125">**Piattaforma UWP (Universal Windows Platform)** Installare [SQLite per la piattaforma UWP (Universal Windows Platform)][5].</span><span class="sxs-lookup"><span data-stu-id="d1b83-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span></span>

     <span data-ttu-id="d1b83-126">Anche se la Guida introduttiva non contiene un Windows universale, la piattaforma UWP (Universal Windows Platform) è supportata con Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="d1b83-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="d1b83-127">(Facoltativo) In ogni progetto app Windows fare clic con il pulsante destro del mouse su **Riferimenti** > **Aggiungi riferimento**, espandere la cartella **Windows** > **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="d1b83-128">Abilitare **SQLite for Windows** SDK appropriato insieme a **Visual C++ 2013 Runtime for Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="d1b83-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="d1b83-129">I nomi degli SDK di SQLite sono leggermente diversi per ogni piattaforma Windows.</span><span class="sxs-lookup"><span data-stu-id="d1b83-129">The SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="d1b83-130">Verificare il codice di sincronizzazione del client</span><span class="sxs-lookup"><span data-stu-id="d1b83-130">Review the client sync code</span></span>
<span data-ttu-id="d1b83-131">Ecco un breve riepilogo degli elementi già inclusi nel codice dell'esercitazione nelle direttive `#if OFFLINE_SYNC_ENABLED` .</span><span class="sxs-lookup"><span data-stu-id="d1b83-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="d1b83-132">La funzionalità di sincronizzazione offline è nel file di progetto TodoItemManager.cs nel progetto Libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="d1b83-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span></span> <span data-ttu-id="d1b83-133">Per una panoramica concettuale della funzionalità, vedere [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="d1b83-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="d1b83-134">Prima di poter eseguire qualsiasi operazione su tabella, è necessario inizializzare l'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="d1b83-134">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="d1b83-135">Il database di archiviazione locale viene inizializzato nel costruttore della classe **TodoItemManager** usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d1b83-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes the SyncContext using the default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="d1b83-136">Questo crea un nuovo database SQL locale usando la classe **MobileServiceSQLiteStore**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="d1b83-137">Il metodo **DefineTable** crea nell'archivio locale una tabella corrispondente ai campi del tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="d1b83-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span></span>  <span data-ttu-id="d1b83-138">Il tipo non deve necessariamente includere tutte le colonne presenti nel database remoto.</span><span class="sxs-lookup"><span data-stu-id="d1b83-138">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="d1b83-139">È possibile archiviare un subset di colonne.</span><span class="sxs-lookup"><span data-stu-id="d1b83-139">It is possible to store a subset of columns.</span></span>
* <span data-ttu-id="d1b83-140">Il campo **todoTable** in **TodoItemManager** è un tipo **IMobileServiceSyncTable** invece di **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="d1b83-141">Questa classe usa il database locale per tutte le operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD, Create, Read, Update, Delete) sulle tabelle.</span><span class="sxs-lookup"><span data-stu-id="d1b83-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="d1b83-142">È possibile decidere quando effettuare il push delle modifiche nel back-end dell'app per dispositivi mobili chiamando **PushAsync** in **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="d1b83-143">Questo contesto di sincronizzazione aiuta a mantenere le relazioni tra tabelle rilevando le modifiche apportate da un'app client in tutte le tabelle ed effettuandone il push quando viene chiamato **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="d1b83-144">Il metodo **SyncAsync** seguente viene chiamato per la sincronizzazione con il back-end dell'app per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="d1b83-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span></span>

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
                        //Update failed, reverting to server's copy.
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

    <span data-ttu-id="d1b83-145">Questo esempio usa la gestione degli errori semplice con il gestore di sincronizzazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="d1b83-145">This sample uses simple error handling with the default sync handler.</span></span> <span data-ttu-id="d1b83-146">Una vera applicazione gestirà i diversi errori come condizioni di rete, conflitti del server e altro usando un'implementazione **IMobileServiceSyncHandler** personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d1b83-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="d1b83-147">Considerazioni sulla sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="d1b83-147">Offline sync considerations</span></span>
<span data-ttu-id="d1b83-148">Nell'esempio il metodo **SyncAsync** viene chiamato solo all'avvio e quando viene richiesta una sincronizzazione in modo specifico.</span><span class="sxs-lookup"><span data-stu-id="d1b83-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="d1b83-149">Per avviare la sincronizzazione in un'app Android o iOS, trascinare verso il basso nell'elenco di elementi. Per Windows, usare il pulsante **Sincronizza**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span></span> <span data-ttu-id="d1b83-150">In un'applicazione effettiva è anche possibile attivare la sincronizzazione in caso di cambiamento dello stato della rete.</span><span class="sxs-lookup"><span data-stu-id="d1b83-150">In a real-world application, you could also make the sync trigger when the network state changes.</span></span>

<span data-ttu-id="d1b83-151">Quando viene effettuato il pull in una tabella con aggiornamenti locali in sospeso rilevati dal contesto, tale operazione attiva automaticamente un'operazione push nel contesto precedente.</span><span class="sxs-lookup"><span data-stu-id="d1b83-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="d1b83-152">Quando si aggiornano, aggiungono e completano elementi in questo esempio, è possibile omettere la chiamata **PushAsync** esplicita.</span><span class="sxs-lookup"><span data-stu-id="d1b83-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span></span>

<span data-ttu-id="d1b83-153">Nel codice fornito viene eseguita una query su tutti i record presenti nella tabella TodoItem remota, ma è anche possibile filtrare i record passando un ID di query e una query a **PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span></span> <span data-ttu-id="d1b83-154">Per altre informazioni, vedere la sezione *Sincronizzazione incrementale* in [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="d1b83-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="d1b83-155">Eseguire l'app client</span><span class="sxs-lookup"><span data-stu-id="d1b83-155">Run the client app</span></span>
<span data-ttu-id="d1b83-156">Con la sincronizzazione offline abilitata, è possibile eseguire l'applicazione client almeno una volta in ogni piattaforma per popolare il database di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="d1b83-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="d1b83-157">Più avanti viene simulato uno scenario offline e vengono modificati i dati nell'archivio locale mentre l'app è offline.</span><span class="sxs-lookup"><span data-stu-id="d1b83-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="update-the-sync-behavior-of-the-client-app"></a><span data-ttu-id="d1b83-158">Aggiornare il comportamento di sincronizzazione dell'app client</span><span class="sxs-lookup"><span data-stu-id="d1b83-158">Update the sync behavior of the client app</span></span>
<span data-ttu-id="d1b83-159">In questa sezione viene modificato il progetto client per simulare uno scenario offline usando un URL di applicazione non valido per il back-end.</span><span class="sxs-lookup"><span data-stu-id="d1b83-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="d1b83-160">In alternativa, è possibile disattivare le connessioni di rete attivando la "Modalità aereo" nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d1b83-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span></span>  <span data-ttu-id="d1b83-161">Quando si aggiungono o si modificano elementi di dati, queste modifiche vengono conservate nell'archivio locale, ma non vengono sincronizzate con l'archivio dati back-end fino a quando non viene ristabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="d1b83-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="d1b83-162">In Esplora soluzioni aprire il file di progetto Constants.cs dal progetto **Portatile** e modificare il valore di `ApplicationURL` in modo che punti a un URL non valido:</span><span class="sxs-lookup"><span data-stu-id="d1b83-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="d1b83-163">Aprire il file TodoItemManager.cs dal progetto **Portable**, quindi aggiungere un blocco **catch** aggiuntivo per la classe **Exception** di base al blocco **try...catch** in **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="d1b83-164">Questo blocco **catch** scrive il messaggio dell'eccezione nella console, come segue:</span><span class="sxs-lookup"><span data-stu-id="d1b83-164">This **catch** block writes the exception message to the console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="d1b83-165">Compilare ed eseguire l'app client.</span><span class="sxs-lookup"><span data-stu-id="d1b83-165">Build and run the client app.</span></span>  <span data-ttu-id="d1b83-166">Aggiungere nuovi elementi.</span><span class="sxs-lookup"><span data-stu-id="d1b83-166">Add some new items.</span></span> <span data-ttu-id="d1b83-167">Si noti che un'eccezione viene registrata nella console per ogni tentativo di sincronizzazione con il back-end.</span><span class="sxs-lookup"><span data-stu-id="d1b83-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span></span> <span data-ttu-id="d1b83-168">I nuovi elementi sono presenti solo nell'archivio locale finché non è possibile effettuarne il push al back-end mobile.</span><span class="sxs-lookup"><span data-stu-id="d1b83-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span></span> <span data-ttu-id="d1b83-169">L'app client si comporta come se fosse connessa al back-end, supportando tutte le operazioni CRUD (creazione, lettura, aggiornamento ed eliminazione).</span><span class="sxs-lookup"><span data-stu-id="d1b83-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="d1b83-170">Chiudere l'app e riavviarla per verificare che i nuovi elementi creati siano salvati in modo permanente nell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="d1b83-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="d1b83-171">(Facoltativo) Usare Visual Studio per visualizzare la tabella di database SQL di Azure per verificare che i dati nel database back-end non siano cambiati.</span><span class="sxs-lookup"><span data-stu-id="d1b83-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="d1b83-172">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="d1b83-173">Passare al database in **Azure**->**Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-173">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="d1b83-174">Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="d1b83-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="d1b83-175">È ora possibile passare alla tabella di database SQL e al relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="d1b83-175">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="update-the-client-app-to-reconnect-your-mobile-backend"></a><span data-ttu-id="d1b83-176">Aggiornare l'app client per la riconnessione al back-end mobile</span><span class="sxs-lookup"><span data-stu-id="d1b83-176">Update the client app to reconnect your mobile backend</span></span>
<span data-ttu-id="d1b83-177">In questa sezione viene riconnessa l'app al back-end mobile, azione che consente di simulare il ritorno dell'app nello stato online.</span><span class="sxs-lookup"><span data-stu-id="d1b83-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="d1b83-178">Quando si esegue il movimento di aggiornamento, i dati vengono sincronizzati con il back-end mobile.</span><span class="sxs-lookup"><span data-stu-id="d1b83-178">When you perform the refresh gesture, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="d1b83-179">Riaprire il file Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="d1b83-179">Reopen Constants.cs.</span></span> <span data-ttu-id="d1b83-180">Correggere il valore `applicationURL` in modo che faccia riferimento all'URL corretto.</span><span class="sxs-lookup"><span data-stu-id="d1b83-180">Correct the `applicationURL` to point to the correct URL.</span></span>
2. <span data-ttu-id="d1b83-181">Ricompilare ed eseguire l'app client.</span><span class="sxs-lookup"><span data-stu-id="d1b83-181">Rebuild and run the client app.</span></span> <span data-ttu-id="d1b83-182">L'app prova a eseguire la sincronizzazione con il back-end dell'app per dispositivi mobili dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="d1b83-182">The app attempts to sync with the mobile app backend after launching.</span></span> <span data-ttu-id="d1b83-183">Verificare che non vengano registrate eccezioni nella console di debug.</span><span class="sxs-lookup"><span data-stu-id="d1b83-183">Verify that no exceptions are logged in the debug console.</span></span>
3. <span data-ttu-id="d1b83-184">(Facoltativo) Visualizzare i dati aggiornati usando Esplora oggetti di SQL Server o uno strumento REST come Fiddler o [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="d1b83-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="d1b83-185">Si noti che i dati sono stati sincronizzati tra il database di back-end e l'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="d1b83-185">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="d1b83-186">Si noti che i dati sono stati sincronizzati tra il database e l'archivio locale e includono gli elementi aggiunti mentre l'app era disconnessa.</span><span class="sxs-lookup"><span data-stu-id="d1b83-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1b83-187">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d1b83-187">Additional Resources</span></span>
* <span data-ttu-id="d1b83-188">[Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure][2]</span><span class="sxs-lookup"><span data-stu-id="d1b83-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="d1b83-189">[Procedura per .NET SDK di App per dispositivi mobili di Azure][8]</span><span class="sxs-lookup"><span data-stu-id="d1b83-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
