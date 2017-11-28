---
title: dati di esempio aaaLoad in SQL Data Warehouse | Documenti Microsoft
description: Caricare i dati di esempio in SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="226a9-103">Caricare i dati di esempio in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="226a9-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="226a9-104">Seguire questi tooload semplici passaggi e i database di esempio Adventure Works hello di query.</span><span class="sxs-lookup"><span data-stu-id="226a9-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="226a9-105">Questi script innanzitutto utilizzano sqlcmd toorun SQL che verranno create tabelle e viste.</span><span class="sxs-lookup"><span data-stu-id="226a9-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="226a9-106">Dopo avere create le tabelle, gli script hello utilizzerà dati tooload bcp.</span><span class="sxs-lookup"><span data-stu-id="226a9-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="226a9-107">Se si dispone già sqlcmd e bcp installato, vedere i collegamenti seguenti troppo[installare bcp] [ install bcp] e troppo[installare sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="226a9-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="226a9-108">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="226a9-108">Load sample data</span></span>
1. <span data-ttu-id="226a9-109">Scaricare hello [script di esempio Adventure Works per SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] file zip.</span><span class="sxs-lookup"><span data-stu-id="226a9-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="226a9-110">Estrarre i file hello dalla directory tooa zip scaricato nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="226a9-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="226a9-111">Modificare aw_create.bat file hello estratto e impostare hello seguenti variabili presenti all'inizio di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="226a9-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="226a9-112">Non essere tooleave che spazi tra hello "=" e il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="226a9-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="226a9-113">Di seguito sono riportati alcuni esempi dell'aspetto che le modifiche potrebbero assumere.</span><span class="sxs-lookup"><span data-stu-id="226a9-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="226a9-114">Da un prompt di Windows, eseguire aw_create.bat hello modificato.</span><span class="sxs-lookup"><span data-stu-id="226a9-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="226a9-115">Assicurarsi che trovano nella directory hello in cui è salvata la versione modificata di aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="226a9-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="226a9-116">Questo script consentirà di eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="226a9-116">This script will...</span></span>
   
   * <span data-ttu-id="226a9-117">Eliminare le tabelle o le visualizzazioni Adventure Works già esistenti nel database</span><span class="sxs-lookup"><span data-stu-id="226a9-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="226a9-118">Creare viste e tabelle di Adventure Works hello</span><span class="sxs-lookup"><span data-stu-id="226a9-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="226a9-119">Caricare tutte le tabelle Adventure Works tramite bcp</span><span class="sxs-lookup"><span data-stu-id="226a9-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="226a9-120">Convalidare i conteggi delle righe per ogni tabella di Adventure Works hello</span><span class="sxs-lookup"><span data-stu-id="226a9-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="226a9-121">Raccogliere le statistiche per ogni colonna di ogni tabella Adventure Works</span><span class="sxs-lookup"><span data-stu-id="226a9-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="226a9-122">Eseguire query sui dati di esempio</span><span class="sxs-lookup"><span data-stu-id="226a9-122">Query sample data</span></span>
<span data-ttu-id="226a9-123">Dopo aver caricato alcuni dati di esempio in SQL Data Warehouse, è possibile eseguire rapidamente alcune query.</span><span class="sxs-lookup"><span data-stu-id="226a9-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="226a9-124">toorun una query, la connessione a database di Adventure Works tooyour appena creati nel data Warehouse di SQL Azure con Visual Studio e SSDT, come descritto in hello [query con Visual Studio] [ query with Visual Studio] documento.</span><span class="sxs-lookup"><span data-stu-id="226a9-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="226a9-125">Esempio di semplice selezionare istruzione tooget tutte le informazioni di hello dei dipendenti hello:</span><span class="sxs-lookup"><span data-stu-id="226a9-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="226a9-126">Esempio di una query più complessa utilizzando costrutti, ad esempio GROUP BY toolook alla quantità totale di hello per tutte le vendite ogni giorno:</span><span class="sxs-lookup"><span data-stu-id="226a9-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="226a9-127">Esempio di un'istruzione SELECT con una toofilter della clausola WHERE gli ordini da prima di una determinata data:</span><span class="sxs-lookup"><span data-stu-id="226a9-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="226a9-128">SQL Data Warehouse supporta quasi tutti i costrutti T-SQL supportati da SQL Server.</span><span class="sxs-lookup"><span data-stu-id="226a9-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="226a9-129">Eventuali differenze sono illustrate nella documentazione relativa alla [migrazione del codice][migrate code].</span><span class="sxs-lookup"><span data-stu-id="226a9-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="226a9-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="226a9-130">Next steps</span></span>
<span data-ttu-id="226a9-131">Ora che hai era un tootry possibilità alcune query con dati di esempio, estrarre come troppo[sviluppare][develop], [caricare][load], o [ eseguire la migrazione] [ migrate] tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="226a9-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
