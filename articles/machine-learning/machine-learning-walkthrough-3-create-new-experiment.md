---
title: 'Passaggio 3: Creare un nuovo esperimento di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 3 della procedura dettagliata Sviluppare una soluzione predittiva: Creare un nuovo esperimento di formazione in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="bec41-103">Passaggio 3 della procedura dettagliata: Creare un nuovo esperimento di Machine Learning di Azure</span><span class="sxs-lookup"><span data-stu-id="bec41-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="bec41-104">Questo è il terzo passaggio della procedura dettagliata [Sviluppare una soluzione di analisi predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="bec41-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="bec41-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bec41-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="bec41-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="bec41-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="bec41-107">**Creare un nuovo esperimento**</span><span class="sxs-lookup"><span data-stu-id="bec41-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="bec41-108">Eseguire il training e valutare i modelli</span><span class="sxs-lookup"><span data-stu-id="bec41-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="bec41-109">Distribuire il servizio Web</span><span class="sxs-lookup"><span data-stu-id="bec41-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="bec41-110">Accedere al servizio Web</span><span class="sxs-lookup"><span data-stu-id="bec41-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="bec41-111">Il passaggio successivo di questa procedura dettagliata consiste nel creare un esperimento in Machine Learning Studio che usi il set di dati che è stato caricato.</span><span class="sxs-lookup"><span data-stu-id="bec41-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="bec41-112">In Studio fare clic su **+NEW** nella parte inferiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="bec41-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="bec41-113">Selezionare **EXPERIMENT**e quindi selezionare "Blank Experiment".</span><span class="sxs-lookup"><span data-stu-id="bec41-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Creare un nuovo esperimento][0]

2. <span data-ttu-id="bec41-115">Selezionare il nome dell'esperimento predefinito nella parte superiore dell'area di disegno e denominarlo in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="bec41-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Rinominare l'esperimento][5]
   
   > [!TIP]
   > <span data-ttu-id="bec41-117">È buona abitudine completare i campi **Summary** (Riepilogo) e **Description** (Descrizione) per l'esperimento nel riquadro **Properties** (Proprietà).</span><span class="sxs-lookup"><span data-stu-id="bec41-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="bec41-118">Queste proprietà offrono la possibilità di documentare l'esperimento, in modo che chiunque in seguito lo esamini sia in grado di comprendere gli obiettivi e la metodologia.</span><span class="sxs-lookup"><span data-stu-id="bec41-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Proprietà dell'esperimento][6]
   > 
3. <span data-ttu-id="bec41-120">Nella tavolozza dei moduli a sinistra dell'area di disegno dell'esperimento, espandere **Set di dati salvati**.</span><span class="sxs-lookup"><span data-stu-id="bec41-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="bec41-121">Trovare il set di dati creato in **My Datasets** e trascinarlo nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="bec41-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="bec41-122">È possibile trovare il set di dati anche immettendone il nome nella casella **Cerca** sopra alla tavolozza.</span><span class="sxs-lookup"><span data-stu-id="bec41-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![Aggiungere il set di dati all'esperimento][7]

