---
title: Analizzare i dati con Azure Machine Learning | Documentazione di Microsoft
description: Usare Azure Machine Learning per creare un modello predittivo di apprendimento automatico basato sui dati archiviati in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3197948e32fe5c95b111fe5495a0e5f85966a24b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="d633d-103">Analizzare i dati con Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d633d-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d633d-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="d633d-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="d633d-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d633d-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="d633d-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d633d-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="d633d-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="d633d-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="d633d-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="d633d-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="d633d-109">Questa esercitazione usa Azure Machine Learning per creare un modello predittivo di apprendimento automatico basato sui dati archiviati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d633d-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d633d-110">Nello specifico, verrà compilata una campagna di marketing mirata di Adventure Works, il negozio di biciclette, per stimare la probabilità che un cliente acquisti una bicicletta o meno.</span><span class="sxs-lookup"><span data-stu-id="d633d-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d633d-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d633d-111">Prerequisites</span></span>
<span data-ttu-id="d633d-112">Per eseguire questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="d633d-112">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="d633d-113">Un'istanza di SQL Data Warehouse in cui sia precaricato il database di esempio AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d633d-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="d633d-114">Per effettuarne il provisioning, vedere [Creare un Azure SQL Data Warehouse][Create a SQL Data Warehouse] e scegliere di caricare i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="d633d-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="d633d-115">Se si ha già un data warehouse, ma non i dati di esempio, è possibile [caricare manualmente i dati di esempio][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="d633d-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-the-data"></a><span data-ttu-id="d633d-116">1. Ottenere i dati</span><span class="sxs-lookup"><span data-stu-id="d633d-116">1. Get the data</span></span>
<span data-ttu-id="d633d-117">I dati sono disponibili nella visualizzazione dbo.vTargetMail nel database AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d633d-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span></span> <span data-ttu-id="d633d-118">Per leggere i dati:</span><span class="sxs-lookup"><span data-stu-id="d633d-118">To read this data:</span></span>

