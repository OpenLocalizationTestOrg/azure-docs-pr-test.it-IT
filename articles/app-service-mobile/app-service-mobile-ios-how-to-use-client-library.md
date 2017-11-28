---
title: Come utilizzare iOS SDK per App Mobile di Azure
description: Come utilizzare iOS SDK per App Mobile di Azure
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
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="63d20-103">Come usare la libreria client iOS per le app mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="63d20-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="63d20-104">Questa guida descrive come eseguire scenari comuni usando il più recente [SDK per iOS per le app per dispositivi mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="63d20-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="63d20-105">Se si ha familiarità con le App per dispositivi mobili di Azure, completare innanzitutto [Azure Mobile App Quick Start] per creare un back-end, creare una tabella e scaricare un progetto Xcode iOS preesistente.</span><span class="sxs-lookup"><span data-stu-id="63d20-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="63d20-106">In questa Guida, l'attenzione è posta sul lato client iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="63d20-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="63d20-107">Per altre informazioni sull'SDK sul lato server per il back-end, vedere le procedure per l'SDK del server.</span><span class="sxs-lookup"><span data-stu-id="63d20-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="63d20-108">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="63d20-108">Reference documentation</span></span>
<span data-ttu-id="63d20-109">La documentazione di riferimento per il client SDK per iOS è disponibile qui: [Riferimento al Client iOS di App per dispositivi mobili di Azure][2].</span><span class="sxs-lookup"><span data-stu-id="63d20-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="63d20-110">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="63d20-110">Supported Platforms</span></span>
<span data-ttu-id="63d20-111">L'SDK di iOS supporta progetti Objective-C, Swift 2.2 e Swift 2.3 per le versioni iOS 8.0 o successive.</span><span class="sxs-lookup"><span data-stu-id="63d20-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="63d20-112">L'autenticazione "flusso server" usa una visualizzazione Web per l'interfaccia utente presentata.</span><span class="sxs-lookup"><span data-stu-id="63d20-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="63d20-113">Se il dispositivo non è in grado di presentare un'interfaccia utente con visualizzazione Web, è necessario un altro metodo di autenticazione non incluso nell'ambito del prodotto.</span><span class="sxs-lookup"><span data-stu-id="63d20-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="63d20-114">Questo SDK non è quindi adatto per i dispositivi di tipo controllo o con restrizioni simili.</span><span class="sxs-lookup"><span data-stu-id="63d20-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="63d20-115"><a name="Setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="63d20-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="63d20-116">In questa guida si presuppone che siano stati creati un backend e una tabella.</span><span class="sxs-lookup"><span data-stu-id="63d20-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="63d20-117">In questa guida si presuppone che la tabella abbia lo stesso schema delle tabelle presenti in tali esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="63d20-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="63d20-118">In questa guida si presuppone inoltre che nel codice, si faccia riferimento a `MicrosoftAzureMobile.framework` e si importi `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="63d20-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="63d20-119"><a name="create-client"></a>Procedura: creare Client</span><span class="sxs-lookup"><span data-stu-id="63d20-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="63d20-120">Per accedere a un back-end di applicazioni per dispositivi mobili di Azure nel progetto, creare un `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="63d20-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="63d20-121">Sostituire `AppUrl` con l'URL dell'app.</span><span class="sxs-lookup"><span data-stu-id="63d20-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="63d20-122">È possibile lasciare `gatewayURLString` e `applicationKey` vuoti.</span><span class="sxs-lookup"><span data-stu-id="63d20-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="63d20-123">Se si configura un gateway per l'autenticazione, popolare `gatewayURLString` con l'URL del gateway.</span><span class="sxs-lookup"><span data-stu-id="63d20-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="63d20-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="63d20-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="63d20-126"><a name="table-reference"></a>Procedura: Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="63d20-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="63d20-127">Per l'accesso o l'aggiornamento dei dati, creare un riferimento alla tabella di back-end.</span><span class="sxs-lookup"><span data-stu-id="63d20-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="63d20-128">Sostituire `TodoItem` con il nome della tabella</span><span class="sxs-lookup"><span data-stu-id="63d20-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="63d20-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="63d20-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="63d20-131"><a name="querying"></a>Procedura: Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="63d20-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="63d20-132">Per creare una query di database, eseguire una query sull'oggetto `MSTable` .</span><span class="sxs-lookup"><span data-stu-id="63d20-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="63d20-133">La query seguente ottiene tutti gli elementi in `TodoItem` e registra il testo di ciascun elemento.</span><span class="sxs-lookup"><span data-stu-id="63d20-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="63d20-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-134">**Objective-C**:</span></span>

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

