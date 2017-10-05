---
title: 'Passaggio 4: Eseguire il training e valutare i modelli analitici predittivi | Microsoft Docs'
description: "Passaggio 4 della procedura dettagliata Sviluppare una soluzione predittiva: Eseguire il training, classificare e valutare più modelli in Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="81018-103">Passaggio 4 della procedura dettagliata: Eseguire il training e valutare i modelli analitici predittivi</span><span class="sxs-lookup"><span data-stu-id="81018-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="81018-104">Questo argomento contiene il quarto passaggio della procedura dettagliata [Sviluppare una soluzione di analisi predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="81018-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="81018-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="81018-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="81018-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="81018-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="81018-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="81018-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="81018-108">**Eseguire il training e valutare i modelli**</span><span class="sxs-lookup"><span data-stu-id="81018-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="81018-109">Distribuire il servizio Web</span><span class="sxs-lookup"><span data-stu-id="81018-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="81018-110">Accedere al servizio Web</span><span class="sxs-lookup"><span data-stu-id="81018-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="81018-111">Uno dei vantaggi che offre Azure Machine Learning Studio per la creazione di modelli di Machine Learning è la possibilità di valutare più tipi di modelli contemporaneamente in un singolo esperimento e confrontare i risultati.</span><span class="sxs-lookup"><span data-stu-id="81018-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="81018-112">Questo tipo di esperimento consente di trovare la soluzione migliore per il problema che si desidera risolvere.</span><span class="sxs-lookup"><span data-stu-id="81018-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="81018-113">Nell'esperimento sviluppato in questa procedura guidata verranno creati due tipi diversi di modello, quindi ne verranno confrontati i punteggi risultanti per decidere quale algoritmo usare nell'esperimento finale.</span><span class="sxs-lookup"><span data-stu-id="81018-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="81018-114">Sono disponibili diversi modelli tra cui scegliere.</span><span class="sxs-lookup"><span data-stu-id="81018-114">There are various models we could choose from.</span></span> <span data-ttu-id="81018-115">Per visualizzare i modelli disponibili, espandere il nodo **Machine Learning** nella tavolozza dei moduli, espandere **Initialize Model** (Inizializza modello) e quindi i nodi al suo interno.</span><span class="sxs-lookup"><span data-stu-id="81018-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="81018-116">Ai fini di questo esperimento, verranno selezionati i moduli [Two-Class Support Vector Machine (SVM)][two-class-support-vector-machine] (Macchina a vettori di supporto a due classi) e [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Albero delle decisioni con boosting a due classi).</span><span class="sxs-lookup"><span data-stu-id="81018-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="81018-117">Per ottenere informazioni circa quale algoritmo di Machine Learning sia più adatto per un problema specifico che si sta tentando di risolvere, vedere [Come scegliere gli algoritmi di Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="81018-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="81018-118">Eseguire il training dei modelli</span><span class="sxs-lookup"><span data-stu-id="81018-118">Train the models</span></span>

<span data-ttu-id="81018-119">In questo esperimento, saranno aggiunti il modulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Albero delle decisioni con boosting a due classi) e il modulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Macchina a vettori di supporto a due classi).</span><span class="sxs-lookup"><span data-stu-id="81018-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="81018-120">Two-Class Boosted Decision Tree</span><span class="sxs-lookup"><span data-stu-id="81018-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="81018-121">Prima di tutto verrà configurato il modello di albero delle decisioni con boosting.</span><span class="sxs-lookup"><span data-stu-id="81018-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="81018-122">Trovare il modulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Albero delle decisioni con boosting a due classi) nella tavolozza dei moduli e trascinarlo nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="81018-123">Trovare il modulo [Train Model][train-model] (Training modello), trascinarlo nell'area di disegno, quindi connettere l'output del modulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Albero delle decisioni con boosting a due classi) alla porta di input sinistra del modulo [Train Model][train-model] (Training modello).</span><span class="sxs-lookup"><span data-stu-id="81018-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="81018-124">Il modulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Albero delle decisioni con boosting a due classi) inizializza il modello generico e [Train Model][train-model] (Training modello) usa i dati di training per il training del modello.</span><span class="sxs-lookup"><span data-stu-id="81018-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="81018-125">Connettere l'output del modulo [Execute R Script][execute-r-script] (Esegui script R) a sinistra alla porta di input destra del modulo [Train Model][train-model] (Training modello). Nel [Passo 3](machine-learning-walkthrough-3-create-new-experiment.md) di questa procedura dettagliata è stato deciso di utilizzare i dati riportati a sinistra del modulo Split Data (Divisione dati) per il training.</span><span class="sxs-lookup"><span data-stu-id="81018-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="81018-126">Due degli input e uno degli output del modulo [Execute R Script][execute-r-script] (Esegui script R) non sono necessari per questo esperimento, pertanto potranno rimanere scollegati.</span><span class="sxs-lookup"><span data-stu-id="81018-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="81018-127">Questa parte dell'esperimento avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="81018-127">This portion of the experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="81018-129">A questo punto è necessario indicare il modulo [Train Model] [ train-model] (Training modello) per cui il modello deve stimare il valore di rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="81018-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="81018-130">Selezionare il modulo [Train Model][train-model] (Training modello).</span><span class="sxs-lookup"><span data-stu-id="81018-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="81018-131">Nel riquadro **Proprietà**, fare clic su **Launch column selector** (Avvia selettore colonne).</span><span class="sxs-lookup"><span data-stu-id="81018-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="81018-132">Nella finestra di dialogo **Select a single column** (Selezionare una singola colonna), digitare "rischio di credito" nel campo di ricerca in **Colonne disponibili**, selezionare "Rischio di credito" di seguito e fare clic sul pulsante freccia destra (**>**) per spostare "Rischio di credito" su **Colonne selezionate**.</span><span class="sxs-lookup"><span data-stu-id="81018-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Selezionare la colonna Rischio di credito per il modulo "Train Model" (Training modello)][0]

