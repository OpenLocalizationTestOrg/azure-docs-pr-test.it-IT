---
title: 'Esercitazione su Azure Analysis Services - Lezione 6: Creare misure | Microsoft Docs'
description: Descrive come creare misure nel progetto per l'esercitazione su Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 90833fa9744eac298b0da82cd3d12f27cc237510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="b617c-103">Lezione 6: Creare misure</span><span class="sxs-lookup"><span data-stu-id="b617c-103">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b617c-104">In questa lezione verranno create le misure da includere nel modello.</span><span class="sxs-lookup"><span data-stu-id="b617c-104">In this lesson, you create measures to be included in your model.</span></span> <span data-ttu-id="b617c-105">In modo simile alle colonne calcolate create, una misura è un calcolo creato usando una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="b617c-105">Similar to the calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="b617c-106">Tuttavia, a differenza delle colonne calcolate, le misure vengono valutate in base a un *filtro* selezionato dall'utente,</span><span class="sxs-lookup"><span data-stu-id="b617c-106">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="b617c-107">ad esempio una particolare colonna o un filtro dei dati aggiunto al campo Etichette di riga in una tabella pivot.</span><span class="sxs-lookup"><span data-stu-id="b617c-107">For example, a particular column or slicer added to the Row Labels field in a PivotTable.</span></span> <span data-ttu-id="b617c-108">Con la misura applicata viene quindi calcolato un valore per ogni cella nel filtro.</span><span class="sxs-lookup"><span data-stu-id="b617c-108">A value for each cell in the filter is then calculated by the applied measure.</span></span> <span data-ttu-id="b617c-109">Le misure sono calcoli potenti e flessibili che è utile includere in quasi tutti i modelli tabulari per eseguire calcoli dinamici su dati numerici.</span><span class="sxs-lookup"><span data-stu-id="b617c-109">Measures are powerful, flexible calculations that you want to include in almost all tabular models to perform dynamic calculations on numerical data.</span></span> <span data-ttu-id="b617c-110">Per altre informazioni, vedere [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular) (Misure).</span><span class="sxs-lookup"><span data-stu-id="b617c-110">To learn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="b617c-111">Per creare le misure si usa la *griglia delle misure*.</span><span class="sxs-lookup"><span data-stu-id="b617c-111">To create measures, you use the *Measure Grid*.</span></span> <span data-ttu-id="b617c-112">Per impostazione predefinita, ogni tabella ha una griglia delle misure vuota, ma di solito non si creano misure per ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="b617c-112">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="b617c-113">La griglia delle misure viene visualizzata sotto una tabella nella finestra di progettazione dei modelli in vista dati.</span><span class="sxs-lookup"><span data-stu-id="b617c-113">The measure grid appears below a table in the model designer when in Data View.</span></span> <span data-ttu-id="b617c-114">Per mostrare o nascondere la griglia delle misure per una tabella, fare clic sul menu **Tabella** e quindi fare clic su **Mostra griglia delle misure**.</span><span class="sxs-lookup"><span data-stu-id="b617c-114">To hide or show the measure grid for a table, click the **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="b617c-115">È possibile creare una misura facendo clic su una cella vuota nella griglia delle misure e quindi digitando una formula DAX nella barra della formula.</span><span class="sxs-lookup"><span data-stu-id="b617c-115">You can create a measure by clicking an empty cell in the measure grid, and then typing a DAX formula in the formula bar.</span></span> <span data-ttu-id="b617c-116">Quando si preme INVIO per completare la formula, la misura verrà quindi visualizzata nella cella.</span><span class="sxs-lookup"><span data-stu-id="b617c-116">When you click ENTER to complete the formula, the measure then appears in the cell.</span></span> <span data-ttu-id="b617c-117">È anche possibile creare misure con una funzione di aggregazione standard facendo clic su una colonna e quindi sul pulsante Somma automatica (**∑**) sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="b617c-117">You can also create measures using a standard aggregation function by clicking a column, and then clicking the AutoSum button (**∑**) on the toolbar.</span></span> <span data-ttu-id="b617c-118">Le misure create con la funzionalità Somma automatica vengono visualizzate nella cella della griglia delle misure direttamente sotto la colonna, ma possono essere spostate.</span><span class="sxs-lookup"><span data-stu-id="b617c-118">Measures created using the AutoSum feature appear in the measure grid cell directly beneath the column, but can be moved.</span></span>  
  
<span data-ttu-id="b617c-119">In questa lezione le misure vengono create sia immettendo una formula DAX nella barra della formula che usando la funzionalità Somma automatica.</span><span class="sxs-lookup"><span data-stu-id="b617c-119">In this lesson, you create measures by both entering a DAX formula in the formula bar, and by using the AutoSum feature.</span></span>  
  