<span data-ttu-id="63d20-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-135">**Swift**:</span></span>

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

## <span data-ttu-id="63d20-136"><a name="filtering"></a>Procedura: Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="63d20-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="63d20-137">Per filtrare i risultati sono disponibili numerose opzioni.</span><span class="sxs-lookup"><span data-stu-id="63d20-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="63d20-138">Per filtrare tramite un predicato, usare `NSPredicate` e `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="63d20-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="63d20-139">I filtri seguenti hanno restituito i dati per trovare solo gli elementi Todo incompleti.</span><span class="sxs-lookup"><span data-stu-id="63d20-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="63d20-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
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

<span data-ttu-id="63d20-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
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

## <span data-ttu-id="63d20-142"><a name="query-object"></a>Procedura: Usare MSQuery</span><span class="sxs-lookup"><span data-stu-id="63d20-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="63d20-143">Per eseguire una query complessa che includa l'ordinamento e il paging, creare un oggetto `MSQuery` , direttamente o tramite un predicato:</span><span class="sxs-lookup"><span data-stu-id="63d20-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="63d20-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="63d20-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="63d20-146">`MSQuery` consente di controllare diversi comportamenti di query.</span><span class="sxs-lookup"><span data-stu-id="63d20-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="63d20-147">Specificare l'ordine dei risultati</span><span class="sxs-lookup"><span data-stu-id="63d20-147">Specify order of results</span></span>
* <span data-ttu-id="63d20-148">Limitare i campi da restituire</span><span class="sxs-lookup"><span data-stu-id="63d20-148">Limit which fields to return</span></span>
* <span data-ttu-id="63d20-149">Limitare il numero di record da restituire</span><span class="sxs-lookup"><span data-stu-id="63d20-149">Limit how many records to return</span></span>
* <span data-ttu-id="63d20-150">Specificare il conteggio totale nella risposta</span><span class="sxs-lookup"><span data-stu-id="63d20-150">Specify total count in response</span></span>
* <span data-ttu-id="63d20-151">Specificare i parametri della stringa di query personalizzata nella richiesta</span><span class="sxs-lookup"><span data-stu-id="63d20-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="63d20-152">Applicare funzioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="63d20-152">Apply additional functions</span></span>

<span data-ttu-id="63d20-153">Eseguire una query `MSQuery` chiamando `readWithCompletion` sull'oggetto.</span><span class="sxs-lookup"><span data-stu-id="63d20-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="63d20-154"><a name="sorting"></a>Procedura: Ordinare i dati con MSQuery</span><span class="sxs-lookup"><span data-stu-id="63d20-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="63d20-155">Per ordinare i risultati, verrà ora esaminato un esempio.</span><span class="sxs-lookup"><span data-stu-id="63d20-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="63d20-156">Per ordinare il campo "text" in ordine crescente, quindi "complete" in ordine decrescente, richiamare `MSQuery` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="63d20-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="63d20-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-157">**Objective-C**:</span></span>

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

<span data-ttu-id="63d20-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-158">**Swift**:</span></span>

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


