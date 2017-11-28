---
title: 'Come tooconfigure routing (peering) per un circuito ExpressRoute: Gestione risorse: Azure | Documenti Microsoft'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="440a1-104">Creare e modificare i peering per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="440a1-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="440a1-105">In questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione di gestione risorse hello utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="440a1-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="440a1-106">È anche possibile controllare lo stato di hello, update o delete e deprovisioning peering per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="440a1-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="440a1-107">Se si desidera toouse toowork un metodo diverso con il circuito, selezionare un articolo da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="440a1-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="440a1-108">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="440a1-108">Configuration prerequisites</span></span>

* <span data-ttu-id="440a1-109">Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) pagina hello [requisiti di routing](expressroute-routing.md) pagina e hello [flussi di lavoro](expressroute-workflows.md) pagina prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="440a1-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="440a1-110">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="440a1-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="440a1-111">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="440a1-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="440a1-112">Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato per si toobe toorun in grado di hello cmdlet nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="440a1-113">Se si intende toouse un hash di chiave/MD5 condiviso, scegliere toouse che questo su entrambi i lati dell'hello tunnel e limite hello del numero massimo di caratteri tooa pari a 25.</span><span class="sxs-lookup"><span data-stu-id="440a1-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="440a1-114">Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="440a1-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="440a1-115">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito una VPN IP, come MPLS), il provider di connettività configura e gestisce il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="440a1-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="440a1-116">È attualmente non inviano annunci peering configurato dai provider di servizi tramite il portale di Gestione servizi hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="440a1-117">L'abilitazione di questa funzionalità sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="440a1-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="440a1-118">Rivolgersi al provider di servizi prima di configurare peering BGP.</span><span class="sxs-lookup"><span data-stu-id="440a1-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="440a1-119">Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="440a1-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="440a1-120">È possibile configurare i peering nell'ordine desiderato.</span><span class="sxs-lookup"><span data-stu-id="440a1-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="440a1-121">Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="440a1-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="440a1-122">Peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-122">Azure private peering</span></span>

