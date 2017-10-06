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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Il Database di Azure per PostgreSQL: usare Node.js tooconnect ed eseguire query sui dati
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL [Node.js](https://nodejs.org/). Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. Hello passaggi in questo articolo si presuppone che si ha familiarità con lo sviluppo usando Node.js e che siano tooworking nuovo con il Database di Azure per PostgreSQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Creare un database: portale](quickstart-create-server-database-portal.md)
- [Creare un database: interfaccia della riga di comando](quickstart-create-server-database-azure-cli.md)

È anche necessario:
- Installare [Node.js](https://nodejs.org)

## <a name="install-pg-client"></a>Installare il client pg
Installare [pg](https://www.npmjs.com/package/pg), un client PostgreSQL per Node.js.

toodo, eseguire Gestione pacchetti di nodi hello (npm) per JavaScript dal client pg hello tooinstall riga di comando.
```bash
npm install pg
```

Verificare l'installazione di hello elencando i pacchetti hello installati.
```bash
npm list
```

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello appena creato.
3. Fare clic su nome hello del server.
4. Server di selezionare hello **Panoramica** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-nodejs/1-connection-string.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>Esecuzione di codice JavaScript hello in Node.js
È possibile avviare Node.js da hello bash shell windows prompt dei comandi o digitando `node`, quindi eseguire codice JavaScript di esempio hello in modo interattivo dalla copia e incollarlo nel prompt dei comandi hello. In alternativa, è possibile salvare il codice JavaScript hello in un file di testo e avviare `node filename.js` con nome file hello toorun un parametro è.

## <a name="connect-create-table-and-insert-data"></a>Connettersi, creare tabelle e inserire dati
Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL.
Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server. Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL. 

Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server. Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL. 

Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database. 

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

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL. Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server. Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL. 

Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database. 

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

## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) oggetto è utilizzato toointerface con server PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) funzione è utilizzata tooestablish hello connessione toohello server. Hello [pg. Client.query()](https://github.com/brianc/node-postgres/wiki/Query) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL. 

Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database. 

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

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./howto-migrate-using-export-and-import.md)
