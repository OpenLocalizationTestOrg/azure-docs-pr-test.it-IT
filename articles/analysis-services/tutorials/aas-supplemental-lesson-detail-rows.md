---
<span data-ttu-id="400bb-101">titolo: aaa "lezione supplementare di Azure Analysis Services tutorial: righe di dettaglio | Descrizione di "Microsoft Docs: viene descritto come toocreate un espressione di righe di dettaglio in hello Azure Analysis Services tutorial.</span><span class="sxs-lookup"><span data-stu-id="400bb-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="400bb-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="400bb-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="400bb-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend</span><span class="sxs-lookup"><span data-stu-id="400bb-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="400bb-104">Lezione supplementare: Righe di dettaglio</span><span class="sxs-lookup"><span data-stu-id="400bb-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="400bb-105">In questa lezione supplementare, utilizzare Editor DAX toodefine hello un'espressione di righe di dettaglio personalizzata.</span><span class="sxs-lookup"><span data-stu-id="400bb-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="400bb-106">Un'espressione di righe di dettaglio è una proprietà su una misura, fornendo agli utenti finali di ulteriori informazioni sui risultati di hello aggregato di una misura.</span><span class="sxs-lookup"><span data-stu-id="400bb-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="400bb-107">Stimato toocomplete ora questa lezione: **10 minuti**</span><span class="sxs-lookup"><span data-stu-id="400bb-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="400bb-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="400bb-108">Prerequisites</span></span>  
<span data-ttu-id="400bb-109">L'argomento di questa lezione supplementare fa parte di un'esercitazione sulla creazione di modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="400bb-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="400bb-110">Prima di eseguire attività di hello in questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o dispone di un progetto di modello di esempio Adventure Works Internet Sales completato.</span><span class="sxs-lookup"><span data-stu-id="400bb-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="400bb-111">Che cosa dobbiamo toosolve?</span><span class="sxs-lookup"><span data-stu-id="400bb-111">What do we need toosolve?</span></span>
<span data-ttu-id="400bb-112">Esaminiamo i dettagli di hello della misura InternetTotalSales, prima di aggiungere un'espressione di righe di dettaglio.</span><span class="sxs-lookup"><span data-stu-id="400bb-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="400bb-113">In SSDT, fare clic su hello **modello** menu > **analizza in Excel** tooopen Excel e creare una tabella pivot vuota.</span><span class="sxs-lookup"><span data-stu-id="400bb-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="400bb-114">In **PivotTable Fields**, aggiungere hello **InternetTotalSales** misure da tabella FactInternetSales hello troppo**valori**, **CalendarYear**dalla hello DimDate tabella troppo**colonne**, e **EnglishCountryRegionName** troppo**righe**.</span><span class="sxs-lookup"><span data-stu-id="400bb-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="400bb-115">La tabella pivot subito produce risultati aggregati da misure InternetTotalSales hello per le aree e anno.</span><span class="sxs-lookup"><span data-stu-id="400bb-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="400bb-117">Nella tabella pivot hello, fare doppio clic su un valore aggregato per un anno e un nome di area.</span><span class="sxs-lookup"><span data-stu-id="400bb-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="400bb-118">Di seguito si fa doppio clic sul valore hello per l'Australia e hello anno 2014.</span><span class="sxs-lookup"><span data-stu-id="400bb-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="400bb-119">Viene aperto un nuovo foglio contenente alcuni dati, ma non molto utili.</span><span class="sxs-lookup"><span data-stu-id="400bb-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="400bb-121">Ciò che si desidera toosee qui è una tabella contenente colonne e righe di dati che contribuiscono toohello aggregati i risultati di una misura InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="400bb-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="400bb-122">toodo, che è possibile aggiungere un'espressione di righe di dettaglio come proprietà della misura hello.</span><span class="sxs-lookup"><span data-stu-id="400bb-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="400bb-123">Aggiungere un'espressione di righe di dettaglio</span><span class="sxs-lookup"><span data-stu-id="400bb-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="400bb-124">toocreate un'espressione di righe di dettaglio</span><span class="sxs-lookup"><span data-stu-id="400bb-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="400bb-125">In SSDT, nella griglia delle misure della tabella FactInternetSales hello, fare clic su hello **InternetTotalSales** misura.</span><span class="sxs-lookup"><span data-stu-id="400bb-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="400bb-126">In **proprietà** > **espressione righe di dettaglio**, fare clic su prova editor pulsante tooopen prova Editor DAX.</span><span class="sxs-lookup"><span data-stu-id="400bb-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="400bb-128">Nell'Editor DAX immettere hello espressione seguente:</span><span class="sxs-lookup"><span data-stu-id="400bb-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="400bb-129">Questa espressione consente di specificare i nomi, le colonne e misure da tabella FactInternetSales hello e le tabelle correlate vengono restituiti quando un utente fa doppio clic su un risultato aggregato in una tabella pivot o un report.</span><span class="sxs-lookup"><span data-stu-id="400bb-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="400bb-130">In Excel, Elimina foglio hello creato nel passaggio 3, quindi fare doppio clic su un valore aggregato.</span><span class="sxs-lookup"><span data-stu-id="400bb-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="400bb-131">Questa volta, con una proprietà di espressione di righe di dettaglio definita per la misura hello, un nuovo foglio apre che contiene dati molto più utili.</span><span class="sxs-lookup"><span data-stu-id="400bb-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="400bb-133">Ridistribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="400bb-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="400bb-134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="400bb-134">See Also</span></span>  
<span data-ttu-id="400bb-135">[SELECTCOLUMNS Function (DAX) (Funzione DAX SELECTCOLUMNS)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="400bb-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="400bb-136">Lezione supplementare: Sicurezza dinamica</span><span class="sxs-lookup"><span data-stu-id="400bb-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="400bb-137">Lezione supplementare: Gerarchie incomplete</span><span class="sxs-lookup"><span data-stu-id="400bb-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
