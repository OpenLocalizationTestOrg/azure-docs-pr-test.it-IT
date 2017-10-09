---
title: aaaCreate un SQL Data Warehouse con TSQL | Documenti Microsoft
description: Informazioni su come toocreate un esempio di SQL Azure Data Warehouse con TSQL
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="8b089-103">Creare un database di SQL Data Warehouse usando Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="8b089-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b089-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b089-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="8b089-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="8b089-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="8b089-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b089-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="8b089-107">Questo articolo illustra come toocreate un SQL Data Warehouse utilizzando T-SQL.</span><span class="sxs-lookup"><span data-stu-id="8b089-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b089-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b089-108">Prerequisites</span></span>
<span data-ttu-id="8b089-109">tooget avviato, è necessario:</span><span class="sxs-lookup"><span data-stu-id="8b089-109">tooget started, you need:</span></span>

* <span data-ttu-id="8b089-110">**Account Azure**: visitare [versione di valutazione gratuita di Azure] [ Azure Free Trial] o [crediti Azure MSDN] [ MSDN Azure Credits] toocreate un account.</span><span class="sxs-lookup"><span data-stu-id="8b089-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="8b089-111">**Server SQL Azure**: vedere [creare un server logico di Database SQL di Azure con il portale di Azure hello] [creare un server logico di Database SQL di Azure con il portale di Azure hello] o [creare un server logico di Database SQL di Azure con PowerShell] [creare SQL Azure Server logico di database con PowerShell] per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="8b089-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="8b089-112">**Gruppo di risorse**: utilizzare hello stessa risorsa gruppo di server SQL Azure o vedere [come un gruppo di risorse toocreate][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="8b089-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="8b089-113">**Ambiente tooexecute T-SQL**: È possibile utilizzare [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], o [SQLServerManagementStudio] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="8b089-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="8b089-114">La creazione di un'istanza di SQL Data Warehouse può dare luogo a un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="8b089-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="8b089-115">Per altre informazioni dettagliate sui prezzi, vedere [Prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="8b089-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="8b089-116">Creare un database con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8b089-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="8b089-117">Nel caso di nuova tooVisual Studio, vedere l'articolo hello [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="8b089-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="8b089-118">toostart, aprire Esplora oggetti di SQL Server in Visual Studio e connettersi toohello server che ospiterà il database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8b089-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="8b089-119">Una volta connessi, è possibile creare un Data Warehouse SQL tramite l'esecuzione comando SQL contro hello seguente hello **master** database.</span><span class="sxs-lookup"><span data-stu-id="8b089-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="8b089-120">Questo comando crea il database di hello MySqlDwDb con un obiettivo di servizio di DW400 e consentire hello toogrow tooa dimensioni massime del database di 10 TB.</span><span class="sxs-lookup"><span data-stu-id="8b089-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="8b089-121">Creare un database con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="8b089-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="8b089-122">In alternativa, è possibile eseguire hello stesso comando con sqlcmd eseguendo hello seguente a un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8b089-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="8b089-123">Hello regole di confronto predefinite quando non viene specificato è COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="8b089-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="8b089-124">Hello `MAXSIZE` deve essere compreso tra 250 GB e TB 240.</span><span class="sxs-lookup"><span data-stu-id="8b089-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="8b089-125">Hello `SERVICE_OBJECTIVE` deve essere compreso tra DW100 e DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="8b089-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="8b089-126">Per un elenco di tutti i valori validi, vedere la documentazione MSDN hello per [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="8b089-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="8b089-127">Hello MAXSIZE sia possono SERVICE_OBJECTIVE essere modificati con un [ALTER DATABASE] [ ALTER DATABASE] comando T-SQL.</span><span class="sxs-lookup"><span data-stu-id="8b089-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="8b089-128">regole di confronto di Hello di un database non possono essere modificate dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="8b089-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="8b089-129">Attenzione deve essere utilizzato quando la modifica hello SERVICE_OBJECTIVE come la modifica DWU comporta il riavvio dei servizi, che annulla tutte le query in fase di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="8b089-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="8b089-130">La modifica di MAXSIZE non riavvia i servizi, perché si tratta di una semplice operazione sui metadati.</span><span class="sxs-lookup"><span data-stu-id="8b089-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b089-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b089-131">Next steps</span></span>
<span data-ttu-id="8b089-132">Dopo aver completato il provisioning è possibile il Data Warehouse di SQL [caricare dati di esempio] [ load sample data] o estrarlo come troppo[sviluppare][develop], [caricare][load], o [migrare][migrate].</span><span class="sxs-lookup"><span data-stu-id="8b089-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
