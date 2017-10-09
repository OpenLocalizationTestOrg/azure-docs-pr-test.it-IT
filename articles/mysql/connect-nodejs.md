---
title: La connessione tooAzure Database MySQL da Node.js | Documenti Microsoft
description: "Questa Guida introduttiva offre numerosi esempi di codice Node.js è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: usare Node.js tooconnect ed eseguire query sui dati
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL [Node.js](https://nodejs.org/) da piattaforme di Windows, Ubuntu Linux e Mac. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. Hello passaggi in questo articolo si presuppone che si ha familiarità con lo sviluppo usando Node.js e che siano tooworking nuovo con il Database di Azure per MySQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

È anche necessario:
- Installare hello [Node.js](https://nodejs.org) runtime.
- Installare [mysql2](https://www.npmjs.com/package/mysql2) tooMySQL tooconnect da Node.js applicazione hello del pacchetto. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Installazione di Node.js e hello connettore MySQL
A seconda della piattaforma, seguire hello istruzioni appropriate tooinstall Node.js. Utilizzare un pacchetto mysql2 hello npm tooinstall e le relative dipendenze nella cartella del progetto.

### <a name="windows"></a>**Windows**
1. Visitare hello [pagina di download di Node.js](https://nodejs.org/en/download/) e selezionare l'opzione di installazione di Windows desiderata.
2. Creare una cartella di progetto locale, ad esempio `nodejsmysql`. 
3. Avviare il prompt hello e cd, ad esempio nella cartella di progetto hello,`cd c:\nodejsmysql\`
4. Eseguire una libreria di hello NPM strumento tooinstall hello mysql2 nella cartella di progetto hello.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Verificare l'installazione di hello controllando hello `npm list` output di testo per `mysql2@1.3.5`.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. La seguente esecuzione hello comandi tooinstall **Node.js** e **npm** hello package manager per Node.js.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Eseguire hello toomake i comandi seguenti di una cartella di progetto `mysqlnodejs` e installare il pacchetto di mysql2 hello in tale cartella.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Verificare l'installazione di hello controllando testo di output dell'elenco di npm per `mysql2@1.3.5`.

### <a name="mac-os"></a>**Mac OS**
1. Immettere i seguenti comandi tooinstall hello **brew**, un manager di pacchetto da utilizzare per Mac OS X e **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Eseguire hello toomake i comandi seguenti di una cartella di progetto `mysqlnodejs` e installare il pacchetto di mysql2 hello in tale cartella.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Verificare l'installazione di hello controllando hello `npm list` output di testo per `mysql2@1.3.6`. numero di versione Hello può variare vengono rilasciate nuove patch.

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel riquadro di sinistra hello, fare clic su **tutte le risorse**e quindi cercare server hello sia stato creato (ad esempio, **myserver4demo**).
3. Fare clic sul nome di server hello **myserver4demo**.
4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per MySQL - Accesso dell'amministratore del server](./media/connect-nodejs/1_server-properties-name-login.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>Esecuzione di codice JavaScript hello in Node.js
1. Incollare il codice JavaScript hello in file di testo e salvare in una cartella di progetto con estensione js file, ad esempio C:\nodejsmysql\createtable.js o /home/username/nodejsmysql/createtable.js
2. Avviare il prompt di comandi hello o della shell bash. Passare alla cartella del progetto `cd nodejsmysql`.
3. un'applicazione hello toorun, digitare il comando di nodo hello seguito dal nome di file hello, ad esempio `node createtable.js`.
4. In Windows, se un'applicazione hello nodo non è presente nel proprio percorso di variabile di ambiente, potrebbe essere necessario toouse hello percorso completo toolaunch hello nodo dell'applicazione, ad esempio`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>Connettersi, creare tabelle e inserire dati
Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL.

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) metodo è toointerface utilizzato con il server MySQL hello. Hello [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) funzione è utilizzata tooestablish hello connessione toohello server. Hello [query ()](https://github.com/mysqljs/mysql#performing-queries) funzione è tooexecute utilizzati nella query SQL hello database MySQL. 

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. 

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) metodo è toointerface utilizzato con il server MySQL hello. Hello [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) metodo è usato tooestablish hello connessione toohello server. Hello [query ()](https://github.com/mysqljs/mysql#performing-queries) metodo è usato tooexecute hello SQL query database MySQL. Matrice di risultati Hello è usato toohold hello risultati della query hello.

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL. 

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) metodo è toointerface utilizzato con il server MySQL hello. Hello [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) metodo è usato tooestablish hello connessione toohello server. Hello [query ()](https://github.com/mysqljs/mysql#performing-queries) metodo è usato tooexecute hello SQL query database MySQL. 

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. 

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) metodo è toointerface utilizzato con il server MySQL hello. Hello [Connect ()](https://github.com/mysqljs/mysql#establishing-connections) metodo è usato tooestablish hello connessione toohello server. Hello [query ()](https://github.com/mysqljs/mysql#performing-queries) metodo è usato tooexecute hello SQL query database MySQL. 

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./concepts-migrate-import-export.md)
