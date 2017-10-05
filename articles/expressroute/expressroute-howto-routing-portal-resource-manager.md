---
title: 'Come configurare il routing (peering) per un circuito ExpressRoute: Resource Manager: Azure | Documentazione Microsoft'
description: Questo articolo descrive come creare ed eseguire il provisioning di un circuito ExpressRoute per il peering privato, il peering pubblico e il peering Microsoft. Questo articolo mostra anche come controllare lo stato e aggiornare o eliminare i peering per un circuito.
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
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="1d445-104">Creare e modificare i peering per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1d445-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="1d445-105">Questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione Resource Manager tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d445-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="1d445-106">La procedura seguente mostra anche come controllare lo stato e aggiornare, eliminare o effettuare il deprovisioning dei peering per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d445-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="1d445-107">Se si vuole usare un metodo diverso per eseguire operazioni nel circuito, selezionare l'articolo appropriato nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="1d445-108">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="1d445-108">Configuration prerequisites</span></span>

* <span data-ttu-id="1d445-109">Prima di iniziare la configurazione, assicurarsi di aver letto le pagine relative ai [prerequisiti](expressroute-prerequisites.md), ai [requisiti per il routing](expressroute-routing.md) e ai [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="1d445-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="1d445-110">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="1d445-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="1d445-111">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e fare in modo che venga abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="1d445-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="1d445-112">Per poter eseguire i cmdlet descritti nelle sezioni successive deve essere stato effettuato il provisioning del circuito ExpressRoute e lo stato del circuito deve essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="1d445-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="1d445-113">Se si prevede di usare un hash MD5/chiave condivisa, assicurarsi di usarli su entrambi i lati del tunnel e limitare il numero di caratteri a un massimo di 25.</span><span class="sxs-lookup"><span data-stu-id="1d445-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="1d445-114">Queste istruzioni si applicano solo ai circuiti creati con provider di servizi che offrono servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="1d445-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="1d445-115">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito una VPN IP, come MPLS), il provider di connettività configura e gestisce il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1d445-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1d445-116">Attualmente non vengono annunciati peering configurati da provider di servizi tramite il portale di gestione del servizio.</span><span class="sxs-lookup"><span data-stu-id="1d445-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="1d445-117">L'abilitazione di questa funzionalità sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="1d445-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="1d445-118">Rivolgersi al provider di servizi prima di configurare peering BGP.</span><span class="sxs-lookup"><span data-stu-id="1d445-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="1d445-119">Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1d445-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="1d445-120">È possibile configurare i peering nell'ordine desiderato.</span><span class="sxs-lookup"><span data-stu-id="1d445-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="1d445-121">assicurandosi, tuttavia, di completare la configurazione di un peering per volta.</span><span class="sxs-lookup"><span data-stu-id="1d445-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="1d445-122">Peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-122">Azure private peering</span></span>

<span data-ttu-id="1d445-123">Questa sezione fornisce le istruzioni per creare, ottenere, aggiornare ed eliminare la configurazione del peering privato di Azure per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d445-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="1d445-124">Per creare un peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-124">To create Azure private peering</span></span>