3. <span data-ttu-id="81018-134">Fare clic sul segno di spunta accanto a **OK**.</span><span class="sxs-lookup"><span data-stu-id="81018-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="81018-135">Two-Class Support Vector Machine</span><span class="sxs-lookup"><span data-stu-id="81018-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="81018-136">È quindi possibile configurare il modello di macchina a vettori di supporto (SVM).</span><span class="sxs-lookup"><span data-stu-id="81018-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="81018-137">Innanzitutto, una breve spiegazione di SVM.</span><span class="sxs-lookup"><span data-stu-id="81018-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="81018-138">Gli alberi delle decisioni con boosting funzionano bene con qualsiasi tipo di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="81018-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="81018-139">Poiché tuttavia il modulo di macchina a vettori di supporto genera un classificatore lineare, il modello che genera ha l'errore di test migliore quando gli elementi numerici hanno la stessa scala.</span><span class="sxs-lookup"><span data-stu-id="81018-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="81018-140">Per convertire tutte le funzioni numeriche nella stessa scala, viene usata una trasformazione "Tanh", con il modulo [Normalize Data][normalize-data] (Normalizza dati).</span><span class="sxs-lookup"><span data-stu-id="81018-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="81018-141">In questo modo, vengono trasformati i numeri nell'intervallo [0,1].</span><span class="sxs-lookup"><span data-stu-id="81018-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="81018-142">I modulo SVM converte gli elementi stringa in elementi di categoria e quindi in elementi 0/1 binari, pertanto non è necessario trasformare manualmente gli elementi stringa.</span><span class="sxs-lookup"><span data-stu-id="81018-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="81018-143">Non si deve inoltre trasformare la colonna Credit Risk (colonna 21): si tratta di un valore numerico, ma è anche il valore per il quale il modulo deve eseguire la previsione dopo il training e non dovrà pertanto essere alterato.</span><span class="sxs-lookup"><span data-stu-id="81018-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="81018-144">Per configurare il modello SVM, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="81018-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="81018-145">Trovare il modulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Macchina a vettori di supporto a due classi) nella tavolozza dei moduli e trascinarlo nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="81018-146">Fare clic con il pulsante destro del mouse sul modulo [Train Model][train-model] (Training modello), scegliere **Copia**, quindi fare clic con il pulsante destro del mouse sull'area di disegno e scegliere **Incolla**.</span><span class="sxs-lookup"><span data-stu-id="81018-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="81018-147">La copia del modulo [Train Model][train-model] (Training modello) presenta la stessa selezione di colonne dell'originale.</span><span class="sxs-lookup"><span data-stu-id="81018-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="81018-148">Connettere l'output del modulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Macchina a vettori di supporto a due classi) alla porta di input sinistra del secondo modulo [Train Model][train-model] (Training modello).</span><span class="sxs-lookup"><span data-stu-id="81018-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="81018-149">Trovare il modulo [Normalize Data][normalize-data] (Normalizza dati) e trascinarlo nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="81018-150">Connettere l'output sinistro del modulo [Execute R Script][execute-r-script] (Esegui script R) sinistro all'input di questo modulo (si noti che la porta di output di un modulo potrebbe essere connessa a più di un modulo).</span><span class="sxs-lookup"><span data-stu-id="81018-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="81018-151">Connettere la porta di output sinistra del modulo [Normalize Data][normalize-data] (Normalizza dati) alla porta di input destra del secondo modulo [Train Model][train-model] (Training modello).</span><span class="sxs-lookup"><span data-stu-id="81018-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="81018-152">Questa parte dell'esperimento avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="81018-152">This portion of our experiment should now look something like this:</span></span>  

