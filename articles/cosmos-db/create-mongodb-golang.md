---
<span data-ttu-id="8b4af-101">titolo: aaa "Azure Cosmos DB: compilare un'applicazione console API MongoDB con Golang e hello portale di Azure | Descrizione di Microsoft Docs": presenta un esempio di codice Golang è possibile utilizzare tooconnect tooand query ai servizi di Azure Cosmos DB: cosmos db autore: manager Durgaprasad Budhwani: jhubbard editor: mimig1</span><span class="sxs-lookup"><span data-stu-id="8b4af-101">title: aaa"Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal | Microsoft Docs" description: Presents a Golang code sample you can use tooconnect tooand query Azure Cosmos DB services: cosmos-db author: Durgaprasad-Budhwani manager: jhubbard editor: mimig1</span></span>

<span data-ttu-id="8b4af-102">ms. Service: ms. topic cosmos db: hero-article ms. date: 07/21/2017 Author: mimig</span><span class="sxs-lookup"><span data-stu-id="8b4af-102">ms.service: cosmos-db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span></span>
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a><span data-ttu-id="8b4af-103">Azure DB Cosmos: Compilare un'applicazione console API MongoDB con Golang e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b4af-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal</span></span>

<span data-ttu-id="8b4af-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8b4af-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8b4af-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="8b4af-106">Questa Guida introduttiva illustra come toouse esistente [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app scritta in [Golang](https://golang.org/) e connetterla tooyour DB Cosmos Azure database, che supporta le connessioni client di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b4af-106">This quick-start demonstrates how toouse an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="8b4af-107">In altre parole, l'applicazione di Golang riconosce solo che viene stabilita la connessione database tooa utilizzando APIs MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b4af-107">In other words, your Golang application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="8b4af-108">È trasparente toohello applicazione hello dati viene archiviato nel database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="8b4af-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b4af-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b4af-109">Prerequisites</span></span>

- <span data-ttu-id="8b4af-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b4af-110">An Azure subscription.</span></span> <span data-ttu-id="8b4af-111">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="8b4af-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="8b4af-112">[Passare](https://golang.org/dl/) e una conoscenza di base di hello [passare](https://golang.org/) language.</span><span class="sxs-lookup"><span data-stu-id="8b4af-112">[Go](https://golang.org/dl/) and a basic knowledge of hello [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="8b4af-113">Un IDE. [Gogland](https://www.jetbrains.com/go/) di Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) di Microsoft o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="8b4af-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="8b4af-114">In questa esercitazione si usa Gogland.</span><span class="sxs-lookup"><span data-stu-id="8b4af-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="8b4af-115">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="8b4af-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="8b4af-116">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="8b4af-116">Clone hello sample application</span></span>

<span data-ttu-id="8b4af-117">Duplicare l'applicazione di esempio hello e installare i pacchetti hello necessario.</span><span class="sxs-lookup"><span data-stu-id="8b4af-117">Clone hello sample application and install hello required packages.</span></span>

1. <span data-ttu-id="8b4af-118">Creare una cartella denominata CosmosDBSample cartella hello GOROOT\src, ovvero C:\Go\ per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8b4af-118">Create a folder named CosmosDBSample inside hello GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="8b4af-119">Eseguire hello comando utilizzando una finestra terminale git, ad esempio l'archivio di git bash tooclone hello esempio nella cartella CosmosDBSample hello seguente.</span><span class="sxs-lookup"><span data-stu-id="8b4af-119">Run hello following command using a git terminal window such as git bash tooclone hello sample repository into hello CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="8b4af-120">Eseguire hello seguente pacchetto mgo hello tooget di comando.</span><span class="sxs-lookup"><span data-stu-id="8b4af-120">Run hello following command tooget hello mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="8b4af-121">Hello [mgo](http://labix.org/mgo) driver (si pronuncia come *mango*) è un [MongoDB](http://www.mongodb.org/) driver per hello [passare language](http://golang.org/) che implementa un RTF e testato selezione di funzionalità in un'API molto semplice seguente idiomi Go standard.</span><span class="sxs-lookup"><span data-stu-id="8b4af-121">hello [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for hello [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="8b4af-122">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="8b4af-122">Update your connection string</span></span>

