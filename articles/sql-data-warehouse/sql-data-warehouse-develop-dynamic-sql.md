---
title: SQL dinamico in SQL Data Warehouse | Documentazione Microsoft
description: "Suggerimenti per l’utilizzo di SQL dinamico in SQL Data Warehouse di Azure per lo sviluppo di soluzioni."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 29228676373aee8dbc7b1b2a7d92ffc978333804
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="e6bc3-103">SQL dinamico in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e6bc3-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="e6bc3-104">Durante lo sviluppo di codice dell'applicazione per SQL Data Warehouse potrebbe essere necessario utilizzare SQL dinamico per offrire soluzioni flessibili, generiche e modulari.</span><span class="sxs-lookup"><span data-stu-id="e6bc3-104">When developing application code for SQL Data Warehouse you may need to use dynamic sql to help deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="e6bc3-105">Attualmente SQL Data Warehouse non supporta i tipi di dati BLOB.</span><span class="sxs-lookup"><span data-stu-id="e6bc3-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="e6bc3-106">Ciò potrebbe limitare le dimensioni delle stringhe poiché i tipi di BLOB includono tipi varchar(max) e nvarchar(max).</span><span class="sxs-lookup"><span data-stu-id="e6bc3-106">This may limit the size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="e6bc3-107">Se sono stati utilizzati questi tipi nel codice dell'applicazione durante la creazione di stringhe molto grandi, è necessario separare il codice in blocchi e utilizzare invece l'istruzione EXEC.</span><span class="sxs-lookup"><span data-stu-id="e6bc3-107">If you have used these types in your application code when building very large strings, you will need to break the code into chunks and use the EXEC statement instead.</span></span>

<span data-ttu-id="e6bc3-108">Un semplice esempio:</span><span class="sxs-lookup"><span data-stu-id="e6bc3-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="e6bc3-109">Se la stringa è breve, è possibile usare [sp_executesql][sp_executesql] come di consueto.</span><span class="sxs-lookup"><span data-stu-id="e6bc3-109">If the string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="e6bc3-110">Le istruzioni eseguite come SQL dinamico saranno ancora soggette a tutte le regole di convalida TSQL.</span><span class="sxs-lookup"><span data-stu-id="e6bc3-110">Statements executed as dynamic SQL will still be subject to all TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6bc3-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6bc3-111">Next steps</span></span>
<span data-ttu-id="e6bc3-112">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="e6bc3-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
