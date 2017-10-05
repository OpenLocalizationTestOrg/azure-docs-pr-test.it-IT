---
title: Usare Python per eseguire query sul database SQL di Azure | Microsoft Docs
description: Questo argomento illustra come usare Python per creare un programma che si connette a un database SQL di Azure ed esegue query usando istruzioni Transact-SQL.
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
ms.openlocfilehash: afffcb9a4938bf97626f182bb4f4d099d807d411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-python-to-query-an-azure-sql-database"></a><span data-ttu-id="0f553-103">Usare Python per eseguire query su un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="0f553-103">Use Python to query an Azure SQL database</span></span>

 <span data-ttu-id="0f553-104">Questa guida introduttiva illustra come usare [Python](https://python.org) per connettersi a un database SQL di Azure e usare istruzioni Transact-SQL per eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="0f553-104">This quick start demonstrates how to use [Python](https://python.org) to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f553-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0f553-105">Prerequisites</span></span>

<span data-ttu-id="0f553-106">Per completare questa esercitazione introduttiva, accertarsi di avere:</span><span class="sxs-lookup"><span data-stu-id="0f553-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="0f553-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f553-107">An Azure SQL database.</span></span> <span data-ttu-id="0f553-108">Questa guida introduttiva usa le risorse create in una delle guide introduttive seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f553-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="0f553-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="0f553-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="0f553-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="0f553-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="0f553-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f553-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="0f553-112">Una [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico del computer usato per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="0f553-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="0f553-113">Avere installato Python e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0f553-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="0f553-114">**MacOS**: installare Homebrew e Python, installare il driver ODBC e SQLCMD e quindi installare il driver Python per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f553-114">**MacOS**: Install Homebrew and Python, install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="0f553-115">Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="0f553-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="0f553-116">**Ubuntu**: installare Python e gli altri pacchetti necessari e quindi installare il driver pacchetto per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f553-116">**Ubuntu**:  Install Python and other required packages, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="0f553-117">Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="0f553-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="0f553-118">**Windows**: installare la versione più recente di Python (la variabile di ambiente ora viene configurata automaticamente), installare il driver ODBC e SQLCMD e quindi installare il driver Python per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f553-118">**Windows**: Install the newest version of Python (environment variable is now configured for you), install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="0f553-119">Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="0f553-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="0f553-120">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f553-120">SQL server connection information</span></span>

<span data-ttu-id="0f553-121">Ottenere le informazioni di connessione necessarie per connettersi al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f553-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="0f553-122">Nelle procedure successive saranno necessari il nome completo del server, il nome del database e le informazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="0f553-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="0f553-123">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0f553-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0f553-124">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="0f553-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="0f553-125">Nella pagina **Panoramica** per il database, verificare il nome completo del server, come mostrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="0f553-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="0f553-126">È possibile passare il puntatore sul nome del server per visualizzare l'opzione **Fare clic per copiare**.</span><span class="sxs-lookup"><span data-stu-id="0f553-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="0f553-128">Se si dimenticano le informazioni di accesso per il server, passare alla pagina del server del database SQL per visualizzare il nome dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="0f553-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="0f553-129">Inserire il codice per eseguire query sul database SQL</span><span class="sxs-lookup"><span data-stu-id="0f553-129">Insert code to query SQL database</span></span> 

1. <span data-ttu-id="0f553-130">Nell'editor di testo preferito creare un nuovo file, **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="0f553-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="0f553-131">Sostituire il contenuto con il codice seguente e aggiungere i valori appropriati per il server, il database, l'utente e la password.</span><span class="sxs-lookup"><span data-stu-id="0f553-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="0f553-132">Eseguire il codice</span><span class="sxs-lookup"><span data-stu-id="0f553-132">Run the code</span></span>

1. <span data-ttu-id="0f553-133">Al prompt dei comandi eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="0f553-133">At the command prompt, run the following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="0f553-134">Verificare che vengano restituite le prime 20 righe e quindi chiudere la finestra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0f553-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f553-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f553-135">Next steps</span></span>

- [<span data-ttu-id="0f553-136">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="0f553-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="0f553-137">Driver Microsoft Python per SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f553-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="0f553-138">Centro per sviluppatori Python</span><span class="sxs-lookup"><span data-stu-id="0f553-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

