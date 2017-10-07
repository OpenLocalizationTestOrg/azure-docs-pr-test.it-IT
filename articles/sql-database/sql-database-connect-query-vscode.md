---
title: 'Visual Studio Code: Connettersi ed eseguire query sui dati nel database SQL di Azure | Microsoft Docs'
description: Informazioni su come tooconnect tooSQL Database in Azure utilizzando Visual Studio Code. Quindi, eseguire istruzioni Transact-SQL (T-SQL) tooquery e modifica dati.
metacanonical: 
keywords: la connessione a database toosql
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
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>Database SQL di Azure: Tooconnect ed eseguire query sui dati di utilizzare Visual Studio Code

[Codice di Visual Studio](https://code.visualstudio.com/docs) è un editor di codice con interfaccia grafica per Linux, macOS, e Windows che supporti le estensioni, tra cui hello [estensione mssql](https://aka.ms/mssql-marketplace) per le query di Microsoft SQL Server, Database SQL di Azure e SQL Data Warehouse. Questa Guida introduttiva viene illustrato come database di SQL Azure tooan tooconnect codice di Visual Studio toouse e tooquery istruzioni di utilizzo di Transact-SQL, inserire, aggiornare ed eliminare dati nel database di hello.

## <a name="prerequisites"></a>Prerequisiti

Questa Guida introduttiva viene utilizzata come le risorse di hello punto iniziale create in una di queste guide introduttive:

- [Creare un database: portale](sql-database-get-started-portal.md)
- [Creare un database: interfaccia della riga di comando](sql-database-get-started-cli.md)
- [Creare un database: PowerShell](sql-database-get-started-powershell.md)

Prima di iniziare, verificare che è stata installata hello la versione più recente di [codice di Visual Studio](https://code.visualstudio.com/Download) e hello caricati [mssql estensione](https://aka.ms/mssql-marketplace). Per istruzioni di installazione per l'estensione mssql hello, vedere [installare Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) e vedere [mssql per Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

## <a name="configure-vs-code"></a>Configurare Visual Studio Code 

### <a name="mac-os"></a>**Mac OS**
Per macOS, è necessario tooinstall OpenSSL ovvero prerequisiti per DotNet tale estensione mssql utilizzata. Aprire terminale e immettere i seguenti comandi tooinstall hello **brew** e **OpenSSL**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

Non è necessaria alcuna configurazione speciale.

### <a name="windows"></a>**Windows**

Non è necessaria alcuna configurazione speciale.

## <a name="sql-server-connection-information"></a>Informazioni di connessione SQL Server

Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect. Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina. 
3. In hello **Panoramica** pagina per il database, revisione hello nome completo del server come illustrato nella seguente immagine hello. È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.

   ![informazioni di connessione](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se si hanno dimenticato di informazioni di accesso hello del server di Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello. 

## <a name="set-language-mode-toosql"></a>Set language modalità tooSQL

Impostare la modalità di linguaggio hello è troppo**SQL** in T-SQL IntelliSense e di comandi di Visual Studio Code tooenable mssql.

1. Aprire una nuova finestra di Visual Studio Code. 

2. Fare clic su **testo normale** in hello angolo inferiore destro della barra di stato hello.
3. In hello **la modalità di selezione lingua** dal menu a discesa che consente di aprire, digitare **SQL**, quindi premere **invio** tooset hello language modalità tooSQL. 

   ![Modalità linguaggio SQL](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>La connessione a database tooyour

Utilizzare Visual Studio Code tooestablish un server di Database SQL di Azure tooyour di connessione.

> [!IMPORTANT]
> Prima di continuare, assicurarsi di avere a portata di mano le informazioni su server, database e account di accesso. Dopo l'inizio di immissione di informazioni sul profilo di connessione hello, se si modifica lo stato attivo dal codice di Visual Studio, è necessario toorestart Creazione profilo di connessione hello.
>

1. Nel codice di Visual Studio, premere **CTRL + MAIUSC + P** (o **F1**) tooopen hello riquadro comandi.

2. Digitare **sqlcon** e premere **INVIO**.

3. Premere **invio** tooselect **Crea profilo di connessione**. Verrà creato un profilo di connessione per l'istanza di SQL Server.

4. Seguire hello richieste toospecify hello le proprietà di connessione per il nuovo profilo di connessione hello. Dopo aver specificato ogni valore, premere **invio** toocontinue. 

   | Impostazione       | Valore consigliato | Descrizione |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome server | nome completo del server Hello | Hello il nome deve essere simile al seguente: **mynewserver20170313.database.windows.net**. |
   | **Database name** (Nome database) | mySampleDatabase | nome Hello di hello database toowhich tooconnect. |
   | **Autenticazione** | Account di accesso SQL| L'autenticazione di SQL è hello unico tipo di autenticazione che è stato configurato in questa esercitazione. |
   | **Nome utente** | account amministratore di server Hello | Si tratta di hello con l'account specificato durante la creazione di server hello. |
   | **Password (SQL Login)** (Password - Account di accesso SQL) | password Hello per l'account di amministratore del server | Si tratta hello password specificata durante la creazione di server hello. |
   | **Save Password?** (Salvare la password?) | Sì o No | Selezionare Sì se non si desidera che la password di hello tooenter ogni volta. |
   | **Immettere un nome per questo profilo** | Nome del profilo, ad esempio **mySampleDatabase** | Un nome del profilo salvato velocizza la connessione agli accessi successivi. | 

5. Hello premere **ESC** chiave tooclose informazioni sul messaggio che informa che il profilo di hello è creato e collegato.

6. Verificare la connessione nella barra di stato hello.

   ![Stato della connessione](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>Eseguire query sui dati

Tooquery per primi 20 prodotti di hello di codice seguente di hello utilizzare per categoria utilizzando hello [selezionare](https://msdn.microsoft.com/library/ms189499.aspx) istruzione Transact-SQL.

1. In hello **Editor** finestra immettere hello query nella finestra query vuota hello seguenti:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. Premere **CTRL + MAIUSC + E** tooretrieve dati da tabelle Product e ProductCategory hello.

    ![Query](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>Inserire dati

Utilizzare hello di codice seguente tooinsert un nuovo prodotto nella tabella SalesLT.Product hello utilizzando hello [inserire](https://msdn.microsoft.com/library/ms174335.aspx) istruzione Transact-SQL.

1. In hello **Editor** finestra, eliminare la query precedente hello e immettere hello seguente query:

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

2. Premere **CTRL + MAIUSC + E** tooinsert una nuova riga nella tabella Product hello.

## <a name="update-data"></a>Aggiornare i dati

Esempio di codice seguente di hello utilizzare nuovo prodotto hello tooupdate precedentemente aggiunto mediante hello [aggiornamento](https://msdn.microsoft.com/library/ms177523.aspx) istruzione Transact-SQL.

1.  In hello **Editor** finestra, eliminare la query precedente hello e immettere hello seguente query:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Premere **CTRL + MAIUSC + E** tooupdate riga specificata di hello nella tabella Product hello.

## <a name="delete-data"></a>Eliminare i dati

Esempio di codice seguente di hello utilizzare nuovo prodotto hello toodelete precedentemente aggiunto mediante hello [eliminare](https://msdn.microsoft.com/library/ms189835.aspx) istruzione Transact-SQL.

1. In hello **Editor** finestra, eliminare la query precedente hello e immettere hello seguente query:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Premere **CTRL + MAIUSC + E** toodelete riga specificata di hello nella tabella Product hello.

## <a name="next-steps"></a>Passaggi successivi

- tooconnect e query tramite SQL Server Management Studio, vedere [Connect e query con SQL Server Management Studio](sql-database-connect-query-ssms.md).
- Per un articolo di MSDN Magazine sull'uso di Visual Studio Code, vedere il post di blog [Crea un IDE di database con estensione MSSQL](https://msdn.microsoft.com/magazine/mt809115).
