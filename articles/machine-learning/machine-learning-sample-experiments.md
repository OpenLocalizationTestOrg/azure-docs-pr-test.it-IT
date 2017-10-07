---
title: aaaCopy machine learning esperimenti di esempio - Azure | Documenti Microsoft
description: Informazioni su come l'apprendimento esempio toouse esperimenti toocreate nuovi esperimenti con Cortana Intelligence Gallery e Microsoft Azure Machine Learning.
keywords: esperimenti di esempio di Machine Learning, esperimento di esempio, esempio di Machine Learning
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 555f05cf9af2040d1703707f7583396d5da9f156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-example-experiments-toocreate-new-machine-learning-experiments"></a><span data-ttu-id="2cb7a-104">Copiare l'esempio esperimenti toocreate nuova macchina negli esperimenti di apprendimento</span><span class="sxs-lookup"><span data-stu-id="2cb7a-104">Copy example experiments toocreate new machine learning experiments</span></span>
<span data-ttu-id="2cb7a-105">Informazioni su come toostart con esempio esperimenti da [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) anziché creare esperimenti di machine learning da zero.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-105">Learn how toostart with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="2cb7a-106">È possibile utilizzare hello esempi toobuild computer apprendimento soluzione.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-106">You can use hello examples toobuild your own machine learning solution.</span></span>

