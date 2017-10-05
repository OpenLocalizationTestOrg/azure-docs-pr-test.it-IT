---
title: Schemi definiti dall'utente in SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="c74e2-103">Schemi definiti dall'utente in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c74e2-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="c74e2-104">I data warehouse tradizionali spesso usano database separati per creare i limiti dell'applicazione in base a carico di lavoro, dominio o di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c74e2-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="c74e2-105">Ad esempio, un data warehouse di SQL Server tradizionale potrebbe includere un database di gestione temporanea, un database del data warehouse e alcuni database del data mart.</span><span class="sxs-lookup"><span data-stu-id="c74e2-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="c74e2-106">In questa topologia ogni database funziona come carico di lavoro e limite di sicurezza nell'architettura.</span><span class="sxs-lookup"><span data-stu-id="c74e2-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="c74e2-107">Al contrario, SQL Data Warehouse esegue tutto il carico di lavoro del data warehouse all'interno di un database.</span><span class="sxs-lookup"><span data-stu-id="c74e2-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="c74e2-108">I join tra database non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="c74e2-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="c74e2-109">SQL Data Warehouse prevede pertanto che tutte le tabelle usate dal data warehouse siano archiviate all'interno di un database.</span><span class="sxs-lookup"><span data-stu-id="c74e2-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="c74e2-110">SQL Data Warehouse non supporta query tra database di alcun tipo.</span><span class="sxs-lookup"><span data-stu-id="c74e2-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="c74e2-111">Di conseguenza, le implementazioni di data warehouse che usano questo modello dovranno essere modificate.</span><span class="sxs-lookup"><span data-stu-id="c74e2-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="c74e2-112">Indicazioni</span><span class="sxs-lookup"><span data-stu-id="c74e2-112">Recommendations</span></span>
<span data-ttu-id="c74e2-113">Si tratta di indicazioni per il consolidamento di carichi di lavoro, sicurezza, dominio e i limiti funzionali mediante l'uso di schemi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="c74e2-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="c74e2-114">Usare un database SQL Data Warehouse per eseguire l'intero carico di lavoro del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c74e2-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="c74e2-115">Consolidare l'ambiente data warehouse esistente per l'uso di un solo database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c74e2-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="c74e2-116">Sfruttare gli **schemi definiti dall'utente** per fornire il limite implementato in precedenza tramite database.</span><span class="sxs-lookup"><span data-stu-id="c74e2-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="c74e2-117">Se gli schemi definiti dall'utente non sono stati usati in precedenza, si avrà uno slate pulito.</span><span class="sxs-lookup"><span data-stu-id="c74e2-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="c74e2-118">Usare semplicemente il nome del database precedente come base per gli schemi definiti dall'utente nel database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c74e2-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="c74e2-119">Se gli schemi sono già stati usati, sono disponibili alcune opzioni:</span><span class="sxs-lookup"><span data-stu-id="c74e2-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="c74e2-120">Rimuovere i nomi degli schemi legacy e ricominciare dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="c74e2-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="c74e2-121">Mantenere i nomi degli schemi legacy premettendo il nome dello schema legacy al nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="c74e2-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="c74e2-122">Mantenere i nomi degli schemi legacy implementando viste sulla tabella in uno schema aggiuntivo per ricreare la struttura dello schema precedente.</span><span class="sxs-lookup"><span data-stu-id="c74e2-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="c74e2-123">A prima vista, l'opzione 3 può sembrare quella più interessante.</span><span class="sxs-lookup"><span data-stu-id="c74e2-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="c74e2-124">È tuttavia importante osservare i dettagli.</span><span class="sxs-lookup"><span data-stu-id="c74e2-124">However, the devil is in the detail.</span></span> <span data-ttu-id="c74e2-125">Le viste sono di sola lettura in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c74e2-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="c74e2-126">Qualsiasi modifica di dati o tabelle dovrà essere eseguita sulla tabella di base.</span><span class="sxs-lookup"><span data-stu-id="c74e2-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="c74e2-127">L'opzione 3 introduce anche un livello di viste nel sistema.</span><span class="sxs-lookup"><span data-stu-id="c74e2-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="c74e2-128">È consigliabile valutare attentamente questo aspetto se si usano già viste nell'architettura.</span><span class="sxs-lookup"><span data-stu-id="c74e2-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="c74e2-129">Esempi:</span><span class="sxs-lookup"><span data-stu-id="c74e2-129">Examples:</span></span>
<span data-ttu-id="c74e2-130">Implementare schemi definiti dall'utente in base ai nomi di database.</span><span class="sxs-lookup"><span data-stu-id="c74e2-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="c74e2-131">Mantenere nomi di schemi legacy premettendoli al nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="c74e2-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="c74e2-132">Usare schemi per il limite del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c74e2-132">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="c74e2-133">Mantenere i nomi di schemi legacy usando viste.</span><span class="sxs-lookup"><span data-stu-id="c74e2-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="c74e2-134">Qualsiasi modifica nella strategia relativa agli schemi richiede una revisione del modello di sicurezza per il database.</span><span class="sxs-lookup"><span data-stu-id="c74e2-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="c74e2-135">In molti casi è possibile semplificare il modello di sicurezza assegnando le autorizzazioni a livello di schema.</span><span class="sxs-lookup"><span data-stu-id="c74e2-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="c74e2-136">Se sono necessarie autorizzazioni più granulari, è possibile utilizzare i ruoli del database.</span><span class="sxs-lookup"><span data-stu-id="c74e2-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c74e2-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c74e2-137">Next steps</span></span>
<span data-ttu-id="c74e2-138">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="c74e2-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
