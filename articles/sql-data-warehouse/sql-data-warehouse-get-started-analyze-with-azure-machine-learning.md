---
title: dati aaaAnalyze con Azure Machine Learning | Documenti Microsoft
description: Utilizzare Azure Machine Learning toobuild un stima modello di machine learning basato sui dati archiviati in Azure SQL Data Warehouse.
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
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="cc2aa-103">Analizzare i dati con Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cc2aa-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc2aa-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="cc2aa-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="cc2aa-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cc2aa-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="cc2aa-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc2aa-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="cc2aa-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="cc2aa-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="cc2aa-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="cc2aa-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="cc2aa-109">Questa esercitazione Usa Azure Machine Learning toobuild un stima modello di machine learning basato sui dati archiviati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="cc2aa-110">In particolare, si compila una campagna di marketing di Adventure Works, shop bike hello, per stimare se un cliente è toobuy probabilmente una bicicletta o non.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cc2aa-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cc2aa-111">Prerequisites</span></span>
<span data-ttu-id="cc2aa-112">toostep di questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="cc2aa-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="cc2aa-113">Un'istanza di SQL Data Warehouse in cui sia precaricato il database di esempio AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="cc2aa-114">tooprovision questa operazione, vedere [creare un Data Warehouse SQL] [ Create a SQL Data Warehouse] e selezionare i dati di esempio hello tooload.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="cc2aa-115">Se si ha già un data warehouse, ma non i dati di esempio, è possibile [caricare manualmente i dati di esempio][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="cc2aa-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="cc2aa-116">1. Ottenere dati hello</span><span class="sxs-lookup"><span data-stu-id="cc2aa-116">1. Get hello data</span></span>
<span data-ttu-id="cc2aa-117">dati Hello sono nella visualizzazione dbo.vTargetMail hello nel database AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="cc2aa-118">tooread dati:</span><span class="sxs-lookup"><span data-stu-id="cc2aa-118">tooread this data:</span></span>

1. <span data-ttu-id="cc2aa-119">Accedere ad [Azure Machine Learning Studio][Azure Machine Learning studio] e fare clic sugli esperimenti personali.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="cc2aa-120">Fare clic su **+NEW** e selezionare **Esperimento vuoto**.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="cc2aa-121">Immettere un nome per l'esperimento: Marketing mirato.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="cc2aa-122">Hello trascinare **lettore** modulo dal riquadro moduli hello in canvas hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="cc2aa-123">Specificare i dettagli di hello del database di SQL Data Warehouse nel riquadro Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="cc2aa-124">Specificare il database di hello **query** dati hello tooread di interesse.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-124">Specify hello database **query** tooread hello data of interest.</span></span>

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

