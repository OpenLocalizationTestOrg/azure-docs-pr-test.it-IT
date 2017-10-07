---
<span data-ttu-id="1c765-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 6: creare misure | Descrizione di "Microsoft Docs: viene descritto come toocreate misure nel progetto di esercitazione di hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="1c765-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="1c765-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="1c765-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="1c765-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend</span><span class="sxs-lookup"><span data-stu-id="1c765-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="1c765-104">Lezione 6: Creare misure</span><span class="sxs-lookup"><span data-stu-id="1c765-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="1c765-105">In questa lezione, creare misure toobe inclusi nel modello.</span><span class="sxs-lookup"><span data-stu-id="1c765-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="1c765-106">Toohello simile calcolata colonne che è stato creato, una misura è un calcolo creato utilizzando una formula DAX.</span><span class="sxs-lookup"><span data-stu-id="1c765-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="1c765-107">Tuttavia, a differenza delle colonne calcolate, le misure vengono valutate in base a un *filtro* selezionato dall'utente,</span><span class="sxs-lookup"><span data-stu-id="1c765-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="1c765-108">Ad esempio, una determinata colonna o sezionamento aggiunto campo etichette di riga toohello in una tabella pivot.</span><span class="sxs-lookup"><span data-stu-id="1c765-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="1c765-109">Viene quindi calcolato un valore per ogni cella nel filtro hello dalla misura hello applicato.</span><span class="sxs-lookup"><span data-stu-id="1c765-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="1c765-110">Le misure sono calcoli potenti e flessibili che si desidera tooinclude in quasi tutti i modelli tabulari tooperform i calcoli dinamici sui dati numerici.</span><span class="sxs-lookup"><span data-stu-id="1c765-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="1c765-111">vedere, più toolearn [misure](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="1c765-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="1c765-112">le misure toocreate, utilizzare hello *griglia delle misure*.</span><span class="sxs-lookup"><span data-stu-id="1c765-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="1c765-113">Per impostazione predefinita, ogni tabella ha una griglia delle misure vuota, ma di solito non si creano misure per ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="1c765-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="1c765-114">la griglia delle misure Hello viene visualizzata sotto una tabella in Progettazione modelli di hello in vista dati.</span><span class="sxs-lookup"><span data-stu-id="1c765-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="1c765-115">griglia delle misure hello toohide o Mostra per una tabella, fare clic su hello **tabella** menu e quindi fare clic su **Mostra griglia delle misure**.</span><span class="sxs-lookup"><span data-stu-id="1c765-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="1c765-116">È possibile creare una misura facendo clic su una cella vuota nella griglia delle misure hello, e quindi digitando una formula DAX nella barra della formula hello.</span><span class="sxs-lookup"><span data-stu-id="1c765-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="1c765-117">Quando fare clic su invio toocomplete hello formula, misura hello quindi viene visualizzato nella cella hello.</span><span class="sxs-lookup"><span data-stu-id="1c765-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="1c765-118">È inoltre possibile creare misure utilizzando una funzione di aggregazione standard facendo clic su una colonna e quindi fare clic sul pulsante Somma automatica di hello (**∑**) sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="1c765-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="1c765-119">Le misure create utilizzando funzionalità Somma automatica hello visualizzata nella cella della griglia di misure hello direttamente sotto la colonna hello, ma possono essere spostate.</span><span class="sxs-lookup"><span data-stu-id="1c765-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="1c765-120">In questa lezione, creare misure sia immettendo una formula DAX nella barra della formula hello e la funzionalità Somma automatica hello.</span><span class="sxs-lookup"><span data-stu-id="1c765-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="1c765-121">Stimato toocomplete ora questa lezione: **30 minuti**</span><span class="sxs-lookup"><span data-stu-id="1c765-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="1c765-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1c765-122">Prerequisites</span></span>  
<span data-ttu-id="1c765-123">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="1c765-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="1c765-124">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 5: creare colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1c765-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="1c765-125">Creare misure</span><span class="sxs-lookup"><span data-stu-id="1c765-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="1c765-126">una misura DaysCurrentQuarterToDate tabella DimDate hello toocreate</span><span class="sxs-lookup"><span data-stu-id="1c765-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="1c765-127">In Progettazione modelli di hello, fare clic su hello **DimDate** tabella.</span><span class="sxs-lookup"><span data-stu-id="1c765-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="1c765-128">Nella griglia delle misure hello, fare clic sulla cella vuota in alto a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="1c765-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="1c765-129">Nella barra della formula hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="1c765-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="1c765-130">Cella superiore sinistra hello di notifica contiene ora un nome di misura, **DaysCurrentQuarterToDate**, seguito dal risultato di hello, **92**.</span><span class="sxs-lookup"><span data-stu-id="1c765-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="1c765-132">A differenza delle colonne calcolate, con le formule delle misure è possibile digitare il nome di misura hello, seguito da due punti, seguiti dall'espressione formula hello.</span><span class="sxs-lookup"><span data-stu-id="1c765-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="1c765-133">una misura DaysInCurrentQuarter tabella DimDate hello toocreate</span><span class="sxs-lookup"><span data-stu-id="1c765-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="1c765-134">Con hello **DimDate** ancora attiva in Progettazione modelli di hello, nella griglia delle misure hello, fare clic sulla cella vuota di hello sotto misura hello creata.</span><span class="sxs-lookup"><span data-stu-id="1c765-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="1c765-135">Nella barra della formula hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="1c765-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="1c765-136">Quando si crea un rapporto di confronto tra un periodo incompleto e hello periodo precedente.</span><span class="sxs-lookup"><span data-stu-id="1c765-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="1c765-137">formula Hello deve calcolare proporzione hello del periodo di hello trascorsa e confrontarla toohello stesso proporzioni in hello periodo precedente.</span><span class="sxs-lookup"><span data-stu-id="1c765-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="1c765-138">In questo caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] fornisce hello proporzione in hello, trascorso il periodo corrente.</span><span class="sxs-lookup"><span data-stu-id="1c765-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="1c765-139">una misura InternetDistinctCountSalesOrder nella tabella FactInternetSales hello toocreate</span><span class="sxs-lookup"><span data-stu-id="1c765-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="1c765-140">Fare clic su hello **FactInternetSales** tabella.</span><span class="sxs-lookup"><span data-stu-id="1c765-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="1c765-141">Fare clic su hello **SalesOrderNumber** intestazione di colonna.</span><span class="sxs-lookup"><span data-stu-id="1c765-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="1c765-142">Sulla barra degli strumenti hello, fare clic su hello sulla freccia avanti toohello Somma automatica (**∑**) e quindi selezionare **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="1c765-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="1c765-143">funzionalità Somma automatica Hello automaticamente creata una misura per la colonna selezionata da hello utilizzando una formula di aggregazione standard DistinctCount hello.</span><span class="sxs-lookup"><span data-stu-id="1c765-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="1c765-145">Nella griglia delle misure hello, fare clic su nuova misura hello e quindi in hello **proprietà** finestra, in **nome misura**, rinominare la misura hello troppo**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="1c765-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="1c765-146">toocreate misure aggiuntive nella tabella FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="1c765-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="1c765-147">La funzionalità Somma automatica hello, creare e denominare hello seguenti misure:</span><span class="sxs-lookup"><span data-stu-id="1c765-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="1c765-148">Colonna</span><span class="sxs-lookup"><span data-stu-id="1c765-148">Column</span></span>|<span data-ttu-id="1c765-149">Nome misura</span><span class="sxs-lookup"><span data-stu-id="1c765-149">Measure name</span></span>|<span data-ttu-id="1c765-150">Somma automatica (∑)</span><span class="sxs-lookup"><span data-stu-id="1c765-150">AutoSum (∑)</span></span>|<span data-ttu-id="1c765-151">Formula</span><span class="sxs-lookup"><span data-stu-id="1c765-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="1c765-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="1c765-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="1c765-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="1c765-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="1c765-154">Numero</span><span class="sxs-lookup"><span data-stu-id="1c765-154">Count</span></span>|<span data-ttu-id="1c765-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="1c765-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="1c765-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="1c765-156">OrderQuantity</span></span>|<span data-ttu-id="1c765-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="1c765-157">InternetTotalUnits</span></span>|<span data-ttu-id="1c765-158">Somma</span><span class="sxs-lookup"><span data-stu-id="1c765-158">Sum</span></span>|<span data-ttu-id="1c765-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="1c765-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="1c765-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="1c765-160">DiscountAmount</span></span>|<span data-ttu-id="1c765-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="1c765-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="1c765-162">Somma</span><span class="sxs-lookup"><span data-stu-id="1c765-162">Sum</span></span>|<span data-ttu-id="1c765-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="1c765-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="1c765-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="1c765-164">TotalProductCost</span></span>|<span data-ttu-id="1c765-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="1c765-165">InternetTotalProductCost</span></span>|<span data-ttu-id="1c765-166">Somma</span><span class="sxs-lookup"><span data-stu-id="1c765-166">Sum</span></span>|<span data-ttu-id="1c765-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="1c765-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="1c765-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="1c765-168">SalesAmount</span></span>|<span data-ttu-id="1c765-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="1c765-169">InternetTotalSales</span></span>|<span data-ttu-id="1c765-170">Somma</span><span class="sxs-lookup"><span data-stu-id="1c765-170">Sum</span></span>|<span data-ttu-id="1c765-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="1c765-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="1c765-172">Margin</span><span class="sxs-lookup"><span data-stu-id="1c765-172">Margin</span></span>|<span data-ttu-id="1c765-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="1c765-173">InternetTotalMargin</span></span>|<span data-ttu-id="1c765-174">Somma</span><span class="sxs-lookup"><span data-stu-id="1c765-174">Sum</span></span>|<span data-ttu-id="1c765-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="1c765-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="1c765-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="1c765-176">TaxAmt</span></span>|<span data-ttu-id="1c765-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="1c765-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="1c765-178">Somma</span><span class="sxs-lookup"><span data-stu-id="1c765-178">Sum</span></span>|<span data-ttu-id="1c765-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="1c765-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="1c765-180">Freight</span><span class="sxs-lookup"><span data-stu-id="1c765-180">Freight</span></span>|<span data-ttu-id="1c765-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="1c765-181">InternetTotalFreight</span></span>|<span data-ttu-id="1c765-182">Somma</span><span class="sxs-lookup"><span data-stu-id="1c765-182">Sum</span></span>|<span data-ttu-id="1c765-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="1c765-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="1c765-184">Facendo clic su una cella vuota nella griglia delle misure hello e utilizzando la barra della formula hello, creare e le misure seguenti hello nome nell'ordine:</span><span class="sxs-lookup"><span data-stu-id="1c765-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
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
  
<span data-ttu-id="1c765-185">Le misure create per la tabella FactInternetSales hello possono essere utilizzato tooanalyze dati finanziari critici, ad esempio vendite, costi e margine di profitto per elementi definiti dal filtro selezionato di hello utente.</span><span class="sxs-lookup"><span data-stu-id="1c765-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="1c765-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c765-186">What's next?</span></span>
<span data-ttu-id="1c765-187">[Lezione 7: Creare indicatori di prestazioni chiave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="1c765-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
