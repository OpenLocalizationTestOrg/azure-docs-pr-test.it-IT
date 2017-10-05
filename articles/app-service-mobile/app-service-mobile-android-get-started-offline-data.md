---
title: Abilitare la sincronizzazione offline per l'app per dispositivi mobili di Azure (Android)
description: Informazioni su come usare le app per dispositivi mobili del servizio app per memorizzare nella cache e sincronizzare i dati offline in un'applicazione Android
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="26eab-103">Abilitare la sincronizzazione offline per l'app per dispositivi mobili di Android</span><span class="sxs-lookup"><span data-stu-id="26eab-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="26eab-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="26eab-104">Overview</span></span>
<span data-ttu-id="26eab-105">Questa esercitazione descrive la funzionalità di sincronizzazione offline delle app per dispositivi mobili di Azure per Android.</span><span class="sxs-lookup"><span data-stu-id="26eab-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="26eab-106">La sincronizzazione offline consente agli utenti finali di interagire con un'app&mdash;visualizzando, aggiungendo e modificando i dati&mdash;anche se non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="26eab-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="26eab-107">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="26eab-107">Changes are stored in a local database.</span></span> <span data-ttu-id="26eab-108">Quando il dispositivo torna online, vengono sincronizzate con il back-end remoto.</span><span class="sxs-lookup"><span data-stu-id="26eab-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="26eab-109">Se questa è la prima esperienza con le app per dispositivi mobili di Azure, è consigliabile completare prima l'esercitazione [Creare un'app Android].</span><span class="sxs-lookup"><span data-stu-id="26eab-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="26eab-110">Se non si usa il progetto server di avvio rapido scaricato, è necessario aggiungere al progetto il pacchetto di estensione per l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="26eab-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="26eab-111">Per altre informazioni sui pacchetti di estensione server, vedere l'articolo relativo all' [utilizzo dell'SDK del server back-end .NET per app per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="26eab-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="26eab-112">Per altre informazioni sulla funzionalità di sincronizzazione offline, vedere l'argomento [Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="26eab-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="26eab-113">Aggiornare l'app per supportare la sincronizzazione offline</span><span class="sxs-lookup"><span data-stu-id="26eab-113">Update the app to support offline sync</span></span>
<span data-ttu-id="26eab-114">Con la sincronizzazione offline si legge e si scrive da una *tabella di sincronizzazione* (usando l'interfaccia *IMobileServiceSyncTable*), che fa parte di un database **SQLite** nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="26eab-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="26eab-115">Per eseguire il push e il pull delle modifiche tra il dispositivo e Servizi mobili di Azure, si usa un *contesto di sincronizzazione* (*MobileServiceClient.SyncContext*), inizializzato con il database locale per archiviare localmente i dati.</span><span class="sxs-lookup"><span data-stu-id="26eab-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="26eab-116">In `TodoActivity.java`, impostare come commento la definizione esistente di `mToDoTable` e rimuovere il commento della versione della tabella di sincronizzazione:</span><span class="sxs-lookup"><span data-stu-id="26eab-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="26eab-117">Nel metodo `onCreate`, impostare come commento l'inizializzazione esistente di `mToDoTable` e rimuovere il commento di questa definizione:</span><span class="sxs-lookup"><span data-stu-id="26eab-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="26eab-118">In `refreshItemsFromTable`, impostare come commento la definizione di `results` e rimuovere il commento di questa definizione:</span><span class="sxs-lookup"><span data-stu-id="26eab-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="26eab-119">Impostare come commento la definizione di `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="26eab-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="26eab-120">Rimuovere il commento dalla definizione di `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="26eab-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="26eab-121">Rimuovere il commento dalla definizione di `sync`:</span><span class="sxs-lookup"><span data-stu-id="26eab-121">Uncomment the definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-the-app"></a><span data-ttu-id="26eab-122">Testare l'app</span><span class="sxs-lookup"><span data-stu-id="26eab-122">Test the app</span></span>
<span data-ttu-id="26eab-123">In questa sezione viene testato il comportamento dell'app con il WiFi attivato e quindi il WiFi viene disattivato per creare uno scenario offline.</span><span class="sxs-lookup"><span data-stu-id="26eab-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="26eab-124">Quando si aggiungono elementi di dati, gli elementi vengono archiviati nell'archivio di SQL Lite, ma vengono sincronizzati con il servizio mobile solo dopo la selezione del pulsante di **aggiornamento** .</span><span class="sxs-lookup"><span data-stu-id="26eab-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="26eab-125">Altre app potrebbero avere requisiti diversi relativi a quando è necessario sincronizzare i dati, ma per, finalità dimostrative, in questa esercitazione la sincronizzazione viene richiesta esplicitamente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="26eab-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="26eab-126">Quando si preme il pulsante, viene avviata una nuova attività in background.</span><span class="sxs-lookup"><span data-stu-id="26eab-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="26eab-127">Viene effettuato prima di tutto il push di tutte le modifiche apportate all'archivio locale usando il contesto di sincronizzazione, quindi viene effettuato il pull di tutti i dati modificati da Azure alla tabella locale.</span><span class="sxs-lookup"><span data-stu-id="26eab-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="26eab-128">Test offline</span><span class="sxs-lookup"><span data-stu-id="26eab-128">Offline testing</span></span>
1. <span data-ttu-id="26eab-129">Attivare la *Modalità aereo*per il dispositivo o il simulatore.</span><span class="sxs-lookup"><span data-stu-id="26eab-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="26eab-130">in modo da creare uno scenario offline.</span><span class="sxs-lookup"><span data-stu-id="26eab-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="26eab-131">Aggiungere alcuni elementi *ToDo* o contrassegnare alcuni elementi come completati.</span><span class="sxs-lookup"><span data-stu-id="26eab-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="26eab-132">Uscire dal dispositivo o dal simulatore (o forzare la chiusura dell'app) e riavviare.</span><span class="sxs-lookup"><span data-stu-id="26eab-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="26eab-133">Verificare che le modifiche siano state rese persistenti nel dispositivo, poiché sono incluse nell'archivio SQLite locale.</span><span class="sxs-lookup"><span data-stu-id="26eab-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="26eab-134">Visualizzare il contenuto della tabella *TodoItem* di Azure mediante uno strumento SQL, come ad esempio *SQL Server Management Studio*, o mediante un client REST, ad esempio *Fiddler* o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="26eab-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="26eab-135">Verificare che i nuovi elementi *non* siano stati sincronizzati con il server</span><span class="sxs-lookup"><span data-stu-id="26eab-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="26eab-136">Per un back-end Node.js, passare al [portale di Azure](https://portal.azure.com/) e nel back-end dell'app per dispositivi mobili fare clic su **Tabelle semplici** > **TodoItem** per visualizzare il contenuto della tabella `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="26eab-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="26eab-137">Per il back-end .NET, visualizzare il contenuto della tabella mediante uno strumento SQL, come ad esempio *SQL Server Management Studio*, o mediante un client REST, ad esempio *Fiddler* o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="26eab-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="26eab-138">Attivare il WiFi nel dispositivo o nel simulatore.</span><span class="sxs-lookup"><span data-stu-id="26eab-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="26eab-139">Premere quindi il pulsante di **aggiornamento** .</span><span class="sxs-lookup"><span data-stu-id="26eab-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="26eab-140">Visualizzare di nuovo i dati TodoItem nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26eab-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="26eab-141">Dovrebbero essere visualizzati gli elementi TodoItems nuovi e modificati.</span><span class="sxs-lookup"><span data-stu-id="26eab-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26eab-142">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="26eab-142">Additional Resources</span></span>
* <span data-ttu-id="26eab-143">[Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure]</span><span class="sxs-lookup"><span data-stu-id="26eab-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="26eab-144">[Cloud Cover: Sincronizzazione offline in Servizi mobili di Azure] \(nota: il video è relativo ai Servizi mobili, ma il funzionamento della sincronizzazione offline è simile nelle app per dispositivi mobili di Azure\)</span><span class="sxs-lookup"><span data-stu-id="26eab-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="26eab-145">[Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="26eab-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="26eab-146">[Creare un'app Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="26eab-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="26eab-147">[Cloud Cover: Sincronizzazione offline in Servizi mobili di Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="26eab-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

