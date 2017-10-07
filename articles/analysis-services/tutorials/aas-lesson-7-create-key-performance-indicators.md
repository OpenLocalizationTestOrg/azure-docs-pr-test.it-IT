---
<span data-ttu-id="880eb-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 7: creare indicatori di prestazioni chiave | Descrizione di "Microsoft Docs: viene descritto come indicatori di prestazioni chiave toocreate in hello progetto tutorial Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="880eb-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="880eb-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="880eb-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="880eb-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend</span><span class="sxs-lookup"><span data-stu-id="880eb-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="880eb-104">Lezione 7: Creare indicatori di prestazioni chiave</span><span class="sxs-lookup"><span data-stu-id="880eb-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="880eb-105">In questa lezione verranno creati alcuni indicatori di prestazioni chiave (KPI).</span><span class="sxs-lookup"><span data-stu-id="880eb-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="880eb-106">Gli indicatori KPI sono utilizzati toogauge prestazioni di un valore definito da un *Base* misura, contro un *destinazione* definito anch'esso da una misura o da un valore assoluto.</span><span class="sxs-lookup"><span data-stu-id="880eb-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="880eb-107">In applicazioni client di reporting, gli indicatori KPI possono fornire ai professionisti di business toounderstand un modo semplice e rapido un riepilogo delle tendenze di esito positivo o tooidentify business.</span><span class="sxs-lookup"><span data-stu-id="880eb-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="880eb-108">vedere, più toolearn [gli indicatori KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="880eb-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="880eb-109">Stimato toocomplete ora questa lezione: **15 minuti**</span><span class="sxs-lookup"><span data-stu-id="880eb-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="880eb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="880eb-110">Prerequisites</span></span>  
<span data-ttu-id="880eb-111">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="880eb-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="880eb-112">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 6: creare misure](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="880eb-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="880eb-113">Creare indicatori di prestazioni chiave</span><span class="sxs-lookup"><span data-stu-id="880eb-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="880eb-114">un KPI InternetCurrentQuarterSalesPerformance toocreate</span><span class="sxs-lookup"><span data-stu-id="880eb-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="880eb-115">In Progettazione modelli di hello, fare clic su hello **FactInternetSales** tabella.</span><span class="sxs-lookup"><span data-stu-id="880eb-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="880eb-116">Nella griglia delle misure hello, fare clic su una cella vuota.</span><span class="sxs-lookup"><span data-stu-id="880eb-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="880eb-117">Nella barra della formula hello, sopra la tabella hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="880eb-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="880eb-118">Questa misura viene utilizzata come misura di Base hello per hello indicatore KPI.</span><span class="sxs-lookup"><span data-stu-id="880eb-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="880eb-119">Fare clic con il pulsante destro del mouse su **InternetCurrentQuarterSalesPerformance** > **Crea KPI**.</span><span class="sxs-lookup"><span data-stu-id="880eb-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="880eb-120">Nella finestra di dialogo indicatore di prestazioni chiave (KPI) hello in **destinazione** selezionare **valore assoluto**, quindi digitare **1.1**.</span><span class="sxs-lookup"><span data-stu-id="880eb-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="880eb-121">Nel campo hello dispositivo di scorrimento sinistro (in basso) digitare **1**, quindi nel dispositivo di scorrimento destro (in alto) hello digitare **1.07**.</span><span class="sxs-lookup"><span data-stu-id="880eb-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="880eb-122">In **Seleziona stile icona**, selezionare triangolo a rombo (rosso), hello (giallo) o cerchio tipo di icona (verde).</span><span class="sxs-lookup"><span data-stu-id="880eb-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="880eb-124">Hello avviso espandibile **descrizioni** etichetta di sotto di stili di icona disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="880eb-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="880eb-125">Utilizzare le descrizioni per hello vari KPI elementi toomake li facilitare l'identificazione nelle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="880eb-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="880eb-126">Fare clic su **OK** toocomplete hello indicatore KPI.</span><span class="sxs-lookup"><span data-stu-id="880eb-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="880eb-127">Nella griglia delle misure hello, si noti hello icona Avanti toohello **InternetCurrentQuarterSalesPerformance** misura.</span><span class="sxs-lookup"><span data-stu-id="880eb-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="880eb-128">Questa icona indica che la misura funge da valore di base per un indicatore KPI.</span><span class="sxs-lookup"><span data-stu-id="880eb-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="880eb-129">un KPI InternetCurrentQuarterMarginPerformance toocreate</span><span class="sxs-lookup"><span data-stu-id="880eb-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="880eb-130">Nella griglia delle misure hello hello **FactInternetSales** tabella, fare clic su una cella vuota.</span><span class="sxs-lookup"><span data-stu-id="880eb-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="880eb-131">Nella barra della formula hello, sopra la tabella hello, digitare hello formula seguente:</span><span class="sxs-lookup"><span data-stu-id="880eb-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="880eb-132">Fare clic con il pulsante destro del mouse su **InternetCurrentQuarterMarginPerformance** > **Crea KPI**.</span><span class="sxs-lookup"><span data-stu-id="880eb-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="880eb-133">Nella finestra di dialogo indicatore di prestazioni chiave (KPI) hello in **destinazione** selezionare **valore assoluto**, quindi digitare **1.25**.</span><span class="sxs-lookup"><span data-stu-id="880eb-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="880eb-134">Nel campo del dispositivo di scorrimento sinistro (in basso) hello, scorrere fino a quando non viene visualizzato il campo hello **0,8**, e quindi hello diapositiva destro campo dispositivo di scorrimento (alto), fino a quando non viene visualizzato il campo hello **1.03**.</span><span class="sxs-lookup"><span data-stu-id="880eb-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="880eb-135">In **Seleziona stile icona**selezionare hello a forma di rombo (rosso), triangolo (giallo), il tipo di icona cerchio (verde) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="880eb-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="880eb-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="880eb-136">What's next?</span></span>
<span data-ttu-id="880eb-137">[Lezione 8: Creare prospettive](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="880eb-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