1. <span data-ttu-id="d633d-119">Accedere ad [Azure Machine Learning Studio][Azure Machine Learning studio] e fare clic sugli esperimenti personali.</span><span class="sxs-lookup"><span data-stu-id="d633d-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="d633d-120">Fare clic su **+NEW** e selezionare **Esperimento vuoto**.</span><span class="sxs-lookup"><span data-stu-id="d633d-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="d633d-121">Immettere un nome per l'esperimento: Marketing mirato.</span><span class="sxs-lookup"><span data-stu-id="d633d-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="d633d-122">Trascinare il modulo **Reader** dal riquadro dei moduli nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="d633d-122">Drag the **Reader** module from the modules pane into the canvas.</span></span>
5. <span data-ttu-id="d633d-123">Nel riquadro Properties specificare i dettagli del database SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d633d-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span></span>
6. <span data-ttu-id="d633d-124">Specificare la **query** di database per leggere i dati di interesse.</span><span class="sxs-lookup"><span data-stu-id="d633d-124">Specify the database **query** to read the data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="d633d-125">Eseguire l'esperimento facendo clic su **Esegui** sotto l'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="d633d-125">Run the experiment by clicking **Run** under the experiment canvas.</span></span>
<span data-ttu-id="d633d-126">![Eseguire l'esperimento][1]</span><span class="sxs-lookup"><span data-stu-id="d633d-126">![Run the experiment][1]</span></span>

<span data-ttu-id="d633d-127">Dopo aver concluso con successo l’esperimento, per visualizzare i dati importati fare clic sulla porta di output nella parte inferiore del modulo Reader e selezionare **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="d633d-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span></span>
<span data-ttu-id="d633d-128">![Visualizzare i dati importati][3]</span><span class="sxs-lookup"><span data-stu-id="d633d-128">![View imported data][3]</span></span>

## <a name="2-clean-the-data"></a><span data-ttu-id="d633d-129">2. Pulire i dati</span><span class="sxs-lookup"><span data-stu-id="d633d-129">2. Clean the data</span></span>
<span data-ttu-id="d633d-130">Per pulire i dati, eliminare alcune colonne non rilevanti per il modello.</span><span class="sxs-lookup"><span data-stu-id="d633d-130">To clean the data, drop some columns that are not relevant for the model.</span></span> <span data-ttu-id="d633d-131">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d633d-131">To do this:</span></span>

1. <span data-ttu-id="d633d-132">Trascinare il modulo **Project Columns** nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="d633d-132">Drag the **Project Columns** module into the canvas.</span></span>
2. <span data-ttu-id="d633d-133">Fare clic su **Launch column selector** nel riquadro Proprietà per specificare le colonne da eliminare.</span><span class="sxs-lookup"><span data-stu-id="d633d-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span></span>
   <span data-ttu-id="d633d-134">![Project Columns][4]</span><span class="sxs-lookup"><span data-stu-id="d633d-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="d633d-135">Escludere due colonne: CustomerAlternateKey e GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="d633d-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="d633d-136">![Rimuovere le colonne non necessarie][5]</span><span class="sxs-lookup"><span data-stu-id="d633d-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-the-model"></a><span data-ttu-id="d633d-137">3. Compilare il modello</span><span class="sxs-lookup"><span data-stu-id="d633d-137">3. Build the model</span></span>
<span data-ttu-id="d633d-138">Si suddivideranno i dati 80-20: 80% per il training di un modello di Machine Learning e 20% per testare il modello.</span><span class="sxs-lookup"><span data-stu-id="d633d-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span></span> <span data-ttu-id="d633d-139">Per questo problema di classificazione binaria si useranno gli algoritmi "Two-Class".</span><span class="sxs-lookup"><span data-stu-id="d633d-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="d633d-140">Trascinare il modulo **Split** nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="d633d-140">Drag the **Split** module into the canvas.</span></span>
2. <span data-ttu-id="d633d-141">Immettere 0,8 per Fraction of rows nel primo set di dati di output nel riquadro Properties.</span><span class="sxs-lookup"><span data-stu-id="d633d-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span></span>
   <span data-ttu-id="d633d-142">![Dividere i dati in set di traning e di test][6]</span><span class="sxs-lookup"><span data-stu-id="d633d-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="d633d-143">Trascinare il modulo **Two-Class Boosted Decision Tree** nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="d633d-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span></span>
4. <span data-ttu-id="d633d-144">Trascinare il modulo **Train Model** nell'area di disegno e specificare gli input.</span><span class="sxs-lookup"><span data-stu-id="d633d-144">Drag the **Train Model** module into the canvas and specify the inputs.</span></span> <span data-ttu-id="d633d-145">Fare clic su **Launch column selector** nel riquadro Properties.</span><span class="sxs-lookup"><span data-stu-id="d633d-145">Then, click **Launch column selector** in the Properties pane.</span></span>
   * <span data-ttu-id="d633d-146">Primo input: algoritmo ML.</span><span class="sxs-lookup"><span data-stu-id="d633d-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="d633d-147">Secondo input: dati su cui eseguire il training dell'algoritmo.</span><span class="sxs-lookup"><span data-stu-id="d633d-147">Second input: Data to train the algorithm on.</span></span>
     <span data-ttu-id="d633d-148">![Connettere il modulo Train Model][7]</span><span class="sxs-lookup"><span data-stu-id="d633d-148">![Connect the Train Model module][7]</span></span>
5. <span data-ttu-id="d633d-149">Selezionare la colonna **BikeBuyer** come colonna da stimare.</span><span class="sxs-lookup"><span data-stu-id="d633d-149">Select the **BikeBuyer** column as the column to predict.</span></span>
   <span data-ttu-id="d633d-150">![Selezionare una colonna da stimare][8]</span><span class="sxs-lookup"><span data-stu-id="d633d-150">![Select Column to predict][8]</span></span>

## <a name="4-score-the-model"></a><span data-ttu-id="d633d-151">4. Assegnare un punteggio al modello</span><span class="sxs-lookup"><span data-stu-id="d633d-151">4. Score the model</span></span>
<span data-ttu-id="d633d-152">A questo punto si verificheranno le prestazioni del modello sui dati di test.</span><span class="sxs-lookup"><span data-stu-id="d633d-152">Now, we will test how the model performs on test data.</span></span> <span data-ttu-id="d633d-153">L'algoritmo scelto verrà confrontato con un algoritmo diverso per verificare quale offre prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="d633d-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span></span>

1. <span data-ttu-id="d633d-154">Trascinare il modulo **Score Model** nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="d633d-154">Drag **Score Model** module into the canvas.</span></span>
    <span data-ttu-id="d633d-155">Primo input: Trained Model Secondo input: Test data ![Assegnare un punteggio al modello][9]</span><span class="sxs-lookup"><span data-stu-id="d633d-155">First input: Trained model Second input: Test data ![Score the model][9]</span></span>
2. <span data-ttu-id="d633d-156">Trascinare il **Two-Class Bayes Point Machine** nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="d633d-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span></span> <span data-ttu-id="d633d-157">Si confronteranno le prestazioni di questo algoritmo rispetto a Two-Class Boosted Decision Tree.</span><span class="sxs-lookup"><span data-stu-id="d633d-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="d633d-158">Copiare e incollare i moduli Train Model e Score Model nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="d633d-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span></span>
4. <span data-ttu-id="d633d-159">Trascinare il modulo **Evaluate Model** nell'area di disegno per confrontare i due algoritmi.</span><span class="sxs-lookup"><span data-stu-id="d633d-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span></span>
5. <span data-ttu-id="d633d-160">**Eseguire** l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="d633d-160">**Run** the experiment.</span></span>
   <span data-ttu-id="d633d-161">![Eseguire l'esperimento][10]</span><span class="sxs-lookup"><span data-stu-id="d633d-161">![Run the experiment][10]</span></span>
6. <span data-ttu-id="d633d-162">Fare clic con il pulsante destro del mouse sulla porta di output del modulo Evaluate Model e scegliere Visualize.</span><span class="sxs-lookup"><span data-stu-id="d633d-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="d633d-163">![Visualizzare i risultati della valutazione][11]</span><span class="sxs-lookup"><span data-stu-id="d633d-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="d633d-164">La metrica fornita include curva ROC, curva di precisione/recupero e curva di accuratezza.</span><span class="sxs-lookup"><span data-stu-id="d633d-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="d633d-165">Esaminando la metrica, si noterà che il primo modello fornisce prestazioni migliori rispetto al secondo.</span><span class="sxs-lookup"><span data-stu-id="d633d-165">Looking at these metrics, we can see that the first model performed better than the second one.</span></span> <span data-ttu-id="d633d-166">Per vedere i quali sono state le previsioni del primo modello, fare clic sulla porta di output di Score Model e scegliere Visualize.</span><span class="sxs-lookup"><span data-stu-id="d633d-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span></span>
<span data-ttu-id="d633d-167">![Visualizzare i risultati di punteggio][12]</span><span class="sxs-lookup"><span data-stu-id="d633d-167">![Visualize score results][12]</span></span>

<span data-ttu-id="d633d-168">Verranno visualizzate altre due colonne aggiunte al set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="d633d-168">You will see two more columns added to your test dataset.</span></span>

* <span data-ttu-id="d633d-169">Scored Probabilities: la probabilità che un cliente sia un acquirente di biciclette.</span><span class="sxs-lookup"><span data-stu-id="d633d-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="d633d-170">Scored Labels: la classificazione eseguita dal modello – acquirente di biciclette (1) o non acquirente (0).</span><span class="sxs-lookup"><span data-stu-id="d633d-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="d633d-171">La soglia di probabilità per le etichette è impostata su 50% e può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="d633d-171">This probability threshold for labeling is set to 50% and can be adjusted.</span></span>

<span data-ttu-id="d633d-172">Confrontando la colonna BikeBuyer (effettivo) con Scored Labels (stima), è possibile vedere il livello di prestazioni del modello.</span><span class="sxs-lookup"><span data-stu-id="d633d-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span></span> <span data-ttu-id="d633d-173">Come passaggi successivi è possibile usare questo modello per eseguire stime per i nuovi clienti e pubblicare il modello come un servizio Web o scrivere i risultati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d633d-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d633d-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d633d-174">Next steps</span></span>
<span data-ttu-id="d633d-175">Per altre informazioni sulla creazione di modelli di apprendimento automatico predittivi, fare riferimento a [Introduzione a Machine Learning in Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="d633d-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
