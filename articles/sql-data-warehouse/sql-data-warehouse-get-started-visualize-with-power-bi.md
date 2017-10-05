---
title: Visualizzare i dati di SQL Data Warehouse con Power BI in Microsoft Azure
description: Visualizzare i dati di SQL Data Warehouse con Power BI
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a41393730143b14e91318a61858d989fff3786c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="daaf5-103">Visualizzare i dati con Power BI</span><span class="sxs-lookup"><span data-stu-id="daaf5-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="daaf5-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="daaf5-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="daaf5-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="daaf5-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="daaf5-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="daaf5-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="daaf5-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="daaf5-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="daaf5-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="daaf5-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="daaf5-109">Questa esercitazione illustra come usare Power BI per connettersi a SQL Data Warehouse e creare alcune visualizzazioni di base.</span><span class="sxs-lookup"><span data-stu-id="daaf5-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="daaf5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="daaf5-110">Prerequisites</span></span>
<span data-ttu-id="daaf5-111">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="daaf5-111">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="daaf5-112">Un'istanza di SQL Data Warehouse in cui sia precaricato il database AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="daaf5-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span></span> <span data-ttu-id="daaf5-113">Per effettuarne il provisioning, vedere [Creare un Azure SQL Data Warehouse][Create a SQL Data Warehouse] e scegliere di caricare i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="daaf5-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="daaf5-114">Se si ha già un data warehouse, ma non i dati di esempio, è possibile [caricare manualmente i dati di esempio][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="daaf5-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-to-your-database"></a><span data-ttu-id="daaf5-115">1. Connettersi al database</span><span class="sxs-lookup"><span data-stu-id="daaf5-115">1. Connect to your database</span></span>
<span data-ttu-id="daaf5-116">Per aprire Power BI e connettersi al database AdventureWorksDW:</span><span class="sxs-lookup"><span data-stu-id="daaf5-116">To open Power BI and connect to your AdventureWorksDW database:</span></span>

