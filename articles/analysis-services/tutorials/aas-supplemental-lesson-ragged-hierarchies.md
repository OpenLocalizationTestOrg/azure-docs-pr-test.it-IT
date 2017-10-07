---
<span data-ttu-id="acdc2-101">titolo: aaa "lezione supplementare esercitazione Azure Analysis Services: gerarchie incomplete | Descrizione di "Microsoft Docs: viene descritto come toofix gerarchie incomplete nell'esercitazione di hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="acdc2-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="acdc2-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="acdc2-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="acdc2-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend</span><span class="sxs-lookup"><span data-stu-id="acdc2-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="acdc2-104">Lezione supplementare: gerarchie incomplete</span><span class="sxs-lookup"><span data-stu-id="acdc2-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="acdc2-105">Questa lezione supplementare spiega come risolvere un problema comune che si verifica quando si applica il calcolo pivot sulle gerarchie che contengono valori (membri) vuoti a livelli diversi.</span><span class="sxs-lookup"><span data-stu-id="acdc2-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="acdc2-106">Per fare un esempio, un'organizzazione in cui un responsabile di alto livello ha sia responsabili di reparto sia non responsabili come dipendenti diretti.</span><span class="sxs-lookup"><span data-stu-id="acdc2-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="acdc2-107">Un altro esempio è rappresentato dalle gerarchie geografiche composte da paese-regione-città, in cui alcune città non dispongono di uno stato o una provincia, ad esempio Washington D.C. e la Città del Vaticano.</span><span class="sxs-lookup"><span data-stu-id="acdc2-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="acdc2-108">Quando si dispone di una gerarchia di membri vuoti, è spesso discende toodifferent o incompleta, livelli.</span><span class="sxs-lookup"><span data-stu-id="acdc2-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="acdc2-110">I modelli tabulari a livello di compatibilità hello 1400 presentano un ulteriore **Nascondi membri** proprietà per le gerarchie.</span><span class="sxs-lookup"><span data-stu-id="acdc2-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="acdc2-111">Hello **predefinito** impostazione presuppone che non esistono membri vuoti a qualsiasi livello.</span><span class="sxs-lookup"><span data-stu-id="acdc2-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="acdc2-112">Hello **nascondere i membri vuoti** impostazione consente di escludere i membri vuoti dalla gerarchia di hello quando aggiunto tooa tabella pivot o un report.</span><span class="sxs-lookup"><span data-stu-id="acdc2-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="acdc2-113">Stimato toocomplete ora questa lezione: **20 minuti**</span><span class="sxs-lookup"><span data-stu-id="acdc2-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="acdc2-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="acdc2-114">Prerequisites</span></span>  
<span data-ttu-id="acdc2-115">L'argomento di questa lezione supplementare fa parte di un'esercitazione sulla creazione di modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="acdc2-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="acdc2-116">Prima di eseguire attività di hello in questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o dispone di un progetto di modello di esempio Adventure Works Internet Sales completato.</span><span class="sxs-lookup"><span data-stu-id="acdc2-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="acdc2-117">Se sono stati creati progetto AW Internet Sales hello come parte dell'esercitazione hello, il modello non contiene ancora dati o gerarchie incomplete.</span><span class="sxs-lookup"><span data-stu-id="acdc2-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="acdc2-118">toocomplete questa lezione supplementare, è necessario innanzitutto toocreate hello problema mediante l'aggiunta di alcune tabelle aggiuntive, creare relazioni, colonne calcolate, una misura e una nuova gerarchia organizzativa.</span><span class="sxs-lookup"><span data-stu-id="acdc2-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="acdc2-119">Questa operazione richiede circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="acdc2-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="acdc2-120">Quindi, si ottiene toosolve in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="acdc2-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="acdc2-121">Aggiungere tabelle e oggetti</span><span class="sxs-lookup"><span data-stu-id="acdc2-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="acdc2-122">nuovo modello di tooyour tabelle tooadd</span><span class="sxs-lookup"><span data-stu-id="acdc2-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="acdc2-123">In Esplora modelli tabulari espandere **Origini dati** e quindi fare clic con il pulsante destro del mouse sulla connessione > **Importa nuove tabelle**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="acdc2-124">Nello strumento di spostamento selezionare **DimEmployee** e **FactResellerSales** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="acdc2-125">Nell'Editor di query fare clic su **Importa**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="acdc2-126">Creare i seguenti hello [relazioni](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="acdc2-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="acdc2-127">Tabella 1</span><span class="sxs-lookup"><span data-stu-id="acdc2-127">Table 1</span></span>           | <span data-ttu-id="acdc2-128">Colonna</span><span class="sxs-lookup"><span data-stu-id="acdc2-128">Column</span></span>       | <span data-ttu-id="acdc2-129">Direzione del filtro</span><span class="sxs-lookup"><span data-stu-id="acdc2-129">Filter Direction</span></span>   | <span data-ttu-id="acdc2-130">Tabella 2</span><span class="sxs-lookup"><span data-stu-id="acdc2-130">Table 2</span></span>     | <span data-ttu-id="acdc2-131">Colonna</span><span class="sxs-lookup"><span data-stu-id="acdc2-131">Column</span></span>      | <span data-ttu-id="acdc2-132">Attivo</span><span class="sxs-lookup"><span data-stu-id="acdc2-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="acdc2-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="acdc2-133">FactResellerSales</span></span> | <span data-ttu-id="acdc2-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="acdc2-134">OrderDateKey</span></span> | <span data-ttu-id="acdc2-135">Default</span><span class="sxs-lookup"><span data-stu-id="acdc2-135">Default</span></span>            | <span data-ttu-id="acdc2-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="acdc2-136">DimDate</span></span>     | <span data-ttu-id="acdc2-137">Data</span><span class="sxs-lookup"><span data-stu-id="acdc2-137">Date</span></span>        | <span data-ttu-id="acdc2-138">Sì</span><span class="sxs-lookup"><span data-stu-id="acdc2-138">Yes</span></span>    |
    | <span data-ttu-id="acdc2-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="acdc2-139">FactResellerSales</span></span> | <span data-ttu-id="acdc2-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="acdc2-140">DueDate</span></span>      | <span data-ttu-id="acdc2-141">Default</span><span class="sxs-lookup"><span data-stu-id="acdc2-141">Default</span></span>            | <span data-ttu-id="acdc2-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="acdc2-142">DimDate</span></span>     | <span data-ttu-id="acdc2-143">Data</span><span class="sxs-lookup"><span data-stu-id="acdc2-143">Date</span></span>        | <span data-ttu-id="acdc2-144">No</span><span class="sxs-lookup"><span data-stu-id="acdc2-144">No</span></span>     |
    | <span data-ttu-id="acdc2-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="acdc2-145">FactResellerSales</span></span> | <span data-ttu-id="acdc2-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="acdc2-146">ShipDateKey</span></span>  | <span data-ttu-id="acdc2-147">Default</span><span class="sxs-lookup"><span data-stu-id="acdc2-147">Default</span></span>            | <span data-ttu-id="acdc2-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="acdc2-148">DimDate</span></span>     | <span data-ttu-id="acdc2-149">Data</span><span class="sxs-lookup"><span data-stu-id="acdc2-149">Date</span></span>        | <span data-ttu-id="acdc2-150">No</span><span class="sxs-lookup"><span data-stu-id="acdc2-150">No</span></span>     |
    | <span data-ttu-id="acdc2-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="acdc2-151">FactResellerSales</span></span> | <span data-ttu-id="acdc2-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="acdc2-152">ProductKey</span></span>   | <span data-ttu-id="acdc2-153">Default</span><span class="sxs-lookup"><span data-stu-id="acdc2-153">Default</span></span>            | <span data-ttu-id="acdc2-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="acdc2-154">DimProduct</span></span>  | <span data-ttu-id="acdc2-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="acdc2-155">ProductKey</span></span>  | <span data-ttu-id="acdc2-156">Sì</span><span class="sxs-lookup"><span data-stu-id="acdc2-156">Yes</span></span>    |
    | <span data-ttu-id="acdc2-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="acdc2-157">FactResellerSales</span></span> | <span data-ttu-id="acdc2-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="acdc2-158">EmployeeKey</span></span>  | <span data-ttu-id="acdc2-159">Tabelle tooBoth</span><span class="sxs-lookup"><span data-stu-id="acdc2-159">tooBoth Tables</span></span> | <span data-ttu-id="acdc2-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="acdc2-160">DimEmployee</span></span> | <span data-ttu-id="acdc2-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="acdc2-161">EmployeeKey</span></span> | <span data-ttu-id="acdc2-162">Sì</span><span class="sxs-lookup"><span data-stu-id="acdc2-162">Yes</span></span>    |

