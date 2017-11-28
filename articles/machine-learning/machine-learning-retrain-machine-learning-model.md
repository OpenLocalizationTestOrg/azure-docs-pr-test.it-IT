---
title: Ripetere il training di un modello di Machine Learning | Documentazione Microsoft
description: Informazioni su come ripetere il training di un modello e aggiornare il servizio Web per usare il modello appena sottoposto a training in Azure Machine Learning.
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
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="efa37-103">Ripetere il training di un modello di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="efa37-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="efa37-104">Come parte del processo di messa in funzione dei modelli di apprendimento automatico in Azure Machine Learning, è necessario sottoporre a training e salvare il modello.</span><span class="sxs-lookup"><span data-stu-id="efa37-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="efa37-105">Lo si userà quindi per creare un servizio Web predicativo.</span><span class="sxs-lookup"><span data-stu-id="efa37-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="efa37-106">Il servizio Web potrà quindi essere utilizzato in siti Web, dashboard e app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="efa37-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="efa37-107">I modelli creati con Machine Learning in genere non sono statici.</span><span class="sxs-lookup"><span data-stu-id="efa37-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="efa37-108">Quando sono disponibili nuovi dati o quando il consumer dell'API ha i propri dati, è necessario ripetere il training del modello.</span><span class="sxs-lookup"><span data-stu-id="efa37-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="efa37-109">La ripetizione del training può avvenire di frequente.</span><span class="sxs-lookup"><span data-stu-id="efa37-109">Retraining may occur frequently.</span></span> <span data-ttu-id="efa37-110">Con la funzionalità delle API di ripetizione del training a livello di codice, è possibile ripetere il training del modello a livello di codice usando le API di ripetizione del training e aggiornare il servizio Web con un modello di cui è stato appena eseguito il training.</span><span class="sxs-lookup"><span data-stu-id="efa37-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="efa37-111">Questo documento descrive il processo di ripetizione del training e illustra come usare le API per la ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="efa37-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="efa37-112">Motivi per cui ripetere il training: definizione del problema</span><span class="sxs-lookup"><span data-stu-id="efa37-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="efa37-113">Durante il processo di training di Machine Learning viene eseguito il training di un modello usando un set di dati.</span><span class="sxs-lookup"><span data-stu-id="efa37-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="efa37-114">I modelli creati con Machine Learning in genere non sono statici.</span><span class="sxs-lookup"><span data-stu-id="efa37-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="efa37-115">Quando sono disponibili nuovi dati o quando il consumer dell'API ha i propri dati, è necessario ripetere il training del modello.</span><span class="sxs-lookup"><span data-stu-id="efa37-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="efa37-116">In questi scenari un'API a livello di codice offre un modo pratico per consentire all'utente dell'API di creare un client in grado di ripetere il training del modello una tantum o periodicamente usando i propri dati.</span><span class="sxs-lookup"><span data-stu-id="efa37-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="efa37-117">Sarà quindi possibile valutare i risultati della ripetizione del training e aggiornare l'API del servizio Web per l'uso del modello appena sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="efa37-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="efa37-118">Se si dispone di un esperimento di training esistente e di un nuovo servizio Web, è possibile che si preferisca fare riferimento all'articolo Ripetere il training di un servizio Web predittivo esistente anziché seguire la procedura dettagliata descritta nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="efa37-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="efa37-119">Flusso di lavoro end-to-end</span><span class="sxs-lookup"><span data-stu-id="efa37-119">End-to-end workflow</span></span>
<span data-ttu-id="efa37-120">Per il processo sono necessari i componenti seguenti: un esperimento di training e un esperimento predittivo pubblicato come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="efa37-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="efa37-121">Per abilitare la ripetizione del training di un modello con training, l'esperimento di training deve essere pubblicato come servizio Web con l'output di un modello con training.</span><span class="sxs-lookup"><span data-stu-id="efa37-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="efa37-122">In questo modo viene abilitato l'accesso dell'API al modello per la ripetizione del training.</span><span class="sxs-lookup"><span data-stu-id="efa37-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="efa37-123">I passaggi seguenti sono validi sia per i nuovi servizi Web sia per i servizi Web classici:</span><span class="sxs-lookup"><span data-stu-id="efa37-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="efa37-124">Creare il servizio Web predittivo iniziale:</span><span class="sxs-lookup"><span data-stu-id="efa37-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="efa37-125">Creare un esperimento di training</span><span class="sxs-lookup"><span data-stu-id="efa37-125">Create a training experiment</span></span>
* <span data-ttu-id="efa37-126">Creare un esperimento Web predittivo</span><span class="sxs-lookup"><span data-stu-id="efa37-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="efa37-127">Distribuire un servizio Web predittivo</span><span class="sxs-lookup"><span data-stu-id="efa37-127">Deploy a predictive web service</span></span>