## <a name="prepare-the-data"></a><span data-ttu-id="bec41-124">Preparare i dati</span><span class="sxs-lookup"><span data-stu-id="bec41-124">Prepare the data</span></span>
<span data-ttu-id="bec41-125">È possibile visualizzare le prime 100 righe di dati e alcune informazioni statistiche per l'intero set di dati: fare clic sulla porta di output del set di dati (il circoletto in basso) e selezionare **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="bec41-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="bec41-126">Poiché il file di dati non presentava intestazioni di colonna, Studio ha assegnato intestazioni generiche (Col1, Col2, *e così via*).</span><span class="sxs-lookup"><span data-stu-id="bec41-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="bec41-127">Anche se per la creazione di un modello non sono indispensabili intestazioni di colonna precise, queste semplificano l'uso dei dati nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bec41-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="bec41-128">Inoltre, quando il modello verrà pubblicato in un servizio Web, le intestazioni aiuteranno gli utenti del servizio a identificare le varie colonne.</span><span class="sxs-lookup"><span data-stu-id="bec41-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="bec41-129">È possibile aggiungere intestazioni di colonna usando il modulo [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="bec41-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="bec41-130">Si usa il modulo [Edit Metadata][edit-metadata] (Modifica metadati) per modificare i metadati associati a un set di dati.</span><span class="sxs-lookup"><span data-stu-id="bec41-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="bec41-131">In questo caso, verrà usato per immettere nomi più descrittivi per le intestazioni di colonna.</span><span class="sxs-lookup"><span data-stu-id="bec41-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="bec41-132">Per usare [Edit Metadata][edit-metadata] (Modifica metadati), è necessario specificare prima di tutto le colonne da modificare, in questo caso tutte. Quindi, è necessario specificare l'azione da eseguire su queste colonne, in questo caso la modifica delle intestazioni di colonna.</span><span class="sxs-lookup"><span data-stu-id="bec41-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="bec41-133">Nella tavolozza dei moduli digitare "metadati" nella casella **Cerca** .</span><span class="sxs-lookup"><span data-stu-id="bec41-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="bec41-134">Nell'elenco dei moduli viene visualizzato il modulo [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="bec41-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="bec41-135">Trascinare il modulo [Edit Metadata][edit-metadata] (Modifica metadati) nell'area di disegno e rilasciarlo sotto il set di dati precedentemente aggiunto.</span><span class="sxs-lookup"><span data-stu-id="bec41-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="bec41-136">Connettere il set di dati a [Edit Metadata][edit-metadata] (Modifica metadati): fare clic sulla porta di output del set di dati (il circoletto in fondo al set di dati), trascinarla sulla porta di input di [Edit Metadata][edit-metadata] (Modifica metadati) (il circoletto nella parte superiore del modulo), quindi rilasciare il pulsante del mouse.</span><span class="sxs-lookup"><span data-stu-id="bec41-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="bec41-137">Il set di dati e il modulo resteranno connessi anche se vengono spostati in un'altra posizione nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="bec41-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="bec41-138">L'esperimento avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="bec41-138">The experiment should now look something like this:</span></span>  
   
   ![Aggiunta di Edit Metadata][1]
   
   <span data-ttu-id="bec41-140">Il punto esclamativo rosso indica che le proprietà di questo modulo non sono ancora state configurate.</span><span class="sxs-lookup"><span data-stu-id="bec41-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="bec41-141">Ce ne occuperemo subito.</span><span class="sxs-lookup"><span data-stu-id="bec41-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bec41-142">È possibile aggiungere un commento a un modulo facendo doppio clic sul modulo e immettendo del testo.</span><span class="sxs-lookup"><span data-stu-id="bec41-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="bec41-143">In tal modo sarà possibile individuare subito l'operazione eseguita dal modulo nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bec41-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="bec41-144">In questo caso, fare doppio clic sul modulo [Edit Metadata][edit-metadata] (Modifica metadati) e digitare il commento "Add column headings".</span><span class="sxs-lookup"><span data-stu-id="bec41-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="bec41-145">Fare clic in un punto qualsiasi dell'area di disegno per chiudere la casella di testo.</span><span class="sxs-lookup"><span data-stu-id="bec41-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="bec41-146">Per visualizzare il commento, fare clic sulla freccia rivolta verso il basso nel modulo.</span><span class="sxs-lookup"><span data-stu-id="bec41-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Modulo (Modifica metadati) con il commento aggiunto][8]
   > 
4. <span data-ttu-id="bec41-148">Selezionare [Edit Metadata][edit-metadata] (Modifica metadati) e nel riquadro **Properties** (Proprietà) a destra dell'area di disegno fare clic su **Launch column selector** (Avvia selettore colonne).</span><span class="sxs-lookup"><span data-stu-id="bec41-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="bec41-149">Nella finestra di dialogo **Select columns** (Seleziona colonne) selezionare tutte le righe in **Available Columns** (Colonne disponibili) e fare clic su > per spostarle in **Selected Columns** (Colonne selezionate).</span><span class="sxs-lookup"><span data-stu-id="bec41-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="bec41-150">La finestra di dialogo dovrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="bec41-150">The dialog should look like this:</span></span>

   ![Selettore di colonna con tutte le colonne selezionate][2]

