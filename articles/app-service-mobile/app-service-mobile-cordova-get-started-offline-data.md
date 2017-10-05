---
title: Abilitare la sincronizzazione offline per l'app per dispositivi mobili di Azure (Cordova) | Documentazione Microsoft
description: Informazioni su come usare le app mobili del servizio app per memorizzare nella cache e sincronizzare i dati offline in un'applicazione Cordova
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="c68c2-103">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Cordova</span><span class="sxs-lookup"><span data-stu-id="c68c2-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="c68c2-104">Questa esercitazione descrive la funzionalità di sincronizzazione offline delle app per dispositivi mobili di Azure per Cordova.</span><span class="sxs-lookup"><span data-stu-id="c68c2-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="c68c2-105">La sincronizzazione offline consente agli utenti finali di interagire con un'app&mdash;visualizzando, aggiungendo e modificando i dati&mdash;anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="c68c2-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="c68c2-106">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="c68c2-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="c68c2-107">Quando il dispositivo torna online, vengono sincronizzate con il servizio remoto.</span><span class="sxs-lookup"><span data-stu-id="c68c2-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="c68c2-108">Questa esercitazione si basa sulla soluzione di avvio rapido Cordova per le app per dispositivi mobili create quando si completa l'esercitazione sull' [avvio rapido di Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="c68c2-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="c68c2-109">In questa esercitazione viene aggiornata la soluzione di avvio rapido per aggiungere le funzionalità offline delle app per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="c68c2-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="c68c2-110">Viene anche evidenziato il codice specifico per le funzionalità offline nell'app.</span><span class="sxs-lookup"><span data-stu-id="c68c2-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="c68c2-111">Per altre informazioni sulla funzionalità di sincronizzazione offline, vedere l'argomento [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="c68c2-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="c68c2-112">Per informazioni dettagliate sull'utilizzo delle API, vedere la [documentazione per le API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="c68c2-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="c68c2-113">Aggiungere la sincronizzazione offline alla soluzione di avvio rapido</span><span class="sxs-lookup"><span data-stu-id="c68c2-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="c68c2-114">È necessario aggiungere dall'app il codice di sincronizzazione offline.</span><span class="sxs-lookup"><span data-stu-id="c68c2-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="c68c2-115">La sincronizzazione offline richiede il plug-in cordova-sqlite-storage, che viene aggiunto automaticamente all'app quando il plug-in App per dispositivi mobili di Azure è incluso nel progetto.</span><span class="sxs-lookup"><span data-stu-id="c68c2-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="c68c2-116">Il progetto di avvio rapido include entrambi questi plug-in.</span><span class="sxs-lookup"><span data-stu-id="c68c2-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="c68c2-117">In Esplora soluzioni di Visual Studio,aprire index.js e sostituire il codice seguente</span><span class="sxs-lookup"><span data-stu-id="c68c2-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="c68c2-118">con questo codice:</span><span class="sxs-lookup"><span data-stu-id="c68c2-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="c68c2-119">Sostituire quindi il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c68c2-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="c68c2-120">con questo codice:</span><span class="sxs-lookup"><span data-stu-id="c68c2-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="c68c2-121">Le aggiunte di codice precedenti inizializzano l'archivio locale e definiscono una tabella locale che corrisponde ai valori di colonna usati nel back-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="c68c2-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="c68c2-122">Non è necessario includere tutti i valori delle colonne in questo codice.  Il campo `version` viene gestito dal back-end per dispositivi mobili e viene usato per la risoluzione dei conflitti.</span><span class="sxs-lookup"><span data-stu-id="c68c2-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="c68c2-123">Per ottenere un riferimento al contesto di sincronizzazione, chiamare **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="c68c2-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="c68c2-124">Il contesto di sincronizzazione aiuta a mantenere le relazioni tra tabelle rilevando le modifiche apportate da un'app client in tutte le tabelle ed eseguendone il push quando viene chiamato `.push()` .</span><span class="sxs-lookup"><span data-stu-id="c68c2-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="c68c2-125">Aggiornare l'URL dell'applicazione con l'URL dell'applicazione App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="c68c2-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="c68c2-126">Quindi, sostituire il codice:</span><span class="sxs-lookup"><span data-stu-id="c68c2-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="c68c2-127">con questo codice:</span><span class="sxs-lookup"><span data-stu-id="c68c2-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="c68c2-128">Il codice precedente inizializza il contesto di sincronizzazione e quindi chiama getSyncTable (invece di getTable) per ottenere un riferimento alla tabella locale.</span><span class="sxs-lookup"><span data-stu-id="c68c2-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="c68c2-129">Questo codice usa il database locale per tutte le operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD, Create, Read, Update, Delete) sulle tabelle.</span><span class="sxs-lookup"><span data-stu-id="c68c2-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="c68c2-130">In questo esempio si esegue una semplice gestione degli errori nei conflitti di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="c68c2-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="c68c2-131">Una vera applicazione gestirà i diversi errori come condizioni di rete, conflitti di server e altro.</span><span class="sxs-lookup"><span data-stu-id="c68c2-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="c68c2-132">Per esempi di codice, vedere l' [esempio di sincronizzazione offline].</span><span class="sxs-lookup"><span data-stu-id="c68c2-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="c68c2-133">Successivamente, aggiungere questa funzione per eseguire la sincronizzazione effettiva.</span><span class="sxs-lookup"><span data-stu-id="c68c2-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="c68c2-134">Decidere quando effettuare il push delle modifiche nel back-end dell'app per dispositivi mobili chiamando **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="c68c2-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="c68c2-135">Ad esempio, è possibile chiamare **syncBackend** in un gestore eventi associato a un pulsante di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="c68c2-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="c68c2-136">Considerazioni sulla sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="c68c2-136">Offline sync considerations</span></span>

