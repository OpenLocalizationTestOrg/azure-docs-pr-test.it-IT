---
title: Usare Ruby per eseguire query sul database SQL di Azure | Microsoft Docs
description: Questo argomento illustra come usare Ruby per creare un programma che si connette a un database SQL di Azure ed esegue query usando istruzioni Transact-SQL.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 25ff9a9cfaa5494dbb006c84e235099fe51e6545
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a><span data-ttu-id="a0397-103">Usare Ruby per eseguire query su un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="a0397-103">Use Ruby to query an Azure SQL database</span></span>

<span data-ttu-id="a0397-104">Questa esercitazione introduttiva illustra come usare [Ruby](https://www.ruby-lang.org) per creare un programma per connettersi a un database SQL di Azure e usare istruzioni Transact-SQL per eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="a0397-104">This quick start tutorial demonstrates how to use [Ruby](https://www.ruby-lang.org) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0397-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a0397-105">Prerequisites</span></span>

<span data-ttu-id="a0397-106">Per completare questa esercitazione introduttiva, accertarsi di avere i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0397-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="a0397-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0397-107">An Azure SQL database.</span></span> <span data-ttu-id="a0397-108">Questa guida introduttiva usa le risorse create in una delle guide introduttive seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0397-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="a0397-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="a0397-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="a0397-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="a0397-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="a0397-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0397-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="a0397-112">Una [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico del computer usato per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="a0397-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="a0397-113">Avere installato Ruby e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a0397-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="a0397-114">**MacOS**: installare Homebrew, installare rbenv e ruby-build, installare Ruby e quindi installare FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="a0397-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="a0397-115">Vedere i [passaggi 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="a0397-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="a0397-116">**Ubuntu**: installare i prerequisiti per Ruby, installare rbenv e ruby-build, installare Ruby e quindi installare FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="a0397-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="a0397-117">Vedere i [passaggi 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="a0397-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="a0397-118">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="a0397-118">SQL server connection information</span></span>

<span data-ttu-id="a0397-119">Ottenere le informazioni di connessione necessarie per connettersi al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0397-119">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="a0397-120">Nelle procedure successive saranno necessari il nome completo del server, il nome del database e le informazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="a0397-120">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="a0397-121">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a0397-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a0397-122">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="a0397-122">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="a0397-123">Nella pagina **Panoramica** del database esaminare il nome completo del server.</span><span class="sxs-lookup"><span data-stu-id="a0397-123">On the **Overview** page for your database, review the fully qualified server name.</span></span> <span data-ttu-id="a0397-124">È possibile passare il puntatore sul nome del server per visualizzare l'opzione **Fare clic per copiare**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="a0397-124">You can hover over the server name to bring up the **Click to copy** option, as shown in the following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="a0397-126">Se si sono dimenticate le informazioni di accesso per il server del database SQL di Azure, passare alla pagina del server del database SQL per visualizzare il nome dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="a0397-126">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0397-127">È necessario avere una regola del firewall impostata per l'indirizzo IP pubblico del computer su cui si esegue questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a0397-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="a0397-128">Se si usa un computer o un indirizzo IP pubblico diverso, creare una [regola del firewall a livello di server con il portale di Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="a0397-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="a0397-129">Inserire il codice per eseguire query sul database SQL</span><span class="sxs-lookup"><span data-stu-id="a0397-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="a0397-130">Nell'editor di testo preferito creare un nuovo file, **sqltest.rb**.</span><span class="sxs-lookup"><span data-stu-id="a0397-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="a0397-131">Sostituire il contenuto con il codice seguente e aggiungere i valori appropriati per il server, il database, l'utente e la password.</span><span class="sxs-lookup"><span data-stu-id="a0397-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-the-code"></a><span data-ttu-id="a0397-132">Eseguire il codice</span><span class="sxs-lookup"><span data-stu-id="a0397-132">Run the code</span></span>

1. <span data-ttu-id="a0397-133">Al prompt dei comandi eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="a0397-133">At the command prompt, run the following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="a0397-134">Verificare che vengano restituite le prime 20 righe e quindi chiudere la finestra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a0397-134">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a0397-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0397-135">Next Steps</span></span>
- [<span data-ttu-id="a0397-136">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="a0397-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="a0397-137">Repository GitHub per TinyTDS</span><span class="sxs-lookup"><span data-stu-id="a0397-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="a0397-138">Segnalare problemi o porre domande su TinyTDS</span><span class="sxs-lookup"><span data-stu-id="a0397-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="a0397-139">Driver Ruby per SQL Server</span><span class="sxs-lookup"><span data-stu-id="a0397-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
