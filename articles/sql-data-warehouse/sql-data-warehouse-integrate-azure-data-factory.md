---
title: Usare Azure Data Factory con SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 7cd113f4a92635bc68253c2beb165ad1f0c96569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="a35b8-103">Usare Data factory di Azure con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a35b8-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="a35b8-104">Data factory di Azure offre un metodo completamente gestito per l'orchestrazione del trasferimento di dati e l'esecuzione di stored procedure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a35b8-104">Azure Data Factory provides a fully managed method for orchestrating the transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="a35b8-105">In questo modo è possibile configurare e pianificare più facilmente procedure ETL (Extract, Transform, Load) complesse con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a35b8-105">This will allow you to more easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="a35b8-106">Per una panoramica più completa di Azure Data Factory, vedere la [documentazione di Azure Data Factory][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="a35b8-106">For a more complete overview of Azure Data Factory, see the [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="a35b8-107">Spostamento dei dati</span><span class="sxs-lookup"><span data-stu-id="a35b8-107">Data Movement</span></span>
<span data-ttu-id="a35b8-108">Data factory di Azure consente lo spostamento di dati tra origini locali e diversi servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="a35b8-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="a35b8-109">In generale, l'attuale integrazione con Data factory di Azure supporta lo spostamento dei dati da e verso le posizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a35b8-109">Overall, current integration with Azure Data Factory supports data movement to and from the following locations:</span></span>

* <span data-ttu-id="a35b8-110">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="a35b8-110">Azure blob storage</span></span>
* <span data-ttu-id="a35b8-111">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="a35b8-111">Azure SQL Database</span></span>
* <span data-ttu-id="a35b8-112">Server SQL locale</span><span class="sxs-lookup"><span data-stu-id="a35b8-112">On-premises SQL Server</span></span>
* <span data-ttu-id="a35b8-113">SQL Server in IaaS</span><span class="sxs-lookup"><span data-stu-id="a35b8-113">SQL Server on IaaS</span></span>

<span data-ttu-id="a35b8-114">Per informazioni su come configurare un'attività di copia, vedere [Copiare i dati con Azure Data Factory][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="a35b8-114">For information on how to set up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="a35b8-115">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="a35b8-115">Stored Procedures</span></span>
 <span data-ttu-id="a35b8-116">Così come può essere usato per pianificare il trasferimento dei dati, Data factory di Azure può essere usato anche per orchestrare l'esecuzione di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="a35b8-116">In the same way it can be used to schedule data transfer, Azure Data Factory can also be used to orchestrate the execution of stored procedures.</span></span>  <span data-ttu-id="a35b8-117">Ciò consente di creare pipeline più complesse ed estende la capacità di Data factory di Azure per sfruttare la potenza di elaborazione di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a35b8-117">This allows more complex pipelines to be created and extends Azure Data Factory's ability to leverage the computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a35b8-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a35b8-118">Next steps</span></span>
<span data-ttu-id="a35b8-119">Per una panoramica dell'integrazione, vedere [Panoramica dell'integrazione di SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="a35b8-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="a35b8-120">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a35b8-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

