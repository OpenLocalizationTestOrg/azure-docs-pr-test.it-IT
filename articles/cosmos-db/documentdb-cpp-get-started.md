---
title: esercitazione aaaC + + per Azure Cosmos DB | Documenti Microsoft
description: "Esercitazione su C++ che crea un database e un'applicazione console in C++ con un SDK per C++ approvato per Azure Cosmos DB. Azure Cosmos DB è un servizio di database con copertura globale."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="29b38-104">Cosmos Azure DB: Esercitazione di applicazione console C++ per hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="29b38-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29b38-105">.NET</span><span class="sxs-lookup"><span data-stu-id="29b38-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="29b38-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="29b38-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="29b38-107">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="29b38-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="29b38-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="29b38-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="29b38-109">Java</span><span class="sxs-lookup"><span data-stu-id="29b38-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="29b38-110">C++</span><span class="sxs-lookup"><span data-stu-id="29b38-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="29b38-111">Esercitazione di C++ toohello iniziale per l'API di Azure Cosmos DB DocumentDB hello approvate per SDK per C++.</span><span class="sxs-lookup"><span data-stu-id="29b38-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="29b38-112">Al termine di questa esercitazione, si otterrà un'applicazione console che consente di creare ed eseguire query sulle risorse di Azure Cosmos DB, incluso un database C++.</span><span class="sxs-lookup"><span data-stu-id="29b38-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="29b38-113">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="29b38-113">We'll cover:</span></span>

