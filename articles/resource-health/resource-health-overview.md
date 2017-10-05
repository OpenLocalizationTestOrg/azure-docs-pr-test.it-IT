---
title: "Panoramica su Integrità risorse di Azure | Microsoft Docs"
description: "Panoramica su Integrità risorse di Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: d54979995ca97a70ba92c64915b919da09f548ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="e2d65-103">Panoramica su Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="e2d65-103">Azure resource health overview</span></span>
 
<span data-ttu-id="e2d65-104">Integrità risorse consente di eseguire una diagnosi e di ottenere supporto quando un problema di Azure ha effetto sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="e2d65-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="e2d65-105">Informa sull'integrità corrente e passata delle risorse e consente di attenuare i problemi.</span><span class="sxs-lookup"><span data-stu-id="e2d65-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="e2d65-106">Integrità risorse offre supporto tecnico quando è necessaria assistenza per problemi con i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2d65-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="e2d65-107">A differenza di [Stato di Azure](https://status.azure.com) che visualizza informazioni sui problemi dei servizi che interessano numerosi clienti di Azure, Integrità risorse offre un dashboard personalizzato dell'integrità delle risorse.</span><span class="sxs-lookup"><span data-stu-id="e2d65-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="e2d65-108">Integrità risorse visualizza tutte le volte in cui le risorse non sono state disponibili a causa di problemi dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2d65-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="e2d65-109">Ciò consente di individuare in modo semplice se è stato violato un contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="e2d65-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="e2d65-110">Qual è la definizione di "risorsa" e in che modo Integrità risorse stabilisce se una risorsa è integra o meno?</span><span class="sxs-lookup"><span data-stu-id="e2d65-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="e2d65-111">Una risorsa è un'istanza di un tipo di risorsa messo a disposizione da un servizio di Azure tramite Azure Resource Manager, ad esempio una macchina virtuale, un'app Web o un database SQL.</span><span class="sxs-lookup"><span data-stu-id="e2d65-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="e2d65-112">Integrità risorse si basa su segnali emessi dai diversi servizi di Azure per determinare se una risorsa è integra o meno.</span><span class="sxs-lookup"><span data-stu-id="e2d65-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="e2d65-113">Se una risorsa non è integra, Integrità risorse analizza informazioni aggiuntive per determinare l'origine del problema.</span><span class="sxs-lookup"><span data-stu-id="e2d65-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="e2d65-114">Identifica anche le azioni intraprese da Microsoft per risolvere il problema o le azioni da eseguire per eliminare la causa del problema.</span><span class="sxs-lookup"><span data-stu-id="e2d65-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="e2d65-115">Esaminare l'elenco completo dei tipi di risorse e dei controlli di integrità in [Integrità risorse di Azure](resource-health-checks-resource-types.md) per altri dettagli sulla modalità di valutazione dell'integrità.</span><span class="sxs-lookup"><span data-stu-id="e2d65-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="e2d65-116">Stato di integrità indicato da Integrità risorse</span><span class="sxs-lookup"><span data-stu-id="e2d65-116">Health status provided by resource health</span></span>
<span data-ttu-id="e2d65-117">L'integrità di una risorsa è indicata da uno degli stati seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2d65-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="e2d65-118">Disponibile</span><span class="sxs-lookup"><span data-stu-id="e2d65-118">Available</span></span>
<span data-ttu-id="e2d65-119">Il servizio non ha rilevato eventi che hanno effetto sull'integrità della risorsa.</span><span class="sxs-lookup"><span data-stu-id="e2d65-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="e2d65-120">Se la risorsa è stata ripristinata da un tempo di inattività non pianificato nelle ultime 24 ore, viene visualizzata la notifica di **recupero recente**.</span><span class="sxs-lookup"><span data-stu-id="e2d65-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![Integrità risorse: macchina virtuale con stato Disponibile](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="e2d65-122">Non disponibile</span><span class="sxs-lookup"><span data-stu-id="e2d65-122">Unavailable</span></span>
<span data-ttu-id="e2d65-123">Il servizio ha rilevato un evento piattaforma o non piattaforma in corso che ha effetto sull'integrità della risorsa.</span><span class="sxs-lookup"><span data-stu-id="e2d65-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="e2d65-124">Eventi piattaforma</span><span class="sxs-lookup"><span data-stu-id="e2d65-124">Platform events</span></span>
<span data-ttu-id="e2d65-125">Questi eventi vengono generati da più componenti dell'infrastruttura di Azure e includono azioni pianificate, ad esempio la manutenzione, ed eventi imprevisti, ad esempio un riavvio dell'host non pianificato.</span><span class="sxs-lookup"><span data-stu-id="e2d65-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="e2d65-126">Integrità risorse visualizza ulteriori dettagli sull'evento, il processo di recupero e consente di contattare il supporto tecnico anche se non si ha un contratto di supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e2d65-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![Integrità risorse: macchina virtuale con stato Non disponibile a causa di un evento piattaforma](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="e2d65-128">Eventi non piattaforma</span><span class="sxs-lookup"><span data-stu-id="e2d65-128">Non-Platform events</span></span>
<span data-ttu-id="e2d65-129">Questi eventi vengono generati da azioni eseguite dagli utenti, ad esempio l'arresto di una macchina virtuale o il raggiungimento del numero massimo di connessioni a una cache Redis.</span><span class="sxs-lookup"><span data-stu-id="e2d65-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![Integrità risorse: macchina virtuale con stato Non disponibile a causa di un evento non piattaforma](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="e2d65-131">Sconosciuto</span><span class="sxs-lookup"><span data-stu-id="e2d65-131">Unknown</span></span>
<span data-ttu-id="e2d65-132">Questo stato indica che Integrità risorse non ha ricevuto informazioni sulla risorsa per più di 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="e2d65-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="e2d65-133">Sebbene questo stato non sia un'indicazione definitiva dello stato della risorsa, è un punto dati importanti nel processo di risoluzione dei problemi:</span><span class="sxs-lookup"><span data-stu-id="e2d65-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="e2d65-134">Se la risorsa viene eseguita come previsto, lo stato della risorsa verrà aggiornato in Disponibile dopo alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="e2d65-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="e2d65-135">Se si verificano problemi con la risorsa, lo stato di integrità Sconosciuto può indicare che la risorsa è stata interessata da un evento nella piattaforma.</span><span class="sxs-lookup"><span data-stu-id="e2d65-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![Integrità risorse: macchina virtuale con stato Sconosciuto](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="e2d65-137">Segnalare uno stato non corretto</span><span class="sxs-lookup"><span data-stu-id="e2d65-137">Report an incorrect status</span></span>
<span data-ttu-id="e2d65-138">Se in qualsiasi momento si ritiene che lo stato di integrità corrente non sia corretto, è possibile inviare una segnalazione facendo clic su **Report incorrect health status** (Segnala stato integrità non corretto).</span><span class="sxs-lookup"><span data-stu-id="e2d65-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="e2d65-139">Se si verifica un problema di Azure, è consigliabile contattare il supporto tecnico dal pannello di Integrità risorse.</span><span class="sxs-lookup"><span data-stu-id="e2d65-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![Integrità risorse: report di stato non corretto](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="e2d65-141">Informazioni sulla cronologia</span><span class="sxs-lookup"><span data-stu-id="e2d65-141">Historical Information</span></span>
<span data-ttu-id="e2d65-142">È possibile accedere a un massimo di 14 giorni di dati cronologici sull'integrità facendo clic su **Visualizza cronologia** nel pannello di Integrità risorse.</span><span class="sxs-lookup"><span data-stu-id="e2d65-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![Integrità risorse: report della cronologia](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="e2d65-144">Introduzione</span><span class="sxs-lookup"><span data-stu-id="e2d65-144">Getting started</span></span>
<span data-ttu-id="e2d65-145">Per aprire Integrità risorse per una risorsa</span><span class="sxs-lookup"><span data-stu-id="e2d65-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="e2d65-146">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2d65-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="e2d65-147">Passare alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="e2d65-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="e2d65-148">Nel menu della risorsa sul lato sinistro fare clic su **Integrità risorsa**.</span><span class="sxs-lookup"><span data-stu-id="e2d65-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![Aprire Integrità risorse dal pannello della risorsa](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="e2d65-150">È anche possibile accedere a Integrità risorse facendo clic su **Altri servizi** e digitando **Integrità risorse** nella casella di testo di filtro per aprire il pannello **Guida e supporto**.</span><span class="sxs-lookup"><span data-stu-id="e2d65-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="e2d65-151">Infine fare clic su [**Integrità risorse**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="e2d65-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Aprire Integrità risorse da Altri servizi](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="e2d65-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2d65-153">Next steps</span></span>

<span data-ttu-id="e2d65-154">Per altre informazioni su Integrità risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="e2d65-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="e2d65-155">Tipi di risorse e controlli di integrità in Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="e2d65-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="e2d65-156">Domande frequenti su Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="e2d65-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




