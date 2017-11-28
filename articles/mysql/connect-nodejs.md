---
title: Connettersi a Database di Azure per MySQL da Node.js | Microsoft Docs
description: "Questa guida introduttiva fornisce diversi esempi di codice Node.js che è possibile usare per connettersi ai dati ed eseguire query da Database di Azure per MySQL."
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
ms.openlocfilehash: 0c0bd4b707c114d2991e5f0473a4bfbe9e463e3c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="1bfc4-103">Database di Azure per MySQL: usare Node.js per connettersi ai dati ed eseguire query</span><span class="sxs-lookup"><span data-stu-id="1bfc4-103">Azure Database for MySQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="1bfc4-104">Questa guida introduttiva illustra come connettersi a un database di Azure per MySQL usando [Node.js](https://nodejs.org/) dalle piattaforme Windows, Ubuntu Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="1bfc4-105">Spiega come usare le istruzioni SQL per eseguire query, inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="1bfc4-106">Le procedure descritte in questo articolo presuppongono che si abbia familiarità con lo sviluppo con Node.js, ma non con Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-106">The steps in this article assume that you are familiar with developing using Node.js, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bfc4-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1bfc4-107">Prerequisites</span></span>
<span data-ttu-id="1bfc4-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="1bfc4-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="1bfc4-109">Creare un database di Azure per il server MySQL tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1bfc4-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="1bfc4-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1bfc4-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="1bfc4-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="1bfc4-111">You also need to:</span></span>
- <span data-ttu-id="1bfc4-112">Installare il runtime di [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="1bfc4-112">Install the [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="1bfc4-113">Installare il pacchetto [mysql2](https://www.npmjs.com/package/mysql2) per connettersi a MySQL dall'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span></span> 

## <a name="install-nodejs-and-the-mysql-connector"></a><span data-ttu-id="1bfc4-114">Installare Node.js e il connettore MySQL</span><span class="sxs-lookup"><span data-stu-id="1bfc4-114">Install Node.js and the MySQL connector</span></span>
<span data-ttu-id="1bfc4-115">A seconda della piattaforma, seguire le istruzioni appropriate per installare Node.js.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-115">Depending on your platform, follow the appropriate instructions to install Node.js.</span></span> <span data-ttu-id="1bfc4-116">Usare npm per installare il pacchetto mysql2 e le relative dipendenze nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="1bfc4-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="1bfc4-117">**Windows**</span></span>
1. <span data-ttu-id="1bfc4-118">Visitare la [pagina di download di Node.js](https://nodejs.org/en/download/) e selezionare l'opzione di installazione di Windows desiderata.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="1bfc4-119">Creare una cartella di progetto locale, ad esempio `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="1bfc4-120">Avviare il prompt dei comandi e passare alla cartella del progetto, ad esempio `cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="1bfc4-120">Launch the command prompt and cd into the project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="1bfc4-121">Eseguire lo strumento NPM per installare la libreria mysql2 nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-121">Run the NPM tool to install the mysql2 library into the project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="1bfc4-122">Verificare l'installazione controllando il testo di output `npm list` per `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="1bfc4-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="1bfc4-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="1bfc4-124">Eseguire questi comandi per installare **Node.js** e la gestione pacchetti **npm** per Node.js.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="1bfc4-125">Eseguire questi comandi per creare una cartella di progetto `mysqlnodejs` e installare il pacchetto mysql2 nella cartella.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-125">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="1bfc4-126">Verificare l'installazione controllando il testo di output npm list per `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="1bfc4-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="1bfc4-127">**Mac OS**</span></span>
1. <span data-ttu-id="1bfc4-128">Immettere i comandi seguenti per installare **brew**, una gestione pacchetti facile da usare per Mac OS X e **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="1bfc4-129">Eseguire questi comandi per creare una cartella di progetto `mysqlnodejs` e installare il pacchetto mysql2 nella cartella.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-129">Run the following commands to make a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="1bfc4-130">Verificare l'installazione controllando il testo di output `npm list` per `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="1bfc4-131">Il numero di versione può variare nel momento in cui vengono rilasciate nuove patch.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-131">The version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="1bfc4-132">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="1bfc4-132">Get connection information</span></span>
<span data-ttu-id="1bfc4-133">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="1bfc4-134">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="1bfc4-135">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1bfc4-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1bfc4-136">Nel riquadro a sinistra fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-136">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="1bfc4-137">Fare clic sul nome server **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-137">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="1bfc4-138">Selezionare la pagina **Proprietà** del server.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="1bfc4-139">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="1bfc4-140">![Database di Azure per MySQL - Accesso dell'amministratore del server](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="1bfc4-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="1bfc4-141">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="1bfc4-142">Esecuzione del codice JavaScript in Node.js</span><span class="sxs-lookup"><span data-stu-id="1bfc4-142">Running the JavaScript code in Node.js</span></span>
1. <span data-ttu-id="1bfc4-143">Incollare il codice JavaScript nei file di testo e salvarli in una cartella di progetto con estensione js, ad esempio C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="1bfc4-143">Paste the JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="1bfc4-144">Avviare il prompt dei comandi o la shell Bash.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-144">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="1bfc4-145">Passare alla cartella del progetto `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="1bfc4-146">Per eseguire l'applicazione, digitare il comando node seguito dal nome del file, ad esempio `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-146">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="1bfc4-147">In Windows, se l'applicazione Node non è presente nella variabile di ambiente PATH potrebbe essere necessario usare il percorso completo per avviare l'applicazione Node, ad esempio `"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="1bfc4-147">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="1bfc4-148">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="1bfc4-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="1bfc4-149">Usare il codice seguente per connettersi e caricare i dati usando le istruzioni SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-149">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="1bfc4-150">Il metodo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) viene usato per l'interfaccia con il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-150">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="1bfc4-151">La funzione [connect()](https://github.com/mysqljs/mysql#establishing-connections) viene usata per stabilire la connessione al server.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-151">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span></span> <span data-ttu-id="1bfc4-152">La funzione [query()](https://github.com/mysqljs/mysql#performing-queries) viene usata per eseguire la query SQL sul database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-152">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="1bfc4-153">Sostituire i parametri `host`, `user`, `password` e `database` con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-153">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="1bfc4-154">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="1bfc4-154">Read data</span></span>
<span data-ttu-id="1bfc4-155">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-155">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="1bfc4-156">Il metodo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) viene usato per l'interfaccia con il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-156">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="1bfc4-157">Il metodo [connect()](https://github.com/mysqljs/mysql#establishing-connections) viene usato per stabilire la connessione al server.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-157">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="1bfc4-158">Il metodo [query()](https://github.com/mysqljs/mysql#performing-queries) viene usato per eseguire la query SQL sul database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-158">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> <span data-ttu-id="1bfc4-159">La matrice dei risultati viene usata per contenere i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-159">The results array is used to hold the results of the query.</span></span>

<span data-ttu-id="1bfc4-160">Sostituire i parametri `host`, `user`, `password` e `database` con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-160">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="1bfc4-161">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="1bfc4-161">Update data</span></span>
<span data-ttu-id="1bfc4-162">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-162">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="1bfc4-163">Il metodo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) viene usato per l'interfaccia con il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-163">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="1bfc4-164">Il metodo [connect()](https://github.com/mysqljs/mysql#establishing-connections) viene usato per stabilire la connessione al server.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-164">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="1bfc4-165">Il metodo [query()](https://github.com/mysqljs/mysql#performing-queries) viene usato per eseguire la query SQL sul database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-165">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="1bfc4-166">Sostituire i parametri `host`, `user`, `password` e `database` con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="1bfc4-167">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="1bfc4-167">Delete data</span></span>
<span data-ttu-id="1bfc4-168">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-168">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="1bfc4-169">Il metodo [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) viene usato per l'interfaccia con il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-169">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="1bfc4-170">Il metodo [connect()](https://github.com/mysqljs/mysql#establishing-connections) viene usato per stabilire la connessione al server.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-170">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="1bfc4-171">Il metodo [query()](https://github.com/mysqljs/mysql#performing-queries) viene usato per eseguire la query SQL sul database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-171">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="1bfc4-172">Sostituire i parametri `host`, `user`, `password` e `database` con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="1bfc4-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1bfc4-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1bfc4-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1bfc4-174">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="1bfc4-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
