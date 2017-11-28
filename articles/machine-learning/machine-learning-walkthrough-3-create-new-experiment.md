---
title: 'Passaggio 3: Creare un nuovo esperimento di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 3 di hello sviluppare una procedura dettagliata soluzione predittiva: creare un nuovo esperimento di training in Azure Machine Learning Studio.'
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
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="305b6-103">Passaggio 3 della procedura dettagliata: Creare un nuovo esperimento di Machine Learning di Azure</span><span class="sxs-lookup"><span data-stu-id="305b6-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="305b6-104">Si tratta di hello passaggio terza procedura dettagliata, hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="305b6-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="305b6-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="305b6-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="305b6-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="305b6-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="305b6-107">**Creare un nuovo esperimento**</span><span class="sxs-lookup"><span data-stu-id="305b6-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="305b6-108">Eseguire il training e valutare i modelli di hello</span><span class="sxs-lookup"><span data-stu-id="305b6-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="305b6-109">Distribuzione di servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="305b6-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="305b6-110">Accedere al servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="305b6-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="305b6-111">passaggio successivo di Hello in questa procedura dettagliata è toocreate un esperimento di Machine Learning Studio che utilizza set di dati hello che è caricati.</span><span class="sxs-lookup"><span data-stu-id="305b6-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="305b6-112">In Studio, fare clic su **+ nuovo** nella parte inferiore di hello della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="305b6-113">Selezionare **EXPERIMENT**e quindi selezionare "Blank Experiment".</span><span class="sxs-lookup"><span data-stu-id="305b6-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Creare un nuovo esperimento][0]

2. <span data-ttu-id="305b6-115">Predefinito selezionare hello sperimentare nome nella parte superiore di hello dell'area di disegno hello e rinominarlo toosomething significativo.</span><span class="sxs-lookup"><span data-stu-id="305b6-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Rinominare l'esperimento][5]
   
   > [!TIP]
   > <span data-ttu-id="305b6-117">È una buona norma toofill **riepilogo** e **descrizione** per esperimento hello in hello **proprietà** riquadro.</span><span class="sxs-lookup"><span data-stu-id="305b6-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="305b6-118">Fornire queste proprietà si hello esperimento di probabilità toodocument hello in modo che chiunque utilizzi in un secondo momento è possibile comprendere gli obiettivi e la metodologia.</span><span class="sxs-lookup"><span data-stu-id="305b6-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Proprietà dell'esperimento][6]
   > 
