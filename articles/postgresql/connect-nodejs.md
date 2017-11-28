---
title: La connessione tooAzure Database PostgreSQL da Node.js | Documenti Microsoft
description: "Questa Guida rapida fornisce un esempio di codice Node.js, è possibile utilizzare tooconnect e cercare i dati dal Database di Azure PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="e8353-103">Il Database di Azure per PostgreSQL: usare Node.js tooconnect ed eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="e8353-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="e8353-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="e8353-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="e8353-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="e8353-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="e8353-106">Hello passaggi in questo articolo si presuppone che si ha familiarità con lo sviluppo usando Node.js e che siano tooworking nuovo con il Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8353-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e8353-107">Prerequisites</span></span>
<span data-ttu-id="e8353-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="e8353-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e8353-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="e8353-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="e8353-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="e8353-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="e8353-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="e8353-111">You also need to:</span></span>
- <span data-ttu-id="e8353-112">Installare [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="e8353-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="e8353-113">Installare il client pg</span><span class="sxs-lookup"><span data-stu-id="e8353-113">Install pg client</span></span>
<span data-ttu-id="e8353-114">Installare [pg](https://www.npmjs.com/package/pg), un client PostgreSQL per Node.js.</span><span class="sxs-lookup"><span data-stu-id="e8353-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="e8353-115">toodo, eseguire Gestione pacchetti di nodi hello (npm) per JavaScript dal client pg hello tooinstall riga di comando.</span><span class="sxs-lookup"><span data-stu-id="e8353-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="e8353-116">Verificare l'installazione di hello elencando i pacchetti hello installati.</span><span class="sxs-lookup"><span data-stu-id="e8353-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="e8353-117">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="e8353-117">Get connection information</span></span>
<span data-ttu-id="e8353-118">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e8353-119">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="e8353-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e8353-120">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e8353-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e8353-121">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="e8353-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="e8353-122">Fare clic su nome hello del server.</span><span class="sxs-lookup"><span data-stu-id="e8353-122">Click hello server name.</span></span>
4. <span data-ttu-id="e8353-123">Server di selezionare hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="e8353-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="e8353-124">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="e8353-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e8353-125">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="e8353-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="e8353-126">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="e8353-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="e8353-127">Esecuzione di codice JavaScript hello in Node.js</span><span class="sxs-lookup"><span data-stu-id="e8353-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="e8353-128">È possibile avviare Node.js da hello bash shell windows prompt dei comandi o digitando `node`, quindi eseguire codice JavaScript di esempio hello in modo interattivo dalla copia e incollarlo nel prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="e8353-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="e8353-129">In alternativa, è possibile salvare il codice JavaScript hello in un file di testo e avviare `node filename.js` con nome file hello toorun un parametro è.</span><span class="sxs-lookup"><span data-stu-id="e8353-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="e8353-130">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="e8353-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="e8353-131">Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="e8353-132">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="e8353-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="e8353-133">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server.</span><span class="sxs-lookup"><span data-stu-id="e8353-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="e8353-134">Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="e8353-135">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="e8353-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a><span data-ttu-id="e8353-136">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="e8353-136">Read data</span></span>
<span data-ttu-id="e8353-137">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="e8353-138">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="e8353-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="e8353-139">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server.</span><span class="sxs-lookup"><span data-stu-id="e8353-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="e8353-140">Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="e8353-141">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="e8353-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a><span data-ttu-id="e8353-142">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="e8353-142">Update data</span></span>
<span data-ttu-id="e8353-143">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="e8353-144">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="e8353-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="e8353-145">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server.</span><span class="sxs-lookup"><span data-stu-id="e8353-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="e8353-146">Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="e8353-147">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="e8353-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a><span data-ttu-id="e8353-148">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="e8353-148">Delete data</span></span>
<span data-ttu-id="e8353-149">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="e8353-150">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="e8353-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="e8353-151">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server.</span><span class="sxs-lookup"><span data-stu-id="e8353-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="e8353-152">Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e8353-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="e8353-153">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="e8353-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a><span data-ttu-id="e8353-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8353-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e8353-155">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="e8353-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