<span data-ttu-id="b617c-120">Tempo previsto per il completamento della lezione: **30 minuti**</span><span class="sxs-lookup"><span data-stu-id="b617c-120">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b617c-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b617c-121">Prerequisites</span></span>  
<span data-ttu-id="b617c-122">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="b617c-122">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b617c-123">Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 5: Creare colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b617c-123">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="b617c-124">Creare misure</span><span class="sxs-lookup"><span data-stu-id="b617c-124">Create measures</span></span>  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a><span data-ttu-id="b617c-125">Per creare una misura DaysCurrentQuarterToDate nella tabella DimDate</span><span class="sxs-lookup"><span data-stu-id="b617c-125">To create a DaysCurrentQuarterToDate measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="b617c-126">Nella finestra di progettazione dei modelli fare clic sula tabella **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="b617c-126">In the model designer, click the **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="b617c-127">Nella griglia delle misure fare clic sulla cella vuota in alto a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b617c-127">In the measure grid, click the top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="b617c-128">Nella barra della formula digitare la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="b617c-128">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="b617c-129">Si noti che la cella in alto a sinistra contiene ora un nome di misura, **DaysCurrentQuarterToDate**, seguito dal risultato, **92**.</span><span class="sxs-lookup"><span data-stu-id="b617c-129">Notice the top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by the result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="b617c-131">Diversamente dalle colonne calcolate, con le formule per le misure è possibile digitare il nome della misura, seguito da due punti, seguiti dall'espressione della formula.</span><span class="sxs-lookup"><span data-stu-id="b617c-131">Unlike calculated columns, with measure formulas you can type the measure name, followed by a colon, followed by the formula expression.</span></span>

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a><span data-ttu-id="b617c-132">Per creare una misura DaysInCurrentQuarter nella tabella DimDate</span><span class="sxs-lookup"><span data-stu-id="b617c-132">To create a DaysInCurrentQuarter measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="b617c-133">Con la tabella **DimDate** ancora attiva nella finestra di progettazione dei modelli, nella griglia delle misure fare clic sulla cella vuota sotto la misura creata.</span><span class="sxs-lookup"><span data-stu-id="b617c-133">With the **DimDate** table still active in the model designer, in the measure grid, click the empty cell below the measure you created.</span></span>  
  
