---
title: aaaUse PHP tooquery Database SQL di Azure | Documenti Microsoft
description: In questo argomento illustra come toouse PHP toocreate un programma che si connette tooan Database SQL di Azure e query tramite istruzioni Transact-SQL.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="9c886-103">Usare PHP tooquery un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="9c886-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="9c886-104">Questa esercitazione introduttiva illustra come toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate un tooan tooconnect programma Azure SQL database e utilizzare dati tooquery di istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="9c886-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c886-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9c886-105">Prerequisites</span></span>

<span data-ttu-id="9c886-106">Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="9c886-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="9c886-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c886-107">An Azure SQL database.</span></span> <span data-ttu-id="9c886-108">Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="9c886-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="9c886-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="9c886-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="9c886-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="9c886-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="9c886-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c886-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="9c886-112">Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="9c886-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="9c886-113">Avere installato PHP e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9c886-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="9c886-114">**MacOS**: installare Homebrew e PHP, installare il driver ODBC hello e SQLCMD e quindi hello PHP Driver per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9c886-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="9c886-115">Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="9c886-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="9c886-116">**Ubuntu**: installare PHP e altri necessari pacchetti e quindi installare hello PHP Driver per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9c886-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="9c886-117">Vedere i [passaggi 1.2 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="9c886-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="9c886-118">**Windows**: versione più recente di hello installazione di PHP per IIS Express, versione più recente di hello di Microsoft Drivers per SQL Server in IIS Express, Chocolatey, il driver ODBC hello e SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="9c886-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="9c886-119">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="9c886-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="9c886-120">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="9c886-120">SQL server connection information</span></span>

<span data-ttu-id="9c886-121">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9c886-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="9c886-122">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="9c886-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="9c886-123">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c886-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9c886-124">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="9c886-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="9c886-125">In hello **Panoramica** pagina per il database, revisione hello nome completo del server come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="9c886-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="9c886-126">È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.</span><span class="sxs-lookup"><span data-stu-id="9c886-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="9c886-128">Se si dimentica le informazioni di accesso del server, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="9c886-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="9c886-129">Inserire codice tooquery SQL database</span><span class="sxs-lookup"><span data-stu-id="9c886-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="9c886-130">Nell'editor di testo preferito creare un nuovo file, **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="9c886-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="9c886-131">Sostituire il contenuto di hello con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.</span><span class="sxs-lookup"><span data-stu-id="9c886-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a><span data-ttu-id="9c886-132">Eseguire il codice hello</span><span class="sxs-lookup"><span data-stu-id="9c886-132">Run hello code</span></span>

1. <span data-ttu-id="9c886-133">Al prompt dei comandi di hello, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9c886-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="9c886-134">Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c886-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c886-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c886-135">Next steps</span></span>
- [<span data-ttu-id="9c886-136">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="9c886-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="9c886-137">Driver Microsoft PHP per SQL Server</span><span class="sxs-lookup"><span data-stu-id="9c886-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="9c886-138">Segnalare problemi o porre domande</span><span class="sxs-lookup"><span data-stu-id="9c886-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
