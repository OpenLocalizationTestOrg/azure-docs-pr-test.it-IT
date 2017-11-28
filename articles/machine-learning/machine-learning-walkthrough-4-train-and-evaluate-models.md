---
title: 'Passaggio 4: Eseguire il training e valutare i modelli di analisi predittiva hello | Documenti Microsoft'
description: "Passaggio 4 di hello sviluppare una procedura dettagliata soluzione predittiva: treno, assegnare un punteggio e valutare più modelli in Azure Machine Learning Studio."
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
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="bd2ac-103">Procedura dettagliata passaggio 4: Eseguire il training e valutare i modelli di analisi predittiva hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="bd2ac-104">In questo argomento contiene quarto passaggio di hello della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="bd2ac-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="bd2ac-105">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bd2ac-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="bd2ac-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="bd2ac-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="bd2ac-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="bd2ac-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="bd2ac-108">**Eseguire il training e valutare i modelli di hello**</span><span class="sxs-lookup"><span data-stu-id="bd2ac-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="bd2ac-109">Distribuzione di servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="bd2ac-110">Accedere al servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="bd2ac-111">Uno dei vantaggi di hello dell'utilizzo di Azure Machine Learning Studio per la creazione di modelli di machine learning è hello possibilità tootry più di un tipo di modello alla volta in un esperimento singolo e confrontare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="bd2ac-112">Questo tipo di sperimentazione consente di trovare la soluzione migliore hello per il problema.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="bd2ac-113">Nell'esperimento di hello è in corso di sviluppo in questa procedura dettagliata viene creare due tipi diversi di modelli e quindi confrontare i relativi toodecide risultati punteggio quale algoritmo desideriamo toouse nell'esperimento finale.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="bd2ac-114">Sono disponibili diversi modelli tra cui scegliere.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-114">There are various models we could choose from.</span></span> <span data-ttu-id="bd2ac-115">modelli hello toosee disponibili, espandere hello **Machine Learning** nodo tavolozza modulo hello, quindi espandere **inizializzare modello** e hello nodi sottostanti.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="bd2ac-116">Ai fini di hello di questo esperimento, si selezionerà hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] (SVM) e hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] moduli.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="bd2ac-117">Guida tooget decidere quale algoritmo di Machine Learning meglio si adatta alle particolare problema hello che stai tentando toosolve, vedere [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="bd2ac-118">Eseguire il training di modelli di hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-118">Train hello models</span></span>

<span data-ttu-id="bd2ac-119">Verranno aggiunti entrambi hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modulo e [Two-Class Support Vector Machine] [ two-class-support-vector-machine] questo modulo esperimento.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="bd2ac-120">Two-Class Boosted Decision Tree</span><span class="sxs-lookup"><span data-stu-id="bd2ac-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="bd2ac-121">In primo luogo, impostazione modello di albero delle decisioni con Boosting hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="bd2ac-122">Trovare hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modulo tavolozza modulo hello e trascinarlo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="bd2ac-123">Trovare hello [Train Model] [ train-model] modulo, trascinarlo nell'area di disegno hello e quindi connettere l'output di hello di hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree]toohello modulo lasciato porta di input di hello [Train Model] [ train-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="bd2ac-124">Hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modulo Inizializza modello generico di hello e [Train Model] [ train-model] utilizza i dati di training modello di hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="bd2ac-125">Connettere hello output a sinistra di sinistra hello [Execute R Script] [ execute-r-script] porta di hello di input di destra toohello modulo [Train Model] [ train-model] modulo (è ha deciso [passaggio 3](machine-learning-walkthrough-3-create-new-experiment.md) di questa procedura dettagliata toouse hello i dati provenienti dal lato sinistro di modulo di hello suddivisione dei dati per il training hello).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bd2ac-126">Non sono necessarie due input hello e uno di output di hello di hello [Execute R Script] [ execute-r-script] modulo per questo esercizio, pertanto è possibile lasciarli scollegato.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="bd2ac-127">Questa parte dell'esperimento hello sarà ora simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="bd2ac-127">This portion of hello experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="bd2ac-129">Ora è necessario tootell hello [Train Model] [ train-model] modulo che si desidera valore del rischio di credito hello toopredict modello hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="bd2ac-130">Seleziona hello [Train Model] [ train-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="bd2ac-131">In hello **proprietà** riquadro, fare clic su **selettore di colonna avvio**.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="bd2ac-132">In hello **selezionare una singola colonna** finestra di dialogo, digitare "rischio di credito" nel campo di ricerca hello in **colonne disponibili**, selezionare "Rischio di credito" di seguito e fare clic sul pulsante freccia destra hello ( **>** ) toomove "Credito rischio" troppo**colonne selezionate**.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Selezionare la colonna di rischio di credito hello per modulo Train Model hello][0]

