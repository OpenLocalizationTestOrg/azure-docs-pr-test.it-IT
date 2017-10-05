---
title: 'Passaggio 2: Caricare dati in un esperimento di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 2 della procedura dettagliata Sviluppare una soluzione predittiva: Caricare dati pubblici archiviati in Azure Machine Learning Studio'
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
ms.openlocfilehash: c2ab5f5252e1ea1ec51f6c3bd489826c70ff011c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="c6809-103">Passaggio 2 della procedura dettagliata: Caricare dati esistenti in un esperimento di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c6809-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="c6809-104">Questo è il secondo passaggio della procedura dettagliata [Sviluppare una soluzione di analisi predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="c6809-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="c6809-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c6809-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="c6809-106">**Caricare i dati esistenti**</span><span class="sxs-lookup"><span data-stu-id="c6809-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="c6809-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="c6809-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="c6809-108">Eseguire il training e valutare i modelli</span><span class="sxs-lookup"><span data-stu-id="c6809-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="c6809-109">Distribuire il servizio Web</span><span class="sxs-lookup"><span data-stu-id="c6809-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="c6809-110">Accedere al servizio Web</span><span class="sxs-lookup"><span data-stu-id="c6809-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="c6809-111">Per sviluppare un modello predittivo per il rischio di credito, abbiamo bisogno di dati da usare per eseguire il training del modello e quindi testare il modello.</span><span class="sxs-lookup"><span data-stu-id="c6809-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="c6809-112">Per questa procedura verrà usato il set di dati "UCI Statlog (German Credit Data)" da UCI Irvine Machine Learning Repository,</span><span class="sxs-lookup"><span data-stu-id="c6809-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="c6809-113">disponibile al seguente indirizzo:</span><span class="sxs-lookup"><span data-stu-id="c6809-113">You can find it here:</span></span>  
<span data-ttu-id="c6809-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="c6809-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="c6809-115">Verrà usato il file denominato **german.data**.</span><span class="sxs-lookup"><span data-stu-id="c6809-115">We'll use the file named **german.data**.</span></span> <span data-ttu-id="c6809-116">Scaricare questo file nel disco rigido locale.</span><span class="sxs-lookup"><span data-stu-id="c6809-116">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="c6809-117">Il set di dati **german.data** contiene le righe di 20 variabili per 1000 clienti che in passato hanno fatto richiesta di un credito.</span><span class="sxs-lookup"><span data-stu-id="c6809-117">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="c6809-118">Queste 20 variabili rappresentano l'insieme di funzionalità del set di dati (*vettore delle funzionalità*) che fornisce le caratteristiche di identificazione di ogni richiedente credito.</span><span class="sxs-lookup"><span data-stu-id="c6809-118">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="c6809-119">Una colonna aggiuntiva in ogni riga rappresenta il rischio di credito calcolato del richiedente. In questa colonna 700 richiedenti sono identificati come a basso rischio e 300 ad alto rischio.</span><span class="sxs-lookup"><span data-stu-id="c6809-119">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="c6809-120">Il sito Web UCI presenta una descrizione degli attributi del vettore delle funzionalità per i dati.</span><span class="sxs-lookup"><span data-stu-id="c6809-120">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="c6809-121">Questo include informazioni finanziarie, storico dei crediti, stato di occupazione e dati personali.</span><span class="sxs-lookup"><span data-stu-id="c6809-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="c6809-122">Per ogni richiedente è stata assegnata una valutazione in formato binario per indicare se è a basso o ad alto rischio.</span><span class="sxs-lookup"><span data-stu-id="c6809-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="c6809-123">Questi dati verranno usati per creare un modello di analisi predittiva.</span><span class="sxs-lookup"><span data-stu-id="c6809-123">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="c6809-124">Dopo aver completato questa operazione, il modello dovrebbe essere in grado di accettare un vettore delle funzionalità per un nuovo cliente e prevedere se tale cliente è a basso o ad alto rischio.</span><span class="sxs-lookup"><span data-stu-id="c6809-124">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="c6809-125">Ma ecco un'interessante svolta.</span><span class="sxs-lookup"><span data-stu-id="c6809-125">Here's an interesting twist.</span></span> <span data-ttu-id="c6809-126">La descrizione del set di dati del sito Web di UCI include i possibili costi in caso di errata classificazione del rischio di credito di un utente.</span><span class="sxs-lookup"><span data-stu-id="c6809-126">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="c6809-127">Se il modello stima un elevato rischio di credito per un utente che è effettivamente a basso rischio, il modello ha eseguito una errata classificazione.</span><span class="sxs-lookup"><span data-stu-id="c6809-127">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="c6809-128">Tuttavia, la classificazione errata inversa è cinque volte più costosa per l'istituto finanziario, ovvero se il modello stima un basso rischio di credito per un utente che in realtà è a elevato rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="c6809-128">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="c6809-129">Pertanto, l'obiettivo è eseguire il training del modello in modo che il costo di quest'ultimo tipo di errata classificazione sia cinque volte superiore rispetto all'altro tipo di errata classificazione.</span><span class="sxs-lookup"><span data-stu-id="c6809-129">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="c6809-130">Un modo semplice per raggiungere questo obiettivo durante il training del modello nell'esperimento consiste nel duplicare (cinque volte) le voci che rappresentano un utente a elevato rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="c6809-130">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="c6809-131">Se il modello classifica un utente erroneamente a basso rischio quando è in realtà a rischio elevato, il modello ripete la stessa errata classificazione cinque volte, una volta per ogni duplicato.</span><span class="sxs-lookup"><span data-stu-id="c6809-131">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="c6809-132">e il costo di questo errore aumenterà nei risultati.</span><span class="sxs-lookup"><span data-stu-id="c6809-132">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="c6809-133">Convertire il formato del set di dati</span><span class="sxs-lookup"><span data-stu-id="c6809-133">Convert the dataset format</span></span>
<span data-ttu-id="c6809-134">Nel set di dati originale viene usato un formato con valori delimitati da spazi vuoti.</span><span class="sxs-lookup"><span data-stu-id="c6809-134">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="c6809-135">Per il funzionamento ottimale di Machine Learning Studio è preferibile usare un file con valori delimitati da virgole (CSV), di conseguenza il set di dati verrà convertito sostituendo gli spazi con le virgole.</span><span class="sxs-lookup"><span data-stu-id="c6809-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="c6809-136">Esistono diversi modi per convertire questi dati.</span><span class="sxs-lookup"><span data-stu-id="c6809-136">There are many ways to convert this data.</span></span> <span data-ttu-id="c6809-137">Un'opzione consiste nell'usare il comando di Windows PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c6809-137">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="c6809-138">Un'altra opzione consiste nell'usare il comando sed di Unix:</span><span class="sxs-lookup"><span data-stu-id="c6809-138">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="c6809-139">In entrambi i casi, è stata creata una versione delimitata da virgole dei dati del file **german.csv** che è possibile usare nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="c6809-139">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="c6809-140">Caricare il set di dati in Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="c6809-140">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="c6809-141">Dopo aver convertito i dati in formato CSV, è necessario caricarli in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c6809-141">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="c6809-142">Aprire la home page di Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="c6809-142">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="c6809-143">Fare clic sul menu ![Menu][1] nell'angolo superiore sinistro della finestra, fare clic su **Azure Machine Learning**, selezionare **Studio** ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="c6809-143">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="c6809-144">Fare clic su **+NEW** nella parte inferiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="c6809-144">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="c6809-145">Selezionare **DATASET**.</span><span class="sxs-lookup"><span data-stu-id="c6809-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="c6809-146">Selezionare **FROM LOCAL FILE**.</span><span class="sxs-lookup"><span data-stu-id="c6809-146">Select **FROM LOCAL FILE**.</span></span>

    ![Aggiungere un set di dati da un file locale][2]

6. <span data-ttu-id="c6809-148">Nella finestra di dialogo **Upload a new dataset** (Carica un nuovo set di dati) fare clic su **Browse** (Sfoglia) e individuare il file **german.csv** creato.</span><span class="sxs-lookup"><span data-stu-id="c6809-148">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="c6809-149">Immettere un nome per il set di dati.</span><span class="sxs-lookup"><span data-stu-id="c6809-149">Enter a name for the dataset.</span></span> <span data-ttu-id="c6809-150">Per questa procedura, il nome sarà "UCI German Credit Card Data".</span><span class="sxs-lookup"><span data-stu-id="c6809-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="c6809-151">Come tipo di dati selezionare **Generic CSV File With no header (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="c6809-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="c6809-152">Aggiungere un'eventuale descrizione.</span><span class="sxs-lookup"><span data-stu-id="c6809-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="c6809-153">Fare clic sul segno di spunta accanto a **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6809-153">Click the **OK** check mark.</span></span>  

    ![Caricare il set di dati][3]

<span data-ttu-id="c6809-155">I dati vengono caricati in un modulo del set di dati che è possibile usare in un esperimento.</span><span class="sxs-lookup"><span data-stu-id="c6809-155">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="c6809-156">È possibile gestire i set di dati caricati in Studio facendo clic su sulla scheda **DATASETS** a sinistra della finestra di Studio.</span><span class="sxs-lookup"><span data-stu-id="c6809-156">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![Gestire i set di dati][4]

<span data-ttu-id="c6809-158">Per altre informazioni sull'importazione di altri tipi di dati in un esperimento, vedere [Importare dati di training in Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="c6809-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="c6809-159">**Passaggi successivi: [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="c6809-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