<span data-ttu-id="efa37-128">Ripetere il training del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="efa37-128">Retrain the Web service:</span></span>

* <span data-ttu-id="efa37-129">Aggiornare l'esperimento di training per consentire la ripetizione del training</span><span class="sxs-lookup"><span data-stu-id="efa37-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="efa37-130">Distribuire la ripetizione del training del servizio Web</span><span class="sxs-lookup"><span data-stu-id="efa37-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="efa37-131">Usare il codice del servizio Esecuzione batch per ripetere il training del modello</span><span class="sxs-lookup"><span data-stu-id="efa37-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="efa37-132">Per una descrizione dettagliata dei passaggi precedenti, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="efa37-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="efa37-133">Per distribuire un nuovo servizio Web è necessario disporre delle autorizzazioni sufficienti nella sottoscrizione a cui si sta distribuendo il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="efa37-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="efa37-134">Per altre informazioni, vedere [Gestire un servizio Web usando il portale dei servizi Web di Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="efa37-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="efa37-135">Se è stato distribuito un servizio Web classico:</span><span class="sxs-lookup"><span data-stu-id="efa37-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="efa37-136">Creare un nuovo endpoint nel servizio Web predittivo</span><span class="sxs-lookup"><span data-stu-id="efa37-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="efa37-137">Ottenere l'URL della PATCH e il codice</span><span class="sxs-lookup"><span data-stu-id="efa37-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="efa37-138">Usare l'URL della PATCH in modo da accedere al nuovo endpoint del modello nuovamente sottoposto a training</span><span class="sxs-lookup"><span data-stu-id="efa37-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="efa37-139">Per una descrizione dettagliata dei passaggi precedenti, vedere [Ripetere il training di un servizio Web classico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="efa37-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="efa37-140">Se si verificano problemi durante la ripetizione del training di un servizio Web classico, vedere [Risoluzione dei problemi relativi alla ripetizione del training di un servizio Web classico di Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="efa37-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="efa37-141">Se è stato distribuito un nuovo servizio Web:</span><span class="sxs-lookup"><span data-stu-id="efa37-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="efa37-142">Accedere con l'account di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="efa37-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="efa37-143">Ottenere la definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="efa37-143">Get the Web service definition</span></span>
* <span data-ttu-id="efa37-144">Esportare la definizione del servizio Web in un file in formato JSON</span><span class="sxs-lookup"><span data-stu-id="efa37-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="efa37-145">Aggiornare il riferimento al BLOB `ilearner` nel file JSON</span><span class="sxs-lookup"><span data-stu-id="efa37-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="efa37-146">Importare il file JSON in una definizione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="efa37-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="efa37-147">Aggiornare il servizio Web con la nuova definizione</span><span class="sxs-lookup"><span data-stu-id="efa37-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="efa37-148">Per una descrizione dettagliata dei passaggi precedenti, vedere [Ripetere il training di un nuovo servizio Web usando i cmdlet di gestione di PowerShell per Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="efa37-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="efa37-149">Il processo per la configurazione della ripetizione del training per un servizio Web classico prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="efa37-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![Panoramica del processo di ripetizione del training][1]

<span data-ttu-id="efa37-151">Il processo per la configurazione della ripetizione del training per un nuovo servizio Web prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="efa37-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![Panoramica del processo di ripetizione del training][7]

## <a name="other-resources"></a><span data-ttu-id="efa37-153">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="efa37-153">Other Resources</span></span>
* <span data-ttu-id="efa37-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/) (Ripetere il training e aggiornare modelli di Azure Machine Learning con Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="efa37-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)</span></span>
* [<span data-ttu-id="efa37-155">Creare più modelli di Machine Learning ed endpoint di servizio Web da un esperimento usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="efa37-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="efa37-156">Il video sulla [ripetizione del training di modelli AML tramite API](https://www.youtube.com/watch?v=wwjglA8xllg) illustra come ripetere il training di modelli di Machine Learning creati in Azure Machine Learning usando la ripetizione del training delle API e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efa37-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

