---
title: aaaDynamic SQL in SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="3337e-103">SQL dinamico in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3337e-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="3337e-104">Quando si sviluppa il codice dell'applicazione per SQL Data Warehouse è possibile necessario toouse sql dinamico toohelp soluzioni flessibili, generico e modulari.</span><span class="sxs-lookup"><span data-stu-id="3337e-104">When developing application code for SQL Data Warehouse you may need toouse dynamic sql toohelp deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="3337e-105">Attualmente SQL Data Warehouse non supporta i tipi di dati BLOB.</span><span class="sxs-lookup"><span data-stu-id="3337e-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="3337e-106">Tale condizione può limitare le dimensioni di hello stringhe come tipi di blob includono tipi varchar (max) e nvarchar (max).</span><span class="sxs-lookup"><span data-stu-id="3337e-106">This may limit hello size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="3337e-107">Se è stata usata questi tipi nel codice dell'applicazione durante la compilazione di stringhe molto grandi, è necessario codice hello toobreak in blocchi e l'istruzione EXEC hello di utilizzare invece.</span><span class="sxs-lookup"><span data-stu-id="3337e-107">If you have used these types in your application code when building very large strings, you will need toobreak hello code into chunks and use hello EXEC statement instead.</span></span>

<span data-ttu-id="3337e-108">Un semplice esempio:</span><span class="sxs-lookup"><span data-stu-id="3337e-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="3337e-109">Se la stringa hello è breve è possibile utilizzare [sp_executesql] [ sp_executesql] come di consueto.</span><span class="sxs-lookup"><span data-stu-id="3337e-109">If hello string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="3337e-110">Le istruzioni eseguite come istruzioni SQL dinamiche saranno ancora le regole di convalida dell'oggetto tooall TSQL.</span><span class="sxs-lookup"><span data-stu-id="3337e-110">Statements executed as dynamic SQL will still be subject tooall TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3337e-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3337e-111">Next steps</span></span>
<span data-ttu-id="3337e-112">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="3337e-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
