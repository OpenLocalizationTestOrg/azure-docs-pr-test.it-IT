---
title: aaaEnable sincronizzazione offline per l'App Mobile di Azure (Android)
description: Informazioni su come toouse App per dispositivi mobili del servizio App toocache e sincronizzazione dati offline nell'applicazione Android
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
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="050fd-103">Abilitare la sincronizzazione offline per l'app per dispositivi mobili di Android</span><span class="sxs-lookup"><span data-stu-id="050fd-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="050fd-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="050fd-104">Overview</span></span>
<span data-ttu-id="050fd-105">In questa esercitazione vengono illustrate funzionalità di sincronizzazione non in linea hello di App mobili di Azure per Android.</span><span class="sxs-lookup"><span data-stu-id="050fd-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="050fd-106">Sincronizzazione non in linea consente toointeract gli utenti finali con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="050fd-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="050fd-107">Le modifiche vengono archiviate in un database locale.</span><span class="sxs-lookup"><span data-stu-id="050fd-107">Changes are stored in a local database.</span></span> <span data-ttu-id="050fd-108">Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con back-end remoto hello.</span><span class="sxs-lookup"><span data-stu-id="050fd-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="050fd-109">Se questa è la prima esperienza con App mobili di Azure, è necessario completare prima esercitazione hello [crea un'App Android].</span><span class="sxs-lookup"><span data-stu-id="050fd-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="050fd-110">Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere hello dati estensione pacchetti tooyour di Microsoft Access.</span><span class="sxs-lookup"><span data-stu-id="050fd-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="050fd-111">Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="050fd-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="050fd-112">toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="050fd-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="050fd-113">Aggiornamento di sincronizzazione non in linea di hello app toosupport</span><span class="sxs-lookup"><span data-stu-id="050fd-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="050fd-114">Con la sincronizzazione offline, leggere scrittura tooand da un *tabella sincronizzazione* (utilizzando hello *IMobileServiceSyncTable* interfaccia), che fa parte di un **SQLite** database sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="050fd-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="050fd-115">toopush e pull delle modifiche tra il dispositivo di hello e servizi mobili di Azure, utilizzare un *contesto di sincronizzazione* (*MobileServiceClient.SyncContext*), che è inizializzare con database locali hello toostore dati in locale.</span><span class="sxs-lookup"><span data-stu-id="050fd-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="050fd-116">In `TodoActivity.java`, impostare come commento la definizione esistente di hello `mToDoTable` e rimuovere il commento di versione di hello sincronizzazione tabella:</span><span class="sxs-lookup"><span data-stu-id="050fd-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="050fd-117">In hello `onCreate` (metodo), impostare come commento l'inizializzazione esistente hello di `mToDoTable` e rimuovere il commento da questa definizione:</span><span class="sxs-lookup"><span data-stu-id="050fd-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="050fd-118">In `refreshItemsFromTable` commento hello definizione di `results` e rimuovere il commento da questa definizione:</span><span class="sxs-lookup"><span data-stu-id="050fd-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="050fd-119">Commento hello definizione di `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="050fd-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="050fd-120">Rimuovere il commento definizione hello di `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="050fd-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="050fd-121">Rimuovere il commento definizione hello di `sync`:</span><span class="sxs-lookup"><span data-stu-id="050fd-121">Uncomment hello definition of `sync`:</span></span>
   
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

## <a name="test-hello-app"></a><span data-ttu-id="050fd-122">Test hello app</span><span class="sxs-lookup"><span data-stu-id="050fd-122">Test hello app</span></span>
<span data-ttu-id="050fd-123">In questa sezione, verificare il comportamento di hello con Wi-Fi in e quindi disattivare Wi-Fi toocreate uno scenario non in linea.</span><span class="sxs-lookup"><span data-stu-id="050fd-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="050fd-124">Quando si aggiungono elementi di dati, vengono mantenuti nell'archivio SQLite locale hello, ma servizio mobile toohello non sincronizzato finché non si preme hello **aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="050fd-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="050fd-125">Altre applicazioni potrebbero avere requisiti diversi riguardanti quando i dati devono toobe sincronizzato, ma per scopi dimostrativi per questa esercitazione sono utente hello richiederlo in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="050fd-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="050fd-126">Quando si preme il pulsante, viene avviata una nuova attività in background.</span><span class="sxs-lookup"><span data-stu-id="050fd-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="050fd-127">Viene innanzitutto inserito tutte le modifiche apportate toohello archivio locale utilizzando il contesto di sincronizzazione, quindi modificato pull tutti i dati dalla tabella locale toohello Azure.</span><span class="sxs-lookup"><span data-stu-id="050fd-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="050fd-128">Test offline</span><span class="sxs-lookup"><span data-stu-id="050fd-128">Offline testing</span></span>
1. <span data-ttu-id="050fd-129">Sul posto hello dispositivo o il simulatore in *modalità aereo*.</span><span class="sxs-lookup"><span data-stu-id="050fd-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="050fd-130">in modo da creare uno scenario offline.</span><span class="sxs-lookup"><span data-stu-id="050fd-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="050fd-131">Aggiungere alcuni elementi *ToDo* o contrassegnare alcuni elementi come completati.</span><span class="sxs-lookup"><span data-stu-id="050fd-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="050fd-132">Chiudere hello dispositivo o simulatore (o app hello chiusura forzata) e riavviare.</span><span class="sxs-lookup"><span data-stu-id="050fd-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="050fd-133">Verificare che le modifiche sono state mantenute nel dispositivo hello momento che vengono mantenuti nell'archivio di SQLite locale hello.</span><span class="sxs-lookup"><span data-stu-id="050fd-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="050fd-134">Visualizzare il contenuto di hello di hello Azure *TodoItem* della tabella con uno strumento SQL, ad esempio *SQL Server Management Studio*, o un client REST, ad esempio *Fiddler* o  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="050fd-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="050fd-135">Verificare che dispongano di nuovi elementi hello *non* stati sincronizzati toohello server</span><span class="sxs-lookup"><span data-stu-id="050fd-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="050fd-136">Per un back-end di Node.js, visitare toohello [portale di Azure](https://portal.azure.com/), nell'App Mobile back-end, fare clic su **tabelle facile** > **TodoItem** contenuto hello tooview di hello `TodoItem` tabella.</span><span class="sxs-lookup"><span data-stu-id="050fd-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="050fd-137">Per un back-end .NET, tabella hello visualizzazione contenuto o con uno strumento SQL, ad esempio *SQL Server Management Studio*, o un client REST, ad esempio *Fiddler* o *Postman*.</span><span class="sxs-lookup"><span data-stu-id="050fd-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="050fd-138">Attivare Wi-Fi nel dispositivo hello o un simulatore.</span><span class="sxs-lookup"><span data-stu-id="050fd-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="050fd-139">Premere quindi hello **aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="050fd-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="050fd-140">Visualizzare di nuovo dati TodoItem hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="050fd-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="050fd-141">Hello che dovrebbe ora apparire TodoItems nuove e modificate.</span><span class="sxs-lookup"><span data-stu-id="050fd-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="050fd-142">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="050fd-142">Additional Resources</span></span>
* <span data-ttu-id="050fd-143">[sincronizzazione dati Offline nelle App mobili di Azure]</span><span class="sxs-lookup"><span data-stu-id="050fd-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="050fd-144">[Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure] \(Nota: hello video si trova in servizi mobili, ma non in linea sincronizzazione funziona in modo analogo in App mobili di Azure\)</span><span class="sxs-lookup"><span data-stu-id="050fd-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[sincronizzazione dati Offline nelle App mobili di Azure]: app-service-mobile-offline-data-sync.md

[crea un'App Android]: app-service-mobile-android-get-started.md

[Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