## <span data-ttu-id="63d20-159"><a name="selecting"></a><a name="parameters"></a>Procedura: Limitare i campi ed espandere i parametri di query di tipo stringa con MSQuery</span><span class="sxs-lookup"><span data-stu-id="63d20-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="63d20-160">Per limitare i campi da restituire in una query, specificare i nomi dei campi nella proprietà **selectFields** .</span><span class="sxs-lookup"><span data-stu-id="63d20-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="63d20-161">Questo esempio restituisce solo i campi text e completed:</span><span class="sxs-lookup"><span data-stu-id="63d20-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="63d20-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="63d20-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="63d20-164">Per includere parametri di query di tipo stringa aggiuntivi nella richiesta server, poiché ad esempio sono usati da uno script sul lato server personalizzato, è possibile popolare `query.parameters` come segue:</span><span class="sxs-lookup"><span data-stu-id="63d20-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="63d20-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="63d20-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="63d20-167"><a name="paging"></a>Procedura: Configurare la dimensione di pagina</span><span class="sxs-lookup"><span data-stu-id="63d20-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="63d20-168">Con App per dispositivi mobili di Azure la dimensione di pagina controlla il numero di record che vengono estratti contemporaneamente dalle tabelle di back-end.</span><span class="sxs-lookup"><span data-stu-id="63d20-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="63d20-169">Una chiamata per eseguire il `pull` dei dati eseguirà il batch sui dati, in base alla dimensione di pagina, fino a quando non ci sono più record da estrarre.</span><span class="sxs-lookup"><span data-stu-id="63d20-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="63d20-170">È possibile configurare la dimensione di pagina mediante **MSPullSettings** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="63d20-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="63d20-171">La dimensione di pagina predefinita è 50 e l'esempio seguente la cambia in 3.</span><span class="sxs-lookup"><span data-stu-id="63d20-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="63d20-172">È possibile configurare una dimensione di pagina diversa per finalità di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="63d20-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="63d20-173">Se si dispone di un numero elevato di record di dati di piccole dimensioni, una dimensione di pagina elevata riduce il numero di round trip al server.</span><span class="sxs-lookup"><span data-stu-id="63d20-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="63d20-174">Questa impostazione controlla la dimensione di pagina solo sul lato client.</span><span class="sxs-lookup"><span data-stu-id="63d20-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="63d20-175">Se il client richiede una pagina più grande di quella supportata dal back-end di App per dispositivi mobili, la dimensione di pagina è limitata al massimo valore che il back-end può supportare.</span><span class="sxs-lookup"><span data-stu-id="63d20-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="63d20-176">Questa impostazione è inoltre il *numero* dei record dei dati, e non la *dimensione in byte*.</span><span class="sxs-lookup"><span data-stu-id="63d20-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="63d20-177">Se si aumenta la dimensione di pagina del client, è necessario aumentare anche la dimensione di pagina sul server.</span><span class="sxs-lookup"><span data-stu-id="63d20-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="63d20-178">Per la procedura da eseguire, vedere ["Procedura: Modificare le dimensioni di pagina delle tabelle"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="63d20-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="63d20-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="63d20-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="63d20-181"><a name="inserting"></a>Procedura: Inserire dati</span><span class="sxs-lookup"><span data-stu-id="63d20-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="63d20-182">Per inserire una nuova riga di tabella, creare un elemento `NSDictionary` e richiamare `table insert`.</span><span class="sxs-lookup"><span data-stu-id="63d20-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="63d20-183">Se [Schema dinamico] è abilitato, il back-end per dispositivi mobili del Servizio app di Azure genera automaticamente nuove colonne in base a `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="63d20-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="63d20-184">Se non viene specificato il valore `id` , il back-end genera automaticamente un nuovo ID univoco.</span><span class="sxs-lookup"><span data-stu-id="63d20-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="63d20-185">Specificare il proprio `id` per usare indirizzi e-mail, nomi utente o valori personalizzati come ID.</span><span class="sxs-lookup"><span data-stu-id="63d20-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="63d20-186">La specifica del proprio ID può semplificare l'esecuzione di join e la logica dei database aziendali.</span><span class="sxs-lookup"><span data-stu-id="63d20-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="63d20-187">`result` contiene il nuovo elemento inserito.</span><span class="sxs-lookup"><span data-stu-id="63d20-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="63d20-188">A seconda della logica del server, può includere dati aggiuntivi o modificati rispetto a quelli passati al server.</span><span class="sxs-lookup"><span data-stu-id="63d20-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="63d20-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-189">**Objective-C**:</span></span>

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

<span data-ttu-id="63d20-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-190">**Swift**:</span></span>

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

