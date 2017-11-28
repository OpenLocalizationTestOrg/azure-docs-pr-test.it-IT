---
title: Esercitazione su C++ per Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="0fb5f-104">Azure Cosmos DB: Esercitazione su un'applicazione console in C++ per l'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fb5f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0fb5f-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="0fb5f-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0fb5f-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="0fb5f-107">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="0fb5f-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="0fb5f-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="0fb5f-109">Java</span><span class="sxs-lookup"><span data-stu-id="0fb5f-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="0fb5f-110">C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="0fb5f-111">Esercitazione su C++ per l'SDK per C++ approvato per l'API DocumentDB di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="0fb5f-112">Al termine di questa esercitazione, si otterrà un'applicazione console che consente di creare ed eseguire query sulle risorse di Azure Cosmos DB, incluso un database C++.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="0fb5f-113">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="0fb5f-113">We'll cover:</span></span>

* <span data-ttu-id="0fb5f-114">Creazione e connessione a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="0fb5f-115">Configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="0fb5f-115">Setting up your application</span></span>
* <span data-ttu-id="0fb5f-116">Creazione di un database Azure Cosmos DB in C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="0fb5f-117">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="0fb5f-117">Creating a collection</span></span>
* <span data-ttu-id="0fb5f-118">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="0fb5f-118">Creating JSON documents</span></span>
* <span data-ttu-id="0fb5f-119">Esecuzione di query sulla raccolta</span><span class="sxs-lookup"><span data-stu-id="0fb5f-119">Querying the collection</span></span>
* <span data-ttu-id="0fb5f-120">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="0fb5f-120">Replacing a document</span></span>
* <span data-ttu-id="0fb5f-121">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="0fb5f-121">Deleting a document</span></span>
* <span data-ttu-id="0fb5f-122">Eliminazione di un database Azure Cosmos DB in C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="0fb5f-123">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="0fb5f-123">Don't have time?</span></span> <span data-ttu-id="0fb5f-124">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-124">Don't worry!</span></span> <span data-ttu-id="0fb5f-125">La soluzione completa è disponibile in [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="0fb5f-126">Per istruzioni rapide, vedere [ottenere la soluzione completa](#GetSolution) .</span><span class="sxs-lookup"><span data-stu-id="0fb5f-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="0fb5f-127">Dopo aver completato l'esercitazione su C++, usare i pulsanti di voto alla fine di questa pagina per fornire commenti e suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="0fb5f-128">Se si desidera contattarci, è possibile includere il proprio indirizzo di posta elettronica nei commenti oppure [scriverci qui](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="0fb5f-129">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="0fb5f-130">Prerequisiti per l'esercitazione su C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="0fb5f-131">Assicurarsi di disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0fb5f-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="0fb5f-132">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-132">An active Azure account.</span></span> <span data-ttu-id="0fb5f-133">Se non si ha un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0fb5f-134">[Visual Studio](https://www.visualstudio.com/downloads/) con installati i componenti del linguaggio C++.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="0fb5f-135">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="0fb5f-136">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="0fb5f-137">Se è già disponibile un account da usare, è possibile passare a [Configurare un'applicazione C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="0fb5f-138"><a id="SetupC++"></a>Passaggio 2. Configurare un'applicazione C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="0fb5f-139">Aprire Visual Studio, quindi nel menu **File** scegliere **Nuovo**, infine fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="0fb5f-140">Nella finestra **Nuovo progetto**, nel riquadro **Installato**, espandere **Visual C++**, fare clic su **Win32** e quindi su **Applicazione console Win32**.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="0fb5f-141">Denominare il progetto hellodocumentdb e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Screenshot della Creazione guidata nuovo progetto](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="0fb5f-143">All'avvio della procedura di creazione guidata dell'applicazione Win32, scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="0fb5f-144">Dopo aver creato il progetto, aprire Gestione pacchetti NuGet facendo clic con il pulsante destro del mouse sul progetto **hellodocumentdb** in **Esplora soluzioni** e quindi su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Screenshot di Gestisci pacchetti NuGet nel menu di progetto](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="0fb5f-146">Nella scheda **NuGet: hellodocumentdb** fare clic su **Sfoglia**, quindi cercare *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="0fb5f-147">Nei risultati selezionare DocumentDbCPP come illustrato nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="0fb5f-148">Questo pacchetto installa i riferimenti all'SDK REST C++, da cui dipende DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![Screenshot con evidenziato il pacchetto DocumentDbCpp](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="0fb5f-150">Dopo aver aggiunto i pacchetti al progetto, è possibile iniziare a scrivere il codice.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="0fb5f-151"><a id="Config"></a>Passaggio 3: Copiare dal portale di Azure i dettagli di connessione per il database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="0fb5f-152">Visualizzare il [portale di Azure](https://portal.azure.com) e accedere all'account database di Azure Cosmos DB creato.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="0fb5f-153">Nel prossimo passaggio sono necessari l'URI e la chiave primaria del Portale di Azure per stabilire una connessione dal frammento di codice C++.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Chiavi e URI di Azure Cosmos DB nel portale di Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="0fb5f-155"><a id="Connect"></a>Passaggio 4: Connettersi a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="0fb5f-156">Aggiungere i seguenti spazi dei nomi e intestazioni al codice sorgente, dopo `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="0fb5f-157">Aggiungere quindi il codice seguente alla funzione principale e sostituire la configurazione dell'account e la chiave primaria in modo che corrispondano alle impostazioni di Azure Cosmos DB del passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="0fb5f-158">Ora che è disponibile il codice per inizializzare il client DocumentDB, è possibile esaminare l'uso delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="0fb5f-159"><a id="CreateDBColl"></a>Passaggio 5. Creare un database e una raccolta C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="0fb5f-160">Per coloro che hanno appena iniziato a usare Azure Cosmos DB, prima di eseguire questo passaggio verrà esaminata l'interazione tra database, raccolta e documenti.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="0fb5f-161">Un [database](documentdb-resources.md#databases) è un contenitore logico di archiviazione documenti partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="0fb5f-162">Una [raccolta](documentdb-resources.md#collections) è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="0fb5f-163">Per altre informazioni sui concetti e sul modello di risorse gerarchico di Azure Cosmos DB, vedere [Modello di risorse gerarchico e concetti relativi ad Azure Cosmos DB](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="0fb5f-164">Per creare un database con relativa raccolta, aggiungere il codice seguente alla fine della funzione principale.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="0fb5f-165">Verranno creati un database denominato 'FamilyRegistry' e una raccolta denominata 'FamilyCollection' tramite la configurazione del client dichiarata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="0fb5f-166"><a id="CreateDoc"></a>Passaggio 6. Creare un documento</span><span class="sxs-lookup"><span data-stu-id="0fb5f-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="0fb5f-167">I [documenti](documentdb-resources.md#documents) corrispondono al contenuto JSON liberamente definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="0fb5f-168">È ora possibile inserire un documento in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="0fb5f-169">È possibile creare un documento copiando il codice seguente alla fine della funzione principale.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="0fb5f-170">Per riassumere, questo codice crea un database, una raccolta e i documenti di Azure Cosmos DB per l'esecuzione di query in Esplora documenti nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Esercitazione C++: diagramma che illustra la relazione gerarchica tra l'account, il database, la raccolta e i documenti](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="0fb5f-172"><a id="QueryDB"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0fb5f-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="0fb5f-173">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="0fb5f-174">Il codice di esempio seguente mostra una query che usa la sintassi SQL e che può essere eseguita sui documenti creati nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="0fb5f-175">La funzione accetta come argomenti l'ID di risorsa o l'identificatore univoco per il database e la raccolta, oltre al client di documenti.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="0fb5f-176">Aggiungere questo codice prima della funzione principale.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="0fb5f-177"><a id="Replace"></a>Passaggio 8. Sostituire un documento</span><span class="sxs-lookup"><span data-stu-id="0fb5f-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="0fb5f-178">Azure Cosmos DB supporta la sostituzione dei documenti JSON, come illustrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="0fb5f-179">Aggiungere questo codice dopo la funzione executesimplequery.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="0fb5f-180"><a id="Delete"></a>Passaggio 9. Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="0fb5f-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="0fb5f-181">In Azure Cosmos DB è possibile eliminare documenti JSON copiando e incollando il codice seguente dopo la funzione replacedocument.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="0fb5f-182"><a id="DeleteDB"></a>Passaggio 10. Eliminare un database</span><span class="sxs-lookup"><span data-stu-id="0fb5f-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="0fb5f-183">Se si elimina il database creato, insieme al database vengono rimosse tutte le risorse figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="0fb5f-184">Copiare e incollare il frammento di codice seguente della funzione cleanup dopo la funzione deletedocument per rimuovere il database e tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="0fb5f-185"><a id="Run"></a>Passaggio 11. Eseguire l'intera applicazione C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="0fb5f-186">A questo punto è stato aggiunto il codice per creare, eseguire query, modificare ed eliminare diverse risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="0fb5f-187">A questo punto è possibile aggiungere chiamate a queste funzioni dalla funzione principale in hellodocumentdb.cpp, insieme ad alcuni messaggi di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="0fb5f-188">Per farlo, è possibile sostituire la funzione principale dell'applicazione con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="0fb5f-189">Vengono sovrascritti i valori account_configuration_uri e primary_key copiati nel codice al Passaggio 3, quindi salvare la riga o copiare nuovamente i valori dal portale.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="0fb5f-190">A questo punto dovrebbe essere possibile compilare ed eseguire il codice in Visual Studio premendo F5 oppure nella finestra del terminale individuando l'applicazione e avviando il file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="0fb5f-191">Verrà visualizzato l'output dell'app introduttiva.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-191">You should see the output of your get started app.</span></span> <span data-ttu-id="0fb5f-192">L'output deve corrispondere a quello illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-192">The output should match the following screenshot.</span></span>

![Output dell'applicazione C++ in Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="0fb5f-194">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-194">Congratulations!</span></span> <span data-ttu-id="0fb5f-195">È stata completata l'esercitazione su C++ ed stata creata la prima applicazione console Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="0fb5f-196"><a id="GetSolution"></a>Ottenere la soluzione completa per l'esercitazione su C++</span><span class="sxs-lookup"><span data-stu-id="0fb5f-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="0fb5f-197">Per creare la soluzione GetStarted completa contenente tutti gli esempi riportati in questo articolo, è necessario avere:</span><span class="sxs-lookup"><span data-stu-id="0fb5f-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="0fb5f-198">[Account Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="0fb5f-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="0fb5f-199">La soluzione [GetStarted](https://github.com/stalker314314/DocumentDBCpp) disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="0fb5f-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fb5f-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0fb5f-200">Next steps</span></span>
* <span data-ttu-id="0fb5f-201">Informazioni su come [monitorare un account Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="0fb5f-202">Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="0fb5f-203">Per altre informazioni sul modello di programmazione, vedere la sezione relativa allo sviluppo nella pagina [Documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0fb5f-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


