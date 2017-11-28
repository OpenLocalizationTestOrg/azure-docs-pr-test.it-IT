---
title: aaaWorking con hello App del servizio App per dispositivi mobili gestiti libreria client (Windows | Documenti Microsoft
description: Informazioni su come toouse un client .NET per App mobili di Azure App Service con le app di Windows e Xamarin.
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
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="4fbd6-103">Modalità di gestione client per App mobili di Azure hello toouse</span><span class="sxs-lookup"><span data-stu-id="4fbd6-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="4fbd6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4fbd6-104">Overview</span></span>
<span data-ttu-id="4fbd6-105">Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello gestita la libreria client per le app di Azure App Service Mobile App per Windows e Xamarin.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="4fbd6-106">Nel caso di nuove app tooMobile, è necessario considerare prima hello completamento [avvio rapido di applicazioni per dispositivi mobili di Azure] [ 1] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="4fbd6-107">In questa guida è incentrata su hello gestito sul lato client SDK.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="4fbd6-108">toolearn ulteriori informazioni sugli hello SDK lato server per le App per dispositivi mobili, vedere documentazione di hello per hello [Server .NET SDK] [ 2] o [Server Node.js SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="4fbd6-109">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="4fbd6-109">Reference documentation</span></span>
<span data-ttu-id="4fbd6-110">Hello documentazione di riferimento per il client di hello SDK è disponibile in: [riferimento client .NET di Azure Mobile app][4].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="4fbd6-111">È anche possibile trovare alcuni esempi di client in hello [repository GitHub degli esempi di Azure][5].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4fbd6-112">Piattaforme supportate</span><span class="sxs-lookup"><span data-stu-id="4fbd6-112">Supported Platforms</span></span>
<span data-ttu-id="4fbd6-113">Hello piattaforma .NET supporta hello piattaforme seguenti:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="4fbd6-114">Versioni Android di Xamarin per API da 19 a 24 (KitKat tramite Nougat)</span><span class="sxs-lookup"><span data-stu-id="4fbd6-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="4fbd6-115">Versioni iOS di Xamarin per le versioni iOS 8.0 e successive</span><span class="sxs-lookup"><span data-stu-id="4fbd6-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="4fbd6-116">Piattaforma UWP (Universal Windows Platform)</span><span class="sxs-lookup"><span data-stu-id="4fbd6-116">Universal Windows Platform</span></span>
* <span data-ttu-id="4fbd6-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="4fbd6-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="4fbd6-118">Windows Phone 8.0, ad eccezione delle applicazioni Silverlight</span><span class="sxs-lookup"><span data-stu-id="4fbd6-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="4fbd6-119">l'autenticazione "server-flusso" Hello utilizza WebView per hello presentata l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="4fbd6-120">Se il dispositivo di hello non è in grado di toopresent una UI WebView, sono necessari altri metodi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="4fbd6-121">Questo SDK non è quindi adatto per i dispositivi di tipo controllo o con restrizioni simili.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="4fbd6-122"><a name="setup"></a>Installazione e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="4fbd6-123">Si presuppone che si sia già creato e pubblicato il progetto di back-end di App per dispositivi mobili, che include almeno una tabella.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="4fbd6-124">Nel codice hello usato in questo argomento, è denominata tabella hello `TodoItem` e ha hello seguenti colonne: `Id`, `Text`, e `Complete`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="4fbd6-125">Questa tabella è hello stessa tabella creata quando si completa la [avvio rapido di applicazioni per dispositivi mobili di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="4fbd6-126">Hello tipizzata sul lato client tipo corrispondente in c# è hello seguente classe:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

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

<span data-ttu-id="4fbd6-127">Hello [JsonPropertyAttribute] [ 6] è usato toodefine hello *PropertyName* il mapping tra campi tabella hello e client hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="4fbd6-128">toolearn toocreate tabelle come back-end App per dispositivi mobili, vedere hello [argomento .NET Server SDK] [ 7] o hello [argomento Node.js Server SDK] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="4fbd6-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="4fbd6-129">Se è stato creato il back-end dell'App per dispositivi mobili in hello Azure mediante portale hello Guida introduttiva, è inoltre possibile utilizzare hello **tabelle facile** impostazione hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="4fbd6-130">Procedura: installazione hello gestiti pacchetto SDK client</span><span class="sxs-lookup"><span data-stu-id="4fbd6-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="4fbd6-131">Utilizzare uno dei seguenti hello tooinstall metodi hello gestiti pacchetto del client SDK per App per dispositivi mobili da [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="4fbd6-132">**Visual Studio** mouse sul progetto, fare clic su **Gestisci pacchetti NuGet**, cercare hello `Microsoft.Azure.Mobile.Client` del pacchetto, quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="4fbd6-133">**Xamarin Studio** mouse sul progetto, fare clic su **Aggiungi** > **aggiungere pacchetti NuGet**, cercare hello `Microsoft.Azure.Mobile.Client `pacchetto e quindi fare clic su **Aggiungi Pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="4fbd6-134">Nel file principale attività, tenere presenti i seguenti di hello tooadd **utilizzando** istruzione:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="4fbd6-135"><a name="symbolsource"></a>Procedura: Usare i simboli di debug in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4fbd6-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="4fbd6-136">i simboli di Hello per spazio dei nomi Microsoft.Azure.Mobile hello sono disponibili in [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="4fbd6-137">Fare riferimento toothe [SymbolSource istruzioni] [ 11] toointegrate SymbolSource con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="4fbd6-138"><a name="create-client"></a>Creare il client di App per dispositivi mobili hello</span><span class="sxs-lookup"><span data-stu-id="4fbd6-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="4fbd6-139">Hello codice seguente viene creata hello [MobileServiceClient] [ 12] oggetto tooaccess utilizzato il back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="4fbd6-140">Nel codice precedente di hello, sostituire `MOBILE_APP_URL` con hello l'URL di back-end App Mobile hello, che si trova nel pannello per il back-end di App per dispositivi mobili in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="4fbd6-141">oggetto MobileServiceClient Hello deve essere un singleton.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="4fbd6-142">Usare le tabelle</span><span class="sxs-lookup"><span data-stu-id="4fbd6-142">Work with Tables</span></span>
<span data-ttu-id="4fbd6-143">Hello seguenti come dettagli di sezione toosearch e recuperare i record e modificare i dati di hello all'interno di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="4fbd6-144">viene trattato i seguenti argomenti Hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="4fbd6-145">Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="4fbd6-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="4fbd6-146">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="4fbd6-146">Query data</span></span>](#querying)
* [<span data-ttu-id="4fbd6-147">Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="4fbd6-148">Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="4fbd6-149">Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="4fbd6-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="4fbd6-150">Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="4fbd6-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="4fbd6-151">Cercare un record per Id</span><span class="sxs-lookup"><span data-stu-id="4fbd6-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="4fbd6-152">Gestione delle query non tipizzate</span><span class="sxs-lookup"><span data-stu-id="4fbd6-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="4fbd6-153">Inserimento dei dati</span><span class="sxs-lookup"><span data-stu-id="4fbd6-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="4fbd6-154">Aggiornamento dei dati</span><span class="sxs-lookup"><span data-stu-id="4fbd6-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="4fbd6-155">Eliminazione dei dati</span><span class="sxs-lookup"><span data-stu-id="4fbd6-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="4fbd6-156">Risoluzione dei conflitti e concorrenza ottimistica</span><span class="sxs-lookup"><span data-stu-id="4fbd6-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="4fbd6-157">Associazione tooa interfaccia utente di Windows</span><span class="sxs-lookup"><span data-stu-id="4fbd6-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="4fbd6-158">Hello la modifica delle dimensioni della pagina</span><span class="sxs-lookup"><span data-stu-id="4fbd6-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="4fbd6-159"><a name="instantiating"></a>Procedura: Creare un riferimento alla tabella</span><span class="sxs-lookup"><span data-stu-id="4fbd6-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="4fbd6-160">Tutto il codice di accesso o modifica i dati in una tabella di back-end hello chiama le funzioni su hello `MobileServiceTable` oggetto.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="4fbd6-161">Per ottenere una tabella di riferimento toohello, chiamata hello [GetTable] (metodo), come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="4fbd6-162">Hello ha restituito l'oggetto utilizza il modello di serializzazione tipizzato hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="4fbd6-163">Viene supportato anche un modello di serializzazione non tipizzato.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="4fbd6-164">Nell'esempio seguente viene [crea una tabella di riferimento tooan non tipizzato]:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="4fbd6-165">Nelle query non tipizzata, è necessario specificare hello sottostante la stringa di query OData.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="4fbd6-166"><a name="querying"></a>Procedura: Eseguire query sui dati dall'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="4fbd6-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="4fbd6-167">Questa sezione descrive come tooissue query toohello back-end App per dispositivi mobili, che include hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="4fbd6-168">Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="4fbd6-169">Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="4fbd6-170">Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="4fbd6-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="4fbd6-171">Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="4fbd6-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="4fbd6-172">Cercare dati in base all'ID</span><span class="sxs-lookup"><span data-stu-id="4fbd6-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="4fbd6-173">Una dimensione di pagina basato su server è imposto tooprevent tutte le righe da restituito.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="4fbd6-174">Paging mantiene richieste predefinito per grandi set di dati da incidere negativamente sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="4fbd6-175">tooreturn più di 50 righe, utilizzare hello `Skip` e `Take` (metodo), come descritto in [restituire i dati nelle pagine](#paging).</span><span class="sxs-lookup"><span data-stu-id="4fbd6-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="4fbd6-176"><a name="filtering"></a>Procedura: Filtrare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="4fbd6-177">Hello codice seguente viene illustrato come dati toofilter includendo un `Where` in una query.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="4fbd6-178">Restituisce tutti gli elementi da `todoTable` cui `Complete` proprietà è uguale a troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="4fbd6-179">Hello [in] funzione si applica un predicato di query hello tabella hello del filtro di riga.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="4fbd6-180">È possibile visualizzare hello URI di back-end toohello di hello richiesta inviata tramite il software del controllo, ad esempio gli strumenti di sviluppo del browser o [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="4fbd6-181">Se si osserva URI della richiesta hello, si noti che la stringa di query hello è stata modificata:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="4fbd6-182">La richiesta di OData viene convertita in una query SQL da hello Server SDK:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="4fbd6-183">funzione che viene passato toohello Hello `Where` metodo può avere un numero arbitrario di condizioni.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="4fbd6-184">In questo esempio sarebbe vengano convertito in una query SQL da hello Server SDK:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="4fbd6-185">Questa query può anche essere suddivisa in più clausole:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="4fbd6-186">Hello due metodi sono equivalenti e possono essere utilizzati indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="4fbd6-187">opzione precedente Hello&mdash;della concatenazione di più predicati in un'unica query&mdash;più compatto e consigliato.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="4fbd6-188">Hello `Where` clausola supporta operazioni che essere convertite in subset di hello OData.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="4fbd6-189">Alcune operazioni sono:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-189">Operations include:</span></span>

* <span data-ttu-id="4fbd6-190">Operatori relazionali (==, !=, <, <=, >, >=)</span><span class="sxs-lookup"><span data-stu-id="4fbd6-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="4fbd6-191">Operatori aritmetici (+, -, /, *, %)</span><span class="sxs-lookup"><span data-stu-id="4fbd6-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="4fbd6-192">Approssimazione dei numeri (Math.Floor, Math.Ceiling)</span><span class="sxs-lookup"><span data-stu-id="4fbd6-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="4fbd6-193">Funzioni di stringa (Length, Substring, Replace, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="4fbd6-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="4fbd6-194">Proprietà relative alla data (Year, Month, Day, Hour, Minute, Second)</span><span class="sxs-lookup"><span data-stu-id="4fbd6-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="4fbd6-195">Proprietà di accesso di un oggetto</span><span class="sxs-lookup"><span data-stu-id="4fbd6-195">Access properties of an object, and</span></span>
* <span data-ttu-id="4fbd6-196">Espressioni che combinano queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="4fbd6-197">Quando considerando cosa hello Server SDK supporta, è possibile considerare hello [documentazione di OData v3].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="4fbd6-198"><a name="sorting"></a>Procedura: Ordinare i dati restituiti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="4fbd6-199">Hello codice seguente viene illustrato come dati toosort includendo un [OrderBy] o [OrderByDescending] funzione hello query.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="4fbd6-200">Restituisce gli elementi da `todoTable` disposti in ordine crescente da hello `Text` campo.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

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

### <span data-ttu-id="4fbd6-201"><a name="paging"></a>Procedura: Restituire i dati in pagine</span><span class="sxs-lookup"><span data-stu-id="4fbd6-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="4fbd6-202">Per impostazione predefinita, solo hello back-end hello restituisce le prime 50 righe.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="4fbd6-203">È possibile aumentare il numero di hello di righe restituite dalla chiamata hello [richiedere] metodo.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="4fbd6-204">Utilizzare `Take` insieme hello [Skip] metodo toorequest specifica "pagina" del set di dati totale hello restituita dalla query hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="4fbd6-205">Hello la query seguente, quando eseguita, restituisce gli elementi delle prime tre hello hello tabella.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="4fbd6-206">Ignora la query modificata seguente Hello hello innanzitutto tre risultati e restituisce hello tre risultati.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="4fbd6-207">Questa query produce hello secondo "pagina" di dati, in cui le dimensioni di pagina hello sono tre elementi.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="4fbd6-208">Hello [IncludeTotalCount] metodo richiede il numero totale di hello per *tutti* hello record che sarebbero stati restituiti, ignorando qualsiasi clausola limite/paginazione specificata:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="4fbd6-209">In un'applicazione reale, è possibile utilizzare toohello simile a query precedente esempio con un controllo cercapersone o dell'interfaccia utente simili per spostarsi tra le pagine.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="4fbd6-210">limite di 50 righe toooverride hello in un back-end dell'App per dispositivi mobili, è inoltre necessario applicare hello [EnableQueryAttribute] toohello pubblico GET (metodo) e specificare il comportamento di paging hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="4fbd6-211">Quando applicato toohello metodo, hello seguente imposta too1000 il numero massimo di righe restituito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="4fbd6-212"><a name="selecting"></a>Procedura: Selezionare colonne specifiche</span><span class="sxs-lookup"><span data-stu-id="4fbd6-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="4fbd6-213">È possibile specificare quale set di proprietà tooinclude in hello risultati aggiungendo un [selezionare] query tooyour clausola.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="4fbd6-214">Ad esempio, hello seguente codice mostra come un solo campo tooselect e anche come tooselect e più campi di formato:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
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

<span data-ttu-id="4fbd6-215">Tutti hello funzioni illustrate finora sono additivi, pertanto è possibile mantenere il concatenamento li.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="4fbd6-216">Ogni chiamata concatenata interessa più query hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="4fbd6-217">Un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="4fbd6-218"><a name="lookingup"></a>Procedura: Cercare dati in base all'ID</span><span class="sxs-lookup"><span data-stu-id="4fbd6-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="4fbd6-219">Hello [LookupAsync] funzione può essere utilizzato toolook degli oggetti dal database di hello con un ID specifico.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="4fbd6-220"><a name="untypedqueries"></a>Procedura: eseguire query non tipizzate</span><span class="sxs-lookup"><span data-stu-id="4fbd6-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="4fbd6-221">Quando si esegue una query utilizzando un oggetto della tabella non tipizzato, è necessario specificare esplicitamente stringa di query OData hello chiamando [ReadAsync], come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="4fbd6-222">Si ottengono valori JSON utilizzabili come contenitore delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="4fbd6-223">Per ulteriori informazioni su JToken e Newtonsoft Json.NET, vedere hello [Json.NET] sito.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="4fbd6-224"><a name="inserting"></a>Procedura: Inserire dati in un back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="4fbd6-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="4fbd6-225">Tutti i tipi di client devono contenere un membro denominato **Id**, che per impostazione predefinita è una stringa.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="4fbd6-226">Questo **Id** è necessaria per eseguire operazioni CRUD e per sincronizzazione offline. hello seguente codice illustra come hello toouse [InsertAsync] nuove righe tooinsert metodo in una tabella.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="4fbd6-227">il parametro Hello contiene toobe dati hello inserito come oggetto .NET.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="4fbd6-228">Se un valore di ID univoco personalizzato non è incluso in hello `todoItem` durante un inserimento, un GUID generato dal server hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="4fbd6-229">È possibile recuperare Id hello generato controllando oggetto hello dopo la chiamata di hello restituisce.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="4fbd6-230">tooinsert non tipizzato dati, è possibile usufruire di Json.NET:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="4fbd6-231">Di seguito è riportato un esempio con un indirizzo di posta elettronica come ID di stringa univoco:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="4fbd6-232">Uso di valori ID</span><span class="sxs-lookup"><span data-stu-id="4fbd6-232">Working with ID values</span></span>
<span data-ttu-id="4fbd6-233">App per dispositivi mobili supporta i valori di stringa personalizzato univoca per della tabella hello **id** colonna.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="4fbd6-234">Valore stringa consente alle applicazioni toouse valori personalizzati, ad esempio indirizzi di posta elettronica o i nomi utente per l'ID di hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="4fbd6-235">ID stringa forniscono hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="4fbd6-236">Vengono generati ID senza un database toohello di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="4fbd6-237">I record sono toomerge più semplice da diverse tabelle o database.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="4fbd6-238">L'integrazione di valori di ID con la logica di un'applicazione è più efficace.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="4fbd6-239">Quando un valore di ID di stringa non è impostato su un record inserito, back-end App Mobile hello genera un valore univoco per l'ID.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="4fbd6-240">È possibile utilizzare hello [Guid.NewGuid] toogenerate metodo i valori, il client hello o nel back-end hello il proprio ID.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="4fbd6-241"><a name="modifying"></a>Procedura: Modificare dati in un back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="4fbd6-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="4fbd6-242">Hello codice seguente viene illustrato come hello toouse [UpdateAsync] metodo tooupdate un record esistente con hello ID con nuove informazioni.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="4fbd6-243">il parametro Hello contiene toobe dati hello aggiornati come un oggetto .NET.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="4fbd6-244">tooupdate non tipizzato dati, è possibile trarre vantaggio da [Json.NET] come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="4fbd6-245">Quando si esegue un aggiornamento è necessario specificare un campo `id` .</span><span class="sxs-lookup"><span data-stu-id="4fbd6-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="4fbd6-246">back-end Hello utilizza hello `id` tooidentify campo cui tooupdate di riga.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="4fbd6-247">Hello `id` campo può essere ottenuto da risultato hello di hello `InsertAsync` chiamare.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="4fbd6-248">Un `ArgumentException` viene generato se si tenta di tooupdate un elemento senza fornire hello `id` valore.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="4fbd6-249"><a name="deleting"></a>Procedura: Eliminare dati in un back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="4fbd6-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="4fbd6-250">Hello codice seguente viene illustrato come hello toouse [DeleteAsync] toodelete metodo un'istanza esistente.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="4fbd6-251">istanza di Hello è identificato da hello `id` campo impostato su hello `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="4fbd6-252">toodelete non tipizzato dati, è possibile usufruire di Json.NET come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="4fbd6-253">Quando si esegue una richiesta di eliminazione, è necessario specificare un ID.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="4fbd6-254">Altre proprietà non viene passata servizio toohello o viene ignorata in servizio hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="4fbd6-255">Hello risultato di un `DeleteAsync` chiamata è in genere `null`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="4fbd6-256">toopass ID Hello in può essere ottenuto da risultato hello di hello `InsertAsync` chiamare.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="4fbd6-257">Oggetto `MobileServiceInvalidOperationException` viene generata quando si tenta di toodelete un elemento senza specificare hello `id` campo.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="4fbd6-258"><a name="optimisticconcurrency"></a>Procedura: Usare la concorrenza ottimistica per la risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="4fbd6-259">Due o più client possono scrivere modifiche toohello stesso elemento in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="4fbd6-260">Senza il rilevamento dei conflitti, dell'ultima scrittura hello sovrascriverebbe eventuali aggiornamenti precedenti.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="4fbd6-261">**controllo della concorrenza ottimistica** presuppone che per ogni transazione sia possibile eseguire il commit, quindi non procede al blocco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="4fbd6-262">Prima di eseguire il commit di una transazione, il controllo della concorrenza ottimistica verifica che nessuna altra transazione ha modificato i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="4fbd6-263">Se i dati di hello sono stati modificati, viene eseguito il rollback di hello commit della transazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="4fbd6-264">App per dispositivi mobili supporta il controllo della concorrenza ottimistica rilevando elemento tooeach modifiche utilizzando hello `version` colonna di proprietà di sistema definite per ogni tabella nel back-end App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="4fbd6-265">Ogni volta che viene aggiornato un record, l'App per dispositivi mobili imposta hello `version` proprietà per tale record tooa nuovo valore.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="4fbd6-266">Durante ogni richiesta di aggiornamento, hello `version` proprietà del record di hello incluso richiesta hello è toohello confrontato stessa proprietà per record hello hello server.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="4fbd6-267">Se la versione passata con hello richiesta non corrisponde a back-end hello e libreria hello del client genera un `MobileServicePreconditionFailedException<T>` eccezione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="4fbd6-268">tipo di Hello incluso con l'eccezione hello è record hello hello back-end contenente hello Server versione di hello record.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="4fbd6-269">Hello applicazione può quindi utilizzare questa toodecide informazioni se richiesta di aggiornamento tooexecute hello con hello corretto `version` valore dalle modifiche di toocommit hello back-end.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="4fbd6-270">Definire una colonna nella classe di tabella hello per hello `version` concorrenza ottimistica tooenable proprietà di sistema.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="4fbd6-271">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-271">For example:</span></span>

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

<span data-ttu-id="4fbd6-272">Le applicazioni di utilizzo di tabelle non tipizzate consentono la concorrenza ottimistica dall'impostazione hello `Version` flag di `SystemProperties` di hello tabella come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="4fbd6-273">In aggiunta tooenabling della concorrenza ottimistica, è necessario intercettare anche hello `MobileServicePreconditionFailedException<T>` eccezione nel codice quando si chiama [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="4fbd6-274">Risolvere il conflitto di hello applicando hello corretto `version` toothe aggiornati i record e chiamare [UpdateAsync] con hello risolto il record.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="4fbd6-275">Hello seguente codice mostra come tooresolve un conflitto di scrittura una volta rilevato:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
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
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="4fbd6-276">Per ulteriori informazioni, vedere hello [non in linea sincronizzazione di dati in App mobili di Azure] argomento.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="4fbd6-277"><a name="binding"></a>Procedura: interfaccia utente di Windows tooa di App per dispositivi mobili associazione dati</span><span class="sxs-lookup"><span data-stu-id="4fbd6-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="4fbd6-278">In questa sezione viene illustrato come toodisplay restituiti oggetti dati utilizzando gli elementi dell'interfaccia utente in un'app di Windows.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="4fbd6-279">Esempio di codice seguente associa toohello origine dell'elenco di hello con una query per elementi incompleti.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="4fbd6-280">[MobileServiceCollection] crea una raccolta di associazione compatibile con App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="4fbd6-281">Alcuni controlli hello gestito chiamata un'interfaccia di supporto di runtime [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="4fbd6-282">Questa interfaccia consente controlli toorequest dati aggiuntivi quando hello utente scorre.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="4fbd6-283">È disponibile un supporto predefinito per questa interfaccia per App universali di Windows tramite [MobileServiceIncrementalLoadingCollection], che gestisce automaticamente le chiamate da controlli hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="4fbd6-284">Usare `MobileServiceIncrementalLoadingCollection` nelle app di Windows come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="4fbd6-285">toouse hello nuova raccolta per le app Windows Phone 8 e "Silverlight", utilizzare hello `ToCollection` metodi di estensione in `IMobileServiceTableQuery<T>` e `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="4fbd6-286">dati tooload, chiamare `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="4fbd6-287">Quando si usa insieme hello creato chiamando `ToCollectionAsync` o `ToCollection`, si ottiene una raccolta che può essere controlli tooUI associato.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="4fbd6-288">Questa raccolta è compatibile con il paging.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-288">This collection is paging-aware.</span></span>  <span data-ttu-id="4fbd6-289">Poiché raccolta hello il caricamento dei dati dalla rete, il caricamento talvolta ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="4fbd6-290">toohandle tali errori, eseguire l'override di hello `OnException` metodo `MobileServiceIncrementalLoadingCollection` toohandle eccezioni determinate dalle chiamate troppo`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="4fbd6-291">Prendere in considerazione se la tabella contiene un numero di campi, ma si desidera solo toodisplay alcuni di essi nel controllo.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="4fbd6-292">È possibile utilizzare istruzioni hello nella precedente sezione hello "[selezionare colonne specifiche](#selecting)" tooselect toodisplay di colonne specifiche in hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="4fbd6-293"><a name="pagesize"></a>Hello Modifica dimensioni pagina</span><span class="sxs-lookup"><span data-stu-id="4fbd6-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="4fbd6-294">Per impostazione predefinita, App per dispositivi mobili di Azure restituisce un massimo di 50 elementi per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="4fbd6-295">È possibile modificare la dimensione del paging hello mediante l'aumento delle dimensioni massime della pagina hello client hello sia nel server.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="4fbd6-296">tooincrease hello dimensioni di pagina richiesto, specificare `PullOptions` quando si utilizza `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="4fbd6-297">Supponendo che sono state apportate hello `PageSize` tooor uguale maggiore di 100 all'interno di server hello, una richiesta restituisce elementi fino a 100.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="4fbd6-298"><a name="#offlinesync"></a>Usare le tabelle offline</span><span class="sxs-lookup"><span data-stu-id="4fbd6-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="4fbd6-299">Le tabelle non in linea utilizzano un locale di SQLite archivio toostore dati per l'utilizzo in modalità offline.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="4fbd6-300">Tabella tutte le operazioni vengono eseguite su hello SQLite locale archiviare invece di archivio di hello server remoto.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="4fbd6-301">toocreate una tabella non in linea, preparare il progetto:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="4fbd6-302">In Visual Studio, fare doppio clic hello soluzione > **Gestisci pacchetti NuGet per la soluzione...** , quindi cercare e installare il **Microsoft.Azure.Mobile.Client.SQLiteStore** pacchetto NuGet per tutti i progetti nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="4fbd6-303">I dispositivi Windows toosupport (facoltativo), installare uno dei seguenti pacchetti runtime SQLite hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="4fbd6-304">**Windows 8.1 Runtime:** installare [SQLite per Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="4fbd6-305">**Windows Phone 8.1:** installare [SQLite per Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="4fbd6-306">**Piattaforma UWP** installare [SQLite per hello Windows universale][5].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="4fbd6-307">(Facoltativo).</span><span class="sxs-lookup"><span data-stu-id="4fbd6-307">(Optional).</span></span> <span data-ttu-id="4fbd6-308">Per i dispositivi Windows, fare clic su **riferimenti** > **Aggiungi riferimento...** , espandere hello **Windows** cartella > **estensioni**, quindi abilitare hello appropriato **SQLite per Windows** SDK insieme hello  **Runtime di Visual C++ 2013 per Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="4fbd6-309">Hello nomi SQLite SDK variano leggermente in ogni piattaforma di Windows.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="4fbd6-310">Prima di poter creare un riferimento alla tabella, è necessario preparare l'archivio locale hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="4fbd6-311">Inizializzazione dell'archivio viene in genere eseguita subito dopo la creazione di client hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="4fbd6-312">Hello **OfflineDbPath** deve essere un nome appropriato per l'utilizzo in tutte le piattaforme supportate.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="4fbd6-313">Se il percorso di hello è un percorso completo (vale a dire inizia con una barra), viene utilizzato tale percorso.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="4fbd6-314">Se il percorso di hello non è completo, file hello viene inserito in un percorso specifico della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="4fbd6-315">Per i dispositivi iOS e Android, percorso predefinito di hello è hello "personale" cartella.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="4fbd6-316">Per i dispositivi Windows, percorso predefinito di hello è cartella di "AppData" hello specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="4fbd6-317">Riferimento a una tabella può essere ottenuto utilizzando hello `GetSyncTable<>` metodo:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="4fbd6-318">Non è necessario tooauthenticate toouse una tabella non in linea.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="4fbd6-319">Tooauthenticate è necessario solo quando si sta comunicando con il servizio back-end hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="4fbd6-320"><a name="syncoffline"></a>Sincronizzazione di una tabella offline</span><span class="sxs-lookup"><span data-stu-id="4fbd6-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="4fbd6-321">Le tabelle non in linea non sono sincronizzate con hello di back-end per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="4fbd6-322">La sincronizzazione è suddivisa in due parti.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="4fbd6-323">È possibile inserire le modifiche separatamente rispetto al download di nuovi elementi.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="4fbd6-324">Ecco un metodo di sincronizzazione tipico:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
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

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
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

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="4fbd6-325">Se hello primo argomento troppo`PullAsync` è null, quindi non viene utilizzata la sincronizzazione incrementale.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="4fbd6-326">Ogni operazione di sincronizzazione recupera tutti i record.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="4fbd6-327">Hello SDK esegue implicita `PushAsync()` prima di estrarre i record.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="4fbd6-328">La gestione dei conflitti viene eseguita su un metodo `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="4fbd6-329">È possibile gestire i conflitti in hello stesso modo delle tabelle in linea.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="4fbd6-330">conflitto di Hello viene generato quando `PullAsync()` viene chiamato anziché durante hello insert, update o delete.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="4fbd6-331">Se si verificano più conflitti, vengono aggregati in un singolo MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="4fbd6-332">Gestire separatamente ogni errore.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-332">Handle each failure separately.</span></span>

## <span data-ttu-id="4fbd6-333"><a name="#customapi"></a>Usare un'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="4fbd6-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="4fbd6-334">Un'API personalizzata consente toodefine endpoint personalizzati che espongono la funzionalità server che non eseguire il mapping delle insert tooan, aggiornare, eliminare o operazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="4fbd6-335">L'utilizzo di un'API personalizzata offre maggiore controllo sulla messaggistica, incluse la lettura e l'impostazione delle intestazioni del messaggio HTTP e la definizione di un formato del corpo del messaggio diverso da JSON.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="4fbd6-336">Chiamare un'API personalizzata chiamando uno dei hello [InvokeApiAsync] metodi nel client hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="4fbd6-337">Ad esempio, hello riga di codice seguente invia un toohello richiesta POST **completeAll** API nel back-end hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="4fbd6-338">Questo modulo è una chiamata al metodo tipizzato e richiede che hello **MarkAllResult** restituire tipo è definito.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="4fbd6-339">Sono supportati sia i metodi tipizzati, sia quelli non tipizzati.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="4fbd6-340">metodo InvokeApiAsync() Hello antepone API toohello 'api /' che si desidera toocall a meno che non hello API inizia con un '/'.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="4fbd6-341">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-341">For example:</span></span>

* <span data-ttu-id="4fbd6-342">`InvokeApiAsync("completeAll",...)`chiama /api/completeAll nel back-end hello</span><span class="sxs-lookup"><span data-stu-id="4fbd6-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="4fbd6-343">`InvokeApiAsync("/.auth/me",...)`chiama /.auth/me nel back-end hello</span><span class="sxs-lookup"><span data-stu-id="4fbd6-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="4fbd6-344">È possibile utilizzare InvokeApiAsync toocall qualsiasi WebAPI, tra cui WebAPIs che non sono definiti con App mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="4fbd6-345">Quando si utilizza InvokeApiAsync(), intestazioni appropriate hello, incluse le intestazioni di autenticazione, vengono inviate con richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="4fbd6-346"><a name="authentication"></a>Autenticare gli utenti</span><span class="sxs-lookup"><span data-stu-id="4fbd6-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="4fbd6-347">App per dispositivi mobili supporta l'autenticazione e l'autorizzazione di utenti di app tramite diversi provider di identità esterni: Facebook, Google, Microsoft Account, Twitter e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="4fbd6-348">È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="4fbd6-349">È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione negli script del server.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="4fbd6-350">Per ulteriori informazioni, vedere l'esercitazione hello [Aggiungi autenticazione tooyour app].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="4fbd6-351">Sono supportati due flussi di autenticazione: flusso *gestito dal client* e flusso *gestito dal server*.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="4fbd6-352">flusso server gestito Hello fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia di autenticazione web del provider di hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="4fbd6-353">flusso client gestito Hello consente una maggiore integrazione con funzionalità specifiche del dispositivo come si basa su SDK specifici del dispositivo specifico del provider.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="4fbd6-354">Nelle app di produzione è consigliabile usare un flusso gestito dal client.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="4fbd6-355">tooset dell'autenticazione, è necessario registrare l'app con uno o più provider di identità.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="4fbd6-356">provider di identità Hello genera un ID client e un segreto client dell'app.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="4fbd6-357">Questi valori vengono quindi impostati nel tooenable back-end, l'autenticazione/autorizzazione di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="4fbd6-358">Per ulteriori informazioni, seguire hello istruzioni dettagliate nell'esercitazione [Aggiungi autenticazione tooyour app].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="4fbd6-359">in questa sezione viene trattato i seguenti argomenti Hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="4fbd6-360">Autenticazione gestita dal client</span><span class="sxs-lookup"><span data-stu-id="4fbd6-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="4fbd6-361">Autenticazione gestita dal server</span><span class="sxs-lookup"><span data-stu-id="4fbd6-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="4fbd6-362">Memorizzazione nella cache i token di autenticazione hello</span><span class="sxs-lookup"><span data-stu-id="4fbd6-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="4fbd6-363"><a name="clientflow"></a>Autenticazione gestita dal client</span><span class="sxs-lookup"><span data-stu-id="4fbd6-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="4fbd6-364">L'app può contattare il provider di identità hello in modo indipendente e quindi fornire token restituito hello durante l'accesso con il back-end.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="4fbd6-365">Questo flusso client consente un'esperienza single sign-on per gli utenti o i dati utente aggiuntivi tooretrieve dal provider di identità hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="4fbd6-366">L'autenticazione del client del flusso è toousing preferita del flusso di un server come provider di identità hello SDK fornisce un'idea dell'esperienza utente più nativa e consente un'ulteriore personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="4fbd6-367">Vengono forniti esempi per hello agli schemi di autenticazione client per il flusso seguente:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="4fbd6-368">Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="4fbd6-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="4fbd6-369">Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="4fbd6-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="4fbd6-370">Live SDK</span><span class="sxs-lookup"><span data-stu-id="4fbd6-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="4fbd6-371"><a name="adal"></a>Autenticare gli utenti con Active Directory Authentication Library hello</span><span class="sxs-lookup"><span data-stu-id="4fbd6-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="4fbd6-372">È possibile utilizzare l'autenticazione utente di hello Active Directory Authentication Library (ADAL) tooinitiate da client hello utilizzando l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="4fbd6-373">Configurare il back-end di app per dispositivi mobili per AAD sign-on da hello seguente [come tooconfigure App del servizio per l'account di accesso Active Directory] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="4fbd6-374">Verificare che passaggio facoltativo in hello toocomplete di registrazione di un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="4fbd6-375">In Visual Studio o Xamarin Studio, aprire il progetto e aggiungere un riferimento toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="4fbd6-376">Includere nella ricerca le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="4fbd6-377">Aggiungere hello applicazione tooyour di codice seguente, in base toohello piattaforma in uso.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="4fbd6-378">In ognuno, apportare hello seguenti sostituzioni:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="4fbd6-379">Sostituire **INSERT-autorità-qui** con nome hello del tenant di hello in cui è stato eseguito il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="4fbd6-380">Il formato deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com. Questo valore può essere copiato da scheda dominio hello in Azure Active Directory in hello [portale di Azure classico].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="4fbd6-381">Sostituire **INSERT-RESOURCE-ID-qui** con hello client ID per il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="4fbd6-382">È possibile ottenere l'ID client hello da hello **avanzate** scheda **impostazioni di Azure Active Directory** nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="4fbd6-383">Sostituire **INSERT-CLIENT-ID-qui** con ID client hello copiato dall'applicazione client nativa hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="4fbd6-384">Sostituire **INSERT-REDIRECT-URI-qui** con il sito */.auth/login/done* endpoint, utilizzando lo schema HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="4fbd6-385">Questo valore dovrebbe essere simile troppo*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="4fbd6-386">codice Hello necessario per ogni piattaforma che segue:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="4fbd6-387">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="4fbd6-387">**Windows:**</span></span>

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

     <span data-ttu-id="4fbd6-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="4fbd6-388">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="4fbd6-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="4fbd6-389">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="4fbd6-390"><a name="client-facebook"></a>Accesso singolo usando un token da Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="4fbd6-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="4fbd6-391">È possibile utilizzare il flusso di hello client come illustrato in questo frammento di codice per Facebook o Google.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
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
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="4fbd6-392"><a name="client-livesdk"></a>Single Sign-On utilizzando l'Account Microsoft con hello Live SDK</span><span class="sxs-lookup"><span data-stu-id="4fbd6-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="4fbd6-393">gli utenti tooauthenticate, è necessario registrare l'app nel centro per sviluppatori di account di Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="4fbd6-394">Configurare i dettagli di registrazione nel back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="4fbd6-395">toocreate Microsoft registrazione dell'account e connetterla back-end App Mobile tooyour, hello completato i passaggi [il toouse app un account Microsoft di registrare].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="4fbd6-396">Se si dispone di Windows Store e Windows Phone 8/Silverlight versioni dell'app, registrare prima versione di Windows Store hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="4fbd6-397">Hello codice riportato di seguito viene autenticato mediante Live SDK e utilizza hello restituito token toosign nel back-end App Mobile tooyour.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
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

<span data-ttu-id="4fbd6-398">Per ulteriori informazioni, vedere hello [Windows Live SDK] documentazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="4fbd6-399"><a name="serverflow"></a>Autenticazione gestita dal server</span><span class="sxs-lookup"><span data-stu-id="4fbd6-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="4fbd6-400">Dopo aver registrato il provider di identità, chiamare hello [LoginAsync] metodo hello [MobileServiceClient] con hello [MobileServiceAuthenticationProvider] valore del provider.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="4fbd6-401">Ad esempio, hello codice seguente avvia un server del flusso Accedi con Facebook.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="4fbd6-402">Se si utilizza un provider di identità diverso da Facebook, modificare il valore di hello di [MobileServiceAuthenticationProvider] toohello valore per il provider.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="4fbd6-403">In un flusso di server, servizio App di Azure gestisce il flusso di autenticazione OAuth di hello visualizzando hello-pagina di accesso del provider selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="4fbd6-404">Una volta restituisce provider di identità hello, Azure App Service genera un token di autenticazione del servizio App.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="4fbd6-405">Hello [LoginAsync] metodo restituisce un [MobileServiceUser], che fornisce sia hello [UserId] di hello autenticato l'utente e hello [ MobileServiceAuthenticationToken], come un token web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="4fbd6-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="4fbd6-406">È possibile memorizzare questo token nella cache e riutilizzarlo fino alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="4fbd6-407">Per ulteriori informazioni, vedere [token di autenticazione di memorizzazione nella cache hello](#caching).</span><span class="sxs-lookup"><span data-stu-id="4fbd6-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="4fbd6-408"><a name="caching"></a>Memorizzazione nella cache i token di autenticazione hello</span><span class="sxs-lookup"><span data-stu-id="4fbd6-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="4fbd6-409">Metodo di accesso toohello chiamata hello in alcuni casi, è possibile evitare dopo l'autenticazione prima hello archiviando i token di autenticazione hello dal provider di hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="4fbd6-410">Le applicazioni Windows Store e UWP possono utilizzare [PasswordVault] toocache l'autenticazione corrente token dopo una corretta accesso, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="4fbd6-411">Hello UserId valore viene archiviato come nome utente della credenziale hello hello e token hello è hello archiviato come hello Password.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="4fbd6-412">In Start-up successive, è possibile controllare hello **PasswordVault** per credenziali memorizzate nella cache.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="4fbd6-413">Hello seguente esempio Usa credenziali memorizzate nella cache quando vengono trovati e in caso contrario tenta tooauthenticate nuovamente con back-end hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="4fbd6-414">Quando ci si disconnette un utente, è necessario rimuovere anche credenziale hello archiviata, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="4fbd6-415">App Xamarin utilizzano hello [Xamarin.Auth] credenziali dell'archivio toosecurely API in un **Account** oggetto.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="4fbd6-416">Per un esempio di utilizzo di queste API, vedere hello [AuthStore.cs] file di codice hello [ContosoMoments foto condivisione esempio](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="4fbd6-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="4fbd6-417">Quando si utilizza l'autenticazione client gestito, è anche possibile memorizzare nella cache i token di accesso hello ottenuto dal provider, ad esempio Facebook o Twitter.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="4fbd6-418">Questo token può essere fornito toorequest un nuovo token di autenticazione dal back-end hello, come segue:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="4fbd6-419"><a name="pushnotifications"></a>Notifiche push</span><span class="sxs-lookup"><span data-stu-id="4fbd6-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="4fbd6-420">Hello negli argomenti seguenti vengono descritte le notifiche Push:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="4fbd6-421">Registrarsi per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="4fbd6-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="4fbd6-422">Ottenere un SID pacchetto di Windows Store</span><span class="sxs-lookup"><span data-stu-id="4fbd6-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="4fbd6-423">Registrare modelli multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="4fbd6-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="4fbd6-424"><a name="register-for-push"></a>Procedura: Registrarsi per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="4fbd6-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="4fbd6-425">il client di App per dispositivi mobili Hello consente tooregister per le notifiche push con hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="4fbd6-426">Durante la registrazione, ottenere un handle ottenuta dal specifico della piattaforma hello Push Notification Service (PNS).</span><span class="sxs-lookup"><span data-stu-id="4fbd6-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="4fbd6-427">È quindi possibile fornire questo valore insieme a eventuali tag quando si crea una registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="4fbd6-428">Hello codice seguente viene registrata l'app di Windows per le notifiche push con hello il servizio di notifica di Windows (WNS):</span><span class="sxs-lookup"><span data-stu-id="4fbd6-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="4fbd6-429">Se si effettua il push tooWNS, quindi è necessario [ottenere un SID del pacchetto di Windows Store](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="4fbd6-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="4fbd6-430">Per ulteriori informazioni sulle app di Windows, come tooregister per le registrazioni del modello, vedere [Aggiungi push notifiche tooyour app].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="4fbd6-431">Richiesta di tag da client hello non è supportata.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="4fbd6-432">Le richieste di tag vengono eliminate automaticamente dalla registrazione.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="4fbd6-433">Se si desidera tooregister il dispositivo con tag, creare un'API personalizzata che utilizza la registrazione di hello hello API degli hub di notifica tooperform per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="4fbd6-434">[Chiamare l'API personalizzata hello](#customapi) anziché hello `RegisterNativeAsync()` metodo.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="4fbd6-435"><a name="package-sid"></a>Procedura: ottenere un SID pacchetto di Windows Store</span><span class="sxs-lookup"><span data-stu-id="4fbd6-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="4fbd6-436">Per abilitare le notifiche push nelle app di Windows Store è necessario un SID pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="4fbd6-437">tooreceive, il SID pacchetto registrare l'applicazione con hello Windows Store.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="4fbd6-438">tooobtain questo valore:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-438">tooobtain this value:</span></span>

1. <span data-ttu-id="4fbd6-439">In Esplora soluzioni Visual Studio, progetto di applicazione Windows Store hello pulsante destro del mouse, fare clic su **archivio** > **Associa applicazione a Store hello...** .</span><span class="sxs-lookup"><span data-stu-id="4fbd6-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="4fbd6-440">Nella procedura guidata hello, fare clic su **Avanti**, accedere con l'account Microsoft, digitare un nome per l'app in **riserva nuovo nome applicazione**, quindi fare clic su **riserva**.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="4fbd6-441">Dopo la registrazione dell'app hello è il nome dell'app è stata creata, selezionare hello, fare clic su **Avanti**, quindi fare clic su **associare**.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="4fbd6-442">Accedi toohello [Windows Dev Center] con l'Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="4fbd6-443">In **le mie app**, fare clic su registrazione dell'app hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="4fbd6-444">Fare clic su **gestione delle App** > **identità App**e quindi scorrere verso il basso toofind il **SID pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="4fbd6-445">Molti utilizzi delle SID pacchetto hello considerano come un URI, nel qual caso è necessario toouse *ms-app: / /* lo schema di hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="4fbd6-446">Prendere nota della versione di hello del pacchetto di SID formato concatenando il valore come un prefisso.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="4fbd6-447">App Xamarin richiedono alcuni tooregister in grado di codice aggiuntivo toobe un'app in esecuzione su piattaforme Android o iOS hello.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="4fbd6-448">Per ulteriori informazioni, vedere l'argomento di hello per la piattaforma:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="4fbd6-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="4fbd6-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="4fbd6-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="4fbd6-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="4fbd6-451"><a name="register-xplat"></a>Procedura: registrazione delle notifiche multipiattaforma toosend push modelli</span><span class="sxs-lookup"><span data-stu-id="4fbd6-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="4fbd6-452">modelli tooregister, utilizzare hello `RegisterAsync()` (metodo) con i modelli di hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="4fbd6-453">I modelli devono essere `JObject` tipi e può contenere più modelli di hello seguendo il formato JSON:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

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

<span data-ttu-id="4fbd6-454">metodo Hello **RegisterAsync()** accetta inoltre riquadri secondari:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="4fbd6-455">Tutti i tag vengono eliminati durante la registrazione per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="4fbd6-456">i tag tooadd tooinstallations o modelli in installazioni, vedere [utilizzare i server back-end di hello .NET SDK per App mobili di Azure].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="4fbd6-457">le notifiche toosend utilizzando questi modelli registrati, fare riferimento toohello [API degli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="4fbd6-458"><a name="misc"></a>Argomenti vari</span><span class="sxs-lookup"><span data-stu-id="4fbd6-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="4fbd6-459"><a name="errors"></a>Procedura: Gestire gli errori</span><span class="sxs-lookup"><span data-stu-id="4fbd6-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="4fbd6-460">Quando si verifica un errore nel back-end hello, client hello SDK genera un `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="4fbd6-461">L'esempio seguente viene illustrato come un'eccezione che viene restituita dal back-end hello toohandle:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
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

<span data-ttu-id="4fbd6-462">Un altro esempio di gestione delle condizioni di errore è reperibile in hello [Mobile App i file di esempio].</span><span class="sxs-lookup"><span data-stu-id="4fbd6-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="4fbd6-463">Il [LoggingHandler] riportato di seguito viene fornito un delegato di registrazione gestore toolog hello richieste da toohello di back-end.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="4fbd6-464"><a name="headers"></a>Procedura: Personalizzare le intestazioni delle richieste</span><span class="sxs-lookup"><span data-stu-id="4fbd6-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="4fbd6-465">toosupport dello scenario di applicazione specifico, potrebbe essere necessario toocustomize comunicazione con back-end di hello App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="4fbd6-466">Ad esempio, si potrebbe tooadd una richiesta in uscita di tooevery intestazione personalizzata o cambiare anche i codici di stato delle risposte.</span><span class="sxs-lookup"><span data-stu-id="4fbd6-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="4fbd6-467">È possibile utilizzare un oggetto personalizzato [DelegatingHandler], come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4fbd6-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

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
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
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

[Aggiungi autenticazione tooyour app]: app-service-mobile-windows-store-dotnet-get-started-users.md
[non in linea sincronizzazione di dati in App mobili di Azure]: app-service-mobile-offline-data-sync.md
[Aggiungi push notifiche tooyour app]: app-service-mobile-windows-store-dotnet-get-started-push.md
[il toouse app un account Microsoft di registrare]: app-service-mobile-how-to-configure-microsoft-authentication.md
[come tooconfigure App del servizio per l'account di accesso Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[crea una tabella di riferimento tooan non tipizzato]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[richiedere]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[selezionare]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[in]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[portale di Azure]: https://portal.azure.com/
[portale di Azure classico]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows Dev Center]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[API degli hub di notifica]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile App i file di esempio]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[documentazione di OData v3]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