## <span data-ttu-id="63d20-191"><a name="modifying"></a>Procedura: Modificare dati</span><span class="sxs-lookup"><span data-stu-id="63d20-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="63d20-192">Per aggiornare una riga esistente, modificare un elemento e chiamare `update`:</span><span class="sxs-lookup"><span data-stu-id="63d20-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="63d20-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-193">**Objective-C**:</span></span>

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

<span data-ttu-id="63d20-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-194">**Swift**:</span></span>

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

<span data-ttu-id="63d20-195">In alternativa, fornire l'ID di riga e il campo aggiornato:</span><span class="sxs-lookup"><span data-stu-id="63d20-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="63d20-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="63d20-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="63d20-198">Per le operazioni di aggiornamento è necessario che sia impostato almeno l'attributo `id` .</span><span class="sxs-lookup"><span data-stu-id="63d20-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="63d20-199"><a name="deleting"></a>Procedura: Eliminare dati</span><span class="sxs-lookup"><span data-stu-id="63d20-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="63d20-200">Per eliminare un elemento, richiamare `delete` con l'elemento:</span><span class="sxs-lookup"><span data-stu-id="63d20-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="63d20-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="63d20-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="63d20-203">In alternativa, eliminarlo specificando un ID di riga:</span><span class="sxs-lookup"><span data-stu-id="63d20-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="63d20-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="63d20-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="63d20-206">Per le operazioni di eliminazione, è necessario che sia impostato almeno l'attributo `id` .</span><span class="sxs-lookup"><span data-stu-id="63d20-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="63d20-207"><a name="customapi"></a>Procedura: Chiamare un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="63d20-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="63d20-208">Con un'API personalizzata è possibile esporre qualsiasi funzionalità di back-end.</span><span class="sxs-lookup"><span data-stu-id="63d20-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="63d20-209">Non occorre eseguire il mapping a un'operazione su tabella.</span><span class="sxs-lookup"><span data-stu-id="63d20-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="63d20-210">In questo modo, non solo si ottiene maggiore controllo sulla messaggistica, ma è anche possibile leggere o impostare le intestazioni e modificare il formato del corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="63d20-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="63d20-211">Per informazioni su come creare un'API personalizzata nel back-end, leggere [API personalizzate](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="63d20-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="63d20-212">Per chiamare un'API personalizzata, chiamare `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="63d20-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="63d20-213">Il contenuto della richiesta e della risposta è in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="63d20-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="63d20-214">Per utilizzare altri tipi di supporto, [usare l'altro overload di `invokeAPI`][5].</span><span class="sxs-lookup"><span data-stu-id="63d20-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="63d20-215">Per eseguire una richiesta `GET` invece di una richiesta `POST`, impostare il parametro `HTTPMethod` su `"GET"` e il parametro `body` su `nil` (dal momento che le richieste GET non hanno corpi dei messaggi). Se l'API personalizzata supporta altri verbi HTTP, modificare `HTTPMethod` in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="63d20-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="63d20-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-216">**Objective-C**:</span></span>

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

<span data-ttu-id="63d20-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-217">**Swift**:</span></span>

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

## <span data-ttu-id="63d20-218"><a name="templates"></a>Procedura: registrare modelli push per inviare notifiche multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="63d20-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="63d20-219">Per registrare i modelli, passare modelli con il metodo **client.push registerDeviceToken** nell'app client.</span><span class="sxs-lookup"><span data-stu-id="63d20-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="63d20-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="63d20-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="63d20-222">I modelli sono di tipo NSDictionary e possono contenere più modelli nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="63d20-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="63d20-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="63d20-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="63d20-225">Tutti i tag vengono rimossi dalla richiesta per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="63d20-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="63d20-226">Per aggiungere tag alle istallazione o ai modelli all'interno delle istallazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure][4].</span><span class="sxs-lookup"><span data-stu-id="63d20-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="63d20-227">Per inviare notifiche tramite questi modelli registrati, usare le [API di Hub di notifica][3].</span><span class="sxs-lookup"><span data-stu-id="63d20-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="63d20-228"><a name="errors"></a>Procedura: Gestire gli errori</span><span class="sxs-lookup"><span data-stu-id="63d20-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="63d20-229">Quando viene eseguita una chiamata a un back-end per dispositivi mobili del Servizio app di Azure, il blocco di completamento contiene un parametro `NSError` .</span><span class="sxs-lookup"><span data-stu-id="63d20-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="63d20-230">Quando si verifica un errore, il parametro sarà diverso da Nil.</span><span class="sxs-lookup"><span data-stu-id="63d20-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="63d20-231">In questo caso, è necessario verificare il parametro nel codice e gestire l'errore nel modo appropriato, come dimostrato nei frammenti di codice precedenti.</span><span class="sxs-lookup"><span data-stu-id="63d20-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="63d20-232">Il file [`<WindowsAzureMobileServices/MSError.h>`][6] definisce le costanti `MSErrorResponseKey`, `MSErrorRequestKey` e `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="63d20-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="63d20-233">Per ottenere più dati relativi all'errore:</span><span class="sxs-lookup"><span data-stu-id="63d20-233">To get more data related to the error:</span></span>

