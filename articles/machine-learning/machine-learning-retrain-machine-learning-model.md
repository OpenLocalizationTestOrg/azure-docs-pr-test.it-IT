---
title: un modello di Machine Learning aaaRetrain | Documenti Microsoft
description: Informazioni su come tooretrain un modello e aggiornamento hello toouse hello appena sottoposto a training modello di servizio Web in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="73d90-103">Ripetere il training di un modello di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="73d90-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="73d90-104">Come parte del processo di hello di rendere operativo il computer di modelli di apprendimento in Azure Machine Learning, il modello è stato sottoposto a training e salvato.</span><span class="sxs-lookup"><span data-stu-id="73d90-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="73d90-105">È quindi utilizzarlo toocreate predicative servizio Web.</span><span class="sxs-lookup"><span data-stu-id="73d90-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="73d90-106">Hello servizio Web può quindi essere utilizzato in siti web, dashboard e App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="73d90-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="73d90-107">I modelli creati con Machine Learning in genere non sono statici.</span><span class="sxs-lookup"><span data-stu-id="73d90-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="73d90-108">Man mano che diventano disponibili nuovi dati o quando il consumer hello di hello API ha i propri modelli di dati hello devono toobe ripetere il training.</span><span class="sxs-lookup"><span data-stu-id="73d90-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="73d90-109">La ripetizione del training può avvenire di frequente.</span><span class="sxs-lookup"><span data-stu-id="73d90-109">Retraining may occur frequently.</span></span> <span data-ttu-id="73d90-110">Grazie a funzionalità di API di ripetizione di training a livello di codice hello, è possibile a livello di programmazione ripetere il training modello di hello utilizzo hello servizio Web hello API ripetizione di training e di aggiornamento con modello sottoposto a training appena hello.</span><span class="sxs-lookup"><span data-stu-id="73d90-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="73d90-111">Questo documento descrive hello processo di ripetizione di training e Mostra come toouse hello API ripetizione di training.</span><span class="sxs-lookup"><span data-stu-id="73d90-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="73d90-112">Motivo per cui ripetere il training: definizione hello problema</span><span class="sxs-lookup"><span data-stu-id="73d90-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="73d90-113">Come parte di hello machine learning processo di training, un modello viene eseguito il training usando un set di dati.</span><span class="sxs-lookup"><span data-stu-id="73d90-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="73d90-114">I modelli creati con Machine Learning in genere non sono statici.</span><span class="sxs-lookup"><span data-stu-id="73d90-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="73d90-115">Man mano che diventano disponibili nuovi dati o quando il consumer hello di hello API ha i propri modelli di dati hello devono toobe ripetere il training.</span><span class="sxs-lookup"><span data-stu-id="73d90-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="73d90-116">In questi scenari, un'API a livello di codice fornisce un modo pratico di tooallow si o hello consumer del toocreate API, un client che è possibile, in modo occasionale o regolare, ripetere il training hello modello utilizzando i propri dati.</span><span class="sxs-lookup"><span data-stu-id="73d90-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="73d90-117">Possono quindi valutare i risultati di hello di ripetizione di training e aggiornare hello API toouse hello appena sottoposto a training modello di servizio Web.</span><span class="sxs-lookup"><span data-stu-id="73d90-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="73d90-118">Se si dispone di un esperimento di Training esistenti e il servizio Web di nuovo, è consigliabile toocheck fuori servizio un Web predittivo esistente anziché hello nella procedura dettagliata seguente indicata nella seguente sezione hello ripeterne il training.</span><span class="sxs-lookup"><span data-stu-id="73d90-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="73d90-119">Flusso di lavoro end-to-end</span><span class="sxs-lookup"><span data-stu-id="73d90-119">End-to-end workflow</span></span>
<span data-ttu-id="73d90-120">processo Hello implica hello seguenti componenti: un esperimento di Training e un esperimento predittiva pubblicata come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="73d90-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="73d90-121">tooenable ripetizione di training di un modello con training, hello esperimento di Training deve essere pubblicata come servizio Web con l'output di hello di un modello con training.</span><span class="sxs-lookup"><span data-stu-id="73d90-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="73d90-122">In questo modo modello toohello di accesso dell'API per la ripetizione di training.</span><span class="sxs-lookup"><span data-stu-id="73d90-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="73d90-123">Hello alla procedura seguente si applica tooboth nuovo e classico servizi Web:</span><span class="sxs-lookup"><span data-stu-id="73d90-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="73d90-124">Creazione del servizio Web predittivo iniziale hello:</span><span class="sxs-lookup"><span data-stu-id="73d90-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="73d90-125">Creare un esperimento di training</span><span class="sxs-lookup"><span data-stu-id="73d90-125">Create a training experiment</span></span>
* <span data-ttu-id="73d90-126">Creare un esperimento Web predittivo</span><span class="sxs-lookup"><span data-stu-id="73d90-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="73d90-127">Distribuire un servizio Web predittivo</span><span class="sxs-lookup"><span data-stu-id="73d90-127">Deploy a predictive web service</span></span>

