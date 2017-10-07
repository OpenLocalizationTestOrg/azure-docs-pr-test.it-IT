---
title: viste aaaUsing T-SQL in Azure SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="c9677-103">Viste in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c9677-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="c9677-104">Le viste sono particolarmente utili in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c9677-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="c9677-105">Possono essere utilizzati in numerosi modi diversi tooimprove hello di qualità della soluzione.</span><span class="sxs-lookup"><span data-stu-id="c9677-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="c9677-106">In questo articolo sono illustrati alcuni esempi di come tooenrich la soluzione con le visualizzazioni, oltre alle limitazioni di hello necessarie toobe considerati.</span><span class="sxs-lookup"><span data-stu-id="c9677-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="c9677-107">La sintassi per `CREATE VIEW` non viene illustrata in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c9677-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="c9677-108">Consultare toohello [CREATE VIEW] [ CREATE VIEW] articolo in MSDN per queste informazioni di riferimento.</span><span class="sxs-lookup"><span data-stu-id="c9677-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="c9677-109">Astrazione dell'architettura</span><span class="sxs-lookup"><span data-stu-id="c9677-109">Architectural abstraction</span></span>
<span data-ttu-id="c9677-110">Uno schema molto comune di applicazione è toore-creare le tabelle mediante creazione tabella AS selezionare (un'istruzione CTAS) seguito da un oggetto ridenominazione modello durante il caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="c9677-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="c9677-111">esempio Hello seguente aggiunge una nuova record tooa data dimensione Data.</span><span class="sxs-lookup"><span data-stu-id="c9677-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="c9677-112">Si noti come un nuovo tabble, DimDate_New, viene creato e quindi rinominato versione originale di hello tooreplace della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="c9677-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="c9677-113">Tuttavia, usando questo approccio la visualizzazione delle tabelle nella vista dell'utente potrebbe non essere costante e potrebbero essere restituiti messaggi di errore di tabella non esistente.</span><span class="sxs-lookup"><span data-stu-id="c9677-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="c9677-114">Viste possono essere utilizzati tooprovide gli utenti con un livello di presentazione coerente al contempo agli oggetti sottostanti hello vengono rinominati.</span><span class="sxs-lookup"><span data-stu-id="c9677-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="c9677-115">Consentendo agli utenti l'accesso toohello dati tramite una visualizzazione, significa che non devono essere toohave visibilità delle tabelle sottostanti hello.</span><span class="sxs-lookup"><span data-stu-id="c9677-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="c9677-116">Ciò offre un'esperienza utente coerente assicurando che le finestre di progettazione di hello data warehouse possono sviluppare il modello di dati di hello e ottimizzare le prestazioni utilizzando un'istruzione CTAS durante il processo di caricamento dati hello.</span><span class="sxs-lookup"><span data-stu-id="c9677-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="c9677-117">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c9677-117">Performance optimization</span></span>
<span data-ttu-id="c9677-118">Viste possono essere inoltre utilizzato tooenforce prestazioni join tra tabelle.</span><span class="sxs-lookup"><span data-stu-id="c9677-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="c9677-119">Ad esempio, una vista è possibile incorporare una chiave di distribuzione ridondante come parte di hello lo spostamento dei dati toominimize di criteri di unione.</span><span class="sxs-lookup"><span data-stu-id="c9677-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="c9677-120">Un altro vantaggio di una vista può essere una query specifica tooforce o hint di join.</span><span class="sxs-lookup"><span data-stu-id="c9677-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="c9677-121">Utilizzo di visualizzazioni in questo modo garantisce che i join vengono sempre eseguiti in modo ottimale eliminando la necessità hello per costrutto corretto hello tooremember di utenti per i join.</span><span class="sxs-lookup"><span data-stu-id="c9677-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="c9677-122">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="c9677-122">Limitations</span></span>
<span data-ttu-id="c9677-123">Le viste in SQL Data Warehouse sono solo metadati.</span><span class="sxs-lookup"><span data-stu-id="c9677-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="c9677-124">Di conseguenza hello le opzioni seguenti non sono disponibile:</span><span class="sxs-lookup"><span data-stu-id="c9677-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="c9677-125">Non esiste alcuna opzione di binding dello schema</span><span class="sxs-lookup"><span data-stu-id="c9677-125">There is no schema binding option</span></span>
* <span data-ttu-id="c9677-126">Impossibile aggiornare le tabelle di base tramite la vista hello</span><span class="sxs-lookup"><span data-stu-id="c9677-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="c9677-127">Non è possibile creare visualizzazioni sulle tabelle temporanee</span><span class="sxs-lookup"><span data-stu-id="c9677-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="c9677-128">Nessun supporto per hello ESPANDI / hint NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="c9677-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="c9677-129">Non sono disponibili viste indicizzate in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c9677-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9677-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9677-130">Next steps</span></span>
<span data-ttu-id="c9677-131">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="c9677-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="c9677-132">Per `CREATE VIEW` sintassi, vedere troppo[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="c9677-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
