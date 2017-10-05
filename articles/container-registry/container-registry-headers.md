---
title: Archivi di registri contenitori di Azure | Documentazione Microsoft
description: Come usare gli archivi di registri contenitori di Azure per le immagini Docker
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
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="6d4ec-103">Archivi di registri contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="6d4ec-103">Azure container registry repositories</span></span>

<span data-ttu-id="6d4ec-104">I registri contenitori di Azure sono compatibili con una vasta gamma di servizi e agenti di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="6d4ec-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="6d4ec-105">Per tenere traccia in modo più semplice dei servizi di origine e degli agenti da cui viene usato il servizio Registro contenitori di Azure, abbiamo iniziato a usare il campo di intestazione Docker nel file Docker.config.</span><span class="sxs-lookup"><span data-stu-id="6d4ec-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="6d4ec-106">Visualizzazione dei repository nel portale</span><span class="sxs-lookup"><span data-stu-id="6d4ec-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="6d4ec-107">Le intestazioni del servizio Registro contenitori di Azure hanno il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="6d4ec-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="6d4ec-108">Cloud: Azure, Azure Stack o altri cloud di Azure per enti pubblici o paesi specifici.</span><span class="sxs-lookup"><span data-stu-id="6d4ec-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="6d4ec-109">Anche se Azure Stack e i cloud per enti pubblici non sono attualmente supportati, questo parametro consente il supporto futuro.</span><span class="sxs-lookup"><span data-stu-id="6d4ec-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="6d4ec-110">Service: nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="6d4ec-110">Service: name of the service.</span></span>
* <span data-ttu-id="6d4ec-111">Optionalservicename: parametro facoltativo per i servizi con servizi secondari o per specificare un'unità SKU (ad esempio, le app Web corrispondono ad Azure/app-service/web-apps).</span><span class="sxs-lookup"><span data-stu-id="6d4ec-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="6d4ec-112">I partner sono invitati a usare valori di intestazione specifici per i loro servizi e agenti di orchestrazione, in modo da agevolare la raccolta dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6d4ec-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="6d4ec-113">Gli utenti possono anche modificare il valore passato all'intestazione, se necessario.</span><span class="sxs-lookup"><span data-stu-id="6d4ec-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="6d4ec-114">Di seguito sono indicati i valori che viene richiesto di usare ai partner del servizio Registro contenitori di Azure per il campo "X-Meta-Source-Client":</span><span class="sxs-lookup"><span data-stu-id="6d4ec-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="6d4ec-115">Nome servizio</span><span class="sxs-lookup"><span data-stu-id="6d4ec-115">Service Name</span></span>              | <span data-ttu-id="6d4ec-116">Intestazione</span><span class="sxs-lookup"><span data-stu-id="6d4ec-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="6d4ec-117">Servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6d4ec-117">Azure Container Service</span></span>   | <span data-ttu-id="6d4ec-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="6d4ec-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="6d4ec-119">Servizio app - App Web</span><span class="sxs-lookup"><span data-stu-id="6d4ec-119">App Service - Web Apps</span></span>    | <span data-ttu-id="6d4ec-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="6d4ec-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="6d4ec-121">Servizio app - App per la logica</span><span class="sxs-lookup"><span data-stu-id="6d4ec-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="6d4ec-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="6d4ec-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="6d4ec-123">Batch</span><span class="sxs-lookup"><span data-stu-id="6d4ec-123">Batch</span></span>                     | <span data-ttu-id="6d4ec-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="6d4ec-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="6d4ec-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="6d4ec-125">Cloud Console</span></span>             | <span data-ttu-id="6d4ec-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="6d4ec-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="6d4ec-127">Funzioni</span><span class="sxs-lookup"><span data-stu-id="6d4ec-127">Functions</span></span>                 | <span data-ttu-id="6d4ec-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="6d4ec-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="6d4ec-129">Internet delle cose - Hub</span><span class="sxs-lookup"><span data-stu-id="6d4ec-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="6d4ec-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="6d4ec-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="6d4ec-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="6d4ec-131">HDInsight</span></span>                 | <span data-ttu-id="6d4ec-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="6d4ec-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="6d4ec-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="6d4ec-133">Jenkins</span></span>                   | <span data-ttu-id="6d4ec-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="6d4ec-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="6d4ec-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6d4ec-135">Machine Learning</span></span>          | <span data-ttu-id="6d4ec-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="6d4ec-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="6d4ec-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d4ec-137">Service Fabric</span></span>            | <span data-ttu-id="6d4ec-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="6d4ec-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="6d4ec-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="6d4ec-139">VSTS</span></span>                      | <span data-ttu-id="6d4ec-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="6d4ec-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="6d4ec-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6d4ec-141">Next steps</span></span>
[<span data-ttu-id="6d4ec-142">Altre informazioni sui registri e i servizi e gli agenti di orchestrazione supportati</span><span class="sxs-lookup"><span data-stu-id="6d4ec-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
