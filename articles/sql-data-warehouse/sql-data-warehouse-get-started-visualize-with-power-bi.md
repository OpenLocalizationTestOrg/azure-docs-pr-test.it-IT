---
title: aaaVisualize dati di SQL Data Warehouse con Microsoft Azure di Power BI
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
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="7b417-103">Visualizzare i dati con Power BI</span><span class="sxs-lookup"><span data-stu-id="7b417-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b417-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="7b417-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="7b417-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b417-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="7b417-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b417-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="7b417-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="7b417-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="7b417-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="7b417-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="7b417-109">In questa esercitazione illustra come toouse Power BI tooconnect tooSQL Data Warehouse e creare alcune visualizzazioni di base.</span><span class="sxs-lookup"><span data-stu-id="7b417-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7b417-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7b417-110">Prerequisites</span></span>
<span data-ttu-id="7b417-111">toostep di questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="7b417-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="7b417-112">Un Data Warehouse SQL precaricati con database AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="7b417-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="7b417-113">tooprovision questa operazione, vedere [creare un Data Warehouse SQL] [ Create a SQL Data Warehouse] e selezionare i dati di esempio hello tooload.</span><span class="sxs-lookup"><span data-stu-id="7b417-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="7b417-114">Se si ha già un data warehouse, ma non i dati di esempio, è possibile [caricare manualmente i dati di esempio][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="7b417-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="7b417-115">1. La connessione a database tooyour</span><span class="sxs-lookup"><span data-stu-id="7b417-115">1. Connect tooyour database</span></span>
<span data-ttu-id="7b417-116">tooopen Power BI e connettersi a database AdventureWorksDW tooyour:</span><span class="sxs-lookup"><span data-stu-id="7b417-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="7b417-117">Sign in hello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="7b417-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="7b417-118">Fare clic su **Database SQL** e scegliere il database SQL Data Warehouse AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="7b417-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Trovare il database][1]
3. <span data-ttu-id="7b417-120">Fare clic su pulsante 'Apri in Power BI' hello.</span><span class="sxs-lookup"><span data-stu-id="7b417-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Pulsante Power BI][2]
4. <span data-ttu-id="7b417-122">Dovrebbe essere pagina connessione di SQL Data Warehouse hello visualizzando l'indirizzo web di database.</span><span class="sxs-lookup"><span data-stu-id="7b417-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="7b417-123">Fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="7b417-123">Click next.</span></span>
   
    ![Connessione a Power BI][3]
5. <span data-ttu-id="7b417-125">Immettere il nome utente del server SQL Azure e la password e sarà completamente connesso tooyour database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7b417-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Accesso a Power BI][4]
6. <span data-ttu-id="7b417-127">Dopo l'accesso a Power BI, fare clic su set di dati AdventureWorksDW hello nel pannello sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="7b417-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="7b417-128">Verrà aperto il database di hello.</span><span class="sxs-lookup"><span data-stu-id="7b417-128">This will open hello database.</span></span>
   
    ![Apertura di AdventureWorksDW in Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="7b417-130">2. Creare un report</span><span class="sxs-lookup"><span data-stu-id="7b417-130">2. Create a report</span></span>
<span data-ttu-id="7b417-131">Si è ora pronti toouse Power BI tooanalyze i dati di esempio AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="7b417-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="7b417-132">analisi di hello tooperform, AdventureWorksDW dispone di una vista denominata AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="7b417-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="7b417-133">Questa vista contiene alcune metriche chiave di hello per l'analisi delle vendite hello della società hello.</span><span class="sxs-lookup"><span data-stu-id="7b417-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="7b417-134">toocreate una mappa dell'importo delle vendite in base a codice toopostal, nel riquadro di destra campi hello, fare clic su hello AggregateSales visualizzazione tooexpand è.</span><span class="sxs-lookup"><span data-stu-id="7b417-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="7b417-135">Fare clic su tooselect di colonne PostalCode e SalesAmount hello li.</span><span class="sxs-lookup"><span data-stu-id="7b417-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Selezione di AggregateSales in Power BI][6]
   
    <span data-ttu-id="7b417-137">Power BI riconosce automaticamente tali informazioni come dati geografici e le inserisce direttamente in una mappa.</span><span class="sxs-lookup"><span data-stu-id="7b417-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mappa di Power BI][7]
2. <span data-ttu-id="7b417-139">In questo passaggio viene creato un grafico a barre che mostra gli importi delle vendite per reddito del cliente.</span><span class="sxs-lookup"><span data-stu-id="7b417-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="7b417-140">toocreate questo toohello passa espanso AggregateSales visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7b417-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="7b417-141">Fare clic su campo SalesAmount hello.</span><span class="sxs-lookup"><span data-stu-id="7b417-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="7b417-142">Trascinare hello reddito del cliente campo toohello sinistro e rilasciarlo nell'asse.</span><span class="sxs-lookup"><span data-stu-id="7b417-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Selezione asse in Power BI][8]
   
    <span data-ttu-id="7b417-144">Grafico a barre hello è stata spostata su hello sinistra.</span><span class="sxs-lookup"><span data-stu-id="7b417-144">We moved hello bar chart over hello left.</span></span>
   
    ![Barra di Power BI][9]
3. <span data-ttu-id="7b417-146">In questo passaggio viene creato un grafico a linee che mostra gli importi delle vendite per data dell'ordine.</span><span class="sxs-lookup"><span data-stu-id="7b417-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="7b417-147">toocreate questo toohello passa espanso AggregateSales visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7b417-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="7b417-148">Fare clic su SalesAmount e OrderDate.</span><span class="sxs-lookup"><span data-stu-id="7b417-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="7b417-149">Nella colonna visualizzazioni hello fare clic sull'icona di grafico a linee di hello; si tratta prima icona hello nella seconda riga di hello in visualizzazioni.</span><span class="sxs-lookup"><span data-stu-id="7b417-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Selezione del grafico a linee in Power BI][10]
   
    <span data-ttu-id="7b417-151">Ora disponibile un report che mostra tre visualizzazioni diverse dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="7b417-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Riga di Power BI][11]

<span data-ttu-id="7b417-153">Per salvare lo stato in qualsiasi momento, fare clic su **File** e selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7b417-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b417-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b417-154">Next steps</span></span>
<span data-ttu-id="7b417-155">Ora che ti forniamo alcuni toowarm ora con dati di esempio hello, vedere come troppo[sviluppare][develop], [caricare][load], o [ eseguire la migrazione][migrate].</span><span class="sxs-lookup"><span data-stu-id="7b417-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="7b417-156">O dare un'occhiata hello [sito Web di Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="7b417-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

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
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