3. <span data-ttu-id="305b6-120">In hello modulo tavolozza toohello a sinistra dell'area di disegno esperimento hello, espandere **Saved Datasets**.</span><span class="sxs-lookup"><span data-stu-id="305b6-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="305b6-121">Trova hello set di dati creati in **set di dati personali** e trascinarlo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="305b6-122">È anche possibile trovare hello set di dati immettendo il nome di hello in hello **ricerca** casella sopra tavolozza hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Aggiungere l'esperimento di toohello hello set di dati][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="305b6-124">Preparare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="305b6-124">Prepare hello data</span></span>
<span data-ttu-id="305b6-125">È possibile visualizzare hello prime 100 righe di dati hello e alcune informazioni statistiche per l'intero set di dati hello: fare clic sulla porta di output di hello del set di dati hello (hello piccolo cerchio nella parte inferiore di hello) e selezionare **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="305b6-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="305b6-126">Poiché le intestazioni di colonna non è disponibile il file di dati di hello, Studio ha fornito le intestazioni generiche (Col1, Col2, *e così via*).</span><span class="sxs-lookup"><span data-stu-id="305b6-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="305b6-127">Buona intestazioni non sono essenziali toocreating un modello, ma rendono più semplice toowork con dati hello nell'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="305b6-128">Inoltre, quando verrà pubblicato alla fine di questo modello in un servizio web, intestazioni hello consentono di identificare hello colonne toohello utente del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="305b6-129">È possibile aggiungere intestazioni di colonna utilizzando hello [Modifica metadati] [ edit-metadata] modulo.</span><span class="sxs-lookup"><span data-stu-id="305b6-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="305b6-130">Utilizzare hello [Modifica metadati] [ edit-metadata] toochange metadati del modulo associato a un set di dati.</span><span class="sxs-lookup"><span data-stu-id="305b6-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="305b6-131">In questo caso, è utilizzarlo tooprovide nomi più descrittivi per le intestazioni di colonna.</span><span class="sxs-lookup"><span data-stu-id="305b6-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="305b6-132">toouse [Modifica metadati][edit-metadata], è innanzitutto necessario specificare quale toomodify colonne (in questo caso, tutti gli elementi.) Specificare quindi hello azione toobe eseguite su tali colonne (in questo caso, la modifica delle intestazioni di colonna.)</span><span class="sxs-lookup"><span data-stu-id="305b6-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="305b6-133">Nella tavolozza modulo hello, digitare "metadati" hello **ricerca** casella.</span><span class="sxs-lookup"><span data-stu-id="305b6-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="305b6-134">Hello [Modifica metadati] [ edit-metadata] viene visualizzato nell'elenco dei moduli di hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="305b6-135">Fare clic e trascinare hello [Modifica metadati] [ edit-metadata] modulo sul hello area di disegno e rilasciarla sotto hello dataset viene aggiunto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="305b6-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="305b6-136">Connettersi hello dataset toohello [Modifica metadati][edit-metadata]: fare clic sulla porta di output di hello del set di dati hello (hello piccolo cerchio nella parte inferiore di hello del set di dati hello), trascinare una porta di input di toohello [Modifica metadati ] [ edit-metadata] (hello piccolo cerchio nella parte superiore di hello del modulo hello), quindi rilasciare il pulsante di mouse hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="305b6-137">nel modulo e set di dati hello rimangano connesse, anche se uno spostarsi nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="305b6-138">sperimentazione Hello dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="305b6-138">hello experiment should now look something like this:</span></span>  
   
   ![Aggiunta di Edit Metadata][1]
   
   <span data-ttu-id="305b6-140">punto esclamativo rosso Hello indica che è ancora non impostato le proprietà di hello per questo modulo.</span><span class="sxs-lookup"><span data-stu-id="305b6-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="305b6-141">Ce ne occuperemo subito.</span><span class="sxs-lookup"><span data-stu-id="305b6-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="305b6-142">È possibile aggiungere un modulo tooa commento facendo doppio clic su modulo hello e immissione di testo.</span><span class="sxs-lookup"><span data-stu-id="305b6-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="305b6-143">Ciò consente di visualizzare a colpo d'occhio esegue il modulo hello nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="305b6-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="305b6-144">In questo caso, fare doppio clic su hello [Modifica metadati] [ edit-metadata] modulo e il tipo hello commento "Add intestazioni di colonna".</span><span class="sxs-lookup"><span data-stu-id="305b6-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="305b6-145">Fare clic su qualsiasi altra posizione nella casella di testo hello tooclose hello area di disegno.</span><span class="sxs-lookup"><span data-stu-id="305b6-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="305b6-146">toodisplay hello commento, fare clic sulla freccia hello sul modulo hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Modulo (Modifica metadati) con il commento aggiunto][8]
   > 
4. <span data-ttu-id="305b6-148">Selezionare [Modifica metadati][edit-metadata]e in hello **proprietà** toohello riquadro a destra dell'area di disegno hello, fare clic su **selettore di colonna avvio**.</span><span class="sxs-lookup"><span data-stu-id="305b6-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="305b6-149">In hello **selezionare colonne** finestra di dialogo, selezionare tutte le righe di hello **colonne disponibili** e fare clic su > toomove li troppo**colonne selezionate**.</span><span class="sxs-lookup"><span data-stu-id="305b6-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="305b6-150">finestra di dialogo Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="305b6-150">hello dialog should look like this:</span></span>

   ![Selettore di colonna con tutte le colonne selezionate][2]

