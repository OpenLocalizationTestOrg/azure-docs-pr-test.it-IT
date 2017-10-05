---
title: Connettersi ad Azure SQL Data Warehouse con sqlcmd | Documentazione Microsoft
description: "Usare l'utilità della riga di comando [sqlcmd][sqlcmd] per connettersi ed eseguire query in un'istanza di Azure SQL Data Warehouse."
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
ms.openlocfilehash: 5a3fe1046c3417070ba8ff5bd18a0485e2152eff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="6332f-103">Connettersi a SQL Data Warehouse con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="6332f-103">Connect to SQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6332f-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="6332f-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="6332f-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6332f-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="6332f-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6332f-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="6332f-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="6332f-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="6332f-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="6332f-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="6332f-109">Usare l'utilità della riga di comando [sqlcmd][sqlcmd] per connettersi ed eseguire query in un'istanza di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6332f-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="6332f-110">1. Connettere</span><span class="sxs-lookup"><span data-stu-id="6332f-110">1. Connect</span></span>
<span data-ttu-id="6332f-111">Per iniziare a usare [sqlcmd][sqlcmd], aprire il prompt dei comandi e immettere **sqlcmd** seguito dalla stringa di connessione per il database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6332f-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="6332f-112">La stringa di connessione richiede i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="6332f-112">The connection string requires the following parameters:</span></span>

* <span data-ttu-id="6332f-113">**Server (-S):** server nel formato `<`Server Name`>`.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="6332f-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="6332f-114">**Database (-d):** nome del database.</span><span class="sxs-lookup"><span data-stu-id="6332f-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="6332f-115">**Abilita identificatori delimitati (-I):** gli identificatori delimitati devono essere abilitati per consentire la connessione a un'istanza di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6332f-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span></span>

<span data-ttu-id="6332f-116">Per usare l'autenticazione di SQL Server è necessario aggiungere i parametri nome utente e password:</span><span class="sxs-lookup"><span data-stu-id="6332f-116">To use SQL Server Authentication, you need to add the username/password parameters:</span></span>

* <span data-ttu-id="6332f-117">**Utente (-U):** utente del server nel formato `<`User`>`</span><span class="sxs-lookup"><span data-stu-id="6332f-117">**User (-U):** Server user in the form `<`User`>`</span></span>
* <span data-ttu-id="6332f-118">**Password (-P):** password associata all'utente.</span><span class="sxs-lookup"><span data-stu-id="6332f-118">**Password (-P):** Password associated with the user.</span></span>

<span data-ttu-id="6332f-119">Ad esempio, la stringa di connessione sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="6332f-119">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="6332f-120">Per usare l'autenticazione integrata di Azure Active Directory è necessario aggiungere i parametri di Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="6332f-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span></span>

* <span data-ttu-id="6332f-121">**Autenticazione di Azure Active Directory (-G):** consente di usare Azure Active Directory per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="6332f-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="6332f-122">Ad esempio, la stringa di connessione sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="6332f-122">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="6332f-123">Per eseguire l'autenticazione tramite Active Directory, è necessario [abilitare l'autenticazione di Azure Active Directory](sql-data-warehouse-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="6332f-123">You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="6332f-124">2. Query</span><span class="sxs-lookup"><span data-stu-id="6332f-124">2. Query</span></span>
<span data-ttu-id="6332f-125">Dopo la connessione sarà possibile eseguire qualsiasi istruzione Transact-SQL supportata nell'istanza.</span><span class="sxs-lookup"><span data-stu-id="6332f-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span></span>  <span data-ttu-id="6332f-126">In questo esempio le query vengono inviate in modalità interattiva.</span><span class="sxs-lookup"><span data-stu-id="6332f-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="6332f-127">Questi esempi successivi illustrano come è possibile eseguire le query in modalità batch usando l'opzione -Q o inviando pipe di SQL a sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="6332f-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="6332f-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6332f-128">Next steps</span></span>
<span data-ttu-id="6332f-129">Per altre informazioni sulle opzioni disponibili in sqlcmd, vedere la [documentazione di sqlcmd][sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="6332f-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
