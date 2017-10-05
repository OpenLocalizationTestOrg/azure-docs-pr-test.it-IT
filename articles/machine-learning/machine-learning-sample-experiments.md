---
title: Copiare gli esperimenti di esempio di Machine Learning - Azure | Microsoft Docs
description: Informazioni su come usare gli esperimenti di Machine Learning per creare nuovi esperimenti con Cortana Intelligence Gallery e Microsoft Azure Machine Learning.
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
ms.openlocfilehash: 55f9bd2ed0d555a14d31bf3d262707d65bd70244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="copy-example-experiments-to-create-new-machine-learning-experiments"></a><span data-ttu-id="8bb02-104">Copiare gli esperimenti di esempio per creare nuovi esperimenti di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8bb02-104">Copy example experiments to create new machine learning experiments</span></span>
<span data-ttu-id="8bb02-105">Questo articolo illustra come usare gli esperimenti di esempio di [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) invece di creare esperimenti di Machine Learning da zero.</span><span class="sxs-lookup"><span data-stu-id="8bb02-105">Learn how to start with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="8bb02-106">È possibile usare gli esempi per compilare la propria soluzione di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8bb02-106">You can use the examples to build your own machine learning solution.</span></span>

<span data-ttu-id="8bb02-107">Nella raccolta sono disponibili esperimenti di esempio del team di Microsoft Azure Machine Learning, oltre a esempi condivisi dalla community di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8bb02-107">The gallery has example experiments by the Microsoft Azure Machine Learning team as well as examples shared by the Machine Learning community.</span></span> <span data-ttu-id="8bb02-108">È anche possibile porre domande o inviare commenti sugli esperimenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="8bb02-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="8bb02-109">Per informazioni su come usare la raccolta, guardare il video di 3 minuti [Copiare il lavoro di altre persone per l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) della serie [Analisi scientifica dei dati per principianti](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="8bb02-109">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-cortana-intelligence-gallery"></a><span data-ttu-id="8bb02-110">Trovare un esperimento da copiare in Cortana Intelligence Gallery</span><span class="sxs-lookup"><span data-stu-id="8bb02-110">Find an experiment to copy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="8bb02-111">Per visualizzare gli esperimenti disponibili, passare a [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) e fare clic su **Experiments** (Esperimenti) nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="8bb02-111">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span></span>

### <a name="find-the-newest-or-most-popular-experiments"></a><span data-ttu-id="8bb02-112">Trovare gli esperimenti più recenti o richiesti</span><span class="sxs-lookup"><span data-stu-id="8bb02-112">Find the newest or most popular experiments</span></span>
<span data-ttu-id="8bb02-113">In questa pagina è possibile visualizzare gli esperimenti **aggiunti di recente**, scorrere per esaminare quelli **più richiesti** o la versione più recente degli **esperimenti Microsoft più richiesti**.</span><span class="sxs-lookup"><span data-stu-id="8bb02-113">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="8bb02-114">Cercare un esperimento che soddisfa requisiti specifici</span><span class="sxs-lookup"><span data-stu-id="8bb02-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="8bb02-115">Per esplorare tutti gli esperimenti:</span><span class="sxs-lookup"><span data-stu-id="8bb02-115">To browse all experiments:</span></span>

1. <span data-ttu-id="8bb02-116">Fare clic su **Browse all** (Esplora tutto) nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="8bb02-116">Click **Browse all** at the top of the page.</span></span>
2. <span data-ttu-id="8bb02-117">In **Refine by** (Affina per) a sinistra nella sezione **Categories** (Categorie) selezionare **Experiment** (Esperimento) per visualizzare tutti gli esperimenti nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="8bb02-117">On the left-hand side, under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span></span>
3. <span data-ttu-id="8bb02-118">È possibile trovare esperimenti che soddisfano i requisiti in due modi diversi:</span><span class="sxs-lookup"><span data-stu-id="8bb02-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="8bb02-119">**Selezionare i filtri a sinistra.**</span><span class="sxs-lookup"><span data-stu-id="8bb02-119">**Select filters on the left.**</span></span> <span data-ttu-id="8bb02-120">Per esaminare ad esempio gli esperimenti che fanno uso di un algoritmo di rilevamento delle anomalie basato su PCA, selezionare **Experiment** (Esperimento) in **Categories** (Categorie) e fare clic su **Show all** (Mostra tutto).</span><span class="sxs-lookup"><span data-stu-id="8bb02-120">For example, to browse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="8bb02-121">In **Algorithms Used** (Algoritmi usati) scegliere **PCA-Based Anomaly Detection** (Rilevamento anomalie basato su PCA).</span><span class="sxs-lookup"><span data-stu-id="8bb02-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="8bb02-122">
     ![Selezione dei filtri](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="8bb02-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="8bb02-123">**Usare la casella di ricerca.**</span><span class="sxs-lookup"><span data-stu-id="8bb02-123">**Use the search box.**</span></span> <span data-ttu-id="8bb02-124">Ad esempio, per trovare esperimenti Microsoft sul riconoscimento di cifre che usano un algoritmo di macchine a vettori di supporto a due classi, immettere "digit recognition" nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8bb02-124">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span></span> <span data-ttu-id="8bb02-125">Selezionare quindi i filtri **Experiment** (Esperimento), **Microsoft content only** (Solo contenuto Microsoft) e **Two-Class Support Vector Machine** (Macchina a vettori di supporto a due classi):</span><span class="sxs-lookup"><span data-stu-id="8bb02-125">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="8bb02-126">
     ![Usare la casella di ricerca](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="8bb02-126">
![Use the search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="8bb02-127">Per altre informazioni su un esperimento, fare clic su di esso.</span><span class="sxs-lookup"><span data-stu-id="8bb02-127">Click an experiment to learn more about it.</span></span>
5. <span data-ttu-id="8bb02-128">Per eseguire e/o modificare l'esperimento, fare clic su **Open in Studio** (Apri in Studio) nella pagina dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="8bb02-128">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span></span> <br></br>

    ![Esperimento di esempio](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="8bb02-130">Quando si apre un esperimento in Machine Learning Studio per la prima volta, è possibile provarlo gratuitamente o acquistare una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8bb02-130">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="8bb02-131">Confronto tra la versione di valutazione gratuita e il servizio a pagamento di Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8bb02-131">Learn about the Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="8bb02-132">Creare un nuovo esperimento usando un esempio come modello</span><span class="sxs-lookup"><span data-stu-id="8bb02-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="8bb02-133">È anche possibile creare un nuovo esperimento in Machine Learning Studio usando come modello un esempio della raccolta.</span><span class="sxs-lookup"><span data-stu-id="8bb02-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="8bb02-134">Accedere a [Studio](https://studio.azureml.net) con le credenziali dell'account Microsoft e quindi fare clic su **Nuovo** per creare un esperimento.</span><span class="sxs-lookup"><span data-stu-id="8bb02-134">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span></span>
2. <span data-ttu-id="8bb02-135">Esplorare il contenuto e fare clic per selezionare un esempio.</span><span class="sxs-lookup"><span data-stu-id="8bb02-135">Browse through the example content and click one.</span></span>

<span data-ttu-id="8bb02-136">Nell'area di lavoro di Machine Learning Studio verrà creato un nuovo esperimento usando l'esperimento di esempio come modello.</span><span class="sxs-lookup"><span data-stu-id="8bb02-136">A new experiment is created in your Machine Learning Studio workspace using the example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bb02-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8bb02-137">Next steps</span></span>
* [<span data-ttu-id="8bb02-138">Importare dati da diverse origini</span><span class="sxs-lookup"><span data-stu-id="8bb02-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="8bb02-139">Esercitazione con guida rapida per il linguaggio di programmazione R per Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8bb02-139">Quickstart tutorial for the R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="8bb02-140">Distribuire un servizio Web di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8bb02-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
