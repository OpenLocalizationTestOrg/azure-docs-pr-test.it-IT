---
title: Creare un'istanza di SQL Data Warehouse con TSQL | Documentazione Microsoft
description: Informazioni su come creare un'istanza di Azure SQL Data Warehouse con TSQL
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
ms.openlocfilehash: 10d8aa2b3ab8d7d8a9b91e95ffccf03faa89d237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="c5997-103">Creare un database di SQL Data Warehouse usando Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="c5997-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5997-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c5997-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="c5997-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="c5997-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="c5997-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5997-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="c5997-107">Questo articolo illustra come creare un'istanza di SQL Data Warehouse usando T-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5997-107">This article shows you how to create a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5997-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c5997-108">Prerequisites</span></span>
<span data-ttu-id="c5997-109">Per iniziare, è necessario:</span><span class="sxs-lookup"><span data-stu-id="c5997-109">To get started, you need:</span></span>

* <span data-ttu-id="c5997-110">**Account Azure**: per creare un account, vedere la [versione di valutazione gratuita][Azure Free Trial] o [MSDN Azure Credits][MSDN Azure Credits] (Crediti Azure MSDN).</span><span class="sxs-lookup"><span data-stu-id="c5997-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="c5997-111">**Server SQL Azure**: vedere [creare un server logico di Database SQL di Azure con il portale di Azure] [creare un server logico di Database SQL di Azure con il portale di Azure] o [creare un server logico di Database SQL di Azure con PowerShell] [creare SQL Azure Server logico di database con PowerShell] per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="c5997-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with the Azure Portal][Create an Azure SQL Database logical server with the Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="c5997-112">**Gruppo di risorse**: usare lo stesso gruppo di risorse del server di Azure SQL oppure vedere [Creare un gruppo di risorse][how to create a resource group].</span><span class="sxs-lookup"><span data-stu-id="c5997-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group][how to create a resource group].</span></span>
* <span data-ttu-id="c5997-113">**Ambiente per l'esecuzione di T-SQL**: per eseguire T-SQL, è possibile usare [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd] o [SSMS][SSMS].</span><span class="sxs-lookup"><span data-stu-id="c5997-113">**Environment to execute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] to execute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="c5997-114">La creazione di un'istanza di SQL Data Warehouse può dare luogo a un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="c5997-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="c5997-115">Per altre informazioni dettagliate sui prezzi, vedere [Prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="c5997-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="c5997-116">Creare un database con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5997-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="c5997-117">Se non si ha familiarità con Visual Studio, vedere l'articolo [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)] (Eseguire query in Azure SQL Data Warehouse (Visual Studio)).</span><span class="sxs-lookup"><span data-stu-id="c5997-117">If you are new to Visual Studio, see the article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="c5997-118">Per iniziare, aprire Esplora oggetti di SQL Server in Visual Studio e connettersi al server che ospiterà il database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c5997-118">To start, open SQL Server Object Explorer in Visual Studio and connect to the server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="c5997-119">Dopo aver stabilito la connessione, è possibile creare un'istanza di SQL Data Warehouse eseguendo questo comando SQL sul database **master** .</span><span class="sxs-lookup"><span data-stu-id="c5997-119">Once connected, you can create a SQL Data Warehouse by running the following SQL command against the **master** database.</span></span>  <span data-ttu-id="c5997-120">Questo comando crea il database MySqlDwDb con un obiettivo di servizio DW400 e consente un aumento delle dimensioni del database fino al limite massimo di 10 TB.</span><span class="sxs-lookup"><span data-stu-id="c5997-120">This command creates the database MySqlDwDb with a Service Objective of DW400 and allow the database to grow to a maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="c5997-121">Creare un database con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c5997-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="c5997-122">In alternativa, è possibile usare lo stesso comando con sqlcmd eseguendo quanto segue al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="c5997-122">Alternatively, you can run the same command with sqlcmd by running the following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="c5997-123">Se non specificate, le regole di confronto predefinite sono COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="c5997-123">The default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="c5997-124">Il parametro `MAXSIZE` può essere compreso tra 250 GB e 240 TB.</span><span class="sxs-lookup"><span data-stu-id="c5997-124">The `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="c5997-125">`SERVICE_OBJECTIVE` può essere compreso tra DW100 e DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="c5997-125">The `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="c5997-126">Per un elenco di tutti i valori validi, vedere la documentazione in MSDN relativa a [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="c5997-126">For a list of all valid values, see the MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="c5997-127">MAXSIZE e SERVICE_OBJECTIVE possono essere entrambi modificati con un comando [ALTER DATABASE][ALTER DATABASE] T-SQL.</span><span class="sxs-lookup"><span data-stu-id="c5997-127">Both the MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="c5997-128">Le regole di confronto di un database non possono essere modificate dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="c5997-128">The collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="c5997-129">Prestare attenzione quando si modifica il parametro SERVICE_OBJECTIVE, perché la modifica di DWU provoca un riavvio dei servizi e il conseguente annullamento delle query in corso.</span><span class="sxs-lookup"><span data-stu-id="c5997-129">Caution should be used when changing the SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="c5997-130">La modifica di MAXSIZE non riavvia i servizi, perché si tratta di una semplice operazione sui metadati.</span><span class="sxs-lookup"><span data-stu-id="c5997-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5997-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5997-131">Next steps</span></span>
<span data-ttu-id="c5997-132">Al termine del provisioning di SQL Data Warehouse, è possibile [caricare dati di esempio][load sample data] o vedere come eseguire le attività di [sviluppo][develop], [caricamento][load] o [migrazione][migrate].</span><span class="sxs-lookup"><span data-stu-id="c5997-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how to create a SQL Data Warehouse from the Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
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