6. <span data-ttu-id="bec41-152">Fare clic sul segno di spunta **OK**.</span><span class="sxs-lookup"><span data-stu-id="bec41-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="bec41-153">Di nuovo nel riquadro **Properties** (Proprietà) cercare il parametro **New column names** (Nuovi nomi di colonna).</span><span class="sxs-lookup"><span data-stu-id="bec41-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="bec41-154">In questo campo immettere un elenco di nomi per le 21 colonne nel set di dati, separati da virgole e nell'ordine delle colonne.</span><span class="sxs-lookup"><span data-stu-id="bec41-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="bec41-155">È possibile ottenere i nomi di colonna dalla documentazione relativa ai set di dati disponibile sul sito Web UCI, oppure, per praticità, è possibile copiare e incollare l'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="bec41-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="bec41-156">Il riquadro Proprietà (Proprietà) ha l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="bec41-156">The Properties pane looks like this:</span></span>
   
   ![Proprietà per Edit Metadata][3]

> [!TIP]
> <span data-ttu-id="bec41-158">Se si vuole verificare le intestazioni di colonna, eseguire l'esperimento (fare clic su **RUN** (ESEGUI) sotto l'area di disegno dell'esperimento).</span><span class="sxs-lookup"><span data-stu-id="bec41-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="bec41-159">Al termine dell'esecuzione, ovvero quando viene visualizzato un segno di spunta in [Edit Metadata][edit-metadata] (Modifica metadati), fare clic sulla porta di output del modulo [Edit Metadata][edit-metadata] (Modifica metadati) e selezionare **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="bec41-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="bec41-160">È possibile visualizzare l'output di ogni modulo nello stesso modo in cui si visualizza lo stato dei dati nel corso dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bec41-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="bec41-161">Creazione di set di dati di training e di test</span><span class="sxs-lookup"><span data-stu-id="bec41-161">Create training and test datasets</span></span>
<span data-ttu-id="bec41-162">Sono necessari alcuni dati per il training e alcuni dati per il test del modello.</span><span class="sxs-lookup"><span data-stu-id="bec41-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="bec41-163">Nel passaggio successivo dell'esperimento, il set di dati viene quindi suddiviso in due set di dati separati: uno per il training e uno per il testing del modello.</span><span class="sxs-lookup"><span data-stu-id="bec41-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="bec41-164">Per eseguire questa operazione, viene usato il modulo [Split Data][split] (Divisione dati).</span><span class="sxs-lookup"><span data-stu-id="bec41-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="bec41-165">Trovare il modulo [Split Data][split] (Divisione dati), trascinarlo nell'area di disegno, quindi connetterlo al modulo [Edit Metadata][edit-metadata] (Modifica metadati).</span><span class="sxs-lookup"><span data-stu-id="bec41-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="bec41-166">Per impostazione predefinita, il rapporto di suddivisione è impostato su 0,5 e il parametro **Suddivisione casuale** è impostato.</span><span class="sxs-lookup"><span data-stu-id="bec41-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="bec41-167">Questo significa che una metà casuale dei dati verrà inviata come output attraverso una porta del modulo [Split Data][split] (Divisione dati) e l'altra metà attraverso l'altra.</span><span class="sxs-lookup"><span data-stu-id="bec41-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="bec41-168">È possibile regolare queste parametri, così come il parametro **Random seed** (Valore di inizializzazione casuale), per modificare la divisione tra dati di training e dati di test.</span><span class="sxs-lookup"><span data-stu-id="bec41-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="bec41-169">Per questo esempio i parametri vengono lasciati inalterati.</span><span class="sxs-lookup"><span data-stu-id="bec41-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bec41-170">La proprietà **Fraction of rows in the first output dataset** determina la quantità di dati da inviare alla porta di output *sinistra*.</span><span class="sxs-lookup"><span data-stu-id="bec41-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="bec41-171">Se ad esempio si imposta il rapporto su 0,7, il 70% dei dati verrà inviato alla porta sinistra e il 30% alla porta destra.</span><span class="sxs-lookup"><span data-stu-id="bec41-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="bec41-172">Fare doppio clic sul modulo [Split Data][split] (Divisione dati) e immettere il commento, "Training/testing data split 50%".</span><span class="sxs-lookup"><span data-stu-id="bec41-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="bec41-173">È possibile usare gli output del modulo [Split Data][split] (Divisione dati) nel modo preferito, ma in questo caso si sceglie di usare l'output sinistro per i dati di training e quello destro per i dati di test.</span><span class="sxs-lookup"><span data-stu-id="bec41-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="bec41-174">Come indicato nel [passaggio precedente](machine-learning-walkthrough-2-upload-data.md), il costo di un'errata classificazione come basso di un rischio di credito elevato è cinque volte maggiore del costo di un'errata classificazione come alto di un rischio di credito basso.</span><span class="sxs-lookup"><span data-stu-id="bec41-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="bec41-175">Tenendo conto di questa indicazione, viene generato un nuovo set di dati che rifletta questa funzione di costo.</span><span class="sxs-lookup"><span data-stu-id="bec41-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="bec41-176">Nel nuovo set di dati ogni esempio a rischio elevato viene replicato cinque volte, mentre ogni esempio a basso rischio non viene replicato.</span><span class="sxs-lookup"><span data-stu-id="bec41-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="bec41-177">Ciò è ottenibile usando il codice R:</span><span class="sxs-lookup"><span data-stu-id="bec41-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="bec41-178">Trovare e trascinare il modulo [Execute R Script][execute-r-script] (Esecuzione script R) nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bec41-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="bec41-179">Connettere la porta di output sinistra del modulo [Split Data][split] (Divisione dati) alla prima porta di input ("Dataset1") del modulo [Execute R Script][execute-r-script] (Esecuzione script R).</span><span class="sxs-lookup"><span data-stu-id="bec41-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="bec41-180">Fare doppio clic sul modulo [Execute R Script][execute-r-script] (Esecuzione script R) e immettere il commento "Set cost adjustment".</span><span class="sxs-lookup"><span data-stu-id="bec41-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="bec41-181">Nel riquadro **Properties** (Proprietà) eliminare il testo predefinito nel parametro **R Script** (Script R) e immettere questo script:</span><span class="sxs-lookup"><span data-stu-id="bec41-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script R nel modulo Execute R Script (Esecuzione script R)][9]

