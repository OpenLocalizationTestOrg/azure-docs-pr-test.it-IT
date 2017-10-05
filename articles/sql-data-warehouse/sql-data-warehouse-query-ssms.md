---
title: 'Connettersi ad Azure SQL Data Warehouse: SSMS | Documentazione Microsoft'
description: Usare SQL Server Management Studio (SSMS) per connettersi ed eseguire query in Azure SQL Data Warehouse.
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
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="dfc3a-103">Connettersi a SQL Data Warehouse con SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="dfc3a-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfc3a-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="dfc3a-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="dfc3a-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="dfc3a-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="dfc3a-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dfc3a-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="dfc3a-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="dfc3a-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="dfc3a-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="dfc3a-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="dfc3a-109">Usare SQL Server Management Studio (SSMS) per connettersi ed eseguire query in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dfc3a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dfc3a-110">Prerequisites</span></span>
<span data-ttu-id="dfc3a-111">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="dfc3a-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="dfc3a-112">Un'istanza di SQL Data Warehouse esistente.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="dfc3a-113">Per crearne una, vedere [Creare un Azure SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="dfc3a-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="dfc3a-114">SQL Server Management Studio (SSMS) installato.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="dfc3a-115">[Installare SSMS][Install SSMS] gratuitamente se non è già stato installato.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="dfc3a-116">Il nome completo dell'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="dfc3a-117">Per trovarlo, vedere [Connettersi ad Azure SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="dfc3a-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="dfc3a-118">1. Connettersi all'istanza di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dfc3a-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="dfc3a-119">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-119">Open SSMS.</span></span>
2. <span data-ttu-id="dfc3a-120">Aprire Esplora oggetti.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-120">Open Object Explorer.</span></span> <span data-ttu-id="dfc3a-121">A questo scopo, selezionare **File** > **Connetti Esplora oggetti**.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Esplora oggetti di SQL Server][1]
3. <span data-ttu-id="dfc3a-123">Compilare i campi nella finestra Connetti al server.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Connetti al server][2]
   
   * <span data-ttu-id="dfc3a-125">**Nome server**.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-125">**Server name**.</span></span> <span data-ttu-id="dfc3a-126">Immettere il **nome server** identificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="dfc3a-127">**Autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-127">**Authentication**.</span></span> <span data-ttu-id="dfc3a-128">Selezionare **Autenticazione di SQL Server** o **Autenticazione integrata di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="dfc3a-129">**Nome utente** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-129">**User Name** and **Password**.</span></span> <span data-ttu-id="dfc3a-130">Se è stata selezionata l'autenticazione di SQL Server, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="dfc3a-131">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-131">Click **Connect**.</span></span>
4. <span data-ttu-id="dfc3a-132">Per l'esplorazione, espandere il server SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="dfc3a-133">È possibile visualizzare i database associati al server.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="dfc3a-134">Espandere AdventureWorksDW per visualizzare le tabelle nel database di esempio.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Esplorare AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="dfc3a-136">2. Eseguire una query di esempio</span><span class="sxs-lookup"><span data-stu-id="dfc3a-136">2. Run a sample query</span></span>
<span data-ttu-id="dfc3a-137">Ora che è stata stabilita una connessione al database, è possibile scrivere una query.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="dfc3a-138">Fare clic con il pulsante destro del mouse sul database in Esplora oggetti di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="dfc3a-139">Scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-139">Select **New Query**.</span></span> <span data-ttu-id="dfc3a-140">Verrà visualizzata una nuova finestra di query.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-140">A new query window opens.</span></span>
   
    ![Nuova query][4]
3. <span data-ttu-id="dfc3a-142">Copiare la query TSQL seguente nella finestra di query:</span><span class="sxs-lookup"><span data-stu-id="dfc3a-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="dfc3a-143">Eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-143">Run the query.</span></span> <span data-ttu-id="dfc3a-144">A questo scopo, fare clic su `Execute` oppure usare la combinazione di tasti seguente: `F5`.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![Esegui query][5]
5. <span data-ttu-id="dfc3a-146">Osservare i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-146">Look at the query results.</span></span> <span data-ttu-id="dfc3a-147">In questo esempio la tabella FactInternetSales include 60398 righe.</span><span class="sxs-lookup"><span data-stu-id="dfc3a-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Risultati query][6]

## <a name="next-steps"></a><span data-ttu-id="dfc3a-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dfc3a-149">Next steps</span></span>
<span data-ttu-id="dfc3a-150">Ora che è possibile connettersi ed eseguire una query, provare a [visualizzare i dati con PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="dfc3a-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="dfc3a-151">Per configurare l'ambiente per l'autenticazione di Azure Active Directory, vedere [Eseguire l'autenticazione in SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="dfc3a-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