5. <span data-ttu-id="acdc2-163">In hello **DimEmployee** tabella, creare i seguenti hello [le colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="acdc2-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="acdc2-164">**Percorso**</span><span class="sxs-lookup"><span data-stu-id="acdc2-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="acdc2-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="acdc2-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="acdc2-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="acdc2-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="acdc2-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="acdc2-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="acdc2-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="acdc2-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="acdc2-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="acdc2-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="acdc2-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="acdc2-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="acdc2-171">In hello **DimEmployee** tabella, creare un [gerarchia](../tutorials/aas-lesson-9-create-hierarchies.md) denominato **organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="acdc2-172">Aggiungere hello colonne nell'ordine seguente: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="acdc2-173">In hello **FactResellerSales** tabella, creare i seguenti hello [misura](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="acdc2-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="acdc2-174">Utilizzare [analizza in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel e creare automaticamente una tabella pivot.</span><span class="sxs-lookup"><span data-stu-id="acdc2-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="acdc2-175">In **PivotTable Fields**, aggiungere hello **organizzazione** gerarchia da hello **DimEmployee** tabella troppo**righe**e hello **ResellerTotalSales** misura dalla hello **FactResellerSales** tabella troppo**valori**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="acdc2-177">Come si vede nella tabella pivot hello, hello gerarchia consente di visualizzare le righe che sono incomplete.</span><span class="sxs-lookup"><span data-stu-id="acdc2-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="acdc2-178">Sono presenti molte righe con membri vuoti.</span><span class="sxs-lookup"><span data-stu-id="acdc2-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="acdc2-179">gerarchia incompleta di hello toofix impostando la proprietà membri Nascondi hello</span><span class="sxs-lookup"><span data-stu-id="acdc2-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="acdc2-180">In **Esplora modelli tabulari** espandere **Tabelle** > **DimEmployee** > **Gerarchie** > **Organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="acdc2-181">In **Proprietà** > **Nascondi membri** selezionare **Nascondi membri vuoti**.</span><span class="sxs-lookup"><span data-stu-id="acdc2-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="acdc2-183">In Excel, aggiornare hello tabella pivot.</span><span class="sxs-lookup"><span data-stu-id="acdc2-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="acdc2-185">La tabella è ora completa.</span><span class="sxs-lookup"><span data-stu-id="acdc2-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="acdc2-186">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="acdc2-186">See Also</span></span>   
[<span data-ttu-id="acdc2-187">Lezione 9: Creare gerarchie</span><span class="sxs-lookup"><span data-stu-id="acdc2-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="acdc2-188">Lezione supplementare: Sicurezza dinamica</span><span class="sxs-lookup"><span data-stu-id="acdc2-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="acdc2-189">Lezione supplementare: Righe di dettaglio</span><span class="sxs-lookup"><span data-stu-id="acdc2-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  