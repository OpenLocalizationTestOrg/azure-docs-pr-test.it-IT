---
title: aaaUse Python tooquery Database SQL di Azure | Documenti Microsoft
description: In questo argomento illustra come toouse Python toocreate un programma che si connette tooan Database SQL di Azure e query tramite istruzioni Transact-SQL.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="b59da-103">Utilizzare Python tooquery un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b59da-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="b59da-104">Questa Guida introduttiva illustra come toouse [Python](https://python.org) tooconnect tooan Azure SQL database e utilizzare dati tooquery di istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="b59da-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b59da-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b59da-105">Prerequisites</span></span>

<span data-ttu-id="b59da-106">Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="b59da-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="b59da-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59da-107">An Azure SQL database.</span></span> <span data-ttu-id="b59da-108">Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="b59da-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="b59da-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="b59da-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="b59da-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="b59da-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="b59da-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="b59da-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="b59da-112">Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="b59da-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="b59da-113">Avere installato Python e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b59da-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="b59da-114">**MacOS**: installare Homebrew e Python, installare il driver ODBC hello e SQLCMD e quindi hello Python Driver per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b59da-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="b59da-115">Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="b59da-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="b59da-116">**Ubuntu**: installare Python e altri necessari pacchetti, quindi installare hello Python Driver per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b59da-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="b59da-117">Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="b59da-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="b59da-118">**Windows**: installare una versione più recente di hello di Python (variabile di ambiente è ora configurata per l'utente), installare il driver ODBC hello e SQLCMD e quindi installare hello Python Driver per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b59da-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="b59da-119">Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="b59da-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="b59da-120">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="b59da-120">SQL server connection information</span></span>

<span data-ttu-id="b59da-121">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b59da-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="b59da-122">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="b59da-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="b59da-123">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b59da-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b59da-124">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="b59da-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="b59da-125">In hello **Panoramica** pagina per il database, revisione hello nome completo del server come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="b59da-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="b59da-126">È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.</span><span class="sxs-lookup"><span data-stu-id="b59da-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="b59da-128">Se si dimentica le informazioni di accesso del server, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="b59da-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="b59da-129">Inserire codice tooquery SQL database</span><span class="sxs-lookup"><span data-stu-id="b59da-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="b59da-130">Nell'editor di testo preferito creare un nuovo file, **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="b59da-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="b59da-131">Sostituire il contenuto di hello con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.</span><span class="sxs-lookup"><span data-stu-id="b59da-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="b59da-132">Eseguire il codice hello</span><span class="sxs-lookup"><span data-stu-id="b59da-132">Run hello code</span></span>

1. <span data-ttu-id="b59da-133">Al prompt dei comandi di hello, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="b59da-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="b59da-134">Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b59da-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b59da-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b59da-135">Next steps</span></span>

- [<span data-ttu-id="b59da-136">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b59da-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="b59da-137">Driver Microsoft Python per SQL Server</span><span class="sxs-lookup"><span data-stu-id="b59da-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="b59da-138">Centro per sviluppatori Python</span><span class="sxs-lookup"><span data-stu-id="b59da-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

