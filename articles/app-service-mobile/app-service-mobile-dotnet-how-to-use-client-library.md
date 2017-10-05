---
title: Uso della libreria client gestita di app per dispositivi mobili del servizio app (Windows) | Documentazione Microsoft
description: Informazioni su come usare un client .NET per App per dispositivi mobili del servizio app di Azure con le app Windows e Xamarin.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="91139-103">Come usare il client gestito per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="91139-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="91139-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="91139-104">Overview</span></span>
<span data-ttu-id="91139-105">Questa guida illustra come eseguire scenari comuni usando la libreria client gestita per App per dispositivi mobili del servizio app di Azure in app Windows e Xamarin.</span><span class="sxs-lookup"><span data-stu-id="91139-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="91139-106">Se non si conosce App per dispositivi mobili, è consigliabile completare prima l'esercitazione sull'[introduzione ad App per dispositivi mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="91139-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="91139-107">In questa Guida, l'attenzione è posta sull'SDK gestito sul lato client.</span><span class="sxs-lookup"><span data-stu-id="91139-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="91139-108">Per altre informazioni sugli SDK lato server per le app per dispositivi mobili, vedere la documentazione per [.NET Server SDK][2] o [Node.js Server SDK][3].</span><span class="sxs-lookup"><span data-stu-id="91139-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="91139-109">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="91139-109">Reference documentation</span></span>
<span data-ttu-id="91139-110">La documentazione di riferimento per l'SDK per client è disponibile qui: [riferimento al client .NET di App per dispositivi mobili di Azure][4].</span><span class="sxs-lookup"><span data-stu-id="91139-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="91139-111">È anche possibile trovare alcuni esempi per client nel [repository GitHub degli esempi di Azure][5].</span><span class="sxs-lookup"><span data-stu-id="91139-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="91139-112">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="91139-112">Supported Platforms</span></span>
<span data-ttu-id="91139-113">La piattaforma .NET supporta le seguenti piattaforme:</span><span class="sxs-lookup"><span data-stu-id="91139-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="91139-114">Versioni Android di Xamarin per API da 19 a 24 (KitKat tramite Nougat)</span><span class="sxs-lookup"><span data-stu-id="91139-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="91139-115">Versioni iOS di Xamarin per le versioni iOS 8.0 e successive</span><span class="sxs-lookup"><span data-stu-id="91139-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="91139-116">Piattaforma UWP (Universal Windows Platform)</span><span class="sxs-lookup"><span data-stu-id="91139-116">Universal Windows Platform</span></span>
* <span data-ttu-id="91139-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="91139-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="91139-118">Windows Phone 8.0, ad eccezione delle applicazioni Silverlight</span><span class="sxs-lookup"><span data-stu-id="91139-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="91139-119">L'autenticazione "flusso server" usa una visualizzazione Web per l'interfaccia utente presentata.</span><span class="sxs-lookup"><span data-stu-id="91139-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="91139-120">Se il dispositivo non è in grado di presentare una interfaccia utente con visualizzazione Web, sono necessari altri metodi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="91139-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="91139-121">Questo SDK non è quindi adatto per i dispositivi di tipo controllo o con restrizioni simili.</span><span class="sxs-lookup"><span data-stu-id="91139-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="91139-122"><a name="setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="91139-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="91139-123">Si presuppone che si sia già creato e pubblicato il progetto di back-end di App per dispositivi mobili, che include almeno una tabella.</span><span class="sxs-lookup"><span data-stu-id="91139-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="91139-124">Nel codice usato in questo argomento la tabella è denominata `TodoItem` e si presenta con le colonne seguenti: `Id`, `Text` e `Complete`.</span><span class="sxs-lookup"><span data-stu-id="91139-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="91139-125">Si tratta della stessa tabella creata durante l'[esercitazione introduttiva ad App per dispositivi mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="91139-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="91139-126">Il tipo sul lato client tipizzato in C# è la classe seguente:</span><span class="sxs-lookup"><span data-stu-id="91139-126">The corresponding typed client-side type in C# is the following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="91139-127">Il valore di [JsonPropertyAttribute][6] viene usato per definire il mapping di *PropertyName* tra il campo del client e il campo della tabella.</span><span class="sxs-lookup"><span data-stu-id="91139-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="91139-128">Per informazioni su come creare le tabelle nel back-end di App per dispositivi mobili, vedere l'argomento [.NET Server SDK][7] o [Node.js Server SDK][8].</span><span class="sxs-lookup"><span data-stu-id="91139-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="91139-129">Se il back-end delle app per dispositivi mobili è stato creato nel portale di Azure mediante l'esercitazione introduttiva, è anche possibile usare l'impostazione **Tabelle semplici** del [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="91139-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="91139-130">Procedura: Installare il pacchetto SDK client gestito</span><span class="sxs-lookup"><span data-stu-id="91139-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="91139-131">Per installare il pacchetto SDK gestito da client per App per dispositivi mobili da [NuGet][9] attenersi a uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="91139-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="91139-132">**Visual Studio** Fare clic sul progetto con il pulsante destro del mouse, scegliere **Gestisci pacchetti NuGet**, cercare il pacchetto `Microsoft.Azure.Mobile.Client` e fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="91139-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="91139-133">**Xamarin Studio** Fare clic sul progetto con il pulsante destro del mouse, scegliere **Aggiungi**>**Aggiungi pacchetti NuGet**, cercare il pacchetto `Microsoft.Azure.Mobile.Client ` e fare clic su **Aggiungi pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="91139-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="91139-134">Nel file dell'attività principale aggiungere l'istruzione **using** seguente:</span><span class="sxs-lookup"><span data-stu-id="91139-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="91139-135"><a name="symbolsource"></a>Procedura: Usare i simboli di debug in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91139-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="91139-136">I simboli per lo spazio dei nomi di Microsoft.Azure.Mobile sono disponibili in [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="91139-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="91139-137">Per l'integrazione di SymbolSource in Visual Studio, vedere le [istruzioni di SymbolSource][11].</span><span class="sxs-lookup"><span data-stu-id="91139-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="91139-138"><a name="create-client"></a>Creare il client di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="91139-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="91139-139">Il codice seguente crea l'oggetto [MobileServiceClient][12] che viene usato per accedere al back-end di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="91139-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="91139-140">Nel codice precedente sostituire `MOBILE_APP_URL` con l'URL del back-end dell'App per dispositivi mobili, che si trova nel pannello relativo al back-end dell'App per dispositivi mobili nel [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="91139-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="91139-141">L'oggetto MobileServiceClient deve essere un singleton.</span><span class="sxs-lookup"><span data-stu-id="91139-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="91139-142">Usare le tabelle</span><span class="sxs-lookup"><span data-stu-id="91139-142">Work with Tables</span></span>
<span data-ttu-id="91139-143">Nella sezione seguente viene illustrato come cercare e recuperare i record e modificare i dati all'interno della tabella.</span><span class="sxs-lookup"><span data-stu-id="91139-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="91139-144">Vengono trattati gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="91139-144">The following topics are covered:</span></span>

