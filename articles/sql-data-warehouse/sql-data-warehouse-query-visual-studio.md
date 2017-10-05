---
title: 'Connettersi ad Azure SQL Data Warehouse: VSTS |Documentazione Microsoft'
description: Eseguire query in SQL Data Warehouse con Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="0f07b-103">Connettersi a SQL Data Warehouse con Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="0f07b-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f07b-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="0f07b-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="0f07b-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0f07b-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="0f07b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f07b-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="0f07b-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="0f07b-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="0f07b-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="0f07b-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="0f07b-109">È possibile usare Visual Studio per eseguire query in Azure SQL Data Warehouse in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0f07b-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="0f07b-110">Questo metodo usa l'estensione di SQL Server Data Tools (SSDT) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f07b-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0f07b-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0f07b-111">Prerequisites</span></span>
<span data-ttu-id="0f07b-112">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0f07b-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="0f07b-113">Un'istanza di SQL Data Warehouse esistente.</span><span class="sxs-lookup"><span data-stu-id="0f07b-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="0f07b-114">Per crearne una, vedere [Creare un Azure SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0f07b-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="0f07b-115">SSDT per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f07b-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="0f07b-116">Se Visual Studio è già installato, probabilmente SSDT è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="0f07b-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="0f07b-117">Per istruzioni sull'installazione e sulle opzioni, vedere [Installazione di Visual Studio e SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="0f07b-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="0f07b-118">Il nome completo dell'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f07b-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="0f07b-119">Per trovarlo, vedere [Connettersi ad Azure SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0f07b-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="0f07b-120">1. Connettersi all'istanza di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0f07b-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="0f07b-121">Aprire Visual Studio 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="0f07b-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="0f07b-122">Aprire Esplora oggetti di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f07b-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="0f07b-123">A questo scopo, selezionare **Visualizza** > **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0f07b-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Esplora oggetti di SQL Server][1]
3. <span data-ttu-id="0f07b-125">Fare clic sull'icona **Aggiungi SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="0f07b-125">Click the **Add SQL Server** icon.</span></span>
   
    ![Aggiungi SQL Server][2]
4. <span data-ttu-id="0f07b-127">Compilare i campi nella finestra Connetti al server.</span><span class="sxs-lookup"><span data-stu-id="0f07b-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Connetti al server][3]
   
   * <span data-ttu-id="0f07b-129">**Nome server**.</span><span class="sxs-lookup"><span data-stu-id="0f07b-129">**Server name**.</span></span> <span data-ttu-id="0f07b-130">Immettere il **nome server** identificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0f07b-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="0f07b-131">**Autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="0f07b-131">**Authentication**.</span></span> <span data-ttu-id="0f07b-132">Selezionare **Autenticazione di SQL Server** o **Autenticazione integrata di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f07b-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="0f07b-133">**Nome utente** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="0f07b-133">**User Name** and **Password**.</span></span> <span data-ttu-id="0f07b-134">Se è stata selezionata l'autenticazione di SQL Server, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="0f07b-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="0f07b-135">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0f07b-135">Click **Connect**.</span></span>
5. <span data-ttu-id="0f07b-136">Per l'esplorazione, espandere il server SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0f07b-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="0f07b-137">È possibile visualizzare i database associati al server.</span><span class="sxs-lookup"><span data-stu-id="0f07b-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="0f07b-138">Espandere AdventureWorksDW per visualizzare le tabelle nel database di esempio.</span><span class="sxs-lookup"><span data-stu-id="0f07b-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Esplorare AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="0f07b-140">2. Eseguire una query di esempio</span><span class="sxs-lookup"><span data-stu-id="0f07b-140">2. Run a sample query</span></span>
<span data-ttu-id="0f07b-141">Ora che è stata stabilita una connessione al database, è possibile scrivere una query.</span><span class="sxs-lookup"><span data-stu-id="0f07b-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="0f07b-142">Fare clic con il pulsante destro del mouse sul database in Esplora oggetti di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0f07b-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="0f07b-143">Scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="0f07b-143">Select **New Query**.</span></span> <span data-ttu-id="0f07b-144">Verrà visualizzata una nuova finestra di query.</span><span class="sxs-lookup"><span data-stu-id="0f07b-144">A new query window opens.</span></span>
   
    ![Nuova query][5]
3. <span data-ttu-id="0f07b-146">Copiare la query TSQL seguente nella finestra di query:</span><span class="sxs-lookup"><span data-stu-id="0f07b-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="0f07b-147">Eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="0f07b-147">Run the query.</span></span> <span data-ttu-id="0f07b-148">A questo scopo, fare clic sulla freccia verde oppure usare la combinazione di tasti seguente: `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="0f07b-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Esegui query][6]
5. <span data-ttu-id="0f07b-150">Osservare i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="0f07b-150">Look at the query results.</span></span> <span data-ttu-id="0f07b-151">In questo esempio la tabella FactInternetSales include 60398 righe.</span><span class="sxs-lookup"><span data-stu-id="0f07b-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Risultati query][7]

## <a name="next-steps"></a><span data-ttu-id="0f07b-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f07b-153">Next steps</span></span>
<span data-ttu-id="0f07b-154">Ora che è possibile connettersi ed eseguire una query, provare a [visualizzare i dati con PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="0f07b-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="0f07b-155">Per configurare l'ambiente per l'autenticazione di Azure Active Directory, vedere [Eseguire l'autenticazione in SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0f07b-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
