---
title: aaaUse tooquery Ruby Database SQL di Azure | Documenti Microsoft
description: In questo argomento illustra come toouse toocreate Ruby un programma che si connette tooan Database SQL di Azure e query tramite istruzioni Transact-SQL.
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
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="77a7e-103">Utilizzare tooquery Ruby un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="77a7e-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="77a7e-104">Questa esercitazione introduttiva illustra come toouse [Ruby](https://www.ruby-lang.org) toocreate un tooan tooconnect programma Azure SQL database e utilizzare dati tooquery di istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="77a7e-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77a7e-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77a7e-105">Prerequisites</span></span>

<span data-ttu-id="77a7e-106">Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="77a7e-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="77a7e-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="77a7e-107">An Azure SQL database.</span></span> <span data-ttu-id="77a7e-108">Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="77a7e-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="77a7e-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="77a7e-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="77a7e-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="77a7e-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="77a7e-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="77a7e-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="77a7e-112">Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="77a7e-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="77a7e-113">Avere installato Ruby e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="77a7e-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="77a7e-114">**MacOS**: installare Homebrew, installare rbenv e ruby-build, installare Ruby e quindi installare FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="77a7e-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="77a7e-115">Vedere i [passaggi 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="77a7e-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="77a7e-116">**Ubuntu**: installare i prerequisiti per Ruby, installare rbenv e ruby-build, installare Ruby e quindi installare FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="77a7e-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="77a7e-117">Vedere i [passaggi 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="77a7e-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="77a7e-118">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="77a7e-118">SQL server connection information</span></span>

<span data-ttu-id="77a7e-119">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="77a7e-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="77a7e-120">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="77a7e-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="77a7e-121">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77a7e-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="77a7e-122">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="77a7e-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="77a7e-123">In hello **Panoramica** pagina per il database, esaminare hello nome completo del server.</span><span class="sxs-lookup"><span data-stu-id="77a7e-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="77a7e-124">È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="77a7e-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="77a7e-126">Se si hanno dimenticato di informazioni di accesso hello del server di Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="77a7e-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77a7e-127">Sul posto per l'indirizzo IP pubblico hello del computer hello in cui si esegue questa esercitazione, è necessario disporre una regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="77a7e-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="77a7e-128">Se in un computer diverso o di un diverso indirizzo IP pubblico, creare un [regola firewall di livello server utilizzando il portale di Azure di hello](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="77a7e-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="77a7e-129">Inserire codice tooquery SQL database</span><span class="sxs-lookup"><span data-stu-id="77a7e-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="77a7e-130">Nell'editor di testo preferito creare un nuovo file, **sqltest.rb**.</span><span class="sxs-lookup"><span data-stu-id="77a7e-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="77a7e-131">Sostituire il contenuto di hello con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.</span><span class="sxs-lookup"><span data-stu-id="77a7e-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="77a7e-132">Eseguire il codice hello</span><span class="sxs-lookup"><span data-stu-id="77a7e-132">Run hello code</span></span>

1. <span data-ttu-id="77a7e-133">Al prompt dei comandi di hello, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="77a7e-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="77a7e-134">Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="77a7e-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="77a7e-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77a7e-135">Next Steps</span></span>
- [<span data-ttu-id="77a7e-136">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="77a7e-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="77a7e-137">Repository GitHub per TinyTDS</span><span class="sxs-lookup"><span data-stu-id="77a7e-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="77a7e-138">Segnalare problemi o porre domande su TinyTDS</span><span class="sxs-lookup"><span data-stu-id="77a7e-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="77a7e-139">Driver Ruby per SQL Server</span><span class="sxs-lookup"><span data-stu-id="77a7e-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
