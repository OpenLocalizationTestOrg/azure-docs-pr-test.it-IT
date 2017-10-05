---
title: Uso di viste T-SQL in Azure SQL Data Warehouse | Documentazione Microsoft
description: Suggerimenti per l'uso di viste Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="0c187-103">Viste in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0c187-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="0c187-104">Le viste sono particolarmente utili in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0c187-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="0c187-105">Risultano utili in molti modi diversi per migliorare la qualità della soluzione.</span><span class="sxs-lookup"><span data-stu-id="0c187-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="0c187-106">Questo articolo contiene alcuni esempi che illustrano come migliorare la soluzione con le viste e le limitazioni da prendere in considerazione.</span><span class="sxs-lookup"><span data-stu-id="0c187-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="0c187-107">La sintassi per `CREATE VIEW` non viene illustrata in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="0c187-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="0c187-108">Per informazioni di riferimento, vedere l'articolo su [CREATE VIEW][CREATE VIEW] in MSDN.</span><span class="sxs-lookup"><span data-stu-id="0c187-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="0c187-109">Astrazione dell'architettura</span><span class="sxs-lookup"><span data-stu-id="0c187-109">Architectural abstraction</span></span>
<span data-ttu-id="0c187-110">Un modello di applicazione molto comune consiste nel ricreare le tabelle usando CREATE TABLE AS SELECT (CTAS) seguito da un modello di ridenominazione di oggetti durante il caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="0c187-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="0c187-111">L'esempio seguente aggiunge nuovi record a una dimensione data.</span><span class="sxs-lookup"><span data-stu-id="0c187-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="0c187-112">Si noti come viene creata una nuova tabella, DimDate_New, e poi rinominata per sostituire la versione originale della tabella.</span><span class="sxs-lookup"><span data-stu-id="0c187-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="0c187-113">Tuttavia, usando questo approccio la visualizzazione delle tabelle nella vista dell'utente potrebbe non essere costante e potrebbero essere restituiti messaggi di errore di tabella non esistente.</span><span class="sxs-lookup"><span data-stu-id="0c187-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="0c187-114">Le viste possono essere usate per garantire agli utenti un livello di presentazione coerente mentre vengono rinominati gli oggetti sottostanti.</span><span class="sxs-lookup"><span data-stu-id="0c187-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="0c187-115">Fornire agli utenti l'accesso ai dati tramite le viste significa che gli utenti non devono necessariamente avere la visibilità delle tabelle sottostanti.</span><span class="sxs-lookup"><span data-stu-id="0c187-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="0c187-116">Questo approccio garantisce la coerenza dell'esperienza utente e consente l'evoluzione del modello dati e l'ottimizzazione delle prestazioni da parte delle finestre di progettazione del data warehouse usando CTAS durante il processo di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="0c187-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="0c187-117">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="0c187-117">Performance optimization</span></span>
<span data-ttu-id="0c187-118">Le viste possono anche essere usate per creare join ottimizzati per le prestazioni tra le tabelle.</span><span class="sxs-lookup"><span data-stu-id="0c187-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="0c187-119">Ad esempio, una vista può incorporare una chiave di distribuzione ridondante come parte dei criteri di join per ridurre al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="0c187-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="0c187-120">Un altro vantaggio delle viste potrebbe essere l'applicazione di una query specifica o di un hint di join.</span><span class="sxs-lookup"><span data-stu-id="0c187-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="0c187-121">Usando le viste in questo modo, i join vengono sempre eseguiti in modo ottimale senza che gli utenti debbano ricordare il costrutto corretto per i relativi join.</span><span class="sxs-lookup"><span data-stu-id="0c187-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="0c187-122">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="0c187-122">Limitations</span></span>
<span data-ttu-id="0c187-123">Le viste in SQL Data Warehouse sono solo metadati.</span><span class="sxs-lookup"><span data-stu-id="0c187-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="0c187-124">Di conseguenza, le opzioni seguenti non sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="0c187-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="0c187-125">Non esiste alcuna opzione di binding dello schema</span><span class="sxs-lookup"><span data-stu-id="0c187-125">There is no schema binding option</span></span>
* <span data-ttu-id="0c187-126">Le tabelle di base non possono essere aggiornate tramite la vista</span><span class="sxs-lookup"><span data-stu-id="0c187-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="0c187-127">Non è possibile creare visualizzazioni sulle tabelle temporanee</span><span class="sxs-lookup"><span data-stu-id="0c187-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="0c187-128">Non è disponibile alcun supporto per gli hint EXPAND/NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="0c187-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="0c187-129">Non sono disponibili viste indicizzate in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0c187-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c187-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c187-130">Next steps</span></span>
<span data-ttu-id="0c187-131">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="0c187-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="0c187-132">Per la sintassi di `CREATE VIEW`, vedere [CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="0c187-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
