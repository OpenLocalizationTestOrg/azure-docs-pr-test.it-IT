---
title: Limiti e quote della sottoscrizione di Azure | Microsoft Docs
description: Fornisce un elenco di limiti, quote e vincoli comuni relativi alle sottoscrizioni e ai servizi di Azure. Sono incluse informazioni su come aumentare i limiti e i valori massimi.
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
ms.openlocfilehash: a76acd67e9ba7822f2837b3c08e2ede389047f11
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="f9579-104">Sottoscrizione di Azure e limiti, quote e vincoli dei servizi</span><span class="sxs-lookup"><span data-stu-id="f9579-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="f9579-105">In questo documento sono elencati alcuni dei limiti più comuni di Microsoft Azure, che vengono definiti anche quote.</span><span class="sxs-lookup"><span data-stu-id="f9579-105">This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="f9579-106">Al momento nel documento non vengono trattati tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="f9579-107">Nel corso del tempo l'elenco verrà ampliato e aggiornato in modo da coprire un maggior numero di servizi della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="f9579-107">Over time, the list will be expanded and updated to cover more of the platform.</span></span>

<span data-ttu-id="f9579-108">Vedere [Prezzi di Azure](https://azure.microsoft.com/pricing/) per altre informazioni sui prezzi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing.</span></span> <span data-ttu-id="f9579-109">Nella pagina è possibile stimare i costi usando il [Calcolatore prezzi](https://azure.microsoft.com/pricing/calculator/) o visitando la pagina dei dettagli dei prezzi per un servizio, ad esempio [Macchine virtuali Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="f9579-109">There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="f9579-110">Per suggerimenti su come gestire i costi, vedere [Evitare costi imprevisti con la fatturazione del costi e la fatturazione di Azure](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f9579-110">For tips to help manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f9579-111">Per aumentare il limite o la quota oltre il valore **Limite predefinito**, è possibile [aprire una richiesta di assistenza clienti online senza alcun addebito](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="f9579-111">If you want to raise the limit or quota above the **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="f9579-112">I limiti non possono essere aumentati oltre il valore **Limite massimo** definito nelle tabelle seguenti.</span><span class="sxs-lookup"><span data-stu-id="f9579-112">The limits can't be raised above the **Maximum Limit** value shown in the following tables.</span></span> <span data-ttu-id="f9579-113">Se non è presente nessuna colonna **Limite massimo**, per la risorsa specificata non sono disponibili limiti regolabili.</span><span class="sxs-lookup"><span data-stu-id="f9579-113">If there is no **Maximum Limit** column, then the resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="f9579-114">Le sottoscrizioni per le versioni di valutazione gratuite non sono idonee ad aumenti di limite o di quota.</span><span class="sxs-lookup"><span data-stu-id="f9579-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="f9579-115">Se è disponibile una versione di valutazione gratuita, è possibile eseguire l'aggiornamento a una sottoscrizione con [pagamento in base al consumo](https://azure.microsoft.com/offers/ms-azr-0003p/) .</span><span class="sxs-lookup"><span data-stu-id="f9579-115">If you have a Free Trial, you can upgrade to a [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="f9579-116">Per altre informazioni, vedere [Aggiornare la versione di valutazione gratuita di Azure all'offerta con pagamento in base al consumo](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="f9579-116">For more information, see [Upgrade Azure Free Trial to Pay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-the-azure-resource-manager"></a><span data-ttu-id="f9579-117">Limiti e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f9579-117">Limits and the Azure Resource Manager</span></span>
<span data-ttu-id="f9579-118">È ora possibile combinare più risorse di Azure in un singolo gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-118">It is now possible to combine multiple Azure resources in to a single Azure Resource Group.</span></span> <span data-ttu-id="f9579-119">Quando si usano i gruppi di risorse, i limiti in precedenza globali vengono gestiti a livello di area con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-119">When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager.</span></span> <span data-ttu-id="f9579-120">Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9579-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f9579-121">Nei limiti indicati di seguito è stata aggiunta una nuova tabella che indica eventuali differenze applicate quando si usa Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-121">In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager.</span></span> <span data-ttu-id="f9579-122">Sono ad esempio presenti una tabella **Limiti delle sottoscrizioni** e una tabella **Limiti delle sottoscrizioni - Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="f9579-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="f9579-123">Quando un limite si applica a entrambi gli scenari, viene indicato solo nella prima tabella.</span><span class="sxs-lookup"><span data-stu-id="f9579-123">When a limit applies to both scenarios, it is only shown in the first table.</span></span> <span data-ttu-id="f9579-124">Se non diversamente indicato, i limiti sono globali in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="f9579-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="f9579-125">È importante sottolineare che le quote per le risorse nei gruppi di risorse di Azure sono da intendersi per ogni area accessibile dalla sottoscrizione e non per ogni sottoscrizione, come nel caso delle quote di gestione del servizio.</span><span class="sxs-lookup"><span data-stu-id="f9579-125">It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are.</span></span> <span data-ttu-id="f9579-126">Si considerino, ad esempio. le quote relative ai core.</span><span class="sxs-lookup"><span data-stu-id="f9579-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="f9579-127">Se è necessario richiedere un aumento della quota con supporto per i core, è necessario stabilire quanti core si desidera usare e in quali aree e quindi effettuare una richiesta specifica per le quote di core del gruppo di risorse di Azure per le quantità e le aree desiderate.</span><span class="sxs-lookup"><span data-stu-id="f9579-127">If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want.</span></span> <span data-ttu-id="f9579-128">Pertanto, se è necessario usare 30 core in Europa occidentale per eseguire l'applicazione, è necessario richiedere in modo specifico 30 core in Europa occidentale.</span><span class="sxs-lookup"><span data-stu-id="f9579-128">Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="f9579-129">La quota di core per le altre aree non verrà tuttavia aumentata, ma sarà disponibile una quota di 30 core solo in Europa occidentale.</span><span class="sxs-lookup"><span data-stu-id="f9579-129">But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="f9579-130">Di conseguenza, può risultare utile stabilire le quote per il gruppo di risorse di Azure necessarie per il carico di lavoro in ogni area e richiedere tale quantità in ogni area in cui si prevede di eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f9579-130">As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="f9579-131">Per altre informazioni su come individuare le quote correnti per aree specifiche, vedere l'argomento relativo alla [risoluzione dei problemi di distribuzione](resource-manager-common-deployment-errors.md) .</span><span class="sxs-lookup"><span data-stu-id="f9579-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="f9579-132">Limiti specifici del servizio</span><span class="sxs-lookup"><span data-stu-id="f9579-132">Service-specific limits</span></span>
* [<span data-ttu-id="f9579-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9579-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="f9579-134">Gestione API</span><span class="sxs-lookup"><span data-stu-id="f9579-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="f9579-135">Servizio app</span><span class="sxs-lookup"><span data-stu-id="f9579-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="f9579-136">Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f9579-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="f9579-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="f9579-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="f9579-138">Automazione</span><span class="sxs-lookup"><span data-stu-id="f9579-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="f9579-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f9579-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="f9579-140">Griglia di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="f9579-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="f9579-141">Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="f9579-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="f9579-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f9579-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="f9579-143">Backup</span><span class="sxs-lookup"><span data-stu-id="f9579-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="f9579-144">Batch</span><span class="sxs-lookup"><span data-stu-id="f9579-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="f9579-145">Servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="f9579-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="f9579-146">RETE CDN</span><span class="sxs-lookup"><span data-stu-id="f9579-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="f9579-147">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="f9579-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="f9579-148">Istanze di contenitore</span><span class="sxs-lookup"><span data-stu-id="f9579-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="f9579-149">Data Factory</span><span class="sxs-lookup"><span data-stu-id="f9579-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="f9579-150">Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="f9579-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="f9579-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f9579-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="f9579-152">DNS</span><span class="sxs-lookup"><span data-stu-id="f9579-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="f9579-153">Hub eventi</span><span class="sxs-lookup"><span data-stu-id="f9579-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="f9579-154">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="f9579-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="f9579-155">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="f9579-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="f9579-156">Log Analytics/Operational Insights</span><span class="sxs-lookup"><span data-stu-id="f9579-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="f9579-157">Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f9579-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="f9579-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f9579-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="f9579-159">Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="f9579-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="f9579-160">Monitorare</span><span class="sxs-lookup"><span data-stu-id="f9579-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="f9579-161">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="f9579-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="f9579-162">Rete</span><span class="sxs-lookup"><span data-stu-id="f9579-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="f9579-163">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f9579-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="f9579-164">Servizio di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="f9579-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="f9579-165">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f9579-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="f9579-166">Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="f9579-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="f9579-167">Search</span><span class="sxs-lookup"><span data-stu-id="f9579-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="f9579-168">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f9579-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="f9579-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f9579-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="f9579-170">Database SQL</span><span class="sxs-lookup"><span data-stu-id="f9579-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="f9579-171">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="f9579-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="f9579-172">Sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="f9579-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="f9579-173">Analisi dei flussi</span><span class="sxs-lookup"><span data-stu-id="f9579-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="f9579-174">Sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f9579-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="f9579-175">Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="f9579-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="f9579-176">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f9579-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="f9579-177">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f9579-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="f9579-178">Limiti delle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="f9579-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="f9579-179">Limiti delle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="f9579-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="f9579-180">Limiti delle sottoscrizioni - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f9579-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="f9579-181">I limiti seguenti si applicano quando si usano Gestione risorse di Azure e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-181">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="f9579-182">I limiti che non cambiano in caso di uso di Gestione risorse di Azure non sono elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f9579-182">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="f9579-183">Per tali limiti, fare riferimento alla tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="f9579-183">Please refer to the previous table for those limits.</span></span>

<span data-ttu-id="f9579-184">Per informazioni sulla gestione dei limiti nelle richieste di Resource Manager, vedere [Throttling Resource Manager requests](resource-manager-request-limits.md) (Limitazione delle richieste di Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="f9579-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="f9579-185">Limiti relativi a Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f9579-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="f9579-186">Limiti relativi a Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f9579-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="f9579-187">Limiti relativi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f9579-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="f9579-188">Limiti relativi a Macchine virtuali - Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="f9579-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="f9579-189">I limiti seguenti si applicano quando si usano Gestione risorse di Azure e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-189">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="f9579-190">I limiti che non cambiano in caso di uso di Gestione risorse di Azure non sono elencati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f9579-190">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="f9579-191">Per tali limiti, fare riferimento alla tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="f9579-191">Please refer to the previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="f9579-192">Limiti dei set di scalabilità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f9579-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="f9579-193">Limiti per Istanze di contenitore</span><span class="sxs-lookup"><span data-stu-id="f9579-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="f9579-194">Limiti relativi alla rete</span><span class="sxs-lookup"><span data-stu-id="f9579-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="f9579-195">Limiti relativi alla rete</span><span class="sxs-lookup"><span data-stu-id="f9579-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="f9579-196">Limiti del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="f9579-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="f9579-197">Limiti relativi a Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f9579-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="f9579-198">Limiti relativi a Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="f9579-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="f9579-199">Limiti relativi a DNS</span><span class="sxs-lookup"><span data-stu-id="f9579-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="f9579-200">Limiti relativi ad Archiviazione</span><span class="sxs-lookup"><span data-stu-id="f9579-200">Storage limits</span></span>
<span data-ttu-id="f9579-201">Per altre informazioni sui limiti dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="f9579-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="f9579-202">Limiti relativi al servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f9579-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="f9579-203">Limiti relativi ai dischi della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f9579-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="f9579-204">Vedere [Dimensioni della macchina virtuale](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="f9579-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="f9579-205">Dischi delle macchine virtuali gestiti</span><span class="sxs-lookup"><span data-stu-id="f9579-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="f9579-206">Dischi delle macchine virtuali non gestiti</span><span class="sxs-lookup"><span data-stu-id="f9579-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="f9579-207">Limiti relativi al provider di risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="f9579-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="f9579-208">Limiti relativi a Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="f9579-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="f9579-209">Limiti relativi a Servizio app</span><span class="sxs-lookup"><span data-stu-id="f9579-209">App Service limits</span></span>
<span data-ttu-id="f9579-210">I seguenti limiti del servizio App includono limiti per le App Web, App mobili, App API e App per la logica.</span><span class="sxs-lookup"><span data-stu-id="f9579-210">The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="f9579-211">Limiti relativi all'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="f9579-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="f9579-212">Limiti relativi a Batch</span><span class="sxs-lookup"><span data-stu-id="f9579-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="f9579-213">Limiti relativi a Servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="f9579-213">BizTalk Services limits</span></span>
<span data-ttu-id="f9579-214">La tabella seguente mostra i limiti per i servizi Biztalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9579-214">The following table shows the limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="f9579-215">Limiti relativi ad Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f9579-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="f9579-216">Azure Cosmos DB è un database con scalabilità globale in cui la velocità effettiva e lo spazio di archiviazione possono essere ridimensionati in modo da gestire qualsiasi requisito dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f9579-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled to handle whatever your application requires.</span></span> <span data-ttu-id="f9579-217">Per eventuali domande sulla scalabilità offerta da Azure Cosmos DB, inviare un messaggio di posta elettronica all'indirizzo askcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f9579-217">If you have any questions about the scale Azure Cosmos DB provides, please send email to askcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="f9579-218">Limiti relativi a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f9579-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="f9579-219">Limiti relativi a Ricerca</span><span class="sxs-lookup"><span data-stu-id="f9579-219">Search limits</span></span>
<span data-ttu-id="f9579-220">I piano tariffari determinano la capacità e i limiti del servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="f9579-220">Pricing tiers determine the capacity and limits of your search service.</span></span> <span data-ttu-id="f9579-221">Sono disponibili i piani seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9579-221">Tiers include:</span></span>

* <span data-ttu-id="f9579-222">*Gratuito* , offre un servizio multi-tenant, condiviso con altri sottoscrittori di Azure, progettato per la valutazione e progetti di sviluppo di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="f9579-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="f9579-223">*Basic* fornisce risorse di calcolo dedicate per i carichi di lavoro di produzione su scala più ridotta, con un massimo di 3 repliche per i carichi di lavoro di query a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="f9579-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.</span></span>
* <span data-ttu-id="f9579-224">*Standard (S1, S2, S3, S3 ad alta densità)* è per i carichi di lavoro di produzione più consistenti.</span><span class="sxs-lookup"><span data-stu-id="f9579-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="f9579-225">All'interno del livello standard esistono più livelli per consentire di scegliere una configurazione delle risorse ottimale per il profilo di carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f9579-225">Multiple levels exist within the standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="f9579-226">**Limiti per ogni sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="f9579-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="f9579-227">**Limiti per servizio di ricerca**</span><span class="sxs-lookup"><span data-stu-id="f9579-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="f9579-228">Per informazioni più dettagliati sui limiti, ad esempio dimensioni dei documenti, query al secondo, chiavi, richieste e risposte, vedere [Limiti dei servizi in Ricerca di Azure](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="f9579-228">To learn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="f9579-229">Limiti relativi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f9579-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="f9579-230">Limiti relativi alla rete CDN</span><span class="sxs-lookup"><span data-stu-id="f9579-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="f9579-231">Limiti relativi a Servizi mobili</span><span class="sxs-lookup"><span data-stu-id="f9579-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="f9579-232">Limiti relativi al monitoraggio</span><span class="sxs-lookup"><span data-stu-id="f9579-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="f9579-233">Limiti relativi al servizio di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="f9579-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="f9579-234">Limiti relativi all'hub eventi</span><span class="sxs-lookup"><span data-stu-id="f9579-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="f9579-235">Limiti relativi al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f9579-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="f9579-236">Limiti relativi all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="f9579-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="f9579-237">Limiti relativi a Data factory</span><span class="sxs-lookup"><span data-stu-id="f9579-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="f9579-238">Limiti di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f9579-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="f9579-239">Limiti di Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f9579-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="f9579-240">Limiti relativi ad analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="f9579-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="f9579-241">Limiti relativi ad Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9579-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="f9579-242">Limiti relativi a Griglia di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="f9579-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="f9579-243">Limiti relativi a RemoteApp di Azure</span><span class="sxs-lookup"><span data-stu-id="f9579-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="f9579-244">Limiti relativi al sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="f9579-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="f9579-245">Limiti relativi a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f9579-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="f9579-246">Limiti relativi a Backup</span><span class="sxs-lookup"><span data-stu-id="f9579-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="f9579-247">Limiti relativi a Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f9579-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="f9579-248">Limiti relativi ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="f9579-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="f9579-249">Limiti relativi a Gestione API</span><span class="sxs-lookup"><span data-stu-id="f9579-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="f9579-250">Limiti relativi a Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="f9579-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="f9579-251">Limiti relativi all'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="f9579-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="f9579-252">Autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="f9579-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="f9579-253">Limiti di automazione</span><span class="sxs-lookup"><span data-stu-id="f9579-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="f9579-254">Limiti relativi a database SQL</span><span class="sxs-lookup"><span data-stu-id="f9579-254">SQL Database limits</span></span>
<span data-ttu-id="f9579-255">Per i limiti di Database SQL, vedere [Limiti delle risorse dei Database SQL](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f9579-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f9579-256">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f9579-256">See also</span></span>
[<span data-ttu-id="f9579-257">Informazioni sui limiti di Azure e su come aumentarli</span><span class="sxs-lookup"><span data-stu-id="f9579-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="f9579-258">Dimensioni delle macchine virtuali e dei servizi cloud per Azure</span><span class="sxs-lookup"><span data-stu-id="f9579-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="f9579-259">Dimensioni per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="f9579-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