<span data-ttu-id="440a1-123">In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="440a1-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="440a1-124">toocreate peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="440a1-125">Configurare il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="440a1-126">Verificare che il circuito hello è stato effettuato il provisioning dal provider di connettività hello prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="440a1-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="440a1-128">Configurare peering privato di Azure per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="440a1-129">Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="440a1-130">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="440a1-131">subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="440a1-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="440a1-132">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="440a1-133">subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="440a1-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="440a1-134">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="440a1-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="440a1-135">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="440a1-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="440a1-136">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="440a1-136">AS number for peering.</span></span> <span data-ttu-id="440a1-137">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="440a1-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="440a1-138">È possibile usare il numero AS privato per questo peering.</span><span class="sxs-lookup"><span data-stu-id="440a1-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="440a1-139">Assicurarsi di non usare il numero 65515.</span><span class="sxs-lookup"><span data-stu-id="440a1-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="440a1-140">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="440a1-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="440a1-141">Selezionare il peering privato di Azure, riga di hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![Privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="440a1-143">Configurare il peering privato.</span><span class="sxs-lookup"><span data-stu-id="440a1-143">Configure private peering.</span></span> <span data-ttu-id="440a1-144">Hello immagine seguente viene illustrato un esempio di configurazione:</span><span class="sxs-lookup"><span data-stu-id="440a1-144">hello following image shows a configuration example:</span></span>

  ![Configurare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="440a1-146">Salvare la configurazione di hello dopo aver specificato tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="440a1-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="440a1-147">Dopo la configurazione di hello è stata accettata correttamente, è visualizzato un codice simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="440a1-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Salvare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="440a1-149">tooview dettagli di peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-149">tooview Azure private peering details</span></span>

<span data-ttu-id="440a1-150">È possibile visualizzare le proprietà di hello di peering privato di Azure selezionando hello peering.</span><span class="sxs-lookup"><span data-stu-id="440a1-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![Visualizzare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="440a1-152">configurazione di peering privato Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="440a1-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="440a1-153">È possibile selezionare la riga hello per il peering e modificare le proprietà di peering hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-153">You can select hello row for peering and modify hello peering properties.</span></span>

![Aggiornare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="440a1-155">toodelete peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-155">toodelete Azure private peering</span></span>

<span data-ttu-id="440a1-156">È possibile rimuovere la configurazione di peering selezionando l'icona di eliminazione hello, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![Eliminare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="440a1-158">Peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-158">Azure public peering</span></span>

<span data-ttu-id="440a1-159">In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="440a1-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="440a1-160">toocreate peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="440a1-161">Configurare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="440a1-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="440a1-162">Verificare che il circuito hello è stato effettuato il provisioning dal provider di connettività hello prima di continuare ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="440a1-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Elencare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="440a1-164">Configurare peering pubblico di Azure per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="440a1-165">Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="440a1-166">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="440a1-167">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="440a1-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="440a1-168">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="440a1-169">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="440a1-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="440a1-170">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="440a1-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="440a1-171">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="440a1-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="440a1-172">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="440a1-172">AS number for peering.</span></span> <span data-ttu-id="440a1-173">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="440a1-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="440a1-174">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="440a1-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="440a1-175">Selezionare hello Azure riga peering pubblico, come mostrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![Selezionare la riga del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="440a1-177">Configurare il peering pubblico.</span><span class="sxs-lookup"><span data-stu-id="440a1-177">Configure public peering.</span></span> <span data-ttu-id="440a1-178">Hello immagine seguente viene illustrato un esempio di configurazione:</span><span class="sxs-lookup"><span data-stu-id="440a1-178">hello following image shows a configuration example:</span></span>

  ![Configurare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="440a1-180">Salvare la configurazione di hello dopo aver specificato tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="440a1-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="440a1-181">Dopo la configurazione di hello è stata accettata correttamente, è visualizzato un codice simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="440a1-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Salvare la configurazione del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="440a1-183">tooview dettagli di peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-183">tooview Azure public peering details</span></span>

<span data-ttu-id="440a1-184">È possibile visualizzare le proprietà di hello di peering pubblico di Azure selezionando hello peering.</span><span class="sxs-lookup"><span data-stu-id="440a1-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![Visualizzare le proprietà del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="440a1-186">configurazione di peering pubblico Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="440a1-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="440a1-187">È possibile selezionare la riga hello per il peering e modificare le proprietà di peering hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-187">You can select hello row for peering and modify hello peering properties.</span></span>

![Selezionare la riga del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="440a1-189">toodelete peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="440a1-189">toodelete Azure public peering</span></span>

<span data-ttu-id="440a1-190">È possibile rimuovere la configurazione di peering selezionando l'icona di eliminazione hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![Eliminare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="440a1-192">Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="440a1-192">Microsoft peering</span></span>

<span data-ttu-id="440a1-193">In questa sezione consente di creare, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="440a1-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="440a1-194">Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite hello peering Microsoft, anche se non sono definiti i filtri di route.</span><span class="sxs-lookup"><span data-stu-id="440a1-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="440a1-195">Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="440a1-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="440a1-196">Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="440a1-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="440a1-197">toocreate peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="440a1-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="440a1-198">Configurare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="440a1-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="440a1-199">Verificare che il circuito hello è stato effettuato il provisioning dal provider di connettività hello prima di continuare ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="440a1-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Elencare il peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="440a1-201">Configurare Microsoft peering per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="440a1-202">Assicurarsi di aver hello le seguenti informazioni prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="440a1-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="440a1-203">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="440a1-204">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="440a1-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="440a1-205">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="440a1-206">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="440a1-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="440a1-207">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="440a1-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="440a1-208">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="440a1-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="440a1-209">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="440a1-209">AS number for peering.</span></span> <span data-ttu-id="440a1-210">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="440a1-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="440a1-211">I prefissi annunciati: È necessario fornire un elenco di tutti i prefissi Prevedi tooadvertise sessione BGP hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="440a1-212">Sono accettati solo prefissi di indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="440a1-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="440a1-213">Se si prevede un set di prefissi toosend, è possibile inviare un elenco delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="440a1-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="440a1-214">I prefissi devono essere registrati tooyou in un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="440a1-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="440a1-215">**Facoltativo:** cliente ASN: nel caso di annunci con prefissi non registrato toohello peering sotto forma di numero, è possibile specificare hello come numero toowhich sono registrati.</span><span class="sxs-lookup"><span data-stu-id="440a1-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="440a1-216">Nome del Registro di sistema di routing: È possibile specificare hello RIR / IRR contro cui hello come numero e i prefissi sono registrati.</span><span class="sxs-lookup"><span data-stu-id="440a1-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="440a1-217">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="440a1-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="440a1-218">È possibile selezionare hello peering desiderato tooconfigure, come illustrato nella seguente hello esempio.</span><span class="sxs-lookup"><span data-stu-id="440a1-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="440a1-219">Selezionare una riga di peering Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-219">Select hello Microsoft peering row.</span></span>

  ![Selezionare la riga del peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="440a1-221">Configurare il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="440a1-221">Configure Microsoft peering.</span></span> <span data-ttu-id="440a1-222">Hello immagine seguente viene illustrato un esempio di configurazione:</span><span class="sxs-lookup"><span data-stu-id="440a1-222">hello following image shows a configuration example:</span></span>

  ![Configurare il peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="440a1-224">Salvare la configurazione di hello dopo aver specificato tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="440a1-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="440a1-225">Se il circuito Ottiene tooa 'Convalida necessaria' stato (come illustrato nell'immagine hello), è necessario aprire una prova di proprietà del team di supporto di hello prefissi tooour tooshow di supporto ticket.</span><span class="sxs-lookup"><span data-stu-id="440a1-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Salvare la configurazione del peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="440a1-227">È possibile aprire un ticket di supporto direttamente dal portale di hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="440a1-228">Dopo la configurazione di hello è stata accettata correttamente, è visualizzato un codice simile toohello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="440a1-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="440a1-229">dettagli di peering Microsoft tooview</span><span class="sxs-lookup"><span data-stu-id="440a1-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="440a1-230">È possibile visualizzare le proprietà di hello di peering pubblico di Azure selezionando hello peering.</span><span class="sxs-lookup"><span data-stu-id="440a1-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="440a1-231">configurazione di peering Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="440a1-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="440a1-232">È possibile selezionare la riga hello per il peering e modificare le proprietà di peering hello.</span><span class="sxs-lookup"><span data-stu-id="440a1-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="440a1-233">toodelete peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="440a1-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="440a1-234">È possibile rimuovere la configurazione di peering selezionando l'icona di eliminazione hello, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="440a1-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="440a1-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="440a1-235">Next steps</span></span>

<span data-ttu-id="440a1-236">Passaggio successivo, [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="440a1-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="440a1-237">Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="440a1-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="440a1-238">Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="440a1-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="440a1-239">Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="440a1-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
