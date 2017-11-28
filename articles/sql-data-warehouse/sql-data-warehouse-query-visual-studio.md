---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Documenti Microsoft
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
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="6b99f-103">Connettersi tooSQL Data Warehouse con Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="6b99f-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b99f-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="6b99f-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="6b99f-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6b99f-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="6b99f-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b99f-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="6b99f-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="6b99f-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="6b99f-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="6b99f-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="6b99f-109">Utilizzare Visual Studio tooquery Azure SQL Data Warehouse in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6b99f-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="6b99f-110">Questo metodo Usa l'estensione di SQL Server Data Tools (SSDT) hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b99f-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6b99f-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6b99f-111">Prerequisites</span></span>
<span data-ttu-id="6b99f-112">toouse questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="6b99f-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="6b99f-113">Un'istanza di SQL Data Warehouse esistente.</span><span class="sxs-lookup"><span data-stu-id="6b99f-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="6b99f-114">toocreate uno, vedere [creare un Data Warehouse SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6b99f-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="6b99f-115">SSDT per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b99f-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="6b99f-116">Se Visual Studio è già installato, probabilmente SSDT è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="6b99f-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="6b99f-117">Per istruzioni sull'installazione e sulle opzioni, vedere [Installazione di Visual Studio e SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="6b99f-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="6b99f-118">Hello completo nome SQL server.</span><span class="sxs-lookup"><span data-stu-id="6b99f-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="6b99f-119">toofind questa operazione, vedere [connessione Data Warehouse tooSQL][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6b99f-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="6b99f-120">1. Connettersi tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6b99f-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="6b99f-121">Aprire Visual Studio 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="6b99f-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="6b99f-122">Aprire Esplora oggetti di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b99f-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="6b99f-123">toodo, selezionare **vista** > **Esplora oggetti di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6b99f-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Esplora oggetti di SQL Server][1]
3. <span data-ttu-id="6b99f-125">Fare clic su hello **aggiungere SQL Server** icona.</span><span class="sxs-lookup"><span data-stu-id="6b99f-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![Aggiungi SQL Server][2]
4. <span data-ttu-id="6b99f-127">Compilare i campi di hello nella finestra di tooServer hello Connect.</span><span class="sxs-lookup"><span data-stu-id="6b99f-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Connettersi tooServer][3]
   
   * <span data-ttu-id="6b99f-129">**Nome server**.</span><span class="sxs-lookup"><span data-stu-id="6b99f-129">**Server name**.</span></span> <span data-ttu-id="6b99f-130">Immettere hello **nome server** identificati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6b99f-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="6b99f-131">**Autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="6b99f-131">**Authentication**.</span></span> <span data-ttu-id="6b99f-132">Selezionare **Autenticazione di SQL Server** o **Autenticazione integrata di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b99f-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="6b99f-133">**Nome utente** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="6b99f-133">**User Name** and **Password**.</span></span> <span data-ttu-id="6b99f-134">Se è stata selezionata l'autenticazione di SQL Server, immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="6b99f-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="6b99f-135">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="6b99f-135">Click **Connect**.</span></span>
5. <span data-ttu-id="6b99f-136">tooexplore, espandere il server SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6b99f-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="6b99f-137">È possibile visualizzare i database di hello associati hello server.</span><span class="sxs-lookup"><span data-stu-id="6b99f-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="6b99f-138">Espandere AdventureWorksDW toosee hello tabelle nel database di esempio.</span><span class="sxs-lookup"><span data-stu-id="6b99f-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Esplorare AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="6b99f-140">2. Eseguire una query di esempio</span><span class="sxs-lookup"><span data-stu-id="6b99f-140">2. Run a sample query</span></span>
<span data-ttu-id="6b99f-141">Ora che una connessione è stata stabilita tooyour database, è possibile scrivere una query.</span><span class="sxs-lookup"><span data-stu-id="6b99f-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="6b99f-142">Fare clic con il pulsante destro del mouse sul database in Esplora oggetti di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b99f-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="6b99f-143">Scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="6b99f-143">Select **New Query**.</span></span> <span data-ttu-id="6b99f-144">Verrà visualizzata una nuova finestra di query.</span><span class="sxs-lookup"><span data-stu-id="6b99f-144">A new query window opens.</span></span>
   
    ![Nuova query][5]
3. <span data-ttu-id="6b99f-146">Copiare la query TSQL nella finestra query hello:</span><span class="sxs-lookup"><span data-stu-id="6b99f-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="6b99f-147">Eseguire query hello.</span><span class="sxs-lookup"><span data-stu-id="6b99f-147">Run hello query.</span></span> <span data-ttu-id="6b99f-148">toodo, fare clic sulla freccia verde hello o utilizzare hello seguente collegamento: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="6b99f-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Esegui query][6]
5. <span data-ttu-id="6b99f-150">Esaminare i risultati di query hello.</span><span class="sxs-lookup"><span data-stu-id="6b99f-150">Look at hello query results.</span></span> <span data-ttu-id="6b99f-151">In questo esempio, nella tabella FactInternetSales hello è 60398 righe.</span><span class="sxs-lookup"><span data-stu-id="6b99f-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Risultati query][7]

## <a name="next-steps"></a><span data-ttu-id="6b99f-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b99f-153">Next steps</span></span>
<span data-ttu-id="6b99f-154">Ora che è possibile connettersi ed eseguire query, provare [visualizzazione dei dati di hello con Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="6b99f-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="6b99f-155">tooconfigure l'ambiente per l'autenticazione di Azure Active Directory, vedere [autenticare tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6b99f-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
