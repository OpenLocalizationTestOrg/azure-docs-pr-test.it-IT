---
title: aaaHow tooUse iOS SDK per App mobili di Azure
description: Come tooUse iOS SDK per App mobili di Azure
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="006e6-103">Come tooUse iOS libreria Client per App mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="006e6-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="006e6-104">Questa guida illustra tooperform scenari comuni di utilizzo più recenti hello [iOS App mobili di Azure SDK][1].</span><span class="sxs-lookup"><span data-stu-id="006e6-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="006e6-105">Nel caso di nuove app per dispositivi mobili tooAzure, completare innanzitutto [avvio rapido di Azure Mobile app] toocreate un back-end, creare una tabella e scaricare un progetto Xcode iOS preesistente.</span><span class="sxs-lookup"><span data-stu-id="006e6-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="006e6-106">In questa Guida, l'attenzione su hello del client iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="006e6-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="006e6-107">toolearn ulteriori informazioni sugli hello SDK lato server per hello di back-end, vedere hello Server SDK oggetti.</span><span class="sxs-lookup"><span data-stu-id="006e6-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="006e6-108">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="006e6-108">Reference documentation</span></span>
<span data-ttu-id="006e6-109">Hello documentazione di riferimento per i client iOS hello SDK è disponibile in: [iOS App mobili di Azure Client riferimento][2].</span><span class="sxs-lookup"><span data-stu-id="006e6-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="006e6-110">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="006e6-110">Supported Platforms</span></span>
<span data-ttu-id="006e6-111">Hello iOS SDK supporta progetti Objective-C, progetti Swift 2.2 e 2.3 Swift progetti per iOS versione 8.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="006e6-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="006e6-112">l'autenticazione "server-flusso" Hello utilizza WebView per hello presentata l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="006e6-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="006e6-113">Se hello dispositivo non è in grado di toopresent una UI WebView, sarà necessario un altro metodo di autenticazione che è di fuori ambito hello del prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="006e6-114">Questo SDK non è quindi adatto per i dispositivi di tipo controllo o con restrizioni simili.</span><span class="sxs-lookup"><span data-stu-id="006e6-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="006e6-115"><a name="Setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="006e6-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="006e6-116">In questa guida si presuppone che siano stati creati un backend e una tabella.</span><span class="sxs-lookup"><span data-stu-id="006e6-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="006e6-117">Questa guida presuppone che la tabella hello con lo stesso schema come tabelle hello in tali esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="006e6-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="006e6-118">In questa guida si presuppone inoltre che nel codice, si faccia riferimento a `MicrosoftAzureMobile.framework` e si importi `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="006e6-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="006e6-119"><a name="create-client"></a>Procedura: creare Client</span><span class="sxs-lookup"><span data-stu-id="006e6-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="006e6-120">tooaccess un back-end di App mobili di Azure nel progetto, creare un `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="006e6-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="006e6-121">Sostituire `AppUrl` con URL app hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="006e6-122">È possibile lasciare `gatewayURLString` e `applicationKey` vuoti.</span><span class="sxs-lookup"><span data-stu-id="006e6-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="006e6-123">Se si configura un gateway per l'autenticazione, popolare `gatewayURLString` con hello gateway URL.</span><span class="sxs-lookup"><span data-stu-id="006e6-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="006e6-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="006e6-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="006e6-126"><a name="table-reference"></a>Procedura: Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="006e6-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="006e6-127">tooaccess o l'aggiornamento dati, creare una tabella di riferimento toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="006e6-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="006e6-128">Sostituire `TodoItem` con nome hello della tabella</span><span class="sxs-lookup"><span data-stu-id="006e6-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="006e6-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="006e6-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="006e6-131"><a name="querying"></a>Procedura: Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="006e6-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="006e6-132">toocreate una query sul database, hello query `MSTable` oggetto.</span><span class="sxs-lookup"><span data-stu-id="006e6-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="006e6-133">Hello query seguente vengono ottenuti tutti gli elementi di hello in `TodoItem` e registri di hello testo di ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="006e6-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="006e6-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="006e6-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="006e6-136"><a name="filtering"></a>Procedura: Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="006e6-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="006e6-137">risultati toofilter, sono disponibili numerose opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="006e6-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="006e6-138">toofilter utilizzando un predicato, utilizzare un `NSPredicate` e `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="006e6-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="006e6-139">esempio Hello Filtra elementi di dati restituiti toofind solo incompleti Todo.</span><span class="sxs-lookup"><span data-stu-id="006e6-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="006e6-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="006e6-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="006e6-142"><a name="query-object"></a>Procedura: Usare MSQuery</span><span class="sxs-lookup"><span data-stu-id="006e6-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="006e6-143">creare una query complessa, incluso l'ordinamento e paging, tooperform un `MSQuery` dell'oggetto, direttamente o tramite un predicato:</span><span class="sxs-lookup"><span data-stu-id="006e6-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="006e6-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="006e6-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="006e6-146">`MSQuery` consente di controllare diversi comportamenti di query.</span><span class="sxs-lookup"><span data-stu-id="006e6-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="006e6-147">Specificare l'ordine dei risultati</span><span class="sxs-lookup"><span data-stu-id="006e6-147">Specify order of results</span></span>
* <span data-ttu-id="006e6-148">Limite quali campi tooreturn</span><span class="sxs-lookup"><span data-stu-id="006e6-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="006e6-149">Limitare il numero di record tooreturn</span><span class="sxs-lookup"><span data-stu-id="006e6-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="006e6-150">Specificare il conteggio totale nella risposta</span><span class="sxs-lookup"><span data-stu-id="006e6-150">Specify total count in response</span></span>
* <span data-ttu-id="006e6-151">Specificare i parametri della stringa di query personalizzata nella richiesta</span><span class="sxs-lookup"><span data-stu-id="006e6-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="006e6-152">Applicare funzioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="006e6-152">Apply additional functions</span></span>

<span data-ttu-id="006e6-153">Eseguire un `MSQuery` query chiamando `readWithCompletion` sull'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="006e6-154"><a name="sorting"></a>Procedura: Ordinare i dati con MSQuery</span><span class="sxs-lookup"><span data-stu-id="006e6-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="006e6-155">risultati toosort, esaminiamo un esempio.</span><span class="sxs-lookup"><span data-stu-id="006e6-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="006e6-156">richiamare toosort dal testo' campo' crescente e decrescente 'completato', `MSQuery` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="006e6-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="006e6-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="006e6-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="006e6-159"><a name="selecting"></a><a name="parameters"></a>Procedura: Limitare i campi ed espandere i parametri di query di tipo stringa con MSQuery</span><span class="sxs-lookup"><span data-stu-id="006e6-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="006e6-160">toolimit toobe di campi restituiti in una query, specificare nomi hello di campi di hello in hello **selectFields** proprietà.</span><span class="sxs-lookup"><span data-stu-id="006e6-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="006e6-161">Questo esempio viene restituito solo il testo hello e campi completati:</span><span class="sxs-lookup"><span data-stu-id="006e6-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="006e6-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="006e6-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="006e6-164">parametri di stringa di query aggiuntive tooinclude in server hello richiedono (ad esempio, perché li utilizza uno script sul lato server personalizzato), popolare `query.parameters` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="006e6-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="006e6-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="006e6-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="006e6-167"><a name="paging"></a>Procedura: Configurare la dimensione di pagina</span><span class="sxs-lookup"><span data-stu-id="006e6-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="006e6-168">Con App mobili di Azure, i controlli di dimensioni pagina hello hello numero di record che vengono estratti in un momento dalle tabelle di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="006e6-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="006e6-169">Mediante una chiamata troppo`pull` dati vengono quindi batch dei dati, in base alle dimensioni di questa pagina, fino a quando non esistono alcun ulteriori toopull record.</span><span class="sxs-lookup"><span data-stu-id="006e6-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="006e6-170">È possibile tooconfigure una dimensione di pagina utilizzando **MSPullSettings** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="006e6-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="006e6-171">dimensioni di pagina predefinite Hello sono 50 ed esempio hello seguente modifica too3.</span><span class="sxs-lookup"><span data-stu-id="006e6-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="006e6-172">È possibile configurare una dimensione di pagina diversa per finalità di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="006e6-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="006e6-173">Se si dispone di un numero elevato di record di dati di piccole dimensioni, dimensioni pagina elevata riducono il numero di hello di andata e ritorno di server.</span><span class="sxs-lookup"><span data-stu-id="006e6-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="006e6-174">Questa impostazione controlla solo hello dimensione di paging sul lato client hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="006e6-175">Se hello client richiede una dimensione di pagina maggiore rispetto a supportato dal back-end App per dispositivi mobili hello, dimensioni della pagina hello limitate a back-end hello massimo hello è toosupport configurato.</span><span class="sxs-lookup"><span data-stu-id="006e6-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="006e6-176">Questa impostazione è anche hello *numero* dei record di dati non hello *dimensioni in byte*.</span><span class="sxs-lookup"><span data-stu-id="006e6-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="006e6-177">Se si aumentano le dimensioni di pagina client hello, è anche necessario aumentare la dimensione di pagina hello sul server hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="006e6-178">Vedere ["procedura: ridimensionare la paginazione tabella hello"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per hello passaggi toodo questo.</span><span class="sxs-lookup"><span data-stu-id="006e6-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="006e6-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="006e6-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="006e6-181"><a name="inserting"></a>Procedura: Inserire dati</span><span class="sxs-lookup"><span data-stu-id="006e6-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="006e6-182">creare una nuova riga di tabella, tooinsert un `NSDictionary` e richiamare `table insert`.</span><span class="sxs-lookup"><span data-stu-id="006e6-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="006e6-183">Se [lo Schema dinamico] è abilitata, back-end per dispositivi mobili di Azure App Service hello generate automaticamente nuove colonne in base a hello `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="006e6-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="006e6-184">Se `id` non viene fornito, back-end hello genera automaticamente un nuovo ID univoco.</span><span class="sxs-lookup"><span data-stu-id="006e6-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="006e6-185">Fornire una propria `id` toouse indirizzi di posta elettronica, i nomi utente, valori personalizzati come ID.</span><span class="sxs-lookup"><span data-stu-id="006e6-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="006e6-186">La specifica del proprio ID può semplificare l'esecuzione di join e la logica dei database aziendali.</span><span class="sxs-lookup"><span data-stu-id="006e6-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="006e6-187">Hello `result` contiene hello nuovo elemento è stato inserito.</span><span class="sxs-lookup"><span data-stu-id="006e6-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="006e6-188">A seconda della logica di server, i dati modificati rispetto toowhat è stato passato toohello server o potrebbe disporre di ulteriori.</span><span class="sxs-lookup"><span data-stu-id="006e6-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="006e6-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="006e6-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="006e6-191"><a name="modifying"></a>Procedura: Modificare dati</span><span class="sxs-lookup"><span data-stu-id="006e6-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="006e6-192">tooupdate una riga esistente, modificare un elemento e chiamare `update`:</span><span class="sxs-lookup"><span data-stu-id="006e6-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="006e6-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="006e6-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="006e6-195">In alternativa, fornire l'ID di riga hello e campo hello aggiornato:</span><span class="sxs-lookup"><span data-stu-id="006e6-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="006e6-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="006e6-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="006e6-198">Come minimo, hello `id` attributo deve essere impostato quando si eseguono aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="006e6-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="006e6-199"><a name="deleting"></a>Procedura: Eliminare dati</span><span class="sxs-lookup"><span data-stu-id="006e6-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="006e6-200">toodelete un elemento, richiamare `delete` con elemento hello:</span><span class="sxs-lookup"><span data-stu-id="006e6-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="006e6-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="006e6-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="006e6-203">In alternativa, eliminarlo specificando un ID di riga:</span><span class="sxs-lookup"><span data-stu-id="006e6-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="006e6-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="006e6-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="006e6-206">Come minimo, hello `id` attributo deve essere impostato quando si elimina apportato.</span><span class="sxs-lookup"><span data-stu-id="006e6-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="006e6-207"><a name="customapi"></a>Procedura: Chiamare un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="006e6-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="006e6-208">Con un'API personalizzata è possibile esporre qualsiasi funzionalità di back-end.</span><span class="sxs-lookup"><span data-stu-id="006e6-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="006e6-209">Non ha toomap tooa operazione di tabella.</span><span class="sxs-lookup"><span data-stu-id="006e6-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="006e6-210">Non solo si ottengono maggiore controllo sulla messaggistica, è anche possibile lettura/set di intestazioni e cambiare formato del corpo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="006e6-211">modalità di lettura toocreate un'API personalizzata nel back-end hello, toolearn [API personalizzate](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="006e6-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="006e6-212">chiamare un'API personalizzata, toocall `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="006e6-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="006e6-213">richiesta di Hello e risposta contenuto vengono considerati come JSON.</span><span class="sxs-lookup"><span data-stu-id="006e6-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="006e6-214">toouse altri tipi di supporti, [hello di utilizzare altri overload di `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="006e6-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="006e6-215">toomake un `GET` richiesta invece di un `POST` richiesta, il parametro set `HTTPMethod` troppo`"GET"` e parametro `body` troppo`nil` (dal momento che le richieste GET non dispone dei corpi dei messaggi.) Se l'API personalizzata supporta altri verbi HTTP, modificare `HTTPMethod` in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="006e6-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="006e6-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="006e6-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="006e6-218"><a name="templates"></a>Procedura: registrazione delle notifiche multipiattaforma toosend push modelli</span><span class="sxs-lookup"><span data-stu-id="006e6-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="006e6-219">modelli tooregister, passare modelli con il **client.push registerDeviceToken** metodo nell'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="006e6-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="006e6-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="006e6-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="006e6-222">I modelli sono di tipo NSDictionary e possono contenere più modelli di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="006e6-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="006e6-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="006e6-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="006e6-225">Tutti i tag vengono rimossi dalla richiesta di hello per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="006e6-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="006e6-226">i tag tooadd tooinstallations o modelli all'interno di installazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure][4].</span><span class="sxs-lookup"><span data-stu-id="006e6-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="006e6-227">funzionamento delle notifiche toosend utilizzando questi modelli, registrati con [API degli hub di notifica][3].</span><span class="sxs-lookup"><span data-stu-id="006e6-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="006e6-228"><a name="errors"></a>Procedura: Gestire gli errori</span><span class="sxs-lookup"><span data-stu-id="006e6-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="006e6-229">Quando si chiama un back-end mobile di servizio App di Azure, il blocco di completamento hello contiene un `NSError` parametro.</span><span class="sxs-lookup"><span data-stu-id="006e6-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="006e6-230">Quando si verifica un errore, il parametro sarà diverso da Nil.</span><span class="sxs-lookup"><span data-stu-id="006e6-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="006e6-231">Nel codice, si deve controllare questo parametro e gestire l'errore hello secondo le esigenze, come dimostrato nel precedente frammenti di codice hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="006e6-232">file Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] definisce le costanti hello `MSErrorResponseKey`, `MSErrorRequestKey`, e `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="006e6-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="006e6-233">tooget toohello errore relativo a più dati:</span><span class="sxs-lookup"><span data-stu-id="006e6-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="006e6-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="006e6-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="006e6-236">Inoltre, il file hello definisce le costanti per ogni codice di errore:</span><span class="sxs-lookup"><span data-stu-id="006e6-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="006e6-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="006e6-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="006e6-239"><a name="adal"></a>Procedura: autenticare gli utenti con Active Directory Authentication Library hello</span><span class="sxs-lookup"><span data-stu-id="006e6-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="006e6-240">È possibile utilizzare gli utenti toosign di Active Directory Authentication Library (ADAL) hello in un'applicazione tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="006e6-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="006e6-241">L'autenticazione di flusso client utilizzando un provider di identità SDK è preferibile toousing hello `loginWithProvider:completion:` metodo.</span><span class="sxs-lookup"><span data-stu-id="006e6-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="006e6-242">L'autenticazione del flusso client garantisce un'esperienza utente più naturale e consente una maggiore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="006e6-243">Configurare il back-end dell'app mobile per l'accesso AAD hello seguente [come tooconfigure App del servizio per l'account di accesso Active Directory] [ 7] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="006e6-244">Verificare che passaggio facoltativo in hello toocomplete di registrazione di un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="006e6-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="006e6-245">Per iOS, è consigliabile che hello URI di reindirizzamento del modulo hello `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="006e6-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="006e6-246">Per ulteriori informazioni, vedere hello [delle Guide rapide iOS ADAL][8].</span><span class="sxs-lookup"><span data-stu-id="006e6-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="006e6-247">Installare ADAL usando Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="006e6-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="006e6-248">Modificare il hello tooinclude Podfile seguente definizione, la sostituzione **del progetto** con nome hello del progetto Xcode:</span><span class="sxs-lookup"><span data-stu-id="006e6-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="006e6-249">e hello Pod:</span><span class="sxs-lookup"><span data-stu-id="006e6-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="006e6-250">Utilizzando hello Terminal, eseguire `pod install` dalla directory hello contenente il progetto e quindi aprire l'area di lavoro Xcode hello generato (non il progetto hello).</span><span class="sxs-lookup"><span data-stu-id="006e6-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="006e6-251">Aggiungere hello applicazione tooyour di codice seguente, in base toohello lingua in uso.</span><span class="sxs-lookup"><span data-stu-id="006e6-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="006e6-252">In ogni esempio eseguire queste sostituzioni:</span><span class="sxs-lookup"><span data-stu-id="006e6-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="006e6-253">Sostituire **INSERT-autorità-qui** con nome hello del tenant di hello in cui è stato eseguito il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="006e6-254">Il formato deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com. Questo valore può essere copiato da scheda dominio hello in Azure Active Directory in hello [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="006e6-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="006e6-255">Sostituire **INSERT-RESOURCE-ID-qui** con hello client ID per il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="006e6-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="006e6-256">È possibile ottenere l'ID client da hello **avanzate** scheda **impostazioni di Azure Active Directory** nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="006e6-257">Sostituire **INSERT-CLIENT-ID-qui** con ID client hello copiato dall'applicazione client nativa hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="006e6-258">Sostituire **INSERT-REDIRECT-URI-qui** con il sito */.auth/login/done* endpoint, utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="006e6-259">Questo valore dovrebbe essere simile troppo*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="006e6-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="006e6-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-260">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="006e6-261">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="006e6-262"><a name="facebook-sdk"></a>Procedura: autenticare gli utenti con hello SDK Facebook per iOS</span><span class="sxs-lookup"><span data-stu-id="006e6-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="006e6-263">È possibile utilizzare hello SDK Facebook per gli utenti di iOS toosign nell'applicazione con Facebook.</span><span class="sxs-lookup"><span data-stu-id="006e6-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="006e6-264">Mediante l'autenticazione di flusso un client è preferibile toousing hello `loginWithProvider:completion:` metodo.</span><span class="sxs-lookup"><span data-stu-id="006e6-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="006e6-265">l'autenticazione del client del flusso di Hello fornisce un'idea dell'esperienza utente più nativa e consente di personalizzare ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="006e6-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="006e6-266">Configurare il back-end dell'app mobile per l'accesso Facebook seguendo il [come tooconfigure App del servizio per l'account di accesso Facebook] [ 9] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="006e6-267">Installare hello SDK Facebook per iOS da hello seguente [SDK Facebook per iOS - Introduzione] [ 10] documentazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="006e6-268">Anziché creare un'app, è possibile aggiungere una registrazione esistente tooyour piattaforma iOS hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="006e6-269">Documentazione di Facebook include codice Objective-C in hello App delegato.</span><span class="sxs-lookup"><span data-stu-id="006e6-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="006e6-270">Se si utilizza **Swift**, è possibile utilizzare hello seguendo le traduzioni per appdelegate. SWIFT:</span><span class="sxs-lookup"><span data-stu-id="006e6-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="006e6-271">In aggiunta tooadding `FBSDKCoreKit.framework` tooyour del progetto, aggiungere anche un riferimento troppo`FBSDKLoginKit.framework` in hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="006e6-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="006e6-272">Aggiungere hello applicazione tooyour di codice seguente, in base toohello lingua in uso.</span><span class="sxs-lookup"><span data-stu-id="006e6-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="006e6-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-273">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="006e6-274">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="006e6-275"><a name="twitter-fabric"></a>Procedura: Autenticare gli utenti con Twitter Fabric for iOS</span><span class="sxs-lookup"><span data-stu-id="006e6-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="006e6-276">È possibile utilizzare l'infrastruttura per gli utenti di iOS toosign nell'applicazione in uso tramite Twitter.</span><span class="sxs-lookup"><span data-stu-id="006e6-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="006e6-277">L'autenticazione del client del flusso è preferibile toousing hello `loginWithProvider:completion:` del metodo, fornisce un'idea dell'esperienza utente più nativa e consente un'ulteriore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="006e6-278">Configurare il back-end dell'app mobile per l'accesso Twitter seguente hello [come tooconfigure App del servizio per l'account di accesso Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="006e6-279">Per aggiungere il progetto di tooyour dell'infrastruttura di hello seguente [dell'infrastruttura per iOS - Introduzione] documentazione e l'impostazione TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="006e6-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="006e6-280">Per impostazione predefinita, Fabric crea automaticamente un'applicazione Twitter.</span><span class="sxs-lookup"><span data-stu-id="006e6-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="006e6-281">È possibile evitare la creazione di un'applicazione registrando hello chiave Consumer e segreto del cliente è stato creato in precedenza mediante hello frammenti di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="006e6-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="006e6-282">In alternativa, è possibile sostituire la chiave Consumer hello e vedere la sezione valori segreto del cliente di fornire i valori da tooApp servizio con hello in hello [Dashboard infrastruttura].</span><span class="sxs-lookup"><span data-stu-id="006e6-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="006e6-283">Se si sceglie questa opzione, essere certi tooset hello callback URL tooa valore segnaposto, ad esempio `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="006e6-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="006e6-284">Se si sceglie toouse segreti hello creato in precedenza, è possibile aggiungere hello tooyour codice delegato App seguenti:</span><span class="sxs-lookup"><span data-stu-id="006e6-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="006e6-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-285">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="006e6-286">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="006e6-287">Aggiungere hello applicazione tooyour di codice seguente, in base toohello lingua in uso.</span><span class="sxs-lookup"><span data-stu-id="006e6-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="006e6-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-288">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="006e6-289">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-289">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="006e6-290"><a name="google-sdk"></a>Procedura: autenticare gli utenti con hello Google Accedi SDK per iOS</span><span class="sxs-lookup"><span data-stu-id="006e6-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="006e6-291">È possibile utilizzare hello Google Accedi SDK per gli utenti di iOS toosign nell'applicazione utilizzando un account di Google.</span><span class="sxs-lookup"><span data-stu-id="006e6-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="006e6-292">Google ha recentemente annunciato modifiche tootheir OAuth i criteri di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="006e6-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="006e6-293">Modifiche apportate ai criteri richiederà utilizzare hello del SDK di Google in hello future.</span><span class="sxs-lookup"><span data-stu-id="006e6-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="006e6-294">Configurare il back-end dell'app mobile per l'accesso Google hello seguente [come tooconfigure App del servizio per l'account di accesso Google](app-service-mobile-how-to-configure-google-authentication.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="006e6-295">Installare hello Google SDK per iOS da hello seguente [Sign-In Google per iOS - avviare l'integrazione di](https://developers.google.com/identity/sign-in/ios/start-integrating) documentazione.</span><span class="sxs-lookup"><span data-stu-id="006e6-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="006e6-296">È possibile ignorare una sezione "Eseguire l'autenticazione con un Server back-end" hello.</span><span class="sxs-lookup"><span data-stu-id="006e6-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="006e6-297">Aggiungere hello seguenti del delegato tooyour `signIn:didSignInForUser:withError:` (metodo), in base toohello lingua in uso.</span><span class="sxs-lookup"><span data-stu-id="006e6-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="006e6-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="006e6-299">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="006e6-300">Assicurarsi di aggiungere anche hello seguente troppo`application:didFinishLaunchingWithOptions:` nell'app, delegato, sostituendo "SERVER_CLIENT_ID" con hello ID che è stato utilizzato tooconfigure servizio App nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="006e6-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="006e6-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="006e6-302">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="006e6-303">Aggiungere hello seguito codice tooyour applicazione in un UIViewController che implementa hello `GIDSignInUIDelegate` protocollo, in base toohello lingua in uso.</span><span class="sxs-lookup"><span data-stu-id="006e6-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="006e6-304">È stato disconnesso prima da firmare nuovamente e anche se non è necessario tooenter le credenziali di nuovo, viene visualizzato una finestra di dialogo di consenso.</span><span class="sxs-lookup"><span data-stu-id="006e6-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="006e6-305">Chiamare questo metodo solo quando il token di sessione hello è scaduto.</span><span class="sxs-lookup"><span data-stu-id="006e6-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="006e6-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="006e6-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="006e6-307">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="006e6-307">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[avvio rapido di Azure Mobile app]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[lo Schema dinamico]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[Dashboard infrastruttura]: https://www.fabric.io/home
[dell'infrastruttura per iOS - Introduzione]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