3. <span data-ttu-id="bd2ac-134">Fare clic su hello **OK** segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="bd2ac-135">Two-Class Support Vector Machine</span><span class="sxs-lookup"><span data-stu-id="bd2ac-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="bd2ac-136">Successivamente, è necessario impostare modello SVM hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="bd2ac-137">Innanzitutto, una breve spiegazione di SVM.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="bd2ac-138">Gli alberi delle decisioni con boosting funzionano bene con qualsiasi tipo di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="bd2ac-139">Tuttavia, poiché il modulo SVM hello genera un classificatore lineare, modello hello che genera errore hello migliore test quando dispongono di tutte le funzionalità numeriche hello stessa scala.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="bd2ac-140">tooconvert numerico tutte le funzionalità toohello stessa scala, si utilizza una trasformazione "Tanh" (con hello [Normalize Data] [ normalize-data] modulo).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="bd2ac-141">Ciò consente di trasformare i numeri nell'intervallo [0,1] hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="bd2ac-142">modulo SVM Hello converte in stringa funzionalità toocategorical funzionalità e quindi toobinary 0/1, in modo non è necessario toomanually trasformare le funzionalità di stringa.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="bd2ac-143">Inoltre, non vogliamo tootransform hello rischio di credito colonna (colonna 21): è numerico, ma è il valore di hello ci stiamo training hello toopredict modello, pertanto è necessario tooleave è da solo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="bd2ac-144">hello tooset modello SVM hello, di seguito:</span><span class="sxs-lookup"><span data-stu-id="bd2ac-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="bd2ac-145">Trovare hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] modulo tavolozza modulo hello e trascinarlo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="bd2ac-146">Pulsante destro del mouse hello [Train Model] [ train-model] modulo, seleziona **copia**, quindi fare doppio clic su area di disegno hello e selezionare **Incolla**.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="bd2ac-147">copia di hello Hello [Train Model] [ train-model] del modulo è hello stesso selezione della colonna come hello originale.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="bd2ac-148">Connettere l'output di hello di hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] toohello modulo lasciato porta di input di hello secondo [Train Model] [ train-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="bd2ac-149">Trovare hello [Normalize Data] [ normalize-data] modulo e trascinarlo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="bd2ac-150">Connettere hello output a sinistra di sinistra hello [Execute R Script] [ execute-r-script] input toohello modulo di questo modulo (si noti che la porta di output di hello di un modulo può essere connesso toomore rispetto a un altro modulo).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="bd2ac-151">Connettersi a sinistra sulla porta di output di hello hello [Normalize Data] [ normalize-data] toohello modulo destra input porta hello secondo [Train Model] [ train-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="bd2ac-152">Questa parte dell'esperimento avrà ora un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="bd2ac-152">This portion of our experiment should now look something like this:</span></span>  

![Training del modello di secondo hello][2]  

