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
# <a name="use-python-tooquery-an-azure-sql-database"></a>Utilizzare Python tooquery un database SQL di Azure

 Questa Guida introduttiva illustra come toouse [Python](https://python.org) tooconnect tooan Azure SQL database e utilizzare dati tooquery di istruzioni Transact-SQL.

## <a name="prerequisites"></a>Prerequisiti

Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere seguito hello:

- un database SQL di Azure. Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive: 

   - [Creare un database: portale](sql-database-get-started-portal.md)
   - [Creare un database: interfaccia della riga di comando](sql-database-get-started-cli.md)
   - [Creare un database: PowerShell](sql-database-get-started-powershell.md)

- Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.

- Avere installato Python e il software correlato per il sistema operativo.

    - **MacOS**: installare Homebrew e Python, installare il driver ODBC hello e SQLCMD e quindi hello Python Driver per SQL Server. Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).
    - **Ubuntu**: installare Python e altri necessari pacchetti, quindi installare hello Python Driver per SQL Server. Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).
    - **Windows**: installare una versione più recente di hello di Python (variabile di ambiente è ora configurata per l'utente), installare il driver ODBC hello e SQLCMD e quindi installare hello Python Driver per SQL Server. Vedere i [passaggi 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/). 

## <a name="sql-server-connection-information"></a>Informazioni di connessione SQL Server

Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect. Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina. 
3. In hello **Panoramica** pagina per il database, revisione hello nome completo del server come illustrato nella seguente immagine hello. È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se si dimentica le informazioni di accesso del server, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello.     
    
## <a name="insert-code-tooquery-sql-database"></a>Inserire codice tooquery SQL database 

1. Nell'editor di testo preferito creare un nuovo file, **sqltest.py**.  

2. Sostituire il contenuto di hello con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.

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

## <a name="run-hello-code"></a>Eseguire il codice hello

1. Al prompt dei comandi di hello, eseguire hello seguenti comandi:

   ```Python
   python sqltest.py
   ```

2. Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.

## <a name="next-steps"></a>Passaggi successivi

- [Progettare il primo database SQL di Azure](sql-database-design-first-database.md)
- [Driver Microsoft Python per SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [Centro per sviluppatori Python](https://azure.microsoft.com/develop/python/?v=17.23h)

