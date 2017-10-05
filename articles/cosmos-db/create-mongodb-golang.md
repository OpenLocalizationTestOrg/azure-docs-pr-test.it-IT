---
title: 'Azure Cosmos DB: creare un''app console per le API MongoDB con Golang e il portale di Azure | Microsoft Docs'
description: Presenta un esempio di codice Golang utilizzabile per connettersi ed eseguire query in Azure Cosmos DB
services: cosmos-db
author: Durgaprasad-Budhwani
manager: jhubbard
editor: mimig1
ms.service: cosmos-db
ms.topic: hero-article
ms.date: 07/21/2017
ms.author: mimig
ms.openlocfilehash: 9461a5d86b321fd02167379ba8751d44a861ebc2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-the-azure-portal"></a><span data-ttu-id="da76b-103">Azure Cosmos DB: creare un'app console per le API MongoDB con Golang e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="da76b-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal</span></span>

<span data-ttu-id="da76b-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da76b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="da76b-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave/valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="da76b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="da76b-106">Questa guida introduttiva illustra come usare un'app [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) esistente scritta in [Golang](https://golang.org/) e connetterla al database Azure Cosmos DB, che supporta connessioni client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="da76b-106">This quick-start demonstrates how to use an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it to your Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="da76b-107">In altri termini, l'applicazione Golang rileva solo la connessione a un database con API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="da76b-107">In other words, your Golang application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="da76b-108">Il fatto che i dati siano archiviati in Azure Cosmos DB è trasparente per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="da76b-108">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da76b-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="da76b-109">Prerequisites</span></span>