<span data-ttu-id="bd2ac-154">Configurare ora hello [Normalize Data] [ normalize-data] modulo:</span><span class="sxs-lookup"><span data-stu-id="bd2ac-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="bd2ac-155">Fare clic su hello tooselect [Normalize Data] [ normalize-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="bd2ac-156">In hello **proprietà** riquadro, selezionare **Tanh** per hello **Transformation method** parametro.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="bd2ac-157">Fare clic su **selettore di colonna avvio**, non selezionare "Nessuna columns" per **iniziano con**selezionare **Include** hello prima dall'elenco a discesa, selezionare **il tipo di colonna**in hello secondo elenco a discesa e selezionare **numerico** nell'elenco a discesa terzo hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="bd2ac-158">Specifica che vengono trasformati tutti hello colonne numeriche (e solo numerico).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="bd2ac-159">Fare clic sul segno più (+) toohello a destra di questa riga hello: verrà creata una riga di menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="bd2ac-160">Selezionare **escludere** hello prima dall'elenco a discesa, selezionare **i nomi di colonna** in hello secondo elenco a discesa, quindi immettere "Credito di rischio" nel campo di testo hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="bd2ac-161">Specifica la colonna di rischio di credito hello deve essere ignorata (dobbiamo toodo questo perché la colonna è numerica e pertanto viene trasformato se è non è stata esclusa).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="bd2ac-162">Fare clic su hello **OK** segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-162">Click hello **OK** check mark.</span></span>  

    ![Selezionare le colonne per il modulo di hello Normalize Data][5]

<span data-ttu-id="bd2ac-164">Hello [Normalize Data] [ normalize-data] modulo viene ora set tooperform una trasformazione Tanh in tutte le colonne numeriche, ad eccezione di colonna di hello rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="bd2ac-165">Assegnare un punteggio e valutare i modelli di hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-165">Score and evaluate hello models</span></span>

