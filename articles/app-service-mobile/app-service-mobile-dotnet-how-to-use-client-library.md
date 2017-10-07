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
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Modalità di gestione client per App mobili di Azure hello toouse
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Panoramica
Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello gestita la libreria client per le app di Azure App Service Mobile App per Windows e Xamarin. Nel caso di nuove app tooMobile, è necessario considerare prima hello completamento [avvio rapido di applicazioni per dispositivi mobili di Azure] [ 1] esercitazione. In questa guida è incentrata su hello gestito sul lato client SDK. toolearn ulteriori informazioni sugli hello SDK lato server per le App per dispositivi mobili, vedere documentazione di hello per hello [Server .NET SDK] [ 2] o [Server Node.js SDK] [ 3].

## <a name="reference-documentation"></a>Documentazione di riferimento
Hello documentazione di riferimento per il client di hello SDK è disponibile in: [riferimento client .NET di Azure Mobile app][4].
È anche possibile trovare alcuni esempi di client in hello [repository GitHub degli esempi di Azure][5].

## <a name="supported-platforms"></a>Piattaforme supportate
Hello piattaforma .NET supporta hello piattaforme seguenti:

* Versioni Android di Xamarin per API da 19 a 24 (KitKat tramite Nougat)
* Versioni iOS di Xamarin per le versioni iOS 8.0 e successive
* Piattaforma UWP (Universal Windows Platform)
* Windows Phone 8.1
* Windows Phone 8.0, ad eccezione delle applicazioni Silverlight

l'autenticazione "server-flusso" Hello utilizza WebView per hello presentata l'interfaccia utente.  Se il dispositivo di hello non è in grado di toopresent una UI WebView, sono necessari altri metodi di autenticazione.  Questo SDK non è quindi adatto per i dispositivi di tipo controllo o con restrizioni simili.

## <a name="setup"></a>Installazione e prerequisiti
Si presuppone che si sia già creato e pubblicato il progetto di back-end di App per dispositivi mobili, che include almeno una tabella.  Nel codice hello usato in questo argomento, è denominata tabella hello `TodoItem` e ha hello seguenti colonne: `Id`, `Text`, e `Complete`. Questa tabella è hello stessa tabella creata quando si completa la [avvio rapido di applicazioni per dispositivi mobili di Azure][1].

Hello tipizzata sul lato client tipo corrispondente in c# è hello seguente classe:

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

Hello [JsonPropertyAttribute] [ 6] è usato toodefine hello *PropertyName* il mapping tra campi tabella hello e client hello.

toolearn toocreate tabelle come back-end App per dispositivi mobili, vedere hello [argomento .NET Server SDK] [ 7] o hello [argomento Node.js Server SDK] [ 8] . Se è stato creato il back-end dell'App per dispositivi mobili in hello Azure mediante portale hello Guida introduttiva, è inoltre possibile utilizzare hello **tabelle facile** impostazione hello [portale di Azure].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Procedura: installazione hello gestiti pacchetto SDK client
Utilizzare uno dei seguenti hello tooinstall metodi hello gestiti pacchetto del client SDK per App per dispositivi mobili da [NuGet][9]:

* **Visual Studio** mouse sul progetto, fare clic su **Gestisci pacchetti NuGet**, cercare hello `Microsoft.Azure.Mobile.Client` del pacchetto, quindi fare clic su **installare**.
* **Xamarin Studio** mouse sul progetto, fare clic su **Aggiungi** > **aggiungere pacchetti NuGet**, cercare hello `Microsoft.Azure.Mobile.Client `pacchetto e quindi fare clic su **Aggiungi Pacchetto**.

Nel file principale attività, tenere presenti i seguenti di hello tooadd **utilizzando** istruzione:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Procedura: Usare i simboli di debug in Visual Studio
i simboli di Hello per spazio dei nomi Microsoft.Azure.Mobile hello sono disponibili in [SymbolSource][10].  Fare riferimento toothe [SymbolSource istruzioni] [ 11] toointegrate SymbolSource con Visual Studio.

## <a name="create-client"></a>Creare il client di App per dispositivi mobili hello
Hello codice seguente viene creata hello [MobileServiceClient] [ 12] oggetto tooaccess utilizzato il back-end dell'App Mobile.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

Nel codice precedente di hello, sostituire `MOBILE_APP_URL` con hello l'URL di back-end App Mobile hello, che si trova nel pannello per il back-end di App per dispositivi mobili in hello [portale di Azure]. oggetto MobileServiceClient Hello deve essere un singleton.

## <a name="work-with-tables"></a>Usare le tabelle
Hello seguenti come dettagli di sezione toosearch e recuperare i record e modificare i dati di hello all'interno di tabella hello.  viene trattato i seguenti argomenti Hello:

