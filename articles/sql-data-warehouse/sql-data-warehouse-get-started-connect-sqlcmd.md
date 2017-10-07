---
title: sqlcmd di SQL Data Warehouse tooAzure aaaConnect | Documenti Microsoft
description: "Utilizzare [sqlcmd] [sqlcmd] utilità della riga di comando tooconnect tooand query un Data Warehouse di SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>Connettersi tooSQL Data Warehouse con sqlcmd
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Utilizzare [sqlcmd] [ sqlcmd] tooand tooconnect utilità della riga di comando di query un Data Warehouse di SQL Azure.  

## <a name="1-connect"></a>1. Connettere
Introduzione tooget [sqlcmd][sqlcmd], aprire il prompt dei comandi di hello e immettere **sqlcmd** seguito dalla stringa di connessione hello per il database di SQL Data Warehouse. stringa di connessione di Hello richiede hello seguenti parametri:

* **Server (-S):** Server in formato hello `<`nome Server`>`. database.windows.net
* **Database (-d):** nome del database.
* **Abilita gli identificatori tra virgolette (-I):** gli identificatori tra virgolette devono essere l'istanza di SQL Data Warehouse tooa tooconnect abilitato.

toouse autenticazione di SQL Server, è necessario parametri nome utente e password di hello tooadd:

* **Utente (-U):** utente del Server in formato hello `<`utente`>`
* **Password (-P):** Password associata all'utente di hello.

Ad esempio, la stringa di connessione simile hello seguenti:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

l'autenticazione di Azure Active Directory Integrated toouse, è necessario parametri di tooadd hello Azure Active Directory:

* **Autenticazione di Azure Active Directory (-G):** consente di usare Azure Active Directory per l'autenticazione.

Ad esempio, la stringa di connessione simile hello seguenti:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> È necessario troppo[abilitare l'autenticazione di Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate utilizzando Active Directory.
> 
> 

## <a name="2-query"></a>2. Query
Dopo la connessione, è possibile eseguire le istruzioni Transact-SQL supportate hello istanza.  In questo esempio le query vengono inviate in modalità interattiva.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Questi esempi successivi mostrano come eseguire le query in modalità batch utilizzando l'opzione -Q hello o inviando tramite pipe il toosqlcmd SQL.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Passaggi successivi
Vedere [sqlcmd documentazione] [ sqlcmd] per ulteriori informazioni sui dettagli sulle opzioni di hello disponibili in sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
