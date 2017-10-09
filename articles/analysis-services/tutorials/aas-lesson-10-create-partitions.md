---
<span data-ttu-id="1a7de-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 10: creare partizioni | Descrizione di "Microsoft Docs: viene descritto come toocreate partizioni nel progetto di esercitazione di hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="1a7de-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="1a7de-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="1a7de-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="1a7de-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend</span><span class="sxs-lookup"><span data-stu-id="1a7de-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="1a7de-104">Lezione 10: Creare partizioni</span><span class="sxs-lookup"><span data-stu-id="1a7de-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="1a7de-105">In questa lezione è creare partizioni toodivide hello FactInternetSales tabella in parti logiche più piccole che possono essere elaborate (aggiornate) indipendentemente dalle altre partizioni.</span><span class="sxs-lookup"><span data-stu-id="1a7de-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="1a7de-106">Per impostazione predefinita, ogni tabella che inclusa nel modello dispone di una partizione, che include colonne e righe della tabella di hello tutti.</span><span class="sxs-lookup"><span data-stu-id="1a7de-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="1a7de-107">Per la tabella FactInternetSales hello vogliamo dati hello toodivide per anno; una partizione per ognuno dei cinque anni della tabella hello.</span><span class="sxs-lookup"><span data-stu-id="1a7de-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="1a7de-108">Ogni partizione può quindi essere elaborata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="1a7de-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="1a7de-109">vedere, più toolearn [partizioni](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="1a7de-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="1a7de-110">Stimato toocomplete ora questa lezione: **15 minuti**</span><span class="sxs-lookup"><span data-stu-id="1a7de-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="1a7de-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1a7de-111">Prerequisites</span></span>  
<span data-ttu-id="1a7de-112">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="1a7de-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="1a7de-113">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 9: creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="1a7de-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="1a7de-114">Creare partizioni</span><span class="sxs-lookup"><span data-stu-id="1a7de-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="1a7de-115">toocreate partizioni nella tabella FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="1a7de-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="1a7de-116">In Esplora modelli tabulari espandere **Tabelle** e quindi fare clic con il pulsante destro del mouse su **FactInternetSales** > **Partizioni**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="1a7de-117">In Gestione partizioni, fare clic su **copia**e quindi modificare il nome di hello troppo**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="1a7de-118">Poiché si desidera hello partizione tooinclude solo le righe all'interno di un determinato periodo, per l'anno hello 2010, è necessario modificare l'espressione di query hello.</span><span class="sxs-lookup"><span data-stu-id="1a7de-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="1a7de-119">Fare clic su **progettazione** tooopen Editor di Query e quindi fare clic su hello **FactInternetSales2010** query.</span><span class="sxs-lookup"><span data-stu-id="1a7de-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="1a7de-120">Nell'anteprima, fare clic su hello freccia giù in hello **OrderDate** intestazione di colonna e quindi fare clic su **filtri data/ora** > **tra**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="1a7de-122">Nella finestra di dialogo Filtra righe hello, in **Mostra righe in cui: OrderDate**, lasciare **è dopo o uguale a**, quindi immettere nel campo Data hello **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="1a7de-123">Lasciare hello **e** operatore selezionato, quindi selezionare **prima**, quindi immettere nel campo Data hello **1/1/2011**e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="1a7de-125">Si noti che nell'Editor di query, in Passaggi applicati, è visualizzato un altro passaggio denominato Filtrate righe.</span><span class="sxs-lookup"><span data-stu-id="1a7de-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="1a7de-126">Questo filtro è tooselect solo date di ordini da 2010.</span><span class="sxs-lookup"><span data-stu-id="1a7de-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="1a7de-127">Fare clic su **Importa**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-127">Click **Import**.</span></span>

    <span data-ttu-id="1a7de-128">In Gestione partizioni, si noti query hello ora l'espressione contiene una clausola di filtrare le righe aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="1a7de-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="1a7de-130">Questa istruzione consente di specificare che la partizione deve includere solo i dati di hello in tali righe in cui è hello OrderDate in hello anno di calendario 2010 come specificato nella clausola di hello righe filtrate.</span><span class="sxs-lookup"><span data-stu-id="1a7de-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="1a7de-131">una partizione per l'anno 2011 hello toocreate</span><span class="sxs-lookup"><span data-stu-id="1a7de-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="1a7de-132">Nell'elenco di partizioni hello, fare clic su hello **FactInternetSales2010** partizione creata e quindi fare clic su **copia**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="1a7de-133">Modificare il nome di partizione hello troppo**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="1a7de-134">Non è necessario toouse Editor di Query toocreate una nuova clausola di righe filtrate.</span><span class="sxs-lookup"><span data-stu-id="1a7de-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="1a7de-135">Poiché una copia della query hello è stato creato per 2010, è sufficiente toodo effettuano una lieve modifica in query di hello per 2011.</span><span class="sxs-lookup"><span data-stu-id="1a7de-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="1a7de-136">In **espressione di Query**, affinché questo tooinclude partizione solo le righe per hello anno 2011, sostituire gli anni di hello nella clausola righe filtrate hello con **2011** e **2012**, rispettivamente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1a7de-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="1a7de-137">partizioni toocreate per 2012, 2013 e 2014.</span><span class="sxs-lookup"><span data-stu-id="1a7de-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="1a7de-138">Seguire i passaggi precedenti hello, creazione di partizioni per 2012, 2013 e 2014, la modifica di anni hello in hello righe filtrate clausola tooinclude solo le righe per tale anno.</span><span class="sxs-lookup"><span data-stu-id="1a7de-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="1a7de-139">Eliminare hello FactInternetSales partizione</span><span class="sxs-lookup"><span data-stu-id="1a7de-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="1a7de-140">Dopo aver creato le partizioni per ogni anno, è possibile eliminare partizione FactInternetSales hello; Quando si sceglie elabora tutte durante l'elaborazione di partizioni, impedendo si sovrappongono.</span><span class="sxs-lookup"><span data-stu-id="1a7de-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="1a7de-141">hello toodelete FactInternetSales partizione</span><span class="sxs-lookup"><span data-stu-id="1a7de-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="1a7de-142">Fare clic sulla partizione FactInternetSales hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="1a7de-143">Elaborare le partizioni</span><span class="sxs-lookup"><span data-stu-id="1a7de-143">Process partitions</span></span>  
<span data-ttu-id="1a7de-144">In Gestione partizioni notare hello **elaborati ultimo** per ognuna delle nuove partizioni hello creato mostra queste partizioni non sono mai state elaborate.</span><span class="sxs-lookup"><span data-stu-id="1a7de-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="1a7de-145">Quando si creano partizioni, è consigliabile eseguire un elabora partizioni o una tabella del processo operazione toorefresh hello dati nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="1a7de-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="1a7de-146">tooprocess hello FactInternetSales partizioni</span><span class="sxs-lookup"><span data-stu-id="1a7de-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="1a7de-147">Fare clic su **OK** tooclose gestione partizioni.</span><span class="sxs-lookup"><span data-stu-id="1a7de-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="1a7de-148">Fare clic su hello **FactInternetSales** tabella, quindi fare clic su hello **modello** menu > **processo** > **elabora partizioni**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="1a7de-149">Nella finestra di dialogo Elabora partizioni hello verificare **modalità** è troppo**elaborazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="1a7de-150">Selezionare la casella di controllo di hello in hello **processo** per ognuna delle cinque hello partizioni creato e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a7de-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="1a7de-152">Se viene chiesto di immettere le credenziali di rappresentazione, immettere nome utente di Windows hello e la password specificati nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="1a7de-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="1a7de-153">Hello **l'elaborazione dati** verrà visualizzata la finestra di dialogo con informazioni dettagliate sul processo per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="1a7de-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="1a7de-154">Si noti che viene trasferito un numero diverso di righe per ogni partizione,</span><span class="sxs-lookup"><span data-stu-id="1a7de-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="1a7de-155">Ogni partizione include solo le righe per anno hello specificato nella clausola WHERE nell'istruzione SQL hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a7de-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="1a7de-156">Al termine dell'elaborazione, vado avanti e chiudere la finestra di dialogo di elaborazione dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="1a7de-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="1a7de-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a7de-158">What's next?</span></span>
<span data-ttu-id="1a7de-159">Lezione successiva passare toohello: [lezione 11: creare ruoli](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1a7de-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