![Training the second model][2]  

<span data-ttu-id="81018-154">Ora configurare il modulo [Normalize Data][normalize-data] (Normalizza dati):</span><span class="sxs-lookup"><span data-stu-id="81018-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="81018-155">Fare clic per selezionare il modulo [Normalize Data][normalize-data] (Normalizza dati).</span><span class="sxs-lookup"><span data-stu-id="81018-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="81018-156">Nel riquadro **Proprietà** relativo al modulo di trasformazione scegliere **Tanh** per il parametro **Transformation method** (Metodo di trasformazione).</span><span class="sxs-lookup"><span data-stu-id="81018-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="81018-157">Fare clic su **Launch column selector** (Avvia selettore di colonna), selezionare "No columns" (Nessuna colonna) per **Begin With** (Inizia con), selezionare **Include** (Includi) nel primo elenco a discesa, selezionare **column type** (tipo di colonna) nel secondo elenco a discesa e infine selezionare **Numeric** (Numerico) nel terzo elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="81018-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="81018-158">Questo specifica che verranno trasformate tutte le colonne numeriche, ma solo quelle di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="81018-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="81018-159">Fare clic sul segno più (+) a destra di questa riga per creare una nuova riga di elenchi a discesa.</span><span class="sxs-lookup"><span data-stu-id="81018-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="81018-160">Selezionare **Escludi** nel primo elenco a discesa, selezionare **column names** (nomi colonna) nel secondo elenco a discesa e immettere "Rischio di credito" nel campo di testo.</span><span class="sxs-lookup"><span data-stu-id="81018-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="81018-161">Questa impostazione specifica che la colonna Rischi di credito deve essere ignorata (è necessario farlo perché la colonna è numerica e pertanto, se non esclusa, verrebbe trasformata).</span><span class="sxs-lookup"><span data-stu-id="81018-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="81018-162">Fare clic sul segno di spunta accanto a **OK**.</span><span class="sxs-lookup"><span data-stu-id="81018-162">Click the **OK** check mark.</span></span>  

    ![Selezionare le colonne per il modulo Normalize Data (Normalizza dati)][5]

<span data-ttu-id="81018-164">Il modulo [Normalize Data][normalize-data] (Normalizza dati) è ora impostato per eseguire una trasformazione tanh su tutte le colonne numeriche, a eccezione della colonna Rischi di credito.</span><span class="sxs-lookup"><span data-stu-id="81018-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="81018-165">Classificare e valutare i modelli</span><span class="sxs-lookup"><span data-stu-id="81018-165">Score and evaluate the models</span></span>