<span data-ttu-id="63d20-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="63d20-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="63d20-236">Il file definisce anche le costanti per ogni codice di errore:</span><span class="sxs-lookup"><span data-stu-id="63d20-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="63d20-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="63d20-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="63d20-239"><a name="adal"></a>Procedura: Autenticare gli utenti con Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="63d20-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="63d20-240">È possibile usare Active Directory Authentication Library (ADAL) per far accedere gli utenti all'applicazione tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="63d20-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="63d20-241">È preferibile usare l'autenticazione del flusso client tramite un SDK del provider di identità anziché il metodo `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="63d20-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="63d20-242">L'autenticazione del flusso client garantisce un'esperienza utente più naturale e consente una maggiore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="63d20-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="63d20-243">Configurare il back-end dell'app per dispositivi mobili per l'accesso ad Azure Active Directory seguendo l'esercitazione [Come configurare un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory][7].</span><span class="sxs-lookup"><span data-stu-id="63d20-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="63d20-244">Assicurarsi di completare il passaggio facoltativo di registrazione di un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="63d20-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="63d20-245">Per iOS è consigliabile che l'URI di reindirizzamento sia nel formato `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="63d20-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="63d20-246">Per altre informazioni, vedere [Guida introduttiva di ADAL iOS][8].</span><span class="sxs-lookup"><span data-stu-id="63d20-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="63d20-247">Installare ADAL usando Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="63d20-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="63d20-248">Modificare il podfile includendo la definizione seguente e sostituendo **YOUR-PROJECT** con il nome del progetto Xcode:</span><span class="sxs-lookup"><span data-stu-id="63d20-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="63d20-249">e il Pod:</span><span class="sxs-lookup"><span data-stu-id="63d20-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="63d20-250">Nel terminale eseguire `pod install` dalla directory contenente il progetto e quindi aprire l'area di lavoro di Xcode generata (non il progetto).</span><span class="sxs-lookup"><span data-stu-id="63d20-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="63d20-251">Aggiungere il codice seguente all'applicazione, in base al linguaggio usato.</span><span class="sxs-lookup"><span data-stu-id="63d20-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="63d20-252">In ogni esempio eseguire queste sostituzioni:</span><span class="sxs-lookup"><span data-stu-id="63d20-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="63d20-253">Sostituire **INSERT-AUTHORITY-HERE** con il nome del tenant in cui è stato eseguito il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="63d20-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="63d20-254">Il formato deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="63d20-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="63d20-255">È possibile copiare questo valore dalla scheda Dominio di Azure Active Directory nel [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="63d20-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="63d20-256">Sostituire **INSERT-RESOURCE-ID-HERE** con l'ID client per il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="63d20-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="63d20-257">L'ID client è disponibile nella scheda **Avanzate** in **Impostazioni di Azure Active Directory** nel portale.</span><span class="sxs-lookup"><span data-stu-id="63d20-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="63d20-258">Sostituire **INSERT-CLIENT-ID-HERE** con l'ID client copiato dall'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="63d20-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="63d20-259">Sostituire **INSERT-REDIRECT-URI-HERE** con l'endpoint */.auth/login/done* del sito, usando lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="63d20-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="63d20-260">Questo valore deve essere simile a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="63d20-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="63d20-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-261">**Objective-C**:</span></span>

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


