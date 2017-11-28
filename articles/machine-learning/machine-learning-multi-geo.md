---
title: documentazione della Guida aaaMulti geografica | Documenti Microsoft
description: Informazioni su come toocreate un'area di lavoro e pubblicare un servizio web in un'area di Azure diversa da hello meridionale centrale United States (SCUS) regione di Azure.
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="03375-103">Guida per più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="03375-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="03375-104">Questo articolo illustra come creare un'area di lavoro e pubblicare un servizio Web in altre aree geografiche di Azure.</span><span class="sxs-lookup"><span data-stu-id="03375-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="03375-105">Hello [prodotti Azure dalla pagina area](https://azure.microsoft.com/en-us/regions/services/) sono elencate le aree in cui Azure Machine Learning è disponibile.</span><span class="sxs-lookup"><span data-stu-id="03375-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="03375-106">Creare un'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="03375-106">Create a workspace</span></span>
1. <span data-ttu-id="03375-107">Accedi toohello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="03375-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="03375-108">Fare clic su **+ NUOVO** > **SERVIZI DATI** > **MACHINE LEARNING** > **CREAZIONE RAPIDA**.</span><span class="sxs-lookup"><span data-stu-id="03375-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="03375-109">In **INDIRIZZO** selezionare un'altra area, ad esempio **Asia sud-orientale**.</span><span class="sxs-lookup"><span data-stu-id="03375-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="03375-110">![Guida per più aree geografiche immagine 1][1]</span><span class="sxs-lookup"><span data-stu-id="03375-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="03375-111">Selezionare l'area di lavoro hello e quindi fare clic su **Accedi tooML Studio**.</span><span class="sxs-lookup"><span data-stu-id="03375-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="03375-112">![Guida per più aree geografiche immagine 2][2]</span><span class="sxs-lookup"><span data-stu-id="03375-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="03375-113">Ora si dispone di un'area di lavoro in un'altra area geografica che può essere utilizzata come qualsiasi altra area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="03375-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="03375-114">tooswitch tra le aree di lavoro, aspetto toohello superiore destro dello schermo.</span><span class="sxs-lookup"><span data-stu-id="03375-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="03375-115">Fare clic su elenco a discesa hello, hello selezionare area e area di lavoro selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="03375-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="03375-116">Tutti gli elementi è l'area dell'area di lavoro locale toohello.</span><span class="sxs-lookup"><span data-stu-id="03375-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="03375-117">Ad esempio, i servizi web creati da un'area di lavoro si trovano nella stessa area di lavoro area hello hello.</span><span class="sxs-lookup"><span data-stu-id="03375-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="03375-118">![Guida per più aree geografiche immagine 3][3]</span><span class="sxs-lookup"><span data-stu-id="03375-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="03375-119">Aprire un esperimento dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="03375-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="03375-120">Se si apre un esperimento dalla raccolta, è possibile selezionare l'area da toocopy hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="03375-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Guida per più aree geografiche immagine 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="03375-122">Gestione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="03375-122">Web service management</span></span>
<span data-ttu-id="03375-123">tooprogrammatically gestire servizi web, ad esempio per la ripetizione di training, Usa hello specifiche indirizzo:</span><span class="sxs-lookup"><span data-stu-id="03375-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="03375-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="03375-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="03375-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="03375-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="03375-126">Operazioni toonote</span><span class="sxs-lookup"><span data-stu-id="03375-126">Things toonote</span></span>
1. <span data-ttu-id="03375-127">È possibile copiare solo esperimenti tra aree di lavoro che appartengono toohello stessa area in questo modo.</span><span class="sxs-lookup"><span data-stu-id="03375-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="03375-128">Se è necessario toocopy esperimento nelle aree di lavoro in aree diverse, è possibile utilizzare hello [PowerShell](http://aka.ms/amlps) cmdlet [ *copia AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish che.</span><span class="sxs-lookup"><span data-stu-id="03375-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="03375-129">Un'altra soluzione alternativa è toopublish hello esperimento nella raccolta in modalità non in elenco, quindi aprirlo nell'area di lavoro hello hello altre aree.</span><span class="sxs-lookup"><span data-stu-id="03375-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="03375-130">selettore di Hello area verrà visualizzate solo le aree di lavoro per un'area alla volta.</span><span class="sxs-lookup"><span data-stu-id="03375-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="03375-131">Un’area di lavoro con accesso libero o Guest (anonimo) verrà creata e ospitata in Stati Uniti centro-meridionali.</span><span class="sxs-lookup"><span data-stu-id="03375-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="03375-132">I servizi Web distribuiti da un'area di lavoro nell’Asia sudorientale verranno anche ospitati in Asia sudorientale.</span><span class="sxs-lookup"><span data-stu-id="03375-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="03375-133">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="03375-133">More information</span></span>
<span data-ttu-id="03375-134">Porre una domanda su hello [forum di Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="03375-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