<span data-ttu-id="bd2ac-166">Utilizziamo hello verifica dei dati che è stati separati da hello [dati divisi] [ split] tooscore modulo nostri modelli con training.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="bd2ac-167">È quindi possibile confrontare i risultati di hello di hello due modelli toosee che ha generato i risultati migliori.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="bd2ac-168">Aggiungere moduli Score Model hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="bd2ac-169">Trovare hello [Score Model] [ score-model] modulo e trascinarlo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="bd2ac-170">Connettersi hello [Train Model] [ train-model] modulo che è connesso toohello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] input di sinistra toohello modulo porta di hello [Score Model] [ score-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="bd2ac-171">Connettersi a destra di hello [Execute R Script] [ execute-r-script] toohello modulo (i dati di test) a destra di input porta hello [Score Model] [ score-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Modulo Score Model (Punteggio modello) connesso][6]
   
   <span data-ttu-id="bd2ac-173">Hello [Score Model] [ score-model] modulo può richiedere ora le informazioni sul credito hello dalla verifica dei dati, eseguirlo tramite il modello di hello, hello e confrontare le stime di hello hello modello genera con hello effettivo rischio di credito colonna in dati di testing hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="bd2ac-174">Copiare e incollare hello [Score Model] [ score-model] toocreate modulo una seconda copia.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="bd2ac-175">Connettere l'output di hello del modello SVM hello (vale a dire, porta di hello di output hello [Train Model] [ train-model] modulo che è connesso toohello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] modulo) toohello input hello porta in secondo luogo [Score Model] [ score-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="bd2ac-176">Per il modello SVM hello abbiamo toodo hello stessi dati di test toohello trasformazione come è stato fatto toohello dati di training.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="bd2ac-177">Pertanto, copiare e incollare hello [Normalize Data] [ normalize-data] toocreate modulo una seconda copia e connetterla destra toohello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="bd2ac-178">La connessione di output a sinistra di hello di hello secondo [Normalize Data] [ normalize-data] toohello modulo destra input porta hello secondo [Score Model] [ score-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Entrambi i moduli Score Model (Punteggio modello) connessi][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="bd2ac-180">Aggiungi modulo Evaluate Model hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="bd2ac-181">tooevaluate hello due risultati del punteggio e confrontarli, utilizziamo un [Evaluate Model] [ evaluate-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="bd2ac-182">Trovare hello [Evaluate Model] [ evaluate-model] modulo e trascinarlo nell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="bd2ac-183">Connettere hello porta di output di hello [Score Model] [ score-model] associato hello modulo boosted decision toohello modello di struttura ad albero a sinistra di input porta hello [Evaluate Model] [ evaluate-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="bd2ac-184">Connettersi hello altri [Score Model] [ score-model] porta di input di destra toohello modulo.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Modulo Evaluate Model (Modello di valutazione) connesso][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="bd2ac-186">Eseguire l'esperimento hello e controllare i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="bd2ac-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="bd2ac-187">toorun hello esperimento, fare clic su hello **eseguire** pulsante sotto l'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="bd2ac-188">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-188">It may take a few minutes.</span></span> <span data-ttu-id="bd2ac-189">Un indicatore rotante in ogni modulo viene illustrato che è in esecuzione e quindi un segno di spunta verde viene visualizzata al termine modulo hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="bd2ac-190">Quando tutti i moduli di hello dispongono di un segno di spunta, esperimento hello è terminata.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="bd2ac-191">sperimentazione Hello dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="bd2ac-191">hello experiment should now look something like this:</span></span>  

![Valutazione di entrambi i modelli][3]

<span data-ttu-id="bd2ac-193">risultati di hello toocheck, fare clic su hello porta di output di hello [Evaluate Model] [ evaluate-model] modulo e selezionare **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="bd2ac-194">Hello [Evaluate Model] [ evaluate-model] modulo produce una coppia di curve e le metriche che consentono di risultati di hello toocompare di due modelli con punteggio di hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="bd2ac-195">È possibile visualizzare i risultati di hello come curve di accuratezza, precisione/richiamo curve o curve ricevitore operatore caratteristica (ROC).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="bd2ac-196">Dati aggiuntivi visualizzati includono una matrice di confusione, valori cumulativi per area hello sotto la curva hello (AUC) e altre metriche.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="bd2ac-197">È possibile modificare il valore di soglia hello mobile hello il dispositivo di scorrimento sinistro o destro e osservare gli effetti set hello di metriche.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="bd2ac-198">toohello destra del grafico hello, fare clic su **Scored dataset** o **Scored dataset toocompare** toohighlight hello associato curva e toodisplay hello associata metriche riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="bd2ac-199">Nella legenda hello per le curve hello, "Set di dati di punteggio" corrisponde a sinistra sulla porta di input di hello toohello [Evaluate Model] [ evaluate-model] modulo - in questo caso, si tratta di modello di albero delle decisioni con Boosting hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="bd2ac-200">"Scored dataset toocompare" corrisponde toohello destra porta di input - modello SVM hello in questo caso.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="bd2ac-201">Quando si fa clic su una delle etichette, curva hello per tale modello è evidenziata e vengono visualizzate le metriche corrispondente hello, come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="bd2ac-203">Esaminando questi valori, è possibile decidere quale sia il modello toogiving più vicino che Hello risultati che si sta cercando.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="bd2ac-204">È possibile tornare indietro e scorrere l'esperimento modificando i valori dei parametri in modelli diversi di hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="bd2ac-205">Scienza Hello ed elementi grafici di interpretare i risultati e ottimizzazione delle prestazioni del modello hello è di fuori ambito hello di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="bd2ac-206">Per ulteriori informazioni, si potrebbe leggere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="bd2ac-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="bd2ac-207">Come tooevaluate modello delle prestazioni in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bd2ac-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="bd2ac-208">Scegliere i parametri toooptimize algoritmi in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bd2ac-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="bd2ac-209">Interpretare i risultati dei modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bd2ac-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="bd2ac-210">Ogni volta che si esegue l'esperimento hello un record di tale iterazione viene mantenuta nella cronologia di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="bd2ac-211">È possibile visualizzare queste iterazioni e restituire tooany di essi, facendo clic su **Visualizza cronologia di esecuzione** sotto l'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="bd2ac-212">È anche possibile fare clic su **eseguire precedente** in hello **proprietà** iterazione di toohello tooreturn riquadro immediatamente precedente hello uno è aperta.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="bd2ac-213">È possibile creare una copia di qualsiasi iterazione dell'esperimento facendo **SAVE AS** sotto l'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="bd2ac-214">Utilizzo dell'esperimento hello **riepilogo** e **descrizione** proprietà tookeep un record di ciò che si è tentato nelle iterazioni esperimento.</span><span class="sxs-lookup"><span data-stu-id="bd2ac-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="bd2ac-215">Per altre informazioni, vedere [Gestire iterazioni dell'esperimento in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="bd2ac-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="bd2ac-216">**Passaggio successivo: [distribuire hello web servizio](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="bd2ac-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
