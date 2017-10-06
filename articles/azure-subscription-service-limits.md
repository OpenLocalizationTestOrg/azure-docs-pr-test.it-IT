---
title: sottoscrizione aaaAzure limiti e quote | Documenti Microsoft
description: Fornisce un elenco di limiti, quote e vincoli comuni relativi alle sottoscrizioni e ai servizi di Azure. Sono incluse informazioni su come tooincrease limita insieme ai valori massimi.
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="5969a-104">Sottoscrizione di Azure e limiti, quote e vincoli dei servizi</span><span class="sxs-lookup"><span data-stu-id="5969a-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="5969a-105">Questo documento sono elencati alcuni dei limiti Microsoft Azure più comuni hello, che vengono definiti anche le quote.</span><span class="sxs-lookup"><span data-stu-id="5969a-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="5969a-106">Al momento nel documento non vengono trattati tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="5969a-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="5969a-107">Nel corso del tempo, elenco hello verrà espanso e aggiornato toocover ulteriori della piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="5969a-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="5969a-108">Visitare [panoramica dei prezzi di Azure](https://azure.microsoft.com/pricing/) toolearn più sui prezzi di Azure.</span><span class="sxs-lookup"><span data-stu-id="5969a-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="5969a-109">Non esiste, è possibile stimare i costi utilizzando hello [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/) o visitando hello prezzi pagina dei dettagli per un servizio (ad esempio, [macchine virtuali Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="5969a-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="5969a-110">Per suggerimenti toohelp gestire i costi, vedere [evitare i costi imprevisti con la fatturazione di Azure e gestione dei costi](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5969a-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5969a-111">Se si desidera che il limite di hello tooraise o quota sopra hello **limite predefinito**, [aprire una richiesta di supporto clienti online senza costi](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="5969a-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="5969a-112">Hello limiti non possono essere generati in precedenza hello **limite massimo** valore mostrato in hello le tabelle seguenti.</span><span class="sxs-lookup"><span data-stu-id="5969a-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="5969a-113">Se è presente alcun **limite massimo** colonna, quindi risorse hello non ha limiti di variabili.</span><span class="sxs-lookup"><span data-stu-id="5969a-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="5969a-114">Le sottoscrizioni per le versioni di valutazione gratuite non sono idonee ad aumenti di limite o di quota.</span><span class="sxs-lookup"><span data-stu-id="5969a-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="5969a-115">Se si dispone di una versione di valutazione gratuita, è possibile aggiornare tooa [consumo](https://azure.microsoft.com/offers/ms-azr-0003p/) sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5969a-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="5969a-116">Per ulteriori informazioni, vedere [aggiornare Azure versione di valutazione gratuita tooPay-come-di-Go](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="5969a-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="5969a-117">Limiti e hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5969a-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="5969a-118">È ora possibile toocombine più risorse di Azure in tooa singolo gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5969a-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="5969a-119">Quando si utilizzano gruppi di risorse, i limiti di una volta sono globali gestiti a un livello regionale con hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5969a-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="5969a-120">Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5969a-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="5969a-121">Nei limiti di hello seguito, una nuova tabella è stato aggiunto tooreflect eventuali differenze nei limiti quando si utilizza hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5969a-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="5969a-122">Sono ad esempio presenti una tabella **Limiti delle sottoscrizioni** e una tabella **Limiti delle sottoscrizioni - Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="5969a-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="5969a-123">Quando un limite si applica tooboth scenari, viene visualizzata solo nella prima tabella hello.</span><span class="sxs-lookup"><span data-stu-id="5969a-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="5969a-124">Se non diversamente indicato, i limiti sono globali in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="5969a-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="5969a-125">È importante tooemphasize quote per le risorse in gruppi di risorse di Azure vengono per ogni area accessibile dalla sottoscrizione che non sono per ogni sottoscrizione, sono le quote di Gestione servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5969a-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="5969a-126">Si considerino, ad esempio. le quote relative ai core.</span><span class="sxs-lookup"><span data-stu-id="5969a-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="5969a-127">Se è necessario toorequest aumentare una quota con il supporto per core, è necessario come toodecide molti core toouse in quali aree desiderato e quindi effettuare una richiesta specifica per il gruppo di risorse di Azure le quote di base per gli importi hello e aree che si desidera.</span><span class="sxs-lookup"><span data-stu-id="5969a-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="5969a-128">Pertanto, se è necessario toouse 30 core in Europa occidentale toorun l'applicazione. in particolare, è necessario richiedere 30 core in Europa occidentale.</span><span class="sxs-lookup"><span data-stu-id="5969a-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="5969a-129">Ma non si avrà una quota di core aumentare in qualsiasi altra area - solo Europa occidentale avrà una quota di core 30 hello.</span><span class="sxs-lookup"><span data-stu-id="5969a-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="5969a-130">Di conseguenza, può risultare utile tooconsider decidere quali le quote del gruppo di risorse di Azure devono toobe il carico di lavoro in qualsiasi uno area e richiesta che importo in ogni area in cui si sta considerando la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5969a-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="5969a-131">Per altre informazioni su come individuare le quote correnti per aree specifiche, vedere l'argomento relativo alla [risoluzione dei problemi di distribuzione](resource-manager-common-deployment-errors.md) .</span><span class="sxs-lookup"><span data-stu-id="5969a-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="5969a-132">Limiti specifici del servizio</span><span class="sxs-lookup"><span data-stu-id="5969a-132">Service-specific limits</span></span>
* [<span data-ttu-id="5969a-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="5969a-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="5969a-134">Gestione API</span><span class="sxs-lookup"><span data-stu-id="5969a-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="5969a-135">Servizio app</span><span class="sxs-lookup"><span data-stu-id="5969a-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="5969a-136">Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="5969a-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="5969a-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="5969a-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="5969a-138">Automazione</span><span class="sxs-lookup"><span data-stu-id="5969a-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="5969a-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5969a-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="5969a-140">Griglia di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="5969a-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="5969a-141">Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="5969a-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="5969a-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5969a-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="5969a-143">Backup</span><span class="sxs-lookup"><span data-stu-id="5969a-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="5969a-144">Batch</span><span class="sxs-lookup"><span data-stu-id="5969a-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="5969a-145">Servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="5969a-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="5969a-146">RETE CDN</span><span class="sxs-lookup"><span data-stu-id="5969a-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="5969a-147">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="5969a-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="5969a-148">Istanze di contenitore</span><span class="sxs-lookup"><span data-stu-id="5969a-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="5969a-149">Data Factory</span><span class="sxs-lookup"><span data-stu-id="5969a-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="5969a-150">Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="5969a-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="5969a-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5969a-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="5969a-152">DNS</span><span class="sxs-lookup"><span data-stu-id="5969a-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="5969a-153">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="5969a-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="5969a-154">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="5969a-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="5969a-155">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="5969a-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="5969a-156">Log Analytics/Operational Insights</span><span class="sxs-lookup"><span data-stu-id="5969a-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="5969a-157">Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5969a-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="5969a-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5969a-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="5969a-159">Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="5969a-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="5969a-160">Monitorare</span><span class="sxs-lookup"><span data-stu-id="5969a-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="5969a-161">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5969a-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="5969a-162">Rete</span><span class="sxs-lookup"><span data-stu-id="5969a-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="5969a-163">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="5969a-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="5969a-164">Servizio di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="5969a-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="5969a-165">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5969a-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="5969a-166">Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="5969a-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="5969a-167">Search</span><span class="sxs-lookup"><span data-stu-id="5969a-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="5969a-168">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="5969a-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="5969a-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5969a-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="5969a-170">Database SQL</span><span class="sxs-lookup"><span data-stu-id="5969a-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="5969a-171">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="5969a-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="5969a-172">Sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="5969a-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="5969a-173">Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="5969a-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="5969a-174">Sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="5969a-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="5969a-175">Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="5969a-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="5969a-176">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5969a-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="5969a-177">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5969a-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="5969a-178">Limiti delle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="5969a-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="5969a-179">Limiti delle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="5969a-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="5969a-180">Limiti delle sottoscrizioni - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5969a-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="5969a-181">Hello seguendo i limiti si applica quando si usa Azure Resource Manager hello e gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5969a-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="5969a-182">I limiti che non sono stati modificati con hello Azure Resource Manager non sono elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="5969a-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="5969a-183">Per tali limiti, vedere la tabella precedente toohello.</span><span class="sxs-lookup"><span data-stu-id="5969a-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="5969a-184">Per informazioni sulla gestione dei limiti nelle richieste di Resource Manager, vedere [Throttling Resource Manager requests](resource-manager-request-limits.md) (Limitazione delle richieste di Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5969a-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="5969a-185">Limiti relativi a Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5969a-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="5969a-186">Limiti relativi a Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5969a-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="5969a-187">Limiti relativi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5969a-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="5969a-188">Limiti relativi a Macchine virtuali - Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="5969a-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="5969a-189">Hello seguendo i limiti si applica quando si usa Azure Resource Manager hello e gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5969a-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="5969a-190">I limiti che non sono stati modificati con hello Azure Resource Manager non sono elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="5969a-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="5969a-191">Per tali limiti, vedere la tabella precedente toohello.</span><span class="sxs-lookup"><span data-stu-id="5969a-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="5969a-192">Limiti dei set di scalabilità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5969a-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="5969a-193">Limiti per Istanze di contenitore</span><span class="sxs-lookup"><span data-stu-id="5969a-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="5969a-194">Limiti relativi alla rete</span><span class="sxs-lookup"><span data-stu-id="5969a-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="5969a-195">Limiti relativi alla rete</span><span class="sxs-lookup"><span data-stu-id="5969a-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="5969a-196">Limiti del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="5969a-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="5969a-197">Limiti relativi a Network Watcher</span><span class="sxs-lookup"><span data-stu-id="5969a-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="5969a-198">Limiti relativi a Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="5969a-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="5969a-199">Limiti relativi a DNS</span><span class="sxs-lookup"><span data-stu-id="5969a-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="5969a-200">Limiti relativi ad Archiviazione</span><span class="sxs-lookup"><span data-stu-id="5969a-200">Storage limits</span></span>
<span data-ttu-id="5969a-201">Per altre informazioni sui limiti dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="5969a-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="5969a-202">Limiti relativi al servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="5969a-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="5969a-203">Limiti relativi ai dischi della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5969a-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="5969a-204">Vedere [Dimensioni della macchina virtuale](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="5969a-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="5969a-205">Dischi delle macchine virtuali gestiti</span><span class="sxs-lookup"><span data-stu-id="5969a-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="5969a-206">Dischi delle macchine virtuali non gestiti</span><span class="sxs-lookup"><span data-stu-id="5969a-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="5969a-207">Limiti relativi al provider di risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="5969a-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="5969a-208">Limiti relativi a Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="5969a-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="5969a-209">Limiti relativi a Servizio app</span><span class="sxs-lookup"><span data-stu-id="5969a-209">App Service limits</span></span>
<span data-ttu-id="5969a-210">seguente Hello limiti di servizio App includono i limiti per le applicazioni Web, applicazioni per dispositivi mobili, App per le API e App per la logica.</span><span class="sxs-lookup"><span data-stu-id="5969a-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="5969a-211">Limiti relativi all'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="5969a-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="5969a-212">Limiti relativi a Batch</span><span class="sxs-lookup"><span data-stu-id="5969a-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="5969a-213">Limiti relativi a Servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="5969a-213">BizTalk Services limits</span></span>
<span data-ttu-id="5969a-214">Hello nella tabella seguente mostra i limiti di hello servizi Biztalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="5969a-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="5969a-215">Limiti relativi ad Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5969a-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="5969a-216">DB Cosmos Azure è un database su scala globale in cui la velocità effettiva e l'archiviazione può essere scalato toohandle qualsiasi richiede l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5969a-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="5969a-217">Se si dispone di domande su scala hello Azure Cosmos DB fornisce, inviare posta elettronica tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="5969a-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="5969a-218">Limiti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5969a-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="5969a-219">Limiti relativi a Ricerca</span><span class="sxs-lookup"><span data-stu-id="5969a-219">Search limits</span></span>
<span data-ttu-id="5969a-220">Piani tariffari determinano la capacità di hello e i limiti del servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="5969a-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="5969a-221">Sono disponibili i piani seguenti:</span><span class="sxs-lookup"><span data-stu-id="5969a-221">Tiers include:</span></span>

* <span data-ttu-id="5969a-222">*Gratuito* , offre un servizio multi-tenant, condiviso con altri sottoscrittori di Azure, progettato per la valutazione e progetti di sviluppo di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="5969a-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="5969a-223">*Base* fornisce risorse di elaborazione dedicate per i carichi di lavoro in scala ridotta, con le repliche toothree per carichi di lavoro di query a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="5969a-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="5969a-224">*Standard (S1, S2, S3, S3 ad alta densità)* è per i carichi di lavoro di produzione più consistenti.</span><span class="sxs-lookup"><span data-stu-id="5969a-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="5969a-225">Più livelli esistono all'interno del livello standard hello in modo che sia possibile scegliere una configurazione di risorsa che corrisponde maggiormente il profilo di carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5969a-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="5969a-226">**Limiti per ogni sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="5969a-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="5969a-227">**Limiti per servizio di ricerca**</span><span class="sxs-lookup"><span data-stu-id="5969a-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="5969a-228">toolearn ulteriori informazioni sui limiti di un livello più granulare, ad esempio dimensioni del documento, le query al secondo, le chiavi, le richieste e risposte, vedere [limiti in ricerca di Azure del servizio](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="5969a-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="5969a-229">Limiti relativi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5969a-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="5969a-230">Limiti relativi alla rete CDN</span><span class="sxs-lookup"><span data-stu-id="5969a-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="5969a-231">Limiti relativi a Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="5969a-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="5969a-232">Limiti relativi al monitoraggio</span><span class="sxs-lookup"><span data-stu-id="5969a-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="5969a-233">Limiti relativi al servizio di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="5969a-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="5969a-234">Limiti relativi all'hub eventi</span><span class="sxs-lookup"><span data-stu-id="5969a-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="5969a-235">Limiti relativi al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="5969a-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="5969a-236">Limiti relativi all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5969a-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="5969a-237">Limiti relativi a Data factory</span><span class="sxs-lookup"><span data-stu-id="5969a-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="5969a-238">Limiti di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5969a-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="5969a-239">Limiti di Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5969a-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="5969a-240">Limiti relativi ad analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="5969a-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="5969a-241">Limiti relativi ad Active Directory</span><span class="sxs-lookup"><span data-stu-id="5969a-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="5969a-242">Limiti relativi a Griglia di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="5969a-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="5969a-243">Limiti relativi a RemoteApp di Azure</span><span class="sxs-lookup"><span data-stu-id="5969a-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="5969a-244">Limiti relativi al sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="5969a-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="5969a-245">Limiti relativi a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5969a-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="5969a-246">Limiti relativi a Backup</span><span class="sxs-lookup"><span data-stu-id="5969a-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="5969a-247">Limiti relativi a Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5969a-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="5969a-248">Limiti relativi ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="5969a-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="5969a-249">Limiti relativi a Gestione API</span><span class="sxs-lookup"><span data-stu-id="5969a-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="5969a-250">Limiti relativi a Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="5969a-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="5969a-251">Limiti relativi all'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="5969a-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="5969a-252">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="5969a-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="5969a-253">Limiti di automazione</span><span class="sxs-lookup"><span data-stu-id="5969a-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="5969a-254">Limiti relativi a database SQL</span><span class="sxs-lookup"><span data-stu-id="5969a-254">SQL Database limits</span></span>
<span data-ttu-id="5969a-255">Per i limiti di Database SQL, vedere [Limiti delle risorse dei Database SQL](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="5969a-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5969a-256">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5969a-256">See also</span></span>
[<span data-ttu-id="5969a-257">Informazioni sui limiti di Azure e su come aumentarli</span><span class="sxs-lookup"><span data-stu-id="5969a-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="5969a-258">Dimensioni delle macchine virtuali e dei servizi cloud per Azure</span><span class="sxs-lookup"><span data-stu-id="5969a-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="5969a-259">Dimensioni per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="5969a-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

