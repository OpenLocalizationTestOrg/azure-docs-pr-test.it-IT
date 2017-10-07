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
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a>Database SQL di Azure: Tooconnect ed eseguire query sui dati di utilizzare SQL Server Management Studio

[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server tooSQL Database per Microsoft Windows. Questa Guida introduttiva viene illustrato come database di SQL Azure toouse SSMS tooconnect tooan e tooquery istruzioni di utilizzo di Transact-SQL, inserire, aggiornare ed eliminare dati nel database di hello. 

## <a name="prerequisites"></a>Prerequisiti

Questa Guida introduttiva viene utilizzata come le risorse di hello punto iniziale create in una di queste guide introduttive:

- [Creare un database: portale](sql-database-get-started-portal.md)
- [Creare un database: interfaccia della riga di comando](sql-database-get-started-cli.md)
- [Creare un database: PowerShell](sql-database-get-started-powershell.md)

Prima di iniziare, verificare che è stata installata hello la versione più recente di [SSMS](https://msdn.microsoft.com/library/mt238290.aspx). 

## <a name="sql-server-connection-information"></a>Informazioni di connessione SQL Server

Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect. Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina. 
3. In hello **Panoramica** pagina per il database, esaminare hello nome completo del server, come illustrato nell'immagine di hello riportata di seguito. È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.

   ![informazioni di connessione](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se si hanno dimenticato di informazioni di accesso hello del server di Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello. 

## <a name="connect-tooyour-database"></a>La connessione a database tooyour

Utilizzare SQL Server Management Studio tooestablish un server di Database SQL di Azure tooyour di connessione. 

> [!IMPORTANT]
> Il server logico del database SQL di Azure è in ascolto sulla porta 1433. Se si sta tentando di tooconnect tooan Database SQL di Azure server logico all'interno di un firewall aziendale, questa porta deve essere aperta nel firewall aziendale hello per la connessione è toosuccessfully.
>

1. Aprire SQL Server Management Studio.

2. In hello **connettersi tooServer** finestra di dialogo immettere hello le seguenti informazioni:

   | Impostazione       | Valore consigliato | Descrizione | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo di server** | Motore di database | Questo valore è obbligatorio. |
   | **Server name** (Nome server) | nome completo del server Hello | Hello il nome deve essere simile al seguente: **mynewserver20170313.database.windows.net**. |
   | **Autenticazione** | Autenticazione di SQL Server | L'autenticazione di SQL è hello unico tipo di autenticazione che è stato configurato in questa esercitazione. |
   | **Accesso** | account amministratore di server Hello | Si tratta di hello con l'account specificato durante la creazione di server hello. |
   | **Password** | password Hello per l'account di amministratore del server | Si tratta hello password specificata durante la creazione di server hello. |

   ![connettersi tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. Fare clic su **opzioni** in hello **connettersi tooserver** la finestra di dialogo. In hello **connettersi toodatabase** immettere **mySampleDatabase** tooconnect toothis database.

   ![connettersi toodb nel server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Fare clic su **Connetti**. verrà visualizzata la finestra di Esplora oggetti Hello in SSMS. 

   ![tooserver connesso](./media/sql-database-connect-query-ssms/connected.png)  

5. In Esplora oggetti espandere **database** e quindi espandere **mySampleDatabase** oggetti hello tooview nel database di esempio hello.

## <a name="query-data"></a>Eseguire query sui dati

Tooquery per primi 20 prodotti di hello di codice seguente di hello utilizzare per categoria utilizzando hello [selezionare](https://msdn.microsoft.com/library/ms189499.aspx) istruzione Transact-SQL.

1. In Esplora oggetti fare clic con il pulsante destro del mouse su **mySampleDatabase** e scegliere **Nuova query**. Query vuota viene visualizzata una finestra che è connesso tooyour database.
2. Nella finestra query hello immettere hello seguente query:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. Sulla barra degli strumenti hello, fare clic su **Execute** tooretrieve dati da tabelle Product e ProductCategory hello.

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a>Inserire dati

Utilizzare hello di codice seguente tooinsert un nuovo prodotto nella tabella SalesLT.Product hello utilizzando hello [inserire](https://msdn.microsoft.com/library/ms174335.aspx) istruzione Transact-SQL.

1. Nella finestra query hello, sostituire la query precedente hello con hello seguente query:

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

2. Sulla barra degli strumenti hello, fare clic su **Execute** tooinsert una nuova riga nella tabella Product hello.

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a>Aggiornare i dati

Esempio di codice seguente di hello utilizzare nuovo prodotto hello tooupdate precedentemente aggiunto mediante hello [aggiornamento](https://msdn.microsoft.com/library/ms177523.aspx) istruzione Transact-SQL.

1. Nella finestra query hello, sostituire la query precedente hello con hello seguente query:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Sulla barra degli strumenti hello, fare clic su **Execute** riga specificata di hello tooupdate nella tabella Product hello.

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a>Eliminare i dati

Esempio di codice seguente di hello utilizzare nuovo prodotto hello toodelete precedentemente aggiunto mediante hello [eliminare](https://msdn.microsoft.com/library/ms189835.aspx) istruzione Transact-SQL.

1. Nella finestra query hello, sostituire la query precedente hello con hello seguente query:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Sulla barra degli strumenti hello, fare clic su **Execute** riga specificata di hello toodelete nella tabella Product hello.

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a>Passaggi successivi

- toolearn sulla creazione e gestione di server e i database con Transact-SQL, vedere [informazioni sul server di Database SQL di Azure e database](sql-database-servers-databases.md).
- Per informazioni su SSMS, vedere [Usare SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
- tooconnect e query tramite il codice di Visual Studio, vedere [Connect e query con codice di Visual Studio](sql-database-connect-query-vscode.md).
- tooconnect e query tramite .NET, vedere [Connect e query con .NET](sql-database-connect-query-dotnet.md).
- tooconnect e query tramite PHP, vedere [Connect e query con PHP](sql-database-connect-query-php.md).
- tooconnect e query tramite Node.js, vedere [Connect e query con Node.js](sql-database-connect-query-nodejs.md).
- tooconnect e query tramite Java, vedere [Connect e query con Java](sql-database-connect-query-java.md).
- tooconnect e query tramite Python, vedere [Connect e query con Python](sql-database-connect-query-python.md).
- tooconnect e query tramite Ruby, vedere [Connect e query con Ruby](sql-database-connect-query-ruby.md).