<span data-ttu-id="73d90-128">Ripetere il training del servizio Web hello:</span><span class="sxs-lookup"><span data-stu-id="73d90-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="73d90-129">Aggiornare tooallow esperimento di training per la ripetizione di training</span><span class="sxs-lookup"><span data-stu-id="73d90-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="73d90-130">Distribuire hello ripetizione di training servizio web</span><span class="sxs-lookup"><span data-stu-id="73d90-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="73d90-131">Utilizzare il modello hello tooretrain di hello servizio esecuzione Batch codice</span><span class="sxs-lookup"><span data-stu-id="73d90-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="73d90-132">Per una procedura dettagliata di hello passaggi precedenti, vedere [Machine Learning ripetere il training dei modelli a livello di codice](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="73d90-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="73d90-133">un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="73d90-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="73d90-134">Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="73d90-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="73d90-135">Se è stato distribuito un servizio Web classico:</span><span class="sxs-lookup"><span data-stu-id="73d90-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="73d90-136">Creare un nuovo Endpoint nel servizio Web predittivo hello</span><span class="sxs-lookup"><span data-stu-id="73d90-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="73d90-137">Ottenere l'URL di PATCH hello e codice</span><span class="sxs-lookup"><span data-stu-id="73d90-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="73d90-138">Utilizzare prova URL PATCH toopoint prova nuovo Endpoint di hello ripetere il training del modello</span><span class="sxs-lookup"><span data-stu-id="73d90-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="73d90-139">Per una procedura dettagliata di hello passaggi precedenti, vedere [ripetere il training di un servizio Web classico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="73d90-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="73d90-140">Se si verificano problemi di un servizio Web classico di ripetizione di training, vedere [risoluzione dei problemi hello ripetizione di training di un servizio Web di Azure Machine Learning classico](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="73d90-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="73d90-141">Se è stato distribuito un nuovo servizio Web:</span><span class="sxs-lookup"><span data-stu-id="73d90-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="73d90-142">Accedi tooyour account di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="73d90-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="73d90-143">Ottenere una definizione del servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="73d90-143">Get hello Web service definition</span></span>
* <span data-ttu-id="73d90-144">Esportazione hello definizione del servizio Web nel formato JSON</span><span class="sxs-lookup"><span data-stu-id="73d90-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="73d90-145">Aggiornare hello riferimento toohello `ilearner` blob in hello JSON</span><span class="sxs-lookup"><span data-stu-id="73d90-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="73d90-146">Importare hello JSON in una definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="73d90-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="73d90-147">Aggiornare il servizio Web hello con nuova definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="73d90-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="73d90-148">Per una procedura dettagliata di hello passaggi precedenti, vedere [ripetere il training di un servizio Web di nuovo utilizzando i cmdlet di PowerShell di gestione di Machine Learning hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="73d90-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="73d90-149">il processo di Hello per la configurazione di ripetizione di training per un servizio Web classico include hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="73d90-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Panoramica del processo di ripetizione del training][1]

<span data-ttu-id="73d90-151">il processo di Hello per la configurazione di ripetizione di training per un servizio Web nuovo include hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="73d90-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Panoramica del processo di ripetizione del training][7]

## <a name="other-resources"></a><span data-ttu-id="73d90-153">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="73d90-153">Other Resources</span></span>
* <span data-ttu-id="73d90-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/) (Ripetere il training e aggiornare modelli di Azure Machine Learning con Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="73d90-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)</span></span>
* [<span data-ttu-id="73d90-155">Creare più modelli di Machine Learning ed endpoint di servizio Web da un esperimento usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="73d90-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="73d90-156">Hello [AML ripetizione di training modelli utilizzando le API](https://www.youtube.com/watch?v=wwjglA8xllg) video illustra la modalità di creazione di modelli di Machine Learning tooretrain in Azure Machine Learning usando hello API ripetizione di training e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73d90-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

