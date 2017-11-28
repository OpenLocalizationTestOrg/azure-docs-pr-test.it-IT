---
title: aaaUse Node.js tooquery Database SQL di Azure | Documenti Microsoft
description: In questo argomento illustra come toouse Node.js toocreate un programma che si connette tooan Database SQL di Azure e query tramite istruzioni Transact-SQL.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="00890-103">Usare Node.js tooquery un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="00890-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="00890-104">Questa esercitazione introduttiva illustra come toouse [Node.js](https://nodejs.org/en/) toocreate un tooan tooconnect programma Azure SQL database e utilizzare dati tooquery di istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="00890-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00890-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00890-105">Prerequisites</span></span>

<span data-ttu-id="00890-106">Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="00890-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="00890-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="00890-107">An Azure SQL database.</span></span> <span data-ttu-id="00890-108">Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="00890-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="00890-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="00890-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="00890-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="00890-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="00890-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="00890-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="00890-112">Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="00890-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="00890-113">Avere installato Node.js e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="00890-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="00890-114">**MacOS**: installare Homebrew e Node.js e quindi installare il driver ODBC hello e SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="00890-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="00890-115">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="00890-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="00890-116">**Ubuntu**: installazione di Node.js e quindi installare il driver ODBC hello e SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="00890-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="00890-117">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="00890-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="00890-118">**Windows**: installare Chocolatey e Node.js e quindi installare il driver ODBC hello e CMD. SQL</span><span class="sxs-lookup"><span data-stu-id="00890-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="00890-119">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="00890-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="00890-120">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="00890-120">SQL server connection information</span></span>

<span data-ttu-id="00890-121">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="00890-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="00890-122">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="00890-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="00890-123">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="00890-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="00890-124">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="00890-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="00890-125">In hello **Panoramica** pagina per il database, revisione hello nome completo del server come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="00890-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="00890-126">È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.</span><span class="sxs-lookup"><span data-stu-id="00890-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="00890-128">Se si hanno dimenticato di informazioni di accesso hello del server di Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="00890-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00890-129">Sul posto per l'indirizzo IP pubblico hello del computer hello in cui si esegue questa esercitazione, è necessario disporre una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="00890-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="00890-130">Se in un computer diverso o di un diverso indirizzo IP pubblico, creare un [regola firewall di livello server utilizzando il portale di Azure di hello](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="00890-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="00890-131">Creare un progetto Web Node.js</span><span class="sxs-lookup"><span data-stu-id="00890-131">Create a Node.js project</span></span>

<span data-ttu-id="00890-132">Aprire un prompt dei comandi e creare una cartella denominata *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="00890-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="00890-133">Esplorazione delle cartelle toohello è creare ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="00890-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="00890-134">Inserire codice tooquery SQL database</span><span class="sxs-lookup"><span data-stu-id="00890-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="00890-135">Nell'ambiente di sviluppo o nell'editor di testo preferito creare un nuovo file, **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="00890-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="00890-136">Sostituire il contenuto di hello con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.</span><span class="sxs-lookup"><span data-stu-id="00890-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt tooconnect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from hello Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-hello-code"></a><span data-ttu-id="00890-137">Eseguire il codice hello</span><span class="sxs-lookup"><span data-stu-id="00890-137">Run hello code</span></span>

1. <span data-ttu-id="00890-138">Al prompt dei comandi di hello, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="00890-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="00890-139">Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00890-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00890-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00890-140">Next steps</span></span>

- <span data-ttu-id="00890-141">Informazioni su hello [Node.js Driver Microsoft per SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="00890-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="00890-142">Informazioni su come troppo[connettersi ed eseguire query su un database SQL di Azure mediante .NET core](sql-database-connect-query-dotnet-core.md) su Linux/Windows/macOS.</span><span class="sxs-lookup"><span data-stu-id="00890-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="00890-143">Informazioni su [Introduzione a .NET Core in Windows o Linux/macOS tramite riga di comando hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="00890-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="00890-144">Informazioni su come troppo[progettazione di un database SQL di Azure utilizzando SSMS](sql-database-design-first-database.md) o [progettazione di un database SQL di Azure usando .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="00890-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="00890-145">Informazioni su come troppo[Connect e query con SQL Server Management Studio](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="00890-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="00890-146">Informazioni su come troppo[Connect e query con codice di Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="00890-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


