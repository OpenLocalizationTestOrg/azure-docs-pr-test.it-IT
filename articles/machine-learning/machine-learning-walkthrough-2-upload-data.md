---
title: 'Passaggio 2: Caricare dati in un esperimento di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 2 di hello sviluppare una procedura dettagliata soluzione predittiva: caricamento archiviati dati pubblici in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="71b03-103">Passaggio 2 della procedura dettagliata: Caricare dati esistenti in un esperimento di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71b03-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="71b03-104">Questo è hello secondo passaggio della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="71b03-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="71b03-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71b03-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="71b03-106">**Caricare i dati esistenti**</span><span class="sxs-lookup"><span data-stu-id="71b03-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="71b03-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="71b03-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="71b03-108">Eseguire il training e valutare i modelli di hello</span><span class="sxs-lookup"><span data-stu-id="71b03-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="71b03-109">Distribuzione di servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="71b03-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="71b03-110">Accedere al servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="71b03-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="71b03-111">toodevelop un modello predittivo per rischio di credito, è necessario che i dati che è possibile utilizzare tootrain e quindi testare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="71b03-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="71b03-112">Per questa procedura dettagliata, verrà utilizzata dal repository UC Irvine Machine Learning hello hello "Set di dati UCI Statlog (tedesco credito dati)".</span><span class="sxs-lookup"><span data-stu-id="71b03-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="71b03-113">disponibile al seguente indirizzo:</span><span class="sxs-lookup"><span data-stu-id="71b03-113">You can find it here:</span></span>  
<span data-ttu-id="71b03-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="71b03-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="71b03-115">Si userà il file hello denominato **german.data**.</span><span class="sxs-lookup"><span data-stu-id="71b03-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="71b03-116">Scaricare questo file tooyour disco rigido locale.</span><span class="sxs-lookup"><span data-stu-id="71b03-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="71b03-117">Hello **german.data** set di dati contiene righe di 20 variabili per 1000 ultimi candidati per la carta di credito.</span><span class="sxs-lookup"><span data-stu-id="71b03-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="71b03-118">Queste 20 variabili rappresentano il set di hello del set di funzionalità (hello *vettore di funzione*), che fornisce le caratteristiche di identificazione per ciascun candidato di carta di credito.</span><span class="sxs-lookup"><span data-stu-id="71b03-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="71b03-119">Una colonna aggiuntiva in ogni riga rappresenta il rischio di credito calcolata del candidato hello, con i 700 candidati identificati come un rischio di credito bassa e 300 come un rischio elevato.</span><span class="sxs-lookup"><span data-stu-id="71b03-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="71b03-120">sito UCI Hello fornisce una descrizione degli attributi di hello del vettore di funzione hello per questi dati.</span><span class="sxs-lookup"><span data-stu-id="71b03-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="71b03-121">Questo include informazioni finanziarie, storico dei crediti, stato di occupazione e dati personali.</span><span class="sxs-lookup"><span data-stu-id="71b03-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="71b03-122">Per ogni richiedente è stata assegnata una valutazione in formato binario per indicare se è a basso o ad alto rischio.</span><span class="sxs-lookup"><span data-stu-id="71b03-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="71b03-123">Verrà utilizzata questa tootrain dati un modello predittivo analitica.</span><span class="sxs-lookup"><span data-stu-id="71b03-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="71b03-124">Al termine, il modello deve essere in grado di tooaccept un vettore di funzione per un nuovo utente e stimare se è un rischio di credito low o high.</span><span class="sxs-lookup"><span data-stu-id="71b03-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="71b03-125">Ma ecco un'interessante svolta.</span><span class="sxs-lookup"><span data-stu-id="71b03-125">Here's an interesting twist.</span></span> <span data-ttu-id="71b03-126">Hello descrizione del set di dati di hello in menziona sito UCI di hello comportano anche costi se si misclassify il rischio di credito di una persona.</span><span class="sxs-lookup"><span data-stu-id="71b03-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="71b03-127">Se il modello di hello viene stimato un rischio elevato per un utente che è effettivamente un rischio di credito bassa, il modello di hello ha una classificazione non corretta.</span><span class="sxs-lookup"><span data-stu-id="71b03-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="71b03-128">Ma classificazione non corretta inversa hello è cinque volte più costosa istituto toohello: se il modello di hello viene stimato un rischio di credito insufficiente per un utente che è effettivamente un rischio elevato.</span><span class="sxs-lookup"><span data-stu-id="71b03-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="71b03-129">In tal caso, è necessario tootrain il nostro modello in modo che il costo di hello di questo tipo di classificazione non corretta di quest'ultimo è cinque volte superiore interpretata hello altro modo.</span><span class="sxs-lookup"><span data-stu-id="71b03-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="71b03-130">Un modo semplice toodo questo modello hello nell'esperimento di training quando è duplicando (cinque volte) le voci che rappresentano un utente con un rischio elevato.</span><span class="sxs-lookup"><span data-stu-id="71b03-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="71b03-131">Quindi, se il modello di hello interpreta come un rischio di credito insufficiente quando sono in realtà un rischio elevato, hello modello non tale classificazione non corretta stesso cinque volte, una volta per ogni elemento duplicato.</span><span class="sxs-lookup"><span data-stu-id="71b03-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="71b03-132">Si aumenterà il costo di hello di questo errore nei risultati di training hello.</span><span class="sxs-lookup"><span data-stu-id="71b03-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="71b03-133">Convertire il formato di set di dati hello</span><span class="sxs-lookup"><span data-stu-id="71b03-133">Convert hello dataset format</span></span>
<span data-ttu-id="71b03-134">set di dati originale Hello utilizza un formato delimitato da spazio vuoto.</span><span class="sxs-lookup"><span data-stu-id="71b03-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="71b03-135">Machine Learning Studio funziona meglio con un valore delimitato da virgole (CSV), quindi verrà convertito hello dataset sostituendo gli spazi con virgole.</span><span class="sxs-lookup"><span data-stu-id="71b03-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="71b03-136">Esistono molti modi tooconvert questi dati.</span><span class="sxs-lookup"><span data-stu-id="71b03-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="71b03-137">Un modo consiste nell'utilizzare hello comando di Windows PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="71b03-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="71b03-138">È inoltre possibile utilizzare hello Unix sed comando:</span><span class="sxs-lookup"><span data-stu-id="71b03-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="71b03-139">In entrambi i casi, è stata creata una versione delimitato da virgole dei dati di hello in un file denominato **german.csv** che è possibile utilizzare nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="71b03-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="71b03-140">Caricare set di dati di hello tooMachine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="71b03-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="71b03-141">Dopo aver convertito tooCSV formato dati hello, dobbiamo tooupload in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="71b03-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="71b03-142">Home page di hello aprire Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="71b03-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="71b03-143">Fare clic sul menu hello ![Menu][1] hello superiore sinistro della finestra hello, fare clic su **Azure Machine Learning**selezionare **Studio**ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="71b03-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="71b03-144">Fare clic su **+ nuovo** nella parte inferiore di hello della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="71b03-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="71b03-145">Selezionare **DATASET**.</span><span class="sxs-lookup"><span data-stu-id="71b03-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="71b03-146">Selezionare **FROM LOCAL FILE**.</span><span class="sxs-lookup"><span data-stu-id="71b03-146">Select **FROM LOCAL FILE**.</span></span>

    ![Aggiungere un set di dati da un file locale][2]

