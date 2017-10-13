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
ms.openlocfilehash: 324b5844362c2712d54fd766eb95e1d9102f757a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a>Azure Cosmos DB: Esercitazione su un'applicazione console in C++ per l'API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js per MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Esercitazione su C++ per l'SDK per C++ approvato per l'API DocumentDB di Azure Cosmos DB Al termine di questa esercitazione, si otterrà un'applicazione console che consente di creare ed eseguire query sulle risorse di Azure Cosmos DB, incluso un database C++.

Tratteremo questo argomento:

* Creazione e connessione a un account Azure Cosmos DB
* Configurazione dell'applicazione
* Creazione di un database Azure Cosmos DB in C++
* Creare una raccolta
* Creazione di documenti JSON
* Esecuzione di query sulla raccolta
* Sostituzione di un documento
* Eliminazione di un documento
* Eliminazione di un database Azure Cosmos DB in C++

Non si ha tempo? Nessun problema. La soluzione completa è disponibile in [GitHub](https://github.com/stalker314314/DocumentDBCpp). Per istruzioni rapide, vedere [ottenere la soluzione completa](#GetSolution) .

Dopo aver completato l'esercitazione su C++, usare i pulsanti di voto alla fine di questa pagina per fornire commenti e suggerimenti. 

Se si desidera contattarci, è possibile includere il proprio indirizzo di posta elettronica nei commenti oppure [scriverci qui](https://www.research.net/r/8BKRJ3Z). 

Ecco come procedere.

## <a name="prerequisites-for-the-c-tutorial"></a>Prerequisiti per l'esercitazione su C++
Assicurarsi di disporre di quanto segue:

* Un account Azure attivo. Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare. 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [Visual Studio 2017](https://www.visualstudio.com/downloads/) con installati i componenti del linguaggio C++. Se Visual Studio 2017 non è ancora installato, è possibile scaricare e usare la versione **gratuita** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Durante l'installazione di Visual Studio abilitare **Sviluppo di Azure**.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se è già disponibile un account da usare, è possibile passare a [Configurare un'applicazione C++](#SetupC++).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Passaggio 2. Configurare un'applicazione C++
1. Aprire Visual Studio, quindi nel menu **File** scegliere **Nuovo**, infine fare clic su **Progetto**. 
2. Nella finestra **Nuovo progetto**, nel riquadro **Installato**, espandere **Visual C++**, fare clic su **Win32** e quindi su **Applicazione console Win32**. Denominare il progetto hellodocumentdb e quindi fare clic su **OK**. 
   
    ![Screenshot della Creazione guidata nuovo progetto](media/documentdb-cpp-get-started/hello.png)
3. All'avvio della procedura di creazione guidata dell'applicazione Win32, scegliere **Fine**.
4. Dopo aver creato il progetto, aprire Gestione pacchetti NuGet facendo clic con il pulsante destro del mouse sul progetto **hellodocumentdb** in **Esplora soluzioni** e quindi su **Gestisci pacchetti NuGet**. 
   
    ![Screenshot di Gestisci pacchetti NuGet nel menu di progetto](media/documentdb-cpp-get-started/nuget.png)
5. Nella scheda **NuGet: hellodocumentdb** fare clic su **Sfoglia**, quindi cercare *documentdbcpp*. Nei risultati selezionare DocumentDbCPP come illustrato nello screenshot seguente. Questo pacchetto installa i riferimenti all'SDK REST C++, da cui dipende DocumentDbCPP.  
   
    ![Screenshot con evidenziato il pacchetto DocumentDbCpp](media/documentdb-cpp-get-started/cpp.png)
   
    Dopo aver aggiunto i pacchetti al progetto, è possibile iniziare a scrivere il codice.   

## <a id="Config"></a>Passaggio 3: Copiare dal portale di Azure i dettagli di connessione per il database di Azure Cosmos DB
Visualizzare il [portale di Azure](https://portal.azure.com) e accedere all'account database di Azure Cosmos DB creato. Nel prossimo passaggio sono necessari l'URI e la chiave primaria del Portale di Azure per stabilire una connessione dal frammento di codice C++. 

![Chiavi e URI di Azure Cosmos DB nel portale di Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Passaggio 4: Connettersi a un account Azure Cosmos DB
1. Aggiungere i seguenti spazi dei nomi e intestazioni al codice sorgente, dopo `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Aggiungere quindi il codice seguente alla funzione principale e sostituire la configurazione dell'account e la chiave primaria in modo che corrispondano alle impostazioni di Azure Cosmos DB del passaggio 3. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Ora che è disponibile il codice per inizializzare il client DocumentDB, è possibile esaminare l'uso delle risorse di Azure Cosmos DB.

## <a id="CreateDBColl"></a>Passaggio 5. Creare un database e una raccolta C++
Per coloro che hanno appena iniziato a usare Azure Cosmos DB, prima di eseguire questo passaggio verrà esaminata l'interazione tra database, raccolta e documenti. Un [database](documentdb-resources.md#databases) è un contenitore logico di archiviazione documenti partizionato nelle raccolte. Una [raccolta](documentdb-resources.md#collections) è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata. Per altre informazioni sui concetti e sul modello di risorse gerarchico di Azure Cosmos DB, vedere [Modello di risorse gerarchico e concetti relativi ad Azure Cosmos DB](documentdb-resources.md).

Per creare un database con relativa raccolta, aggiungere il codice seguente alla fine della funzione principale. Verranno creati un database denominato 'FamilyRegistry' e una raccolta denominata 'FamilyCollection' tramite la configurazione del client dichiarata nel passaggio precedente.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Passaggio 6. Creare un documento
I [documenti](documentdb-resources.md#documents) corrispondono al contenuto JSON liberamente definito dall'utente. È ora possibile inserire un documento in Azure Cosmos DB. È possibile creare un documento copiando il codice seguente alla fine della funzione principale. 

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

Per riassumere, questo codice crea un database, una raccolta e i documenti di Azure Cosmos DB per l'esecuzione di query in Esplora documenti nel portale di Azure. 

![Esercitazione C++: diagramma che illustra la relazione gerarchica tra l'account, il database, la raccolta e i documenti](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB
Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta. Il codice di esempio seguente mostra una query che usa la sintassi SQL e che può essere eseguita sui documenti creati nel passaggio precedente.

La funzione accetta come argomenti l'ID di risorsa o l'identificatore univoco per il database e la raccolta, oltre al client di documenti. Aggiungere questo codice prima della funzione principale.

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
Azure Cosmos DB supporta la sostituzione dei documenti JSON, come illustrato nel codice seguente. Aggiungere questo codice dopo la funzione executesimplequery.

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
In Azure Cosmos DB è possibile eliminare documenti JSON copiando e incollando il codice seguente dopo la funzione replacedocument. 

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
Se si elimina il database creato, insieme al database vengono rimosse tutte le risorse figlio (raccolte, documenti e così via).

Copiare e incollare il frammento di codice seguente della funzione cleanup dopo la funzione deletedocument per rimuovere il database e tutte le risorse figlio.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Passaggio 11. Eseguire l'intera applicazione C++
A questo punto è stato aggiunto il codice per creare, eseguire query, modificare ed eliminare diverse risorse di Azure Cosmos DB.  A questo punto è possibile aggiungere chiamate a queste funzioni dalla funzione principale in hellodocumentdb.cpp, insieme ad alcuni messaggi di diagnostica.

Per farlo, è possibile sostituire la funzione principale dell'applicazione con il codice seguente. Vengono sovrascritti i valori account_configuration_uri e primary_key copiati nel codice al Passaggio 3, quindi salvare la riga o copiare nuovamente i valori dal portale. 

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

A questo punto dovrebbe essere possibile compilare ed eseguire il codice in Visual Studio premendo F5 oppure nella finestra del terminale individuando l'applicazione e avviando il file eseguibile. 

Verrà visualizzato l'output dell'app introduttiva. L'output deve corrispondere a quello illustrato nella schermata seguente.

![Output dell'applicazione C++ in Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

Congratulazioni. È stata completata l'esercitazione su C++ ed stata creata la prima applicazione console Azure Cosmos DB.

## <a id="GetSolution"></a>Ottenere la soluzione completa per l'esercitazione su C++
Per creare la soluzione GetStarted completa contenente tutti gli esempi riportati in questo articolo, è necessario avere:

* [Account Azure Cosmos DB][create-account].
* La soluzione [GetStarted](https://github.com/stalker314314/DocumentDBCpp) disponibile su GitHub.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come [monitorare un account Azure Cosmos DB](monitor-accounts.md).
* Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).
* Per altre informazioni sul modello di programmazione, vedere la sezione relativa allo sviluppo nella pagina [Documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