1. <span data-ttu-id="daaf5-117">Accedere al [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="daaf5-117">Sign into the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="daaf5-118">Fare clic su **Database SQL** e scegliere il database SQL Data Warehouse AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="daaf5-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Trovare il database][1]
3. <span data-ttu-id="daaf5-120">Fare clic sul pulsante Apri in Power BI.</span><span class="sxs-lookup"><span data-stu-id="daaf5-120">Click the 'Open in Power BI' button.</span></span>
   
    ![Pulsante Power BI][2]
4. <span data-ttu-id="daaf5-122">Verrà visualizzata la pagina di connessione di SQL Data Warehouse che visualizza l'indirizzo Web del database.</span><span class="sxs-lookup"><span data-stu-id="daaf5-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="daaf5-123">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="daaf5-123">Click next.</span></span>
   
    ![Connessione a Power BI][3]
5. <span data-ttu-id="daaf5-125">Immettere il nome utente e la password del server Azure SQL per connettersi al database SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="daaf5-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span></span>
   
    ![Accesso a Power BI][4]
6. <span data-ttu-id="daaf5-127">Dopo aver eseguito l'accesso a Power BI, fare clic sul set di dati AdventureWorksDW nel pannello sinistro.</span><span class="sxs-lookup"><span data-stu-id="daaf5-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span></span> <span data-ttu-id="daaf5-128">Verrà aperto il database.</span><span class="sxs-lookup"><span data-stu-id="daaf5-128">This will open the database.</span></span>
   
    ![Apertura di AdventureWorksDW in Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="daaf5-130">2. Creare un report</span><span class="sxs-lookup"><span data-stu-id="daaf5-130">2. Create a report</span></span>
<span data-ttu-id="daaf5-131">È ora possibile usare Power BI per analizzare i dati di esempio di AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="daaf5-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="daaf5-132">Per eseguire l'analisi, AdventureWorksDW dispone di una visualizzazione denominata VenditeAggregate.</span><span class="sxs-lookup"><span data-stu-id="daaf5-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="daaf5-133">Questa visualizzazione contiene alcune metriche chiave per l'analisi delle vendite della società.</span><span class="sxs-lookup"><span data-stu-id="daaf5-133">This view contains a few of the key metrics for analyzing the sales of the company.</span></span>

1. <span data-ttu-id="daaf5-134">Per creare una mappa degli importi di vendita in base al codice postale, nel riquadro con i campi a destra fare clic su AggregateSales per espanderlo.</span><span class="sxs-lookup"><span data-stu-id="daaf5-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span></span> <span data-ttu-id="daaf5-135">Fare clic sulle colonne PostalCode e SalesAmount per selezionarle.</span><span class="sxs-lookup"><span data-stu-id="daaf5-135">Click the PostalCode and SalesAmount columns to select them.</span></span>
   
    ![Selezione di AggregateSales in Power BI][6]
   
    <span data-ttu-id="daaf5-137">Power BI riconosce automaticamente tali informazioni come dati geografici e le inserisce direttamente in una mappa.</span><span class="sxs-lookup"><span data-stu-id="daaf5-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mappa di Power BI][7]
2. <span data-ttu-id="daaf5-139">In questo passaggio viene creato un grafico a barre che mostra gli importi delle vendite per reddito del cliente.</span><span class="sxs-lookup"><span data-stu-id="daaf5-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="daaf5-140">Per creare il grafico, passare alla visualizzazione AggregateSales espansa.</span><span class="sxs-lookup"><span data-stu-id="daaf5-140">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="daaf5-141">Fare clic sul campo SalesAmount.</span><span class="sxs-lookup"><span data-stu-id="daaf5-141">Click the SalesAmount field.</span></span> <span data-ttu-id="daaf5-142">Trascinare il campo Customer Income a sinistra e rilasciarlo sull'asse.</span><span class="sxs-lookup"><span data-stu-id="daaf5-142">Drag the Customer Income field to the left and drop it into Axis.</span></span>
   
    ![Selezione asse in Power BI][8]
   
    <span data-ttu-id="daaf5-144">Il grafico a barre è stato spostato a sinistra.</span><span class="sxs-lookup"><span data-stu-id="daaf5-144">We moved the bar chart over the left.</span></span>
   
    ![Barra di Power BI][9]
3. <span data-ttu-id="daaf5-146">In questo passaggio viene creato un grafico a linee che mostra gli importi delle vendite per data dell'ordine.</span><span class="sxs-lookup"><span data-stu-id="daaf5-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="daaf5-147">Per creare il grafico, passare alla visualizzazione AggregateSales espansa.</span><span class="sxs-lookup"><span data-stu-id="daaf5-147">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="daaf5-148">Fare clic su SalesAmount e OrderDate.</span><span class="sxs-lookup"><span data-stu-id="daaf5-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="daaf5-149">Nella colonna Visualizzazioni fare clic sull'icona del grafico a linee. Si tratta della prima icona nella seconda riga in Visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="daaf5-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span></span>
   
    ![Selezione del grafico a linee in Power BI][10]
   
    <span data-ttu-id="daaf5-151">Ora è disponibile un report che mostra tre diverse visualizzazioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="daaf5-151">You now have a report that shows three different visualizations of the data.</span></span>
   
    ![Riga di Power BI][11]

<span data-ttu-id="daaf5-153">Per salvare lo stato in qualsiasi momento, fare clic su **File** e selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="daaf5-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daaf5-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="daaf5-154">Next steps</span></span>
<span data-ttu-id="daaf5-155">Dopo essersi esercitati con i dati di esempio, si passerà ora alle operazioni di [sviluppo][develop], [caricamento][load] o [migrazione][migrate].</span><span class="sxs-lookup"><span data-stu-id="daaf5-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="daaf5-156">In alternativa, vedere il [sito Web di Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="daaf5-156">Or take a look at the [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting to SQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
