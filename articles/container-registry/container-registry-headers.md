---
title: repository del Registro di sistema di contenitore aaaAzure | Documenti Microsoft
description: Il repository del Registro di sistema di Azure contenitore toouse per le immagini Docker
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="cc961-103">Archivi di registri contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cc961-103">Azure container registry repositories</span></span>

<span data-ttu-id="cc961-104">I registri contenitori di Azure sono compatibili con una vasta gamma di servizi e agenti di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="cc961-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="cc961-105">toomake è più facile tootrack hello origine i servizi e gli agenti da cui viene utilizzato ACR, abbiamo iniziato con campo di intestazione hello Docker nel file Docker.config hello.</span><span class="sxs-lookup"><span data-stu-id="cc961-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="cc961-106">Visualizzazione di repository in hello portale</span><span class="sxs-lookup"><span data-stu-id="cc961-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="cc961-107">intestazioni ACR Hello seguono il formato di hello:</span><span class="sxs-lookup"><span data-stu-id="cc961-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="cc961-108">Cloud: Azure, Azure Stack o altri cloud di Azure per enti pubblici o paesi specifici.</span><span class="sxs-lookup"><span data-stu-id="cc961-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="cc961-109">Anche se Azure Stack e i cloud per enti pubblici non sono attualmente supportati, questo parametro consente il supporto futuro.</span><span class="sxs-lookup"><span data-stu-id="cc961-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="cc961-110">Servizio: nome del servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="cc961-110">Service: name of hello service.</span></span>
* <span data-ttu-id="cc961-111">Optionalservicename: parametro facoltativo per i servizi con i servizi secondari o toospecify uno SKU (ex: corrispondono App web con Azure/app-servizio/web-App).</span><span class="sxs-lookup"><span data-stu-id="cc961-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="cc961-112">Orchestrators e servizi dei partner sono invitati toouse intestazione specifici valori toohelp con i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="cc961-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="cc961-113">Gli utenti possono inoltre modificare il valore di hello passato toohello intestazione se desiderano.</span><span class="sxs-lookup"><span data-stu-id="cc961-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="cc961-114">di seguito sono valori Hello si vuole creare ACR partner toouse toopopulate hello "X-Meta-origine-Client" campo:</span><span class="sxs-lookup"><span data-stu-id="cc961-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="cc961-115">Nome servizio</span><span class="sxs-lookup"><span data-stu-id="cc961-115">Service Name</span></span>              | <span data-ttu-id="cc961-116">Intestazione</span><span class="sxs-lookup"><span data-stu-id="cc961-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="cc961-117">Servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="cc961-117">Azure Container Service</span></span>   | <span data-ttu-id="cc961-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="cc961-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="cc961-119">Servizio app - App Web</span><span class="sxs-lookup"><span data-stu-id="cc961-119">App Service - Web Apps</span></span>    | <span data-ttu-id="cc961-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="cc961-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="cc961-121">Servizio app - App per la logica</span><span class="sxs-lookup"><span data-stu-id="cc961-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="cc961-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="cc961-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="cc961-123">Batch</span><span class="sxs-lookup"><span data-stu-id="cc961-123">Batch</span></span>                     | <span data-ttu-id="cc961-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="cc961-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="cc961-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="cc961-125">Cloud Console</span></span>             | <span data-ttu-id="cc961-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="cc961-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="cc961-127">Funzioni</span><span class="sxs-lookup"><span data-stu-id="cc961-127">Functions</span></span>                 | <span data-ttu-id="cc961-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="cc961-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="cc961-129">Internet delle cose - Hub</span><span class="sxs-lookup"><span data-stu-id="cc961-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="cc961-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="cc961-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="cc961-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc961-131">HDInsight</span></span>                 | <span data-ttu-id="cc961-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="cc961-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="cc961-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="cc961-133">Jenkins</span></span>                   | <span data-ttu-id="cc961-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="cc961-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="cc961-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cc961-135">Machine Learning</span></span>          | <span data-ttu-id="cc961-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="cc961-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="cc961-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cc961-137">Service Fabric</span></span>            | <span data-ttu-id="cc961-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="cc961-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="cc961-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="cc961-139">VSTS</span></span>                      | <span data-ttu-id="cc961-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="cc961-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="cc961-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc961-141">Next steps</span></span>
[<span data-ttu-id="cc961-142">Altre informazioni sui registri e i servizi di hello è supportato e orchestrators</span><span class="sxs-lookup"><span data-stu-id="cc961-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
