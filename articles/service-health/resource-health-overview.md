---
title: Panoramica dello stato delle risorse aaaAzure | Documenti Microsoft
description: "Panoramica su Integrità risorse di Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="07b38-103">Panoramica su Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="07b38-103">Azure resource health overview</span></span>
 
<span data-ttu-id="07b38-104">Integrità risorse consente di eseguire una diagnosi e di ottenere supporto quando un problema di Azure ha effetto sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="07b38-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="07b38-105">Informato dello stato corrente e precedenti hello delle risorse e consente di attenuare i problemi.</span><span class="sxs-lookup"><span data-stu-id="07b38-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="07b38-106">Integrità risorse offre supporto tecnico quando è necessaria assistenza per problemi con i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="07b38-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="07b38-107">Mentre [stato Azure](https://status.azure.com) informare sui problemi di servizio che interessano una vasta gamma di clienti di Azure, l'integrità delle risorse offre un dashboard di integrità hello delle risorse personalizzato.</span><span class="sxs-lookup"><span data-stu-id="07b38-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="07b38-108">Integrità delle risorse viene sempre hello le risorse non sono disponibili in hello scaduta tooAzure i problemi del servizio.</span><span class="sxs-lookup"><span data-stu-id="07b38-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="07b38-109">Questo rende semplice per è toounderstand se è stato violato un contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="07b38-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="07b38-110">Qual è la definizione di "risorsa" e in che modo Integrità risorse stabilisce se una risorsa è integra o meno?</span><span class="sxs-lookup"><span data-stu-id="07b38-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="07b38-111">Una risorsa è un'istanza di un tipo di risorsa messo a disposizione da un servizio di Azure tramite Azure Resource Manager, ad esempio una macchina virtuale, un'app Web o un database SQL.</span><span class="sxs-lookup"><span data-stu-id="07b38-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="07b38-112">Integrità delle risorse si basa su segnali emessi da hello diversi servizi Azure tooassess se una risorsa è integro o non.</span><span class="sxs-lookup"><span data-stu-id="07b38-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="07b38-113">Se una risorsa non è integra, integrità delle risorse analizza le informazioni aggiuntive toodetermine hello causa hello problema.</span><span class="sxs-lookup"><span data-stu-id="07b38-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="07b38-114">Vengono inoltre identificati azioni che richiede Microsoft problema hello toofix o quali azioni da eseguire tooaddress hello causano del problema hello.</span><span class="sxs-lookup"><span data-stu-id="07b38-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="07b38-115">Elenco completo di hello revisione dei tipi di risorse e l'integrità controlla [integrità delle risorse Azure](resource-health-checks-resource-types.md) per ulteriori informazioni sulle modalità di valutazione di integrità.</span><span class="sxs-lookup"><span data-stu-id="07b38-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="07b38-116">Stato di integrità indicato da Integrità risorse</span><span class="sxs-lookup"><span data-stu-id="07b38-116">Health status provided by resource health</span></span>
<span data-ttu-id="07b38-117">integrità Hello di una risorsa è uno dei seguenti stati hello:</span><span class="sxs-lookup"><span data-stu-id="07b38-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="07b38-118">Disponibile</span><span class="sxs-lookup"><span data-stu-id="07b38-118">Available</span></span>
<span data-ttu-id="07b38-119">servizio Hello non è stata rilevata tutti gli eventi che hanno un impatto integrità hello della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="07b38-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="07b38-120">Nei casi in cui risorse hello è stata ripristinata da tempi di inattività imprevisti durante hello ultime 24 ore, verrà visualizzato hello **ripristinato di recente** notifica.</span><span class="sxs-lookup"><span data-stu-id="07b38-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Integrità risorse: macchina virtuale con stato Disponibile](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="07b38-122">Non disponibile</span><span class="sxs-lookup"><span data-stu-id="07b38-122">Unavailable</span></span>
<span data-ttu-id="07b38-123">Hello servizio ha rilevato un evento di non piattaforma conseguenze integrità hello della risorsa hello o di piattaforma in corso.</span><span class="sxs-lookup"><span data-stu-id="07b38-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="07b38-124">Eventi piattaforma</span><span class="sxs-lookup"><span data-stu-id="07b38-124">Platform events</span></span>
<span data-ttu-id="07b38-125">Questi eventi vengono attivati da più componenti di infrastruttura di Azure hello e includono sia azioni pianificate come la manutenzione pianificata e gli eventi imprevisti imprevisti come il riavvio di un host non pianificato.</span><span class="sxs-lookup"><span data-stu-id="07b38-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="07b38-126">Integrità delle risorse sono disponibili ulteriori dettagli sull'evento hello, il processo di ripristino di hello e consente il supporto toocontact anche se non si dispone di Microsoft active contratto di supporto.</span><span class="sxs-lookup"><span data-stu-id="07b38-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Risorsa integrità disponibile macchina virtuale a causa di eventi tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="07b38-128">Eventi non piattaforma</span><span class="sxs-lookup"><span data-stu-id="07b38-128">Non-Platform events</span></span>
<span data-ttu-id="07b38-129">Questi eventi vengono attivati da azioni eseguite dagli utenti, ad esempio l'arresto di una macchina virtuale o raggiungere hello il numero massimo di connessioni tooa Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="07b38-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Risorsa integrità disponibile macchina virtuale a causa di evento toonon piattaforma](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="07b38-131">Sconosciuto</span><span class="sxs-lookup"><span data-stu-id="07b38-131">Unknown</span></span>
<span data-ttu-id="07b38-132">Questo stato indica che Integrità risorse non ha ricevuto informazioni sulla risorsa per più di 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="07b38-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="07b38-133">Sebbene questo stato non è un'indicazione dello stato di hello della risorsa hello definitiva, è un punto dati importanti nel processo di risoluzione dei problemi di hello:</span><span class="sxs-lookup"><span data-stu-id="07b38-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="07b38-134">Se la risorsa hello è in esecuzione allo stato previsto hello della risorsa hello aggiornerà tooAvailable dopo alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="07b38-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="07b38-135">Se si verificano problemi con la risorsa hello, hello lo stato di integrità sconosciuto può suggerire risorse hello sono stata interessata da un evento nella piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="07b38-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Integrità risorse: macchina virtuale con stato Sconosciuto](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="07b38-137">Segnalare uno stato non corretto</span><span class="sxs-lookup"><span data-stu-id="07b38-137">Report an incorrect status</span></span>
<span data-ttu-id="07b38-138">Se in qualsiasi momento si ritiene che lo stato di integrità corrente hello è corretto, è possibile segnalarlo facendo **segnalare lo stato di integrità corretto**.</span><span class="sxs-lookup"><span data-stu-id="07b38-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="07b38-139">Nei casi in cui sono interessati da un problema di Azure, si consiglia di supporto toocontact dal pannello integrità della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="07b38-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Integrità risorse: report di stato non corretto](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="07b38-141">Informazioni sulla cronologia</span><span class="sxs-lookup"><span data-stu-id="07b38-141">Historical Information</span></span>
<span data-ttu-id="07b38-142">I giorni too14 dei dati cronologici di integrità di cui è possibile accedere facendo clic su **Visualizza cronologia** nel Pannello di integrità risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="07b38-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Integrità risorse: report della cronologia](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="07b38-144">introduttiva</span><span class="sxs-lookup"><span data-stu-id="07b38-144">Getting started</span></span>
<span data-ttu-id="07b38-145">tooopen integrità delle risorse per una risorsa</span><span class="sxs-lookup"><span data-stu-id="07b38-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="07b38-146">Accedere in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07b38-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="07b38-147">Passare tooyour risorse.</span><span class="sxs-lookup"><span data-stu-id="07b38-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="07b38-148">Scegliere dal menu risorse hello si trova nella parte sinistra hello **integrità delle risorse**.</span><span class="sxs-lookup"><span data-stu-id="07b38-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Aprire Integrità risorse dal pannello della risorsa](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="07b38-150">È inoltre possibile accedere integrità delle risorse facendo **più servizi**e digitando **integrità delle risorse** in hello tooopen casella testo di filtro **della Guida e supporto** blade.</span><span class="sxs-lookup"><span data-stu-id="07b38-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="07b38-151">Infine fare clic su [**Integrità risorse**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="07b38-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Aprire Integrità risorse da Altri servizi](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="07b38-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07b38-153">Next steps</span></span>

<span data-ttu-id="07b38-154">Consultare queste risorse toolearn più sull'integrità delle risorse:</span><span class="sxs-lookup"><span data-stu-id="07b38-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="07b38-155">Tipi di risorse e controlli di integrità in Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="07b38-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="07b38-156">Domande frequenti su Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="07b38-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