<span data-ttu-id="63d20-262">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
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

## <span data-ttu-id="63d20-263"><a name="facebook-sdk"></a>Procedura: Autenticare gli utenti con Facebook SDK for iOS</span><span class="sxs-lookup"><span data-stu-id="63d20-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="63d20-264">È possibile usare Facebook SDK for iOS per consentire l'accesso degli utenti all'applicazione tramite Facebook.</span><span class="sxs-lookup"><span data-stu-id="63d20-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="63d20-265">È preferibile usare l'autenticazione del flusso client all'uso del metodo `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="63d20-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="63d20-266">L'autenticazione del flusso client garantisce un'esperienza utente più naturale e consente una maggiore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="63d20-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="63d20-267">Configurare il back-end dell'app per dispositivi mobili per l'accesso con l'account Facebook seguendo l'esercitazione [Come configurare un'applicazione del servizio App per usare l'account di accesso di Facebook][9].</span><span class="sxs-lookup"><span data-stu-id="63d20-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="63d20-268">Installare Facebook SDK for iOS secondo le indicazioni della documentazione [Facebook SDK for iOS - Getting Started][10] (Facebook SDK for iOS: guida introduttiva).</span><span class="sxs-lookup"><span data-stu-id="63d20-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="63d20-269">Anziché creare un'app, è possibile aggiungere la piattaforma iOS alla procedura di registrazione esistente.</span><span class="sxs-lookup"><span data-stu-id="63d20-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="63d20-270">La documentazione di Facebook include codice Objective-C nel delegato dell'app.</span><span class="sxs-lookup"><span data-stu-id="63d20-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="63d20-271">Se si usa **Swift**, è possibile utilizzare le seguenti traduzioni per AppDelegate.swift:</span><span class="sxs-lookup"><span data-stu-id="63d20-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
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
4. <span data-ttu-id="63d20-272">Oltre ad aggiungere `FBSDKCoreKit.framework` al progetto, aggiungere nello stesso modo anche un riferimento a `FBSDKLoginKit.framework`.</span><span class="sxs-lookup"><span data-stu-id="63d20-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="63d20-273">Aggiungere il codice seguente all'applicazione, in base al linguaggio usato.</span><span class="sxs-lookup"><span data-stu-id="63d20-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="63d20-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-274">**Objective-C**:</span></span>

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

<span data-ttu-id="63d20-275">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
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

## <span data-ttu-id="63d20-276"><a name="twitter-fabric"></a>Procedura: Autenticare gli utenti con Twitter Fabric for iOS</span><span class="sxs-lookup"><span data-stu-id="63d20-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="63d20-277">È possibile usare Fabric for iOS per consentire l'accesso degli utenti all'applicazione tramite Twitter.</span><span class="sxs-lookup"><span data-stu-id="63d20-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="63d20-278">L'autenticazione del flusso client è preferibile all'uso del metodo `loginWithProvider:completion:` , perché garantisce un'esperienza utente più naturale e consente una maggiore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="63d20-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="63d20-279">Configurare il back-end dell'app per dispositivi mobili per l'accesso con l'account Twitter seguendo l'esercitazione [Come configurare un'applicazione del servizio app per usare l'account di accesso di Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="63d20-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="63d20-280">Aggiungere Fabric al progetto seguendo le indicazioni della documentazione [Fabric for iOS - Getting Started] (Fabric for iOS: guida introduttiva) e configurando TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="63d20-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="63d20-281">Per impostazione predefinita, Fabric crea automaticamente un'applicazione Twitter.</span><span class="sxs-lookup"><span data-stu-id="63d20-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="63d20-282">È possibile evitare di creare un'applicazione registrando la chiave utente e il segreto utente creati in precedenza tramite i frammenti di codice seguenti.</span><span class="sxs-lookup"><span data-stu-id="63d20-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="63d20-283">In alternativa, è possibile sostituire i valori relativi alla chiave utente e al segreto utente forniti al servizio app con i valori visualizzati nel [dashboard di Fabric].</span><span class="sxs-lookup"><span data-stu-id="63d20-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="63d20-284">Se si sceglie questa opzione, assicurarsi di impostare l'URL di callback su un valore segnaposto, ad esempio `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="63d20-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="63d20-285">Se si sceglie di usare i segreti creati in precedenza, aggiungere il codice seguente al delegato dell'app:</span><span class="sxs-lookup"><span data-stu-id="63d20-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="63d20-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-286">**Objective-C**:</span></span>

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

    <span data-ttu-id="63d20-287">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="63d20-288">Aggiungere il codice seguente all'applicazione, in base al linguaggio usato.</span><span class="sxs-lookup"><span data-stu-id="63d20-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="63d20-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-289">**Objective-C**:</span></span>

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

