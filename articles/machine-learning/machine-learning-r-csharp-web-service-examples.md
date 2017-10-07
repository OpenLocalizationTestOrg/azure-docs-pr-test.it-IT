---
title: esempi compilati con R - Azure dei servizi web di learning macchina AAA(deprecated) | Documenti Microsoft
description: (obsoleto) Trovare un utile set di esempi di servizi web creati con il codice R e Machine Learning e pubblicato toohello Azure Marketplace.
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
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="9767d-104">(obsoleto) Esempi di utilizzo di codice R in Azure Machine Learning e pubblicati tooMicrosoft Azure Marketplace di servizi Web</span><span class="sxs-lookup"><span data-stu-id="9767d-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="9767d-105">è stata ritirata Hello Microsoft DataMarket e queste API sono state deprecate.</span><span class="sxs-lookup"><span data-stu-id="9767d-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="9767d-106">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9767d-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9767d-107">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="9767d-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9767d-108">In questo articolo sono web di esempio i servizi creati con Azure Machine Learning e pubblicati toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9767d-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="9767d-109">Ogni esempio di servizio web dispone di un documento completo collegato, incorporamento di set di dati di esempio per test di servizi di hello e che spiega come hello utente può creare un servizio simile autonomamente.</span><span class="sxs-lookup"><span data-stu-id="9767d-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="9767d-110">In Azure Machine Learning Studio, gli utenti possono scrivere il codice R e con pochi clic, pubblicarlo come un servizio web per applicazioni e dispositivi tooconsume tutto il mondo hello.</span><span class="sxs-lookup"><span data-stu-id="9767d-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9767d-111">Da produrre calcolatori semplici che forniscono funzionalità statistica toocreating previsione personalizzato text mining sentiment analysis, gli utenti di R sia nuovi che esperti possono beneficiare facilità hello con cui gli utenti di Azure Machine Learning è possano rendere operativo R codice.</span><span class="sxs-lookup"><span data-stu-id="9767d-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="9767d-112">Mentre questi servizi web che poteva essere usati dagli utenti, potenzialmente tramite un'app mobile o un sito Web, scopo hello di questi servizi web esempi è tooshow come Machine Learning è possibile utilizzare R script per scopi analitici e toocreate utilizzati servizi web in inizio del codice R.</span><span class="sxs-lookup"><span data-stu-id="9767d-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="9767d-113">Ogni esempio include codice C# per l'utilizzo del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="9767d-113">Each example includes a C# example for web service consumption.</span></span>

![Diagramma del codice R in Azure Machine Learning: soluzioni R per uso proprietaria o pubblicato toohello Azure Marketplace.][1]

<span data-ttu-id="9767d-115">Prendere in considerazione hello seguenti scenari.</span><span class="sxs-lookup"><span data-stu-id="9767d-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="9767d-116">Scenario 1: Modello generico</span><span class="sxs-lookup"><span data-stu-id="9767d-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="9767d-117">Un utente interagisce con un modello generico che può essere dati applicato tooa del nuovo utente, ad esempio una previsione di base di dati della serie temporale o un metodo di R personalizzato con analitica avanzate.</span><span class="sxs-lookup"><span data-stu-id="9767d-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="9767d-118">Questo utente pubblica hello del modello come un servizio web per altri tooconsume con i relativi dati.</span><span class="sxs-lookup"><span data-stu-id="9767d-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="9767d-119">Binary Classifier</span><span class="sxs-lookup"><span data-stu-id="9767d-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="9767d-120">Modello di cluster</span><span class="sxs-lookup"><span data-stu-id="9767d-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="9767d-121">Multivariate Linear Regression</span><span class="sxs-lookup"><span data-stu-id="9767d-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="9767d-122">Forecasting-Exponential Smoothing</span><span class="sxs-lookup"><span data-stu-id="9767d-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="9767d-123">Previsioni - ETS + STL</span><span class="sxs-lookup"><span data-stu-id="9767d-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="9767d-124">Previsioni - Modello autoregressivo integrato a media mobile (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="9767d-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="9767d-125">Analisi di sopravvivenza</span><span class="sxs-lookup"><span data-stu-id="9767d-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="9767d-126">Scenario 2 : Modello di training - Dati specifici</span><span class="sxs-lookup"><span data-stu-id="9767d-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="9767d-127">Un utente dispone di dati che forniscono utili stime tramite codice R, ad esempio un grande campione di questionari personalità cluster tramite k-means algoritmo toopredict hello personalità tipo di un utente o dati che possono essere utilizzati toopredict il sondaggio integrità un singolo rischio per cancer polmonare con un pacchetto di analisi R sopravvivenza.</span><span class="sxs-lookup"><span data-stu-id="9767d-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="9767d-128">utente Hello pubblica dati hello tramite un servizio web che consente di stimare il risultato di un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="9767d-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="9767d-129">Scenario 3 Modello di ttraining - Dati generici</span><span class="sxs-lookup"><span data-stu-id="9767d-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="9767d-130">Un utente dispone di dati generici (ad esempio, una raccolta di testo) che consente un toobe del servizio web compilato e applicate genericamente a diversi tipi di casi d'uso e scenari.</span><span class="sxs-lookup"><span data-stu-id="9767d-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="9767d-131">Analisi dei sentimenti basata sul lessico</span><span class="sxs-lookup"><span data-stu-id="9767d-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="9767d-132">Scenario 4: Calcolatrice avanzata</span><span class="sxs-lookup"><span data-stu-id="9767d-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="9767d-133">Un utente fornisce calcoli avanzati o simulazioni che non richiedono alcun modello con training adattamento di un modello toohello dati utente.</span><span class="sxs-lookup"><span data-stu-id="9767d-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="9767d-134">Difference in Proportions Test</span><span class="sxs-lookup"><span data-stu-id="9767d-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="9767d-135">Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="9767d-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="9767d-136">Binomial Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="9767d-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="9767d-137">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="9767d-137">FAQ</span></span>
<span data-ttu-id="9767d-138">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9767d-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



