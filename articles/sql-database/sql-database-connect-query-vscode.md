---
title: 'Visual Studio Code: Connettersi ed eseguire query sui dati nel database SQL di Azure | Microsoft Docs'
description: Informazioni su come connettersi a un database SQL in Azure tramite Visual Studio Code. Eseguire quindi istruzioni Transact-SQL (T-SQL) per eseguire query e modificare i dati.
metacanonical: 
keywords: connettersi al database SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: 4076b1e7ab3a70009217a1deff72da4bff0dc871
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-use-visual-studio-code-to-connect-and-query-data"></a><span data-ttu-id="4cfd7-105">Database SQL di Azure: Usare Visual Studio Code per connettersi ai dati ed eseguire query</span><span class="sxs-lookup"><span data-stu-id="4cfd7-105">Azure SQL Database: Use Visual Studio Code to connect and query data</span></span>

<span data-ttu-id="4cfd7-106">[Visual Studio Code](https://code.visualstudio.com/docs) è un editor grafico di codice per Linux, macOS e Windows che supporta le estensioni, tra cui l'[estensione mssql](https://aka.ms/mssql-marketplace), per le query di Microsoft SQL Server, database SQL di Azure e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="4cfd7-107">Questa guida introduttiva illustra come usare Visual Studio Code per connettersi a un database SQL di Azure e quindi usare istruzioni Transact-SQL per eseguire query e inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-107">This quick start demonstrates how to use Visual Studio Code to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cfd7-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4cfd7-108">Prerequisites</span></span>

<span data-ttu-id="4cfd7-109">Questa guida introduttiva usa come punto di partenza le risorse create in una delle guide introduttive seguenti:</span><span class="sxs-lookup"><span data-stu-id="4cfd7-109">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="4cfd7-110">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="4cfd7-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="4cfd7-111">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="4cfd7-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="4cfd7-112">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cfd7-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="4cfd7-113">Prima di iniziare, assicurarsi di avere installato la versione più recente di [Visual Studio Code](https://code.visualstudio.com/Download) e di aver caricato l'[estensione mssql](https://aka.ms/mssql-marketplace).</span><span class="sxs-lookup"><span data-stu-id="4cfd7-113">Before you start, make sure you have installed the newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded the [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="4cfd7-114">Per istruzioni sull'installazione dell'estensione mssql, vedere [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) (Installare Visual Studio Code) e [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) (mssql per Visual Studio Code).</span><span class="sxs-lookup"><span data-stu-id="4cfd7-114">For installation guidance for the mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="4cfd7-115">Configurare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4cfd7-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="4cfd7-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="4cfd7-116">**Mac OS**</span></span>
<span data-ttu-id="4cfd7-117">Per macOS è necessario installare OpenSSL. Si tratta di un prerequisito per DotNet Core, che viene usato dall'estensione mssql.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-117">For macOS, you need to install OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="4cfd7-118">Aprire il terminale e immettere i comandi seguenti per installare **brew** e **OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-118">Open your terminal and enter the following commands to install **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="4cfd7-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="4cfd7-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="4cfd7-120">Non è necessaria alcuna configurazione speciale.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="4cfd7-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="4cfd7-121">**Windows**</span></span>

<span data-ttu-id="4cfd7-122">Non è necessaria alcuna configurazione speciale.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="4cfd7-123">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="4cfd7-123">SQL server connection information</span></span>

<span data-ttu-id="4cfd7-124">Ottenere le informazioni di connessione necessarie per connettersi al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-124">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="4cfd7-125">Nelle procedure successive saranno necessari il nome completo del server, il nome del database e le informazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-125">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="4cfd7-126">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4cfd7-126">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4cfd7-127">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-127">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="4cfd7-128">Nella pagina **Panoramica** per il database, verificare il nome completo del server, come mostrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-128">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="4cfd7-129">È possibile passare il puntatore sul nome del server per visualizzare l'opzione **Fare clic per copiare**.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-129">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![informazioni di connessione](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="4cfd7-131">Se si sono dimenticate le informazioni di accesso per il server del database SQL di Azure, passare alla pagina del server del database SQL per visualizzare il nome dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-131">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="set-language-mode-to-sql"></a><span data-ttu-id="4cfd7-132">Impostare la modalità linguaggio SQL</span><span class="sxs-lookup"><span data-stu-id="4cfd7-132">Set language mode to SQL</span></span>

<span data-ttu-id="4cfd7-133">Impostare la modalità linguaggio su **SQL** in Visual Studio Code per abilitare i comandi mssql e T-SQL IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-133">Set the language mode is set to **SQL** in Visual Studio Code to enable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="4cfd7-134">Aprire una nuova finestra di Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="4cfd7-135">Fare clic su **Testo normale** nell'angolo inferiore destro della barra di stato.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-135">Click **Plain Text** in the lower right-hand corner of the status bar.</span></span>
3. <span data-ttu-id="4cfd7-136">Nel menu a discesa **Seleziona modalità linguaggio** che viene visualizzato, digitare **SQL** e quindi premere **INVIO** per impostare la modalità del linguaggio su SQL.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-136">In the **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** to set the language mode to SQL.</span></span> 

   ![Modalità linguaggio SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-to-your-database"></a><span data-ttu-id="4cfd7-138">Connettersi al database</span><span class="sxs-lookup"><span data-stu-id="4cfd7-138">Connect to your database</span></span>

<span data-ttu-id="4cfd7-139">Usare Visual Studio Code per stabilire una connessione al server del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-139">Use Visual Studio Code to establish a connection to your Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4cfd7-140">Prima di continuare, assicurarsi di avere a portata di mano le informazioni su server, database e account di accesso.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="4cfd7-141">Se si modifica lo stato attivo dopo aver iniziato a immettere le informazioni sul profilo di connessione in Visual Studio Code, sarà necessario riavviare la creazione del profilo di connessione.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-141">Once you begin entering the connection profile information, if you change your focus from Visual Studio Code, you have to restart creating the connection profile.</span></span>
>

1. <span data-ttu-id="4cfd7-142">In Visual Studio Code premere **CTRL+MAIUSC+P** o **F1** per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) to open the Command Palette.</span></span>

2. <span data-ttu-id="4cfd7-143">Digitare **sqlcon** e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="4cfd7-144">Premere **INVIO** per selezionare **Create Connection Profile** (Creare profilo di connessione).</span><span class="sxs-lookup"><span data-stu-id="4cfd7-144">Press **ENTER** to select **Create Connection Profile**.</span></span> <span data-ttu-id="4cfd7-145">Verrà creato un profilo di connessione per l'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="4cfd7-146">Seguire le istruzioni per specificare le proprietà di connessione per il nuovo profilo di connessione.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-146">Follow the prompts to specify the connection properties for the new connection profile.</span></span> <span data-ttu-id="4cfd7-147">Dopo aver specificato ogni valore, premere **INVIO** per continuare.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-147">After specifying each value, press **ENTER** to continue.</span></span> 

   | <span data-ttu-id="4cfd7-148">Impostazione</span><span class="sxs-lookup"><span data-stu-id="4cfd7-148">Setting</span></span>       | <span data-ttu-id="4cfd7-149">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="4cfd7-149">Suggested value</span></span> | <span data-ttu-id="4cfd7-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4cfd7-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="4cfd7-151">**Nome server</span><span class="sxs-lookup"><span data-stu-id="4cfd7-151">**Server name</span></span> | <span data-ttu-id="4cfd7-152">Nome completo del server</span><span class="sxs-lookup"><span data-stu-id="4cfd7-152">The fully qualified server name</span></span> | <span data-ttu-id="4cfd7-153">Il nome sarà simile a: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-153">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="4cfd7-154">**Database name** (Nome database)</span><span class="sxs-lookup"><span data-stu-id="4cfd7-154">**Database name**</span></span> | <span data-ttu-id="4cfd7-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="4cfd7-155">mySampleDatabase</span></span> | <span data-ttu-id="4cfd7-156">Nome del database a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-156">The name of the database to which to connect.</span></span> |
   | <span data-ttu-id="4cfd7-157">**Autenticazione**</span><span class="sxs-lookup"><span data-stu-id="4cfd7-157">**Authentication**</span></span> | <span data-ttu-id="4cfd7-158">Account di accesso SQL</span><span class="sxs-lookup"><span data-stu-id="4cfd7-158">SQL Login</span></span>| <span data-ttu-id="4cfd7-159">L'autenticazione SQL è il solo tipo di autenticazione configurato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-159">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="4cfd7-160">**Nome utente**</span><span class="sxs-lookup"><span data-stu-id="4cfd7-160">**User name**</span></span> | <span data-ttu-id="4cfd7-161">Account amministratore del server</span><span class="sxs-lookup"><span data-stu-id="4cfd7-161">The server admin account</span></span> | <span data-ttu-id="4cfd7-162">Si tratta dell'account specificato quando è stato creato il server.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-162">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="4cfd7-163">**Password (SQL Login)** (Password - Account di accesso SQL)</span><span class="sxs-lookup"><span data-stu-id="4cfd7-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="4cfd7-164">Password per l'account amministratore del server</span><span class="sxs-lookup"><span data-stu-id="4cfd7-164">The password for your server admin account</span></span> | <span data-ttu-id="4cfd7-165">Si tratta della password specificata quando è stato creato il server.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-165">This is the password that you specified when you created the server.</span></span> |
   | <span data-ttu-id="4cfd7-166">**Save Password?** (Salvare la password?)</span><span class="sxs-lookup"><span data-stu-id="4cfd7-166">**Save Password?**</span></span> | <span data-ttu-id="4cfd7-167">Sì o No</span><span class="sxs-lookup"><span data-stu-id="4cfd7-167">Yes or No</span></span> | <span data-ttu-id="4cfd7-168">Selezionare Sì se non si vuole immettere la password ogni volta.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-168">Select Yes if you do not want to enter the password each time.</span></span> |
   | <span data-ttu-id="4cfd7-169">**Immettere un nome per questo profilo**</span><span class="sxs-lookup"><span data-stu-id="4cfd7-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="4cfd7-170">Nome del profilo, ad esempio **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="4cfd7-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="4cfd7-171">Un nome del profilo salvato velocizza la connessione agli accessi successivi.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="4cfd7-172">Premere il tasto **ESC** per chiudere il messaggio che informa che il profilo è stato creato e connesso.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-172">Press the **ESC** key to close the info message that informs you that the profile is created and connected.</span></span>

6. <span data-ttu-id="4cfd7-173">Verificare la connessione nella barra di stato.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-173">Verify your connection in the status bar.</span></span>

   ![Stato della connessione](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="4cfd7-175">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="4cfd7-175">Query data</span></span>

<span data-ttu-id="4cfd7-176">Usare il codice seguente per eseguire una query per individuare i primi 20 prodotti per categoria usando l'istruzione [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) di Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-176">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4cfd7-177">Nella finestra dell'**editor** immettere la query seguente nella finestra di query vuota:</span><span class="sxs-lookup"><span data-stu-id="4cfd7-177">In the **Editor** window, enter the following query in the empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="4cfd7-178">Premere **CTRL+MAIUSC+E** per recuperare dati dalle tabelle Product e ProductCategory.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-178">Press **CTRL+SHIFT+E** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![Query](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="4cfd7-180">Inserire dati</span><span class="sxs-lookup"><span data-stu-id="4cfd7-180">Insert data</span></span>

<span data-ttu-id="4cfd7-181">Usare il codice seguente per inserire un nuovo prodotto nella tabella SalesLT.Product usando l'istruzione [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) di Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-181">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4cfd7-182">Nella finestra dell'**editor** eliminare la query precedente e immettere la query seguente:</span><span class="sxs-lookup"><span data-stu-id="4cfd7-182">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="4cfd7-183">Premere **CTRL+MAIUSC+E** per inserire una nuova riga nella tabella Product.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-183">Press **CTRL+SHIFT+E** to insert a new row in the Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="4cfd7-184">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="4cfd7-184">Update data</span></span>

<span data-ttu-id="4cfd7-185">Usare il codice seguente per aggiornare il nuovo prodotto aggiunto in precedenza usando l'istruzione [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) di Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-185">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="4cfd7-186">Nella finestra dell'**editor** eliminare la query precedente e immettere la query seguente:</span><span class="sxs-lookup"><span data-stu-id="4cfd7-186">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="4cfd7-187">Premere **CTRL+MAIUSC+E** per aggiornare la riga specificata nella tabella Product.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-187">Press **CTRL+SHIFT+E** to update the specified row in the Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="4cfd7-188">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="4cfd7-188">Delete data</span></span>

<span data-ttu-id="4cfd7-189">Usare il codice seguente per eliminare il nuovo prodotto aggiunto in precedenza usando l'istruzione [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) di Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-189">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4cfd7-190">Nella finestra dell'**editor** eliminare la query precedente e immettere la query seguente:</span><span class="sxs-lookup"><span data-stu-id="4cfd7-190">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="4cfd7-191">Premere **CTRL+MAIUSC+E** per eliminare la riga specificata nella tabella Product.</span><span class="sxs-lookup"><span data-stu-id="4cfd7-191">Press **CTRL+SHIFT+E** to delete the specified row in the Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cfd7-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4cfd7-192">Next steps</span></span>

- <span data-ttu-id="4cfd7-193">Per connettersi ed eseguire una query usando SQL Server Management Studio, vedere [Connettersi ed eseguire una query con SSMS](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="4cfd7-193">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="4cfd7-194">Per un articolo di MSDN Magazine sull'uso di Visual Studio Code, vedere il post di blog [Crea un IDE di database con estensione MSSQL](https://msdn.microsoft.com/magazine/mt809115).</span><span class="sxs-lookup"><span data-stu-id="4cfd7-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
