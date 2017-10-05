---
title: Creare un'istanza di SQL Data Warehouse con PowerShell | Documentazione Microsoft
description: Creare un'istanza di SQL Data Warehouse con PowerShell
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: a763f1c600c1a3f37cb565a8eb7db3c3f27dcf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="6fb84-103">Creare SQL Data Warehouse con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fb84-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6fb84-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6fb84-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="6fb84-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="6fb84-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="6fb84-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fb84-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="6fb84-107">Questo articolo illustra come creare un'istanza di SQL Data Warehouse usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fb84-107">This article shows you how to create a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fb84-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6fb84-108">Prerequisites</span></span>
<span data-ttu-id="6fb84-109">Per iniziare, è necessario:</span><span class="sxs-lookup"><span data-stu-id="6fb84-109">To get started, you need:</span></span>

* <span data-ttu-id="6fb84-110">**Account Azure**: per creare un account, vedere la [versione di valutazione gratuita][Azure Free Trial] o [MSDN Azure Credits][MSDN Azure Credits] (Crediti Azure MSDN).</span><span class="sxs-lookup"><span data-stu-id="6fb84-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="6fb84-111">**Server SQL di Azure**: per altre informazioni dettagliate, vedere [Create an Azure SQL database in the Azure Portal][Create an Azure SQL database in the Azure Portal] (Creare un database SQL di Azure nel portale di Azure) o [Creare un database SQL di Azure con PowerShell][Create an Azure SQL database with PowerShell].</span><span class="sxs-lookup"><span data-stu-id="6fb84-111">**Azure SQL server**:  See [Create an Azure SQL database in the Azure Portal][Create an Azure SQL database in the Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="6fb84-112">**Gruppo di risorse**: usare lo stesso gruppo di risorse del server di Azure SQL oppure vedere [Creare un gruppo di risorse](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6fb84-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="6fb84-113">**PowerShell versione 1.0.3 o successiva**: è possibile verificare la versione in uso eseguendo **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="6fb84-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="6fb84-114">È possibile installare la versione più recente usando [Installazione guidata piattaforma Web Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="6fb84-114">The latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="6fb84-115">Per altre informazioni sull'installazione della versione più recente, vedere [Come installare e configurare Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="6fb84-115">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="6fb84-116">La creazione di un'istanza di SQL Data Warehouse può dare luogo a un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="6fb84-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="6fb84-117">Per altre informazioni dettagliate sui prezzi, vedere [Prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="6fb84-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="6fb84-118">Creare un SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6fb84-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="6fb84-119">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fb84-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="6fb84-120">Eseguire questo cmdlet per accedere a Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb84-120">Run this cmdlet to login to Azure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="6fb84-121">Selezionare la sottoscrizione da usare per la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="6fb84-121">Select the subscription you want to use for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="6fb84-122">Creare il database.</span><span class="sxs-lookup"><span data-stu-id="6fb84-122">Create database.</span></span> <span data-ttu-id="6fb84-123">Questo esempio crea un database denominato "mynewsqldw", con un livello di obiettivo di servizio "DW400" nel server denominato "sqldwserver1" incluso nel gruppo di risorse "mywesteuroperesgp1".</span><span class="sxs-lookup"><span data-stu-id="6fb84-123">This example creates a database named "mynewsqldw", with service objective level "DW400", to the server named "sqldwserver1", which is in the resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="6fb84-124">I parametri obbligatori sono:</span><span class="sxs-lookup"><span data-stu-id="6fb84-124">Required Parameters are:</span></span>

* <span data-ttu-id="6fb84-125">**RequestedServiceObjectiveName**: quantità di [DWU][DWU] richiesta.</span><span class="sxs-lookup"><span data-stu-id="6fb84-125">**RequestedServiceObjectiveName**: The amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="6fb84-126">I valori supportati sono: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 e DW6000.</span><span class="sxs-lookup"><span data-stu-id="6fb84-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="6fb84-127">**DatabaseName**: il nome dell'istanza di SQL Data Warehouse che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="6fb84-127">**DatabaseName**: The name of the SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="6fb84-128">**ServerName**: il nome del server che si sta usando per la creazione (deve essere V12).</span><span class="sxs-lookup"><span data-stu-id="6fb84-128">**ServerName**: The name of the server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="6fb84-129">**ResourceGroupName**: il gruppo di risorse in uso.</span><span class="sxs-lookup"><span data-stu-id="6fb84-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="6fb84-130">Per trovare i gruppi di risorse disponibili nella sottoscrizione, usare Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="6fb84-130">To find available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="6fb84-131">**Edition**: per creare un'istanza di SQL Data Warehouse, deve essere "DataWarehouse".</span><span class="sxs-lookup"><span data-stu-id="6fb84-131">**Edition**: Must be "DataWarehouse" to create a SQL Data Warehouse.</span></span>

<span data-ttu-id="6fb84-132">I parametri facoltativi sono:</span><span class="sxs-lookup"><span data-stu-id="6fb84-132">Optional Parameters are:</span></span>

* <span data-ttu-id="6fb84-133">**CollationName**: se non specificate, le regole di confronto predefinite sono SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="6fb84-133">**CollationName**: The default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="6fb84-134">Non è possibile modificare le regole di confronto in un database.</span><span class="sxs-lookup"><span data-stu-id="6fb84-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="6fb84-135">**MaxSizeBytes**: la dimensione massima predefinita di un database è 10 GB.</span><span class="sxs-lookup"><span data-stu-id="6fb84-135">**MaxSizeBytes**: The default max size of a database is 10 GB.</span></span>

<span data-ttu-id="6fb84-136">Per altre informazioni dettagliate sulle opzioni dei parametri, vedere [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] e [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="6fb84-136">For more details on the parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fb84-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6fb84-137">Next steps</span></span>
<span data-ttu-id="6fb84-138">Al termine del provisioning di SQL Data Warehouse, è possibile provare a [caricare dati di esempio][loading sample data] o scoprire come eseguire le attività di [sviluppo][develop], [caricamento][load] o [migrazione][migrate].</span><span class="sxs-lookup"><span data-stu-id="6fb84-138">After your SQL Data Warehouse has finished provisioning you may want to try [loading sample data][loading sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="6fb84-139">Per altre informazioni su come gestire SQL Data Warehouse a livello di codice, vedere l'articolo sull'uso dei [cmdlet di PowerShell e le API REST][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="6fb84-139">If you're interested in more on how to manage SQL Data Warehouse programmatically, check out our article on how to use [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how to create a SQL Data Warehouse from the Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
