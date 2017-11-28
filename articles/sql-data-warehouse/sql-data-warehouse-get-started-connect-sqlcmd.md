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
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="3def0-103">Connettersi tooSQL Data Warehouse con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="3def0-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3def0-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="3def0-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="3def0-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3def0-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="3def0-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3def0-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="3def0-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="3def0-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="3def0-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="3def0-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="3def0-109">Utilizzare [sqlcmd] [ sqlcmd] tooand tooconnect utilità della riga di comando di query un Data Warehouse di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3def0-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="3def0-110">1. Connettere</span><span class="sxs-lookup"><span data-stu-id="3def0-110">1. Connect</span></span>
<span data-ttu-id="3def0-111">Introduzione tooget [sqlcmd][sqlcmd], aprire il prompt dei comandi di hello e immettere **sqlcmd** seguito dalla stringa di connessione hello per il database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3def0-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="3def0-112">stringa di connessione di Hello richiede hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="3def0-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="3def0-113">**Server (-S):** Server in formato hello `<`nome Server`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="3def0-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="3def0-114">**Database (-d):** nome del database.</span><span class="sxs-lookup"><span data-stu-id="3def0-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="3def0-115">**Abilita gli identificatori tra virgolette (-I):** gli identificatori tra virgolette devono essere l'istanza di SQL Data Warehouse tooa tooconnect abilitato.</span><span class="sxs-lookup"><span data-stu-id="3def0-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="3def0-116">toouse autenticazione di SQL Server, è necessario parametri nome utente e password di hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="3def0-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="3def0-117">**Utente (-U):** utente del Server in formato hello `<`utente`>`</span><span class="sxs-lookup"><span data-stu-id="3def0-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="3def0-118">**Password (-P):** Password associata all'utente di hello.</span><span class="sxs-lookup"><span data-stu-id="3def0-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="3def0-119">Ad esempio, la stringa di connessione simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3def0-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="3def0-120">l'autenticazione di Azure Active Directory Integrated toouse, è necessario parametri di tooadd hello Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="3def0-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="3def0-121">**Autenticazione di Azure Active Directory (-G):** consente di usare Azure Active Directory per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3def0-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="3def0-122">Ad esempio, la stringa di connessione simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3def0-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="3def0-123">È necessario troppo[abilitare l'autenticazione di Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate utilizzando Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3def0-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="3def0-124">2. Query</span><span class="sxs-lookup"><span data-stu-id="3def0-124">2. Query</span></span>
<span data-ttu-id="3def0-125">Dopo la connessione, è possibile eseguire le istruzioni Transact-SQL supportate hello istanza.</span><span class="sxs-lookup"><span data-stu-id="3def0-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="3def0-126">In questo esempio le query vengono inviate in modalità interattiva.</span><span class="sxs-lookup"><span data-stu-id="3def0-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="3def0-127">Questi esempi successivi mostrano come eseguire le query in modalità batch utilizzando l'opzione -Q hello o inviando tramite pipe il toosqlcmd SQL.</span><span class="sxs-lookup"><span data-stu-id="3def0-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="3def0-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3def0-128">Next steps</span></span>
<span data-ttu-id="3def0-129">Vedere [sqlcmd documentazione] [ sqlcmd] per ulteriori informazioni sui dettagli sulle opzioni di hello disponibili in sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="3def0-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