* [<span data-ttu-id="91139-145">Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="91139-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="91139-146">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="91139-146">Query data</span></span>](#querying)
* [<span data-ttu-id="91139-147">Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="91139-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="91139-148">Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="91139-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="91139-149">Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="91139-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="91139-150">Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="91139-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="91139-151">Cercare un record per Id</span><span class="sxs-lookup"><span data-stu-id="91139-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="91139-152">Gestione delle query non tipizzate</span><span class="sxs-lookup"><span data-stu-id="91139-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="91139-153">Inserimento dei dati</span><span class="sxs-lookup"><span data-stu-id="91139-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="91139-154">Aggiornamento dei dati</span><span class="sxs-lookup"><span data-stu-id="91139-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="91139-155">Eliminazione dei dati</span><span class="sxs-lookup"><span data-stu-id="91139-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="91139-156">Risoluzione dei conflitti e concorrenza ottimistica</span><span class="sxs-lookup"><span data-stu-id="91139-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="91139-157">Associazione a un'interfaccia utente di Windows</span><span class="sxs-lookup"><span data-stu-id="91139-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="91139-158">Modifica delle dimensioni di pagina</span><span class="sxs-lookup"><span data-stu-id="91139-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="91139-159"><a name="instantiating"></a>Procedura: Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="91139-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="91139-160">Tutti i codici che accedono o modificano i dati nella tabella del back-end chiamano funzioni sull'oggetto `MobileServiceTable` .</span><span class="sxs-lookup"><span data-stu-id="91139-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="91139-161">Ottenere un riferimento alla tabella chiamando il metodo [GetTable] , nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="91139-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="91139-162">L'oggetto restituito usa il modello di serializzazione tipizzato.</span><span class="sxs-lookup"><span data-stu-id="91139-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="91139-163">Viene supportato anche un modello di serializzazione non tipizzato.</span><span class="sxs-lookup"><span data-stu-id="91139-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="91139-164">L'esempio seguente [crea un riferimento a una tabella non tipizzata]:</span><span class="sxs-lookup"><span data-stu-id="91139-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="91139-165">Nelle query non tipizzate, è necessario specificare la stringa di query OData sottostante.</span><span class="sxs-lookup"><span data-stu-id="91139-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="91139-166"><a name="querying"></a>Procedura: Eseguire query sui dati dall'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="91139-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="91139-167">Questa sezione descrive come eseguire query nel back-end di App per dispositivi mobili, incluse le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="91139-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="91139-168">Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="91139-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="91139-169">Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="91139-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="91139-170">Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="91139-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="91139-171">Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="91139-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="91139-172">Cercare dati in base all'ID</span><span class="sxs-lookup"><span data-stu-id="91139-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="91139-173">Viene usata una dimensione di pagina basata sul server, per evitare la restituzione di tutte le righe.</span><span class="sxs-lookup"><span data-stu-id="91139-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="91139-174">Grazie al paging le richieste predefinite di set di dati di grandi dimensioni non hanno conseguenze negative sul servizio.</span><span class="sxs-lookup"><span data-stu-id="91139-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="91139-175">Per restituire più di 50 righe, usare i metodi `Skip` e `Take`, come descritto in [Restituire i dati in pagine](#paging).</span><span class="sxs-lookup"><span data-stu-id="91139-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="91139-176"><a name="filtering"></a>Procedura: Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="91139-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="91139-177">Il codice seguente illustra come filtrare i dati includendo una clausola `Where` in una query.</span><span class="sxs-lookup"><span data-stu-id="91139-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="91139-178">Restituisce tutti gli elementi da `todoTable` per i quali la proprietà `Complete` è uguale a `false`.</span><span class="sxs-lookup"><span data-stu-id="91139-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="91139-179">La funzione [Where] applica un predicato di filtro di riga alla query sulla tabella.</span><span class="sxs-lookup"><span data-stu-id="91139-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="91139-180">È possibile visualizzare l'URI della richiesta inviata al back-end usando un software di ispezione dei messaggi come gli strumenti di sviluppo per browser o [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="91139-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="91139-181">Nell'URI della richiesta notare che la stringa di query è modificata:</span><span class="sxs-lookup"><span data-stu-id="91139-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="91139-182">Questa richiesta OData viene convertita in una query SQL da un SDK del server:</span><span class="sxs-lookup"><span data-stu-id="91139-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="91139-183">La funzione passata al metodo `Where` può avere un numero di condizioni arbitrario.</span><span class="sxs-lookup"><span data-stu-id="91139-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="91139-184">Questo esempio viene convertito in una query SQL dall'SDK del server:</span><span class="sxs-lookup"><span data-stu-id="91139-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="91139-185">Questa query può anche essere suddivisa in più clausole:</span><span class="sxs-lookup"><span data-stu-id="91139-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="91139-186">I due metodi si equivalgono e possono essere utilizzati in modo intercambiabile.</span><span class="sxs-lookup"><span data-stu-id="91139-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="91139-187">La prima opzione, che prevede la concatenazione di più predicati in una query, è più compatta ed è consigliata.</span><span class="sxs-lookup"><span data-stu-id="91139-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="91139-188">La clausola `Where` supporta operazioni che vengono convertite nel subset OData.</span><span class="sxs-lookup"><span data-stu-id="91139-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="91139-189">Alcune operazioni sono:</span><span class="sxs-lookup"><span data-stu-id="91139-189">Operations include:</span></span>

* <span data-ttu-id="91139-190">Operatori relazionali (==, !=, <, <=, >, >=)</span><span class="sxs-lookup"><span data-stu-id="91139-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="91139-191">Operatori aritmetici (+, -, /, *, %)</span><span class="sxs-lookup"><span data-stu-id="91139-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="91139-192">Approssimazione dei numeri (Math.Floor, Math.Ceiling)</span><span class="sxs-lookup"><span data-stu-id="91139-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="91139-193">Funzioni di stringa (Length, Substring, Replace, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="91139-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="91139-194">Proprietà relative alla data (Year, Month, Day, Hour, Minute, Second)</span><span class="sxs-lookup"><span data-stu-id="91139-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="91139-195">Proprietà di accesso di un oggetto</span><span class="sxs-lookup"><span data-stu-id="91139-195">Access properties of an object, and</span></span>
* <span data-ttu-id="91139-196">Espressioni che combinano queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="91139-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="91139-197">Per determinare gli elementi supportati dall'SDK del server, vedere la [documentazione relativa a OData v3].</span><span class="sxs-lookup"><span data-stu-id="91139-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="91139-198"><a name="sorting"></a>Procedura: Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="91139-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="91139-199">Il codice seguente illustra come ordinare i dati includendo una funzione [OrderBy] o [OrderByDescending] nella query.</span><span class="sxs-lookup"><span data-stu-id="91139-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="91139-200">L'operazione restituisce elementi della tabella `todoTable` in ordine crescente in base al campo `Text`.</span><span class="sxs-lookup"><span data-stu-id="91139-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="91139-201"><a name="paging"></a>Procedura: Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="91139-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="91139-202">Per impostazione predefinita, il server restituisce solo le prime 50 righe.</span><span class="sxs-lookup"><span data-stu-id="91139-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="91139-203">È possibile aumentare il numero di righe restituite mediante una chiamata al metodo [Take] .</span><span class="sxs-lookup"><span data-stu-id="91139-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="91139-204">Usare `Take` insieme al metodo [Skip] per richiedere una "pagina" specifica dell'intero set di dati restituito dalla query.</span><span class="sxs-lookup"><span data-stu-id="91139-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="91139-205">La query seguente, se eseguita, restituisce le prime tre voci della tabella.</span><span class="sxs-lookup"><span data-stu-id="91139-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="91139-206">La query modificata seguente ignora i primi tre risultati e restituisce i tre risultati successivi.</span><span class="sxs-lookup"><span data-stu-id="91139-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="91139-207">La query produce la seconda "pagina" di dati, la cui dimensione corrisponde a tre voci.</span><span class="sxs-lookup"><span data-stu-id="91139-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="91139-208">Il metodo [IncludeTotalCount] richiede il conteggio totale di *tutti* i record che sarebbero stati restituiti ignorando qualsiasi clausola di limite/paging specificata:</span><span class="sxs-lookup"><span data-stu-id="91139-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="91139-209">In un'app reale è possibile usare query simili all'esempio precedente con un controllo pager o un'interfaccia utente paragonabile per passare da una pagina all'altra.</span><span class="sxs-lookup"><span data-stu-id="91139-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="91139-210">Per ignorare il limite di 50 righe in un back-end di App per dispositivi mobili, è necessario anche applicare l'attributo [EnableQueryAttribute] al metodo pubblico GET e specificare il comportamento di paging.</span><span class="sxs-lookup"><span data-stu-id="91139-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="91139-211">Se applicato al metodo, l'attributo seguente imposta il numero massimo di righe restituite su 1000:</span><span class="sxs-lookup"><span data-stu-id="91139-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="91139-212"><a name="selecting"></a>Procedura: Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="91139-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="91139-213">È possibile specificare il set di proprietà da includere nei risultati aggiungendo alla query una clausola [Select] .</span><span class="sxs-lookup"><span data-stu-id="91139-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="91139-214">Ad esempio, nel codice seguente viene illustrato come selezionare un solo campo e come selezionare e formattare più campi:</span><span class="sxs-lookup"><span data-stu-id="91139-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="91139-215">Tutte le funzioni descritte in precedenza sono di tipo additivo ed è quindi possibile usare la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="91139-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="91139-216">Ogni chiamata concatenata incide ulteriormente sulla query.</span><span class="sxs-lookup"><span data-stu-id="91139-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="91139-217">Un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="91139-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="91139-218"><a name="lookingup"></a>Procedura: Cercare dati in base all'ID</span><span class="sxs-lookup"><span data-stu-id="91139-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="91139-219">Per cercare oggetti dal database caratterizzati da un particolare ID, è possibile utilizzare la funzione [LookupAsync] .</span><span class="sxs-lookup"><span data-stu-id="91139-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="91139-220"><a name="untypedqueries"></a>Procedura: eseguire query non tipizzate</span><span class="sxs-lookup"><span data-stu-id="91139-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="91139-221">Quando si esegue una query usando un oggetto di tabella non tipizzata, è necessario specificare esplicitamente la stringa di query OData eseguendo una chiamata a [ReadAsync], come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="91139-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="91139-222">Si ottengono valori JSON utilizzabili come contenitore delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="91139-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="91139-223">Per altre informazioni su JToken e Newtonsoft Json.NET, visitare il sito [Json.NET] .</span><span class="sxs-lookup"><span data-stu-id="91139-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="91139-224"><a name="inserting"></a>Procedura: Inserire dati in un back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="91139-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="91139-225">Tutti i tipi di client devono contenere un membro denominato **Id**, che per impostazione predefinita è una stringa.</span><span class="sxs-lookup"><span data-stu-id="91139-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="91139-226">Questo **Id** è necessario per eseguire le operazioni CRUD e per la sincronizzazione offline.</span><span class="sxs-lookup"><span data-stu-id="91139-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="91139-227">Il codice seguente illustra come usare il metodo [InsertAsync] per inserire nuove righe in una tabella.</span><span class="sxs-lookup"><span data-stu-id="91139-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="91139-228">Il parametro contiene i dati da inserire come oggetto .NET.</span><span class="sxs-lookup"><span data-stu-id="91139-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="91139-229">Se nell'elemento `todoItem` non è incluso un valore ID univoco personalizzato durante un inserimento, il server genera un GUID.</span><span class="sxs-lookup"><span data-stu-id="91139-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="91139-230">È possibile recuperare l'ID generato controllando l'oggetto al termine della chiamata.</span><span class="sxs-lookup"><span data-stu-id="91139-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="91139-231">Per inserire dati non tipizzati, è possibile usare Json.NET:</span><span class="sxs-lookup"><span data-stu-id="91139-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="91139-232">Di seguito è riportato un esempio con un indirizzo di posta elettronica come ID di stringa univoco:</span><span class="sxs-lookup"><span data-stu-id="91139-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="91139-233">Uso di valori ID</span><span class="sxs-lookup"><span data-stu-id="91139-233">Working with ID values</span></span>
<span data-ttu-id="91139-234">App per dispositivi mobili supporta valori di stringa univoci personalizzati per la colonna **id** della tabella.</span><span class="sxs-lookup"><span data-stu-id="91139-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="91139-235">Un valore di stringa consente alle applicazioni di usare valori personalizzati come indirizzi e-mail o nomi utente per l'ID.</span><span class="sxs-lookup"><span data-stu-id="91139-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="91139-236">Gli ID stringa offrono i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="91139-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="91139-237">Gli ID vengono generati senza creare un round trip al database.</span><span class="sxs-lookup"><span data-stu-id="91139-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="91139-238">L'unione di record da tabelle o database diversi risulta semplificata.</span><span class="sxs-lookup"><span data-stu-id="91139-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="91139-239">L'integrazione di valori di ID con la logica di un'applicazione è più efficace.</span><span class="sxs-lookup"><span data-stu-id="91139-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="91139-240">Quando un valore ID di stringa non è impostato su un record inserito, App per dispositivi mobili genera un valore univoco per l'ID.</span><span class="sxs-lookup"><span data-stu-id="91139-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="91139-241">È possibile usare il metodo [Guid.NewGuid] per generare valori ID personalizzati sul client o nel back-end.</span><span class="sxs-lookup"><span data-stu-id="91139-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="91139-242"><a name="modifying"></a>Procedura: Modificare dati in un back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="91139-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="91139-243">Il codice seguente illustra come usare il metodo [UpdateAsync] per aggiornare un record esistente con lo stesso ID con le nuove informazioni.</span><span class="sxs-lookup"><span data-stu-id="91139-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="91139-244">Il parametro contiene i dati da aggiornare come oggetto .NET.</span><span class="sxs-lookup"><span data-stu-id="91139-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="91139-245">Per eliminare dati non tipizzati, è possibile usare [Json.NET] come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="91139-246">Quando si esegue un aggiornamento è necessario specificare un campo `id` .</span><span class="sxs-lookup"><span data-stu-id="91139-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="91139-247">Il back-end usa il campo `id` per identificare la riga da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="91139-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="91139-248">È possibile ottenere il campo `id` dal risultato della chiamata `InsertAsync`.</span><span class="sxs-lookup"><span data-stu-id="91139-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="91139-249">Quando si tenta di aggiornare un elemento senza specificare il valore `ArgumentException`, viene generata un'eccezione `id`.</span><span class="sxs-lookup"><span data-stu-id="91139-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="91139-250"><a name="deleting"></a>Procedura: Eliminare dati in un back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="91139-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="91139-251">Il codice seguente illustra come usare il metodo [DeleteAsync] per eliminare un'istanza esistente.</span><span class="sxs-lookup"><span data-stu-id="91139-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="91139-252">L'istanza è identificata dal campo `id` impostato in `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="91139-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="91139-253">Per eliminare dati non tipizzati, è possibile utilizzare Json.NET come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="91139-254">Quando si esegue una richiesta di eliminazione, è necessario specificare un ID.</span><span class="sxs-lookup"><span data-stu-id="91139-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="91139-255">Altre proprietà non vengono passate al servizio o vengono ignorate nel servizio.</span><span class="sxs-lookup"><span data-stu-id="91139-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="91139-256">Il risultato di una chiamata `DeleteAsync` equivale in genere a `null`.</span><span class="sxs-lookup"><span data-stu-id="91139-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="91139-257">È possibile ottenere l'ID da passare dal risultato della chiamata `InsertAsync` .</span><span class="sxs-lookup"><span data-stu-id="91139-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="91139-258">Quando si tenta di eliminare un elemento senza specificare il campo `id`, viene generata un'eccezione `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="91139-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="91139-259"><a name="optimisticconcurrency"></a>Procedura: Usare la concorrenza ottimistica per la risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="91139-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="91139-260">È possibile che due o più client scrivano modifiche nello stesso elemento contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="91139-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="91139-261">Se non viene rilevato un conflitto, l'ultima scrittura sovrascrive tutti gli aggiornamenti precedenti.</span><span class="sxs-lookup"><span data-stu-id="91139-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="91139-262">**controllo della concorrenza ottimistica** presuppone che per ogni transazione sia possibile eseguire il commit, quindi non procede al blocco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="91139-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="91139-263">Prima di effettuare il commit di una transazione, il controllo della concorrenza ottimistica verifica che i dati non siano stati modificati da un'altra transazione.</span><span class="sxs-lookup"><span data-stu-id="91139-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="91139-264">Se i dati sono stati modificati, verrà eseguito il rollback di tale transazione.</span><span class="sxs-lookup"><span data-stu-id="91139-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="91139-265">App per dispositivi mobili supporta il controllo della concorrenza ottimistica tenendo traccia delle modifiche apportate a ogni elemento, usando la colonna di proprietà di sistema `version` definita per ogni tabella nel back-end di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="91139-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="91139-266">Ogni volta che un record viene aggiornato, App per dispositivi mobili imposta la proprietà `version` per quel record su un nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="91139-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="91139-267">Durante ogni richiesta di aggiornamento, la proprietà `version` del record inclusa nella richiesta viene confrontata con la stessa proprietà relativa al record sul server.</span><span class="sxs-lookup"><span data-stu-id="91139-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="91139-268">Se la versione passata con la richiesta non corrisponde a quella del back-end, la libreria client genera un'eccezione `MobileServicePreconditionFailedException<T>` .</span><span class="sxs-lookup"><span data-stu-id="91139-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="91139-269">Il tipo incluso nell'eccezione corrisponde al record del back-end contenente la versione dei server del record.</span><span class="sxs-lookup"><span data-stu-id="91139-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="91139-270">L'applicazione può quindi usare questa informazione per decidere se eseguire nuovamente la richiesta di aggiornamento con il valore `version` corretto dal back-end per effettuare il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="91139-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="91139-271">Per abilitare la concorrenza ottimistica, definire una colonna sulla classe di tabella per la proprietà di sistema `version` .</span><span class="sxs-lookup"><span data-stu-id="91139-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="91139-272">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="91139-272">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="91139-273">Le applicazioni che usano tabelle non tipizzate abilitano la concorrenza ottimistica impostando il flag `Version` per `SystemProperties` della tabella, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="91139-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="91139-274">Oltre ad abilitare la concorrenza ottimistica, è necessario individuare l'eccezione `MobileServicePreconditionFailedException<T>` nel codice quando si esegue una chiamata a [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="91139-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="91139-275">Risolvere il conflitto applicando il valore corretto `version` al record aggiornato ed eseguire una chiamata a [UpdateAsync] con il record risolto.</span><span class="sxs-lookup"><span data-stu-id="91139-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="91139-276">Il codice seguente illustra come risolvere un conflitto di scrittura, qualora venga rilevato.</span><span class="sxs-lookup"><span data-stu-id="91139-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="91139-277">Per altre informazioni, vedere l'argomento [Sincronizzazione di dati offline nelle App per dispositivi mobili di Azure] .</span><span class="sxs-lookup"><span data-stu-id="91139-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="91139-278"><a name="binding"></a>Procedura: Associare dati di App per dispositivi mobili a un'interfaccia utente Windows</span><span class="sxs-lookup"><span data-stu-id="91139-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="91139-279">Questa sezione illustra come visualizzare gli oggetti dati restituiti usando elementi dell'interfaccia utente in un'app Windows.</span><span class="sxs-lookup"><span data-stu-id="91139-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="91139-280">L'esempio di codice seguente associa all'origine dell'elenco una query per la ricerca di elementi non completati.</span><span class="sxs-lookup"><span data-stu-id="91139-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="91139-281">[MobileServiceCollection] crea una raccolta di associazione compatibile con App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="91139-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="91139-282">Alcuni controlli del runtime gestito supportano un'interfaccia denominata [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="91139-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="91139-283">Questa interfaccia consente ai controlli di richiedere dati aggiuntivi nello scorrimento verso il basso.</span><span class="sxs-lookup"><span data-stu-id="91139-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="91139-284">Per questa interfaccia per le app di Windows universale è disponibile un supporto incorporato tramite [MobileServiceIncrementalLoadingCollection], che gestisce automaticamente le chiamate dai controlli.</span><span class="sxs-lookup"><span data-stu-id="91139-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="91139-285">Usare `MobileServiceIncrementalLoadingCollection` nelle app di Windows come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="91139-286">Per usare la nuova raccolta in app di Windows Phone 8 e "Silverlight", usare i metodi di estensione `ToCollection` su `IMobileServiceTableQuery<T>` e `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="91139-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="91139-287">Per caricare i dati, chiamare `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="91139-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="91139-288">Quando si usa la raccolta creata tramite la chiamata a `ToCollectionAsync` o `ToCollection`, si ottiene una raccolta che può essere associata ai controlli dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="91139-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="91139-289">Questa raccolta è compatibile con il paging.</span><span class="sxs-lookup"><span data-stu-id="91139-289">This collection is paging-aware.</span></span>  <span data-ttu-id="91139-290">Poiché la raccolta sta caricando i dati dalla rete, talvolta il caricamento ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="91139-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="91139-291">Per risolvere questi errori, eseguire l'override del metodo `OnException` in `MobileServiceIncrementalLoadingCollection` per gestire le eccezioni derivanti da chiamate a `LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="91139-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="91139-292">Si supponga che la tabella sia costituita da molti campi, ma che si desideri visualizzarne solo alcuni nel controllo.</span><span class="sxs-lookup"><span data-stu-id="91139-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="91139-293">È possibile seguire le indicazioni riportate nella sezione "[Selezionare colonne specifiche](#selecting)" precedente per scegliere specifiche colonne da visualizzare nell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="91139-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="91139-294"><a name="pagesize"></a>Modificare le dimensioni di pagina</span><span class="sxs-lookup"><span data-stu-id="91139-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="91139-295">Per impostazione predefinita, App per dispositivi mobili di Azure restituisce un massimo di 50 elementi per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="91139-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="91139-296">È possibile modificare la dimensione del paging aumentando le dimensioni massime della pagina nel client e nel server.</span><span class="sxs-lookup"><span data-stu-id="91139-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="91139-297">Per aumentare le dimensioni richieste, specificare `PullOptions` quando si usa `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="91139-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="91139-298">Se il valore di `PageSize` è impostato in modo da essere uguale a o maggiore di 100 all'interno del server, verranno restituiti al massimo 100 elementi.</span><span class="sxs-lookup"><span data-stu-id="91139-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="91139-299"><a name="#offlinesync"></a>Usare le tabelle offline</span><span class="sxs-lookup"><span data-stu-id="91139-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="91139-300">Le tabelle offline usano un archivio SQLite locale per archiviare dati da usare in modalità offline.</span><span class="sxs-lookup"><span data-stu-id="91139-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="91139-301">Tutte le operazioni delle tabelle vengono eseguite nell'archivio SQLite locale anziché nell'archivio sul server remoto.</span><span class="sxs-lookup"><span data-stu-id="91139-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="91139-302">Per creare una tabella offline è necessario innanzitutto preparare il progetto:</span><span class="sxs-lookup"><span data-stu-id="91139-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="91139-303">In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione > **Gestisci pacchetti NuGet per la soluzione**, quindi cercare e installare il pacchetto NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** per tutti i progetti della soluzione.</span><span class="sxs-lookup"><span data-stu-id="91139-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="91139-304">(Facoltativo) Per supportare i dispositivi Windows, installare uno dei pacchetti di runtime SQLite seguenti:</span><span class="sxs-lookup"><span data-stu-id="91139-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="91139-305">**Windows 8.1 Runtime:** installare [SQLite per Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="91139-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="91139-306">**Windows Phone 8.1:** installare [SQLite per Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="91139-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="91139-307">**Piattaforma UWP (Universal Windows Platform):** installare [SQLite per Universal Windows Platform][5].</span><span class="sxs-lookup"><span data-stu-id="91139-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="91139-308">(Facoltativo).</span><span class="sxs-lookup"><span data-stu-id="91139-308">(Optional).</span></span> <span data-ttu-id="91139-309">Per i dispositivi Windows fare clic su **Riferimenti** > **Aggiungi riferimento**, espandere la cartella **Windows** > **Estensioni**, quindi abilitare **SQLite for Windows Runtime** SDK con **Visual C++ 2013 Runtime for Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="91139-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="91139-310">I nomi degli SDK di SQLite sono leggermente diversi per ogni piattaforma Windows.</span><span class="sxs-lookup"><span data-stu-id="91139-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="91139-311">Prima di poter creare un riferimento alla tabella è necessario preparare l'archivio locale:</span><span class="sxs-lookup"><span data-stu-id="91139-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="91139-312">L'inizializzazione dell'archivio di solito viene effettuata immediatamente dopo aver creato il client.</span><span class="sxs-lookup"><span data-stu-id="91139-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="91139-313">**OfflineDbPath** deve essere un nome di file appropriato per l'uso in tutte le piattaforme supportate.</span><span class="sxs-lookup"><span data-stu-id="91139-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="91139-314">Se il percorso è completo (ovvero inizia con una barra), viene usato il percorso.</span><span class="sxs-lookup"><span data-stu-id="91139-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="91139-315">Se il percorso non è completo, il file viene posizionato in un percorso che dipende dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="91139-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="91139-316">Per i dispositivi iOS e Android il percorso predefinito è la cartella "File personali".</span><span class="sxs-lookup"><span data-stu-id="91139-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="91139-317">Per i dispositivi Windows il percorso predefinito è la cartella "AppData" specifica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="91139-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="91139-318">È possibile ottenere un riferimento alla tabella usando il metodo `GetSyncTable<>`:</span><span class="sxs-lookup"><span data-stu-id="91139-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="91139-319">Per usare una tabella offline non è necessario eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="91139-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="91139-320">È necessario eseguire l'autenticazione solo quando si comunica con il servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="91139-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="91139-321"><a name="syncoffline"></a>Sincronizzazione di una tabella offline</span><span class="sxs-lookup"><span data-stu-id="91139-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="91139-322">Per impostazione predefinita le tabelle offline non sono sincronizzate con il back-end.</span><span class="sxs-lookup"><span data-stu-id="91139-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="91139-323">La sincronizzazione è suddivisa in due parti.</span><span class="sxs-lookup"><span data-stu-id="91139-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="91139-324">È possibile inserire le modifiche separatamente rispetto al download di nuovi elementi.</span><span class="sxs-lookup"><span data-stu-id="91139-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="91139-325">Ecco un metodo di sincronizzazione tipico:</span><span class="sxs-lookup"><span data-stu-id="91139-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
            //Use a different query name for each unique query in your program
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

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
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

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="91139-326">Se il primo argomento di `PullAsync` è null, non viene usata la sincronizzazione incrementale.</span><span class="sxs-lookup"><span data-stu-id="91139-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="91139-327">Ogni operazione di sincronizzazione recupera tutti i record.</span><span class="sxs-lookup"><span data-stu-id="91139-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="91139-328">L'SDK esegue un `PushAsync()` implicito prima di estrarre i record.</span><span class="sxs-lookup"><span data-stu-id="91139-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="91139-329">La gestione dei conflitti viene eseguita su un metodo `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="91139-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="91139-330">È possibile gestire i conflitti allo stesso modo delle tabelle in linea.</span><span class="sxs-lookup"><span data-stu-id="91139-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="91139-331">Il conflitto viene generato quando viene chiamato `PullAsync()` al posto di durante l'inserimento, l'aggiornamento o l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="91139-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="91139-332">Se si verificano più conflitti, vengono aggregati in un singolo MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="91139-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="91139-333">Gestire separatamente ogni errore.</span><span class="sxs-lookup"><span data-stu-id="91139-333">Handle each failure separately.</span></span>

## <span data-ttu-id="91139-334"><a name="#customapi"></a>Usare un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="91139-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="91139-335">Un'API personalizzata consente di definire endpoint personalizzati che espongono la funzionalità del server di cui non è possibile eseguire il mapping a un'operazione di inserimento, aggiornamento, eliminazione o lettura.</span><span class="sxs-lookup"><span data-stu-id="91139-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="91139-336">L'utilizzo di un'API personalizzata offre maggiore controllo sulla messaggistica, incluse la lettura e l'impostazione delle intestazioni del messaggio HTTP e la definizione di un formato del corpo del messaggio diverso da JSON.</span><span class="sxs-lookup"><span data-stu-id="91139-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="91139-337">Per chiamare un'API personalizzata, è sufficiente chiamare uno dei metodi [InvokeApiAsync] sul client.</span><span class="sxs-lookup"><span data-stu-id="91139-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="91139-338">Ad esempio, la riga di codice seguente invia una richiesta POST all'API **completeAll** sul back-end:</span><span class="sxs-lookup"><span data-stu-id="91139-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="91139-339">Questo formato è una chiamata tipizzata al metodo, che richiede che il tipo restituito **MarkAllResult** sia definito.</span><span class="sxs-lookup"><span data-stu-id="91139-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="91139-340">Sono supportati sia i metodi tipizzati, sia quelli non tipizzati.</span><span class="sxs-lookup"><span data-stu-id="91139-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="91139-341">Il metodo InvokeApiAsync() antepone "/api/" all'API che si desidera chiamare, a meno che l'API non inizi con una "/".</span><span class="sxs-lookup"><span data-stu-id="91139-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="91139-342">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="91139-342">For example:</span></span>

* <span data-ttu-id="91139-343">`InvokeApiAsync("completeAll",...)` chiama /api/completeAll nel back-end</span><span class="sxs-lookup"><span data-stu-id="91139-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="91139-344">`InvokeApiAsync("/.auth/me",...)` chiama /.auth/me nel back-end</span><span class="sxs-lookup"><span data-stu-id="91139-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="91139-345">È possibile utilizzare InvokeApiAsync per chiamare qualsiasi API Web, tra cui le API Web che non sono definite con App per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="91139-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="91139-346">Quando si utilizza InvokeApiAsync(), le intestazioni appropriate, incluse le intestazioni di autenticazione, vengono inviate con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="91139-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="91139-347"><a name="authentication"></a>Autenticare gli utenti</span><span class="sxs-lookup"><span data-stu-id="91139-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="91139-348">App per dispositivi mobili supporta l'autenticazione e l'autorizzazione di utenti di app tramite diversi provider di identità esterni: Facebook, Google, Microsoft Account, Twitter e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91139-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="91139-349">È possibile impostare le autorizzazioni per le tabelle per limitare l'accesso per operazioni specifiche solo agli utenti autenticati.</span><span class="sxs-lookup"><span data-stu-id="91139-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="91139-350">È inoltre possibile utilizzare l'identità degli utenti autenticati per implementare regole di autorizzazione negli script del server.</span><span class="sxs-lookup"><span data-stu-id="91139-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="91139-351">Per altre informazioni, vedere l'esercitazione [Aggiungere l'autenticazione all'app di Servizi mobili].</span><span class="sxs-lookup"><span data-stu-id="91139-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="91139-352">Sono supportati due flussi di autenticazione: flusso *gestito dal client* e flusso *gestito dal server*.</span><span class="sxs-lookup"><span data-stu-id="91139-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="91139-353">Il flusso gestito dal server è il processo di autenticazione più semplice, poiché si basa sull'interfaccia di autenticazione Web del provider.</span><span class="sxs-lookup"><span data-stu-id="91139-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="91139-354">Il flusso gestito dal client assicura una maggiore integrazione con funzionalità specifiche del dispositivo, poiché si basa su SDK specifici del provider e del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91139-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="91139-355">Nelle app di produzione è consigliabile usare un flusso gestito dal client.</span><span class="sxs-lookup"><span data-stu-id="91139-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="91139-356">Per configurare l'autenticazione, è necessario registrare l'app con uno o più provider di identità.</span><span class="sxs-lookup"><span data-stu-id="91139-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="91139-357">Il provider di identità genera un ID client e un segreto client per l'app.</span><span class="sxs-lookup"><span data-stu-id="91139-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="91139-358">Questi valori vengono quindi impostati nel back-end per abilitare l'autenticazione/l'autorizzazione del Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="91139-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="91139-359">Per altre informazioni, seguire le istruzioni dettagliate dell'esercitazione [Aggiungere l'autenticazione all'app di Servizi mobili].</span><span class="sxs-lookup"><span data-stu-id="91139-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="91139-360">Questo articolo descrive gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="91139-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="91139-361">Autenticazione gestita dal client</span><span class="sxs-lookup"><span data-stu-id="91139-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="91139-362">Autenticazione gestita dal server</span><span class="sxs-lookup"><span data-stu-id="91139-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="91139-363">Memorizzazione nella cache del token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="91139-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="91139-364"><a name="clientflow"></a>Autenticazione gestita dal client</span><span class="sxs-lookup"><span data-stu-id="91139-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="91139-365">L'app può contattare il provider di identità in modo indipendente e quindi fornire il token restituito durante l'accesso con il back-end.</span><span class="sxs-lookup"><span data-stu-id="91139-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="91139-366">Mediante il flusso client è possibile consentire agli utenti di effettuare l'accesso un'unica volta o recuperare dal provider di identità dati utente aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="91139-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="91139-367">L'autenticazione del flusso client è preferibile rispetto all'uso di un flusso server, perché l'SDK del provider di identità garantisce un'esperienza utente più naturale e consente una maggiore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="91139-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="91139-368">Vengono forniti esempi per i modelli di autenticazione del flusso client seguenti:</span><span class="sxs-lookup"><span data-stu-id="91139-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="91139-369">Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="91139-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="91139-370">Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="91139-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="91139-371">Live SDK</span><span class="sxs-lookup"><span data-stu-id="91139-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="91139-372"><a name="adal"></a>Autenticare gli utenti con Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="91139-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="91139-373">È possibile usare Active Directory Authentication Library (ADAL) per avviare l'autenticazione degli utenti dal client usando l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91139-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="91139-374">Configurare il back-end dell'app per dispositivi mobili per l'accesso ad Azure Active Directory seguendo l'esercitazione [Come configurare un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="91139-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="91139-375">Assicurarsi di completare il passaggio facoltativo di registrazione di un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="91139-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="91139-376">In Visual Studio o Xamarin Studio aprire il progetto e aggiungere un riferimento al pacchetto NuGet `Microsoft.IdentityModel.CLients.ActiveDirectory` .</span><span class="sxs-lookup"><span data-stu-id="91139-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="91139-377">Includere nella ricerca le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="91139-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="91139-378">Aggiungere il codice seguente all'applicazione, in base alla piattaforma usata.</span><span class="sxs-lookup"><span data-stu-id="91139-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="91139-379">Apportare le sostituzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="91139-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="91139-380">Sostituire **INSERT-AUTHORITY-HERE** con il nome del tenant in cui è stato eseguito il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="91139-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="91139-381">Il formato deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="91139-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="91139-382">È possibile copiare questo valore dalla scheda Dominio di Azure Active Directory nel [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="91139-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="91139-383">Sostituire **INSERT-RESOURCE-ID-HERE** con l'ID client per il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="91139-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="91139-384">L'ID client è disponibile nella scheda **Avanzate** in **Impostazioni di Azure Active Directory** nel portale.</span><span class="sxs-lookup"><span data-stu-id="91139-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="91139-385">Sostituire **INSERT-CLIENT-ID-HERE** con l'ID client copiato dall'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="91139-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="91139-386">Sostituire **INSERT-REDIRECT-URI-HERE** con l'endpoint */.auth/login/done* del sito, usando lo schema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="91139-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="91139-387">Questo valore deve essere simile a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="91139-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="91139-388">Il codice necessario per ogni piattaforma è riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="91139-389">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="91139-389">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="91139-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="91139-390">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="91139-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="91139-391">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="91139-392"><a name="client-facebook"></a>Accesso singolo usando un token da Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="91139-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="91139-393">È possibile usare il flusso client come illustrato in questo frammento di codice per Facebook o Google.</span><span class="sxs-lookup"><span data-stu-id="91139-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="91139-394"><a name="client-livesdk"></a>Accesso Single Sign-On tramite account Microsoft con Live SDK</span><span class="sxs-lookup"><span data-stu-id="91139-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="91139-395">Per autenticare gli utenti, è necessario registrare l'app presso il centro per sviluppatori degli account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91139-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="91139-396">Configurare i dettagli di registrazione nel back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="91139-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="91139-397">Per creare la registrazione di un account Microsoft e connetterlo al back-end dell'app per dispositivi mobili, completare i passaggi nell'articolo [Come configurare l'applicazione del servizio app per usare l'account di accesso Microsoft].</span><span class="sxs-lookup"><span data-stu-id="91139-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="91139-398">Se si dispone di entrambe le versioni dell'app (Windows Store e Windows Phone 8/Silverlight), registrare prima la versione di Windows Store.</span><span class="sxs-lookup"><span data-stu-id="91139-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="91139-399">Il codice seguente esegue l'autenticazione usando Live SDK e usa il token restituito per accedere al back-end di App per i dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="91139-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="91139-400">Per altre informazioni, vedere la documentazione su [Windows Live SDK] .</span><span class="sxs-lookup"><span data-stu-id="91139-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="91139-401"><a name="serverflow"></a>Autenticazione gestita dal server</span><span class="sxs-lookup"><span data-stu-id="91139-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="91139-402">Dopo avere eseguito la registrazione del provider di identità, chiamare il metodo [LoginAsync] su [MobileServiceClient] con il valore [MobileServiceAuthenticationProvider] del provider.</span><span class="sxs-lookup"><span data-stu-id="91139-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="91139-403">Ad esempio, con il codice seguente viene avviato un accesso al flusso server mediante Facebook.</span><span class="sxs-lookup"><span data-stu-id="91139-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="91139-404">Se si usa un provider di identità diverso da Facebook, sostituire il valore di [MobileServiceAuthenticationProvider] con il nome del provider.</span><span class="sxs-lookup"><span data-stu-id="91139-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="91139-405">In un flusso server, il Servizio app di Azure gestisce il flusso di autenticazione OAuth visualizzando la pagina di accesso del provider selezionato.</span><span class="sxs-lookup"><span data-stu-id="91139-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="91139-406">Una volta tornato al provider di identità, il Servizio app di Azure genera un token di autenticazione del servizio app.</span><span class="sxs-lookup"><span data-stu-id="91139-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="91139-407">Il metodo [LoginAsync] restituisce un utente [MobileServiceUser], che fornisce sia un elemento [UserId] dell'utente autenticato sia un elemento [MobileServiceAuthenticationToken] sotto forma di token JSON Web (JWT).</span><span class="sxs-lookup"><span data-stu-id="91139-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="91139-408">È possibile memorizzare questo token nella cache e riutilizzarlo fino alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="91139-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="91139-409">Per ulteriori informazioni, vedere [Memorizzazione nella cache del token di autenticazione](#caching).</span><span class="sxs-lookup"><span data-stu-id="91139-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="91139-410"><a name="caching"></a>Memorizzazione nella cache del token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="91139-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="91139-411">In alcuni casi, la chiamata al metodo di accesso può essere evitata dopo la prima autenticazione riuscita, archiviando il token di autenticazione del provider.</span><span class="sxs-lookup"><span data-stu-id="91139-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="91139-412">Le app di Windows Store e UWP possono usare [PasswordVault] per memorizzare nella cache il token di autenticazione corrente dopo un accesso riuscito, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="91139-413">Il valore UserId viene archiviato come UserName delle credenziali e il token viene archiviato come Password.</span><span class="sxs-lookup"><span data-stu-id="91139-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="91139-414">Negli avvii successivi è possibile usare **PasswordVault** per verificare le credenziali memorizzate nella cache.</span><span class="sxs-lookup"><span data-stu-id="91139-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="91139-415">L'esempio seguente usa le credenziali memorizzate nella cache quando vengono trovate e, in caso contrario, prova a eseguire di nuovo l'autenticazione con il back-end:</span><span class="sxs-lookup"><span data-stu-id="91139-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="91139-416">Quando si disconnette un utente, è necessario rimuovere anche le credenziali archiviate, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="91139-417">Le app Xamarin usano le API [Xamarin.Auth] per archiviare in modo sicuro le credenziali in un oggetto **Account** .</span><span class="sxs-lookup"><span data-stu-id="91139-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="91139-418">Per un esempio dell'uso di queste API, vedere il file di codice [AuthStore.cs] nell'[esempio di condivisione di foto di ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="91139-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="91139-419">Quando si usa l'autenticazione gestita dal client, è anche possibile memorizzare nella cache il token di accesso fornito dal provider, ad esempio Facebook o Twitter.</span><span class="sxs-lookup"><span data-stu-id="91139-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="91139-420">Questo token può essere fornito per richiedere un nuovo token di autenticazione dal back-end, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="91139-421"><a name="pushnotifications"></a>Notifiche push</span><span class="sxs-lookup"><span data-stu-id="91139-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="91139-422">Gli argomenti seguenti descrivono le notifiche push:</span><span class="sxs-lookup"><span data-stu-id="91139-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="91139-423">Registrarsi per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="91139-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="91139-424">Ottenere un SID pacchetto di Windows Store</span><span class="sxs-lookup"><span data-stu-id="91139-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="91139-425">Registrare modelli multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="91139-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="91139-426"><a name="register-for-push"></a>Procedura: Registrarsi per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="91139-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="91139-427">Il client di App per dispositivi mobili consente di registrarsi per le notifiche push con Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="91139-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="91139-428">Durante la registrazione, si ottiene un handle fornito dal servizio di notifica push specifico della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="91139-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="91139-429">È quindi possibile specificare questo valore con qualsiasi tag al momento della creazione della registrazione.</span><span class="sxs-lookup"><span data-stu-id="91139-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="91139-430">Il codice seguente registra l'app Windows per le notifiche push mediante il Servizio di notifica Windows (WNS):</span><span class="sxs-lookup"><span data-stu-id="91139-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="91139-431">Se si effettua il push a WNS, è necessario [ottenere un SID pacchetto di Windows Store](#package-sid) (vedere sotto).</span><span class="sxs-lookup"><span data-stu-id="91139-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="91139-432">Per ulteriori informazioni sulle app di Windows, compresa la modalità di registrazione per le registrazioni del modello, vedere [Aggiungere notifiche push all'app].</span><span class="sxs-lookup"><span data-stu-id="91139-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="91139-433">La richiesta di tag dal client non è supportata.</span><span class="sxs-lookup"><span data-stu-id="91139-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="91139-434">Le richieste di tag vengono eliminate automaticamente dalla registrazione.</span><span class="sxs-lookup"><span data-stu-id="91139-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="91139-435">Se si desidera registrare il dispositivo con tag, creare un'API personalizzata che usa l'API di hub di notifica per eseguire la registrazione automaticamente.</span><span class="sxs-lookup"><span data-stu-id="91139-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="91139-436">[Eseguire una chiamata all'API personalizzata](#customapi) invece che al metodo `RegisterNativeAsync()`.</span><span class="sxs-lookup"><span data-stu-id="91139-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="91139-437"><a name="package-sid"></a>Procedura: ottenere un SID pacchetto di Windows Store</span><span class="sxs-lookup"><span data-stu-id="91139-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="91139-438">Per abilitare le notifiche push nelle app di Windows Store è necessario un SID pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91139-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="91139-439">Per ricevere un SID pacchetto, registrare l'applicazione in Windows Store.</span><span class="sxs-lookup"><span data-stu-id="91139-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="91139-440">Per ottenere questo valore:</span><span class="sxs-lookup"><span data-stu-id="91139-440">To obtain this value:</span></span>

1. <span data-ttu-id="91139-441">In Esplora soluzioni di Visual Studio, fare clic con il pulsante destro del mouse sul progetto app di Windows Store, quindi scegliere **Store** > **Associa applicazione a Store**.</span><span class="sxs-lookup"><span data-stu-id="91139-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="91139-442">Nella procedura guidata fare clic su **Avanti**, effettuare l'accesso con l'account Microsoft, immettere un nome per l'app in **Riserva un nuovo nome dell'app** e quindi fare clic su **Riserva**.</span><span class="sxs-lookup"><span data-stu-id="91139-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="91139-443">Dopo la creazione della registrazione dell'app, selezionare il nome dell'app, fare clic su **Avanti** e quindi su **Associa**.</span><span class="sxs-lookup"><span data-stu-id="91139-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="91139-444">Accedere al [Windows Dev Center] con l'account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91139-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="91139-445">In **App personali**fare clic sulla registrazione dell'app creata.</span><span class="sxs-lookup"><span data-stu-id="91139-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="91139-446">Fare clic su **Gestione dell'app** > **Identità dell'app**, e poi scorrere fino a trovare il **SID pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="91139-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="91139-447">In molti casi il SID pacchetto viene considerato come un URI ed è necessario usare *ms-app: / /* come schema.</span><span class="sxs-lookup"><span data-stu-id="91139-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="91139-448">Prendere nota della versione del SID pacchetto formato tramite la concatenazione di questo valore come prefisso.</span><span class="sxs-lookup"><span data-stu-id="91139-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="91139-449">Le app di Xamarin richiedono codice aggiuntivo per registrare un'app in esecuzione sulle piattaforme Android o iOS.</span><span class="sxs-lookup"><span data-stu-id="91139-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="91139-450">Per altre informazioni, vedere l'argomento relativo alla piattaforma in uso:</span><span class="sxs-lookup"><span data-stu-id="91139-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="91139-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="91139-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="91139-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="91139-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="91139-453"><a name="register-xplat"></a>Procedura: registrare modelli push per inviare notifiche multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="91139-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="91139-454">Per registrare i modelli, usare il metodo `RegisterAsync()` con i modelli, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91139-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="91139-455">I modelli sono di tipo `JObject` e possono contenere più modelli nel formato JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="91139-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="91139-456">Il metodo **RegisterAsync()** accetta anche riquadri secondari:</span><span class="sxs-lookup"><span data-stu-id="91139-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="91139-457">Tutti i tag vengono eliminati durante la registrazione per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="91139-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="91139-458">Per aggiungere tag alle istallazione o modelli all'interno delle istallazioni, vedere [Lavorare con l'SDK del server back-end .NET per App per dispositivi mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="91139-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="91139-459">Per inviare notifiche usando questi modelli registrati, vedere l'argomento relativo alle [API di Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="91139-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="91139-460"><a name="misc"></a>Argomenti vari</span><span class="sxs-lookup"><span data-stu-id="91139-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="91139-461"><a name="errors"></a>Procedura: Gestire gli errori</span><span class="sxs-lookup"><span data-stu-id="91139-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="91139-462">Quando si verifica un errore nel back-end, l'SDK del client genera `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="91139-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="91139-463">Nell'esempio seguente viene illustrato come gestire un'eccezione che viene restituita dal back-end:</span><span class="sxs-lookup"><span data-stu-id="91139-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="91139-464">Un altro esempio di gestione delle condizioni di errore è disponibile nell' [esempio di file di App per dispositivi mobili].</span><span class="sxs-lookup"><span data-stu-id="91139-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="91139-465">L'esempio [LoggingHandler] fornisce un gestore delegato di registrazione per registrare le richieste inoltrate al back-end.</span><span class="sxs-lookup"><span data-stu-id="91139-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="91139-466"><a name="headers"></a>Procedura: Personalizzare le intestazioni delle richieste</span><span class="sxs-lookup"><span data-stu-id="91139-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="91139-467">Per supportare lo scenario specifico dell'app, potrebbe essere necessario personalizzare la comunicazione con il back-end di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="91139-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="91139-468">È possibile ad esempio aggiungere un'intestazione personalizzata a tutte le richieste in uscita oppure modificare i codici di stato delle risposte.</span><span class="sxs-lookup"><span data-stu-id="91139-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="91139-469">È possibile usare un [DelegatingHandler] personalizzato, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="91139-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

<span data-ttu-id="91139-470">[Aggiungere l'autenticazione all'app di Servizi mobili]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="91139-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="91139-471">[Sincronizzazione di dati offline nelle App per dispositivi mobili di Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="91139-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="91139-472">[Aggiungere notifiche push all'app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="91139-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="91139-473">[Come configurare l'applicazione del servizio app per usare l'account di accesso Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="91139-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="91139-474">[Come configurare un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="91139-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="91139-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-481">[crea un riferimento a una tabella non tipizzata]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="91139-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="91139-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="91139-497">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="91139-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="91139-498">[portale di Azure classico]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="91139-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="91139-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="91139-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="91139-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="91139-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="91139-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="91139-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="91139-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="91139-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="91139-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="91139-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="91139-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="91139-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="91139-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="91139-506">[API di Hub di notifica]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="91139-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="91139-507">[esempio di file di App per dispositivi mobili]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="91139-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="91139-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="91139-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="91139-509">[documentazione relativa a OData v3]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="91139-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="91139-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="91139-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="91139-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="91139-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="91139-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="91139-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="91139-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="91139-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