<span data-ttu-id="c68c2-137">Nell'esempio, il metodo **push** di **syncContext** viene chiamato solo all'avvio dell'app nella funzione di callback per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c68c2-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="c68c2-138">In un'applicazione vera e propria è anche possibile attivare questa funzionalità di sincronizzazione manualmente o quando lo stato della rete cambia.</span><span class="sxs-lookup"><span data-stu-id="c68c2-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="c68c2-139">Quando viene effettuato il pull in una tabella con aggiornamenti locali in sospeso rilevati dal contesto, tale operazione attiva automaticamente un'operazione push.</span><span class="sxs-lookup"><span data-stu-id="c68c2-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="c68c2-140">Quando si aggiornano, aggiungono e completano elementi in questo esempio, è possibile omettere la chiamata **push** esplicita, perché potrebbe essere ridondante.</span><span class="sxs-lookup"><span data-stu-id="c68c2-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="c68c2-141">Nel codice fornito viene eseguita una query su tutti i record presenti nella tabella TodoItem remota, ma è anche possibile filtrare i record passando un ID query e una query a **push**.</span><span class="sxs-lookup"><span data-stu-id="c68c2-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="c68c2-142">Per altre informazioni, vedere la sezione *Sincronizzazione incrementale* in [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="c68c2-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="c68c2-143">(Facoltativo) Disabilitare l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="c68c2-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="c68c2-144">Se non si vuole configurare l'autenticazione prima di testare la sincronizzazione offline, impostare come commento la funzione di callback per l'accesso, ma lasciare il codice all'interno della funzione di callback in cui sono stati rimossi i commenti.</span><span class="sxs-lookup"><span data-stu-id="c68c2-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="c68c2-145">Dopo l'impostazione come commento delle righe di accesso, il codice sarà come segue:</span><span class="sxs-lookup"><span data-stu-id="c68c2-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="c68c2-146">A questo punto, l'app viene sincronizzata con il back-end di Azure quando si esegue l'app.</span><span class="sxs-lookup"><span data-stu-id="c68c2-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="c68c2-147">Eseguire l'app client</span><span class="sxs-lookup"><span data-stu-id="c68c2-147">Run the client app</span></span>
<span data-ttu-id="c68c2-148">Con la sincronizzazione offline abilitata, è possibile eseguire l'applicazione client almeno una volta in ogni piattaforma per popolare il database di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="c68c2-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="c68c2-149">Più avanti viene simulato uno scenario offline e vengono modificati i dati nell'archivio locale mentre l'app è offline.</span><span class="sxs-lookup"><span data-stu-id="c68c2-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="c68c2-150">(Facoltativo) Testare il comportamento di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="c68c2-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="c68c2-151">In questa sezione viene modificato il progetto client per simulare uno scenario offline usando un URL di applicazione non valido per il back-end.</span><span class="sxs-lookup"><span data-stu-id="c68c2-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="c68c2-152">Quando si aggiungono o si modificano elementi di dati, queste modifiche vengono conservate nell'archivio locale, ma non vengono sincronizzate con l'archivio dati back-end fino a quando non viene ristabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="c68c2-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="c68c2-153">In Esplora soluzioni aprire il file di progetto index.js e modificare l'URL dell'applicazione, in modo che punti a un URL non valido, come nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c68c2-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="c68c2-154">Nel file Index. HTML aggiornare l'elemento `<meta>` CSP con lo stesso URL non valido.</span><span class="sxs-lookup"><span data-stu-id="c68c2-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="c68c2-155">Compilare ed eseguire l'app client e notare che un'eccezione viene registrata nella console quando l'app prova a sincronizzarsi con il back-end dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c68c2-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="c68c2-156">Gli eventuali nuovi elementi aggiunti esistono solo nell'archivio locale fino a quando non ne viene effettuato il push nel back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="c68c2-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="c68c2-157">L'app client si comporta come se fosse connessa al back-end.</span><span class="sxs-lookup"><span data-stu-id="c68c2-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="c68c2-158">Chiudere l'app e riavviarla per verificare che i nuovi elementi creati siano salvati in modo permanente nell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="c68c2-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="c68c2-159">(Facoltativo) Usare Visual Studio per visualizzare la tabella di database SQL di Azure per verificare che i dati nel database back-end non siano cambiati.</span><span class="sxs-lookup"><span data-stu-id="c68c2-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="c68c2-160">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="c68c2-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="c68c2-161">Passare al database in **Azure**->**Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="c68c2-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="c68c2-162">Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c68c2-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="c68c2-163">È ora possibile passare alla tabella di database SQL e al relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="c68c2-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="c68c2-164">(Facoltativo) Testare la riconnessione al back-end mobile</span><span class="sxs-lookup"><span data-stu-id="c68c2-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="c68c2-165">In questa sezione, l'app viene riconnessa al back-end del'app per dispositivi mobili, azione che simula il ritorno dell'app allo stato online.</span><span class="sxs-lookup"><span data-stu-id="c68c2-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="c68c2-166">Quando si esegue l'accesso, i dati verranno sincronizzati con il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="c68c2-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="c68c2-167">Riaprire index. js e ripristinare l'URL dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c68c2-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="c68c2-168">Riaprire index.htnl e correggere l'URL dell'applicazione nell'elemento `<meta>` CSP.</span><span class="sxs-lookup"><span data-stu-id="c68c2-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="c68c2-169">Ricompilare ed eseguire l'app client.</span><span class="sxs-lookup"><span data-stu-id="c68c2-169">Rebuild and run the client app.</span></span> <span data-ttu-id="c68c2-170">L'app prova a eseguire la sincronizzazione con il back-end dell'app per dispositivi mobili dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c68c2-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="c68c2-171">Verificare che non vengano registrate eccezioni nella console di debug.</span><span class="sxs-lookup"><span data-stu-id="c68c2-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="c68c2-172">(Facoltativo) Visualizzare i dati aggiornati usando Esplora oggetti di SQL Server o uno strumento REST come Fiddler.</span><span class="sxs-lookup"><span data-stu-id="c68c2-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="c68c2-173">Si noti che i dati sono stati sincronizzati tra il database di back-end e l'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="c68c2-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="c68c2-174">Si noti che i dati sono stati sincronizzati tra il database e l'archivio locale e includono gli elementi aggiunti mentre l'app era disconnessa.</span><span class="sxs-lookup"><span data-stu-id="c68c2-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c68c2-175">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c68c2-175">Additional resources</span></span>
* <span data-ttu-id="c68c2-176">[Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure]</span><span class="sxs-lookup"><span data-stu-id="c68c2-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="c68c2-177">[Visual Studio Tools per Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="c68c2-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c68c2-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c68c2-178">Next steps</span></span>
* <span data-ttu-id="c68c2-179">Nell'[esempio di sincronizzazione offline] sono disponibili informazioni sulle funzionalità di sincronizzazione offline più avanzate, ad esempio la risoluzione dei conflitti.</span><span class="sxs-lookup"><span data-stu-id="c68c2-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="c68c2-180">Vedere le informazioni di riferimento sull'API di sincronizzazione offline nella [documentazione per l'API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="c68c2-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="c68c2-181">[avvio rapido di Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c68c2-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="c68c2-182">[esempio di sincronizzazione offline]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="c68c2-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="c68c2-183">[Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="c68c2-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="c68c2-184">[Visual Studio Tools per Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="c68c2-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
