---
<span data-ttu-id="f6af3-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 5: creare colonne calcolate | Descrizione di Microsoft Docs": descrive toocreate calcolo di colonne nel progetto di esercitazione di hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="f6af3-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="f6af3-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="f6af3-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="f6af3-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend</span><span class="sxs-lookup"><span data-stu-id="f6af3-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="f6af3-104">Lezione 5: Creare colonne calcolate</span><span class="sxs-lookup"><span data-stu-id="f6af3-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="f6af3-105">In questa lezione vengono creati dati nel modello aggiungendo colonne calcolate.</span><span class="sxs-lookup"><span data-stu-id="f6af3-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="f6af3-106">È possibile creare colonne calcolate (come le colonne personalizzate) quando si usa recupera dati, utilizzando hello Editor di Query o nel tipo di finestra di progettazione modello hello eseguire qui.</span><span class="sxs-lookup"><span data-stu-id="f6af3-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="f6af3-107">vedere, più toolearn [le colonne calcolate](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="f6af3-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="f6af3-108">Vengono create cinque nuove colonne calcolate in tre tabelle diverse.</span><span class="sxs-lookup"><span data-stu-id="f6af3-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="f6af3-109">Hello passaggi sono leggermente diversi per ogni attività che mostra esistono diversi modi toocreate colonne, rinominarle e posizionarli in diverse posizioni in una tabella.</span><span class="sxs-lookup"><span data-stu-id="f6af3-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="f6af3-110">Questa è anche la prima lezione in cui si usano espressioni DAX (Data Analysis Expressions).</span><span class="sxs-lookup"><span data-stu-id="f6af3-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="f6af3-111">DAX è un linguaggio speciale per la creazione di espressioni per formule altamente personalizzabili per i modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="f6af3-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="f6af3-112">In questa esercitazione, utilizzare le colonne calcolate toocreate DAX, misure e filtri di ruolo.</span><span class="sxs-lookup"><span data-stu-id="f6af3-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="f6af3-113">vedere, più toolearn [DAX nei modelli tabulari](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="f6af3-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="f6af3-114">Stimato toocomplete ora questa lezione: **15 minuti**</span><span class="sxs-lookup"><span data-stu-id="f6af3-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="f6af3-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f6af3-115">Prerequisites</span></span>  
<span data-ttu-id="f6af3-116">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="f6af3-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="f6af3-117">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 4: creare relazioni](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="f6af3-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="f6af3-118">Creare colonne calcolate</span><span class="sxs-lookup"><span data-stu-id="f6af3-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="f6af3-119">Creare una colonna calcolata di MonthCalendar tabella DimDate hello</span><span class="sxs-lookup"><span data-stu-id="f6af3-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="f6af3-120">Fare clic su hello **modello** menu > **vista modello** > **vista dati**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="f6af3-121">Le colonne calcolate possono essere create solo tramite Progettazione modelli di hello in vista dati.</span><span class="sxs-lookup"><span data-stu-id="f6af3-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="f6af3-122">In Progettazione modelli di hello, fare clic su hello **DimDate** tabella (scheda).</span><span class="sxs-lookup"><span data-stu-id="f6af3-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="f6af3-123">Pulsante destro del mouse hello **CalendarQuarter** intestazione di colonna e quindi fare clic su **Inserisci colonna**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="f6af3-124">Una nuova colonna denominata **calcolato 1 colonna** è toohello inserito a sinistra di hello **Calendar Quarter** colonna.</span><span class="sxs-lookup"><span data-stu-id="f6af3-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="f6af3-125">Nella barra della formula hello sopra la tabella hello, digitare hello seguente formula DAX: consente il completamento automatico si digita hello nomi completi di colonne e tabelle e gli elenchi di hello funzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="f6af3-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="f6af3-126">I valori vengono quindi popolati per tutte le righe di hello nella colonna calcolata hello.</span><span class="sxs-lookup"><span data-stu-id="f6af3-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="f6af3-127">È possibile scorrere verso il basso nella tabella hello, vedrai che le righe possono avere valori diversi per questa colonna, in base ai dati hello in ogni riga.</span><span class="sxs-lookup"><span data-stu-id="f6af3-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="f6af3-128">Rinominare questa colonna troppo**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="f6af3-130">colonna calcolata di MonthCalendar Hello fornisce un nome ordinabile per mese.</span><span class="sxs-lookup"><span data-stu-id="f6af3-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="f6af3-131">Creare una colonna calcolata DayOfWeek tabella DimDate hello</span><span class="sxs-lookup"><span data-stu-id="f6af3-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="f6af3-132">Con hello **DimDate** ancora attiva, fare clic sul hello **colonna** menu e quindi fare clic su **Aggiungi colonna**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="f6af3-133">Nella barra della formula hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="f6af3-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="f6af3-134">Al termine della compilazione hello formula, premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="f6af3-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="f6af3-135">Hello nuova colonna viene aggiunta a destra della tabella hello toohello.</span><span class="sxs-lookup"><span data-stu-id="f6af3-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="f6af3-136">Rinominare la colonna hello troppo**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="f6af3-137">Fare clic sull'intestazione di colonna hello e quindi trascinare la colonna hello tra hello **EnglishDayNameOfWeek** colonna e hello **DayNumberOfMonth** colonna.</span><span class="sxs-lookup"><span data-stu-id="f6af3-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="f6af3-138">Lo spostamento delle colonne nella tabella rende più semplice toonavigate.</span><span class="sxs-lookup"><span data-stu-id="f6af3-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="f6af3-139">colonna calcolata di Hello DayOfWeek fornisce un nome ordinabile per giorno hello della settimana.</span><span class="sxs-lookup"><span data-stu-id="f6af3-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="f6af3-140">Creare una colonna calcolata ProductSubcategoryName nella tabella DimProduct hello</span><span class="sxs-lookup"><span data-stu-id="f6af3-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="f6af3-141">In hello **DimProduct** tabella, toohello a destra della tabella di hello di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="f6af3-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="f6af3-142">Colonna più a destra di preavviso hello è denominata **Aggiungi colonna** (in corsivo), fare clic sull'intestazione di colonna hello.</span><span class="sxs-lookup"><span data-stu-id="f6af3-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="f6af3-143">Nella barra della formula hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="f6af3-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="f6af3-144">Rinominare la colonna hello troppo**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="f6af3-145">colonna calcolata di Hello ProductSubcategoryName è toocreate utilizzata una gerarchia nella tabella DimProduct hello, che include i dati dalla colonna EnglishProductSubcategoryName hello nella tabella DimProductSubcategory hello.</span><span class="sxs-lookup"><span data-stu-id="f6af3-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="f6af3-146">Le gerarchie non possono essere estese a più di una tabella.</span><span class="sxs-lookup"><span data-stu-id="f6af3-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="f6af3-147">Le gerarchie verranno create più avanti nella lezione 9.</span><span class="sxs-lookup"><span data-stu-id="f6af3-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="f6af3-148">Creare una colonna calcolata ProductCategoryName nella tabella DimProduct hello</span><span class="sxs-lookup"><span data-stu-id="f6af3-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="f6af3-149">Con hello **DimProduct** ancora attiva, fare clic sul hello **colonna** menu e quindi fare clic su **Aggiungi colonna**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="f6af3-150">Nella barra della formula hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="f6af3-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="f6af3-151">Rinominare la colonna hello troppo**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="f6af3-152">colonna calcolata di ProductCategoryName Hello è toocreate utilizzata una gerarchia nella tabella DimProduct hello, che include dati dalla colonna EnglishProductCategoryName hello hello DimProductCategory tabella.</span><span class="sxs-lookup"><span data-stu-id="f6af3-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="f6af3-153">Le gerarchie non possono essere estese a più di una tabella.</span><span class="sxs-lookup"><span data-stu-id="f6af3-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="f6af3-154">Creare una colonna calcolata Margin nella tabella FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="f6af3-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="f6af3-155">In Progettazione modelli di hello, selezionare hello **FactInternetSales** tabella.</span><span class="sxs-lookup"><span data-stu-id="f6af3-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="f6af3-156">Creare una nuova colonna calcolata tra hello **SalesAmount** colonna e hello **TaxAmt** colonna.</span><span class="sxs-lookup"><span data-stu-id="f6af3-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="f6af3-157">Nella barra della formula hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="f6af3-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="f6af3-158">Rinominare la colonna hello troppo**margine**.</span><span class="sxs-lookup"><span data-stu-id="f6af3-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="f6af3-160">colonna calcolata Margin Hello è tooanalyze utilizzati i margini di profitto per ogni vendita.</span><span class="sxs-lookup"><span data-stu-id="f6af3-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="f6af3-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6af3-161">What's next?</span></span>
<span data-ttu-id="f6af3-162">[Lezione 6: Creare misure](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="f6af3-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