* <span data-ttu-id="29b38-114">Creazione e connessione account Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="29b38-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="29b38-115">Configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="29b38-115">Setting up your application</span></span>
* <span data-ttu-id="29b38-116">Creazione di un database Azure Cosmos DB in C++</span><span class="sxs-lookup"><span data-stu-id="29b38-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="29b38-117">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="29b38-117">Creating a collection</span></span>
* <span data-ttu-id="29b38-118">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="29b38-118">Creating JSON documents</span></span>
* <span data-ttu-id="29b38-119">Esecuzione di query hello raccolta</span><span class="sxs-lookup"><span data-stu-id="29b38-119">Querying hello collection</span></span>
* <span data-ttu-id="29b38-120">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="29b38-120">Replacing a document</span></span>
* <span data-ttu-id="29b38-121">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="29b38-121">Deleting a document</span></span>
* <span data-ttu-id="29b38-122">L'eliminazione di database C++ Azure Cosmos DB hello</span><span class="sxs-lookup"><span data-stu-id="29b38-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="29b38-123">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="29b38-123">Don't have time?</span></span> <span data-ttu-id="29b38-124">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="29b38-124">Don't worry!</span></span> <span data-ttu-id="29b38-125">la soluzione completa di Hello è disponibile in [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="29b38-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="29b38-126">Vedere [ottenere una soluzione completa hello](#GetSolution) per istruzioni rapide.</span><span class="sxs-lookup"><span data-stu-id="29b38-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="29b38-127">Dopo aver completato l'esercitazione C++ hello,. voto hello utilizzare i pulsanti nella parte inferiore di hello del toogive pagina ci commenti e suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="29b38-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="29b38-128">Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti o [raggiungere qui toous](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="29b38-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="29b38-129">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="29b38-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="29b38-130">Prerequisiti per l'esercitazione hello C++</span><span class="sxs-lookup"><span data-stu-id="29b38-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="29b38-131">Assicurarsi di avere hello segue:</span><span class="sxs-lookup"><span data-stu-id="29b38-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="29b38-132">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="29b38-132">An active Azure account.</span></span> <span data-ttu-id="29b38-133">Se non si ha un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29b38-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="29b38-134">[Visual Studio](https://www.visualstudio.com/downloads/), con i componenti di linguaggio C++ hello installati.</span><span class="sxs-lookup"><span data-stu-id="29b38-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="29b38-135">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29b38-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="29b38-136">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29b38-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="29b38-137">Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[del programma di installazione dell'applicazione C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="29b38-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="29b38-138"><a id="SetupC++"></a>Passaggio 2. Configurare un'applicazione C++</span><span class="sxs-lookup"><span data-stu-id="29b38-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="29b38-139">Aprire Visual Studio, quindi scegliere hello **File** menu, fare clic su **nuovo**e quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="29b38-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="29b38-140">In hello **nuovo progetto** finestra hello **installato** riquadro espandere **Visual C++**, fare clic su **Win32**, quindi fare clic su  **Applicazione Console Win32**.</span><span class="sxs-lookup"><span data-stu-id="29b38-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="29b38-141">Hellodocumentdb progetto hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="29b38-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Schermata della creazione guidata nuovo progetto hello](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="29b38-143">Quando si avvia Creazione guidata applicazione Win32 hello, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="29b38-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="29b38-144">Dopo aver creato il progetto di hello, aprire Gestione pacchetti NuGet di hello facendo hello **hellodocumentdb** nel progetto **Esplora** e facendo clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="29b38-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Screenshot che illustra la gestione pacchetti NuGet dal menu progetto hello](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="29b38-146">In hello **NuGet: hellodocumentdb** scheda, fare clic su **Sfoglia**e quindi cercare *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="29b38-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="29b38-147">Nei risultati di hello, selezionare DocumentDbCPP, come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="29b38-148">Il pacchetto installa tooC riferimenti c++ REST SDK, che è una dipendenza per hello DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="29b38-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Pacchetto di DocumentDbCpp hello screenshot che mostra evidenziato](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="29b38-150">Dopo aver aggiunto i pacchetti hello progetto tooyour, siamo tutti toostart set scrivere del codice.</span><span class="sxs-lookup"><span data-stu-id="29b38-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="29b38-151"><a id="Config"></a>Passaggio 3: Copiare dal portale di Azure i dettagli di connessione per il database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29b38-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="29b38-152">Visualizzare [portale di Azure](https://portal.azure.com) e attraversare toohello Azure Cosmos DB account del database è stato creato.</span><span class="sxs-lookup"><span data-stu-id="29b38-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="29b38-153">È necessario hello URI e chiave primaria di hello dal portale di Azure in hello successivo passaggio tooestablish una connessione da questo frammento di codice C++.</span><span class="sxs-lookup"><span data-stu-id="29b38-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB URI e le chiavi in hello portale di Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="29b38-155"><a id="Connect"></a>Passaggio 4: Connettere l'account di Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="29b38-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="29b38-156">Aggiungere hello seguenti spazi dei nomi e le intestazioni tooyour codice sorgente dopo `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="29b38-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="29b38-157">Successivamente aggiungere seguente hello tooyour main (funzione) del codice e sostituire le impostazioni di Azure Cosmos DB ottenuto al passaggio 3 di configurazione dell'account hello e toomatch chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="29b38-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="29b38-158">Ora che si dispone di client di hello codice tooinitialize hello documentdb, esaminiamo un utilizzo delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29b38-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="29b38-159"><a id="CreateDBColl"></a>Passaggio 5. Creare un database e una raccolta C++</span><span class="sxs-lookup"><span data-stu-id="29b38-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="29b38-160">Prima che si esegue questo passaggio, è opportuno discutere interagiscono di un database, raccolta e documenti per gli utenti che sono nuovi tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="29b38-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="29b38-161">Un [database](documentdb-resources.md#databases) è un contenitore logico di archiviazione documenti partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="29b38-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="29b38-162">Oggetto [raccolta](documentdb-resources.md#collections) è un contenitore di documenti JSON e hello associati logica dell'applicazione JavaScript.</span><span class="sxs-lookup"><span data-stu-id="29b38-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="29b38-163">È possibile apprendere informazioni modello gerarchica di risorse di Azure Cosmos DB hello e concetti in [concetti e modello gerarchica di risorse di Azure Cosmos DB](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="29b38-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="29b38-164">aggiungere hello successivo toohello codice alla fine della funzione principale toocreate un database e una raccolta corrispondente.</span><span class="sxs-lookup"><span data-stu-id="29b38-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="29b38-165">Verrà creato un database denominato 'FamilyRegistry' e una raccolta denominata 'FamilyCollection' con configurazione di client hello dichiarati nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="29b38-166"><a id="CreateDoc"></a>Passaggio 6. Creare un documento</span><span class="sxs-lookup"><span data-stu-id="29b38-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="29b38-167">I [documenti](documentdb-resources.md#documents) corrispondono al contenuto JSON liberamente definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="29b38-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="29b38-168">È ora possibile inserire un documento in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29b38-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="29b38-169">È possibile creare un documento tramite la copia hello seguente di codice nell'entità finale della funzione principale di hello hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="29b38-170">toosummarize, questo codice crea un database di Azure Cosmos DB e raccolta documenti, è possibile eseguire una query in Document Explorer nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="29b38-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Esercitazione per C++ - diagramma che illustra relazione gerarchica di hello tra account hello, database hello, raccolta hello e documenti hello](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="29b38-172"><a id="QueryDB"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29b38-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="29b38-173">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="29b38-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="29b38-174">Hello codice di esempio seguente viene illustrata una query eseguita utilizzando la sintassi SQL che è possibile eseguire sui documenti hello creati nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="29b38-175">funzione Hello accetta come argomenti hello identificatore univoco o id di risorsa per il database di hello e la raccolta di hello insieme ai client di documento hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="29b38-176">Aggiungere questo codice prima della funzione principale.</span><span class="sxs-lookup"><span data-stu-id="29b38-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="29b38-177"><a id="Replace"></a>Passaggio 8. Sostituire un documento</span><span class="sxs-lookup"><span data-stu-id="29b38-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="29b38-178">DB Cosmos Azure supporta sostituendo documenti JSON, come illustrato nel seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="29b38-179">Aggiungere questo codice dopo la funzione executesimplequery hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="29b38-180"><a id="Delete"></a>Passaggio 9. Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="29b38-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="29b38-181">Azure Cosmos DB supporta l'eliminazione di documenti JSON, è possibile farlo da copiare e incollare hello seguente codice dopo la funzione replacedocument hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="29b38-182"><a id="DeleteDB"></a>Passaggio 10. Eliminare un database</span><span class="sxs-lookup"><span data-stu-id="29b38-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="29b38-183">L'eliminazione database hello creato rimuove database hello e tutte le risorse figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="29b38-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="29b38-184">Copiare e incollare hello seguente frammento di codice (pulizia di funzione) dopo il database di hello deletedocument funzione tooremove hello e tutte le risorse figlio hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="29b38-185"><a id="Run"></a>Passaggio 11. Eseguire l'intera applicazione C++</span><span class="sxs-lookup"><span data-stu-id="29b38-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="29b38-186">È stato aggiunto codice toocreate, eseguire una query, modificare ed eliminare risorse Azure Cosmos DB diverse.</span><span class="sxs-lookup"><span data-stu-id="29b38-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="29b38-187">Segnalare il problema ora associare questo aggiungendo la funzione principale in hellodocumentdb.cpp insieme ad alcuni messaggi di diagnostica chiamate toothese diverse funzioni.</span><span class="sxs-lookup"><span data-stu-id="29b38-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="29b38-188">È possibile farlo sostituendo hello main (funzione) dell'applicazione con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="29b38-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="29b38-189">Questo scritture account_configuration_uri hello e primary_key copiati nel codice hello nel passaggio 3, quindi è necessario salvare che i valori hello di riga o la copia nel nuovo dal portale di hello.</span><span class="sxs-lookup"><span data-stu-id="29b38-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="29b38-190">È ora deve essere in grado di toobuild e premere F5 per eseguire il codice in Visual Studio o in alternativa, nella finestra terminal hello individuando applicazione hello e in esecuzione hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="29b38-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="29b38-191">Si dovrebbe vedere l'output di hello dell'app avviata get.</span><span class="sxs-lookup"><span data-stu-id="29b38-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="29b38-192">output di Hello deve corrispondere hello seguente schermata.</span><span class="sxs-lookup"><span data-stu-id="29b38-192">hello output should match hello following screenshot.</span></span>

![Output dell'applicazione C++ in Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="29b38-194">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="29b38-194">Congratulations!</span></span> <span data-ttu-id="29b38-195">È stata completata l'esercitazione C++ hello e la prima applicazione console Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="29b38-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="29b38-196"><a id="GetSolution"></a>Ottenere hello soluzione completa di C++ dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="29b38-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="29b38-197">soluzione GetStarted hello toobuild che contiene tutti gli esempi di hello in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="29b38-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="29b38-198">[Account Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="29b38-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="29b38-199">Hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) soluzione disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="29b38-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29b38-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="29b38-200">Next steps</span></span>
* <span data-ttu-id="29b38-201">Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="29b38-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="29b38-202">Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="29b38-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="29b38-203">Ulteriori informazioni sul modello di programmazione hello nella sezione sviluppo di hello hello [pagina della documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="29b38-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


