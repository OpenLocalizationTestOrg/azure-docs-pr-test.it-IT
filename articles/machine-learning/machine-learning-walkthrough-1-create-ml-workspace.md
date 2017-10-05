---
title: 'Passaggio 1: Creare un''area di lavoro di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 1 della procedura dettagliata Sviluppare una soluzione predittiva: informazioni su come configurare una nuova area di lavoro di Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="3ee51-103">Passaggio 1 della procedura dettagliata: Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3ee51-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="3ee51-104">Questo è il primo passaggio della procedura dettagliata per [sviluppare una soluzione di analisi predittiva con Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="3ee51-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="3ee51-105">**Creare un'area di lavoro di Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="3ee51-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="3ee51-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="3ee51-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="3ee51-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="3ee51-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="3ee51-108">Eseguire il training e valutare i modelli</span><span class="sxs-lookup"><span data-stu-id="3ee51-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="3ee51-109">Distribuire il servizio Web</span><span class="sxs-lookup"><span data-stu-id="3ee51-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="3ee51-110">Accedere al servizio Web</span><span class="sxs-lookup"><span data-stu-id="3ee51-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="3ee51-111">Per usare Machine Learning Studio, è necessario disporre di un'area di lavoro di Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3ee51-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="3ee51-112">Quest'area di lavoro contiene tutti gli strumenti necessari per la creazione, la gestione e la pubblicazione di esperimenti.</span><span class="sxs-lookup"><span data-stu-id="3ee51-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="3ee51-113">L'amministratore della sottoscrizione di Azure deve creare l'area di lavoro e quindi aggiungere l'utente come proprietario o collaboratore.</span><span class="sxs-lookup"><span data-stu-id="3ee51-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="3ee51-114">Per informazioni, vedere [Creare un'area di lavoro di Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3ee51-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="3ee51-115">Dopo aver creato l'area di lavoro, aprire Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="3ee51-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="3ee51-116">Se sono disponibili più aree di lavoro, è possibile selezionare l'area di lavoro nella barra degli strumenti nell'angolo superiore destro della finestra.</span><span class="sxs-lookup"><span data-stu-id="3ee51-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Selezionare l'area di lavoro in Studio][2]

> [!TIP]
> <span data-ttu-id="3ee51-118">Se si è proprietari dell'area di lavoro, è possibile condividere gli esperimenti su cui si sta lavorando invitando altri utenti nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3ee51-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="3ee51-119">Questa operazione può essere eseguita nella pagina **SETTINGS** di Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3ee51-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="3ee51-120">È sufficiente conoscere l'account Microsoft o l'account aziendale di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="3ee51-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="3ee51-121">Nella pagina **SETTINGS** fare clic su **USERS** e quindi su **INVITE MORE USERS** nella parte inferiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="3ee51-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="3ee51-122">**Passaggio successivo: [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="3ee51-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