2.  <span data-ttu-id="b617c-134">Nella barra della formula digitare la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="b617c-134">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="b617c-135">Quando si crea un rapporto di confronto tra un periodo incompleto e il periodo precedente,</span><span class="sxs-lookup"><span data-stu-id="b617c-135">When creating a comparison ratio between one incomplete period and the previous period.</span></span> <span data-ttu-id="b617c-136">la formula deve tenere conto della proporzione del periodo trascorso e confrontarla con la stessa proporzione del periodo precedente.</span><span class="sxs-lookup"><span data-stu-id="b617c-136">The formula must calculate the proportion of the period that has elapsed and compare it to the same proportion in the previous period.</span></span> <span data-ttu-id="b617c-137">In questo caso, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] restituisce la proporzione per il periodo corrente.</span><span class="sxs-lookup"><span data-stu-id="b617c-137">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives the proportion elapsed in the current period.</span></span>  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a><span data-ttu-id="b617c-138">Per creare una misura InternetDistinctCountSalesOrder nella tabella FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="b617c-138">To create an InternetDistinctCountSalesOrder measure in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="b617c-139">Fare clic sulla tabella **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="b617c-139">Click the **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="b617c-140">Fare clic sull'intestazione di colonna **SalesOrderNumber**.</span><span class="sxs-lookup"><span data-stu-id="b617c-140">Click the **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="b617c-141">Sulla barra degli strumenti fare clic sulla freccia in giù accanto a Somma automatica (**∑**) e quindi selezionare **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="b617c-141">On the toolbar, click the down-arrow next to the AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="b617c-142">La funzionalità Somma automatica crea automaticamente una misura per la colonna selezionata usando la formula di aggregazione standard DistinctCount.</span><span class="sxs-lookup"><span data-stu-id="b617c-142">The AutoSum feature automatically creates a measure for the selected column using the DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="b617c-144">Nella griglia delle misure fare clic sulla nuova misura e quindi nella finestra **Proprietà**, in **Nome misura**, rinominare la misura in **InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="b617c-144">In the measure grid, click the new measure, and then in the **Properties** window, in **Measure Name**, rename the measure to **InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a><span data-ttu-id="b617c-145">Per creare altre misure nella tabella FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="b617c-145">To create additional measures in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="b617c-146">Usare la funzionalità Somma automatica e creare le misure seguenti con i nomi indicati:</span><span class="sxs-lookup"><span data-stu-id="b617c-146">By using the AutoSum feature, create and name the following measures:</span></span>  

    |<span data-ttu-id="b617c-147">Colonna</span><span class="sxs-lookup"><span data-stu-id="b617c-147">Column</span></span>|<span data-ttu-id="b617c-148">Nome misura</span><span class="sxs-lookup"><span data-stu-id="b617c-148">Measure name</span></span>|<span data-ttu-id="b617c-149">Somma automatica (∑)</span><span class="sxs-lookup"><span data-stu-id="b617c-149">AutoSum (∑)</span></span>|<span data-ttu-id="b617c-150">Formula</span><span class="sxs-lookup"><span data-stu-id="b617c-150">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="b617c-151">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="b617c-151">SalesOrderLineNumber</span></span>|<span data-ttu-id="b617c-152">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="b617c-152">InternetOrderLinesCount</span></span>|<span data-ttu-id="b617c-153">Numero</span><span class="sxs-lookup"><span data-stu-id="b617c-153">Count</span></span>|<span data-ttu-id="b617c-154">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="b617c-154">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="b617c-155">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="b617c-155">OrderQuantity</span></span>|<span data-ttu-id="b617c-156">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="b617c-156">InternetTotalUnits</span></span>|<span data-ttu-id="b617c-157">Somma</span><span class="sxs-lookup"><span data-stu-id="b617c-157">Sum</span></span>|<span data-ttu-id="b617c-158">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="b617c-158">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="b617c-159">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="b617c-159">DiscountAmount</span></span>|<span data-ttu-id="b617c-160">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="b617c-160">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="b617c-161">Somma</span><span class="sxs-lookup"><span data-stu-id="b617c-161">Sum</span></span>|<span data-ttu-id="b617c-162">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="b617c-162">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="b617c-163">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="b617c-163">TotalProductCost</span></span>|<span data-ttu-id="b617c-164">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="b617c-164">InternetTotalProductCost</span></span>|<span data-ttu-id="b617c-165">Somma</span><span class="sxs-lookup"><span data-stu-id="b617c-165">Sum</span></span>|<span data-ttu-id="b617c-166">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="b617c-166">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="b617c-167">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="b617c-167">SalesAmount</span></span>|<span data-ttu-id="b617c-168">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="b617c-168">InternetTotalSales</span></span>|<span data-ttu-id="b617c-169">Somma</span><span class="sxs-lookup"><span data-stu-id="b617c-169">Sum</span></span>|<span data-ttu-id="b617c-170">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="b617c-170">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="b617c-171">Margin</span><span class="sxs-lookup"><span data-stu-id="b617c-171">Margin</span></span>|<span data-ttu-id="b617c-172">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="b617c-172">InternetTotalMargin</span></span>|<span data-ttu-id="b617c-173">Somma</span><span class="sxs-lookup"><span data-stu-id="b617c-173">Sum</span></span>|<span data-ttu-id="b617c-174">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="b617c-174">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="b617c-175">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="b617c-175">TaxAmt</span></span>|<span data-ttu-id="b617c-176">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="b617c-176">InternetTotalTaxAmt</span></span>|<span data-ttu-id="b617c-177">Somma</span><span class="sxs-lookup"><span data-stu-id="b617c-177">Sum</span></span>|<span data-ttu-id="b617c-178">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="b617c-178">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="b617c-179">Freight</span><span class="sxs-lookup"><span data-stu-id="b617c-179">Freight</span></span>|<span data-ttu-id="b617c-180">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="b617c-180">InternetTotalFreight</span></span>|<span data-ttu-id="b617c-181">Somma</span><span class="sxs-lookup"><span data-stu-id="b617c-181">Sum</span></span>|<span data-ttu-id="b617c-182">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="b617c-182">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="b617c-183">Facendo clic su una cella vuota nella griglia delle misure e usando quindi la barra della formula, creare le misure seguenti con il nome indicato in ordine:</span><span class="sxs-lookup"><span data-stu-id="b617c-183">By clicking an empty cell in the measure grid, and by using the formula bar, create, and name the following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="b617c-184">Le misure create per la tabella FactInternetSales possono essere usate per analizzare dati finanziari importanti, ad esempio vendite, costi e margine di profitto per gli elementi definiti dal filtro selezionato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="b617c-184">Measures created for the FactInternetSales table can be used to analyze critical financial data such as sales, costs, and profit margin for items defined by the user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="b617c-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b617c-185">What's next?</span></span>
<span data-ttu-id="b617c-186">[Lezione 7: Creare indicatori di prestazioni chiave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="b617c-186">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
