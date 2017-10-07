---
<span data-ttu-id="a08a7-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 2: ottenere i dati | Descrizione di "Microsoft Docs: viene descritto come tooget e Importa dati in hello progetto tutorial Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="a08a7-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="a08a7-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="a08a7-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="a08a7-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend</span><span class="sxs-lookup"><span data-stu-id="a08a7-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="a08a7-104">Lezione 2: Ottenere i dati</span><span class="sxs-lookup"><span data-stu-id="a08a7-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="a08a7-105">In questa lezione, Usa Recupera dati in database di esempio tooconnect toohello AdventureWorksDW2014 SSDT, i dati selezionati, anteprima e filtro e quindi importare nell'area di lavoro modello.</span><span class="sxs-lookup"><span data-stu-id="a08a7-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="a08a7-106">Con Recupera dati è possibile importare dati da un'ampia gamma di origini: database SQL di Azure, Oracle, Sybase, feed OData, Teradata, file e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="a08a7-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="a08a7-107">I dati possono essere recuperati anche tramite query, usando un'espressione di formula Power Query M.</span><span class="sxs-lookup"><span data-stu-id="a08a7-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="a08a7-108">Stimato toocomplete ora questa lezione: **10 minuti**</span><span class="sxs-lookup"><span data-stu-id="a08a7-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a08a7-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a08a7-109">Prerequisites</span></span>  
<span data-ttu-id="a08a7-110">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="a08a7-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="a08a7-111">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 1: creare un nuovo progetto di modello tabulare](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="a08a7-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="a08a7-112">Creare una connessione</span><span class="sxs-lookup"><span data-stu-id="a08a7-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="a08a7-113">un database toohello AdventureWorksDW2014 connessione toocreate</span><span class="sxs-lookup"><span data-stu-id="a08a7-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="a08a7-114">In Esplora modelli tabulari fare doppio clic su **Origini dati** > **Importa da origine dati**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="a08a7-115">Verrà avviata recupera dati, che ti assisterà connessione origine dati di tooa.</span><span class="sxs-lookup"><span data-stu-id="a08a7-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="a08a7-116">Se non viene visualizzato Esplora modelli tabulari, **Esplora**, fare doppio clic su **Model.bim** modello hello tooopen nella finestra di progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="a08a7-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="a08a7-118">In Recupera dati fare clic su **Database** > **Database di SQL Server** > **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="a08a7-119">In hello **Database di SQL Server** finestra di dialogo, nella **Server**, digitare il nome di hello del server di hello in cui è installato il database di hello AdventureWorksDW2014 e quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="a08a7-120">Quando richiesto tooenter credenziali, è necessario che le credenziali di hello toospecify Analysis Services utilizza l'origine dei dati toohello tooconnect durante l'importazione e l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="a08a7-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="a08a7-121">In **Modalità di rappresentazione** selezionare **Rappresenta account**, immettere le credenziali e quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="a08a7-122">È consigliabile che utilizzare un account in cui è senza scadenza password hello.</span><span class="sxs-lookup"><span data-stu-id="a08a7-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="a08a7-124">Utilizzando un account utente di Windows e una password fornisce un metodo più sicuro hello di connessione origine dati di tooa.</span><span class="sxs-lookup"><span data-stu-id="a08a7-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="a08a7-125">Nel Pannello di navigazione, selezionare hello **AdventureWorksDW2014** database e quindi fare clic su **OK**. Crea database toohello di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="a08a7-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="a08a7-126">Nel Pannello di navigazione, selezionare hello casella di controllo per le tabelle seguenti hello: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="a08a7-128">Dopo aver fatto clic su OK verrà aperto l'Editor di query.</span><span class="sxs-lookup"><span data-stu-id="a08a7-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="a08a7-129">Nella sezione successiva hello, si seleziona solo i dati di hello desiderati tooimport.</span><span class="sxs-lookup"><span data-stu-id="a08a7-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="a08a7-130">Filtrare i dati della tabella hello</span><span class="sxs-lookup"><span data-stu-id="a08a7-130">Filter hello table data</span></span>  
<span data-ttu-id="a08a7-131">Le tabelle nel database di esempio hello AdventureWorksDW2014 contengono dati non sono necessario tooinclude nel modello.</span><span class="sxs-lookup"><span data-stu-id="a08a7-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="a08a7-132">Quando possibile, è opportuno toofilter out spazio in memoria di dati non necessari toosave utilizzato dal modello hello.</span><span class="sxs-lookup"><span data-stu-id="a08a7-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="a08a7-133">Filtrare determinati hello le colonne di tabelle in modo non si importati nel database dell'area di lavoro hello o database modello hello dopo che è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="a08a7-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="a08a7-134">dati della tabella hello toofilter prima dell'importazione</span><span class="sxs-lookup"><span data-stu-id="a08a7-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="a08a7-135">Nell'Editor di Query selezionare hello **DimCustomer** tabella.</span><span class="sxs-lookup"><span data-stu-id="a08a7-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="a08a7-136">Verrà visualizzata una vista della tabella DimCustomer hello in datasource hello (il database di esempio AdventureWorksDWQ2014).</span><span class="sxs-lookup"><span data-stu-id="a08a7-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="a08a7-137">Effettuare una selezione multipla con CTRL+clic di **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, fare clic con il pulsante destro del mouse e quindi scegliere **Rimuovi colonne**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="a08a7-139">Poiché i valori hello per le colonne selezionate non sono rilevanti tooInternet analisi delle vendite, non è alcuna necessità tooimport queste colonne.</span><span class="sxs-lookup"><span data-stu-id="a08a7-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="a08a7-140">L'eliminazione delle colonne superflue consente di ridurre le dimensioni del modello e di aumentarne l'efficienza.</span><span class="sxs-lookup"><span data-stu-id="a08a7-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="a08a7-141">Filtrare hello rimanenti tabelle rimuovendo hello colonne in ogni tabella di seguito:</span><span class="sxs-lookup"><span data-stu-id="a08a7-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="a08a7-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="a08a7-142">**DimDate**</span></span>
    
      |<span data-ttu-id="a08a7-143">Colonna</span><span class="sxs-lookup"><span data-stu-id="a08a7-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="a08a7-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="a08a7-144">DateKey</span></span>|  
      |<span data-ttu-id="a08a7-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a08a7-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="a08a7-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a08a7-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="a08a7-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="a08a7-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="a08a7-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="a08a7-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="a08a7-150">Colonna</span><span class="sxs-lookup"><span data-stu-id="a08a7-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="a08a7-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="a08a7-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="a08a7-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="a08a7-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="a08a7-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="a08a7-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="a08a7-155">Colonna</span><span class="sxs-lookup"><span data-stu-id="a08a7-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="a08a7-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="a08a7-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="a08a7-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="a08a7-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="a08a7-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="a08a7-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="a08a7-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="a08a7-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="a08a7-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="a08a7-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="a08a7-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="a08a7-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="a08a7-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="a08a7-167">Colonna</span><span class="sxs-lookup"><span data-stu-id="a08a7-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="a08a7-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="a08a7-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="a08a7-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="a08a7-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="a08a7-171">Colonna</span><span class="sxs-lookup"><span data-stu-id="a08a7-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="a08a7-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="a08a7-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="a08a7-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="a08a7-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="a08a7-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="a08a7-175">Colonna</span><span class="sxs-lookup"><span data-stu-id="a08a7-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="a08a7-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="a08a7-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="a08a7-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="a08a7-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="a08a7-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="a08a7-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="a08a7-179"><a name="Import"></a>Importare i dati delle colonne e tabelle hello selezionato</span><span class="sxs-lookup"><span data-stu-id="a08a7-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="a08a7-180">Ora che è stato visualizzato in anteprima e filtrati i dati non necessari, è possibile importare rest hello hello di dati.</span><span class="sxs-lookup"><span data-stu-id="a08a7-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="a08a7-181">Hello importazione dei dati di tabella hello insieme a tutte le relazioni tra tabelle.</span><span class="sxs-lookup"><span data-stu-id="a08a7-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="a08a7-182">Vengono create nuove tabelle e colonne nel modello hello e non è possibile importare i dati esclusi tramite filtro.</span><span class="sxs-lookup"><span data-stu-id="a08a7-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="a08a7-183">hello tooimport selezionate tabelle e i dati della colonna</span><span class="sxs-lookup"><span data-stu-id="a08a7-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="a08a7-184">Controllare le selezioni.</span><span class="sxs-lookup"><span data-stu-id="a08a7-184">Review your selections.</span></span> <span data-ttu-id="a08a7-185">Se è tutto corretto, fare clic su **Importa**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="a08a7-186">finestra di dialogo l'elaborazione dati Hello Mostra stato hello di dati da importare dall'origine dati nel database dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a08a7-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="a08a7-188">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="a08a7-189">Salvare il progetto del modello</span><span class="sxs-lookup"><span data-stu-id="a08a7-189">Save your model project</span></span>  
<span data-ttu-id="a08a7-190">È importante toofrequently salvare il progetto di modello.</span><span class="sxs-lookup"><span data-stu-id="a08a7-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="a08a7-191">progetto di modello hello toosave</span><span class="sxs-lookup"><span data-stu-id="a08a7-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="a08a7-192">Fare clic su **File** > **Salva tutti**.</span><span class="sxs-lookup"><span data-stu-id="a08a7-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="a08a7-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a08a7-193">What's next?</span></span>
<span data-ttu-id="a08a7-194">[Lezione 3: Contrassegnare come tabella data](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="a08a7-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
