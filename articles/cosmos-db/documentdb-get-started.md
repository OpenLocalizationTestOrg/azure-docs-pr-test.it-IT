---
title: 'Azure Cosmos DB: Esercitazione introduttiva per l''API DocumentDB | Microsoft Docs'
description: Un'esercitazione che consente di creare un database online e l'applicazione console c# utilizzando hello API DocumentDB.
keywords: esercitazione su nosql, database online, applicazione console C#
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB: Esercitazione introduttiva per l'API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js per MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Benvenuto toohello API DocumentDB di Azure Cosmos DB esercitazione introduttiva! Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.

Tratteremo questo argomento:

* Creazione e connessione account Azure Cosmos DB tooan
* Configurare una soluzione Visual Studio
* Creazione di un database online
* Creare una raccolta
* Creazione di documenti JSON
* Esecuzione di query hello raccolta
* Sostituzione di un documento
* Eliminazione di un documento
* L'eliminazione di database hello

Non si ha tempo? Nessun problema. la soluzione completa di Hello è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Passare toohello [ottenere hello completo NoSQL soluzione di esercitazione sezione](#GetSolution) per istruzioni rapide.

Successivamente, per utilizzare hello pulsanti di voto hello sopra o sotto di questo toogive pagina ci commenti e suggerimenti. Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti.

Ecco come procedere.

## <a name="prerequisites"></a>Prerequisiti
Assicurarsi di avere hello segue:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/). 
    * In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[soluzione di Visual Studio del programma di installazione](#SetupVS). Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[soluzione di Visual Studio del programma di installazione](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Passaggio 2: Configurare la soluzione di Visual Studio
1. Aprire **Visual Studio 2017** nel computer.
2. In hello **File** dal menu **New**, quindi scegliere **progetto**.
3. In hello **nuovo progetto** finestra di dialogo Seleziona **modelli** / **Visual c#** / **applicazione Console**, nome il progetto e quindi fare clic su **OK**.
   ![Cattura di schermata della finestra Nuovo progetto hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. In hello **Esplora**, fare clic con il pulsante destro sulla nuova applicazione console, ovvero in una soluzione di Visual Studio, e quindi fare clic su **Gestisci pacchetti NuGet...**
    
    ![Cattura di schermata del diritto hello Menu selezionato per hello progetto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. In hello **Nuget** scheda, fare clic su **Sfoglia**e il tipo **azure documentdb** nella casella di ricerca hello.
6. All'interno dei risultati di hello, trovare **Microsoft.Azure.DocumentDB** e fare clic su **installare**.
   ID del pacchetto per la libreria Client dell'API Azure Cosmos DB DocumentDB hello Hello è [libreria Client di Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Cattura di schermata di hello Nuget Menu per la ricerca di Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    Se viene visualizzato un messaggio i esaminato soluzione toohello modifiche, fare clic su **OK**. Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.

L'installazione è riuscita. Ora che è stata completata l'installazione di hello, iniziamo a scrivere del codice. Un progetto di codice completo di questa esercitazione è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).

## <a id="Connect"></a>Passaggio 3: Connettere l'account di Azure Cosmos DB tooan
In primo luogo, aggiungere questi riferimenti inizio toohello dell'applicazione c#, nel file Program.cs hello:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> Nell'esercitazione di hello toocomplete ordine, accertarsi di aggiungere le dipendenze di hello precedente.
> 
> 

Aggiungere ora queste due costanti e la variabile *client* sotto la classe pubblica *Program*.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

Successivamente, head nuovamente toohello [portale Azure](https://portal.azure.com) tooretrieve l'URL dell'endpoint e la chiave primaria. URL dell'endpoint Hello e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.

In hello portale di Azure, passare tooyour Azure Cosmos DB account e quindi fare clic su **chiavi**.

Copiare hello URI dal portale di hello e incollarlo in `<your endpoint URL>` nel file program.cs hello. Quindi copia hello chiave primaria dal portale hello e incollarlo in `<your primary key>`.

![Cattura di schermata del portale di Azure utilizzato da hello NoSQL esercitazione toocreate un'applicazione console c# hello. Viene illustrato un database di Azure Cosmos account, con l'hub attivo hello evidenziato, hello pulsante CHIAVI evidenziato nel Pannello di account Azure Cosmos DB hello e valori URI, la chiave primaria e SECONDARIA hello evidenziato nella hello pannello chiavi][keys]

Successivamente, si prenderà innanzitutto un'applicazione hello creando una nuova istanza di hello **DocumentClient**.

Di sotto di hello **Main** metodo, aggiungere la nuova attività asincrona chiamata **GetStartedDemo**, che creerà il nuovo **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Aggiungere l'esempio di codice seguente hello toorun l'attività asincrona dal **Main** metodo. Hello **Main** metodo intercettare le eccezioni e scriverli toohello console.

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
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
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

Premere **F5** toorun l'applicazione. output della finestra della console Hello Visualizza messaggio hello `End of demo, press any key tooexit.` per confermare che è stata effettuata la connessione hello.  È quindi possibile chiudere la finestra di console hello. 

Congratulazioni. È una connessione account Azure Cosmos DB tooan, Ora esaminiamo un utilizzo delle risorse di Azure Cosmos DB.  

## <a name="step-4-create-a-database"></a>Passaggio 4: Creare un database
Prima di aggiungere codice hello per la creazione di un database, aggiungere un metodo di supporto per la scrittura di toohello console.

Copiare e incollare hello **WriteToConsoleAndPromptToContinue** metodo dopo hello **GetStartedDemo** metodo.

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Il database di Azure Cosmos [database](documentdb-resources.md#databases) possono essere create usando hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metodo hello **DocumentClient** classe. Un database è contenitore logico di hello di archiviazione di documenti JSON partizionato nelle raccolte.

Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione di client hello. Verrà creato un database denominato *FamilyDB*.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Premere **F5** toorun l'applicazione.

Congratulazioni. La creazione di un database di Azure Cosmos DB è stata completata.  

## <a id="CreateColl"></a>Passaggio 5: Creare una raccolta
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi. Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Oggetto [raccolta](documentdb-resources.md#collections) possono essere create usando hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metodo hello **DocumentClient** classe. Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.

Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione del database hello. Verrà creata una raccolta di documenti denominata *FamilyCollection*.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Premere **F5** toorun l'applicazione.

Congratulazioni. La creazione di una raccolta di documenti di Azure Cosmos DB è stata completata.  

## <a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON
Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metodo hello **DocumentClient** classe. I documenti sono contenuto JSON definito dall'utente (arbitrario). Ora è possibile inserire uno o più documenti. Se si dispongono già di dati desiderato toostore nel database, è possibile utilizzare hello Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md) dati hello tooimport in un database.

Innanzitutto, è necessario toocreate un **famiglia** classe che rappresenta gli oggetti archiviati all'interno di Azure Cosmos DB in questo esempio. Verranno create anche le sottoclassi **Parent**, **Child**, **Pet** e **Address** da usare in **Family**. Si noti che i documenti devono avere una proprietà **Id** serializzata come **id** in JSON. Creare queste classi aggiungendo le seguenti classi secondario interne dopo hello hello **GetStartedDemo** metodo.

Copiare e incollare hello **famiglia**, **padre**, **figlio**, **Pet**, e **indirizzo** classi dopo hello **WriteToConsoleAndPromptToContinue** metodo.

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
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

Copiare e incollare hello **CreateFamilyDocumentIfNotExists** metodo sotto il **indirizzo** classe.

    // ADD THIS PART tooYOUR CODE
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

Inserire due documenti, uno per hello Andersen famiglia e hello Wakefield famiglia.

Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione della raccolta documenti di hello.

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

Premere **F5** toorun l'applicazione.

Congratulazioni. La creazione di due documenti di Azure Cosmos DB è stata completata.  

![Diagramma che illustra relazione gerarchica di hello tra account hello, database online hello, raccolta hello e documenti hello utilizzato dai hello NoSQL esercitazione toocreate un'applicazione console c#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB
Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.  Hello codice di esempio seguente vengono illustrate diverse query - utilizzando entrambi SQL di Azure Cosmos DB sintassi, nonché LINQ - che è possibile eseguire hello è inseriti nel passaggio precedente hello documenti.

Copiare e incollare hello **ExecuteSimpleQuery** metodo dopo il **CreateFamilyDocumentIfNotExists** metodo.

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione di documenti secondo hello.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Premere **F5** toorun l'applicazione.

Congratulazioni. L'esecuzione di una query in una raccolta di Azure Cosmos DB è stata completata.

Hello diagramma seguente illustra come query di database SQL di Azure Cosmos hello sintassi viene chiamata insieme hello creata e hello stessa logica si applica anche query con LINQ toohello.

![Diagramma che illustra ambito hello e il significato della query hello utilizzato da hello NoSQL esercitazione toocreate un'applicazione console c#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Hello [FROM](documentdb-sql-query.md#FromClause) parola chiave è facoltativa in query hello perché le query di database di Azure Cosmos sono già tooa con ambito singola raccolta. Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta. Azure DB Cosmos dedurrà famiglie, alla radice o il nome di variabile hello scelto, raccolta corrente hello di riferimento per impostazione predefinita.

## <a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON
Azure Cosmos DB supporta la sostituzione di documenti JSON.  

Copiare e incollare hello **ReplaceFamilyDocument** metodo dopo il **ExecuteSimpleQuery** metodo.

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo l'esecuzione di query hello, alla fine di hello del metodo hello. Dopo la sostituzione del documento hello, verrà eseguito hello stessa query nuovamente tooview hello modificato documento.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Premere **F5** toorun l'applicazione.

Congratulazioni. La sostituzione di un documento di Azure Cosmos DB è stata completata.

## <a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON
Azure Cosmos DB supporta l'eliminazione di documenti JSON.  

Copiare e incollare hello **DeleteFamilyDocument** metodo dopo il **ReplaceFamilyDocument** metodo.

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo hello seconda esecuzione della query, alla fine di hello del metodo hello.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Premere **F5** toorun l'applicazione.

Congratulazioni. L'eliminazione di un documento di Azure Cosmos DB è stata completata.

## <a id="DeleteDatabase"></a>Passaggio 10: Eliminare database hello
L'eliminazione hello creata database rimuoverà database hello e tutte le risorse di elementi figlio (raccolte, documenti e così via).

Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo documento hello eliminare toodelete hello intero database e tutte le risorse di elementi figlio.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Premere **F5** toorun l'applicazione.

Congratulazioni. L'eliminazione di un database di Azure Cosmos DB è stata completata.

## <a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console C#
In un'applicazione hello toobuild Visual Studio in modalità di debug, premere F5.

Si dovrebbe vedere l'output di hello dell'app get avviata in una finestra della console. output di Hello saranno visualizzati i risultati di hello di hello query è aggiunto e deve corrispondere il testo di esempio hello riportato di seguito.

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

Congratulazioni. È stata completata l'esercitazione hello e dispone di un'applicazione di console lavoro c#!

## <a id="GetSolution"></a>Ottenere una soluzione di esercitazione completa hello
Se si non ho avuto tempo hello toocomplete i passaggi in questa esercitazione, oppure solo gli esempi di codice hello di desidera toodownload, è possibile ottenere dalla [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

soluzione di GetStarted toobuild hello, sarà necessario seguente hello:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).
* Un [account Azure Cosmos DB][cosmos-db-create-account].
* Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) soluzione disponibile su GitHub.

toorestore hello riferimenti toohello SDK .NET di Azure Cosmos DB in Visual Studio, fare doppio clic su hello **GetStarted** soluzione in Esplora soluzioni e quindi fare clic su **abilitare il ripristino del pacchetto NuGet**. Quindi, nel file app. config hello, aggiornare i valori EndpointUrl e AuthorizationKey hello come descritto in [connettere account Azure Cosmos DB tooan](#Connect).

Per completare la procedura, è sufficiente procedere alla compilazione.


## <a name="next-steps"></a>Passaggi successivi
* Per un'esercitazione su MVC ASP.NET più complessa, vedere [Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-dotnet-application.md).
* Desidera tooperform scala e test delle prestazioni con Azure Cosmos DB? vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).
* Informazioni su come troppo[controlla le richieste, utilizzo e archiviazione di Azure Cosmos DB](monitor-accounts.md).
* Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).
* toolearn ulteriori informazioni su Azure Cosmos DB, vedere [benvenuto tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
