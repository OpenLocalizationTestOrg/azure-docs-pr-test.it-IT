---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Documenti Microsoft
description: Utilizzare SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="e9b1a-103">Connettersi tooSQL Data Warehouse con SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="e9b1a-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9b1a-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="e9b1a-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="e9b1a-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e9b1a-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="e9b1a-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9b1a-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="e9b1a-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="e9b1a-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="e9b1a-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="e9b1a-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="e9b1a-109">Utilizzare SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e9b1a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e9b1a-110">Prerequisites</span></span>
<span data-ttu-id="e9b1a-111">toouse questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e9b1a-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="e9b1a-112">Un'istanza di SQL Data Warehouse esistente.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="e9b1a-113">toocreate uno, vedere [creare un Data Warehouse SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e9b1a-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="e9b1a-114">SQL Server Management Studio (SSMS) installato.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="e9b1a-115">[Installare SSMS][Install SSMS] gratuitamente se non è già stato installato.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="e9b1a-116">Hello completo nome SQL server.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="e9b1a-117">toofind questa operazione, vedere [connessione Data Warehouse tooSQL][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e9b1a-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="e9b1a-118">1. Connettersi tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e9b1a-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="e9b1a-119">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-119">Open SSMS.</span></span>
2. <span data-ttu-id="e9b1a-120">Aprire Esplora oggetti.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-120">Open Object Explorer.</span></span> <span data-ttu-id="e9b1a-121">toodo, selezionare **File** > **Connetti Esplora oggetti**.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Esplora oggetti di SQL Server][1]
3. <span data-ttu-id="e9b1a-123">Compilare i campi di hello nella finestra di tooServer hello Connect.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Connettersi tooServer][2]
   
   * <span data-ttu-id="e9b1a-125">**Nome server**.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-125">**Server name**.</span></span> <span data-ttu-id="e9b1a-126">Immettere hello **nome server** identificati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="e9b1a-127">**Autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-127">**Authentication**.</span></span> <span data-ttu-id="e9b1a-128">Selezionare **Autenticazione di SQL Server** o **Autenticazione integrata di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="e9b1a-129">**Nome utente** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-129">**User Name** and **Password**.</span></span> <span data-ttu-id="e9b1a-130">Se è stata selezionata l'autenticazione di SQL Server, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="e9b1a-131">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-131">Click **Connect**.</span></span>
4. <span data-ttu-id="e9b1a-132">tooexplore, espandere il server SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="e9b1a-133">È possibile visualizzare i database di hello associati hello server.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="e9b1a-134">Espandere AdventureWorksDW toosee hello tabelle nel database di esempio.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Esplorare AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="e9b1a-136">2. Eseguire una query di esempio</span><span class="sxs-lookup"><span data-stu-id="e9b1a-136">2. Run a sample query</span></span>
<span data-ttu-id="e9b1a-137">Ora che una connessione è stata stabilita tooyour database, è possibile scrivere una query.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="e9b1a-138">Fare clic con il pulsante destro del mouse sul database in Esplora oggetti di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="e9b1a-139">Scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-139">Select **New Query**.</span></span> <span data-ttu-id="e9b1a-140">Verrà visualizzata una nuova finestra di query.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-140">A new query window opens.</span></span>
   
    ![Nuova query][4]
3. <span data-ttu-id="e9b1a-142">Copiare la query TSQL nella finestra query hello:</span><span class="sxs-lookup"><span data-stu-id="e9b1a-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="e9b1a-143">Eseguire query hello.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-143">Run hello query.</span></span> <span data-ttu-id="e9b1a-144">toodo, fare clic su `Execute` o utilizzare hello seguente collegamento: `F5`.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Esegui query][5]
5. <span data-ttu-id="e9b1a-146">Esaminare i risultati di query hello.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-146">Look at hello query results.</span></span> <span data-ttu-id="e9b1a-147">In questo esempio, nella tabella FactInternetSales hello è 60398 righe.</span><span class="sxs-lookup"><span data-stu-id="e9b1a-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Risultati query][6]

## <a name="next-steps"></a><span data-ttu-id="e9b1a-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9b1a-149">Next steps</span></span>
<span data-ttu-id="e9b1a-150">Ora che è possibile connettersi ed eseguire query, provare [visualizzazione dei dati di hello con Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="e9b1a-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="e9b1a-151">tooconfigure l'ambiente per l'autenticazione di Azure Active Directory, vedere [autenticare tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e9b1a-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
