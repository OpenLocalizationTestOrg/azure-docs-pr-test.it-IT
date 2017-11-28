---
title: un Data Warehouse di SQL nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un Azure SQL Data Warehouse in hello portale di Azure
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="156f3-103">Creare un Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="156f3-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="156f3-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="156f3-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="156f3-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="156f3-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="156f3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="156f3-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="156f3-107">Questa esercitazione Usa hello toocreate portale Azure un SQL Data Warehouse che contiene un database di esempio AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="156f3-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="156f3-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="156f3-108">Prerequisites</span></span>
<span data-ttu-id="156f3-109">tooget avviato, è necessario:</span><span class="sxs-lookup"><span data-stu-id="156f3-109">tooget started, you need:</span></span>

* <span data-ttu-id="156f3-110">**Account Azure**: visitare [versione di valutazione gratuita di Azure] [ Azure Free Trial] o [crediti Azure MSDN] [ MSDN Azure Credits] toocreate un account.</span><span class="sxs-lookup"><span data-stu-id="156f3-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="156f3-111">**Server SQL Azure**: vedere [creare un database SQL di Azure con il portale di Azure hello] [ Create an Azure SQL database in hello Azure portal] per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="156f3-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="156f3-112">La creazione di un'istanza di SQL Data Warehouse può avere come risultato un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="156f3-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="156f3-113">Per altri dettagli, vedere la pagina relativa ai [prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="156f3-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="156f3-114">Creare un SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="156f3-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="156f3-115">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="156f3-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="156f3-116">Fare clic su **+ Nuovo** > **Database** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="156f3-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Create](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="156f3-118">In hello **SQL Data Warehouse** pannello, compilare informazioni hello necessarie, quindi premere toocreate 'Crea'.</span><span class="sxs-lookup"><span data-stu-id="156f3-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Creazione del database](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="156f3-120">**Server**: è consigliabile selezionare prima di tutto il server.</span><span class="sxs-lookup"><span data-stu-id="156f3-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="156f3-121">**Nome del database**: nome hello hello tooreference utilizzato SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="156f3-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="156f3-122">Deve essere univoco toohello server.</span><span class="sxs-lookup"><span data-stu-id="156f3-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="156f3-123">**Prestazioni**: è consigliabile iniziare con 400 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="156f3-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="156f3-124">È possibile spostare hello toohello di dispositivo di scorrimento sinistro o destro del mouse sulle prestazioni di hello tooadjust del data warehouse o scala verso l'alto o verso il basso dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="156f3-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="156f3-125">toolearn ulteriori informazioni su Dwu, vedere la documentazione su [scalabilità](sql-data-warehouse-manage-compute-overview.md) o la [pagina dei prezzi][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="156f3-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="156f3-126">**Sottoscrizione**: hello seleziona [sottoscrizione] che questo Data Warehouse SQL verranno fatturate per.</span><span class="sxs-lookup"><span data-stu-id="156f3-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="156f3-127">**Gruppo di risorse**: [gruppi di risorse] [ Resource group] sono toohelp contenitori progettati gestire una raccolta di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="156f3-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="156f3-128">Altre informazioni sui [gruppi di risorse](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="156f3-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="156f3-129">**Selezionare l'origine**: fare clic su **Selezionare l'origine** > **Esempio**.</span><span class="sxs-lookup"><span data-stu-id="156f3-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="156f3-130">Azure popola automaticamente hello **esempio seleziona** opzione con AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="156f3-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="156f3-131">regole di confronto predefinite Hello per un SQL Data Warehouse è SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="156f3-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="156f3-132">Se sono necessarie regole di confronto diverse, [T-SQL] [ T-SQL] può essere utilizzato toocreate hello database con regole di confronto diverse.</span><span class="sxs-lookup"><span data-stu-id="156f3-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="156f3-133">Fare clic su **crea** toocreate il SQL del Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="156f3-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="156f3-134">Attendere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="156f3-134">Wait for a few minutes.</span></span> <span data-ttu-id="156f3-135">Quando il data warehouse è pronto, devono essere restituiti toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="156f3-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="156f3-136">È possibile trovare il Data Warehouse di SQL nel dashboard, elencati in database SQL o nella risorsa hello gruppo è stato utilizzato toocreate è.</span><span class="sxs-lookup"><span data-stu-id="156f3-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![Visualizzazione del portale](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="156f3-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="156f3-138">Next steps</span></span>
<span data-ttu-id="156f3-139">Ora che è stato creato un SQL Data Warehouse, si è pronti troppo[Connetti](sql-data-warehouse-connect-overview.md) e iniziare l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="156f3-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="156f3-140">dati di tooload in SQL Data Warehouse, vedere hello [durante il caricamento di panoramica](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="156f3-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="156f3-141">Se si sta tentando di toomigrate un tooSQL di database del Data Warehouse esistente, vedere hello [Cenni preliminari sulla migrazione](sql-data-warehouse-overview-migrate.md) o utilizzare [utilità di migrazione](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="156f3-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="156f3-142">Le regole firewall possono anche essere configurate con Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="156f3-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="156f3-143">Per altre informazioni, vedere [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="156f3-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="156f3-144">È anche una buona idea toolook in hello [consigliate][Best practices].</span><span class="sxs-lookup"><span data-stu-id="156f3-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[sottoscrizione]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
