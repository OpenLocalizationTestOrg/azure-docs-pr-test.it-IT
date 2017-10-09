---
title: Data Factory di Azure con SQL Data Warehouse aaaUse | Documenti Microsoft
description: Suggerimenti per l'uso di Data factory di Azure con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="8f8b2-103">Usare Data factory di Azure con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8f8b2-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="8f8b2-104">Data Factory di Azure fornisce un metodo completamente gestito per l'orchestrazione trasferimento hello dei dati e l'esecuzione di stored procedure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f8b2-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="8f8b2-105">In questo modo si toomore facilmente installazione e pianificazione estrarre trasformazione e caricamento (ETL) procedure complesse con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f8b2-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="8f8b2-106">Per una panoramica più completa di Azure Data Factory, vedere hello [documentazione di Azure Data Factory][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="8f8b2-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="8f8b2-107">Spostamento dei dati</span><span class="sxs-lookup"><span data-stu-id="8f8b2-107">Data Movement</span></span>
<span data-ttu-id="8f8b2-108">Data factory di Azure consente lo spostamento di dati tra origini locali e diversi servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f8b2-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="8f8b2-109">In generale, corrente integrazione con Data Factory di Azure supporta tooand lo spostamento dei dati da hello posizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f8b2-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="8f8b2-110">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8f8b2-110">Azure blob storage</span></span>
* <span data-ttu-id="8f8b2-111">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="8f8b2-111">Azure SQL Database</span></span>
* <span data-ttu-id="8f8b2-112">Server SQL locale</span><span class="sxs-lookup"><span data-stu-id="8f8b2-112">On-premises SQL Server</span></span>
* <span data-ttu-id="8f8b2-113">SQL Server in IaaS</span><span class="sxs-lookup"><span data-stu-id="8f8b2-113">SQL Server on IaaS</span></span>

<span data-ttu-id="8f8b2-114">Per informazioni su come attività di copia tooset backup di un tipo di dati, vedere [copiare i dati con Data Factory di Azure][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="8f8b2-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="8f8b2-115">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="8f8b2-115">Stored Procedures</span></span>
 <span data-ttu-id="8f8b2-116">In hello stesso modo è possibile utilizzare tooschedule trasferimento dei dati, può essere Data Factory di Azure anche essere utilizzati tooorchestrate hello esecuzione di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="8f8b2-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="8f8b2-117">In questo modo più complesso toobe pipeline creato e si estende possibilità tooleverage hello la potenza di calcolo della Data Factory di Azure di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f8b2-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f8b2-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f8b2-118">Next steps</span></span>
<span data-ttu-id="8f8b2-119">Per una panoramica dell'integrazione, vedere [Panoramica dell'integrazione di SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="8f8b2-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="8f8b2-120">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="8f8b2-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

