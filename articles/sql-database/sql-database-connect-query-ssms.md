---
title: 'SSMS: Connettersi ed eseguire query sui dati nel database SQL di Azure | Microsoft Docs'
description: Informazioni su come connettersi a un database SQL in Azure tramite SQL Server Management Studio (SSMS). Eseguire quindi istruzioni Transact-SQL (T-SQL) per eseguire query sui dati e modificare questi ultimi.
metacanonical: 
keywords: connettersi al database sql,sql server management studio
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: Active
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 11/28/2017
ms.author: carlrab
ms.openlocfilehash: c60158c07fb517e12d73f9739286fe871afeca2e
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-to-connect-and-query-data"></a>Database SQL di Azure: usare SQL Server Management Studio per connettersi ed eseguire query sui dati

[SQL Server Management Studio][ssms-install-latest-84g] (SSMS) è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server al database SQL per Microsoft Windows. Questa guida introduttiva illustra come usare SSMS per connettersi a un database SQL di Azure e quindi usare istruzioni Transact-SQL per eseguire query e inserire, eliminare e aggiornare dati nel database. 

## <a name="prerequisites"></a>Prerequisiti

Questa guida introduttiva usa come punto di partenza le risorse create in una delle guide introduttive seguenti:

[!INCLUDE [prerequisites-create-db](../../includes/sql-database-connect-query-prerequisites-create-db-includes.md)]

#### <a name="install-the-latest-ssms"></a>Installare la versione di SSMS più recente

Prima di iniziare, assicurarsi di avere installato la versione più recente di [SSMS][ssms-install-latest-84g]. 

## <a name="sql-server-connection-information"></a>Informazioni di connessione SQL Server

[!INCLUDE [prerequisites-server-connection-info](../../includes/sql-database-connect-query-prerequisites-server-connection-info-includes.md)]

## <a name="connect-to-your-database"></a>Connettersi al database

Usare SQL Server Management Studio per stabilire una connessione al server del database SQL di Azure. 

> [!IMPORTANT]
> Il server logico del database SQL di Azure è in ascolto sulla porta 1433. Se si sta tentando di connettersi a un server logico del database SQL di Azure dall'interno di un firewall aziendale, questa porta deve essere aperta.
>

1. Aprire SQL Server Management Studio.

2. Nella finestra di dialogo **Connetti al server** immettere le informazioni seguenti:

   | Impostazione      | Valore consigliato    | Descrizione | 
   | ------------ | ------------------ | ----------- | 
   | **Tipo di server** | Motore di database | Questo valore è obbligatorio. |
   | **Server name** (Nome server) | Nome completo del server | Il nome sarà simile a: **mynewserver20170313.database.windows.net**. |
   | **Autenticazione** | Autenticazione di SQL Server | L'autenticazione SQL è il solo tipo di autenticazione configurato in questa esercitazione. |
   | **Accesso** | Account amministratore del server | Si tratta dell'account specificato quando è stato creato il server. |
   | **Password** | Password per l'account amministratore del server | Si tratta della password specificata quando è stato creato il server. |
   ||||

   ![connetti al server](./media/sql-database-connect-query-ssms/connect.png)  

3. Fare clic su **Opzioni** nella finestra di dialogo **Connetti al server**. Nella sezione **Connetti al database** immettere **mySampleDatabase** per connettersi a tale database.

   ![connettersi al database nel server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Fare clic su **Connetti**. La finestra Esplora oggetti viene visualizzata in SSMS. 

   ![connesso al server](./media/sql-database-connect-query-ssms/connected.png)  

5. In Esplora oggetti espandere **Database** e quindi espandere **mySampleDatabase** per visualizzare gli oggetti disponibili nel database di esempio.

## <a name="query-data"></a>Eseguire query sui dati

Usare il codice seguente per eseguire una query per individuare i primi 20 prodotti per categoria usando l'istruzione [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) di Transact-SQL.

1. In Esplora oggetti fare clic con il pulsante destro del mouse su **mySampleDatabase** e scegliere **Nuova query**. Viene visualizzata una finestra di query vuota, connessa al database.
2. Nella finestra delle query, immettere la query seguente:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. Sulla barra degli strumenti fare clic su **Esegui** per recuperare dati dalle tabelle Product e ProductCategory.

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a>Inserire dati

Usare il codice seguente per inserire un nuovo prodotto nella tabella SalesLT.Product usando l'istruzione [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) di Transact-SQL.

1. Nella finestra delle query, sostituire la query precedente con quella seguente:

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

2. Sulla barra degli strumenti fare clic su **Esegui** per inserire una nuova riga nella tabella Product.

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a>Aggiornare i dati

Usare il codice seguente per aggiornare il nuovo prodotto aggiunto in precedenza usando l'istruzione [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) di Transact-SQL.

1. Nella finestra delle query, sostituire la query precedente con quella seguente:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Sulla barra degli strumenti fare clic su **Esegui** per aggiornare la riga specificata nella tabella Product.

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a>Eliminare i dati

Usare il codice seguente per eliminare il nuovo prodotto aggiunto in precedenza usando l'istruzione [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) di Transact-SQL.

1. Nella finestra delle query, sostituire la query precedente con quella seguente:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Sulla barra degli strumenti fare clic su **Esegui** per eliminare la riga specificata nella tabella Product.

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sulla creazione e gestione di server e database con Transact-SQL, vedere [Informazioni su server e database del database SQL di Azure](sql-database-servers-databases.md).
- Per informazioni su SSMS, vedere [Usare SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).
- Per connettersi ed eseguire query tramite il portale di Azure, vedere [Connettersi ed eseguire query con l'editor di query SQL del portale di Azure](sql-database-connect-query-portal.md).
- Per connettersi ed eseguire query usando Visual Studio Code, vedere [Connettersi ed eseguire query con Visual Studio Code](sql-database-connect-query-vscode.md).
- Per connettersi ed eseguire query usando .NET, vedere [Connettersi ed eseguire query con .NET](sql-database-connect-query-dotnet.md).
- Per connettersi ed eseguire query usando PHP, vedere [Connettersi ed eseguire query con PHP](sql-database-connect-query-php.md).
- Per connettersi ed eseguire query usando Node.js, vedere [Connettersi ed eseguire query con Node.js](sql-database-connect-query-nodejs.md).
- Per connettersi ed eseguire query usando Java, vedere [Connettersi ed eseguire query con Java](sql-database-connect-query-java.md).
- Per connettersi ed eseguire query usando Python, vedere [Connettersi ed eseguire query con Python](sql-database-connect-query-python.md).
- Per connettersi ed eseguire query usando Ruby, vedere [Connettersi ed eseguire query con Ruby](sql-database-connect-query-ruby.md).


<!-- Article link references. -->

[ssms-install-latest-84g]: https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms

