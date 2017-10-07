---
title: aaaEnable sincronizzazione offline per l'App Mobile di Azure (Cordova) | Documenti Microsoft
description: Informazioni su come toouse App del servizio Mobile App toocache e sincronizzazione dati offline nella propria applicazione Cordova
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
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="ac0c6-103">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Cordova</span><span class="sxs-lookup"><span data-stu-id="ac0c6-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="ac0c6-104">In questa esercitazione introduce funzionalità di sincronizzazione non in linea hello di App mobili di Azure per Cordova.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="ac0c6-105">Sincronizzazione non in linea consente toointeract gli utenti finali con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="ac0c6-106">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="ac0c6-107">Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con servizio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="ac0c6-108">In questa esercitazione si basa sull'hello Cordova delle Guide rapide soluzione per App per dispositivi mobili creati quando si completa hello esercitazione [avvio rapido di Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="ac0c6-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="ac0c6-109">In questa esercitazione è aggiornare hello delle Guide rapide tooadd offline caratteristiche della soluzione di App mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="ac0c6-110">È inoltre evidenziati codice specifico per la linea hello in app hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="ac0c6-111">toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="ac0c6-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="ac0c6-112">Per informazioni dettagliate sull'utilizzo di API, vedere hello [documentazione dell'API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="ac0c6-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="ac0c6-113">Aggiungi soluzione di sincronizzazione non in linea toohello Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="ac0c6-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="ac0c6-114">aggiungere il codice di sincronizzazione non in linea Hello toohello app.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="ac0c6-115">Sincronizzazione non in linea richiede plug-in cordova-sqlite-archiviazione hello, che viene aggiunto automaticamente app tooyour quando plug-in App mobili di Azure hello è incluso nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="ac0c6-116">progetto di avvio rapido Hello include entrambi questi plug-in.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="ac0c6-117">In Esplora soluzioni di Visual Studio, aprire index.js e sostituire hello seguente di codice</span><span class="sxs-lookup"><span data-stu-id="ac0c6-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="ac0c6-118">con questo codice:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="ac0c6-119">Successivamente, sostituire hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="ac0c6-120">con questo codice:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-120">with this code:</span></span>

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

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    <span data-ttu-id="ac0c6-121">inizializzare l'archivio locale hello Hello aggiunte di codice precedente e definire una tabella locale che corrisponde a valori di colonna hello utilizzati in di Azure back-end.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="ac0c6-122">(Non è necessario tooinclude tutti i valori di colonna in questo codice.)  Hello `version` campo gestito dal back-end mobile hello e viene utilizzato per la risoluzione dei conflitti.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="ac0c6-123">Ottenere un contesto di sincronizzazione toohello riferimento chiamando **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="ac0c6-124">Hello contesto di sincronizzazione consente di mantenere le relazioni tra tabelle e di rilevamento e il push delle modifiche in tutte le tabelle modificato quando un'app client `.push()` viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="ac0c6-125">Aggiornare l'URL dell'applicazione Mobile App tooyour URL applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="ac0c6-126">Quindi, sostituire il codice:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="ac0c6-127">con questo codice:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-127">with this code:</span></span>

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="ac0c6-128">Hello precedente codice inizializza il contesto di sincronizzazione hello e quindi chiama tooget getSyncTable (anziché getTable) una tabella di riferimento toohello locale.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="ac0c6-129">Il database locale di hello utilizza codice per tutti creare, leggere, aggiornare ed eliminazione (CRUD) nella tabella.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="ac0c6-130">In questo esempio si esegue una semplice gestione degli errori nei conflitti di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="ac0c6-131">Un'applicazione reale si gestisce hello diversi errori, ad esempio le condizioni della rete, server è in conflitto e altri.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="ac0c6-132">Per esempi di codice, vedere hello [esempio di sincronizzazione non in linea].</span><span class="sxs-lookup"><span data-stu-id="ac0c6-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="ac0c6-133">Successivamente, aggiungere la sincronizzazione di funzione tooperform hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="ac0c6-134">Si decide quando toopush cambia back-end App Mobile toohello chiamando **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="ac0c6-135">Ad esempio, è possibile chiamare **syncBackend** in un evento gestore tooa legati sincronizzazione pulsante.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="ac0c6-136">Considerazioni sulla sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="ac0c6-136">Offline sync considerations</span></span>

