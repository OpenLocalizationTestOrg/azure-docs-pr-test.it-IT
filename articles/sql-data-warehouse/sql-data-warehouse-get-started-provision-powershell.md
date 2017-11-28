---
title: aaaCreate SQL Data Warehouse mediante PowerShell | Documenti Microsoft
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
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="e8e66-103">Creare SQL Data Warehouse con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8e66-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8e66-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e8e66-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="e8e66-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="e8e66-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="e8e66-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8e66-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="e8e66-107">Questo articolo illustra come toocreate un SQL Data Warehouse tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8e66-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8e66-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e8e66-108">Prerequisites</span></span>
<span data-ttu-id="e8e66-109">tooget avviato, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e8e66-109">tooget started, you need:</span></span>

* <span data-ttu-id="e8e66-110">**Account Azure**: visitare [versione di valutazione gratuita di Azure] [ Azure Free Trial] o [crediti Azure MSDN] [ MSDN Azure Credits] toocreate un account.</span><span class="sxs-lookup"><span data-stu-id="e8e66-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="e8e66-111">**Server SQL Azure**: vedere [creare un database SQL di Azure nel portale di Azure hello] [ Create an Azure SQL database in hello Azure Portal] o [creare un database SQL di Azure con PowerShell] [ Create an Azure SQL database with PowerShell] per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="e8e66-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="e8e66-112">**Gruppo di risorse**: utilizzare hello stessa risorsa gruppo di server SQL Azure o vedere [come un gruppo di risorse toocreate](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e8e66-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="e8e66-113">**PowerShell versione 1.0.3 o successiva**: è possibile verificare la versione in uso eseguendo **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="e8e66-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="e8e66-114">è possibile installare la versione più recente di Hello da [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="e8e66-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="e8e66-115">Per ulteriori informazioni su come installare la versione più recente di hello, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="e8e66-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="e8e66-116">La creazione di un'istanza di SQL Data Warehouse può dare luogo a un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="e8e66-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="e8e66-117">Per altre informazioni dettagliate sui prezzi, vedere [Prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="e8e66-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="e8e66-118">Creare un SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e8e66-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="e8e66-119">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8e66-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e8e66-120">Eseguire questo tooAzure toologin cmdlet Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="e8e66-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="e8e66-121">Selezionare la sottoscrizione di hello da toouse per la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="e8e66-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="e8e66-122">Creare il database.</span><span class="sxs-lookup"><span data-stu-id="e8e66-122">Create database.</span></span> <span data-ttu-id="e8e66-123">In questo esempio viene creato un database denominato "mynewsqldw", con l'obiettivo livello di servizio "DW400", toohello server denominato "sqldwserver1", nel gruppo di risorse di hello denominato "mywesteuroperesgp1".</span><span class="sxs-lookup"><span data-stu-id="e8e66-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="e8e66-124">I parametri obbligatori sono:</span><span class="sxs-lookup"><span data-stu-id="e8e66-124">Required Parameters are:</span></span>

* <span data-ttu-id="e8e66-125">**RequestedServiceObjectiveName**: quantità di hello di [DWU] [ DWU] richiesta.</span><span class="sxs-lookup"><span data-stu-id="e8e66-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="e8e66-126">I valori supportati sono: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 e DW6000.</span><span class="sxs-lookup"><span data-stu-id="e8e66-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="e8e66-127">**DatabaseName**: nome hello di hello SQL Data Warehouse che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="e8e66-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="e8e66-128">**ServerName**: nome hello del server di hello che si sta utilizzando per la creazione (deve essere V12).</span><span class="sxs-lookup"><span data-stu-id="e8e66-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="e8e66-129">**ResourceGroupName**: il gruppo di risorse in uso.</span><span class="sxs-lookup"><span data-stu-id="e8e66-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="e8e66-130">toofind gruppi di risorse disponibili nella sottoscrizione utilizzano Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="e8e66-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="e8e66-131">**Edizione**: deve essere "Data warehouse" toocreate un SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e8e66-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="e8e66-132">I parametri facoltativi sono:</span><span class="sxs-lookup"><span data-stu-id="e8e66-132">Optional Parameters are:</span></span>

* <span data-ttu-id="e8e66-133">**CollationName**: hello regole di confronto predefinite se non specificato è SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="e8e66-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="e8e66-134">Non è possibile modificare le regole di confronto in un database.</span><span class="sxs-lookup"><span data-stu-id="e8e66-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="e8e66-135">**MaxSizeBytes**: dimensioni massime di hello predefinito di un database sono di 10 GB.</span><span class="sxs-lookup"><span data-stu-id="e8e66-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="e8e66-136">Per ulteriori dettagli sulle opzioni di parametro hello, vedere [New AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] e [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="e8e66-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8e66-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8e66-137">Next steps</span></span>
<span data-ttu-id="e8e66-138">Dopo che il Data Warehouse SQL ha completato il provisioning è opportuno tootry [durante il caricamento di dati di esempio] [ loading sample data] o estrarlo come troppo[sviluppare] [ develop] , [caricare][load], o [migrare][migrate].</span><span class="sxs-lookup"><span data-stu-id="e8e66-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="e8e66-139">Se si è interessati in altre informazioni su come toomanage SQL Data Warehouse a livello di codice, vedere l'articolo su come toouse [i cmdlet di PowerShell e API REST][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="e8e66-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