6. <span data-ttu-id="305b6-152">Fare clic su hello **OK** segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="305b6-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="305b6-153">In hello **proprietà** riquadro, cercare hello **nuovi nomi di colonna** parametro.</span><span class="sxs-lookup"><span data-stu-id="305b6-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="305b6-154">In questo campo, immettere un elenco di nomi per le colonne di 21 hello nel set di dati hello, separati da virgole e nell'ordine delle colonne.</span><span class="sxs-lookup"><span data-stu-id="305b6-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="305b6-155">È possibile ottenere i nomi delle colonne hello nella documentazione di set di dati hello sul sito UCI hello, oppure per motivi di praticità, è possibile copiare e incollare hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="305b6-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="305b6-156">riquadro Proprietà Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="305b6-156">hello Properties pane looks like this:</span></span>
   
   ![Proprietà per Edit Metadata][3]

> [!TIP]
> <span data-ttu-id="305b6-158">Se si desidera intestazioni di colonna hello tooverify, eseguire l'esperimento hello (fare clic su **eseguire** sotto l'area di disegno esperimento hello).</span><span class="sxs-lookup"><span data-stu-id="305b6-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="305b6-159">Quando al termine dell'esecuzione (viene visualizzato un segno di spunta verde nella [Modifica metadati][edit-metadata]), fare clic sulla porta di output di hello di hello [Modifica metadati] [ edit-metadata] modulo, quindi selezionare **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="305b6-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="305b6-160">È possibile visualizzare l'output di hello di qualsiasi modulo in hello stesso modo tooview hello lo stato di avanzamento dei dati di hello tramite esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="305b6-161">Creazione di set di dati di training e di test</span><span class="sxs-lookup"><span data-stu-id="305b6-161">Create training and test datasets</span></span>
<span data-ttu-id="305b6-162">Abbiamo bisogno di un modello di dati tootrain hello e alcuni tootest è.</span><span class="sxs-lookup"><span data-stu-id="305b6-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="305b6-163">Pertanto in hello passaggio successivo dell'esperimento hello hello set di dati verranno suddivise in due set di dati separati: uno per il training, il modello e uno per il testing.</span><span class="sxs-lookup"><span data-stu-id="305b6-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="305b6-164">toodo, utilizziamo hello [dati divisi] [ split] modulo.</span><span class="sxs-lookup"><span data-stu-id="305b6-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="305b6-165">Trovare hello [dati divisi] [ split] modulo, trascinarla nell'area di disegno hello e connetterla toohello [Modifica metadati] [ edit-metadata] modulo.</span><span class="sxs-lookup"><span data-stu-id="305b6-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="305b6-166">Per impostazione predefinita, il rapporto di divisione hello è 0,5 e hello **divisione casuale** parametro è impostato.</span><span class="sxs-lookup"><span data-stu-id="305b6-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="305b6-167">Ciò significa che una metà casuale dei dati hello è output tramite una porta di hello [dati divisi] [ split] modulo e metà tramita hello altri.</span><span class="sxs-lookup"><span data-stu-id="305b6-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="305b6-168">È possibile modificare questi parametri, nonché hello **Random seed** parametro hello toochange suddiviso tra i set di training e dati di testing.</span><span class="sxs-lookup"><span data-stu-id="305b6-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="305b6-169">Per questo esempio i parametri vengono lasciati inalterati.</span><span class="sxs-lookup"><span data-stu-id="305b6-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="305b6-170">proprietà Hello **frazione di righe in hello set di dati di output prima** determina la quantità di dati hello è output tramite hello *sinistro* porta di output.</span><span class="sxs-lookup"><span data-stu-id="305b6-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="305b6-171">Ad esempio, se si imposta hello rapporto too0.7, 70% dei dati hello è output tramite hello lasciato porta e il 30% tramite la porta di destra hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="305b6-172">Fare doppio clic su hello [dati divisi] [ split] modulo e immettere il commento hello, "dati di testing/Training divisione 50%".</span><span class="sxs-lookup"><span data-stu-id="305b6-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="305b6-173">È possibile utilizzare l'output di hello di hello [dati divisi] [ split] test come dati di output di modulo, tuttavia è ad esempio, ma è opportuno scegliere toouse hello output a sinistra sotto forma di dati di training e hello destra.</span><span class="sxs-lookup"><span data-stu-id="305b6-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="305b6-174">Come accennato in hello [passaggio precedente](machine-learning-walkthrough-2-upload-data.md), interpretato come un rischio elevato come basso costo hello è cinque volte superiore costo hello interpretato come un rischio di credito bassa come high.</span><span class="sxs-lookup"><span data-stu-id="305b6-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="305b6-175">tooaccount per questo, si genera un nuovo set di dati che riflette la funzione di costo.</span><span class="sxs-lookup"><span data-stu-id="305b6-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="305b6-176">In hello nuovo set di dati, ogni esempio ad alto rischio viene replicato cinque volte, ogni esempio basso rischio non viene replicata.</span><span class="sxs-lookup"><span data-stu-id="305b6-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="305b6-177">Ciò è ottenibile usando il codice R:</span><span class="sxs-lookup"><span data-stu-id="305b6-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="305b6-178">Individuare e trascinare hello [Execute R Script] [ execute-r-script] modulo nell'area di disegno di hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="305b6-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="305b6-179">Connettersi a sinistra sulla porta di output di hello hello [dati divisi] [ split] toohello modulo ("Dataset1") di porta di input prima di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="305b6-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="305b6-180">Fare doppio clic su hello [Execute R Script] [ execute-r-script] modulo e immettere il commento hello, "Set rettifica costo".</span><span class="sxs-lookup"><span data-stu-id="305b6-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="305b6-181">In hello **proprietà** riquadro testo predefinito hello di eliminazione in hello **Script R** parametro e immettere lo script:</span><span class="sxs-lookup"><span data-stu-id="305b6-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script R nel modulo Execute R Script hello][9]

