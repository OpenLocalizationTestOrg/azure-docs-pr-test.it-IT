---
title: aaaA soluzione predittiva per il rischio di credito con Machine Learning | Documenti Microsoft
description: Una procedura dettagliata che illustra come una soluzione analitica predittiva, per la carta di credito toocreate valutazione dei rischi in Azure Machine Learning Studio.
keywords: rischio di credito, soluzione di analisi predittiva, valutazione del rischio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="fc1d9-104">Procedura dettagliata: Sviluppare una soluzione di analisi predittiva per la valutazione del rischio di credito in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fc1d9-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="fc1d9-105">In questa procedura dettagliata, abbiamo esaminato un estesa processo hello di sviluppo di una soluzione analitica predittiva in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="fc1d9-106">È un semplice modello di Machine Learning Studio di sviluppare e quindi distribuirla come servizio web di Azure Machine Learning in modello hello possibile effettuare stime utilizzando nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="fc1d9-107">In questa procedura dettagliata si presuppone che Machine Learning Studio sia già stato usato almeno una volta e che alcuni concetti di Machine Learning siano noti,</span><span class="sxs-lookup"><span data-stu-id="fc1d9-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="fc1d9-108">ma non si dà per scontato che l'utente sia un esperto.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="fc1d9-109">Se non si è mai utilizzato **Azure Machine Learning Studio** prima, potrebbe essere necessario toostart esercitazione hello, [crea l'analisi scientifica dei dati prima di provare in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="fc1d9-110">Tale esercitazione illustra Machine Learning Studio hello per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="fc1d9-111">Viene nozioni fondamentali di hello dei moduli come toodrag e rilascio nell'esperimento, collegarli, eseguire l'esperimento hello e visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="fc1d9-112">Un altro strumento che può risultare utile per iniziare è un diagramma che offra una panoramica delle funzionalità di hello di Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="fc1d9-113">È possibile scaricarlo e stamparlo da qui: [Diagramma della panoramica delle funzionalità di Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="fc1d9-114">Se si è nuovo campo toohello di machine learning in generale, è una serie di video che potrebbe essere utile tooyou.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="fc1d9-115">Viene chiamato [analisi scientifica dei dati per i principianti](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) ed è possibile concedere una formazione toomachine introduzione grande usando vocaboli e concetti.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="fc1d9-116">problema di Hello</span><span class="sxs-lookup"><span data-stu-id="fc1d9-116">hello problem</span></span>

<span data-ttu-id="fc1d9-117">Si supponga che è necessario toopredict il rischio di credito dei singoli in base alle informazioni di hello fornita in un'applicazione di carta di credito.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="fc1d9-118">La valutazione del rischio di credito è un problema complesso, ma è possibile semplificarla per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="fc1d9-119">Verrà usata come esempio di come è possibile creare una soluzione di analisi predittiva con Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="fc1d9-120">toodo, vengono utilizzati da Azure Machine Learning Studio e un servizio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="fc1d9-121">soluzione Hello</span><span class="sxs-lookup"><span data-stu-id="fc1d9-121">hello solution</span></span>

<span data-ttu-id="fc1d9-122">In questa procedura dettagliata, si inizia con dati sul rischio di credito disponibili pubblicamente, quindi si sviluppa e si crea un modello predittivo in base a tali dati.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="fc1d9-123">Quindi è distribuire il modello di hello come servizio web in modo che può essere utilizzato da altri utenti per valutare il rischio di credito.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="fc1d9-124">toocreate questa soluzione di valutazione dei rischi di carta di credito, eseguire la procedura seguente è:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="fc1d9-125">Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fc1d9-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="fc1d9-126">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="fc1d9-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="fc1d9-127">Creare un esperimento</span><span class="sxs-lookup"><span data-stu-id="fc1d9-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="fc1d9-128">Eseguire il training e valutare i modelli di hello</span><span class="sxs-lookup"><span data-stu-id="fc1d9-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="fc1d9-129">Distribuzione di servizio web hello</span><span class="sxs-lookup"><span data-stu-id="fc1d9-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="fc1d9-130">Servizio web di accesso hello</span><span class="sxs-lookup"><span data-stu-id="fc1d9-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="fc1d9-131">È possibile trovare una copia di lavoro dell'esperimento hello che si sviluppa in questa procedura dettagliata in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="fc1d9-132">Andare troppo**[procedura dettagliata: stima di rischio di credito](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  e fare clic su **Open in Studio** toodownload una copia dell'esperimento hello nell'area di lavoro di Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="fc1d9-133">Questa procedura dettagliata è basata su una versione semplificata dell'esperimento di esempio hello [Binary Classification: stima di rischio di credito](http://go.microsoft.com/fwlink/?LinkID=525270), disponibile anche in hello [raccolta](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