<span data-ttu-id="63d20-290">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-290">**Swift**:</span></span>

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

## <span data-ttu-id="63d20-291"><a name="google-sdk"></a>Procedura: Autenticare gli utenti con Google Sign-In SDK for iOS</span><span class="sxs-lookup"><span data-stu-id="63d20-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="63d20-292">È possibile usare Google Sign-In SDK for iOS per consentire l'accesso degli utenti all'applicazione tramite un account Google.</span><span class="sxs-lookup"><span data-stu-id="63d20-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="63d20-293">Google ha annunciato recentemente modifiche ai criteri di sicurezza di OAuth.</span><span class="sxs-lookup"><span data-stu-id="63d20-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="63d20-294">Queste modifiche apportate ai criteri richiederanno l'uso di Google SDK in futuro.</span><span class="sxs-lookup"><span data-stu-id="63d20-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="63d20-295">Configurare il back-end dell'app per dispositivi mobili per l'accesso con l'account Google seguendo l'esercitazione [Come configurare un'applicazione del servizio app per usare l'account di accesso di Google](app-service-mobile-how-to-configure-google-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="63d20-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="63d20-296">Installare Google SDK for iOS seguendo le istruzioni nel documento [Start integrating Google Sign-In into your iOS app](https://developers.google.com/identity/sign-in/ios/start-integrating) (Iniziare a integrare l'accesso di Google nell'app iOS).</span><span class="sxs-lookup"><span data-stu-id="63d20-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="63d20-297">È possibile ignorare la sezione relativa all'autenticazione con un server di back-end.</span><span class="sxs-lookup"><span data-stu-id="63d20-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="63d20-298">Aggiungere quanto segue al metodo `signIn:didSignInForUser:withError:` di delegato, a seconda del linguaggio usato.</span><span class="sxs-lookup"><span data-stu-id="63d20-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="63d20-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="63d20-300">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="63d20-301">Aggiungere anche il codice seguente a `application:didFinishLaunchingWithOptions:` nel delegato dell'app, sostituendo "SERVER_CLIENT_ID" con lo stesso ID usato per configurare il servizio app nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="63d20-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="63d20-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="63d20-303">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="63d20-304">Aggiungere il codice seguente all'applicazione in una classe UIViewController che implementi il protocollo `GIDSignInUIDelegate` , in base al linguaggio usato.</span><span class="sxs-lookup"><span data-stu-id="63d20-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="63d20-305">L'utente viene disconnesso prima di accedere nuovamente e anche se non è necessario immettere le credenziali una seconda volta, verrà visualizzata una finestra di dialogo di consenso.</span><span class="sxs-lookup"><span data-stu-id="63d20-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="63d20-306">Chiamare questo metodo solo quando il token della sessione è scaduto.</span><span class="sxs-lookup"><span data-stu-id="63d20-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="63d20-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="63d20-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="63d20-308">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="63d20-308">**Swift**:</span></span>

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
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="63d20-309">[Azure Mobile App Quick Start]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="63d20-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="63d20-310">[Schema dinamico]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="63d20-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="63d20-311">[dashboard di Fabric]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="63d20-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="63d20-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="63d20-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
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
