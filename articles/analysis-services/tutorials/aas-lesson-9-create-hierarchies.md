---
<span data-ttu-id="65cfb-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 9: creare gerarchie | Descrizione di Microsoft Docs": servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="65cfb-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="65cfb-102">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend</span><span class="sxs-lookup"><span data-stu-id="65cfb-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="65cfb-103">Lezione 9: Creare gerarchie</span><span class="sxs-lookup"><span data-stu-id="65cfb-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="65cfb-104">In questa lezione verranno create gerarchie.</span><span class="sxs-lookup"><span data-stu-id="65cfb-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="65cfb-105">Le gerarchie sono gruppi di colonne disposti in livelli. Ad esempio, una gerarchia Geografia può includere i sottolivelli Paese, Stato, Regione e Città.</span><span class="sxs-lookup"><span data-stu-id="65cfb-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="65cfb-106">Le gerarchie possono verificarsi separatamente dalle altre colonne in un elenco di campi dell'applicazione client reporting, agevolando client toonavigate gli utenti e includere in un report.</span><span class="sxs-lookup"><span data-stu-id="65cfb-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="65cfb-107">vedere, più toolearn [gerarchie](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="65cfb-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="65cfb-108">gerarchie toocreate, utilizzare Progettazione modelli di hello in *vista diagramma*.</span><span class="sxs-lookup"><span data-stu-id="65cfb-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="65cfb-109">La creazione e la gestione delle gerarchie non è supportata in vista dati.</span><span class="sxs-lookup"><span data-stu-id="65cfb-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="65cfb-110">Stimato toocomplete ora questa lezione: **20 minuti**</span><span class="sxs-lookup"><span data-stu-id="65cfb-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="65cfb-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="65cfb-111">Prerequisites</span></span>  
<span data-ttu-id="65cfb-112">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="65cfb-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="65cfb-113">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 8: creare prospettive](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="65cfb-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="65cfb-114">Creare gerarchie</span><span class="sxs-lookup"><span data-stu-id="65cfb-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="65cfb-115">una gerarchia Category nella tabella DimProduct hello toocreate</span><span class="sxs-lookup"><span data-stu-id="65cfb-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="65cfb-116">In Progettazione modelli hello (vista diagramma) fare doppio clic su hello **DimProduct** tabella > **crea gerarchia**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="65cfb-117">Nella parte inferiore della finestra di tabella hello hello disponibile per una nuova gerarchia.</span><span class="sxs-lookup"><span data-stu-id="65cfb-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="65cfb-118">Rinominare la gerarchia hello **categoria**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="65cfb-119">Fare clic e trascinare hello **ProductCategoryName** toohello colonna nuova **categoria** gerarchia.</span><span class="sxs-lookup"><span data-stu-id="65cfb-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="65cfb-120">In hello **categoria** gerarchia, hello rapida **ProductCategoryName** > **rinominare**, quindi digitare **categoria**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="65cfb-121">Ridenominazione di una colonna in una gerarchia non comporta la ridenominazione di tale colonna nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="65cfb-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="65cfb-122">Una colonna in una gerarchia è semplicemente una rappresentazione della colonna hello nella tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="65cfb-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="65cfb-123">Fare clic e trascinare hello **ProductSubcategoryName** colonna toohello **categoria** gerarchia.</span><span class="sxs-lookup"><span data-stu-id="65cfb-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="65cfb-124">Rinominarla **Subcategory**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="65cfb-125">Pulsante destro del mouse hello **ModelName** colonna > **aggiungere toohierarchy**, quindi selezionare **categoria**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="65cfb-126">Rinominarla **Model**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="65cfb-127">Infine, aggiungere **EnglishProductName** toohello gerarchia di categorie.</span><span class="sxs-lookup"><span data-stu-id="65cfb-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="65cfb-128">Rinominarla **Product**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="65cfb-130">gerarchie toocreate tabella DimDate hello</span><span class="sxs-lookup"><span data-stu-id="65cfb-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="65cfb-131">In hello **DimDate** tabella, creare una gerarchia denominata **calendario**.</span><span class="sxs-lookup"><span data-stu-id="65cfb-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="65cfb-132">Aggiungere hello colonne nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="65cfb-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="65cfb-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="65cfb-133">CalendarYear</span></span>
    *  <span data-ttu-id="65cfb-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="65cfb-134">CalendarSemester</span></span>
    *  <span data-ttu-id="65cfb-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="65cfb-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="65cfb-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="65cfb-136">MonthCalendar</span></span>
    *  <span data-ttu-id="65cfb-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="65cfb-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="65cfb-138">In hello **DimDate** tabella, creare un **fiscale** gerarchia.</span><span class="sxs-lookup"><span data-stu-id="65cfb-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="65cfb-139">Includere hello colonne nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="65cfb-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="65cfb-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="65cfb-140">FiscalYear</span></span>
    *  <span data-ttu-id="65cfb-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="65cfb-141">FiscalSemester</span></span>
    *  <span data-ttu-id="65cfb-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="65cfb-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="65cfb-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="65cfb-143">MonthCalendar</span></span>
    *  <span data-ttu-id="65cfb-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="65cfb-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="65cfb-145">Infine, in hello **DimDate** tabella, creare un **ProductionCalendar** gerarchia.</span><span class="sxs-lookup"><span data-stu-id="65cfb-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="65cfb-146">Includere hello colonne nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="65cfb-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="65cfb-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="65cfb-147">CalendarYear</span></span>
    *  <span data-ttu-id="65cfb-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="65cfb-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="65cfb-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="65cfb-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="65cfb-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65cfb-150">What's next?</span></span>
<span data-ttu-id="65cfb-151">[Lezione 10: Creare partizioni](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="65cfb-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
