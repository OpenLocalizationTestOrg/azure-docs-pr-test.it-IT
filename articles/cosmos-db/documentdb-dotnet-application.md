---
title: 'Esercitazione su ASP.NET MVC per Azure Cosmos DB: sviluppo di un''applicazione Web | Microsoft Docs'
description: "ASP.NET MVC toocreate esercitazione un'applicazione web MVC utilizza Azure Cosmos DB. Si archivieranno documenti JSON e si accederà ai dati da un'app todo ospitata in siti Web di Azure - Esercitazione dettagliata su MVC ASP.NET."
keywords: esercitazione su mvc asp.net, sviluppo di applicazioni web, applicazione web mvc, esercitazione dettagliata su mvc asp net
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight illustrato in modo efficiente, è possibile utilizzare Azure Cosmos DB toostore e query documenti JSON, in questo articolo fornisce una procedura dettagliata end-to-end che mostra come un'app todo tramite Azure Cosmos DB toobuild. attività Hello verranno archiviate come documenti JSON in Azure Cosmos DB.

![Cattura di schermata dell'elenco attività hello applicazione web MVC creato da questa esercitazione - esercitazione ASP NET MVC dettagliate](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Questa procedura dettagliata viene illustrato come toouse hello Azure Cosmos DB servizio toostore e accedere ai dati da un'applicazione web MVC ASP.NET ospitata in Azure. Se si sta cercando un'esercitazione che consente solo di Azure Cosmos DB, e non hello componenti ASP.NET MVC, vedere [compilare un'applicazione console Azure Cosmos DB c#](documentdb-get-started.md).

> [!TIP]
> Questa esercitazione presuppone già una certa esperienza nell'uso di MCV ASP.NET e di Siti Web di Azure. Se si tooASP.NET nuova o hello [strumenti prerequisiti](#_Toc395637760), si consiglia di scaricare il progetto di esempio completo hello da [GitHub] [ GitHub] e seguendo le istruzioni di hello in In questo esempio. Quando l'applicazione viene compilata, è possibile esaminare informazioni dettagliate di toogain questo articolo sul codice hello nel contesto di hello del progetto hello.
> 
> 

## <a name="_Toc395637760"></a>Prerequisiti per questa esercitazione sul database
Prima di seguire le istruzioni di hello in questo articolo, è necessario assicurarsi di aver seguito hello:

* Un account Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 

    OPPURE

    Un'installazione locale di hello [emulatore di Azure Cosmos DB](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Microsoft Azure SDK per .NET per Visual Studio 2017, disponibili tramite hello programma di installazione di Visual Studio.

Tutte le schermate di hello in questo articolo sono state prese utilizzando Microsoft Visual Studio Community 2017. Se il sistema è configurato con una versione diversa, che è possibile che le schermate e le opzioni non corrispondono completamente, ma se si soddisfa hello sopra prerequisiti dovrebbe funzionare questa soluzione.

## <a name="_Toc395637761"></a>Passaggio 1: Creare un account del database di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se è già un account SQL (DocumentDB) per Azure Cosmos DB o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[creare una nuova applicazione MVC ASP.NET](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Verrà ora descritto come toocreate una nuova applicazione MVC ASP.NET da hello interamente progettato. 

## <a name="_Toc395637762"></a>Passaggio 2: Creare una nuova applicazione MVC ASP.NET

1. In Visual Studio, su hello **File** menu, scegliere troppo**New**e quindi fare clic su **progetto**. Hello **nuovo progetto** viene visualizzata la finestra di dialogo.

2. In hello **tipi di progetto** riquadro espandere **modelli**, **Visual c#**, **Web**, quindi selezionare **applicazione Web ASP.NET** .

      ![Cattura di schermata della finestra di dialogo Nuovo progetto hello con tipo di progetto applicazione Web ASP.NET hello evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. In hello **nome** casella, nome del progetto hello hello di tipo. Questa esercitazione viene utilizzato il nome di hello "attività". Se si sceglie un valore diverso da questo toouse, ogni volta che questa esercitazione parla hello dello spazio dei nomi di attività, è necessario tooadjust hello fornito codice esempi toouse qualsiasi denominata dell'applicazione. 
4. Fare clic su **Sfoglia** toonavigate toohello cartella in cui sarebbe come progetto di hello toocreate e quindi fare clic su **OK**.
   
      Hello **nuova applicazione Web ASP.NET** viene visualizzata la finestra di dialogo.
   
    ![Cattura di schermata della finestra di dialogo nuova applicazione Web ASP.NET hello con modello di applicazione MVC hello evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. Nel riquadro Modelli hello selezionare **MVC**.

6. Fare clic su **OK** e consentire a Visual Studio di eseguire le operazioni necessarie per il modello ASP.NET MVC vuoto di scaffolding hello. 

          
7. Una volta Visual Studio ha terminato la creazione di un'applicazione MVC boilerplate hello è un'applicazione ASP.NET vuota che è possibile eseguire in locale.
   
    Si verrà trattata progetto hello in esecuzione in locale perché si è certi che abbiamo hello rilevato tutti ASP.NET "Hello World" dell'applicazione. Segue un' tooadding retta Azure Cosmos DB toothis progetto e la compilazione dell'applicazione.

## <a name="_Toc395637767"></a>Passaggio 3: Aggiungere il progetto applicazione web di Azure Cosmos DB tooyour MVC
Ora che è disponibile la maggior parte dei plumbing di ASP.NET MVC hello necessaria per questa soluzione, iniziamo toohello vero scopo di questa esercitazione, aggiunta di applicazione web di Azure Cosmos DB tooour MVC.

1. Hello Azure Cosmos DB .NET SDK è incluso nel pacchetto e distribuito come pacchetto NuGet. tooget hello pacchetto NuGet in Visual Studio, usare Gestione pacchetti NuGet di hello in Visual Studio facendo clic sul progetto hello in **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**.
   
    ![Cattura di schermata di hello fare doppio clic su Opzioni per il progetto di applicazione web hello in Esplora soluzioni, con Gestione pacchetti NuGet evidenziato.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Hello **Gestisci pacchetti NuGet** viene visualizzata la finestra di dialogo.
2. In hello NuGet **Sfoglia** digitare ***Azure DocumentDB***. (nome del pacchetto hello non è stato aggiornato tooAzure DB Cosmos.)
   
    Dai risultati di hello, installare hello **Microsoft.Azure.DocumentDB da Microsoft** pacchetto. Ciò Scarica e installa il pacchetto di Azure Cosmos DB hello, nonché tutte le dipendenze, ad esempio newtonsoft. JSON. Fare clic su **OK** in hello **anteprima** finestra e **accetto** in hello **dell'accettazione della licenza** finestra toocomplete hello installazione.
   
    ![Cattura di screen della finestra Gestisci pacchetti NuGet hello con hello libreria Client di Microsoft Azure DocumentDB evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      In alternativa è possibile utilizzare il pacchetto di hello tooinstall Console di gestione pacchetti hello. toodo in questo caso, hello **strumenti** menu, fare clic su **Gestione pacchetti NuGet**, quindi fare clic su **Package Manager Console**. Al prompt dei comandi hello, digitare il seguente hello.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Dopo aver installato il pacchetto di hello, la soluzione di Visual Studio dovrebbe essere simile a seguito di hello con due nuovi riferimenti aggiunti, Microsoft.Azure.Documents.Client e newtonsoft. JSON.
   
    ![Cattura screen di due riferimenti hello aggiunti toohello progetto di dati JSON in Esplora soluzioni](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>Passaggio 4: Configurare l'applicazione ASP.NET MVC hello
A questo punto aggiungere modelli, visualizzazioni e controller toothis MVC applicazione hello:

* [Aggiungere un modello](#_Toc395637764).
* [Aggiungere un controller](#_Toc395637765).
* [Aggiungere visualizzazioni](#_Toc395637766).

### <a name="_Toc395637764"></a>Aggiungere un modello di dati JSON
Si inizia creando hello **M** in MVC hello modello. 

1. In **Esplora**, hello rapida **modelli** cartella, fare clic su **Aggiungi**e quindi fare clic su **classe**.
   
      Hello **Aggiungi nuovo elemento** viene visualizzata la finestra di dialogo.
2. Denominare la nuova classe **Item.cs** e fare clic su **Aggiungi**. 
3. In questo nuovo **Item.cs** file, aggiungere ultimo segue hello dopo hello *utilizzando l'istruzione*.
   
        using Newtonsoft.Json;
4. A questo punto sostituire il codice 
   
        public class Item
        {
        }
   
    con hello seguente codice.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Tutti i dati nel database di Azure Cosmos viene trasmessa in transito hello e archiviata come JSON. toocontrol hello modo gli oggetti serializzati o deserializzati dal JSON.NET è possibile utilizzare hello **JsonProperty** attributo come dimostrato nel hello **elemento** classe appena creata. In caso contrario **hanno** toodo questo ma si desidera che le proprietà seguono le convenzioni di denominazione di hello JSON camelCase tooensure. 
   
    Non solo è possibile controllare il formato di hello hello del nome della proprietà quando entra in JSON, ma è possibile rinominare le proprietà .NET completamente come con hello **descrizione** proprietà. 

### <a name="_Toc395637765"></a>Aggiungere un controller
Che si occupa di hello **M**, ora è possibile crearne hello **C** in una classe controller MVC.

1. In **Esplora**, hello rapida **controller** cartella, fare clic su **Aggiungi**e quindi fare clic su **Controller**.
   
    Hello **aggiungere lo scaffolding** viene visualizzata la finestra di dialogo.
2. Selezionare **Controller MVC 5 - Vuoto** e quindi fare clic su **Aggiungi**.
   
    ![Cattura di schermata della hello aggiungere lo scaffolding di finestra di dialogo hello Controller MVC 5 - opzione vuoto evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Assegnare al controller il nome **ItemController.**
   
    ![Cattura di schermata della finestra di dialogo Aggiungi Controller hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Una volta creato il file hello, la soluzione di Visual Studio dovrebbe essere simile seguente hello con nuovo file ItemController.cs hello in **Esplora**. viene inoltre visualizzato Hello Item.cs file creato in precedenza.
   
    ![Cattura di schermata della soluzione di Visual Studio - Esplora soluzioni con file ItemController.cs nuovo hello e Item.cs file evidenziato hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    È possibile chiudere ItemController.cs, si ritornerà tooit in un secondo momento. 

### <a name="_Toc395637766"></a>Aggiungere visualizzazioni
A questo punto, è possibile crearne hello **V** in MVC hello viste:

* [Aggiungere una visualizzazione Indice elemento](#AddItemIndexView).
* [Aggiungere una visualizzazione Nuovo elemento](#AddNewIndexView).
* [Aggiungere una visualizzazione Modifica elemento](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Aggiungere una visualizzazione Indice elemento
1. In **Esplora**, espandere hello **viste** cartella, il pulsante destro del mouse hello vuoto **elemento** cartella in cui verrà creata automaticamente quando si aggiunge hello  **ItemController** in precedenza, fare clic su **Aggiungi**, quindi fare clic su **vista**.
   
    ![Cattura di schermata della finestra Esplora soluzioni con cartella elemento hello creato da Visual Studio con i comandi Aggiungi visualizzazione hello evidenziati](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. In hello **Aggiungi visualizzazione** finestra di dialogo casella, hello seguenti:
   
   * In hello **nome vista** digitare ***indice***.
   * In hello **modello** , quindi selezionare ***elenco***.
   * In hello **classe modello** , quindi selezionare ***elemento (todo. I modelli)***.
   * Nella casella di pagina di layout hello, digitare ***~/Views/Shared/_Layout.cshtml***.
     
   ![Schermata di finestra di dialogo Aggiungi visualizzazione hello cattura di schermata](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Una volta impostati tutti questi valori, fare clic su **Aggiungi** , in modo che venga creata una nuova visualizzazione modello in Visual Studio. Al termine, si aprirà file cshtml hello che è stato creato. È possibile chiudere il file in Visual Studio come si tornerà tooit in un secondo momento.

#### <a name="AddNewIndexView"></a>Aggiungere una visualizzazione Nuovo elemento
Toohow simile è stato creato un **indice dell'elemento** vista, si creerà una nuova visualizzazione per la creazione di nuovi **elementi**.

1. In **Esplora**, hello rapida **elemento** cartella fare nuovamente clic **Aggiungi**e quindi fare clic su **vista**.
2. In hello **Aggiungi visualizzazione** finestra di dialogo casella, hello seguenti:
   
   * In hello **nome vista** digitare ***crea***.
   * In hello **modello** , quindi selezionare ***crea***.
   * In hello **classe modello** , quindi selezionare ***elemento (todo. I modelli)***.
   * Nella casella di pagina di layout hello, digitare ***~/Views/Shared/_Layout.cshtml***.
   * Fare clic su **Aggiungi**.
   
#### <a name="_Toc395888515"></a>Aggiungere una visualizzazione Modifica elemento
Infine, aggiungere una visualizzazione ultima per la modifica di un **elemento** in hello esattamente come in precedenza.

1. In **Esplora**, hello rapida **elemento** cartella fare nuovamente clic **Aggiungi**e quindi fare clic su **vista**.
2. In hello **Aggiungi visualizzazione** finestra di dialogo casella, hello seguenti:
   
   * In hello **nome vista** digitare ***modifica***.
   * In hello **modello** , quindi selezionare ***modifica***.
   * In hello **classe modello** , quindi selezionare ***elemento (todo. I modelli)***.
   * Nella casella di pagina di layout hello, digitare ***~/Views/Shared/_Layout.cshtml***.
   * Fare clic su **Aggiungi**.

Al termine, chiudere tutti i documenti cshtml hello in Visual Studio come abbiamo restituiranno viste toothese in un secondo momento.

## <a name="_Toc395637769"></a>Passaggio 5: Completamento dell'aggiunta di Azure Cosmos DB
Ora che stuff MVC standard hello viene preso in considerazione, passiamo codice hello tooadding per Azure Cosmos DB. 

In questa sezione verrà aggiunto codice che segue toohandle hello:

* [Creare un elenco di elementi incompleti](#_Toc395637770).
* [Aggiungere elementi](#_Toc395637771).
* [Modificare elementi](#_Toc395637772).

### <a name="_Toc395637770"></a>Elenco di elementi incompleti in un'applicazione Web MVC
Hello prima cosa, toodo qui è aggiungere una classe che contiene hello logica tooconnect tooand utilizzo di tutti i database di Azure Cosmos. Per questa esercitazione si sarà incapsulare tutti questa logica in classe repository tooa chiamato DocumentDBRepository. 

1. In **Esplora**destro del mouse sul progetto hello, fare clic su **Aggiungi**, quindi fare clic su **classe**. Nome nuova classe hello **DocumentDBRepository** e fare clic su **Aggiungi**.
2. In hello appena creato **DocumentDBRepository** classe e aggiungere il seguente hello *utilizzando istruzioni* sopra hello *dello spazio dei nomi* dichiarazione
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    A questo punto sostituire il codice 
   
        public class DocumentDBRepository
        {
        }
   
    con hello seguente codice.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. Si desidera leggere alcuni valori dalla configurazione, quindi aprire hello **Web. config** file dell'applicazione e aggiungere hello seguenti righe di sotto hello `<AppSettings>` sezione.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Aggiornare i valori hello per *endpoint* e *authKey* utilizzando il pannello chiavi hello di hello portale di Azure. Utilizzare hello **URI** dal Pannello di chiavi hello come valore di hello dell'impostazione di endpoint hello e utilizzare hello **chiave primaria**, o **chiave SECONDARIA** dal Pannello di chiavi hello come valore di hello di hello impostazione authKey.

    Che farà associando repository Azure Cosmos DB hello, ora si aggiungere la logica dell'applicazione.

1. Hello in primo luogo è necessario toodo in grado di toobe con un'applicazione elenco da fare è elementi incompleto di toodisplay hello.  Copiare e incollare hello seguente frammento di codice in un punto qualsiasi all'interno di hello **DocumentDBRepository** classe.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Aprire hello **ItemController** è aggiunto in precedenza e aggiungere il seguente hello *utilizzando istruzioni* sopra dichiarazione dello spazio dei nomi hello.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Se il progetto non è denominato "todo", è necessario tooupdate utilizzando "l'attività. Modelli". nome di hello tooreflect del progetto.
   
    A questo punto sostituire il codice
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    con hello seguente codice.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Aprire **Global.asax.cs** e aggiungere hello seguente riga toohello **Application_Start** (metodo) 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

A questo punto la soluzione deve essere in grado di toobuild senza errori.

Se si esegue ora l'applicazione hello, si passa toohello **HomeController** hello e **indice** visualizzazione di tale controller. Questo è il comportamento predefinito hello per il progetto di modello MVC hello che è stato scelto all'avvio di hello ma non vogliamo che! È necessario modificare hello routing su questo tooalter applicazione MVC questo comportamento.

Aprire ***App\_Start\RouteConfig.cs*** e individuare una riga hello inizia con "valori predefiniti:" e modificarlo hello tooresemble seguente.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

A questo punto indica ASP.NET MVC che se non è stato specificato un valore in hello URL toocontrol hello comportamento di routing che invece di **Home**, utilizzare **elemento** come controller di hello e utente **indice** come visualizzazione hello.

Ora se si esegue un'applicazione hello, chiama nel **ItemController** che chiamare nella classe repository toohello e utilizzare hello GetItems metodo tooreturn tutti hello elementi incompleti toohello **viste** \\ **Elemento**\\**indice** visualizzazione. 

Se compilato ed eseguito ora, il progetto avrà un aspetto simile al seguente.    

![Cattura di schermata dell'applicazione web elenco attività hello creata da questa esercitazione database](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Aggiungere elementi
Consente di inserire si alcuni elementi al database in modo che abbiamo più di un toolook di griglia vuota in.

Aggiungere codice troppo Azure Cosmos DBRepository ItemController toopersist hello record nel database di Azure Cosmos.

1. Aggiungere hello seguente metodo tooyour **DocumentDBRepository** classe.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   È sufficiente, questo metodo accetta un oggetto passato tooit e rende persistente nel database di Azure Cosmos.
2. Aprire il file ItemController.cs hello e aggiungere hello seguente frammento di codice all'interno di classe hello. Si tratta come ASP.NET MVC sa quale toodo per hello **crea** azione. In questo caso il rendering solo hello associati Create.cshtml vista creata in precedenza.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    È ora necessario codice in questo controller che accetterà invio hello da hello **crea** visualizzazione.
3. Aggiungere hello successivo blocco di codice toohello classe ItemController.cs che indica quali toodo con un POST di form per questo controller di ASP.NET MVC.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Questo codice chiama in toohello DocumentDBRepository e utilizza hello CreateItemAsync metodo toopersist hello nuovo todo toohello database degli elementi. 
   
    **Nota sulla sicurezza**: hello **ValidateAntiForgeryToken** attributo viene utilizzato qui toohelp proteggere l'applicazione contro attacchi di cross-site request forgery. È più tooit rispetto all'aggiunta solo di questo attributo, le visualizzazioni necessario toowork con questo token antifalsificazione anche. Per ulteriori informazioni sul soggetto hello ed esempi di come tooimplement questo correttamente, vedere [impedendo Cross-Site Request Forgery][Preventing Cross-Site Request Forgery]. nel codice sorgente Hello [GitHub] [ GitHub] dispone di implementazione completa di hello.
   
    **Nota sulla sicurezza**: Utilizziamo inoltre hello **associare** attributo toohelp parametro di metodo hello proteggersi da attacchi di registrazione eccessiva. Per altre informazioni dettagliate, vedere [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] (Operazioni CRUD di base in MVC ASP.NET).

Questa operazione conclude hello codice necessario tooadd nuovi elementi tooour database.

### <a name="_Toc395637772"></a>Modificare elementi
C'è una cosa ultimo per noi toodo, ovvero tooadd hello possibilità tooedit **elementi** nel database di hello e toomark come completato. Hello visualizzazione per la modifica è già stato aggiunto il progetto toohello, pertanto è sufficiente tooadd alcune code tooour controller e toohello **DocumentDBRepository** classe nuovamente.

1. Aggiungere hello seguente toohello **DocumentDBRepository** classe.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    primo di questi metodi, Hello **GetItem** recupera un elemento dal database di Azure Cosmos passato toohello back- **ItemController** e quindi su toohello **modifica** visualizzazione.
   
    Hello secondo dei metodi di hello è stato appena aggiunto sostituisce hello **documento** nel database di Azure Cosmos con versione di hello di hello **documento** passati da hello **ItemController**.
2. Aggiungere hello seguente toohello **ItemController** classe.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    Hello primo metodo gestisca hello Http GET che si verifica quando si fa clic sull'utente hello nella hello **modifica** collegamento da hello **indice** visualizzazione. Questo metodo recupera una [ **documento** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) dal database di Azure Cosmos e lo passa a toohello **modifica** visualizzazione.
   
    Hello **modifica** vista eseguirà quindi toohello un Http POST **IndexController**. 
   
    secondo metodo Hello abbiamo aggiunto handle passando hello aggiornato oggetto tooAzure DB Cosmos toobe persistenti nel database di hello.

Questo è tutto, ovvero tutto il necessario toorun l'applicazione, elenco incompleto **elementi**, aggiungere nuovi **elementi**e modificare **elementi**.

## <a name="_Toc395637773"></a>Passaggio 6: Eseguire un'applicazione hello in locale
nel computer locale, un'applicazione hello tootest hello seguenti:

1. In un'applicazione hello toobuild Visual Studio in modalità di debug, premere F5. Deve compilare un'applicazione hello e avviare un browser con una pagina di griglia vuota hello che abbiamo visto prima:
   
    ![Cattura di schermata dell'applicazione web elenco attività hello creata da questa esercitazione database](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Fare clic su hello **Crea nuovo** collegamento e aggiungere i valori toohello **nome** e **descrizione** campi. Lasciare hello **completato** casella di controllo è deselezionata in caso contrario hello nuovo **elemento** verranno aggiunti in uno stato completato e non verrà visualizzato nell'elenco iniziale hello.
   
    ![Cattura di schermata della visualizzazione di creazione di hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Fare clic su **crea** e si è reindirizzato toohello Indietro **indice** Vista e **elemento** viene visualizzato nell'elenco di hello.
   
    ![Cattura di schermata della visualizzazione dell'indice hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    È gratuito tooadd alcune ulteriori **elementi** tooyour elenco di attività.
    
4. Fare clic su **modifica** tooan Avanti **elemento** in elenco hello e si provengono toohello **modifica** vista in cui è possibile aggiornare le proprietà dell'oggetto, tra cui hello  **Completamento** flag. Se si contrassegna hello **completa** flag e fare clic su **salvare**, hello **elemento** viene rimosso dall'elenco di hello di attività non completate.
   
    ![Cattura di schermata della visualizzazione dell'indice con hello completato casella selezionata hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Dopo aver verificato app hello, premere Ctrl + F5 toostop Debug applicazione hello. Si è pronti toodeploy!

## <a name="_Toc395637774"></a>Passaggio 7: Distribuire tooAzure applicazione hello servizio App 
Dopo aver creato un'applicazione hello completo funzioni correttamente con Azure Cosmos DB verrà toodeploy questo tooAzure app web del servizio App.  

1. toopublish tutti questa applicazione è necessario toodo è destro del mouse sul progetto hello in **Esplora** e fare clic su **pubblica**.
   
    ![Cattura di schermata di hello opzione pubblica in Esplora soluzioni](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. In hello **pubblica** la finestra di dialogo, fare clic su **servizio App di Microsoft Azure**, quindi selezionare **Crea nuovo** toocreate un servizio App profilo oppure fare clic su **selezionare Esistente** toouse un profilo esistente.

    ![Finestra di dialogo Pubblica in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Se si dispone di un profilo del Servizio app di Azure esistente, immettere il nome della sottoscrizione. Hello utilizzare **vista** filtrare toosort dal gruppo di risorse o tipo di risorsa, quindi selezionare il servizio App di Azure. 
   
    ![Finestra di dialogo del servizio app in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. Fare clic su un nuovo profilo di servizio App di Azure, toocreate **Crea nuovo** in hello **pubblica** la finestra di dialogo. In hello **Crea servizio App** finestra di dialogo, immettere il nome dell'App Web e sottoscrizione appropriata, gruppo di risorse e piano di servizio App, quindi fare clic su **crea**.

    ![Finestra di dialogo Crea servizio app in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

Dopo alcuni secondi, Visual Studio completerà la pubblicazione dell'applicazione Web e avvierà un browser in cui sarà possibile ammirare il proprio lavoro in esecuzione in Azure.



## <a name="_Toc395637775"></a>Passaggi successivi
Congratulazioni. Appena compilato ASP.NET MVC prima dell'applicazione web tramite Azure Cosmos DB e pubblicarlo tooAzure. codice sorgente per l'applicazione hello completa, inclusi i dettagli di hello Hello ed eliminare funzionalità non incluse in questa esercitazione può essere scaricato o clonato [GitHub][GitHub]. Pertanto se si desidera aggiungere app tooyour, selezionare codice hello e aggiungerlo toothis app.

applicazione tooyour tooadd funzionalità aggiuntive revisione hello API disponibili in hello [libreria .NET di Azure Cosmos DB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) e si ritiene che libera toocontribute toohello libreria .NET di Azure Cosmos DB su [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
