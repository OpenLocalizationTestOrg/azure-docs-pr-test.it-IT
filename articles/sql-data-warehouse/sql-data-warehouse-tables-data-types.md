---
title: Linee guida per i tipi di dati - Azure SQL Data Warehouse | Microsoft Docs
description: Raccomandazioni per definire tipi di dati che siano compatibili con SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 5c24c71af16bd9851d9caf15fecfa4bb76f5f77e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="48bcb-103">Linee guida per la definizione dei tipi di dati per le tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="48bcb-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="48bcb-104">Usare queste raccomandazioni per definire tipi di dati per le tabelle che siano compatibili con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="48bcb-104">Use these recommendations to define table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="48bcb-105">Oltre a garantire la compatibilità, ridurre al minimo le dimensioni dei tipi di dati consente di migliorare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="48bcb-105">In addition to compatibility, minimizing the size of data types improves query performance.</span></span>

<span data-ttu-id="48bcb-106">SQL Data Warehouse supporta i tipi di dati più diffusi.</span><span class="sxs-lookup"><span data-stu-id="48bcb-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="48bcb-107">Per un elenco dei tipi di dati supportati, vedere [tipi di dati](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) nell'istruzione CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="48bcb-107">For a list of the supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in the CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="48bcb-108">Ridurre al minimo la lunghezza di riga</span><span class="sxs-lookup"><span data-stu-id="48bcb-108">Minimize row length</span></span>
<span data-ttu-id="48bcb-109">Ridurre al minimo le dimensioni dei tipi di dati consente di ridurre la lunghezza di riga, con conseguenti prestazioni migliori per le query.</span><span class="sxs-lookup"><span data-stu-id="48bcb-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="48bcb-110">Usare il tipo di dati più piccolo adatto ai dati.</span><span class="sxs-lookup"><span data-stu-id="48bcb-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="48bcb-111">Evitare di definire le colonne di tipo carattere con una lunghezza predefinita elevata.</span><span class="sxs-lookup"><span data-stu-id="48bcb-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="48bcb-112">Ad esempio, se il valore più lungo è 25 caratteri, definire la colonna come VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="48bcb-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="48bcb-113">Evitare di usare [NVARCHAR][NVARCHAR] quando serve solo VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="48bcb-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="48bcb-114">Quando possibile, usare NVARCHAR(4000) o VARCHAR(8000) invece di NVARCHAR(MAX) o VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="48bcb-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="48bcb-115">Se si usa Polybase per caricare le tabelle, la lunghezza definita per la riga della tabella non può essere maggiore di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="48bcb-115">If you are using Polybase to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="48bcb-116">Quando una riga con dati di lunghezza variabile supera 1 MB, è possibile caricare la riga con BCP, ma non con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="48bcb-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="48bcb-117">Identificare i tipi di dati non supportati</span><span class="sxs-lookup"><span data-stu-id="48bcb-117">Identify unsupported data types</span></span>
<span data-ttu-id="48bcb-118">Se si esegue la migrazione del database da un altro database SQL, durante la migrazione è possibile riscontrare tipi di dati non supportati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="48bcb-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="48bcb-119">Usare questa query per individuare i tipi di dati non supportati nello schema SQL esistente.</span><span class="sxs-lookup"><span data-stu-id="48bcb-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="48bcb-120"><a name="unsupported-data-types"></a>Usare alternative per i tipi di dati non supportati</span><span class="sxs-lookup"><span data-stu-id="48bcb-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="48bcb-121">L'elenco seguente mostra i tipi di dati non supportati da SQL Data Warehouse e indica le alternative utilizzabili al posto dei tipi di dati non supportati.</span><span class="sxs-lookup"><span data-stu-id="48bcb-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="48bcb-122">Tipo di dati non supportati</span><span class="sxs-lookup"><span data-stu-id="48bcb-122">Unsupported data type</span></span> | <span data-ttu-id="48bcb-123">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="48bcb-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="48bcb-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="48bcb-124">[geometry][geometry]</span></span> |<span data-ttu-id="48bcb-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="48bcb-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="48bcb-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="48bcb-126">[geography][geography]</span></span> |<span data-ttu-id="48bcb-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="48bcb-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="48bcb-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="48bcb-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="48bcb-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="48bcb-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="48bcb-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="48bcb-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="48bcb-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="48bcb-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="48bcb-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="48bcb-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="48bcb-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="48bcb-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="48bcb-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="48bcb-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="48bcb-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="48bcb-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="48bcb-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="48bcb-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="48bcb-137">Dividere la colonna in più colonne fortemente tipizzate.</span><span class="sxs-lookup"><span data-stu-id="48bcb-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="48bcb-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="48bcb-138">[table][table]</span></span> |<span data-ttu-id="48bcb-139">Convertire in tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="48bcb-139">Convert to temporary tables.</span></span> |
| <span data-ttu-id="48bcb-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="48bcb-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="48bcb-141">Rielaborare il codice per l'uso di [datetime2][datetime2] e della funzione `CURRENT_TIMESTAMP`.</span><span class="sxs-lookup"><span data-stu-id="48bcb-141">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="48bcb-142">Solo le costanti sono supportate come valori predefiniti, quindi non è possibile definire current_timestamp come vincolo predefinito.</span><span class="sxs-lookup"><span data-stu-id="48bcb-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="48bcb-143">Se è necessario eseguire la migrazione di valori della versione di riga da una colonna di tipo timestamp, usare [BINARY][BINARY](8) o [VARBINARY][BINARY](8) per valori della versione di riga NOT NULL o NULL.</span><span class="sxs-lookup"><span data-stu-id="48bcb-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="48bcb-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="48bcb-144">[xml][xml]</span></span> |<span data-ttu-id="48bcb-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="48bcb-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="48bcb-146">[tipo definito dall'utente (UDT)][user defined types]</span><span class="sxs-lookup"><span data-stu-id="48bcb-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="48bcb-147">Riconvertire nel tipo di dati nativo, se possibile.</span><span class="sxs-lookup"><span data-stu-id="48bcb-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="48bcb-148">valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="48bcb-148">default values</span></span> | <span data-ttu-id="48bcb-149">I valori predefiniti supportano solo valori letterali e costanti.</span><span class="sxs-lookup"><span data-stu-id="48bcb-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="48bcb-150">Le espressioni o le funzioni non deterministiche, ad esempio `GETDATE()` o `CURRENT_TIMESTAMP`, non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="48bcb-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="48bcb-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48bcb-151">Next steps</span></span>
<span data-ttu-id="48bcb-152">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="48bcb-152">To learn more, see:</span></span>

- <span data-ttu-id="48bcb-153">[Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="48bcb-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="48bcb-154">[Panoramica delle tabelle][Overview]</span><span class="sxs-lookup"><span data-stu-id="48bcb-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="48bcb-155">[Distribuzione di una tabella][Distribute]</span><span class="sxs-lookup"><span data-stu-id="48bcb-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="48bcb-156">[Indicizzazione di una tabella][Index]</span><span class="sxs-lookup"><span data-stu-id="48bcb-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="48bcb-157">[Partizionamento di una tabella][Partition]</span><span class="sxs-lookup"><span data-stu-id="48bcb-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="48bcb-158">[Gestire le statistiche delle tabelle][Statistics]</span><span class="sxs-lookup"><span data-stu-id="48bcb-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="48bcb-159">[Tabelle temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="48bcb-159">[Temporary Tables][Temporary]</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