* [Creare un riferimento alla tabella](#instantiating)
* [Eseguire query sui dati](#querying)
* [Filtrare i dati restituiti](#filtering)
* [Ordinare i dati restituiti](#sorting)
* [Restituire i dati in pagine](#paging)
* [Selezionare colonne specifiche](#selecting)
* [Cercare un record per Id](#lookingup)
* [Gestione delle query non tipizzate](#untypedqueries)
* [Inserimento dei dati](#inserting)
* [Aggiornamento dei dati](#updating)
* [Eliminazione dei dati](#deleting)
* [Risoluzione dei conflitti e concorrenza ottimistica](#optimisticconcurrency)
* [Associazione tooa interfaccia utente di Windows](#binding)
* [Hello la modifica delle dimensioni della pagina](#pagesize)

### <a name="instantiating"></a>Procedura: Creare un riferimento alla tabella
Tutto il codice di accesso o modifica i dati in una tabella di back-end hello chiama le funzioni su hello `MobileServiceTable` oggetto. Per ottenere una tabella di riferimento toohello, chiamata hello [GetTable] (metodo), come indicato di seguito:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Hello ha restituito l'oggetto utilizza il modello di serializzazione tipizzato hello. Viene supportato anche un modello di serializzazione non tipizzato. Nell'esempio seguente viene [crea una tabella di riferimento tooan non tipizzato]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

Nelle query non tipizzata, è necessario specificare hello sottostante la stringa di query OData.

### <a name="querying"></a>Procedura: Eseguire query sui dati dall'app per dispositivi mobili
Questa sezione descrive come tooissue query toohello back-end App per dispositivi mobili, che include hello seguenti funzionalità:

* [Filtrare i dati restituiti](#filtering)
* [Ordinare i dati restituiti](#sorting)
* [Restituire i dati in pagine](#paging)
* [Selezionare colonne specifiche](#selecting)
* [Cercare dati in base all'ID](#lookingup)

> [!NOTE]
> Una dimensione di pagina basato su server è imposto tooprevent tutte le righe da restituito.  Paging mantiene richieste predefinito per grandi set di dati da incidere negativamente sul servizio hello.  tooreturn più di 50 righe, utilizzare hello `Skip` e `Take` (metodo), come descritto in [restituire i dati nelle pagine](#paging).

### <a name="filtering"></a>Procedura: Filtrare i dati restituiti
Hello codice seguente viene illustrato come dati toofilter includendo un `Where` in una query. Restituisce tutti gli elementi da `todoTable` cui `Complete` proprietà è uguale a troppo`false`. Hello [in] funzione si applica un predicato di query hello tabella hello del filtro di riga.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

È possibile visualizzare hello URI di back-end toohello di hello richiesta inviata tramite il software del controllo, ad esempio gli strumenti di sviluppo del browser o [Fiddler]. Se si osserva URI della richiesta hello, si noti che la stringa di query hello è stata modificata:

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

La richiesta di OData viene convertita in una query SQL da hello Server SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

funzione che viene passato toohello Hello `Where` metodo può avere un numero arbitrario di condizioni.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

In questo esempio sarebbe vengano convertito in una query SQL da hello Server SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

Questa query può anche essere suddivisa in più clausole:

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Hello due metodi sono equivalenti e possono essere utilizzati indifferentemente.  opzione precedente Hello&mdash;della concatenazione di più predicati in un'unica query&mdash;più compatto e consigliato.

Hello `Where` clausola supporta operazioni che essere convertite in subset di hello OData. Alcune operazioni sono:

* Operatori relazionali (==, !=, <, <=, >, >=)
* Operatori aritmetici (+, -, /, *, %)
* Approssimazione dei numeri (Math.Floor, Math.Ceiling)
* Funzioni di stringa (Length, Substring, Replace, IndexOf, StartsWith, EndsWith)
* Proprietà relative alla data (Year, Month, Day, Hour, Minute, Second)
* Proprietà di accesso di un oggetto
* Espressioni che combinano queste operazioni.

Quando considerando cosa hello Server SDK supporta, è possibile considerare hello [documentazione di OData v3].

### <a name="sorting"></a>Procedura: Ordinare i dati restituiti
Hello codice seguente viene illustrato come dati toosort includendo un [OrderBy] o [OrderByDescending] funzione hello query. Restituisce gli elementi da `todoTable` disposti in ordine crescente da hello `Text` campo.

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

### <a name="paging"></a>Procedura: Restituire i dati in pagine
Per impostazione predefinita, solo hello back-end hello restituisce le prime 50 righe. È possibile aumentare il numero di hello di righe restituite dalla chiamata hello [richiedere] metodo. Utilizzare `Take` insieme hello [Skip] metodo toorequest specifica "pagina" del set di dati totale hello restituita dalla query hello. Hello la query seguente, quando eseguita, restituisce gli elementi delle prime tre hello hello tabella.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Ignora la query modificata seguente Hello hello innanzitutto tre risultati e restituisce hello tre risultati. Questa query produce hello secondo "pagina" di dati, in cui le dimensioni di pagina hello sono tre elementi.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hello [IncludeTotalCount] metodo richiede il numero totale di hello per *tutti* hello record che sarebbero stati restituiti, ignorando qualsiasi clausola limite/paginazione specificata:

```
query = query.IncludeTotalCount();
```

In un'applicazione reale, è possibile utilizzare toohello simile a query precedente esempio con un controllo cercapersone o dell'interfaccia utente simili per spostarsi tra le pagine.

> [!NOTE]
> limite di 50 righe toooverride hello in un back-end dell'App per dispositivi mobili, è inoltre necessario applicare hello [EnableQueryAttribute] toohello pubblico GET (metodo) e specificare il comportamento di paging hello. Quando applicato toohello metodo, hello seguente imposta too1000 il numero massimo di righe restituito:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Procedura: Selezionare colonne specifiche
È possibile specificare quale set di proprietà tooinclude in hello risultati aggiungendo un [selezionare] query tooyour clausola. Ad esempio, hello seguente codice mostra come un solo campo tooselect e anche come tooselect e più campi di formato:

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

Tutti hello funzioni illustrate finora sono additivi, pertanto è possibile mantenere il concatenamento li. Ogni chiamata concatenata interessa più query hello. Un altro esempio:

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Procedura: Cercare dati in base all'ID
Hello [LookupAsync] funzione può essere utilizzato toolook degli oggetti dal database di hello con un ID specifico.

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Procedura: eseguire query non tipizzate
Quando si esegue una query utilizzando un oggetto della tabella non tipizzato, è necessario specificare esplicitamente stringa di query OData hello chiamando [ReadAsync], come illustrato nell'esempio seguente hello:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

Si ottengono valori JSON utilizzabili come contenitore delle proprietà. Per ulteriori informazioni su JToken e Newtonsoft Json.NET, vedere hello [Json.NET] sito.

### <a name="inserting"></a>Procedura: Inserire dati in un back-end di App per dispositivi mobili
Tutti i tipi di client devono contenere un membro denominato **Id**, che per impostazione predefinita è una stringa. Questo **Id** è necessaria per eseguire operazioni CRUD e per sincronizzazione offline. hello seguente codice illustra come hello toouse [InsertAsync] nuove righe tooinsert metodo in una tabella. il parametro Hello contiene toobe dati hello inserito come oggetto .NET.

```
await todoTable.InsertAsync(todoItem);
```

Se un valore di ID univoco personalizzato non è incluso in hello `todoItem` durante un inserimento, un GUID generato dal server hello.
È possibile recuperare Id hello generato controllando oggetto hello dopo la chiamata di hello restituisce.

tooinsert non tipizzato dati, è possibile usufruire di Json.NET:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

Di seguito è riportato un esempio con un indirizzo di posta elettronica come ID di stringa univoco:

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>Uso di valori ID
App per dispositivi mobili supporta i valori di stringa personalizzato univoca per della tabella hello **id** colonna. Valore stringa consente alle applicazioni toouse valori personalizzati, ad esempio indirizzi di posta elettronica o i nomi utente per l'ID di hello.  ID stringa forniscono hello seguenti vantaggi:

* Vengono generati ID senza un database toohello di andata e ritorno.
* I record sono toomerge più semplice da diverse tabelle o database.
* L'integrazione di valori di ID con la logica di un'applicazione è più efficace.

Quando un valore di ID di stringa non è impostato su un record inserito, back-end App Mobile hello genera un valore univoco per l'ID. È possibile utilizzare hello [Guid.NewGuid] toogenerate metodo i valori, il client hello o nel back-end hello il proprio ID.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Procedura: Modificare dati in un back-end di App per dispositivi mobili
Hello codice seguente viene illustrato come hello toouse [UpdateAsync] metodo tooupdate un record esistente con hello ID con nuove informazioni. il parametro Hello contiene toobe dati hello aggiornati come un oggetto .NET.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate non tipizzato dati, è possibile trarre vantaggio da [Json.NET] come indicato di seguito:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

Quando si esegue un aggiornamento è necessario specificare un campo `id` . back-end Hello utilizza hello `id` tooidentify campo cui tooupdate di riga. Hello `id` campo può essere ottenuto da risultato hello di hello `InsertAsync` chiamare. Un `ArgumentException` viene generato se si tenta di tooupdate un elemento senza fornire hello `id` valore.

### <a name="deleting"></a>Procedura: Eliminare dati in un back-end di App per dispositivi mobili
Hello codice seguente viene illustrato come hello toouse [DeleteAsync] toodelete metodo un'istanza esistente. istanza di Hello è identificato da hello `id` campo impostato su hello `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete non tipizzato dati, è possibile usufruire di Json.NET come indicato di seguito:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

Quando si esegue una richiesta di eliminazione, è necessario specificare un ID. Altre proprietà non viene passata servizio toohello o viene ignorata in servizio hello. Hello risultato di un `DeleteAsync` chiamata è in genere `null`. toopass ID Hello in può essere ottenuto da risultato hello di hello `InsertAsync` chiamare. Oggetto `MobileServiceInvalidOperationException` viene generata quando si tenta di toodelete un elemento senza specificare hello `id` campo.

### <a name="optimisticconcurrency"></a>Procedura: Usare la concorrenza ottimistica per la risoluzione dei conflitti
Due o più client possono scrivere modifiche toohello stesso elemento in hello stesso tempo. Senza il rilevamento dei conflitti, dell'ultima scrittura hello sovrascriverebbe eventuali aggiornamenti precedenti. **controllo della concorrenza ottimistica** presuppone che per ogni transazione sia possibile eseguire il commit, quindi non procede al blocco delle risorse.  Prima di eseguire il commit di una transazione, il controllo della concorrenza ottimistica verifica che nessuna altra transazione ha modificato i dati di hello. Se i dati di hello sono stati modificati, viene eseguito il rollback di hello commit della transazione.

App per dispositivi mobili supporta il controllo della concorrenza ottimistica rilevando elemento tooeach modifiche utilizzando hello `version` colonna di proprietà di sistema definite per ogni tabella nel back-end App per dispositivi mobili. Ogni volta che viene aggiornato un record, l'App per dispositivi mobili imposta hello `version` proprietà per tale record tooa nuovo valore. Durante ogni richiesta di aggiornamento, hello `version` proprietà del record di hello incluso richiesta hello è toohello confrontato stessa proprietà per record hello hello server. Se la versione passata con hello richiesta non corrisponde a back-end hello e libreria hello del client genera un `MobileServicePreconditionFailedException<T>` eccezione. tipo di Hello incluso con l'eccezione hello è record hello hello back-end contenente hello Server versione di hello record. Hello applicazione può quindi utilizzare questa toodecide informazioni se richiesta di aggiornamento tooexecute hello con hello corretto `version` valore dalle modifiche di toocommit hello back-end.

Definire una colonna nella classe di tabella hello per hello `version` concorrenza ottimistica tooenable proprietà di sistema. ad esempio:

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

Le applicazioni di utilizzo di tabelle non tipizzate consentono la concorrenza ottimistica dall'impostazione hello `Version` flag di `SystemProperties` di hello tabella come indicato di seguito.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

In aggiunta tooenabling della concorrenza ottimistica, è necessario intercettare anche hello `MobileServicePreconditionFailedException<T>` eccezione nel codice quando si chiama [UpdateAsync].  Risolvere il conflitto di hello applicando hello corretto `version` toothe aggiornati i record e chiamare [UpdateAsync] con hello risolto il record. Hello seguente codice mostra come tooresolve un conflitto di scrittura una volta rilevato:

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

Per ulteriori informazioni, vedere hello [non in linea sincronizzazione di dati in App mobili di Azure] argomento.

### <a name="binding"></a>Procedura: interfaccia utente di Windows tooa di App per dispositivi mobili associazione dati
In questa sezione viene illustrato come toodisplay restituiti oggetti dati utilizzando gli elementi dell'interfaccia utente in un'app di Windows.  Esempio di codice seguente associa toohello origine dell'elenco di hello con una query per elementi incompleti. [MobileServiceCollection] crea una raccolta di associazione compatibile con App per dispositivi mobili.

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

Alcuni controlli hello gestito chiamata un'interfaccia di supporto di runtime [ISupportIncrementalLoading]. Questa interfaccia consente controlli toorequest dati aggiuntivi quando hello utente scorre. È disponibile un supporto predefinito per questa interfaccia per App universali di Windows tramite [MobileServiceIncrementalLoadingCollection], che gestisce automaticamente le chiamate da controlli hello. Usare `MobileServiceIncrementalLoadingCollection` nelle app di Windows come indicato di seguito:

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse hello nuova raccolta per le app Windows Phone 8 e "Silverlight", utilizzare hello `ToCollection` metodi di estensione in `IMobileServiceTableQuery<T>` e `IMobileServiceTable<T>`. dati tooload, chiamare `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

Quando si usa insieme hello creato chiamando `ToCollectionAsync` o `ToCollection`, si ottiene una raccolta che può essere controlli tooUI associato.  Questa raccolta è compatibile con il paging.  Poiché raccolta hello il caricamento dei dati dalla rete, il caricamento talvolta ha esito negativo. toohandle tali errori, eseguire l'override di hello `OnException` metodo `MobileServiceIncrementalLoadingCollection` toohandle eccezioni determinate dalle chiamate troppo`LoadMoreItemsAsync`.

Prendere in considerazione se la tabella contiene un numero di campi, ma si desidera solo toodisplay alcuni di essi nel controllo. È possibile utilizzare istruzioni hello nella precedente sezione hello "[selezionare colonne specifiche](#selecting)" tooselect toodisplay di colonne specifiche in hello dell'interfaccia utente.

### <a name="pagesize"></a>Hello Modifica dimensioni pagina
Per impostazione predefinita, App per dispositivi mobili di Azure restituisce un massimo di 50 elementi per ogni richiesta.  È possibile modificare la dimensione del paging hello mediante l'aumento delle dimensioni massime della pagina hello client hello sia nel server.  tooincrease hello dimensioni di pagina richiesto, specificare `PullOptions` quando si utilizza `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Supponendo che sono state apportate hello `PageSize` tooor uguale maggiore di 100 all'interno di server hello, una richiesta restituisce elementi fino a 100.

## <a name="#offlinesync"></a>Usare le tabelle offline
Le tabelle non in linea utilizzano un locale di SQLite archivio toostore dati per l'utilizzo in modalità offline.  Tabella tutte le operazioni vengono eseguite su hello SQLite locale archiviare invece di archivio di hello server remoto.  toocreate una tabella non in linea, preparare il progetto:

1. In Visual Studio, fare doppio clic hello soluzione > **Gestisci pacchetti NuGet per la soluzione...** , quindi cercare e installare il **Microsoft.Azure.Mobile.Client.SQLiteStore** pacchetto NuGet per tutti i progetti nella soluzione hello.
2. I dispositivi Windows toosupport (facoltativo), installare uno dei seguenti pacchetti runtime SQLite hello:

   * **Windows 8.1 Runtime:** installare [SQLite per Windows 8.1][3].
   * **Windows Phone 8.1:** installare [SQLite per Windows Phone 8.1][4].
   * **Piattaforma UWP** installare [SQLite per hello Windows universale][5].
3. (Facoltativo). Per i dispositivi Windows, fare clic su **riferimenti** > **Aggiungi riferimento...** , espandere hello **Windows** cartella > **estensioni**, quindi abilitare hello appropriato **SQLite per Windows** SDK insieme hello  **Runtime di Visual C++ 2013 per Windows** SDK.
    Hello nomi SQLite SDK variano leggermente in ogni piattaforma di Windows.

Prima di poter creare un riferimento alla tabella, è necessario preparare l'archivio locale hello:

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

Inizializzazione dell'archivio viene in genere eseguita subito dopo la creazione di client hello.  Hello **OfflineDbPath** deve essere un nome appropriato per l'utilizzo in tutte le piattaforme supportate.  Se il percorso di hello è un percorso completo (vale a dire inizia con una barra), viene utilizzato tale percorso.  Se il percorso di hello non è completo, file hello viene inserito in un percorso specifico della piattaforma.

* Per i dispositivi iOS e Android, percorso predefinito di hello è hello "personale" cartella.
* Per i dispositivi Windows, percorso predefinito di hello è cartella di "AppData" hello specifici dell'applicazione.

Riferimento a una tabella può essere ottenuto utilizzando hello `GetSyncTable<>` metodo:

```
var table = client.GetSyncTable<TodoItem>();
```

Non è necessario tooauthenticate toouse una tabella non in linea.  Tooauthenticate è necessario solo quando si sta comunicando con il servizio back-end hello.

### <a name="syncoffline"></a>Sincronizzazione di una tabella offline
Le tabelle non in linea non sono sincronizzate con hello di back-end per impostazione predefinita.  La sincronizzazione è suddivisa in due parti.  È possibile inserire le modifiche separatamente rispetto al download di nuovi elementi.  Ecco un metodo di sincronizzazione tipico:

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

Se hello primo argomento troppo`PullAsync` è null, quindi non viene utilizzata la sincronizzazione incrementale.  Ogni operazione di sincronizzazione recupera tutti i record.

Hello SDK esegue implicita `PushAsync()` prima di estrarre i record.

La gestione dei conflitti viene eseguita su un metodo `PullAsync()`.  È possibile gestire i conflitti in hello stesso modo delle tabelle in linea.  conflitto di Hello viene generato quando `PullAsync()` viene chiamato anziché durante hello insert, update o delete. Se si verificano più conflitti, vengono aggregati in un singolo MobileServicePushFailedException.  Gestire separatamente ogni errore.

## <a name="#customapi"></a>Usare un'API personalizzata
Un'API personalizzata consente toodefine endpoint personalizzati che espongono la funzionalità server che non eseguire il mapping delle insert tooan, aggiornare, eliminare o operazione di lettura. L'utilizzo di un'API personalizzata offre maggiore controllo sulla messaggistica, incluse la lettura e l'impostazione delle intestazioni del messaggio HTTP e la definizione di un formato del corpo del messaggio diverso da JSON.

Chiamare un'API personalizzata chiamando uno dei hello [InvokeApiAsync] metodi nel client hello. Ad esempio, hello riga di codice seguente invia un toohello richiesta POST **completeAll** API nel back-end hello:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Questo modulo è una chiamata al metodo tipizzato e richiede che hello **MarkAllResult** restituire tipo è definito. Sono supportati sia i metodi tipizzati, sia quelli non tipizzati.

metodo InvokeApiAsync() Hello antepone API toohello 'api /' che si desidera toocall a meno che non hello API inizia con un '/'.
ad esempio:

* `InvokeApiAsync("completeAll",...)`chiama /api/completeAll nel back-end hello
* `InvokeApiAsync("/.auth/me",...)`chiama /.auth/me nel back-end hello

È possibile utilizzare InvokeApiAsync toocall qualsiasi WebAPI, tra cui WebAPIs che non sono definiti con App mobili di Azure.  Quando si utilizza InvokeApiAsync(), intestazioni appropriate hello, incluse le intestazioni di autenticazione, vengono inviate con richiesta di hello.

## <a name="authentication"></a>Autenticare gli utenti
App per dispositivi mobili supporta l'autenticazione e l'autorizzazione di utenti di app tramite diversi provider di identità esterni: Facebook, Google, Microsoft Account, Twitter e Azure Active Directory. È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users. È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione negli script del server. Per ulteriori informazioni, vedere l'esercitazione hello [Aggiungi autenticazione tooyour app].

Sono supportati due flussi di autenticazione: flusso *gestito dal client* e flusso *gestito dal server*. flusso server gestito Hello fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia di autenticazione web del provider di hello. flusso client gestito Hello consente una maggiore integrazione con funzionalità specifiche del dispositivo come si basa su SDK specifici del dispositivo specifico del provider.

> [!NOTE]
> Nelle app di produzione è consigliabile usare un flusso gestito dal client.

tooset dell'autenticazione, è necessario registrare l'app con uno o più provider di identità.  provider di identità Hello genera un ID client e un segreto client dell'app.  Questi valori vengono quindi impostati nel tooenable back-end, l'autenticazione/autorizzazione di servizio App di Azure.  Per ulteriori informazioni, seguire hello istruzioni dettagliate nell'esercitazione [Aggiungi autenticazione tooyour app].

in questa sezione viene trattato i seguenti argomenti Hello:

* [Autenticazione gestita dal client](#clientflow)
* [Autenticazione gestita dal server](#serverflow)
* [Memorizzazione nella cache i token di autenticazione hello](#caching)

### <a name="clientflow"></a>Autenticazione gestita dal client
L'app può contattare il provider di identità hello in modo indipendente e quindi fornire token restituito hello durante l'accesso con il back-end. Questo flusso client consente un'esperienza single sign-on per gli utenti o i dati utente aggiuntivi tooretrieve dal provider di identità hello tooprovide. L'autenticazione del client del flusso è toousing preferita del flusso di un server come provider di identità hello SDK fornisce un'idea dell'esperienza utente più nativa e consente un'ulteriore personalizzazione.

Vengono forniti esempi per hello agli schemi di autenticazione client per il flusso seguente:

* [Active Directory Authentication Library](#adal)
* [Facebook o Google](#client-facebook)
* [Live SDK](#client-livesdk)

#### <a name="adal"></a>Autenticare gli utenti con Active Directory Authentication Library hello
È possibile utilizzare l'autenticazione utente di hello Active Directory Authentication Library (ADAL) tooinitiate da client hello utilizzando l'autenticazione di Azure Active Directory.

1. Configurare il back-end di app per dispositivi mobili per AAD sign-on da hello seguente [come tooconfigure App del servizio per l'account di accesso Active Directory] esercitazione. Verificare che passaggio facoltativo in hello toocomplete di registrazione di un'applicazione client nativa.
2. In Visual Studio o Xamarin Studio, aprire il progetto e aggiungere un riferimento toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` pacchetto NuGet. Includere nella ricerca le versioni non definitive.
3. Aggiungere hello applicazione tooyour di codice seguente, in base toohello piattaforma in uso. In ognuno, apportare hello seguenti sostituzioni:

   * Sostituire **INSERT-autorità-qui** con nome hello del tenant di hello in cui è stato eseguito il provisioning dell'applicazione. Il formato deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com. Questo valore può essere copiato da scheda dominio hello in Azure Active Directory in hello [portale di Azure classico].
   * Sostituire **INSERT-RESOURCE-ID-qui** con hello client ID per il back-end dell'app per dispositivi mobili. È possibile ottenere l'ID client hello da hello **avanzate** scheda **impostazioni di Azure Active Directory** nel portale di hello.
   * Sostituire **INSERT-CLIENT-ID-qui** con ID client hello copiato dall'applicazione client nativa hello.
   * Sostituire **INSERT-REDIRECT-URI-qui** con il sito */.auth/login/done* endpoint, utilizzando lo schema HTTPS hello. Questo valore dovrebbe essere simile troppo*https://contoso.azurewebsites.net/.auth/login/done*.

     codice Hello necessario per ogni piattaforma che segue:

     **Windows:**

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

     **Xamarin.iOS**

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

     **Xamarin.Android**

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

#### <a name="client-facebook"></a>Accesso singolo usando un token da Facebook o Google
È possibile utilizzare il flusso di hello client come illustrato in questo frammento di codice per Facebook o Google.

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

#### <a name="client-livesdk"></a>Single Sign-On utilizzando l'Account Microsoft con hello Live SDK
gli utenti tooauthenticate, è necessario registrare l'app nel centro per sviluppatori di account di Microsoft hello. Configurare i dettagli di registrazione nel back-end dell'app per dispositivi mobili. toocreate Microsoft registrazione dell'account e connetterla back-end App Mobile tooyour, hello completato i passaggi [il toouse app un account Microsoft di registrare]. Se si dispone di Windows Store e Windows Phone 8/Silverlight versioni dell'app, registrare prima versione di Windows Store hello.

Hello codice riportato di seguito viene autenticato mediante Live SDK e utilizza hello restituito token toosign nel back-end App Mobile tooyour.

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

Per ulteriori informazioni, vedere hello [Windows Live SDK] documentazione.

### <a name="serverflow"></a>Autenticazione gestita dal server
Dopo aver registrato il provider di identità, chiamare hello [LoginAsync] metodo hello [MobileServiceClient] con hello [MobileServiceAuthenticationProvider] valore del provider. Ad esempio, hello codice seguente avvia un server del flusso Accedi con Facebook.

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

Se si utilizza un provider di identità diverso da Facebook, modificare il valore di hello di [MobileServiceAuthenticationProvider] toohello valore per il provider.

In un flusso di server, servizio App di Azure gestisce il flusso di autenticazione OAuth di hello visualizzando hello-pagina di accesso del provider selezionato hello.  Una volta restituisce provider di identità hello, Azure App Service genera un token di autenticazione del servizio App. Hello [LoginAsync] metodo restituisce un [MobileServiceUser], che fornisce sia hello [UserId] di hello autenticato l'utente e hello [ MobileServiceAuthenticationToken], come un token web JSON (JWT). È possibile memorizzare questo token nella cache e riutilizzarlo fino alla scadenza. Per ulteriori informazioni, vedere [token di autenticazione di memorizzazione nella cache hello](#caching).

### <a name="caching"></a>Memorizzazione nella cache i token di autenticazione hello
Metodo di accesso toohello chiamata hello in alcuni casi, è possibile evitare dopo l'autenticazione prima hello archiviando i token di autenticazione hello dal provider di hello.  Le applicazioni Windows Store e UWP possono utilizzare [PasswordVault] toocache l'autenticazione corrente token dopo una corretta accesso, come indicato di seguito:

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Hello UserId valore viene archiviato come nome utente della credenziale hello hello e token hello è hello archiviato come hello Password. In Start-up successive, è possibile controllare hello **PasswordVault** per credenziali memorizzate nella cache. Hello seguente esempio Usa credenziali memorizzate nella cache quando vengono trovati e in caso contrario tenta tooauthenticate nuovamente con back-end hello:

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

Quando ci si disconnette un utente, è necessario rimuovere anche credenziale hello archiviata, come indicato di seguito:

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

App Xamarin utilizzano hello [Xamarin.Auth] credenziali dell'archivio toosecurely API in un **Account** oggetto. Per un esempio di utilizzo di queste API, vedere hello [AuthStore.cs] file di codice hello [ContosoMoments foto condivisione esempio](https://github.com/azure-appservice-samples/ContosoMoments).

Quando si utilizza l'autenticazione client gestito, è anche possibile memorizzare nella cache i token di accesso hello ottenuto dal provider, ad esempio Facebook o Twitter. Questo token può essere fornito toorequest un nuovo token di autenticazione dal back-end hello, come segue:

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Notifiche push
Hello negli argomenti seguenti vengono descritte le notifiche Push:

* [Registrarsi per le notifiche push](#register-for-push)
* [Ottenere un SID pacchetto di Windows Store](#package-sid)
* [Registrare modelli multipiattaforma](#register-xplat)

### <a name="register-for-push"></a>Procedura: Registrarsi per le notifiche push
il client di App per dispositivi mobili Hello consente tooregister per le notifiche push con hub di notifica di Azure. Durante la registrazione, ottenere un handle ottenuta dal specifico della piattaforma hello Push Notification Service (PNS). È quindi possibile fornire questo valore insieme a eventuali tag quando si crea una registrazione hello. Hello codice seguente viene registrata l'app di Windows per le notifiche push con hello il servizio di notifica di Windows (WNS):

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

Se si effettua il push tooWNS, quindi è necessario [ottenere un SID del pacchetto di Windows Store](#package-sid).  Per ulteriori informazioni sulle app di Windows, come tooregister per le registrazioni del modello, vedere [Aggiungi push notifiche tooyour app].

Richiesta di tag da client hello non è supportata.  Le richieste di tag vengono eliminate automaticamente dalla registrazione.
Se si desidera tooregister il dispositivo con tag, creare un'API personalizzata che utilizza la registrazione di hello hello API degli hub di notifica tooperform per conto dell'utente.  [Chiamare l'API personalizzata hello](#customapi) anziché hello `RegisterNativeAsync()` metodo.

### <a name="package-sid"></a>Procedura: ottenere un SID pacchetto di Windows Store
Per abilitare le notifiche push nelle app di Windows Store è necessario un SID pacchetto.  tooreceive, il SID pacchetto registrare l'applicazione con hello Windows Store.

tooobtain questo valore:

1. In Esplora soluzioni Visual Studio, progetto di applicazione Windows Store hello pulsante destro del mouse, fare clic su **archivio** > **Associa applicazione a Store hello...** .
2. Nella procedura guidata hello, fare clic su **Avanti**, accedere con l'account Microsoft, digitare un nome per l'app in **riserva nuovo nome applicazione**, quindi fare clic su **riserva**.
3. Dopo la registrazione dell'app hello è il nome dell'app è stata creata, selezionare hello, fare clic su **Avanti**, quindi fare clic su **associare**.
4. Accedi toohello [Windows Dev Center] con l'Account Microsoft. In **le mie app**, fare clic su registrazione dell'app hello è stato creato.
5. Fare clic su **gestione delle App** > **identità App**e quindi scorrere verso il basso toofind il **SID pacchetto**.

Molti utilizzi delle SID pacchetto hello considerano come un URI, nel qual caso è necessario toouse *ms-app: / /* lo schema di hello. Prendere nota della versione di hello del pacchetto di SID formato concatenando il valore come un prefisso.

App Xamarin richiedono alcuni tooregister in grado di codice aggiuntivo toobe un'app in esecuzione su piattaforme Android o iOS hello. Per ulteriori informazioni, vedere l'argomento di hello per la piattaforma:

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Procedura: registrazione delle notifiche multipiattaforma toosend push modelli
modelli tooregister, utilizzare hello `RegisterAsync()` (metodo) con i modelli di hello, come indicato di seguito:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

I modelli devono essere `JObject` tipi e può contenere più modelli di hello seguendo il formato JSON:

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

metodo Hello **RegisterAsync()** accetta inoltre riquadri secondari:

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Tutti i tag vengono eliminati durante la registrazione per motivi di sicurezza. i tag tooadd tooinstallations o modelli in installazioni, vedere [utilizzare i server back-end di hello .NET SDK per App mobili di Azure].

le notifiche toosend utilizzando questi modelli registrati, fare riferimento toohello [API degli hub di notifica].

## <a name="misc"></a>Argomenti vari
### <a name="errors"></a>Procedura: Gestire gli errori
Quando si verifica un errore nel back-end hello, client hello SDK genera un `MobileServiceInvalidOperationException`.  L'esempio seguente viene illustrato come un'eccezione che viene restituita dal back-end hello toohandle:

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

Un altro esempio di gestione delle condizioni di errore è reperibile in hello [Mobile App i file di esempio]. Il [LoggingHandler] riportato di seguito viene fornito un delegato di registrazione gestore toolog hello richieste da toohello di back-end.

### <a name="headers"></a>Procedura: Personalizzare le intestazioni delle richieste
toosupport dello scenario di applicazione specifico, potrebbe essere necessario toocustomize comunicazione con back-end di hello App per dispositivi mobili. Ad esempio, si potrebbe tooadd una richiesta in uscita di tooevery intestazione personalizzata o cambiare anche i codici di stato delle risposte. È possibile utilizzare un oggetto personalizzato [DelegatingHandler], come illustrato nell'esempio seguente hello:

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