6. <span data-ttu-id="71b03-148">In hello **caricare un nuovo set di dati** finestra di dialogo, fare clic su **Sfoglia** e trovare hello **german.csv** file creato.</span><span class="sxs-lookup"><span data-stu-id="71b03-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="71b03-149">Immettere un nome per set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="71b03-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="71b03-150">Per questa procedura, il nome sarà "UCI German Credit Card Data".</span><span class="sxs-lookup"><span data-stu-id="71b03-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="71b03-151">Come tipo di dati selezionare **Generic CSV File With no header (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="71b03-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="71b03-152">Aggiungere un'eventuale descrizione.</span><span class="sxs-lookup"><span data-stu-id="71b03-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="71b03-153">Fare clic su hello **OK** segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="71b03-153">Click hello **OK** check mark.</span></span>  

    ![Caricare set di dati hello][3]

<span data-ttu-id="71b03-155">Consente di caricare dati hello in un modulo di set di dati che è possibile utilizzare in un esperimento.</span><span class="sxs-lookup"><span data-stu-id="71b03-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="71b03-156">È possibile gestire i set di dati che è stato caricato tooStudio facendo hello **set di dati** toohello scheda a sinistra della finestra Studio hello.</span><span class="sxs-lookup"><span data-stu-id="71b03-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Gestire i set di dati][4]

<span data-ttu-id="71b03-158">Per altre informazioni sull'importazione di altri tipi di dati in un esperimento, vedere [Importare dati di training in Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="71b03-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="71b03-159">**Passaggi successivi: [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="71b03-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