- <span data-ttu-id="da76b-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="da76b-110">An Azure subscription.</span></span> <span data-ttu-id="da76b-111">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="da76b-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="da76b-112">[Go](https://golang.org/dl/) e una conoscenza di base del linguaggio [Go](https://golang.org/).</span><span class="sxs-lookup"><span data-stu-id="da76b-112">[Go](https://golang.org/dl/) and a basic knowledge of the [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="da76b-113">Un IDE. [Gogland](https://www.jetbrains.com/go/) di Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) di Microsoft o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="da76b-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="da76b-114">In questa esercitazione si usa Gogland.</span><span class="sxs-lookup"><span data-stu-id="da76b-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="da76b-115">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="da76b-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="da76b-116">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="da76b-116">Clone the sample application</span></span>

<span data-ttu-id="da76b-117">Clonare l'applicazione di esempio e installare i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="da76b-117">Clone the sample application and install the required packages.</span></span>

1. <span data-ttu-id="da76b-118">Creare una cartella denominata CosmosDBSample all'interno della cartella GOROOT\src, che per impostazione predefinita è C:\Go\.</span><span class="sxs-lookup"><span data-stu-id="da76b-118">Create a folder named CosmosDBSample inside the GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="da76b-119">Eseguire questo comando usando una finestra del terminale git, ad esempio git bash, per clonare il repository di esempio nella cartella CosmosDBSample.</span><span class="sxs-lookup"><span data-stu-id="da76b-119">Run the following command using a git terminal window such as git bash to clone the sample repository into the CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="da76b-120">Eseguire questo comando per ottenere il pacchetto mgo.</span><span class="sxs-lookup"><span data-stu-id="da76b-120">Run the following command to get the mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="da76b-121">Il driver [mgo](http://labix.org/mgo) (pronunciato *mango*) è un driver [MongoDB](http://www.mongodb.org/) per il [linguaggio Go](http://golang.org/) che implementa una selezione estesa e ben collaudata di funzionalità in un'API molto semplice basata sui termini Go standard.</span><span class="sxs-lookup"><span data-stu-id="da76b-121">The [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for the [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="da76b-122">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="da76b-122">Update your connection string</span></span>

<span data-ttu-id="da76b-123">Tornare ora al portale di Azure per recuperare le informazioni sulla stringa di connessione e copiarle nell'app.</span><span class="sxs-lookup"><span data-stu-id="da76b-123">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="da76b-124">Fare clic su **Avvio rapido** nel menu di spostamento a sinistra e quindi su **Altri** per visualizzare le informazioni relative alla stringa di connessione necessarie per l'applicazione Go.</span><span class="sxs-lookup"><span data-stu-id="da76b-124">Click **Quick start** in the left navigation menu, and then click **Other** to view the connection string information required by the Go application.</span></span>

2. <span data-ttu-id="da76b-125">In Gogland aprire il file main.go nella directory GOROOT\CosmosDBSample e aggiornare le righe di codice seguenti usando le informazioni relative alla stringa di connessione del portale di Azure illustrate nello screenshot riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="da76b-125">In Goglang, open the main.go file in the GOROOT\CosmosDBSample directory and update the following lines of code using the connection string information from the Azure portal as shown in the following screenshot.</span></span> 

    <span data-ttu-id="da76b-126">Il nome del database è il prefisso del valore **Host** nel riquadro relativo alla stringa di connessione del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="da76b-126">The Database name is the prefix of the **Host** value in the Azure portal connection string pane.</span></span> <span data-ttu-id="da76b-127">Per l'account riportato nell'immagine seguente, il nome del database è golang-coach.</span><span class="sxs-lookup"><span data-stu-id="da76b-127">For the account shown in the image below, the Database name is golang-coach.</span></span>

    ```go
    Database: "The prefix of the Host value in the Azure portal",
    Username: "The Username in the Azure portal",
    Password: "The Password in the Azure portal",
    ```

    ![Scheda Altri del riquadro Avvio rapido nel portale di Azure con le informazioni relative alla stringa di connessione](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="da76b-129">Salvare il file main.go.</span><span class="sxs-lookup"><span data-stu-id="da76b-129">Save the main.go file.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="da76b-130">Esaminare il codice</span><span class="sxs-lookup"><span data-stu-id="da76b-130">Review the code</span></span>

<span data-ttu-id="da76b-131">Di seguito è riportata una breve panoramica delle operazioni eseguite nel file main.go.</span><span class="sxs-lookup"><span data-stu-id="da76b-131">Let's make a quick review of what's happening in the main.go file.</span></span> 

### <a name="connecting-the-go-app-to-azure-cosmos-db"></a><span data-ttu-id="da76b-132">Connessione dell'app Go ad Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="da76b-132">Connecting the Go app to Azure Cosmos DB</span></span>

<span data-ttu-id="da76b-133">Azure Cosmos DB supporta le istanze di MongoDB abilitate per SSL.</span><span class="sxs-lookup"><span data-stu-id="da76b-133">Azure Cosmos DB supports the SSL-enabled MongoDB.</span></span> <span data-ttu-id="da76b-134">Per connettersi a un'istanza di MongoDB abilitata per SSL, è necessario definire la funzione **DialServer** in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo) e usare la funzione [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) per eseguire la connessione.</span><span class="sxs-lookup"><span data-stu-id="da76b-134">To connect to an SSL-enabled MongoDB, you need to define the **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of the [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function to perform the connection.</span></span>

<span data-ttu-id="da76b-135">Il frammento di codice Golang seguente connette l'app Go con l'API MongoDB di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="da76b-135">The following Golang code snippet connects the Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="da76b-136">La classe *DialInfo* contiene opzioni per stabilire una sessione con un cluster MongoDB.</span><span class="sxs-lookup"><span data-stu-id="da76b-136">The *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

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
// to our Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect to mongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes the session safety mode.
// If the safe parameter is nil, the session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. The unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="da76b-137">Il metodo **mgo.Dial()** viene usato quando non è disponibile una connessione SSL.</span><span class="sxs-lookup"><span data-stu-id="da76b-137">The **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="da76b-138">Per una connessione SSL è necessario il metodo **mgo.DialWithInfo()**.</span><span class="sxs-lookup"><span data-stu-id="da76b-138">For an SSL connection, the **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="da76b-139">Per creare l'oggetto sessione viene usata un'istanza dell'oggetto **DialWIthInfo{}**.</span><span class="sxs-lookup"><span data-stu-id="da76b-139">An instance of the **DialWIthInfo{}** object is used to create the session object.</span></span> <span data-ttu-id="da76b-140">Dopo che la sessione è stata stabilita, è possibile accedere alla raccolta usando il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="da76b-140">Once the session is established, you can access the collection by using the following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="da76b-141">Creare un documento</span><span class="sxs-lookup"><span data-stu-id="da76b-141">Create a document</span></span>

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

### <a name="query-or-read-a-document"></a><span data-ttu-id="da76b-142">Leggere o eseguire query in un documento</span><span class="sxs-lookup"><span data-stu-id="da76b-142">Query or read a document</span></span>

<span data-ttu-id="da76b-143">Azure Cosmos DB supporta query avanzate sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="da76b-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="da76b-144">L'esempio di codice seguente illustra una query eseguibile nei documenti della raccolta.</span><span class="sxs-lookup"><span data-stu-id="da76b-144">The following sample code shows a query that you can run against the documents in your collection.</span></span>

```go
// Get a Document from the collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="da76b-145">Aggiornare un documento</span><span class="sxs-lookup"><span data-stu-id="da76b-145">Update a document</span></span>

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

### <a name="delete-a-document"></a><span data-ttu-id="da76b-146">Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="da76b-146">Delete a document</span></span>

<span data-ttu-id="da76b-147">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="da76b-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-the-app"></a><span data-ttu-id="da76b-148">Esecuzione dell'app</span><span class="sxs-lookup"><span data-stu-id="da76b-148">Run the app</span></span>

1. <span data-ttu-id="da76b-149">In Gogland verificare che il valore GOPATH, disponibile in **File**, **Settings** (Impostazioni), **Go**, **GOPATH**, includa il percorso di installazione di gopkg, che per impostazione predefinita è USERPROFILE\g.</span><span class="sxs-lookup"><span data-stu-id="da76b-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include the location in which the gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="da76b-150">Impostare come commento le righe 91-96 che eliminano il documento per poter visualizzare il documento dopo l'esecuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="da76b-150">Comment out the lines that delete the document, lines 91-96, so that you can see the document after running the app.</span></span>
3. <span data-ttu-id="da76b-151">In Gogland fare clic su **Run** (Esegui) e quindi su **Run 'Build main.go and run'** (Esegui 'Compila main.go ed esegui').</span><span class="sxs-lookup"><span data-stu-id="da76b-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="da76b-152">L'app viene completata e visualizza la descrizione del documento creato in [Creare un documento](#create-document).</span><span class="sxs-lookup"><span data-stu-id="da76b-152">The app finishes and displays the description of the document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Visualizzazione dell'output dell'app in Gogland](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="da76b-154">Esaminare il documento in Esplora dati</span><span class="sxs-lookup"><span data-stu-id="da76b-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="da76b-155">Tornare al portale di Azure per visualizzare il documento in Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="da76b-155">Go back to the Azure portal to see your document in Data Explorer.</span></span>

1. <span data-ttu-id="da76b-156">Fare clic su **Esplora dati (anteprima)** nel menu di spostamento a sinistra, espandere **golang-coach**, **pacchetto** e quindi fare clic su **Documenti**.</span><span class="sxs-lookup"><span data-stu-id="da76b-156">Click **Data Explorer (Preview)** in the left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="da76b-157">Nella scheda **Documenti** fare clic su \_id per visualizzare il documento nel riquadro destro.</span><span class="sxs-lookup"><span data-stu-id="da76b-157">In the **Documents** tab, click the \_id to display the document in the right pane.</span></span> 

    ![Esplora dati con documento appena creato](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="da76b-159">Si può quindi lavorare sul documento inline e fare clic su **Aggiorna** per salvarlo.</span><span class="sxs-lookup"><span data-stu-id="da76b-159">You can then work with the document inline and click **Update** to save it.</span></span> <span data-ttu-id="da76b-160">È anche possibile eliminare il documento oppure creare nuovi documenti o nuove query.</span><span class="sxs-lookup"><span data-stu-id="da76b-160">You can also delete the document, or create new documents or queries.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="da76b-161">Esaminare i contratti di servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="da76b-161">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="da76b-162">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="da76b-162">Clean up resources</span></span>

<span data-ttu-id="da76b-163">Se non si intende continuare a usare l'app, eliminare tutte le risorse create tramite questa guida di avvio rapido nel portale di Azure eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="da76b-163">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="da76b-164">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="da76b-164">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="da76b-165">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="da76b-165">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da76b-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da76b-166">Next steps</span></span>

<span data-ttu-id="da76b-167">In questa guida introduttiva si è appreso come creare un account Azure Cosmos DB ed eseguire un'app Golang con l'API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="da76b-167">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Golang app using the API for MongoDB.</span></span> <span data-ttu-id="da76b-168">È ora possibile importare dati aggiuntivi nell'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="da76b-168">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="da76b-169">Importare dati in Azure Cosmos DB per l'API MongoDB</span><span class="sxs-lookup"><span data-stu-id="da76b-169">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)
