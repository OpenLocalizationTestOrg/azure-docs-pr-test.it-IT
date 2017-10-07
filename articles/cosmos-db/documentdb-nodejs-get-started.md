---
title: esercitazione aaaNode.js per hello API DocumentDB per Azure Cosmos DB | Documenti Microsoft
description: In questa esercitazione Node.js che crea un database Cosmos con hello API DocumentDB.
keywords: esercitazione su node.js, database nodo
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Esercitazione di Node.js: hello di utilizzare l'API DocumentDB in Azure Cosmos DB toocreate un'applicazione console Node.js
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js per MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Benvenuti toohello Node.js esercitazione per hello Azure Cosmos DB Node.js SDK. Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.

Tratteremo questo argomento:

* Creazione e connessione account Azure Cosmos DB tooan
* Configurazione dell'applicazione
* Creazione di un database nodo
* Creare una raccolta
* Creazione di documenti JSON
* Esecuzione di query hello raccolta
* Sostituzione di un documento
* Eliminazione di un documento
* L'eliminazione di hello nodo database

Non si ha tempo? Nessun problema. la soluzione completa di Hello è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Vedere [ottenere una soluzione completa hello](#GetSolution) per istruzioni rapide.

Dopo aver completato l'esercitazione Node.js hello,. utilizzare hello pulsanti di voto in hello superiore e inferiore di questa pagina di toogive ci commenti e suggerimenti. Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti.

Ecco come procedere.

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Prerequisiti per l'esercitazione Node.js hello
Assicurarsi di avere hello segue:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
    * In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione.
* [Node.js](https://nodejs.org/) v0.10.29 o versioni successive.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[impostare l'applicazione di Node.js](#SetupNode). Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[impostare l'applicazione di Node.js](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Passaggio 2: Configurare l'applicazione Node.js
1. Aprire il terminale preferito.
2. Individuare la cartella hello o la directory in cui si desidera toosave l'applicazione di Node.js.
3. Creare due file JavaScript vuoti con hello seguenti comandi:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Installare il modulo documentdb hello tramite npm. Utilizzare hello comando seguente:
   * ```npm install documentdb --save```

L'installazione è riuscita. Dopo avere completato l'installazione, è possibile iniziare a scrivere il codice.

## <a id="Config"></a>Passaggio 3: Impostare le configurazioni dell'app
Aprire il file ```config.js``` in un editor di testo.

Quindi, copia e Incolla frammento di codice hello seguente e impostare le proprietà ```config.endpoint``` e ```config.primaryKey``` tooyour Azure Cosmos DB uri di endpoint e la chiave primaria. Entrambe queste configurazioni sono reperibili hello [portale di Azure](https://portal.azure.com).

![Esercitazione per Node.js - cattura di schermata del portale di Azure, con un account di Azure Cosmos DB, con l'hub attivo hello hello evidenziato, pulsante CHIAVI hello evidenziata nel Pannello di account Azure Cosmos DB hello hello URI, la chiave primaria e SECONDARIA i valori ed evidenziati nella hello Pannello di chiavi - database nodo][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Copiare e incollare hello ```database id```, ```collection id```, e ```JSON documents``` tooyour ```config``` sottostante dell'oggetto in cui vengono impostati i ```config.endpoint``` e ```config.authKey``` proprietà. Se si dispongono già di dati desiderato toostore nel database, è possibile utilizzare Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md) invece di aggiungere le definizioni di hello document.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Hello database raccolta e definizioni del documento, che fungerà del database di Azure Cosmos ```database id```, ```collection id```e i dati dei documenti.

Infine, esportare il ```config``` dell'oggetto, in modo che sia possibile farvi riferimento all'interno di hello ```app.js``` file.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Passaggio 4: Connettere l'account di Azure Cosmos DB tooan
Aprire il vuoto ```app.js``` file nell'editor di testo hello. Copiare e incollare il codice hello seguito hello tooimport ```documentdb``` modulo e appena creata ```config``` modulo.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Copiare e incollare hello toouse di codice hello salvato in precedenza ```config.endpoint``` e ```config.primaryKey``` toocreate DocumentClient una nuova.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Ora che si dispone di client di hello codice tooinitialize hello DB Cosmos Azure, esaminiamo un utilizzo delle risorse di Azure Cosmos DB.

## <a name="step-5-create-a-node-database"></a>Passaggio 5: Creare un database di Node
Copiare e incollare il codice hello seguito hello tooset stato HTTP per non trovato, l'url di database hello e l'url della raccolta hello. Questi URL sono ricerca client DB Cosmos Azure hello insieme e il database corretto hello.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

Oggetto [database](documentdb-resources.md#databases) possono essere create usando hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funzione di hello **DocumentClient** classe. Un database è contenitore logico di hello di archiviazione documenti partizionato nelle raccolte.

Copiare e incollare hello **getDatabase** funzione per la creazione del nuovo database nel file app.js hello con hello ```id``` specificato in hello ```config``` oggetto. Hello funzione controllerà se hello del database con hello stesso ```FamilyRegistry``` id esiste già. Se esiste, verrà restituito il database esistente, invece di procedere con la creazione di un nuovo database.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copiare e incollare codice hello riportato di seguito in cui vengono impostate hello **getDatabase** funzione funzione di supporto hello tooadd **uscire** che verrà stampato il messaggio di uscita hello e chiamata hello troppo**getDatabase** (funzione).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```

Congratulazioni. La creazione di un database di Azure Cosmos DB è stata completata.

## <a id="CreateColl"></a>Passaggio 6: Creare una raccolta
> [!WARNING]
> **CreateDocumentCollectionAsync** crea una nuova raccolta, che ha implicazioni in termini di prezzi. Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Oggetto [raccolta](documentdb-resources.md#collections) possono essere create usando hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funzione di hello **DocumentClient** classe. Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.

Copiare e incollare hello **getCollection** funzione sotto hello **getDatabase** funzionare in hello app.js file toocreate la nuova raccolta con hello ```id``` specificato in hello ```config```oggetto. Nuovamente, verificheremo toomake assicurarsi che una raccolta con hello stesso ```FamilyCollection``` id esiste già. Se esiste, verrà restituita la raccolta esistente, invece di procedere con la creazione di una nuova raccolta.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copiare e incollare il codice hello sotto la chiamata hello troppo**getDatabase** tooexecute hello **getCollection** (funzione).

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```

Congratulazioni. La creazione di una raccolta di Azure Cosmos DB è stata completata.

## <a id="CreateDoc"></a>Passaggio 7: Creare un documento
Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) funzione di hello **DocumentClient** classe. I documenti sono contenuto JSON definito dall'utente (arbitrario). È ora possibile inserire un documento in Azure Cosmos DB.

Copiare e incollare hello **getFamilyDocument** funzione sotto hello **getCollection** funzione per la creazione di documenti di hello che contengono i dati JSON hello salvati in hello ```config``` oggetto. Nuovamente, verificheremo toomake assicurarsi che un documento con lo stesso id esiste già hello.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Copiare e incollare il codice hello sotto la chiamata hello troppo**getCollection** tooexecute hello **getFamilyDocument** (funzione).

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```

Congratulazioni. La creazione di un documento di Azure Cosmos DB è stata completata.

![Database - diagramma che illustra relazione gerarchica di hello tra account hello, database hello, raccolta hello e documenti hello - nodo esercitazione Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Passaggio 8: Eseguire query sulle risorse di Azure Cosmos DB
Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta. Hello codice di esempio seguente viene illustrata una query che è possibile eseguire sui documenti hello nella raccolta.

Copiare e incollare hello **queryCollection** funzione sotto hello **getFamilyDocument** funzione nel file app.js hello. Azure Cosmos DB supporta query simili a SQL, come illustrato di seguito. Per ulteriori informazioni sulla compilazione di query complesse, estrarre hello [Query Playground](https://www.documentdb.com/sql/demo) hello e [query documentazione](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


Hello seguente diagramma viene illustrato come query di database SQL di Azure Cosmos hello sintassi viene chiamata insieme hello creata.

![Database - diagramma che illustra ambito hello e il significato della query hello - nodo esercitazione Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Hello [FROM](documentdb-sql-query.md#FromClause) parola chiave è facoltativa in query hello perché le query di database di Azure Cosmos sono già tooa con ambito singola raccolta. Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta. Azure DB Cosmos dedurrà famiglie, alla radice o il nome di variabile hello scelto, raccolta corrente hello di riferimento per impostazione predefinita.

Copiare e incollare il codice hello sotto la chiamata hello troppo**getFamilyDocument** tooexecute hello **queryCollection** (funzione).

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```

Congratulazioni. L'esecuzione di query sui documenti di Azure Cosmos DB è stata completata.

## <a id="ReplaceDocument"></a>Passaggio 9: Sostituire un documento
Azure Cosmos DB supporta la sostituzione di documenti JSON.

Copiare e incollare hello **replaceFamilyDocument** funzione sotto hello **queryCollection** funzione nel file app.js hello.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copiare e incollare il codice hello sotto la chiamata hello troppo**queryCollection** tooexecute hello **replaceDocument** (funzione). Inoltre, aggiungere toocall codice hello **queryCollection** nuovamente tooverify documento hello è stata modificata.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```

Congratulazioni. La sostituzione di un documento di Azure Cosmos DB è stata completata.

## <a id="DeleteDocument"></a>Passaggio 10: Eliminare un documento
Azure Cosmos DB supporta l'eliminazione di documenti JSON.

Copiare e incollare hello **deleteFamilyDocument** funzione sotto hello **replaceFamilyDocument** (funzione).

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copiare e incollare il codice di hello seguito hello chiamata toohello secondo **queryCollection** tooexecute hello **deleteDocument** (funzione).

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```

Congratulazioni. L'eliminazione di un documento di Azure Cosmos DB è stata completata.

## <a id="DeleteDatabase"></a>Passaggio 11: Eliminare database nodo hello
L'eliminazione hello creata database rimuoverà database hello e tutte le risorse di elementi figlio (raccolte, documenti e così via).

Copiare e incollare hello **pulizia** funzione sotto hello **deleteFamilyDocument** database hello tooremove e tutte le risorse figlio di hello di funzione.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Copiare e incollare il codice hello sotto la chiamata hello troppo**deleteFamilyDocument** tooexecute hello **pulizia** (funzione).

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>Passaggio 12: Eseguire l'applicazione Node.js
Sequenza hello per chiamare le funzioni inconsistenze, dovrebbe essere simile al seguente:

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello:```node app.js```

Si dovrebbe vedere l'output di hello dell'app avviata get. output di Hello devono corrispondere a testo di esempio hello riportato di seguito.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

Congratulazioni. È stato creato è stata completata l'esercitazione Node.js hello e avere la prima applicazione console Azure Cosmos DB!

## <a id="GetSolution"></a>Ottenere hello completo Node.js soluzione di esercitazione
Se non hai tempo toocomplete hello passaggi in questa esercitazione, oppure solo da codice hello toodownload, è possibile ottenere dalla [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

soluzione GetStarted hello toorun che contiene tutti gli esempi di hello in questo articolo, è necessario seguente hello:

* [Account Azure Cosmos DB][create-account].
* Hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) soluzione disponibile su GitHub.

Installare hello **documentdb** modulo tramite npm. Utilizzare hello comando seguente:

* ```npm install documentdb --save```

Successivamente, nel hello ```config.js``` file, i valori di config.endpoint e config.authKey hello aggiornamento come descritto in [passaggio 3: impostare le configurazioni dell'applicazione](#Config). 

Quindi nella finestra del terminale, individuare il ```app.js``` file ed eseguire il comando di hello: ```node app.js```.

Per completare la procedura, è sufficiente procedere alla compilazione. 

## <a name="next-steps"></a>Passaggi successivi
* Per un esempio più complesso relativo a Node.js, Vedere [Creare un'applicazione Web Node.js con Azure Cosmos DB](documentdb-nodejs-application.md).
* Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).
* Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).
* Ulteriori informazioni sul modello di programmazione hello nella sezione sviluppo di hello hello [pagina della documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
