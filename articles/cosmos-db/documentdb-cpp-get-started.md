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
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Cosmos Azure DB: Esercitazione di applicazione console C++ per hello API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js per MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Esercitazione di C++ toohello iniziale per l'API di Azure Cosmos DB DocumentDB hello approvate per SDK per C++. Al termine di questa esercitazione, si otterrà un'applicazione console che consente di creare ed eseguire query sulle risorse di Azure Cosmos DB, incluso un database C++.

Tratteremo questo argomento:

* Creazione e connessione account Azure Cosmos DB tooan
* Configurazione dell'applicazione
* Creazione di un database Azure Cosmos DB in C++
* Creare una raccolta
* Creazione di documenti JSON
* Esecuzione di query hello raccolta
* Sostituzione di un documento
* Eliminazione di un documento
* L'eliminazione di database C++ Azure Cosmos DB hello

Non si ha tempo? Nessun problema. la soluzione completa di Hello è disponibile in [GitHub](https://github.com/stalker314314/DocumentDBCpp). Vedere [ottenere una soluzione completa hello](#GetSolution) per istruzioni rapide.

Dopo aver completato l'esercitazione C++ hello,. voto hello utilizzare i pulsanti nella parte inferiore di hello del toogive pagina ci commenti e suggerimenti. 

Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti o [raggiungere qui toous](https://www.research.net/r/8BKRJ3Z). 

Ecco come procedere.

## <a name="prerequisites-for-hello-c-tutorial"></a>Prerequisiti per l'esercitazione hello C++
Assicurarsi di avere hello segue:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/), con i componenti di linguaggio C++ hello installati.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[del programma di installazione dell'applicazione C++](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Passaggio 2. Configurare un'applicazione C++
1. Aprire Visual Studio, quindi scegliere hello **File** menu, fare clic su **nuovo**e quindi fare clic su **progetto**. 
2. In hello **nuovo progetto** finestra hello **installato** riquadro espandere **Visual C++**, fare clic su **Win32**, quindi fare clic su  **Applicazione Console Win32**. Hellodocumentdb progetto hello e quindi fare clic su **OK**. 
   
    ![Schermata della creazione guidata nuovo progetto hello](media/documentdb-cpp-get-started/hello.png)
3. Quando si avvia Creazione guidata applicazione Win32 hello, fare clic su **fine**.
4. Dopo aver creato il progetto di hello, aprire Gestione pacchetti NuGet di hello facendo hello **hellodocumentdb** nel progetto **Esplora** e facendo clic su **Gestisci pacchetti NuGet**. 
   
    ![Screenshot che illustra la gestione pacchetti NuGet dal menu progetto hello](media/documentdb-cpp-get-started/nuget.png)
5. In hello **NuGet: hellodocumentdb** scheda, fare clic su **Sfoglia**e quindi cercare *documentdbcpp*. Nei risultati di hello, selezionare DocumentDbCPP, come illustrato nella seguente schermata hello. Il pacchetto installa tooC riferimenti c++ REST SDK, che è una dipendenza per hello DocumentDbCPP.  
   
    ![Pacchetto di DocumentDbCpp hello screenshot che mostra evidenziato](media/documentdb-cpp-get-started/cpp.png)
   
    Dopo aver aggiunto i pacchetti hello progetto tooyour, siamo tutti toostart set scrivere del codice.   

## <a id="Config"></a>Passaggio 3: Copiare dal portale di Azure i dettagli di connessione per il database di Azure Cosmos DB
Visualizzare [portale di Azure](https://portal.azure.com) e attraversare toohello Azure Cosmos DB account del database è stato creato. È necessario hello URI e chiave primaria di hello dal portale di Azure in hello successivo passaggio tooestablish una connessione da questo frammento di codice C++. 

![Azure Cosmos DB URI e le chiavi in hello portale di Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Passaggio 4: Connettere l'account di Azure Cosmos DB tooan
1. Aggiungere hello seguenti spazi dei nomi e le intestazioni tooyour codice sorgente dopo `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Successivamente aggiungere seguente hello tooyour main (funzione) del codice e sostituire le impostazioni di Azure Cosmos DB ottenuto al passaggio 3 di configurazione dell'account hello e toomatch chiave primaria. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Ora che si dispone di client di hello codice tooinitialize hello documentdb, esaminiamo un utilizzo delle risorse di Azure Cosmos DB.

## <a id="CreateDBColl"></a>Passaggio 5. Creare un database e una raccolta C++
Prima che si esegue questo passaggio, è opportuno discutere interagiscono di un database, raccolta e documenti per gli utenti che sono nuovi tooAzure DB Cosmos. Un [database](documentdb-resources.md#databases) è un contenitore logico di archiviazione documenti partizionato nelle raccolte. Oggetto [raccolta](documentdb-resources.md#collections) è un contenitore di documenti JSON e hello associati logica dell'applicazione JavaScript. È possibile apprendere informazioni modello gerarchica di risorse di Azure Cosmos DB hello e concetti in [concetti e modello gerarchica di risorse di Azure Cosmos DB](documentdb-resources.md).

aggiungere hello successivo toohello codice alla fine della funzione principale toocreate un database e una raccolta corrispondente. Verrà creato un database denominato 'FamilyRegistry' e una raccolta denominata 'FamilyCollection' con configurazione di client hello dichiarati nel passaggio precedente hello.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Passaggio 6. Creare un documento
I [documenti](documentdb-resources.md#documents) corrispondono al contenuto JSON liberamente definito dall'utente. È ora possibile inserire un documento in Azure Cosmos DB. È possibile creare un documento tramite la copia hello seguente di codice nell'entità finale della funzione principale di hello hello. 

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

toosummarize, questo codice crea un database di Azure Cosmos DB e raccolta documenti, è possibile eseguire una query in Document Explorer nel portale di Azure. 

![Esercitazione per C++ - diagramma che illustra relazione gerarchica di hello tra account hello, database hello, raccolta hello e documenti hello](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB
Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta. Hello codice di esempio seguente viene illustrata una query eseguita utilizzando la sintassi SQL che è possibile eseguire sui documenti hello creati nel passaggio precedente hello.

funzione Hello accetta come argomenti hello identificatore univoco o id di risorsa per il database di hello e la raccolta di hello insieme ai client di documento hello. Aggiungere questo codice prima della funzione principale.

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

## <a id="Replace"></a>Passaggio 8. Sostituire un documento
DB Cosmos Azure supporta sostituendo documenti JSON, come illustrato nel seguente codice hello. Aggiungere questo codice dopo la funzione executesimplequery hello.

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

## <a id="Delete"></a>Passaggio 9. Eliminare un documento
Azure Cosmos DB supporta l'eliminazione di documenti JSON, è possibile farlo da copiare e incollare hello seguente codice dopo la funzione replacedocument hello. 

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

## <a id="DeleteDB"></a>Passaggio 10. Eliminare un database
L'eliminazione database hello creato rimuove database hello e tutte le risorse figlio (raccolte, documenti e così via).

Copiare e incollare hello seguente frammento di codice (pulizia di funzione) dopo il database di hello deletedocument funzione tooremove hello e tutte le risorse figlio hello.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Passaggio 11. Eseguire l'intera applicazione C++
È stato aggiunto codice toocreate, eseguire una query, modificare ed eliminare risorse Azure Cosmos DB diverse.  Segnalare il problema ora associare questo aggiungendo la funzione principale in hellodocumentdb.cpp insieme ad alcuni messaggi di diagnostica chiamate toothese diverse funzioni.

È possibile farlo sostituendo hello main (funzione) dell'applicazione con hello seguente codice. Questo scritture account_configuration_uri hello e primary_key copiati nel codice hello nel passaggio 3, quindi è necessario salvare che i valori hello di riga o la copia nel nuovo dal portale di hello. 

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

È ora deve essere in grado di toobuild e premere F5 per eseguire il codice in Visual Studio o in alternativa, nella finestra terminal hello individuando applicazione hello e in esecuzione hello eseguibile. 

Si dovrebbe vedere l'output di hello dell'app avviata get. output di Hello deve corrispondere hello seguente schermata.

![Output dell'applicazione C++ in Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

Congratulazioni. È stata completata l'esercitazione C++ hello e la prima applicazione console Azure Cosmos DB!

## <a id="GetSolution"></a>Ottenere hello soluzione completa di C++ dell'esercitazione
soluzione GetStarted hello toobuild che contiene tutti gli esempi di hello in questo articolo, è necessario seguente hello:

* [Account Azure Cosmos DB][create-account].
* Hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) soluzione disponibile su GitHub.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).
* Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).
* Ulteriori informazioni sul modello di programmazione hello nella sezione sviluppo di hello hello [pagina della documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


