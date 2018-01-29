---
title: 'Azure Cosmos DB: API di SQL Introduzione a esercitazione .NET Core | Documenti Microsoft'
description: Un'esercitazione che consente di creare un database online e l'applicazione console c# con Azure Cosmos DB SQL API .NET Core SDK.
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.custom: devcenter
ms.openlocfilehash: 0b19071bf871029b488b26d3f125d08d7d2a2dd4
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-sql-api-and-net-core"></a>Azure Cosmos DB: Guida introduttiva con l'API di SQL e .NET Core
> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Node.js per MongoDB](mongodb-samples.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [C++](sql-api-cpp-get-started.md)
>  
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Introduzione all'API di SQL Azure Cosmos DB introduzione esercitazione .NET Core. Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.

Contenuto dell'esercitazione:

* Creazione e connessione a un account Azure Cosmos DB
* Configurare una soluzione Visual Studio
* Creazione di un database online
* Creare una raccolta
* Creazione di documenti JSON
* Esecuzione di query sulla raccolta
* Sostituzione di un documento
* Eliminazione di un documento
* Eliminazione del database

Non si ha tempo? Nessun problema. La soluzione completa è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started). Per istruzioni rapide, vedere la sezione [Ottenere la soluzione completa](#GetSolution) .

Per compilare un file di Xamarin iOS, Android o form applicazione utilizzando l'API di SQL e .NET Core SDK? vedere [Creare applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB](mobile-apps-with-xamarin.md).

> [!NOTE]
> Azure Cosmos DB .NET Core SDK usato in questa esercitazione non è ancora compatibile con le app della piattaforma UWP (Universal Windows Platform). Per una versione di anteprima di .NET Core SDK che supporta le app della piattaforma UWP, inviare un messaggio di posta elettronica a [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

Ecco come procedere.

## <a name="prerequisites"></a>Prerequisiti

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/). 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [!INCLUDE [cosmos-db-emulator-vs](../../includes/cosmos-db-emulator-vs.md)] 
    * Se si sta lavorando MacOS o Linux, è possibile sviluppare applicazioni di .NET Core dalla riga di comando tramite l'installazione di [.NET Core SDK](https://www.microsoft.com/net/core#macos) per la piattaforma di propria scelta. 
    * Se si lavora in Windows, è possibile sviluppare applicazioni .NET Core dalla riga di comando tramite l'installazione di [.NET Core SDK](https://www.microsoft.com/net/core#windows). 
    * È possibile utilizzare un editor o scaricare [codice di Visual Studio](https://code.visualstudio.com/), che è gratuito e funziona in Windows, Linux e MacOS. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se si ha già un account, è possibile ignorare questo passaggio e passare a [Configurare la soluzione Visual Studio](#SetupVS). Se si utilizza l'emulatore di Azure Cosmos DB, seguire i passaggi in [emulatore di Azure Cosmos DB](local-emulator.md) per configurare l'emulatore e passare direttamente alla [soluzione di Visual Studio del programma di installazione](#SetupVS).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Passaggio 2: Configurare la soluzione di Visual Studio
1. Aprire **Visual Studio 2017** nel computer.
2. Scegliere **Nuovo** dal menu **File** e quindi selezionare **Progetto**.
3. Nella finestra di dialogo **Nuovo progetto** selezionare **Modelli** / **Visual C#** / **.NET Core**/**Applicazione console (.NET Core)**, assegnare il nome **DocumentDBGettingStarted** al progetto e quindi fare clic su **OK**.

   ![Screenshot della finestra Nuovo progetto](./media/sql-api-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **DocumentDBGettingStarted**.
5. Senza uscire dal menu fare clic su **Gestisci pacchetti NuGet**.

   ![Screenshot del menu selezionato con il pulsante destro del mouse per il progetto](./media/sql-api-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. Nella scheda **NuGet** fare clic su **Sfoglia** nella parte superiore della finestra e digitare **azure documentdb** nella casella di ricerca.
7. Nei risultati trovare **Microsoft.Azure.DocumentDB.Core** e fare clic su **Installa**.
   L'ID di pacchetto per la libreria è [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core). Se si fa riferimento a una versione di .NET Framework, ad esempio net461, non supportata da questo pacchetto .NET Core NuGet, usare [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) che supporta tutte le versioni di .NET Framework a partire da .NET Framework 4.5.
8. Quando richiesto, accettare le installazioni del pacchetto NuGet e il contratto di licenza.

L'installazione è riuscita. Ora che il programma di installazione è stata completata, iniziamo a scrivere del codice. Un progetto di codice completo di questa esercitazione è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).

## <a id="Connect"></a>Passaggio 3: Connettersi a un account Azure Cosmos DB
In primo luogo, aggiungere questi riferimenti all'inizio dell'applicazione c#, nel file Program.cs:

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> Per completare questa esercitazione, assicurarsi di aggiungere le dipendenze illustrate sopra.

Aggiungere ora queste due costanti e la variabile *client* sotto la classe pubblica *Program*.

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

Passare quindi al [portale di Azure](https://portal.azure.com) per recuperare l'URI e la chiave primaria. L'URI e la chiave primaria di Azure Cosmos DB sono necessari all'applicazione per conoscere la destinazione della connessione e ad Azure Cosmos DB per considerare attendibile la connessione dell'applicazione.

Nel portale di Azure passare all'account Azure Cosmos DB e quindi fare clic su **Chiavi**.

Copiare l'URI dal portale e incollarlo in `<your endpoint URI>` nel file program.cs. Copiare quindi la CHIAVE PRIMARIA dal portale e incollarla in `<your key>`. Se si usa l'emulatore Azure Cosmos DB, usare `https://localhost:8081` come endpoint e la chiave di autorizzazione ben definita di [Come sviluppare usando l'emulatore Azure Cosmos DB](local-emulator.md). Assicurarsi di rimuovere < e > lasciando le virgolette doppie che racchiudono l'endpoint e la chiave.

![Screenshot del portale di Azure usato nell'esercitazione su NoSQL per creare un'applicazione console C#. Mostra un account Azure Cosmos DB, con l'hub attivo evidenziato, pulsante CHIAVI evidenziato nella pagina account di Azure Cosmos DB e i valori URI, chiave primaria e chiave SECONDARIA evidenziati nella pagina delle chiavi][keys]

Per avviare l'applicazione introduttiva, si creerà una nuova istanza di **DocumentClient**.

Sotto il metodo **Main** aggiungere la nuova attività asincrona denominata **GetStartedDemo** che creerà la nuova istanza di **DocumentClient**.

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

Aggiungere questo codice per eseguire l'attività asincrona dal metodo **Main** . Il **Main** metodo intercetta le eccezioni e li scrive nella console.

```csharp
static void Main(string[] args)
{
        // ADD THIS PART TO YOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key to exit.");
                Console.ReadKey();
        }
```

Premere il pulsante **DocumentDBGettingStarted** per compilare ed eseguire l'applicazione.

Congratulazioni! La connessione a un account Azure Cosmos DB è stata stabilita. Ora è possibile esaminare l'uso delle risorse di Azure Cosmos DB.  

## <a name="step-4-create-a-database"></a>Passaggio 4: Creare un database
Prima di aggiungere il codice per la creazione di un database, aggiungere un metodo helper per la scrittura nella console.

Copiare e incollare il metodo **WriteToConsoleAndPromptToContinue** sotto il metodo **GetStartedDemo**.

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

È possibile creare un [database](sql-api-resources.md#databases) di Azure Cosmos DB usando il metodo [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) della classe **DocumentClient**. Un database è il contenitore logico per l'archiviazione di documenti JSON partizionato nelle raccolte.

Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di creazione del client. Verrà creato un database denominato *FamilyDB*.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.

Congratulazioni! La creazione di un database di Azure Cosmos DB è stata completata.  

## <a id="CreateColl"></a>Passaggio 5: Creare una raccolta
> [!WARNING]
> **CreateDocumentCollectionAsync** crea una nuova raccolta con velocità effettiva riservata con prezzi implicazioni. Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).

È possibile creare una [raccolta](sql-api-resources.md#collections) usando il metodo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) della classe **DocumentClient**. Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.

Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di creazione del database. Verrà creata una raccolta di documenti denominata *FamilyCollection_oa*.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.

Congratulazioni! La creazione di una raccolta di documenti di Azure Cosmos DB è stata completata.  

## <a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON
È possibile creare un [documento](sql-api-resources.md#documents) usando il metodo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) della classe **DocumentClient**. I documenti sono contenuto JSON definito dall'utente (arbitrario). Ora è possibile inserire uno o più documenti. Se sono già disponibili dati da archiviare nel database, è possibile usare lo [strumento di migrazione dei dati](import-data.md)di Azure Cosmos DB.

È necessario creare prima di tutto una classe **Family** che rappresenterà gli oggetti archiviati in Azure Cosmos DB in questo esempio. Verranno create anche le sottoclassi **Parent**, **Child**, **Pet** e **Address** da usare in **Family**. Si noti che i documenti devono avere una proprietà **Id** serializzata come **id** in JSON. Creare queste classi aggiungendo le classi secondarie interne seguenti dopo il metodo **GetStartedDemo** .

Copiare e incollare le classi **Family**, **Parent**, **Child**, **Pet** e **Address** sotto il metodo **WriteToConsoleAndPromptToContinue**.

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key to continue ...");
    Console.ReadKey();
}

// ADD THIS PART TO YOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

Copiare e incollare il metodo **CreateFamilyDocumentIfNotExists** sotto il metodo **CreateDocumentCollectionIfNotExists**.

```csharp
// ADD THIS PART TO YOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

Inserire anche due documenti, relativi rispettivamente alla famiglia Andersen e alla famiglia Wakefield.

Copiare e incollare il codice riportato dopo `// ADD THIS PART TO YOUR CODE` nel metodo **GetStartedDemo** sotto il codice di creazione della raccolta di documenti.

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.

Congratulazioni! La creazione di due documenti di Azure Cosmos DB è stata completata.  

![Diagramma che illustra la relazione gerarchica tra l'account, il database online, la raccolta e i documenti usati nell'esercitazione su NoSQL per creare un'applicazione console C#](./media/sql-api-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB
Azure Cosmos DB supporta [query complesse](sql-api-sql-query.md) sui documenti JSON archiviati in ogni raccolta.  Il codice di esempio seguente mostra diverse query che usano la sintassi SQL di Azure Cosmos DB e LINQ e che possono essere eseguite sui documenti inseriti nel passaggio precedente.

Copiare e incollare il metodo **ExecuteSimpleQuery** sotto il metodo **CreateFamilyDocumentIfNotExists**.

```csharp
// ADD THIS PART TO YOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find the Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute the same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di creazione del secondo documento.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.

Congratulazioni! L'esecuzione di una query in una raccolta di Azure Cosmos DB è stata completata.

Il diagramma seguente illustra il modo in cui la sintassi di query di SQL di Azure Cosmos DB viene chiamata sulla raccolta creata e la stessa logica viene applicata alla query di LINQ.

![Diagramma che illustra l'ambito e il significato della query usata nell'esercitazione su NoSQL per creare un'applicazione console C#](./media/sql-api-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

La parola chiave [FROM](sql-api-sql-query.md#FromClause) è facoltativa nella query perché le query di Azure Cosmos DB sono già limitate a una singola raccolta. Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta. Azure DB Cosmos deduce le famiglie, alla radice o il nome della variabile che è stata selezionata, la raccolta corrente per impostazione predefinita di riferimento.

## <a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON
Azure Cosmos DB supporta la sostituzione di documenti JSON.  

Copiare e incollare il metodo **ReplaceFamilyDocument** sotto il metodo **ExecuteSimpleQuery**.

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di esecuzione della query. Dopo aver sostituito il documento, verrà eseguita di nuovo la stessa query per visualizzare il documento modificato.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.

Congratulazioni! La sostituzione di un documento di Azure Cosmos DB è stata completata.

## <a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON
Azure Cosmos DB supporta l'eliminazione di documenti JSON.  

Copiare e incollare il metodo **DeleteFamilyDocument** sotto il metodo **ReplaceFamilyDocument**.

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di esecuzione della seconda query.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.

Congratulazioni! L'eliminazione di un documento di Azure Cosmos DB è stata completata.

## <a id="DeleteDatabase"></a>Passaggio 10: Eliminare il database
Se si elimina il database creato, verrà rimosso il database e tutte le risorse figlio (raccolte, documenti e così via).

Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di eliminazione del documento per eliminare l'intero database e tutte le risorse figlio.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.

Congratulazioni! L'eliminazione di un database di Azure Cosmos DB è stata completata.

## <a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console C#
Premere il pulsante **DocumentDBGettingStarted** in Visual Studio per compilare l'applicazione in modalità di debug.

Verrà visualizzato l'output dell'app introduttiva nella finestra della console. L'output visualizzerà i risultati delle query aggiunte e dovrà corrispondere al testo di esempio riportato di seguito.

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
Press any key to continue ...
Created Family Andersen.1
Press any key to continue ...
Created Family Wakefield.7
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key to exit.
```

Congratulazioni! L'esercitazione è stata completata ed è stata creata un'applicazione console C# funzionante.

## <a id="GetSolution"></a> Ottenere la soluzione completa per l'esercitazione
Per creare la soluzione GetStarted completa contenente tutti gli esempi riportati in questo articolo, è necessario avere:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).
* Un [account Azure Cosmos DB][create-sql-api-dotnet.md#create-account].
* La soluzione [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) disponibile su GitHub.

Per ripristinare i riferimenti all'API di SQL Azure Cosmos DB SDK per .NET Core in Visual Studio, fare doppio clic su di **GetStarted** soluzione in Esplora soluzioni e quindi fare clic su **abilitare il ripristino del pacchetto NuGet**. Nel file Program.cs aggiornare quindi i valori EndpointUrl e AuthorizationKey come illustrato nell'articolo [Connettersi a un account Azure Cosmos DB](#Connect).

## <a name="next-steps"></a>Passaggi successivi
* Per un'esercitazione su MVC ASP.NET più complessa, vedere [Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB](sql-api-dotnet-application.md).
* Per sviluppare un Xamarin iOS, Android o form applicazione usando l'API di SQL Azure Cosmos DB SDK per .NET Core? vedere [Creare applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB](mobile-apps-with-xamarin.md).
* Per la scalabilità e i test delle prestazioni con Azure Cosmos DB, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).
* Informazioni su come [Monitorare le richieste, l'utilizzo e le risorse di archiviazione di Azure Cosmos DB](monitor-accounts.md).
* Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).
* Per altre informazioni sul modello di programmazione, vedere [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

[create-sql-api-dotnet.md#create-account]: create-sql-api-dotnet.md#create-account
[keys]: media/sql-api-dotnetcore-get-started/nosql-tutorial-keys.png
