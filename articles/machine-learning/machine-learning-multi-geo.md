---
title: "Guida per più aree geografiche | Documentazione Microsoft"
description: Informazioni su come creare un'area di lavoro e pubblicare un servizio web in un'area di Azure diversa da quella degli Stati Uniti centro meridionali (SCUS).
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="27d33-103">Guida per più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="27d33-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="27d33-104">Questo articolo illustra come creare un'area di lavoro e pubblicare un servizio Web in altre aree geografiche di Azure.</span><span class="sxs-lookup"><span data-stu-id="27d33-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="27d33-105">La [pagina sui prodotti Azure per area geografica](https://azure.microsoft.com/en-us/regions/services/) fornisce un elenco delle aree in cui Azure Machine Learning è disponibile.</span><span class="sxs-lookup"><span data-stu-id="27d33-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="27d33-106">Creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="27d33-106">Create a workspace</span></span>
1. <span data-ttu-id="27d33-107">Accedere al portale di Microsoft Azure classico.</span><span class="sxs-lookup"><span data-stu-id="27d33-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="27d33-108">Fare clic su **+ NUOVO** > **SERVIZI DATI** > **MACHINE LEARNING** > **CREAZIONE RAPIDA**.</span><span class="sxs-lookup"><span data-stu-id="27d33-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="27d33-109">In **INDIRIZZO** selezionare un'altra area, ad esempio **Asia sud-orientale**.</span><span class="sxs-lookup"><span data-stu-id="27d33-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="27d33-110">![Guida per più aree geografiche immagine 1][1]</span><span class="sxs-lookup"><span data-stu-id="27d33-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="27d33-111">Selezionare l'area di lavoro, quindi fare clic su **Accedi a ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="27d33-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="27d33-112">![Guida per più aree geografiche immagine 2][2]</span><span class="sxs-lookup"><span data-stu-id="27d33-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="27d33-113">Ora si dispone di un'area di lavoro in un'altra area geografica che può essere utilizzata come qualsiasi altra area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="27d33-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="27d33-114">Per passare da un’area di lavoro ad un’altra, cercare in alto a destra dello schermo.</span><span class="sxs-lookup"><span data-stu-id="27d33-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="27d33-115">Fare clic sul menu a discesa, selezionare l'area geografica e quindi selezionare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="27d33-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="27d33-116">Tutto è locale rispetto all'area geografica dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="27d33-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="27d33-117">Ad esempio, tutti i servizi Web creati da un'area di lavoro saranno nella stessa area geografica in cui si trova l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="27d33-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="27d33-118">![Guida per più aree geografiche immagine 3][3]</span><span class="sxs-lookup"><span data-stu-id="27d33-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="27d33-119">Aprire un esperimento dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="27d33-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="27d33-120">Se si apre un esperimento dalla raccolta, è inoltre possibile selezionare in quale area geografica si desidera copiare l’esperimento.</span><span class="sxs-lookup"><span data-stu-id="27d33-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Guida per più aree geografiche immagine 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="27d33-122">Gestione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="27d33-122">Web service management</span></span>
<span data-ttu-id="27d33-123">Per gestire a livello di programmazione i servizi web, ad esempio per la ripetizione della formazione, usare l'indirizzo specifico dell'area geografica:</span><span class="sxs-lookup"><span data-stu-id="27d33-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="27d33-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="27d33-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="27d33-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="27d33-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="27d33-126">Punti da notare</span><span class="sxs-lookup"><span data-stu-id="27d33-126">Things to note</span></span>
1. <span data-ttu-id="27d33-127">In questo modo è possibile copiare solo esperimenti tra aree di lavoro che appartengono alla stessa area geografica.</span><span class="sxs-lookup"><span data-stu-id="27d33-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="27d33-128">Se è necessario copiare un esperimento fra aree di lavoro che appartengono ad aree diverse, è possibile usare il commandlet di [PowerShell](http://aka.ms/amlps) [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment).</span><span class="sxs-lookup"><span data-stu-id="27d33-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="27d33-129">Un'altra soluzione alternativa consiste nel pubblicare l'esperimento nella raccolta in modalità non in elenco, quindi aprirlo nell'area di lavoro dall'altra area.</span><span class="sxs-lookup"><span data-stu-id="27d33-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="27d33-130">Il selettore dell’area visualizzerà solo le aree di lavoro di una determinata area geografica alla volta.</span><span class="sxs-lookup"><span data-stu-id="27d33-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="27d33-131">Un’area di lavoro con accesso libero o Guest (anonimo) verrà creata e ospitata in Stati Uniti centro-meridionali.</span><span class="sxs-lookup"><span data-stu-id="27d33-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="27d33-132">I servizi Web distribuiti da un'area di lavoro nell’Asia sudorientale verranno anche ospitati in Asia sudorientale.</span><span class="sxs-lookup"><span data-stu-id="27d33-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="27d33-133">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="27d33-133">More information</span></span>
<span data-ttu-id="27d33-134">Aggiungere una domanda sul [forum di Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="27d33-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