<span data-ttu-id="cc2aa-125">Eseguire l'esperimento hello facendo **eseguire** sotto l'area di disegno di hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="cc2aa-126">![Eseguire l'esperimento hello][1]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="cc2aa-127">Al termine esperimento hello eseguite correttamente, fare clic sulla porta di output di hello nella parte inferiore di hello del modulo del lettore hello e selezionare **Visualizza** toosee hello importati i dati.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="cc2aa-128">![Visualizzare i dati importati][3]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="cc2aa-129">2. Dati hello pulita</span><span class="sxs-lookup"><span data-stu-id="cc2aa-129">2. Clean hello data</span></span>
<span data-ttu-id="cc2aa-130">dati hello tooclean, eliminare alcune colonne non rilevanti per il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="cc2aa-131">toodo questo:</span><span class="sxs-lookup"><span data-stu-id="cc2aa-131">toodo this:</span></span>

1. <span data-ttu-id="cc2aa-132">Hello trascinare **Project Columns** modulo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="cc2aa-133">Fare clic su **selettore di colonna avvio** in hello proprietà riquadro toospecify le colonne che si desidera toodrop.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="cc2aa-134">![Project Columns][4]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="cc2aa-135">Escludere due colonne: CustomerAlternateKey e GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="cc2aa-136">![Rimuovere le colonne non necessarie][5]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="cc2aa-137">3. Compilare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="cc2aa-137">3. Build hello model</span></span>
<span data-ttu-id="cc2aa-138">Si suddividerà hello dati 80: 20: 80% tootrain un modello di machine learning e 20% tootest hello modello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="cc2aa-139">Verrà utilizzare algoritmi di "Two-Class" hello per questo problema di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="cc2aa-140">Hello trascinare **Split** modulo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="cc2aa-141">Immettere 0,8 per la frazione di righe in hello primo output set di dati nel riquadro Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="cc2aa-142">![Dividere i dati in set di traning e di test][6]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="cc2aa-143">Hello trascinare **Two-Class Boosted Decision Tree** modulo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="cc2aa-144">Hello trascinare **Train Model** modulo in hello area di disegno e specificare gli input hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="cc2aa-145">Quindi, fare clic su **selettore di colonna avvio** nel riquadro Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="cc2aa-146">Primo input: algoritmo ML.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="cc2aa-147">Secondo input: algoritmo hello tootrain dei dati in.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="cc2aa-148">![Connettersi modulo Train Model hello][7]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="cc2aa-149">Seleziona hello **BikeBuyer** colonna come colonna toopredict hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="cc2aa-150">![Selezionare una colonna toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="cc2aa-151">4. Modello di punteggio hello</span><span class="sxs-lookup"><span data-stu-id="cc2aa-151">4. Score hello model</span></span>
<span data-ttu-id="cc2aa-152">A questo punto, si testerà il modello di hello esegue sui dati di test.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="cc2aa-153">Confronteremo algoritmo hello scelto con un algoritmo diverso di toosee che offre prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="cc2aa-154">Trascinare **Score Model** modulo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="cc2aa-155">Primo input: training del modello secondo input: dati di Test ![Score model hello][9]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="cc2aa-156">Hello trascinare **Two-Class Bayes Point Machine** nell'area di disegno di hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="cc2aa-157">Confronteremo modalità di funzionamento di questo algoritmo in confronto toohello Two-Class Boosted Decision Tree.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="cc2aa-158">Copia e Incolla hello moduli Train Model e Score Model hello area di disegno.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="cc2aa-159">Hello trascinare **Evaluate Model** modulo negli algoritmi di hello canvas toocompare hello due.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="cc2aa-160">**Eseguire** hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="cc2aa-161">![Eseguire l'esperimento hello][10]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="cc2aa-162">Fare clic sulla porta di output di hello nella parte inferiore di hello del modulo Evaluate Model hello e fare clic su Visualizza.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="cc2aa-163">![Visualizzare i risultati della valutazione][11]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="cc2aa-164">metriche Hello fornite sono curve ROC hello, precisione, richiamo diagramma e accuratezza curva.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="cc2aa-165">Analizzando queste metriche, possiamo vedere che primo modello hello eseguita meglio di hello secondo.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="cc2aa-166">toolook in hello cosa hello primo modello previsto, fare clic sulla porta di output di hello Score Model e fare clic su Visualizza.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="cc2aa-167">![Visualizzare i risultati di punteggio][12]</span><span class="sxs-lookup"><span data-stu-id="cc2aa-167">![Visualize score results][12]</span></span>

<span data-ttu-id="cc2aa-168">Verrà visualizzato che il set di test tooyour di aggiunto altre due colonne.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="cc2aa-169">Probabilità con punteggi: probabilità hello che un cliente è un acquirente di biciclette.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="cc2aa-170">Etichette con punteggio: hello classificazione eseguita dal modello hello – acquirente di biciclette (1) o non (0).</span><span class="sxs-lookup"><span data-stu-id="cc2aa-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="cc2aa-171">Questa soglia di probabilità per le etichette è impostata too50% e può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="cc2aa-172">Confronto tra la colonna hello BikeBuyer (effettivo) con hello Scored Labels (stima), è possibile visualizzare l'accuratezza modello di hello è ha eseguito.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="cc2aa-173">Come passaggi successivi, è possibile utilizzare le stime toomake questo modello per i nuovi clienti e pubblicare questo modello come un servizio web o scrivere risultati indietro tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc2aa-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc2aa-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc2aa-174">Next steps</span></span>
<span data-ttu-id="cc2aa-175">toolearn creazione predittivo modelli di machine learning, vedere troppo[tooMachine introduzione di apprendimento in Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="cc2aa-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

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
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
