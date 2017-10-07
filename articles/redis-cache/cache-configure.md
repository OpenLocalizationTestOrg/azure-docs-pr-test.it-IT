---
title: aaaHow tooconfigure Cache Redis di Azure | Documenti Microsoft
description: Informazioni di configurazione di hello predefinita Redis per Cache Redis di Azure e informazioni su come tooconfigure di Azure Redis nella Cache istanze
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="ee4da-103">La modalità di Cache Redis di Azure di tooconfigure</span><span class="sxs-lookup"><span data-stu-id="ee4da-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="ee4da-104">In questo argomento viene descritto come hello tooreview e aggiornamento configurazione per le istanze di Cache Redis di Azure e configurazione server Redis copre hello predefinita per le istanze di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4da-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="ee4da-105">Per ulteriori informazioni sulla configurazione e utilizzo funzionalità di cache premium, vedere [come persistenza tooconfigure](cache-how-to-premium-persistence.md), [come tooconfigure clustering](cache-how-to-premium-clustering.md), e [supporto delle tooconfigure rete virtuale ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="ee4da-106">Configurare le impostazioni di Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="ee4da-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="ee4da-107">Impostazioni Cache Redis di Azure vengono visualizzate e configurate in hello **Cache Redis** pannello utilizzando hello **risorsa Menu**.</span><span class="sxs-lookup"><span data-stu-id="ee4da-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Impostazioni di Cache Redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="ee4da-109">È possibile visualizzare e configurare hello seguendo le impostazioni utilizzando hello **risorsa Menu**.</span><span class="sxs-lookup"><span data-stu-id="ee4da-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="ee4da-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ee4da-110">Overview</span></span>](#overview)
* [<span data-ttu-id="ee4da-111">Log attività</span><span class="sxs-lookup"><span data-stu-id="ee4da-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="ee4da-112">Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="ee4da-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="ee4da-113">Tag</span><span class="sxs-lookup"><span data-stu-id="ee4da-113">Tags</span></span>](#tags)
* [<span data-ttu-id="ee4da-114">Diagnostica e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ee4da-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="ee4da-115">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="ee4da-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="ee4da-116">Chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="ee4da-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="ee4da-117">Impostazioni avanzate</span><span class="sxs-lookup"><span data-stu-id="ee4da-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="ee4da-118">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="ee4da-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="ee4da-119">Ridimensionare</span><span class="sxs-lookup"><span data-stu-id="ee4da-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="ee4da-120">Dimensione del cluster Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="ee4da-121">Persistenza dei dati Redis:</span><span class="sxs-lookup"><span data-stu-id="ee4da-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="ee4da-122">Pianificare gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="ee4da-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="ee4da-123">Replica geografica</span><span class="sxs-lookup"><span data-stu-id="ee4da-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="ee4da-124">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="ee4da-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="ee4da-125">Firewall</span><span class="sxs-lookup"><span data-stu-id="ee4da-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="ee4da-126">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ee4da-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="ee4da-127">Blocchi</span><span class="sxs-lookup"><span data-stu-id="ee4da-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="ee4da-128">Script di automazione</span><span class="sxs-lookup"><span data-stu-id="ee4da-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="ee4da-129">Amministrazione</span><span class="sxs-lookup"><span data-stu-id="ee4da-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="ee4da-130">Importazione dei dati</span><span class="sxs-lookup"><span data-stu-id="ee4da-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="ee4da-131">Esportazione dei dati</span><span class="sxs-lookup"><span data-stu-id="ee4da-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="ee4da-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="ee4da-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="ee4da-133">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="ee4da-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="ee4da-134">Metriche di Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="ee4da-135">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="ee4da-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="ee4da-136">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="ee4da-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="ee4da-137">Supporto e impostazioni di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ee4da-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="ee4da-138">Integrità delle risorse</span><span class="sxs-lookup"><span data-stu-id="ee4da-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="ee4da-139">Nuova richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="ee4da-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="ee4da-140">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ee4da-140">Overview</span></span>

<span data-ttu-id="ee4da-141">**Panoramica** include le informazioni di base sulla cache, ad esempio nome, porte, piano tariffario e le metriche della cache selezionata.</span><span class="sxs-lookup"><span data-stu-id="ee4da-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="ee4da-142">Log attività</span><span class="sxs-lookup"><span data-stu-id="ee4da-142">Activity log</span></span>

<span data-ttu-id="ee4da-143">Fare clic su **log attività** tooview azioni eseguite nella cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="ee4da-144">È inoltre possibile utilizzare tooexpand filtro tooinclude questa vista ad altre risorse.</span><span class="sxs-lookup"><span data-stu-id="ee4da-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="ee4da-145">Per altre informazioni sull'uso dei log di controllo, vedere l'articolo relativo alle [operazioni di controllo con Resource Manager](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="ee4da-146">Per altre informazioni sul monitoraggio degli eventi di Cache Redis di Azure, vedere [Operazioni e avvisi](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="ee4da-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="ee4da-147">Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="ee4da-147">Access control (IAM)</span></span>

<span data-ttu-id="ee4da-148">Hello **Access control (IAM)** sezione fornisce supporto per il controllo di accesso basato sui ruoli (RBAC) in hello toohelp portale Azure organizzazioni soddisfino i requisiti di gestione accesso semplice e preciso.</span><span class="sxs-lookup"><span data-stu-id="ee4da-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="ee4da-149">Per ulteriori informazioni, vedere [controllo di accesso basato sui ruoli nel portale di Azure hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="ee4da-150">Tag</span><span class="sxs-lookup"><span data-stu-id="ee4da-150">Tags</span></span>

<span data-ttu-id="ee4da-151">Hello **tag** sezione consente di organizzare le risorse.</span><span class="sxs-lookup"><span data-stu-id="ee4da-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="ee4da-152">Per ulteriori informazioni, vedere [tramite tag tooorganize le risorse di Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="ee4da-153">Diagnostica e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ee4da-153">Diagnose and solve problems</span></span>

<span data-ttu-id="ee4da-154">Fare clic su **diagnosticare e risolvere i problemi** toobe fornito con problemi comuni e le strategie per risolverli.</span><span class="sxs-lookup"><span data-stu-id="ee4da-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="ee4da-155">Impostazioni</span><span class="sxs-lookup"><span data-stu-id="ee4da-155">Settings</span></span>
<span data-ttu-id="ee4da-156">Hello **impostazioni** sezione per tooaccess e la configurazione seguente le impostazioni della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="ee4da-157">Chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="ee4da-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="ee4da-158">Impostazioni avanzate</span><span class="sxs-lookup"><span data-stu-id="ee4da-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="ee4da-159">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="ee4da-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="ee4da-160">Ridimensionare</span><span class="sxs-lookup"><span data-stu-id="ee4da-160">Scale</span></span>](#scale)
* [<span data-ttu-id="ee4da-161">Dimensione del cluster Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="ee4da-162">Persistenza dei dati Redis:</span><span class="sxs-lookup"><span data-stu-id="ee4da-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="ee4da-163">Pianificare gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="ee4da-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="ee4da-164">Replica geografica</span><span class="sxs-lookup"><span data-stu-id="ee4da-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="ee4da-165">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="ee4da-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="ee4da-166">Firewall</span><span class="sxs-lookup"><span data-stu-id="ee4da-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="ee4da-167">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ee4da-167">Properties</span></span>](#properties)
* [<span data-ttu-id="ee4da-168">Blocchi</span><span class="sxs-lookup"><span data-stu-id="ee4da-168">Locks</span></span>](#locks)
* [<span data-ttu-id="ee4da-169">Script di automazione</span><span class="sxs-lookup"><span data-stu-id="ee4da-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="ee4da-170">Chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="ee4da-170">Access keys</span></span>
<span data-ttu-id="ee4da-171">Fare clic su **le chiavi di accesso** accesso hello tooview o rigenerare le chiavi per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="ee4da-172">Queste chiavi vengono utilizzate dai client hello tooyour cache di connessione.</span><span class="sxs-lookup"><span data-stu-id="ee4da-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Chiavi di accesso di Cache Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="ee4da-174">Impostazioni avanzate</span><span class="sxs-lookup"><span data-stu-id="ee4da-174">Advanced settings</span></span>
<span data-ttu-id="ee4da-175">Hello seguenti siano configurate su hello **impostazioni avanzate** blade.</span><span class="sxs-lookup"><span data-stu-id="ee4da-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="ee4da-176">Porte di accesso</span><span class="sxs-lookup"><span data-stu-id="ee4da-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="ee4da-177">Criteri di memoria</span><span class="sxs-lookup"><span data-stu-id="ee4da-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="ee4da-178">Notifiche di Keyspace (impostazioni avanzate)</span><span class="sxs-lookup"><span data-stu-id="ee4da-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="ee4da-179">Porte di accesso</span><span class="sxs-lookup"><span data-stu-id="ee4da-179">Access Ports</span></span>
<span data-ttu-id="ee4da-180">Per le nuove cache la porta senza SSL è disabilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ee4da-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="ee4da-181">tooenable hello non SSL porta, fare clic su **n** per **consentire l'accesso solo tramite SSL** su hello **impostazioni avanzate** blade e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="ee4da-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Porte di accesso di Cache Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="ee4da-183">Criteri di memoria</span><span class="sxs-lookup"><span data-stu-id="ee4da-183">Memory policies</span></span>
<span data-ttu-id="ee4da-184">Hello **criteri di Maxmemory**, **riservato maxmemory**, e **riservato maxfragmentationmemory** impostazioni hello **Impostazioniavanzate**pannello configurare criteri di memoria hello per cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Criterio maxmemory di Cache Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="ee4da-186">**Criteri di MaxMemory** consente di configurare i criteri di rimozione hello per cache di hello e consente toochoose da hello seguenti criteri di eliminazione:</span><span class="sxs-lookup"><span data-stu-id="ee4da-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="ee4da-187">`volatile-lru`-si tratta hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="ee4da-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="ee4da-188">Per altre informazioni sui criteri `maxmemory`, vedere [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Criteri di rimozione).</span><span class="sxs-lookup"><span data-stu-id="ee4da-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="ee4da-189">Hello **riservato maxmemory** consente di configurare la quantità hello di memoria in MB è riservato per le operazioni non cache, ad esempio la replica durante il failover.</span><span class="sxs-lookup"><span data-stu-id="ee4da-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="ee4da-190">Impostando questo valore consente un'esperienza più coerente di server Redis toohave quando il carico varia.</span><span class="sxs-lookup"><span data-stu-id="ee4da-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="ee4da-191">Questo valore deve essere più alto per i carichi di lavoro ad intensa attività di scrittura.</span><span class="sxs-lookup"><span data-stu-id="ee4da-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="ee4da-192">Quando la memoria è riservata per tali operazioni non è disponibile per l'archiviazione dei dati della cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="ee4da-193">Hello **riservato maxfragmentationmemory** consente di configurare la quantità hello di memoria in MB è tooaccommodate riservato per la frammentazione della memoria.</span><span class="sxs-lookup"><span data-stu-id="ee4da-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="ee4da-194">Impostando questo valore consente un'esperienza più coerente di server Redis toohave quando la cache di hello è piena o Chiudi toofull e hello rapporto di frammentazione è elevata.</span><span class="sxs-lookup"><span data-stu-id="ee4da-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="ee4da-195">Quando la memoria è riservata per tali operazioni non è disponibile per l'archiviazione dei dati della cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="ee4da-196">Tooconsider una cosa, quando si sceglie un nuovo valore di prenotazione di memoria (**riservato maxmemory** o **riservato maxfragmentationmemory**) è come questa modifica potrebbe influire su una cache che è già in esecuzione con grandi quantità di dati in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="ee4da-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="ee4da-197">Ad esempio, se si dispone di una cache 53 GB con 49 GB di dati, modificare hello prenotazione valore too8 GB, questa verrà eliminata hello max la memoria disponibile per il sistema hello verso il basso too45 GB.</span><span class="sxs-lookup"><span data-stu-id="ee4da-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="ee4da-198">Se il valore corrente `used_memory` oppure il `used_memory_rss` valori sono maggiori di nuovo limite di hello 45 GB, quindi sistema hello avrà tooevict dati fino a quando sia `used_memory` e `used_memory_rss` sono inferiori a 45 GB.</span><span class="sxs-lookup"><span data-stu-id="ee4da-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="ee4da-199">La rimozione può aumentare il carico del server e la frammentazione della memoria.</span><span class="sxs-lookup"><span data-stu-id="ee4da-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="ee4da-200">Per altre informazioni sulle metriche della cache come `used_memory` e `used_memory_rss` vedere [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) (Metriche disponibili e intervalli di report).</span><span class="sxs-lookup"><span data-stu-id="ee4da-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee4da-201">Hello **riservato maxmemory** e **riservato maxfragmentationmemory** impostazioni sono disponibili solo per Standard e Premium memorizza nella cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="ee4da-202">Notifiche di Keyspace (impostazioni avanzate)</span><span class="sxs-lookup"><span data-stu-id="ee4da-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="ee4da-203">Le notifiche sono configurate su hello spazio delle chiavi di redis **impostazioni avanzate** blade.</span><span class="sxs-lookup"><span data-stu-id="ee4da-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="ee4da-204">Le notifiche di spazio delle chiavi consentono ai client tooreceive notifiche quando si verificano determinati eventi.</span><span class="sxs-lookup"><span data-stu-id="ee4da-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Impostazioni avanzate di Cache Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="ee4da-206">Spazio delle chiavi le notifiche e hello **notifica eventi di spazio delle chiavi** impostazione sono disponibili solo per le cache Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="ee4da-207">Per altre informazioni, vedere [Notifiche di Keyspace Redis](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="ee4da-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="ee4da-208">Per esempio di codice, vedere hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) esempio.</span><span class="sxs-lookup"><span data-stu-id="ee4da-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="ee4da-209">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="ee4da-209">Redis Cache Advisor</span></span>
<span data-ttu-id="ee4da-210">Hello **Redis Cache Advisor** pannello Visualizza indicazioni per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="ee4da-211">Durante il normale funzionamento non viene visualizzata nessuna raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="ee4da-211">During normal operations, no recommendations are displayed.</span></span> 

![Raccomandazioni](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="ee4da-213">Se tutte le condizioni si verificano durante le operazioni di hello della cache, ad esempio l'utilizzo elevato della memoria, larghezza di banda di rete o del carico del server, viene visualizzato un avviso su hello **Cache Redis** blade.</span><span class="sxs-lookup"><span data-stu-id="ee4da-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Raccomandazioni](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="ee4da-215">Per ulteriori informazioni possono trovarsi in hello **indicazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="ee4da-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Raccomandazioni](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="ee4da-217">È possibile monitorare queste metriche in hello [grafici di monitoraggio](cache-how-to-monitor.md#monitoring-charts) e [grafici relativi all'utilizzo](cache-how-to-monitor.md#usage-charts) sezioni di hello **Cache Redis** blade.</span><span class="sxs-lookup"><span data-stu-id="ee4da-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="ee4da-218">Ogni piano tariffario presenta diversi limiti di connessioni client, memoria e larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="ee4da-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="ee4da-219">Se la cache rasenta la capacità massima di queste metriche per un periodo prolungato, viene creata una raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="ee4da-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="ee4da-220">Per ulteriori informazioni sulle metriche hello e limiti esaminati da hello **indicazioni** strumento, vedere hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="ee4da-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="ee4da-221">Metrica della cache Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-221">Redis Cache metric</span></span> | <span data-ttu-id="ee4da-222">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="ee4da-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="ee4da-223">Uso della larghezza di banda di rete</span><span class="sxs-lookup"><span data-stu-id="ee4da-223">Network bandwidth usage</span></span> |[<span data-ttu-id="ee4da-224">Prestazioni della cache - Larghezza di banda disponibile</span><span class="sxs-lookup"><span data-stu-id="ee4da-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="ee4da-225">Client connessi</span><span class="sxs-lookup"><span data-stu-id="ee4da-225">Connected clients</span></span> |[<span data-ttu-id="ee4da-226">Configurazione predefinita del server Redis - maxclients</span><span class="sxs-lookup"><span data-stu-id="ee4da-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="ee4da-227">Carico del server</span><span class="sxs-lookup"><span data-stu-id="ee4da-227">Server load</span></span> |[<span data-ttu-id="ee4da-228">Grafici di utilizzo - Carico server Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="ee4da-229">Utilizzo della memoria</span><span class="sxs-lookup"><span data-stu-id="ee4da-229">Memory usage</span></span> |[<span data-ttu-id="ee4da-230">Prestazioni della cache - Dimensioni</span><span class="sxs-lookup"><span data-stu-id="ee4da-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="ee4da-231">tooupgrade cache, fare clic su **Aggiorna** hello toochange livello di prezzo e [scala](#scale) la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="ee4da-232">Per altre informazioni su come scegliere un piano tariffario, vedere [Quali offerte e dimensioni della Cache Redis è consigliabile usare?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="ee4da-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="ee4da-233">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="ee4da-233">Scale</span></span>
<span data-ttu-id="ee4da-234">Fare clic su **scala** hello tooview o modificare piano tariffario per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="ee4da-235">Per ulteriori informazioni sulla scalabilità, vedere [la modalità di Cache Redis di Azure di tooScale](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Livello di prezzo di Cache Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="ee4da-237">Dimensione del cluster Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-237">Redis Cluster Size</span></span>
<span data-ttu-id="ee4da-238">Fare clic su **dimensione del Cluster Redis (anteprima)** la cache di dimensione del cluster hello toochange un premio in esecuzione con clustering abilitato.</span><span class="sxs-lookup"><span data-stu-id="ee4da-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="ee4da-239">Si noti che mentre hello Azure Redis Cache Premium livello è stato rilasciato tooGeneral disponibilità, funzionalità di dimensioni del Cluster Redis hello sono attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="ee4da-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Dimensione del cluster Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="ee4da-241">dimensione del cluster toochange hello, utilizzare il dispositivo di scorrimento hello o digitare un numero compreso tra 1 e 10 hello **numero di partizioni** casella di testo e fare clic su **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="ee4da-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee4da-242">Il clustering Redis è disponibile esclusivamente per le cache Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="ee4da-243">Per ulteriori informazioni, vedere [come tooconfigure clustering per una Cache Redis di Azure Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="ee4da-244">Persistenza dei dati Redis:</span><span class="sxs-lookup"><span data-stu-id="ee4da-244">Redis data persistence</span></span>
<span data-ttu-id="ee4da-245">Fare clic su **persistenza dei dati Redis** tooenable, disabilitare o configurare la persistenza dei dati per la cache premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="ee4da-246">Cache Redis di Azure offre la persistenza dei dati Redis tramite la [persistenza RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) o la [persistenza AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="ee4da-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="ee4da-247">Per ulteriori informazioni, vedere [come persistenza tooconfigure per una Cache Redis di Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="ee4da-248">La persistenza dei dati Redis è disponibile solo per le cache Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="ee4da-249">Pianificare gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="ee4da-249">Schedule updates</span></span>
<span data-ttu-id="ee4da-250">Hello **pianificare aggiornamenti** pannello consente toodesignate una finestra di manutenzione per gli aggiornamenti server Redis per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ee4da-251">finestra di manutenzione Hello si applica solo aggiornamenti di server tooRedis e tooany Azure aggiorna o aggiorna il sistema operativo toohello delle macchine virtuali di hello che ospitano una cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![Pianificare gli aggiornamenti](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="ee4da-253">toospecify una finestra di manutenzione, controllare i giorni hello desiderato e specificare l'ora di inizio finestra di manutenzione di hello per ogni giorno e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee4da-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="ee4da-254">Si noti che ora finestra di manutenzione hello è in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="ee4da-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ee4da-255">Hello **pianificare aggiornamenti** funzionalità è disponibile solo per le cache di livello Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="ee4da-256">Per altre informazioni e istruzioni, vedere [Come amministrare Cache Redis di Azure - Pianificare gli aggiornamenti](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="ee4da-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="ee4da-257">Replica geografica</span><span class="sxs-lookup"><span data-stu-id="ee4da-257">Geo-replication</span></span>

<span data-ttu-id="ee4da-258">Hello **-replica geografica** pannello fornisce un meccanismo per il collegamento di due istanze di Cache Redis di Azure di livello Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="ee4da-259">Una cache viene definita come cache collegato primario hello e altri come cache collegato secondaria hello hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="ee4da-260">cache collegato secondaria Hello diventa di sola lettura e cache primaria toohello scritti i dati replicati cache collegato secondaria toohello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="ee4da-261">Questa funzionalità può essere utilizzato tooreplicate una cache nelle aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4da-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee4da-262">**Replica geografica** è disponibile solo per le cache del piano Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="ee4da-263">Per ulteriori informazioni e istruzioni, vedere [come tooconfigure replica geografica per Cache Redis di Azure](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="ee4da-264">Rete virtuale</span><span class="sxs-lookup"><span data-stu-id="ee4da-264">Virtual Network</span></span>
<span data-ttu-id="ee4da-265">Hello **rete virtuale** sezione consente di impostazioni della rete virtuale hello tooconfigure per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="ee4da-266">Per informazioni sulla creazione di una cache premium con una rete virtuale supporta e aggiornamento delle impostazioni, vedere [come tooconfigure supporta la rete virtuale per una Cache Redis di Azure Premium](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee4da-267">Le impostazioni della rete virtuale sono disponibili solo per le cache di livello Premium configurate con il supporto della rete virtuale durante la creazione della cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="ee4da-268">Firewall</span><span class="sxs-lookup"><span data-stu-id="ee4da-268">Firewall</span></span>

<span data-ttu-id="ee4da-269">Fare clic su **Firewall** tooview e configurare le regole del firewall per la Cache Redis di Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Firewall](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="ee4da-271">È possibile specificare le regole del firewall con un intervallo di indirizzi IP iniziale e finale.</span><span class="sxs-lookup"><span data-stu-id="ee4da-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="ee4da-272">Quando le regole del firewall sono configurate, solo le connessioni client da hello specificare intervalli di indirizzi IP possono connettersi toohello cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="ee4da-273">Quando viene salvata di una regola del firewall è un breve ritardo prima regola hello è valida.</span><span class="sxs-lookup"><span data-stu-id="ee4da-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="ee4da-274">Questo tempo è in genere meno di un minuto.</span><span class="sxs-lookup"><span data-stu-id="ee4da-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee4da-275">Le connessioni dai sistemi di monitoraggio di Cache Redis di Azure sono sempre consentite, anche se le regole del firewall sono configurate.</span><span class="sxs-lookup"><span data-stu-id="ee4da-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="ee4da-276">Le regole del firewall sono disponibili solo per le cache del piano Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="ee4da-277">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ee4da-277">Properties</span></span>
<span data-ttu-id="ee4da-278">Fare clic su **proprietà** tooview informazioni sulla cache, incluse le porte ed endpoint della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Proprietà di Cache Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="ee4da-280">Blocchi</span><span class="sxs-lookup"><span data-stu-id="ee4da-280">Locks</span></span>
<span data-ttu-id="ee4da-281">Hello **blocca** sezione consente di toolock una sottoscrizione, gruppo di risorse o risorse tooprevent altri utenti nell'organizzazione da un'accidentale eliminazione o modifica di risorse critiche.</span><span class="sxs-lookup"><span data-stu-id="ee4da-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="ee4da-282">Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="ee4da-283">Script di automazione</span><span class="sxs-lookup"><span data-stu-id="ee4da-283">Automation script</span></span>

<span data-ttu-id="ee4da-284">Fare clic su **script di automazione** toobuild ed esportare un modello di risorse distribuite per le distribuzioni future.</span><span class="sxs-lookup"><span data-stu-id="ee4da-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="ee4da-285">Per altre informazioni sull'uso dei modelli, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="ee4da-286">Impostazioni di amministrazione</span><span class="sxs-lookup"><span data-stu-id="ee4da-286">Administration settings</span></span>
<span data-ttu-id="ee4da-287">le impostazioni di hello Hello **amministrazione** sezione consentono di hello tooperform seguendo le attività amministrative per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Amministrazione](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="ee4da-289">Importazione dei dati</span><span class="sxs-lookup"><span data-stu-id="ee4da-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="ee4da-290">Esportazione dei dati</span><span class="sxs-lookup"><span data-stu-id="ee4da-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="ee4da-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="ee4da-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="ee4da-292">Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="ee4da-292">Import/Export</span></span>
<span data-ttu-id="ee4da-293">Importazione/esportazione è un'operazione di gestione di dati Cache Redis di Azure, che consente di tooimport ed esportare i dati nella cache di hello dall'importazione ed esportazione di uno snapshot del Database di Cache Redis (RDB) da un blob di pagine tooa cache premium in un Account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4da-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="ee4da-294">Importazione/esportazione consente toomigrate tra istanze diverse di Cache Redis di Azure o memorizzare nella cache di hello con i dati prima dell'uso.</span><span class="sxs-lookup"><span data-stu-id="ee4da-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="ee4da-295">Importazione può essere utilizzati toobring Redis compatibile RDB file da qualsiasi server Redis in esecuzione in qualsiasi cloud o di un ambiente, compresi Redis in esecuzione in Linux, Windows o di qualsiasi provider di cloud come Amazon Web Services e altre.</span><span class="sxs-lookup"><span data-stu-id="ee4da-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="ee4da-296">Importazione di dati è un toocreate facilmente una cache con dati pre-popolati.</span><span class="sxs-lookup"><span data-stu-id="ee4da-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="ee4da-297">Durante il processo di importazione hello Cache Redis di Azure Carica file RDB hello dall'archiviazione di Azure in memoria e quindi inserisce chiavi hello nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="ee4da-298">Esporta consente dati hello tooexport archiviati nei file di Cache Redis di Azure tooRedis compatibili RDB.</span><span class="sxs-lookup"><span data-stu-id="ee4da-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="ee4da-299">È possibile utilizzare i dati da una Cache Redis di Azure istanza tooanother o server Redis tooanother toomove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ee4da-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="ee4da-300">Durante il processo di esportazione hello, viene creato un file temporaneo nella macchina virtuale che ospita hello istanza server di Cache Redis di Azure e file hello è caricato toohello definito account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="ee4da-301">Quando l'operazione di esportazione hello viene completato con stato di esito positivo o negativo, viene eliminato il file temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee4da-302">La funzionalità Importazione/Esportazione è disponibile solo per le cache del piano Premium.</span><span class="sxs-lookup"><span data-stu-id="ee4da-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="ee4da-303">Per altre informazioni e istruzioni, vedere [Importare ed esportare dati in Cache Redis di Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="ee4da-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="ee4da-304">Reboot</span></span>
<span data-ttu-id="ee4da-305">Hello **riavviare** pannello consente nodi hello tooreboot della cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="ee4da-306">Questa funzionalità di riavvio consente si tootest all'applicazione per garantire la resilienza, se si verifica un errore di un nodo della cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="ee4da-308">Se si dispone di una cache premium con clustering abilitato, è possibile selezionare le partizioni di tooreboot cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="ee4da-310">tooreboot uno o più nodi della cache, selezionare i nodi di hello desiderato e fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="ee4da-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="ee4da-311">Se si dispone di una cache premium con clustering abilitato, selezionare tooreboot shard(s) hello e quindi fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="ee4da-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="ee4da-312">Dopo alcuni minuti, hello il riavvio di nodi selezionato e sono in linea alcuni minuti in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ee4da-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee4da-313">Il riavvio ora è disponibile per tutti i piani tariffari.</span><span class="sxs-lookup"><span data-stu-id="ee4da-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="ee4da-314">Per altre informazioni e istruzioni, vedere [Come amministrare Cache Redis di Azure - Riavvia](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="ee4da-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="ee4da-315">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="ee4da-315">Monitoring</span></span>

<span data-ttu-id="ee4da-316">Hello **monitoraggio** sezione consente di tooconfigure diagnostica e monitoraggio per la Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="ee4da-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="ee4da-317">Per ulteriori informazioni sulla diagnostica e monitoraggio di Cache Redis di Azure, vedere [la modalità di Cache Redis di Azure di toomonitor](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostica](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="ee4da-319">Metriche di Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="ee4da-320">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="ee4da-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="ee4da-321">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="ee4da-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="ee4da-322">Metriche Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-322">Redis metrics</span></span>
<span data-ttu-id="ee4da-323">Fare clic su **Redis metriche** troppo[visualizzare le metriche](cache-how-to-monitor.md#view-cache-metrics) per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="ee4da-324">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="ee4da-324">Alert rules</span></span>

<span data-ttu-id="ee4da-325">Fare clic su **regole di avviso** tooconfigure avvisi in base alle metriche di Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="ee4da-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="ee4da-326">Per altre informazioni, vedere [Avvisi](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="ee4da-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="ee4da-327">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="ee4da-327">Diagnostics</span></span>

<span data-ttu-id="ee4da-328">Per impostazione predefinita, le metriche relative alla cache in Monitoraggio di Azure vengono [archiviate per 30 giorni](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e quindi vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="ee4da-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="ee4da-329">Scegliere le metriche della cache per più di 30 giorni, toopersist **diagnostica** troppo[configurare account di archiviazione hello](cache-how-to-monitor.md#export-cache-metrics) utilizzato toostore della diagnostica della cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="ee4da-330">In aggiunta tooarchiving toostorage le metriche di cache, è anche possibile [trasmessi tooan hub di eventi o inviare loro tooLog Analitica](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="ee4da-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="ee4da-331">Supporto e impostazioni di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ee4da-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="ee4da-332">le impostazioni di hello Hello **supporto + risoluzione dei problemi** sezione forniscono le opzioni per la risoluzione dei problemi con la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Supporto e risoluzione dei problemi](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="ee4da-334">Integrità delle risorse</span><span class="sxs-lookup"><span data-stu-id="ee4da-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="ee4da-335">Nuova richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="ee4da-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="ee4da-336">Integrità delle risorse</span><span class="sxs-lookup"><span data-stu-id="ee4da-336">Resource health</span></span>
<span data-ttu-id="ee4da-337">**Integrità risorsa** esamina la risorsa e indica se viene eseguita nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="ee4da-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="ee4da-338">Per ulteriori informazioni su hello servizio di integrità delle risorse di Azure, vedere [Panoramica di integrità delle risorse di Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ee4da-339">Integrità delle risorse è attualmente in grado di tooreport integrità hello di istanze di Cache Redis di Azure ospitati in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ee4da-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="ee4da-340">Per altre informazioni, vedere [Tutte le funzionalità della cache funzionano quando si ospita una cache in una rete virtuale?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="ee4da-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="ee4da-341">Nuova richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="ee4da-341">New support request</span></span>
<span data-ttu-id="ee4da-342">Fare clic su **nuova richiesta di assistenza** tooopen una richiesta di supporto per la cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="ee4da-343">Configurazione predefinita del server Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-343">Default Redis server configuration</span></span>
<span data-ttu-id="ee4da-344">Nuova Cache Redis di Azure vengono configurate con hello seguente i valori predefiniti di configurazione di Redis.</span><span class="sxs-lookup"><span data-stu-id="ee4da-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="ee4da-345">impostazioni di Hello in questa sezione non possono essere modificate utilizzando hello `StackExchange.Redis.IServer.ConfigSet` metodo.</span><span class="sxs-lookup"><span data-stu-id="ee4da-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="ee4da-346">Se questo metodo viene chiamato con uno dei comandi di hello in questa sezione, viene generata un' seguente toohello simile di eccezione:</span><span class="sxs-lookup"><span data-stu-id="ee4da-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="ee4da-347">I valori che sono configurabili, ad esempio **criteri di memoria max**, possono essere configurate tramite hello portale di Azure o gli strumenti di gestione della riga di comando, ad esempio CLI di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee4da-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="ee4da-348">Impostazione</span><span class="sxs-lookup"><span data-stu-id="ee4da-348">Setting</span></span> | <span data-ttu-id="ee4da-349">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="ee4da-349">Default value</span></span> | <span data-ttu-id="ee4da-350">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ee4da-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="ee4da-351">16</span><span class="sxs-lookup"><span data-stu-id="ee4da-351">16</span></span> |<span data-ttu-id="ee4da-352">numero di database predefinito di Hello è 16, ma è possibile configurare un diverso numero hello in base a livello di prezzo. <sup>1</sup> database predefinito hello è DB 0, è possibile selezionare una diversa in ogni singola una connessione utilizzando `connection.GetDatabase(dbid)` in `dbid` è un numero compreso tra `0` e `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="ee4da-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="ee4da-353">Dipende dal livello di prezzo hello<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="ee4da-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="ee4da-354">Questo è hello il numero massimo di client connessi in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="ee4da-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="ee4da-355">Quando viene raggiunto il limite di hello Redis chiude tutte le nuove connessioni a hello, restituendo un errore di 'numero massimo di client raggiunto'.</span><span class="sxs-lookup"><span data-stu-id="ee4da-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="ee4da-356">Criteri di MaxMemory sono l'impostazione di hello per la modalità di selezione quali tooremove Redis quando `maxmemory` viene raggiunta (hello dimensione della cache di hello offerta selezionato al momento della creazione della cache di hello).</span><span class="sxs-lookup"><span data-stu-id="ee4da-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="ee4da-357">Impostazione predefinita di hello Cache Redis di Azure è `volatile-lru`, che rimuove le chiavi di hello con una scadenza impostata mediante l'algoritmo LRU.</span><span class="sxs-lookup"><span data-stu-id="ee4da-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="ee4da-358">Questa impostazione può essere configurata in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4da-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="ee4da-359">Per altre informazioni, vedere [Criteri di memoria](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="ee4da-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="ee4da-360">3</span><span class="sxs-lookup"><span data-stu-id="ee4da-360">3</span></span> |<span data-ttu-id="ee4da-361">memoria toosave, LRU e algoritmi TTL minimo sono algoritmi approssimativa anziché precisi.</span><span class="sxs-lookup"><span data-stu-id="ee4da-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="ee4da-362">Per impostazione predefinita Redis controlli tre chiavi e i prelievi hello uno utilizzati meno recente.</span><span class="sxs-lookup"><span data-stu-id="ee4da-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="ee4da-363">5.000</span><span class="sxs-lookup"><span data-stu-id="ee4da-363">5,000</span></span> |<span data-ttu-id="ee4da-364">Tempo massimo di esecuzione di uno script Lua in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="ee4da-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="ee4da-365">Se viene raggiunto il tempo di esecuzione massimo hello, Redis registra uno script è ancora in esecuzione dopo hello massimo consentito di tempo che inizia tooreply tooqueries con un errore.</span><span class="sxs-lookup"><span data-stu-id="ee4da-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="ee4da-366">500</span><span class="sxs-lookup"><span data-stu-id="ee4da-366">500</span></span> |<span data-ttu-id="ee4da-367">Dimensione massima della coda di eventi di script.</span><span class="sxs-lookup"><span data-stu-id="ee4da-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="ee4da-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="ee4da-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="ee4da-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="ee4da-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="ee4da-370">Hello i limiti del buffer di output di client possono essere utilizzato tooforce disconnessione dei client che non leggono i dati dal server hello sufficientemente veloce per qualche motivo (una causa comune è che un client di pubblicazione/sottoscrizione non può utilizzare la stessa velocità pubblicazione hello può produrre tali messaggi).</span><span class="sxs-lookup"><span data-stu-id="ee4da-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="ee4da-371">Per altre informazioni, vedere [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="ee4da-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="ee4da-372"><a name="databases"></a>
<sup>1</sup>limite hello per `databases` è diverso per Azure Redis Cache di ogni livello di prezzo e può essere impostato al momento della creazione della cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="ee4da-373">Se non `databases` impostazione viene specificato durante la creazione della cache predefinita hello è 16.</span><span class="sxs-lookup"><span data-stu-id="ee4da-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="ee4da-374">Cache di base e Standard</span><span class="sxs-lookup"><span data-stu-id="ee4da-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="ee4da-375">C0 cache (250 MB): Backup database too16</span><span class="sxs-lookup"><span data-stu-id="ee4da-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="ee4da-376">C1 cache (1 GB) - backup di database too16</span><span class="sxs-lookup"><span data-stu-id="ee4da-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="ee4da-377">C2 cache (2,5 GB) - backup di database too16</span><span class="sxs-lookup"><span data-stu-id="ee4da-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="ee4da-378">C3 cache (6 GB) - backup di database too16</span><span class="sxs-lookup"><span data-stu-id="ee4da-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="ee4da-379">C4 cache (13 GB) - backup di database too32</span><span class="sxs-lookup"><span data-stu-id="ee4da-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="ee4da-380">C5 cache (26 GB) - backup di database too48</span><span class="sxs-lookup"><span data-stu-id="ee4da-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="ee4da-381">C6 cache (53 GB) - backup di database too64</span><span class="sxs-lookup"><span data-stu-id="ee4da-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="ee4da-382">Cache Premium</span><span class="sxs-lookup"><span data-stu-id="ee4da-382">Premium caches</span></span>
  * <span data-ttu-id="ee4da-383">P1 (6 GB - 60 GB) - backup di database too16</span><span class="sxs-lookup"><span data-stu-id="ee4da-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="ee4da-384">P2 (13 GB - 130 GB) - backup di database too32</span><span class="sxs-lookup"><span data-stu-id="ee4da-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="ee4da-385">P3 (26 GB - 260 GB) - backup di database too48</span><span class="sxs-lookup"><span data-stu-id="ee4da-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="ee4da-386">P4 (53 GB - 530 GB) - backup di database too64</span><span class="sxs-lookup"><span data-stu-id="ee4da-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="ee4da-387">Tutte le cache premium con cluster Redis abilitata - Redis cluster supporta solo l'uso di database 0 hello in modo `databases` limitare per tutte le cache premium con cluster Redis abilitata in modo efficace è di 1 e hello [selezionare](http://redis.io/commands/select) comando non è consentito.</span><span class="sxs-lookup"><span data-stu-id="ee4da-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="ee4da-388">Per ulteriori informazioni, vedere [devo toomake qualsiasi toouse applicazione di modifiche toomy client clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="ee4da-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="ee4da-389">Per altre informazioni sui database SQL di Azure, vedere [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Cosa sono i database Redis?)</span><span class="sxs-lookup"><span data-stu-id="ee4da-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="ee4da-390">Hello `databases` impostazione può essere configurata solo durante la creazione della cache e solo tramite PowerShell, CLI o altri client di gestione.</span><span class="sxs-lookup"><span data-stu-id="ee4da-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="ee4da-391">Per un esempio di configurazione di `databases` durante la creazione della cache con PowerShell, vedere [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="ee4da-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="ee4da-392"><a name="maxclients"></a>
<sup>2</sup>Il valore di `maxclients` è diverso per ogni piano tariffario di Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4da-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="ee4da-393">Cache di base e Standard</span><span class="sxs-lookup"><span data-stu-id="ee4da-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="ee4da-394">C0 cache (250 MB): le connessioni too256</span><span class="sxs-lookup"><span data-stu-id="ee4da-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="ee4da-395">C1 cache (1 GB) - backup too1, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="ee4da-396">C2 cache (2,5 GB) - backup too2, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="ee4da-397">C3 cache (6 GB) - backup too5, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="ee4da-398">C4 cache (13 GB) - backup too10, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="ee4da-399">C5 cache (26 GB) - backup too15, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="ee4da-400">C6 cache (53 GB) - backup too20, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="ee4da-401">Cache Premium</span><span class="sxs-lookup"><span data-stu-id="ee4da-401">Premium caches</span></span>
  * <span data-ttu-id="ee4da-402">P1 (6 GB - 60 GB) - backup too7, connessioni a 500</span><span class="sxs-lookup"><span data-stu-id="ee4da-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="ee4da-403">P2 (13 GB - 130 GB) - backup too15, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="ee4da-404">P3 (26 GB - 260 GB) - backup too30, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="ee4da-405">P4 (53 GB - 530 GB) - backup too40, connessioni 000</span><span class="sxs-lookup"><span data-stu-id="ee4da-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="ee4da-406">Mentre ogni dimensione della cache consente *fino a* un determinato numero di connessioni, ogni tooRedis connessione overhead è associato.</span><span class="sxs-lookup"><span data-stu-id="ee4da-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="ee4da-407">Un esempio di questo sovraccarico potrebbe essere l'utilizzo della CPU e della memoria a causa della crittografia TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="ee4da-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="ee4da-408">limite massimo di connessioni Hello per una dimensione della cache specificata si presuppone una cache con caricata ridotto.</span><span class="sxs-lookup"><span data-stu-id="ee4da-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="ee4da-409">Se caricare dall'overhead connessione *più* carico dalle operazioni client supera la capacità di sistema di hello, cache di hello possa verificarsi problemi di capacità, anche se non è stato superato il limite di connessioni hello per la dimensione corrente della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="ee4da-410">Comandi di Redis non supportati in Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="ee4da-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee4da-411">Poiché configurazione e gestione delle istanze di Cache Redis di Azure viene gestito da Microsoft, hello comandi seguenti sono disabilitati.</span><span class="sxs-lookup"><span data-stu-id="ee4da-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="ee4da-412">Se si tenta di tooinvoke loro, viene visualizzato un messaggio di errore simile troppo`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="ee4da-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="ee4da-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="ee4da-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="ee4da-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="ee4da-414">BGSAVE</span></span>
> * <span data-ttu-id="ee4da-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="ee4da-415">CONFIG</span></span>
> * <span data-ttu-id="ee4da-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="ee4da-416">DEBUG</span></span>
> * <span data-ttu-id="ee4da-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="ee4da-417">MIGRATE</span></span>
> * <span data-ttu-id="ee4da-418">Salva</span><span class="sxs-lookup"><span data-stu-id="ee4da-418">SAVE</span></span>
> * <span data-ttu-id="ee4da-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="ee4da-419">SHUTDOWN</span></span>
> * <span data-ttu-id="ee4da-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="ee4da-420">SLAVEOF</span></span>
> * <span data-ttu-id="ee4da-421">CLUSTER: i comandi di scrittura del cluster sono disabilitati, ma i comandi del cluster di sola lettura sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="ee4da-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="ee4da-422">Per ulteriori informazioni sui comandi di Redis, vedere [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="ee4da-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="ee4da-423">Console Redis</span><span class="sxs-lookup"><span data-stu-id="ee4da-423">Redis console</span></span>
<span data-ttu-id="ee4da-424">In modo sicuro è possibile emettere comandi tooyour le istanze di Cache Redis di Azure utilizzando hello **Console Redis**, disponibile nel portale di Azure per tutti i livelli di cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="ee4da-425">Hello Console Redis non funziona con [rete virtuale](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="ee4da-426">Quando la cache fa parte di una rete virtuale, solo i client nella rete virtuale hello possono accedere cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="ee4da-427">La Console Redis viene eseguita nel browser locale, non è compreso hello rete virtuale, non è possibile connettersi tooyour cache.</span><span class="sxs-lookup"><span data-stu-id="ee4da-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="ee4da-428">Non tutti i comandi di Redis sono supportati in Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee4da-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="ee4da-429">Per un elenco di comandi di Redis che sono disabilitate per Cache Redis di Azure, vedere hello precedente [comandi non supportati in Cache Redis di Azure Redis](#redis-commands-not-supported-in-azure-redis-cache) sezione.</span><span class="sxs-lookup"><span data-stu-id="ee4da-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="ee4da-430">Per ulteriori informazioni sui comandi di Redis, vedere [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="ee4da-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="ee4da-431">hello tooaccess Console Redis, fare clic su **Console** da hello **Cache Redis** blade.</span><span class="sxs-lookup"><span data-stu-id="ee4da-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Console Redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="ee4da-433">comandi tooissue contro l'istanza di cache, semplicemente hello di tipo desiderato comando nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Console Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="ee4da-435">Utilizzando hello cache Redis Console con un premio cluster</span><span class="sxs-lookup"><span data-stu-id="ee4da-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="ee4da-436">Quando con un premio di hello Console Redis cache del cluster, è possibile eseguire una singola partizione tooa comandi della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="ee4da-437">tooissue una partizione specifica tooa di comando, connettersi innanzitutto partizione desiderata toohello facendo doppio clic sul selettore di partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Console Redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="ee4da-439">Se si tenta di tooaccess una chiave archiviata in una partizione diversa rispetto a hello partizioni connesso, verrà visualizzato un toohello simile messaggio di errore seguente messaggio.</span><span class="sxs-lookup"><span data-stu-id="ee4da-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="ee4da-440">Nell'esempio precedente hello partizione 1 è partizione selezionata hello, ma `myKey` si trova nella partizione 0, come indicato dal hello `(shard 0)` parte del messaggio di errore hello.</span><span class="sxs-lookup"><span data-stu-id="ee4da-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="ee4da-441">In questo esempio, tooaccess `myKey`, selezionare 0 partizioni utilizzando hello selezione partizioni e quindi problema hello desiderato del comando.</span><span class="sxs-lookup"><span data-stu-id="ee4da-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="ee4da-442">Spostare la nuova sottoscrizione tooa di cache</span><span class="sxs-lookup"><span data-stu-id="ee4da-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="ee4da-443">È possibile spostare la nuova sottoscrizione di tooa cache facendo **spostare**.</span><span class="sxs-lookup"><span data-stu-id="ee4da-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Spostare la cache Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="ee4da-445">Per informazioni sullo spostamento di risorse da una risorsa gruppo tooanother e da una sottoscrizione tooanother, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ee4da-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee4da-446">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee4da-446">Next steps</span></span>
* <span data-ttu-id="ee4da-447">Per altre informazioni sull'uso dei comandi di Redis, vedere [Come è possibile eseguire i comandi di Redis?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="ee4da-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

