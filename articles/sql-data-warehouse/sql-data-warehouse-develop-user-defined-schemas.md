---
title: gli schemi definiti aaaUser in SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per l'uso di schemi Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="d452c-103">Schemi definiti dall'utente in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d452c-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="d452c-104">Data warehouse tradizionali spesso utilizzare database separati toocreate limiti per le applicazioni in base a carico di lavoro, dominio o sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d452c-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="d452c-105">Ad esempio, un data warehouse di SQL Server tradizionale potrebbe includere un database di gestione temporanea, un database del data warehouse e alcuni database del data mart.</span><span class="sxs-lookup"><span data-stu-id="d452c-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="d452c-106">In questa topologia ogni database funziona come un carico di lavoro e il limite di sicurezza nell'architettura di hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="d452c-107">Al contrario, SQL Data Warehouse viene eseguito hello intero data warehouse del carico di lavoro all'interno di un database.</span><span class="sxs-lookup"><span data-stu-id="d452c-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="d452c-108">I join tra database non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="d452c-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="d452c-109">Di conseguenza SQL Data Warehouse prevede che tutte le tabelle utilizzate da hello warehouse toobe archiviati all'interno di un database di hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="d452c-110">SQL Data Warehouse non supporta query tra database di alcun tipo.</span><span class="sxs-lookup"><span data-stu-id="d452c-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="d452c-111">Di conseguenza, implementazioni di data warehouse che utilizzano questo schema saranno necessario toobe rivisto.</span><span class="sxs-lookup"><span data-stu-id="d452c-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="d452c-112">Raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="d452c-112">Recommendations</span></span>
<span data-ttu-id="d452c-113">Si tratta di indicazioni per il consolidamento di carichi di lavoro, sicurezza, dominio e i limiti funzionali mediante l'uso di schemi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d452c-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="d452c-114">Utilizzare un Data Warehouse di SQL database toorun il carico di lavoro intero data warehouse</span><span class="sxs-lookup"><span data-stu-id="d452c-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="d452c-115">Consolidare dati warehouse ambiente toouse un Data Warehouse di SQL database esistente</span><span class="sxs-lookup"><span data-stu-id="d452c-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="d452c-116">Usare **degli schemi definiti dall'utente** limite hello tooprovide precedentemente implementata utilizzando i database.</span><span class="sxs-lookup"><span data-stu-id="d452c-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="d452c-117">Se gli schemi definiti dall'utente non sono stati usati in precedenza, si avrà uno slate pulito.</span><span class="sxs-lookup"><span data-stu-id="d452c-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="d452c-118">Consente di usare semplicemente il nome di database precedente hello come base di hello per gli schemi definiti dall'utente nel database di SQL Data Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="d452c-119">Se gli schemi sono già stati usati, sono disponibili alcune opzioni:</span><span class="sxs-lookup"><span data-stu-id="d452c-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="d452c-120">Rimuovere i nomi di schema legacy hello e iniziare</span><span class="sxs-lookup"><span data-stu-id="d452c-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="d452c-121">Mantenere i nomi di schema legacy hello dal nome di tabella toohello nome schema legacy hello già in sospeso</span><span class="sxs-lookup"><span data-stu-id="d452c-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="d452c-122">Mantenere i nomi di schema legacy hello implementando viste su tabella hello in un toore aggiuntivo schema-creare una struttura dello schema precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="d452c-123">Al primo opzione 3 può sembrare opzione più interessante hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="d452c-124">È tuttavia importante sottolineare hello in dettaglio hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="d452c-125">Le viste sono di sola lettura in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d452c-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="d452c-126">Qualsiasi modifica di dati o la tabella sarà necessario toobe eseguita sulla tabella di base hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="d452c-127">L'opzione 3 introduce anche un livello di viste nel sistema.</span><span class="sxs-lookup"><span data-stu-id="d452c-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="d452c-128">È possibile toogive questo un lavoro aggiuntivo se si utilizza le viste dell'architettura già.</span><span class="sxs-lookup"><span data-stu-id="d452c-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="d452c-129">Esempi:</span><span class="sxs-lookup"><span data-stu-id="d452c-129">Examples:</span></span>
<span data-ttu-id="d452c-130">Implementare schemi definiti dall'utente in base ai nomi di database.</span><span class="sxs-lookup"><span data-stu-id="d452c-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="d452c-131">Mantenere schema legacy assegna un nome mediante il nome di tabella toohello.</span><span class="sxs-lookup"><span data-stu-id="d452c-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="d452c-132">Usare gli schemi per il limite di carico di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-132">Use schemas for hello workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="d452c-133">Mantenere i nomi di schemi legacy usando viste.</span><span class="sxs-lookup"><span data-stu-id="d452c-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="d452c-134">Qualsiasi modifica nella strategia di schema deve una revisione del modello di sicurezza hello per database hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="d452c-135">In molti casi potrebbe essere in grado di toosimplify modello di sicurezza hello assegnando le autorizzazioni a livello di schema hello.</span><span class="sxs-lookup"><span data-stu-id="d452c-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="d452c-136">Se sono necessarie autorizzazioni più granulari, è possibile utilizzare i ruoli del database.</span><span class="sxs-lookup"><span data-stu-id="d452c-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d452c-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d452c-137">Next steps</span></span>
<span data-ttu-id="d452c-138">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="d452c-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