<span data-ttu-id="81018-166">Verranno usati i dati di test separati dal modulo [Split Data][split] (Divisione dati) per assegnare il punteggio ai moduli oggetto del training.</span><span class="sxs-lookup"><span data-stu-id="81018-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="81018-167">Sarà quindi possibile confrontare i risultati dei due modelli per stabilire quale ha generato i risultati migliori.</span><span class="sxs-lookup"><span data-stu-id="81018-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="81018-168">Aggiungere i moduli Score Model (Punteggio modello)</span><span class="sxs-lookup"><span data-stu-id="81018-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="81018-169">Trovare il modulo [Score Model][score-model] (Punteggio modello) e trascinarlo nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="81018-170">Connettere il modulo [Train Model][train-model] (Training modello) connesso al modulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Albero delle decisioni con boosting a due classi) alla porta di input sinistra del modulo [Score Model][score-model] (Punteggio modello).</span><span class="sxs-lookup"><span data-stu-id="81018-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="81018-171">Connettere il modulo [Execute R Script][execute-r-script] (Esegui script R) alla porta di input destra del modulo [Score Model][score-model] (Punteggio modello).</span><span class="sxs-lookup"><span data-stu-id="81018-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Modulo Score Model (Punteggio modello) connesso][6]
   
   <span data-ttu-id="81018-173">Il modulo [Score Model][score-model] (Punteggio modello) può ora prelevare le informazioni sul credito dai dati di test, eseguirle tramite il modello e confrontare le previsioni generate dal modello con la colonna relativa al rischio di credito dei dati di test.</span><span class="sxs-lookup"><span data-stu-id="81018-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="81018-174">Copiare e incollare il modulo [Score Model][score-model] (Punteggio modello) per creare una seconda copia.</span><span class="sxs-lookup"><span data-stu-id="81018-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="81018-175">Connettere l'output del modello SVM (vale a dire la porta di output del modulo [Train Model][train-model] (Training modello) connessa al modulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Macchina a vettori di supporto a due classi) alla porta di input del secondo modulo [Score Model][score-model] (Punteggio modello).</span><span class="sxs-lookup"><span data-stu-id="81018-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="81018-176">Per il modello SVM, è necessario eseguire la stessa trasformazione sui dati di test eseguita in precedenza sui dati di training.</span><span class="sxs-lookup"><span data-stu-id="81018-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="81018-177">Pertanto, copiare e incollare il modulo [Normalize Data][normalize-data] (Normalizza dati) per creare una seconda copia e connetterla al modulo [Execute R Script][execute-r-script] (Esegui script R).</span><span class="sxs-lookup"><span data-stu-id="81018-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="81018-178">Connettere l'output sinistra del secondo modulo [Normalize Data][normalize-data] (Normalizza dati) alla porta di input destra del secondo modulo [Score Model][score-model] (Punteggio modello).</span><span class="sxs-lookup"><span data-stu-id="81018-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Entrambi i moduli Score Model (Punteggio modello) connessi][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="81018-180">Aggiungere il modulo Evaluate Model (Modello di valutazione)</span><span class="sxs-lookup"><span data-stu-id="81018-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="81018-181">Per valutare i due risultati di punteggio e confrontarli, viene usato il modulo [Evaluate Model][evaluate-model] (Modello di valutazione).</span><span class="sxs-lookup"><span data-stu-id="81018-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="81018-182">Trovare il modulo [Evaluate Model][evaluate-model] (Modello di valutazione) e trascinarlo nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="81018-183">Connettere la porta di output del modulo [Score Model][score-model] (Punteggio modello) associata al modello di albero delle decisioni con boosting alla porta di input sinistra del modulo [Evaluate Model][evaluate-model] (Modello di valutazione).</span><span class="sxs-lookup"><span data-stu-id="81018-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="81018-184">Connettere l'altro modulo [Score Model][score-model] (Punteggio modello) alla porta di input destra.</span><span class="sxs-lookup"><span data-stu-id="81018-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Modulo Evaluate Model (Modello di valutazione) connesso][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="81018-186">Eseguire l'esperimento e controllare i risultati</span><span class="sxs-lookup"><span data-stu-id="81018-186">Run the experiment and check the results</span></span>

<span data-ttu-id="81018-187">Per eseguire l'esperimento, fare clic sul pulsante **RUN** (ESEGUI) sotto l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="81018-188">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="81018-188">It may take a few minutes.</span></span> <span data-ttu-id="81018-189">Su ogni modulo verrà visualizzato un indicatore rotante per indicare che il modulo è in esecuzione, quindi apparirà un segno di spunta verde al termine dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="81018-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="81018-190">Quando tutti i moduli presentano il segno di spunta, l'esecuzione dell'esperimento sarà completa.</span><span class="sxs-lookup"><span data-stu-id="81018-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="81018-191">L'esperimento avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="81018-191">The experiment should now look something like this:</span></span>  

