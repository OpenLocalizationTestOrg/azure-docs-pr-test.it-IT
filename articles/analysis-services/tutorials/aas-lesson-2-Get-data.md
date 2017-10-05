---
title: 'Esercitazione su Azure Analysis Services - Lezione 2: Ottenere i dati | Microsoft Docs'
description: Descrive come ottenere e importare i dati nel progetto per l'esercitazione su Azure Analysis Services.
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
ms.openlocfilehash: e77de4b9a74b528fa8a7ce86424fc14628b2cacc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-2-get-data"></a><span data-ttu-id="94085-103">Lezione 2: Ottenere i dati</span><span class="sxs-lookup"><span data-stu-id="94085-103">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="94085-104">In questa lezione si usa la funzionalità Recupera dati in SSDT per connettersi al database di esempio AdventureWorksDW2014, selezionare i dati, visualizzarli in anteprima e filtrarli, quindi importarli nell'area di lavoro del modello.</span><span class="sxs-lookup"><span data-stu-id="94085-104">In this lesson, you use Get Data in SSDT to connect to the AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="94085-105">Con Recupera dati è possibile importare dati da un'ampia gamma di origini: database SQL di Azure, Oracle, Sybase, feed OData, Teradata, file e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="94085-105">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="94085-106">I dati possono essere recuperati anche tramite query, usando un'espressione di formula Power Query M.</span><span class="sxs-lookup"><span data-stu-id="94085-106">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="94085-107">Tempo previsto per il completamento della lezione: **10 minuti**</span><span class="sxs-lookup"><span data-stu-id="94085-107">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="94085-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94085-108">Prerequisites</span></span>  
<span data-ttu-id="94085-109">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="94085-109">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="94085-110">Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 1: Creare un nuovo progetto di modello tabulare](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="94085-110">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="94085-111">Creare una connessione</span><span class="sxs-lookup"><span data-stu-id="94085-111">Create a connection</span></span>  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw2014-database"></a><span data-ttu-id="94085-112">Per creare una connessione al database AdventureWorksDW2014</span><span class="sxs-lookup"><span data-stu-id="94085-112">To create a connection to the AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="94085-113">In Esplora modelli tabulari fare doppio clic su **Origini dati** > **Importa da origine dati**.</span><span class="sxs-lookup"><span data-stu-id="94085-113">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="94085-114">Verrà avviata la funzionalità Recupera dati che consente di eseguire in modo guidato i passaggi per la connessione a un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="94085-114">This launches Get Data, which guides you through connecting to a data source.</span></span> <span data-ttu-id="94085-115">Se Esplora modelli tabulari non è visibile, in **Esplora soluzioni** fare doppio clic su **Model.bim** per aprire il modello nella finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="94085-115">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** to open the model in the designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="94085-117">In Recupera dati fare clic su **Database** > **Database di SQL Server** > **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="94085-117">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="94085-118">Nella finestra di dialogo **Database di SQL Server**, in **Server**, digitare il nome del server in cui è stato installato il database AdventureWorksDW2014 e quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="94085-118">In the **SQL Server Database** dialog, in **Server**, type the name of the server where you installed the AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="94085-119">Quando viene richiesto di immettere le credenziali, è necessario specificare le credenziali usate da Analysis Services per connettersi all'origine dati durante l'importazione e l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="94085-119">When prompted to enter credentials, you need to specify the credentials Analysis Services uses to connect to the data source when importing and processing data.</span></span> <span data-ttu-id="94085-120">In **Modalità di rappresentazione** selezionare **Rappresenta account**, immettere le credenziali e quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="94085-120">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="94085-121">È consigliabile usare un account con password senza scadenza.</span><span class="sxs-lookup"><span data-stu-id="94085-121">It's recommended you use an account where the password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="94085-123">Il metodo più sicuro per la connessione a un'origine dati consiste nell'usare un account utente di Windows e relativa password.</span><span class="sxs-lookup"><span data-stu-id="94085-123">Using a Windows user account and password provides the most secure method of connecting to a data source.</span></span>
  
5.  <span data-ttu-id="94085-124">Nello strumento di navigazione selezionare il database **AdventureWorksDW2014** e quindi fare clic su **OK**. Verrà creata la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="94085-124">In Navigator, select the **AdventureWorksDW2014** database, and then click **OK**.This creates the connection to the database.</span></span> 
  
6.  <span data-ttu-id="94085-125">Nello strumento di navigazione selezionare la casella di controllo per le tabelle seguenti: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** e **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="94085-125">In Navigator, select the check box for the following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="94085-127">Dopo aver fatto clic su OK verrà aperto l'Editor di query.</span><span class="sxs-lookup"><span data-stu-id="94085-127">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="94085-128">Nella sezione successiva si selezioneranno solo i dati da importare.</span><span class="sxs-lookup"><span data-stu-id="94085-128">In the next section, you select only the data you want to import.</span></span>

  
## <a name="filter-the-table-data"></a><span data-ttu-id="94085-129">Filtrare i dati della tabella</span><span class="sxs-lookup"><span data-stu-id="94085-129">Filter the table data</span></span>  
<span data-ttu-id="94085-130">Le tabelle nel database di esempio AdventureWorksDW2014 includono dati che non è necessario includere nel modello.</span><span class="sxs-lookup"><span data-stu-id="94085-130">Tables in the AdventureWorksDW2014 sample database have data that isn't necessary to include in your model.</span></span> <span data-ttu-id="94085-131">Se possibile, è consigliabile filtrare i dati in modo da escludere quelli non necessari e ridurre così lo spazio in memoria occupato dal modello.</span><span class="sxs-lookup"><span data-stu-id="94085-131">When possible, you want to filter out unnecessary data to save in-memory space used by the model.</span></span> <span data-ttu-id="94085-132">Con il filtro è possibile escludere alcune colonne dalle tabelle, in modo che non vengano importate nel database dell'area di lavoro o nel database del modello dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="94085-132">You filter out some of the columns from tables so they're not imported into the workspace database, or the model database after it has been deployed.</span></span> 
  
#### <a name="to-filter-the-table-data-before-importing"></a><span data-ttu-id="94085-133">Per filtrare i dati della tabella prima dell'importazione</span><span class="sxs-lookup"><span data-stu-id="94085-133">To filter the table data before importing</span></span>  
  
1.  <span data-ttu-id="94085-134">Nell'Editor di query selezionare la tabella **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="94085-134">In Query Editor, select the **DimCustomer** table.</span></span> <span data-ttu-id="94085-135">Verrà aperta una vista della tabella DimCustomer nell'origine dati, ovvero il database di esempio AdventureWorksDWQ2014.</span><span class="sxs-lookup"><span data-stu-id="94085-135">A view of the DimCustomer table at the datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="94085-136">Effettuare una selezione multipla con CTRL+clic di **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, fare clic con il pulsante destro del mouse e quindi scegliere **Rimuovi colonne**.</span><span class="sxs-lookup"><span data-stu-id="94085-136">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="94085-138">Dato che i valori per queste colonne non sono attinenti all'analisi delle vendite Internet, non è necessario importare queste colonne.</span><span class="sxs-lookup"><span data-stu-id="94085-138">Since the values for these columns are not relevant to Internet sales analysis, there is no need to import these columns.</span></span> <span data-ttu-id="94085-139">L'eliminazione delle colonne superflue consente di ridurre le dimensioni del modello e di aumentarne l'efficienza.</span><span class="sxs-lookup"><span data-stu-id="94085-139">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="94085-140">Filtrare le tabelle restanti rimuovendo le colonne seguenti in ogni tabella:</span><span class="sxs-lookup"><span data-stu-id="94085-140">Filter the remaining tables by removing the following columns in each table:</span></span>  
    
    <span data-ttu-id="94085-141">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="94085-141">**DimDate**</span></span>
    
      |<span data-ttu-id="94085-142">Colonna</span><span class="sxs-lookup"><span data-stu-id="94085-142">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="94085-143">DateKey</span><span class="sxs-lookup"><span data-stu-id="94085-143">DateKey</span></span>|  
      |<span data-ttu-id="94085-144">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="94085-144">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="94085-145">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="94085-145">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="94085-146">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="94085-146">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="94085-147">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="94085-147">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="94085-148">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="94085-148">**DimGeography**</span></span>
  
      |<span data-ttu-id="94085-149">Colonna</span><span class="sxs-lookup"><span data-stu-id="94085-149">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="94085-150">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="94085-150">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="94085-151">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="94085-151">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="94085-152">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="94085-152">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="94085-153">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="94085-153">**DimProduct**</span></span>
  
      |<span data-ttu-id="94085-154">Colonna</span><span class="sxs-lookup"><span data-stu-id="94085-154">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="94085-155">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="94085-155">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="94085-156">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="94085-156">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="94085-157">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-157">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="94085-158">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-158">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="94085-159">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-159">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="94085-160">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-160">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="94085-161">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-161">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="94085-162">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-162">**GermanDescription**</span></span>|  
      |<span data-ttu-id="94085-163">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-163">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="94085-164">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="94085-164">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="94085-165">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="94085-165">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="94085-166">Colonna</span><span class="sxs-lookup"><span data-stu-id="94085-166">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="94085-167">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="94085-167">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="94085-168">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="94085-168">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="94085-169">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="94085-169">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="94085-170">Colonna</span><span class="sxs-lookup"><span data-stu-id="94085-170">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="94085-171">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="94085-171">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="94085-172">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="94085-172">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="94085-173">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="94085-173">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="94085-174">Colonna</span><span class="sxs-lookup"><span data-stu-id="94085-174">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="94085-175">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="94085-175">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="94085-176">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="94085-176">**DueDateKey**</span></span>|  
      |<span data-ttu-id="94085-177">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="94085-177">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="94085-178"><a name="Import"></a>Importare i dati delle tabelle e delle colonne selezionate</span><span class="sxs-lookup"><span data-stu-id="94085-178"><a name="Import"></a>Import the selected tables and column data</span></span>  
<span data-ttu-id="94085-179">Dopo aver visualizzato in anteprima i dati e avere escluso quelli non necessari, è possibile importare il resto dei dati necessari.</span><span class="sxs-lookup"><span data-stu-id="94085-179">Now that you've previewed and filtered out unnecessary data, you can import the rest of the data you do want.</span></span> <span data-ttu-id="94085-180">La procedura guidata importa i dati delle tabelle insieme alle eventuali relazioni tra le tabelle.</span><span class="sxs-lookup"><span data-stu-id="94085-180">The wizard imports the table data along with any relationships between tables.</span></span> <span data-ttu-id="94085-181">Nel modello vengono create nuove tabelle e colonne e i dati esclusi tramite filtro non vengono importati.</span><span class="sxs-lookup"><span data-stu-id="94085-181">New tables and columns are created in the model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a><span data-ttu-id="94085-182">Per importare i dati delle tabelle e delle colonne selezionate</span><span class="sxs-lookup"><span data-stu-id="94085-182">To import the selected tables and column data</span></span>  
  
1.  <span data-ttu-id="94085-183">Controllare le selezioni.</span><span class="sxs-lookup"><span data-stu-id="94085-183">Review your selections.</span></span> <span data-ttu-id="94085-184">Se è tutto corretto, fare clic su **Importa**.</span><span class="sxs-lookup"><span data-stu-id="94085-184">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="94085-185">Nella finestra di dialogo Elaborazione dati viene visualizzato lo stato dell'importazione dei dati dall'origine dati al database dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="94085-185">The Data Processing dialog shows the status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="94085-187">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="94085-187">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="94085-188">Salvare il progetto del modello</span><span class="sxs-lookup"><span data-stu-id="94085-188">Save your model project</span></span>  
<span data-ttu-id="94085-189">È importante salvare frequentemente il progetto del modello.</span><span class="sxs-lookup"><span data-stu-id="94085-189">It's important to frequently save your model project.</span></span>  
  
#### <a name="to-save-the-model-project"></a><span data-ttu-id="94085-190">Per salvare il progetto del modello</span><span class="sxs-lookup"><span data-stu-id="94085-190">To save the model project</span></span>  
  
-   <span data-ttu-id="94085-191">Fare clic su **File** > **Salva tutti**.</span><span class="sxs-lookup"><span data-stu-id="94085-191">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="94085-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94085-192">What's next?</span></span>
<span data-ttu-id="94085-193">[Lezione 3: Contrassegnare come tabella data](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="94085-193">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
