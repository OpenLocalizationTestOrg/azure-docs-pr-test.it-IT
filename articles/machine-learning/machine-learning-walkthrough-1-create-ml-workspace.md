---
title: 'Passaggio 1: Creare un''area di lavoro di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 1 di hello sviluppare una procedura dettagliata soluzione predittiva: informazioni su come tooset una nuova area di lavoro di Azure Machine Learning Studio.'
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
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="a3373-103">Passaggio 1 della procedura dettagliata: Creare un'area di lavoro di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a3373-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="a3373-104">Questo è hello primo passaggio della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="a3373-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="a3373-105">**Creare un'area di lavoro di Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="a3373-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="a3373-106">Caricare i dati esistenti</span><span class="sxs-lookup"><span data-stu-id="a3373-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="a3373-107">Creare un nuovo esperimento</span><span class="sxs-lookup"><span data-stu-id="a3373-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a3373-108">Eseguire il training e valutare i modelli di hello</span><span class="sxs-lookup"><span data-stu-id="a3373-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="a3373-109">Distribuzione di servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="a3373-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="a3373-110">Accedere al servizio Web hello</span><span class="sxs-lookup"><span data-stu-id="a3373-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="a3373-111">toouse Machine Learning Studio, è necessario toohave un'area di lavoro di Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a3373-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="a3373-112">L'area di lavoro contiene strumenti hello necessari toocreate, gestire e pubblicare esperimenti.</span><span class="sxs-lookup"><span data-stu-id="a3373-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="a3373-113">messaggio per l'amministratore per la sottoscrizione di Azure deve dell'area di lavoro di toocreate hello e quindi aggiunto come proprietario o collaboratore.</span><span class="sxs-lookup"><span data-stu-id="a3373-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="a3373-114">Per informazioni, vedere [Creare un'area di lavoro di Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="a3373-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="a3373-115">Dopo aver creato l'area di lavoro, aprire Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="a3373-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="a3373-116">Se si dispone di più di un'area di lavoro, è possibile selezionare l'area di lavoro hello hello sulla barra degli strumenti hello alto a destra della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="a3373-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Selezionare l'area di lavoro in Studio][2]

> [!TIP]
> <span data-ttu-id="a3373-118">Se sono state apportate un proprietario dell'area di lavoro hello, è possibile condividere gli esperimenti di hello si sta lavorando per invitare altri utenti toohello dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a3373-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="a3373-119">È possibile farlo in Machine Learning Studio su hello **impostazioni** pagina.</span><span class="sxs-lookup"><span data-stu-id="a3373-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="a3373-120">Per ogni utente è sufficiente hello account di Microsoft o aziendale.</span><span class="sxs-lookup"><span data-stu-id="a3373-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="a3373-121">In hello **impostazioni** pagina, fare clic su **utenti**, quindi fare clic su **INVITARE utenti più** nella parte inferiore di hello della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="a3373-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="a3373-122">**Passaggio successivo: [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="a3373-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