![Valutazione di entrambi i modelli][3]

<span data-ttu-id="81018-193">Per verificare i risultati, fare clic sulla porta di output del modulo [Evaluate Model][evaluate-model] (Modello di valutazione) e selezionare **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="81018-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="81018-194">Il modulo [Evaluate Model][evaluate-model] (Modello di valutazione) produce un paio di curve e metriche che consentono di confrontare i risultati dei due modelli classificati.</span><span class="sxs-lookup"><span data-stu-id="81018-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="81018-195">È possibile visualizzare i risultati come curve ROC (Receiver Operator Characteristic), curve precisione/recupero o curve di accuratezza.</span><span class="sxs-lookup"><span data-stu-id="81018-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="81018-196">Altri dati visualizzati includono una matrice di confusione, valori cumulativi per l'area nella curva (AUC) e altra metrica.</span><span class="sxs-lookup"><span data-stu-id="81018-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="81018-197">È possibile modificare il valore soglia spostando il dispositivo di scorrimento a sinistra o a destra e vedere come ciò influisce sul set della metrica.</span><span class="sxs-lookup"><span data-stu-id="81018-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="81018-198">A destra del grafico fare clic su **Scored dataset** (Set di dati con punteggio) o **Scored dataset to compare** (Set di dati con punteggio da confrontare) per evidenziare la curva associata e visualizzare le metriche associate più sotto.</span><span class="sxs-lookup"><span data-stu-id="81018-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="81018-199">Nella legenda per le curve, "Scored dataset" (Set di dati con punteggio) corrisponde alla porta di input sinistra del modulo [Evaluate Model][evaluate-model] (Modello di valutazione). In questo caso si tratta del modello di albero delle decisioni con boosting.</span><span class="sxs-lookup"><span data-stu-id="81018-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="81018-200">"Scored dataset to compare" corrisponde alla porta di input destra, in questo caso il modello di macchina a vettori di supporto.</span><span class="sxs-lookup"><span data-stu-id="81018-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="81018-201">Quando si fa clic su una di queste etichette, viene evidenziata la curva per il modello e viene visualizzata la metrica corrispondente, come mostrato dalla grafica seguente.</span><span class="sxs-lookup"><span data-stu-id="81018-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="81018-203">Esaminando questi valori, è possibile decidere quale sia il modello che più si avvicina ai risultati previsti.</span><span class="sxs-lookup"><span data-stu-id="81018-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="81018-204">È possibile tornare indietro ed eseguire l'iterazione dell'esperimento modificando i valori di parametro dei vari modelli.</span><span class="sxs-lookup"><span data-stu-id="81018-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="81018-205">La scienza e l'arte di interpretare questi risultati e di ottimizzare le prestazioni del modello non rientrano nell'ambito di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="81018-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="81018-206">Per ulteriori informazioni, è possibile leggere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="81018-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="81018-207">Come valutare le prestazioni del modello in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="81018-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="81018-208">Scegliere i parametri per ottimizzare gli algoritmi in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="81018-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="81018-209">Interpretare i risultati dei modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="81018-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="81018-210">Ogni volta che si esegue l'esperimento, viene conservato un record dell'iterazione nella cronologia di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="81018-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="81018-211">È possibile visualizzare le iterazioni e tornare a una qualsiasi di esse facendo clic su **VISUALIZZA CRONOLOGIA ESECUZIONI** sotto l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="81018-212">È anche possibile fare clic su **Prior Run** (Esecuzione precedente) nel riquadro **Properties** (Proprietà) per tornare all'iterazione immediatamente precedente a quella aperta.</span><span class="sxs-lookup"><span data-stu-id="81018-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="81018-213">È possibile eseguire una copia di qualsiasi interazione dell'esperimento facendo clic su **SALVA CON NOME** sotto l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="81018-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="81018-214">Usare le proprietà **Summary** (Riepilogo) e **Description** (Descrizione) dell'esperimento per tenere traccia dei tentativi eseguiti nelle iterazioni dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="81018-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="81018-215">Per altre informazioni, vedere [Gestire iterazioni dell'esperimento in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="81018-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="81018-216">**Passaggio successivo: [Distribuire il servizio Web](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="81018-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