1. <span data-ttu-id="1d445-125">Configurare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d445-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="1d445-126">Prima di continuare, assicurarsi che il provider di connettività abbia effettuato il provisioning completo del circuito.</span><span class="sxs-lookup"><span data-stu-id="1d445-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="1d445-128">Configurare il peering privato di Azure per il circuito.</span><span class="sxs-lookup"><span data-stu-id="1d445-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="1d445-129">Prima di procedere con i passaggi successivi, verificare che siano presenti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d445-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="1d445-130">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="1d445-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="1d445-131">La subnet non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="1d445-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="1d445-132">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="1d445-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="1d445-133">La subnet non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="1d445-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="1d445-134">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="1d445-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="1d445-135">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="1d445-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="1d445-136">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="1d445-136">AS number for peering.</span></span> <span data-ttu-id="1d445-137">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="1d445-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="1d445-138">È possibile usare il numero AS privato per questo peering.</span><span class="sxs-lookup"><span data-stu-id="1d445-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="1d445-139">Assicurarsi di non usare il numero 65515.</span><span class="sxs-lookup"><span data-stu-id="1d445-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="1d445-140">**Facoltativo:** un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="1d445-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="1d445-141">Selezionare la riga del peering privato di Azure, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![Privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="1d445-143">Configurare il peering privato.</span><span class="sxs-lookup"><span data-stu-id="1d445-143">Configure private peering.</span></span> <span data-ttu-id="1d445-144">L'immagine seguente mostra un esempio di configurazione:</span><span class="sxs-lookup"><span data-stu-id="1d445-144">The following image shows a configuration example:</span></span>

  ![Configurare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="1d445-146">Salvare la configurazione dopo aver specificato tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="1d445-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="1d445-147">Dopo che la configurazione è stata accettata, viene visualizzata una schermata simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Salvare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="1d445-149">Per visualizzare i dettagli relativi al peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-149">To view Azure private peering details</span></span>

<span data-ttu-id="1d445-150">È possibile visualizzare le proprietà del peering privato di Azure selezionandolo.</span><span class="sxs-lookup"><span data-stu-id="1d445-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![Visualizzare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="1d445-152">Per aggiornare la configurazione del peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="1d445-153">È possibile selezionare la riga per il peering e modificare le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="1d445-153">You can select the row for peering and modify the peering properties.</span></span>

![Aggiornare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="1d445-155">Per eliminare un peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-155">To delete Azure private peering</span></span>

<span data-ttu-id="1d445-156">È possibile rimuovere la configurazione del peering facendo clic sull'icona Elimina, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![Eliminare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="1d445-158">Peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-158">Azure public peering</span></span>

<span data-ttu-id="1d445-159">Questa sezione consente di creare, ottenere, aggiornare ed eliminare la configurazione del peering pubblico di Azure per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d445-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="1d445-160">Per creare un peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-160">To create Azure public peering</span></span>

1. <span data-ttu-id="1d445-161">Configurare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d445-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="1d445-162">Prima di continuare, assicurarsi che il provider di connettività abbia effettuato il provisioning completo del circuito.</span><span class="sxs-lookup"><span data-stu-id="1d445-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Elencare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="1d445-164">Configurare il peering pubblico di Azure per il circuito.</span><span class="sxs-lookup"><span data-stu-id="1d445-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="1d445-165">Prima di procedere con i passaggi successivi, verificare che siano presenti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d445-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="1d445-166">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="1d445-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="1d445-167">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="1d445-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="1d445-168">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="1d445-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="1d445-169">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="1d445-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="1d445-170">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="1d445-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="1d445-171">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="1d445-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="1d445-172">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="1d445-172">AS number for peering.</span></span> <span data-ttu-id="1d445-173">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="1d445-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="1d445-174">**Facoltativo:** un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="1d445-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="1d445-175">Selezionare la riga del peering pubblico di Azure, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![Selezionare la riga del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="1d445-177">Configurare il peering pubblico.</span><span class="sxs-lookup"><span data-stu-id="1d445-177">Configure public peering.</span></span> <span data-ttu-id="1d445-178">L'immagine seguente mostra un esempio di configurazione:</span><span class="sxs-lookup"><span data-stu-id="1d445-178">The following image shows a configuration example:</span></span>

  ![Configurare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="1d445-180">Salvare la configurazione dopo aver specificato tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="1d445-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="1d445-181">Dopo che la configurazione è stata accettata, viene visualizzata una schermata simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Salvare la configurazione del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="1d445-183">Per visualizzare i dettagli relativi al peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-183">To view Azure public peering details</span></span>

<span data-ttu-id="1d445-184">È possibile visualizzare le proprietà del peering pubblico di Azure selezionandolo.</span><span class="sxs-lookup"><span data-stu-id="1d445-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![Visualizzare le proprietà del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="1d445-186">Per aggiornare la configurazione del peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="1d445-187">È possibile selezionare la riga per il peering e modificare le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="1d445-187">You can select the row for peering and modify the peering properties.</span></span>

![Selezionare la riga del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="1d445-189">Per eliminare un peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="1d445-189">To delete Azure public peering</span></span>

<span data-ttu-id="1d445-190">È possibile rimuovere la configurazione del peering facendo clic sull'icona Elimina, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![Eliminare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="1d445-192">Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d445-192">Microsoft peering</span></span>

<span data-ttu-id="1d445-193">Questa sezione consente di creare, ottenere, aggiornare ed eliminare la configurazione del peering Microsoft per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d445-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d445-194">Per i circuiti ExpressRoute configurati prima del 1 agosto 2017 tutti i prefissi di servizio saranno annunciati tramite il peering Microsoft, anche se non sono definiti i filtri di route.</span><span class="sxs-lookup"><span data-stu-id="1d445-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="1d445-195">Per il peering Microsoft dei circuiti ExpressRoute configurati dopo il 1 agosto 2017 non verrà annunciato alcun prefisso fino a quando non viene associato un filtro di route al circuito.</span><span class="sxs-lookup"><span data-stu-id="1d445-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="1d445-196">Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1d445-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="1d445-197">Per creare il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d445-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="1d445-198">Configurare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1d445-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="1d445-199">Prima di continuare, assicurarsi che il provider di connettività abbia effettuato il provisioning completo del circuito.</span><span class="sxs-lookup"><span data-stu-id="1d445-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Elencare il peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="1d445-201">Configurare il peering Microsoft per il circuito.</span><span class="sxs-lookup"><span data-stu-id="1d445-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="1d445-202">Prima di procedere, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1d445-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="1d445-203">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="1d445-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="1d445-204">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="1d445-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="1d445-205">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="1d445-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="1d445-206">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="1d445-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="1d445-207">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="1d445-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="1d445-208">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="1d445-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="1d445-209">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="1d445-209">AS number for peering.</span></span> <span data-ttu-id="1d445-210">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="1d445-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="1d445-211">Advertised prefixes: è necessario fornire un elenco di tutti i prefissi che si intende pubblicizzare nella sessione BGP.</span><span class="sxs-lookup"><span data-stu-id="1d445-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="1d445-212">Sono accettati solo prefissi di indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="1d445-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="1d445-213">Se si intende inviare un set di prefissi, è possibile creare un elenco delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="1d445-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="1d445-214">Questi prefissi devono essere intestati all'utente in un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="1d445-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="1d445-215">**Facoltativo -** ASN cliente: se si annunciano prefissi non registrati nel numero AS di peering, è possibile specificare il numero AS in cui sono registrati.</span><span class="sxs-lookup"><span data-stu-id="1d445-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="1d445-216">Routing Registry Name: è possibile specificare il registro RIR/IRR in cui sono registrati il numero AS e i prefissi.</span><span class="sxs-lookup"><span data-stu-id="1d445-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="1d445-217">**Facoltativo:** un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="1d445-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="1d445-218">È possibile selezionare il peering che si vuole configurare, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="1d445-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="1d445-219">Selezionare la riga del peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1d445-219">Select the Microsoft peering row.</span></span>

  ![Selezionare la riga del peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="1d445-221">Configurare il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1d445-221">Configure Microsoft peering.</span></span> <span data-ttu-id="1d445-222">L'immagine seguente mostra un esempio di configurazione:</span><span class="sxs-lookup"><span data-stu-id="1d445-222">The following image shows a configuration example:</span></span>

  ![Configurare il peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="1d445-224">Salvare la configurazione dopo aver specificato tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="1d445-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="1d445-225">Se il circuito raggiunge lo stato "Convalida necessaria", come illustrato nell'immagine, si dovrà aprire un ticket di supporto per fornire la prova della proprietà dei prefissi al team di supporto.</span><span class="sxs-lookup"><span data-stu-id="1d445-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Salvare la configurazione del peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="1d445-227">È possibile aprire un ticket di supporto direttamente dal portale, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="1d445-228">Dopo che la configurazione è stata accettata, viene visualizzata una schermata simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="1d445-229">Per visualizzare i dettagli del peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d445-229">To view Microsoft peering details</span></span>

<span data-ttu-id="1d445-230">È possibile visualizzare le proprietà del peering pubblico di Azure selezionandolo.</span><span class="sxs-lookup"><span data-stu-id="1d445-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="1d445-231">Per aggiornare la configurazione del peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d445-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="1d445-232">È possibile selezionare la riga per il peering e modificare le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="1d445-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="1d445-233">Per eliminare il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d445-233">To delete Microsoft peering</span></span>

<span data-ttu-id="1d445-234">È possibile rimuovere la configurazione del peering facendo clic sull'icona Elimina, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="1d445-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="1d445-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d445-235">Next steps</span></span>

<span data-ttu-id="1d445-236">Successivamente, [collegare una rete virtuale a un circuito ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="1d445-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="1d445-237">Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="1d445-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="1d445-238">Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="1d445-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="1d445-239">Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d445-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