<span data-ttu-id="bec41-183">È necessario eseguire la stessa operazione di replica per ogni output del modulo [Split Data][split] (Divisione dati) in modo che i dati di training e di test abbiano la stessa rettifica del costo.</span><span class="sxs-lookup"><span data-stu-id="bec41-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="bec41-184">A questo scopo, il modulo [Execute R Script][execute-r-script] (Esecuzione script R) appena creato verrà duplicato e connesso all'altra porta di output del modulo [Split Data][split] (Divisione dati).</span><span class="sxs-lookup"><span data-stu-id="bec41-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="bec41-185">Fare clic con il pulsante destro del mouse sul modulo [Execute R Script][execute-r-script] (Esecuzione script R) e scegliere **Copy** (Copia).</span><span class="sxs-lookup"><span data-stu-id="bec41-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="bec41-186">Fare clic con il pulsante destro del mouse nell'area di disegno dell'esperimento, quindi selezionare **Incolla**.</span><span class="sxs-lookup"><span data-stu-id="bec41-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="bec41-187">Trascinare il nuovo modulo nella posizione scelta e quindi connettere la porta di output destra del modulo [Split Data][split] (Divisione dati) alla prima porta di input di questo nuovo modulo [Execute R Script][execute-r-script] (Esecuzione script R).</span><span class="sxs-lookup"><span data-stu-id="bec41-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="bec41-188">Fare clic su **Run** (Esegui) nella parte inferiore dell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="bec41-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="bec41-189">La copia del modulo Esecuzione script R contiene lo stesso script contenuto nel modulo originale.</span><span class="sxs-lookup"><span data-stu-id="bec41-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="bec41-190">Quando si copia e incolla un modulo sull'area di disegno, la copia conserva tutte le proprietà dell'originale.</span><span class="sxs-lookup"><span data-stu-id="bec41-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="bec41-191">L'esperimento avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="bec41-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="bec41-193">Per altre informazioni sull'uso di script R negli esperimenti, vedere [Estendere l'esperimento con R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="bec41-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="bec41-194">**Passaggio successivo: [Eseguire il training e la valutazione del modello](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="bec41-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
