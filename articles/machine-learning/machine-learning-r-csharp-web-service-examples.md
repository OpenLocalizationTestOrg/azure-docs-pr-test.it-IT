---
title: (Deprecato) Esempi di servizi Web di Machine Learning creati con R - Azure | Documentazione Microsoft
description: (Deprecato) Trovare un insieme utile di esempi di servizi Web creati con codice R e Machine Learning e pubblicati in Azure Marketplace.
keywords: csharp, codice r, esempi di servizi web
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="66321-104">(Deprecato) Esempi di servizi Web che usano codice R in Azure Machine Learning e pubblicati in Microsoft Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="66321-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="66321-105">Microsoft DataMarket è in fase di ritiro e queste API sono state deprecate.</span><span class="sxs-lookup"><span data-stu-id="66321-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="66321-106">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="66321-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="66321-107">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="66321-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="66321-108">Questo articolo contiene servizi Web di esempio che sono stati creati utilizzando Azure Machine Learning e che sono stati pubblicati in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="66321-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="66321-109">A ogni servizio Web è associata una documentazione completa, che include set di dati di esempio per il test dei servizi e una spiegazione della modalità in cui un utente può creare un servizio analogo da solo.</span><span class="sxs-lookup"><span data-stu-id="66321-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="66321-110">Azure Machine Learning Studio permette agli utenti di scrivere codice R e, selezionando alcuni pulsanti, di pubblicare tale codice come servizio Web, affinché possa essere usato da altri utenti e dispositivi in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="66321-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="66321-111">Dalla produzione di semplici calcolatrici, che forniscono funzionalità statistiche, alla creazione di predittori personalizzati per l'analisi dei sentimenti per il data mining dei testi, ad esempio, i nuovi utenti e gli utenti esperti di R possono usufruire della semplicità con cui gli utenti di Azure Machine Learning possono rendere operativo il codice R.</span><span class="sxs-lookup"><span data-stu-id="66321-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="66321-112">Benché questi servizi Web possano essere usati dagli utenti, potenzialmente tramite un'app mobile o un sito Web, la loro finalità  consiste anche nel fungere da esempio dell'uso di Machine Learning per rendere operativi script R per fini analitici e per la creazione di servizi Web basati sul codice R.</span><span class="sxs-lookup"><span data-stu-id="66321-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="66321-113">Ogni esempio include codice C# per l'utilizzo del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66321-113">Each example includes a C# example for web service consumption.</span></span>

![Diagramma del codice R in Azure Machine Learning: soluzioni R per l’uso proprietario o pubblicate in Azure Marketplace.][1]

<span data-ttu-id="66321-115">Esaminare gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="66321-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="66321-116">Scenario 1: Modello generico</span><span class="sxs-lookup"><span data-stu-id="66321-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="66321-117">Un utente usa un modello generico, applicabile a nuovi dati dell'utente, ad esempio una previsione di base dei dati di una serie temporale o un metodo R personalizzato con funzionalità di analisi avanzate.</span><span class="sxs-lookup"><span data-stu-id="66321-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="66321-118">L'utente pubblica il modello come servizio Web, in modo che altri utenti possano usarlo con i propri dati.</span><span class="sxs-lookup"><span data-stu-id="66321-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="66321-119">Binary Classifier</span><span class="sxs-lookup"><span data-stu-id="66321-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="66321-120">Modello di cluster</span><span class="sxs-lookup"><span data-stu-id="66321-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="66321-121">Multivariate Linear Regression</span><span class="sxs-lookup"><span data-stu-id="66321-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="66321-122">Forecasting-Exponential Smoothing</span><span class="sxs-lookup"><span data-stu-id="66321-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="66321-123">Previsioni - ETS + STL</span><span class="sxs-lookup"><span data-stu-id="66321-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="66321-124">Previsioni - Modello autoregressivo integrato a media mobile (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="66321-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="66321-125">Analisi di sopravvivenza</span><span class="sxs-lookup"><span data-stu-id="66321-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="66321-126">Scenario 2 : Modello di training - Dati specifici</span><span class="sxs-lookup"><span data-stu-id="66321-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="66321-127">Un utente ha a disposizione dati che forniscono previsioni utili tramite il codice R, ad esempio un ampio campione di questionari relativi alla personalità raggruppati in cluster tramite un algoritmo k-means per prevedere il tipo di personalità dell'utente oppure i dati relativi a un sondaggio sulla salute che possono essere usati per prevedere il rischio di un individuo a livello di cancro ai polmoni tramite un pacchetto R dell'analisi di sopravvivenza.</span><span class="sxs-lookup"><span data-stu-id="66321-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="66321-128">L'utente pubblica i dati tramite un servizio Web che prevede l'esito relativo a un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="66321-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="66321-129">Scenario 3 Modello di ttraining - Dati generici</span><span class="sxs-lookup"><span data-stu-id="66321-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="66321-130">Un utente ha a disposizione dati generici, ad esempio un corpus di testo, che permettono la creazione di un servizio Web che è possibile creare e applicare in modo generico a diversi tipi di casi e scenari.</span><span class="sxs-lookup"><span data-stu-id="66321-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="66321-131">Analisi dei sentimenti basata sul lessico</span><span class="sxs-lookup"><span data-stu-id="66321-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="66321-132">Scenario 4: Calcolatrice avanzata</span><span class="sxs-lookup"><span data-stu-id="66321-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="66321-133">Un utente fornisce calcoli o simulazioni avanzate, che non richiedono alcun modello di training o alcun adattamento di modelli ai dati dell'utente.</span><span class="sxs-lookup"><span data-stu-id="66321-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="66321-134">Difference in Proportions Test</span><span class="sxs-lookup"><span data-stu-id="66321-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="66321-135">Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="66321-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="66321-136">Binomial Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="66321-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="66321-137">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="66321-137">FAQ</span></span>
<span data-ttu-id="66321-138">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione nel Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="66321-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