<span data-ttu-id="2cb7a-107">raccolta di Hello è esperimenti di esempio dal team di Microsoft Azure Machine Learning hello nonché esempi condivisi da hello community di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-107">hello gallery has example experiments by hello Microsoft Azure Machine Learning team as well as examples shared by hello Machine Learning community.</span></span> <span data-ttu-id="2cb7a-108">È anche possibile porre domande o inviare commenti sugli esperimenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="2cb7a-109">toosee come toouse hello raccolta, guardare il video di 3 minuti hello [copiare analisi scientifica dei dati di altre persone lavoro toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) dalla serie hello [analisi scientifica dei dati per i principianti](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="2cb7a-109">toosee how toouse hello gallery, watch hello 3-minute video [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from hello series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-toocopy-in-cortana-intelligence-gallery"></a><span data-ttu-id="2cb7a-110">Trovare un esperimento toocopy nella raccolta di Intelligence Cortana</span><span class="sxs-lookup"><span data-stu-id="2cb7a-110">Find an experiment toocopy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="2cb7a-111">toosee quali esperimenti sono disponibile, andare toohello [raccolta](https://gallery.cortanaintelligence.com/) e fare clic su **esperimenti** nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-111">toosee what experiments are available, go toohello [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at hello top of hello page.</span></span>

### <a name="find-hello-newest-or-most-popular-experiments"></a><span data-ttu-id="2cb7a-112">Trovare hello esperimenti più o meno recenti</span><span class="sxs-lookup"><span data-stu-id="2cb7a-112">Find hello newest or most popular experiments</span></span>
<span data-ttu-id="2cb7a-113">In questa pagina, è possibile visualizzare **aggiunti di recente** esperimenti o scorrere verso il basso toolook in **novità più diffuso** hello più recente o **esperimenti comune Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-113">On this page, you can see **Recently added** experiments, or scroll down toolook at **What's popular** or hello latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="2cb7a-114">Cercare un esperimento che soddisfa requisiti specifici</span><span class="sxs-lookup"><span data-stu-id="2cb7a-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="2cb7a-115">esperimenti toobrowse tutte:</span><span class="sxs-lookup"><span data-stu-id="2cb7a-115">toobrowse all experiments:</span></span>

1. <span data-ttu-id="2cb7a-116">Fare clic su **Sfoglia tutto** nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-116">Click **Browse all** at hello top of hello page.</span></span>
2. <span data-ttu-id="2cb7a-117">Sul lato sinistro di hello, in **ridefinire** in hello **categorie** selezionare **esperimento** hello di toosee tutti hello esperimenti nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-117">On hello left-hand side, under **Refine by** in hello **Categories** section, select **Experiment** toosee all hello experiments in hello Gallery.</span></span>
3. <span data-ttu-id="2cb7a-118">È possibile trovare esperimenti che soddisfano i requisiti in due modi diversi:</span><span class="sxs-lookup"><span data-stu-id="2cb7a-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="2cb7a-119">**Selezionare i filtri a sinistra di hello.**</span><span class="sxs-lookup"><span data-stu-id="2cb7a-119">**Select filters on hello left.**</span></span> <span data-ttu-id="2cb7a-120">Ad esempio, gli esperimenti toobrowse che usano un algoritmo di rilevamento delle anomalie basato su PCA: con **esperimento** selezionato in **categorie**, fare clic su **Mostra tutto**.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-120">For example, toobrowse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="2cb7a-121">In **Algorithms Used** (Algoritmi usati) scegliere **PCA-Based Anomaly Detection** (Rilevamento anomalie basato su PCA).</span><span class="sxs-lookup"><span data-stu-id="2cb7a-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="2cb7a-122">
     ![Selezione dei filtri](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="2cb7a-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="2cb7a-123">**Utilizzare la casella di ricerca hello.**</span><span class="sxs-lookup"><span data-stu-id="2cb7a-123">**Use hello search box.**</span></span> <span data-ttu-id="2cb7a-124">Ad esempio, toofind esperimenti fornito da Microsoft correlati riconoscimento toodigit che usano un algoritmo di machine vettori di supporto di due classi, immettere "riconoscimento di cifre" nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-124">For example, toofind experiments contributed by Microsoft related toodigit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in hello search box.</span></span> <span data-ttu-id="2cb7a-125">Quindi, selezionare hello filtri **esperimento**, **solo il contenuto Microsoft**, e **Two-Class Support Vector Machine**:</span><span class="sxs-lookup"><span data-stu-id="2cb7a-125">Then, select hello filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="2cb7a-126">
     ![Utilizzare la casella di ricerca hello](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="2cb7a-126">
![Use hello search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="2cb7a-127">Fare clic su un esperimento toolearn ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-127">Click an experiment toolearn more about it.</span></span>
5. <span data-ttu-id="2cb7a-128">toorun e/o modificare l'esperimento hello, fare clic su **Open in Studio** nella pagina dell'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-128">toorun and/or modify hello experiment, click **Open in Studio** on hello experiment's page.</span></span> <br></br>

    ![Esperimento di esempio](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="2cb7a-130">Quando si apre un esperimento in Machine Learning Studio hello per la prima volta, è possibile provare gratuitamente o acquista una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-130">When you open an experiment in Machine Learning Studio for hello first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="2cb7a-131">Informazioni sulla versione di valutazione gratuita Machine Learning Studio rispetto al servizio a pagamento hello</span><span class="sxs-lookup"><span data-stu-id="2cb7a-131">Learn about hello Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="2cb7a-132">Creare un nuovo esperimento usando un esempio come modello</span><span class="sxs-lookup"><span data-stu-id="2cb7a-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="2cb7a-133">È anche possibile creare un nuovo esperimento in Machine Learning Studio usando come modello un esempio della raccolta.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="2cb7a-134">Accedere con il toohello le credenziali di account Microsoft [Studio](https://studio.azureml.net), quindi fare clic su **New** toocreate un esperimento.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-134">Sign in with your Microsoft account credentials toohello [Studio](https://studio.azureml.net), and then click **New** toocreate an experiment.</span></span>
2. <span data-ttu-id="2cb7a-135">Esplorare il contenuto di esempio hello e fare clic su uno.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-135">Browse through hello example content and click one.</span></span>

<span data-ttu-id="2cb7a-136">Nell'area di lavoro di Machine Learning Studio utilizzando hello esperimento di esempio come modello, viene creato un esperimento di nuovo.</span><span class="sxs-lookup"><span data-stu-id="2cb7a-136">A new experiment is created in your Machine Learning Studio workspace using hello example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cb7a-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2cb7a-137">Next steps</span></span>
* [<span data-ttu-id="2cb7a-138">Importare dati da diverse origini</span><span class="sxs-lookup"><span data-stu-id="2cb7a-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="2cb7a-139">Esercitazione di avvio rapido per la lingua di hello R in Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2cb7a-139">Quickstart tutorial for hello R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="2cb7a-140">Distribuire un servizio Web di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2cb7a-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