<span data-ttu-id="8b4af-123">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-123">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="8b4af-124">Fare clic su **introduttiva** in hello dal menu di navigazione a sinistra e quindi fare clic su **altri** sulle stringhe di tooview hello connessione richieste dal hello applicazione Go.</span><span class="sxs-lookup"><span data-stu-id="8b4af-124">Click **Quick start** in hello left navigation menu, and then click **Other** tooview hello connection string information required by hello Go application.</span></span>

2. <span data-ttu-id="8b4af-125">Nel Goglang, aprire il file di main.go hello nella directory GOROOT\CosmosDBSample hello e aggiorna hello seguenti righe di codice utilizzando informazioni della stringa di connessione hello da hello portale di Azure, come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-125">In Goglang, open hello main.go file in hello GOROOT\CosmosDBSample directory and update hello following lines of code using hello connection string information from hello Azure portal as shown in hello following screenshot.</span></span> 

    <span data-ttu-id="8b4af-126">nome del Database Hello è il prefisso hello di hello **Host** valore nel riquadro di stringa di connessione del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-126">hello Database name is hello prefix of hello **Host** value in hello Azure portal connection string pane.</span></span> <span data-ttu-id="8b4af-127">Per l'account di hello illustrato nell'immagine di hello riportata di seguito, il nome di Database hello è golang autobus.</span><span class="sxs-lookup"><span data-stu-id="8b4af-127">For hello account shown in hello image below, hello Database name is golang-coach.</span></span>

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Avvio rapido di riquadro, scheda altro informazioni della stringa di connessione hello che Mostra portale Azure hello](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="8b4af-129">Salvare il file di main.go hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-129">Save hello main.go file.</span></span>

## <a name="review-hello-code"></a><span data-ttu-id="8b4af-130">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="8b4af-130">Review hello code</span></span>

<span data-ttu-id="8b4af-131">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nel file main.go hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-131">Let's make a quick review of what's happening in hello main.go file.</span></span> 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a><span data-ttu-id="8b4af-132">Connessione hello Go app tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b4af-132">Connecting hello Go app tooAzure Cosmos DB</span></span>

<span data-ttu-id="8b4af-133">DB Cosmos Azure supporta hello MongoDB abilitato per SSL.</span><span class="sxs-lookup"><span data-stu-id="8b4af-133">Azure Cosmos DB supports hello SSL-enabled MongoDB.</span></span> <span data-ttu-id="8b4af-134">tooconnect tooan MongoDB abilitato per SSL, è necessario hello toodefine **DialServer** funzionare in [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)e utilizzare di hello [tls. *Connessione* ](http://golang.org/pkg/crypto/tls#Dial) funzione connessione hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="8b4af-134">tooconnect tooan SSL-enabled MongoDB, you need toodefine hello **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of hello [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function tooperform hello connection.</span></span>

<span data-ttu-id="8b4af-135">Hello seguente frammento di codice Golang connette hello Go app con l'API di Azure Cosmos DB MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b4af-135">hello following Golang code snippet connects hello Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="8b4af-136">Hello *DialInfo* classe contiene le opzioni per stabilire una sessione con un cluster di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b4af-136">hello *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="8b4af-137">Hello **mgo. Dial()** metodo viene utilizzato quando è presente alcuna connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="8b4af-137">hello **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="8b4af-138">Per una connessione SSL, hello **mgo. DialWithInfo()** metodo è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="8b4af-138">For an SSL connection, hello **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="8b4af-139">Un'istanza di hello **{} DialWIthInfo** è oggetto di sessione utilizzato toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-139">An instance of hello **DialWIthInfo{}** object is used toocreate hello session object.</span></span> <span data-ttu-id="8b4af-140">Una volta stabilita la sessione hello, è possibile accedere raccolta hello utilizzando hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8b4af-140">Once hello session is established, you can access hello collection by using hello following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="8b4af-141">Creare un documento</span><span class="sxs-lookup"><span data-stu-id="8b4af-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="8b4af-142">Leggere o eseguire query in un documento</span><span class="sxs-lookup"><span data-stu-id="8b4af-142">Query or read a document</span></span>

<span data-ttu-id="8b4af-143">Azure Cosmos DB supporta query avanzate sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="8b4af-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="8b4af-144">Hello codice di esempio seguente viene illustrata una query che è possibile eseguire sui documenti hello nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="8b4af-144">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="8b4af-145">Aggiornare un documento</span><span class="sxs-lookup"><span data-stu-id="8b4af-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="8b4af-146">Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="8b4af-146">Delete a document</span></span>

<span data-ttu-id="8b4af-147">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="8b4af-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a><span data-ttu-id="8b4af-148">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="8b4af-148">Run hello app</span></span>

1. <span data-ttu-id="8b4af-149">In Goglang, assicurarsi che il GOPATH (disponibile in **File**, **impostazioni**, **passare**, **GOPATH**) includono hello percorso nel quale hello gopkg è stato installato, ovvero USERPROFILE\go per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8b4af-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include hello location in which hello gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="8b4af-150">Commento le righe di hello che Elimina documento hello, righe 91 a 96, in modo che è possibile visualizzare il documento hello dopo l'applicazione hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8b4af-150">Comment out hello lines that delete hello document, lines 91-96, so that you can see hello document after running hello app.</span></span>
3. <span data-ttu-id="8b4af-151">In Gogland fare clic su **Run** (Esegui) e quindi su **Run 'Build main.go and run'** (Esegui 'Compila main.go ed esegui').</span><span class="sxs-lookup"><span data-stu-id="8b4af-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="8b4af-152">app Hello termina e viene visualizzata la descrizione hello del documento hello creata [creare un documento](#create-document).</span><span class="sxs-lookup"><span data-stu-id="8b4af-152">hello app finishes and displays hello description of hello document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Visualizzazione output di hello dell'applicazione hello Goglang](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="8b4af-154">Esaminare il documento in Esplora dati</span><span class="sxs-lookup"><span data-stu-id="8b4af-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="8b4af-155">Tornare toohello toosee portale di Azure in Esplora dati del documento.</span><span class="sxs-lookup"><span data-stu-id="8b4af-155">Go back toohello Azure portal toosee your document in Data Explorer.</span></span>

1. <span data-ttu-id="8b4af-156">Fare clic su **Esplora dati (anteprima)** nel menu di navigazione a sinistra, hello espandere **golang autobus**, **pacchetto**, quindi fare clic su **documenti**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-156">Click **Data Explorer (Preview)** in hello left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="8b4af-157">In hello **documenti** scheda, fare clic su hello \_documento hello toodisplay di id nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="8b4af-157">In hello **Documents** tab, click hello \_id toodisplay hello document in hello right pane.</span></span> 

    ![Documento di hello appena creato che mostra Esplora dati](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="8b4af-159">È possibile quindi utilizzare hello documento inline e fare clic su **aggiornamento** toosave è.</span><span class="sxs-lookup"><span data-stu-id="8b4af-159">You can then work with hello document inline and click **Update** toosave it.</span></span> <span data-ttu-id="8b4af-160">È possibile eliminare il documento hello o creare nuovi documenti o query.</span><span class="sxs-lookup"><span data-stu-id="8b4af-160">You can also delete hello document, or create new documents or queries.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="8b4af-161">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="8b4af-161">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="8b4af-162">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="8b4af-162">Clean up resources</span></span>

<span data-ttu-id="8b4af-163">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8b4af-163">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="8b4af-164">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="8b4af-164">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="8b4af-165">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-165">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b4af-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b4af-166">Next steps</span></span>

<span data-ttu-id="8b4af-167">In questa Guida rapida, si è appreso come un account Azure Cosmos DB toocreate ed eseguire un'app Golang usando hello API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b4af-167">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a Golang app using hello API for MongoDB.</span></span> <span data-ttu-id="8b4af-168">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="8b4af-168">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8b4af-169">Importare dati in Azure Cosmos DB per hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="8b4af-169">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)
