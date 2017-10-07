---
title: aaaData tipi riferimento - Azure SQL Data Warehouse | Documenti Microsoft
description: I tipi di dati toodefine indicazioni sono compatibili con SQL Data Warehouse.
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
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="77e79-103">Linee guida per la definizione dei tipi di dati per le tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="77e79-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="77e79-104">Utilizzare questi tipi di dati nella tabella di toodefine indicazioni che sono compatibili con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="77e79-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="77e79-105">Inoltre toocompatibility, riducendo al minimo le dimensioni di hello dei tipi di dati consente di migliorare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="77e79-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="77e79-106">SQL Data Warehouse supporta i tipi di dati hello comunemente utilizzato.</span><span class="sxs-lookup"><span data-stu-id="77e79-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="77e79-107">Per un elenco di tipi di dati hello supportato, vedere [tipi di dati](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello istruzione CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="77e79-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="77e79-108">Ridurre al minimo la lunghezza di riga</span><span class="sxs-lookup"><span data-stu-id="77e79-108">Minimize row length</span></span>
<span data-ttu-id="77e79-109">Ridurre al minimo le dimensioni di hello dei tipi di dati, lunghezza di riga hello, ottenendo le prestazioni delle query toobetter si riduce.</span><span class="sxs-lookup"><span data-stu-id="77e79-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="77e79-110">Utilizzare il tipo di dati più piccolo hello che funziona per i dati.</span><span class="sxs-lookup"><span data-stu-id="77e79-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="77e79-111">Evitare di definire le colonne di tipo carattere con una lunghezza predefinita elevata.</span><span class="sxs-lookup"><span data-stu-id="77e79-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="77e79-112">Ad esempio, se più lungo valore hello è di 25 caratteri, quindi definire la colonna come VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="77e79-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="77e79-113">Evitare di usare [NVARCHAR][NVARCHAR] quando serve solo VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="77e79-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="77e79-114">Quando possibile, usare NVARCHAR(4000) o VARCHAR(8000) invece di NVARCHAR(MAX) o VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="77e79-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="77e79-115">Se si utilizza Polybase tooload le tabelle, la lunghezza definita hello hello di riga della tabella non può superare 1 MB.</span><span class="sxs-lookup"><span data-stu-id="77e79-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="77e79-116">Quando una riga con dati a lunghezza variabile supera 1 MB, è possibile caricare riga hello BCP, ma non con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="77e79-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="77e79-117">Identificare i tipi di dati non supportati</span><span class="sxs-lookup"><span data-stu-id="77e79-117">Identify unsupported data types</span></span>
<span data-ttu-id="77e79-118">Se si esegue la migrazione del database da un altro database SQL, durante la migrazione è possibile riscontrare tipi di dati non supportati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="77e79-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="77e79-119">Utilizzare questa query toodiscover non supportati i tipi di dati nello schema SQL esistente.</span><span class="sxs-lookup"><span data-stu-id="77e79-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="77e79-120"><a name="unsupported-data-types"></a>Usare alternative per i tipi di dati non supportati</span><span class="sxs-lookup"><span data-stu-id="77e79-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="77e79-121">Hello elenco riportato di seguito viene illustrato hello tipi di dati che non supporta SQL Data Warehouse e offre alternative che è possibile usare invece hello non supportati i tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="77e79-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="77e79-122">Tipo di dati non supportati</span><span class="sxs-lookup"><span data-stu-id="77e79-122">Unsupported data type</span></span> | <span data-ttu-id="77e79-123">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="77e79-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="77e79-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="77e79-124">[geometry][geometry]</span></span> |<span data-ttu-id="77e79-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="77e79-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="77e79-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="77e79-126">[geography][geography]</span></span> |<span data-ttu-id="77e79-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="77e79-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="77e79-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="77e79-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="77e79-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="77e79-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="77e79-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="77e79-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="77e79-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="77e79-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="77e79-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="77e79-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="77e79-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="77e79-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="77e79-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="77e79-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="77e79-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="77e79-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="77e79-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="77e79-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="77e79-137">Dividere la colonna in più colonne fortemente tipizzate.</span><span class="sxs-lookup"><span data-stu-id="77e79-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="77e79-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="77e79-138">[table][table]</span></span> |<span data-ttu-id="77e79-139">Convertire tabelle tootemporary.</span><span class="sxs-lookup"><span data-stu-id="77e79-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="77e79-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="77e79-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="77e79-141">Rielaborazione codice toouse [datetime2] [ datetime2] e `CURRENT_TIMESTAMP` (funzione).</span><span class="sxs-lookup"><span data-stu-id="77e79-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="77e79-142">Solo le costanti sono supportate come valori predefiniti, quindi non è possibile definire current_timestamp come vincolo predefinito.</span><span class="sxs-lookup"><span data-stu-id="77e79-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="77e79-143">Se è necessario toomigrate valori di versione di riga da una colonna tipizzata timestamp, quindi utilizzare [binario][BINARY](8) o [VARBINARY][BINARY](8) per NOT NULL o I valori di versione di riga è NULL.</span><span class="sxs-lookup"><span data-stu-id="77e79-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="77e79-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="77e79-144">[xml][xml]</span></span> |<span data-ttu-id="77e79-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="77e79-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="77e79-146">[tipo definito dall'utente (UDT)][user defined types]</span><span class="sxs-lookup"><span data-stu-id="77e79-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="77e79-147">Convertire il tipo di dati nativi toohello indietro quando possibile.</span><span class="sxs-lookup"><span data-stu-id="77e79-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="77e79-148">valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="77e79-148">default values</span></span> | <span data-ttu-id="77e79-149">I valori predefiniti supportano solo valori letterali e costanti.</span><span class="sxs-lookup"><span data-stu-id="77e79-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="77e79-150">Le espressioni o le funzioni non deterministiche, ad esempio `GETDATE()` o `CURRENT_TIMESTAMP`, non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="77e79-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="77e79-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77e79-151">Next steps</span></span>
<span data-ttu-id="77e79-152">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="77e79-152">toolearn more, see:</span></span>

- <span data-ttu-id="77e79-153">[Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="77e79-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="77e79-154">[Panoramica delle tabelle][Overview]</span><span class="sxs-lookup"><span data-stu-id="77e79-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="77e79-155">[Distribuzione di una tabella][Distribute]</span><span class="sxs-lookup"><span data-stu-id="77e79-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="77e79-156">[Indicizzazione di una tabella][Index]</span><span class="sxs-lookup"><span data-stu-id="77e79-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="77e79-157">[Partizionamento di una tabella][Partition]</span><span class="sxs-lookup"><span data-stu-id="77e79-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="77e79-158">[Gestire le statistiche delle tabelle][Statistics]</span><span class="sxs-lookup"><span data-stu-id="77e79-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="77e79-159">[Tabelle temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="77e79-159">[Temporary Tables][Temporary]</span></span>

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