<span data-ttu-id="ac0c6-137">Nell'esempio hello hello **push** metodo **syncContext** viene chiamato solo all'avvio dell'app in funzione di callback hello per account di accesso.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="ac0c6-138">In un'applicazione reale, è possibile apportare questa funzionalità di sincronizzazione attivata manualmente o quando cambia stato rete hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="ac0c6-139">Quando viene eseguita un'operazione di pull in una tabella che è in sospeso aggiornamenti locali registrati dal contesto hello, che pull operazione automaticamente i trigger di push.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="ac0c6-140">Quando l'aggiornamento, l'aggiunta e il completamento di elementi in questo esempio, è possibile omettere hello esplicita **push** chiamare, perché potrebbe essere ridondante.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="ac0c6-141">Nel codice hello fornito, tutti i record nella tabella todoItem remoto hello esecuzione di query, ma è anche possibile toofilter record passando un id di query e una query troppo**push**.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="ac0c6-142">Per ulteriori informazioni, vedere la sezione hello *sincronizzazione incrementale* in [sincronizzazione dati Offline nelle App mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="ac0c6-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="ac0c6-143">(Facoltativo) Disabilitare l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="ac0c6-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="ac0c6-144">Se si non desidera tooset autenticazione prima di testare la sincronizzazione non in linea, impostare come commento la funzione di callback hello per account di accesso, ma lasciare hello codice all'interno di rimuovere la funzione di callback hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="ac0c6-145">Dopo l'impostazione come commento le righe di account di accesso hello, codice hello seguente:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="ac0c6-146">A questo punto, hello app esegue la sincronizzazione con il back-end Azure quando si esegue l'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="ac0c6-147">Eseguire app di hello client</span><span class="sxs-lookup"><span data-stu-id="ac0c6-147">Run hello client app</span></span>
<span data-ttu-id="ac0c6-148">Con questo punto è abilitata la sincronizzazione non in linea, è possibile eseguire un'applicazione hello client almeno una volta in ogni piattaforma per popolare il database di archivio locale hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="ac0c6-149">In un secondo momento, simulare uno scenario offline e modificare i dati di hello nell'archivio locale hello mentre l'applicazione hello è offline.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="ac0c6-150">(Facoltativo) Testare il comportamento di sincronizzazione hello</span><span class="sxs-lookup"><span data-stu-id="ac0c6-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="ac0c6-151">In questa sezione è modificare hello client progetto toosimulate uno scenario offline tramite un URL dell'applicazione non valido per il back-end.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="ac0c6-152">Quando si aggiunge o modifica gli elementi di dati, queste modifiche vengono mantenute nell'archivio locale, ma non sono sincronizzati toohello archivio di dati back-end fino a quando non viene ristabilita la connessione di hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="ac0c6-153">Nel hello Esplora soluzioni, aprire il file di progetto index.js hello e modificare hello applicazione URL toopoint a un URL non valido, ad esempio hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ac0c6-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="ac0c6-154">In index.html, aggiornare hello CSP `<meta>` elemento con hello stesso URL non valido.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="ac0c6-155">Compilare ed eseguire app client hello e si noti che un'eccezione viene registrata nella console di hello quando hello app tenta di sincronizzarsi con back-end hello dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="ac0c6-156">I nuovi elementi che aggiunti esistono solo nell'archivio locale di hello fino a quando queste vengono inviate back-end mobile toohello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="ac0c6-157">app client Hello si comporta come se fosse connesso toohello di back-end.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="ac0c6-158">Chiudere l'applicazione hello e riavviarlo tooverify che è stato creato in base ai nuovi elementi hello siano archivio locale toohello persistente.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="ac0c6-159">(Facoltativo) Utilizzare Visual Studio tooview toosee di tabella del Database SQL di Azure che hello dati nel database back-end hello non vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="ac0c6-160">In Visual Studio aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="ac0c6-161">Esplorare database tooyour **Azure**->**database SQL**.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="ac0c6-162">Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="ac0c6-163">È possibile cercare tooyour tabella di database SQL e il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="ac0c6-164">(Facoltativo) Test hello riconnessione tooyour mobile back-end</span><span class="sxs-lookup"><span data-stu-id="ac0c6-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="ac0c6-165">In questa sezione si riconnette hello app toohello mobile back-end, che simula l'applicazione hello proveniente da uno stato online.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="ac0c6-166">Quando si accede, i dati sono back-end mobile tooyour sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="ac0c6-167">Riaprire index.js e ripristinare l'URL dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="ac0c6-168">Riaprire index.html e correggere l'URL dell'applicazione hello in hello CSP `<meta>` elemento.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="ac0c6-169">Ricompilare ed eseguire l'applicazione client hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="ac0c6-170">app Hello tenta toosync con back-end dell'app mobile hello dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="ac0c6-171">Verificare che nessuna eccezione vengono registrata nella console di debug hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="ac0c6-172">(Facoltativo) Hello visualizzazione aggiornata dei dati utilizzando Esplora oggetti di SQL Server o uno strumento REST come Fiddler.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="ac0c6-173">Si noti hello dati sono stati sincronizzati tra i database di back-end hello e archivio locale hello.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="ac0c6-174">Avviso hello dati sincronizzati tra database hello e archivio locale hello e contiene elementi hello che aggiunti mentre l'app è stata disconnessa.</span><span class="sxs-lookup"><span data-stu-id="ac0c6-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac0c6-175">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ac0c6-175">Additional resources</span></span>
* <span data-ttu-id="ac0c6-176">[sincronizzazione dati Offline nelle App mobili di Azure]</span><span class="sxs-lookup"><span data-stu-id="ac0c6-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="ac0c6-177">[Visual Studio Tools per Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="ac0c6-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac0c6-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac0c6-178">Next steps</span></span>
* <span data-ttu-id="ac0c6-179">Esaminare più avanzate funzionalità di sincronizzazione non in linea, ad esempio la risoluzione dei conflitti in hello [esempio di sincronizzazione non in linea]</span><span class="sxs-lookup"><span data-stu-id="ac0c6-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="ac0c6-180">Esaminare la sincronizzazione non in linea hello riferimento all'API in hello [documentazione dell'API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="ac0c6-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[avvio rapido di Apache Cordova]: app-service-mobile-cordova-get-started.md
[esempio di sincronizzazione non in linea]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[sincronizzazione dati Offline nelle App mobili di Azure]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools per Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