<span data-ttu-id="305b6-183">È necessario toodo la stessa operazione di replica per ogni output di hello [dati divisi] [ split] rettifica costo di modulo in modo da avere hello che hello set di training e dati di test stesso.</span><span class="sxs-lookup"><span data-stu-id="305b6-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="305b6-184">Hello più semplice toodo modo tratta duplicando hello [Execute R Script] [ execute-r-script] modulo è appena creata e connetterlo toohello altri output porta di hello [dati divisi] [ split] modulo.</span><span class="sxs-lookup"><span data-stu-id="305b6-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="305b6-185">Pulsante destro del mouse hello [Execute R Script] [ execute-r-script] modulo e selezionare **copia**.</span><span class="sxs-lookup"><span data-stu-id="305b6-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="305b6-186">Area di disegno esperimento hello e scegliere **Incolla**.</span><span class="sxs-lookup"><span data-stu-id="305b6-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="305b6-187">Trascinare il nuovo modulo hello nella posizione e quindi connettere la porta di output di destra hello di hello [dati divisi] [ split] modulo toohello prima porta di input di questo nuovo [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="305b6-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="305b6-188">Nella parte inferiore di hello dell'area di disegno hello, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="305b6-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="305b6-189">copia di Hello del modulo Execute R Script hello contiene hello stesso script come modulo originale hello.</span><span class="sxs-lookup"><span data-stu-id="305b6-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="305b6-190">Quando si copia e Incolla di un modulo nell'area di disegno hello, copia hello mantiene tutte le proprietà di hello di hello originale.</span><span class="sxs-lookup"><span data-stu-id="305b6-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="305b6-191">L'esperimento avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="305b6-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="305b6-193">Per altre informazioni sull'uso di script R negli esperimenti, vedere [Estendere l'esperimento con R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="305b6-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="305b6-194">**Passaggio successivo: [Train e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="305b6-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
