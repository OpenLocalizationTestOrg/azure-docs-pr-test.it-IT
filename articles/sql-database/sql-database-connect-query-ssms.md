---
title: 'SSMS: Connettersi ed eseguire query sui dati nel database SQL di Azure | Microsoft Docs'
description: Informazioni su come tooconnect tooSQL Database in Azure utilizzando SQL Server Management Studio (SSMS). Quindi, eseguire istruzioni Transact-SQL (T-SQL) tooquery e modifica dati.
metacanonical: 
keywords: la connessione a database toosql, studio di gestione di sql server
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a><span data-ttu-id="c2cc0-105">Database SQL di Azure: Tooconnect ed eseguire query sui dati di utilizzare SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="c2cc0-105">Azure SQL Database: Use SQL Server Management Studio tooconnect and query data</span></span>

<span data-ttu-id="c2cc0-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server tooSQL Database per Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span> <span data-ttu-id="c2cc0-107">Questa Guida introduttiva viene illustrato come database di SQL Azure toouse SSMS tooconnect tooan e tooquery istruzioni di utilizzo di Transact-SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-107">This quick start demonstrates how toouse SSMS tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c2cc0-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c2cc0-108">Prerequisites</span></span>

<span data-ttu-id="c2cc0-109">Questa Guida introduttiva viene utilizzata come le risorse di hello punto iniziale create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="c2cc0-110">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="c2cc0-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="c2cc0-111">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="c2cc0-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="c2cc0-112">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2cc0-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="c2cc0-113">Prima di iniziare, verificare che è stata installata hello la versione più recente di [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-113">Before you start, make sure you have installed hello newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="c2cc0-114">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="c2cc0-114">SQL server connection information</span></span>

<span data-ttu-id="c2cc0-115">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="c2cc0-116">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="c2cc0-117">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c2cc0-118">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="c2cc0-119">In hello **Panoramica** pagina per il database, esaminare hello nome completo del server, come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello image below.</span></span> <span data-ttu-id="c2cc0-120">È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![informazioni di connessione](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="c2cc0-122">Se si hanno dimenticato di informazioni di accesso hello del server di Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-122">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="connect-tooyour-database"></a><span data-ttu-id="c2cc0-123">La connessione a database tooyour</span><span class="sxs-lookup"><span data-stu-id="c2cc0-123">Connect tooyour database</span></span>

<span data-ttu-id="c2cc0-124">Utilizzare SQL Server Management Studio tooestablish un server di Database SQL di Azure tooyour di connessione.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-124">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c2cc0-125">Il server logico del database SQL di Azure è in ascolto sulla porta 1433.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="c2cc0-126">Se si sta tentando di tooconnect tooan Database SQL di Azure server logico all'interno di un firewall aziendale, questa porta deve essere aperta nel firewall aziendale hello per la connessione è toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-126">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

1. <span data-ttu-id="c2cc0-127">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="c2cc0-128">In hello **connettersi tooServer** finestra di dialogo immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-128">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="c2cc0-129">Impostazione</span><span class="sxs-lookup"><span data-stu-id="c2cc0-129">Setting</span></span>       | <span data-ttu-id="c2cc0-130">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="c2cc0-130">Suggested value</span></span> | <span data-ttu-id="c2cc0-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c2cc0-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="c2cc0-132">**Tipo di server**</span><span class="sxs-lookup"><span data-stu-id="c2cc0-132">**Server type**</span></span> | <span data-ttu-id="c2cc0-133">Motore di database</span><span class="sxs-lookup"><span data-stu-id="c2cc0-133">Database engine</span></span> | <span data-ttu-id="c2cc0-134">Questo valore è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-134">This value is required.</span></span> |
   | <span data-ttu-id="c2cc0-135">**Server name** (Nome server)</span><span class="sxs-lookup"><span data-stu-id="c2cc0-135">**Server name**</span></span> | <span data-ttu-id="c2cc0-136">nome completo del server Hello</span><span class="sxs-lookup"><span data-stu-id="c2cc0-136">hello fully qualified server name</span></span> | <span data-ttu-id="c2cc0-137">Hello il nome deve essere simile al seguente: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-137">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="c2cc0-138">**Autenticazione**</span><span class="sxs-lookup"><span data-stu-id="c2cc0-138">**Authentication**</span></span> | <span data-ttu-id="c2cc0-139">Autenticazione di SQL Server</span><span class="sxs-lookup"><span data-stu-id="c2cc0-139">SQL Server Authentication</span></span> | <span data-ttu-id="c2cc0-140">L'autenticazione di SQL è hello unico tipo di autenticazione che è stato configurato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-140">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="c2cc0-141">**Accesso**</span><span class="sxs-lookup"><span data-stu-id="c2cc0-141">**Login**</span></span> | <span data-ttu-id="c2cc0-142">account amministratore di server Hello</span><span class="sxs-lookup"><span data-stu-id="c2cc0-142">hello server admin account</span></span> | <span data-ttu-id="c2cc0-143">Si tratta di hello con l'account specificato durante la creazione di server hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-143">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="c2cc0-144">**Password**</span><span class="sxs-lookup"><span data-stu-id="c2cc0-144">**Password**</span></span> | <span data-ttu-id="c2cc0-145">password Hello per l'account di amministratore del server</span><span class="sxs-lookup"><span data-stu-id="c2cc0-145">hello password for your server admin account</span></span> | <span data-ttu-id="c2cc0-146">Si tratta hello password specificata durante la creazione di server hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-146">This is hello password that you specified when you created hello server.</span></span> |

   ![connettersi tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="c2cc0-148">Fare clic su **opzioni** in hello **connettersi tooserver** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-148">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="c2cc0-149">In hello **connettersi toodatabase** immettere **mySampleDatabase** tooconnect toothis database.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-149">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![connettersi toodb nel server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="c2cc0-151">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-151">Click **Connect**.</span></span> <span data-ttu-id="c2cc0-152">verrà visualizzata la finestra di Esplora oggetti Hello in SSMS.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-152">hello Object Explorer window opens in SSMS.</span></span> 

   ![tooserver connesso](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="c2cc0-154">In Esplora oggetti espandere **database** e quindi espandere **mySampleDatabase** oggetti hello tooview nel database di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="c2cc0-155">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="c2cc0-155">Query data</span></span>

<span data-ttu-id="c2cc0-156">Tooquery per primi 20 prodotti di hello di codice seguente di hello utilizzare per categoria utilizzando hello [selezionare](https://msdn.microsoft.com/library/ms189499.aspx) istruzione Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-156">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="c2cc0-157">In Esplora oggetti fare clic con il pulsante destro del mouse su **mySampleDatabase** e scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="c2cc0-158">Query vuota viene visualizzata una finestra che è connesso tooyour database.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-158">A blank query window opens that is connected tooyour database.</span></span>
2. <span data-ttu-id="c2cc0-159">Nella finestra query hello immettere hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-159">In hello query window, enter hello following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="c2cc0-160">Sulla barra degli strumenti hello, fare clic su **Execute** tooretrieve dati da tabelle Product e ProductCategory hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-160">On hello toolbar, click **Execute** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="c2cc0-162">Inserire dati</span><span class="sxs-lookup"><span data-stu-id="c2cc0-162">Insert data</span></span>

<span data-ttu-id="c2cc0-163">Utilizzare hello di codice seguente tooinsert un nuovo prodotto nella tabella SalesLT.Product hello utilizzando hello [inserire](https://msdn.microsoft.com/library/ms174335.aspx) istruzione Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-163">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="c2cc0-164">Nella finestra query hello, sostituire la query precedente hello con hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-164">In hello query window, replace hello previous query with hello following query:</span></span>

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

2. <span data-ttu-id="c2cc0-165">Sulla barra degli strumenti hello, fare clic su **Execute** tooinsert una nuova riga nella tabella Product hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-165">On hello toolbar, click **Execute**  tooinsert a new row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="c2cc0-166">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="c2cc0-166">Update data</span></span>

<span data-ttu-id="c2cc0-167">Esempio di codice seguente di hello utilizzare nuovo prodotto hello tooupdate precedentemente aggiunto mediante hello [aggiornamento](https://msdn.microsoft.com/library/ms177523.aspx) istruzione Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-167">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="c2cc0-168">Nella finestra query hello, sostituire la query precedente hello con hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-168">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="c2cc0-169">Sulla barra degli strumenti hello, fare clic su **Execute** riga specificata di hello tooupdate nella tabella Product hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-169">On hello toolbar, click **Execute** tooupdate hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="c2cc0-170">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="c2cc0-170">Delete data</span></span>

<span data-ttu-id="c2cc0-171">Esempio di codice seguente di hello utilizzare nuovo prodotto hello toodelete precedentemente aggiunto mediante hello [eliminare](https://msdn.microsoft.com/library/ms189835.aspx) istruzione Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-171">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="c2cc0-172">Nella finestra query hello, sostituire la query precedente hello con hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-172">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="c2cc0-173">Sulla barra degli strumenti hello, fare clic su **Execute** riga specificata di hello toodelete nella tabella Product hello.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-173">On hello toolbar, click **Execute** toodelete hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="c2cc0-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2cc0-174">Next steps</span></span>

- <span data-ttu-id="c2cc0-175">toolearn sulla creazione e gestione di server e i database con Transact-SQL, vedere [informazioni sul server di Database SQL di Azure e database](sql-database-servers-databases.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-175">toolearn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="c2cc0-176">Per informazioni su SSMS, vedere [Usare SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="c2cc0-177">tooconnect e query tramite il codice di Visual Studio, vedere [Connect e query con codice di Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-177">tooconnect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="c2cc0-178">tooconnect e query tramite .NET, vedere [Connect e query con .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-178">tooconnect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="c2cc0-179">tooconnect e query tramite PHP, vedere [Connect e query con PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-179">tooconnect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="c2cc0-180">tooconnect e query tramite Node.js, vedere [Connect e query con Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-180">tooconnect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="c2cc0-181">tooconnect e query tramite Java, vedere [Connect e query con Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-181">tooconnect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="c2cc0-182">tooconnect e query tramite Python, vedere [Connect e query con Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-182">tooconnect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="c2cc0-183">tooconnect e query tramite Ruby, vedere [Connect e query con Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-183">tooconnect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
