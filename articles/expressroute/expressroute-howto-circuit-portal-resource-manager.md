---
title: 'Creare e modificare un circuito ExpressRoute: Portale di Azure| Microsoft Docs'
description: Questo articolo descrive le procedure di creazione, provisioning, verifica, aggiornamento, eliminazione e deprovisioning di un circuito ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: e3721cd3c031622788f553e71a6555b844f3f7dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="acc02-103">Creare e modificare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="acc02-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="acc02-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="acc02-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="acc02-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="acc02-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="acc02-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="acc02-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="acc02-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="acc02-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="acc02-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="acc02-109">Questo articolo descrive la procedura di creazione di un circuito ExpressRoute di Azure usando il portale di Azure e il modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="acc02-109">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="acc02-110">I passaggi seguenti descrivono anche come controllare lo stato del circuito ed eseguirne l'aggiornamento, l'eliminazione e il deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="acc02-110">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="acc02-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="acc02-111">Before you begin</span></span>
* <span data-ttu-id="acc02-112">Prima di iniziare la configurazione, verificare i [prerequisiti](expressroute-prerequisites.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="acc02-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="acc02-113">Verificare di avere accesso al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="acc02-113">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="acc02-114">Verificare di avere le autorizzazioni necessarie per creare nuove risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="acc02-114">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="acc02-115">Se non si hanno le autorizzazioni appropriate, contattare l'amministratore dell'account.</span><span class="sxs-lookup"><span data-stu-id="acc02-115">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="acc02-116">È possibile [visualizzare un video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) prima di iniziare, per ottenere una comprensione migliore della procedura.</span><span class="sxs-lookup"><span data-stu-id="acc02-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="acc02-117">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="acc02-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="acc02-118">1. Accedere al portale di Azure</span><span class="sxs-lookup"><span data-stu-id="acc02-118">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="acc02-119">In un browser passare al [portale di Azure](http://portal.azure.com) e accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="acc02-119">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="acc02-120">2. Creare un nuovo circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="acc02-121">Il circuito ExpressRoute viene addebitato dal momento in cui emessa una chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="acc02-121">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="acc02-122">Verificare che l'operazione venga eseguita quando il provider di connettività è pronto a effettuare il provisioning del circuito.</span><span class="sxs-lookup"><span data-stu-id="acc02-122">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

1. <span data-ttu-id="acc02-123">È possibile creare un circuito ExpressRoute selezionando l'opzione che consente di creare una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="acc02-123">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="acc02-124">Fare clic su **Nuovo** > **Rete** > **ExpressRoute**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="acc02-124">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![Creare un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="acc02-126">Dopo aver fatto clic su **ExpressRoute**, verrà visualizzato il pannello **Crea un circuito ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="acc02-126">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="acc02-127">Quando si compila questo pannello, verificare che siano specificati i valori corretti per il livello SKU e la misurazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="acc02-127">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="acc02-128">**livello** determina se è abilitato un componente aggiuntivo ExpressRoute Standard o ExpressRoute Premium.</span><span class="sxs-lookup"><span data-stu-id="acc02-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="acc02-129">È possibile specificare **Standard** per ottenere lo SKU Standard o **Premium** per il componente aggiuntivo Premium.</span><span class="sxs-lookup"><span data-stu-id="acc02-129">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="acc02-130">**misurazione dei dati** determina il tipo di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="acc02-130">**Data metering** determines the billing type.</span></span> <span data-ttu-id="acc02-131">È possibile specificare **A consumo** per un piano dati a consumo e **Senza limiti** per un piano dati illimitato.</span><span class="sxs-lookup"><span data-stu-id="acc02-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="acc02-132">Si noti che è possibile modificare il tipo di fatturazione da **A consumo** a **Senza limiti**, ma non è possibile passare da **Senza limiti** ad **A consumo**.</span><span class="sxs-lookup"><span data-stu-id="acc02-132">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![Configurazione del livello SKU e misurazione dei dati](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="acc02-134">Tenere presente che il percorso di Peering indica la [posizione fisica](expressroute-locations.md) in cui si esegue il peering con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="acc02-134">Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="acc02-135">Questo percorso **non** è collegato alla proprietà "Location", ovvero all'area geografica in cui si trova il provider di risorse di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="acc02-135">This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located.</span></span> <span data-ttu-id="acc02-136">Dal momento che non sono collegati, è consigliabile scegliere un provider di risorse di rete geograficamente vicino alla posizione di peering del circuito.</span><span class="sxs-lookup"><span data-stu-id="acc02-136">While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit.</span></span> 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="acc02-137">3. Visualizzare circuiti e proprietà</span><span class="sxs-lookup"><span data-stu-id="acc02-137">3. View the circuits and properties</span></span>
<span data-ttu-id="acc02-138">**Visualizzare tutti i circuiti**</span><span class="sxs-lookup"><span data-stu-id="acc02-138">**View all the circuits**</span></span>

<span data-ttu-id="acc02-139">È possibile visualizzare tutti i circuiti creati selezionando **Tutte le risorse** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="acc02-139">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![Visualizzazione dei circuiti](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="acc02-141">**Visualizzare le proprietà**</span><span class="sxs-lookup"><span data-stu-id="acc02-141">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![Visualizza proprietà](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="acc02-143">4. Inviare la chiave di servizio al provider di connettività per il provisioning</span><span class="sxs-lookup"><span data-stu-id="acc02-143">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="acc02-144">In questo pannello **Stato provider** offre informazioni sullo stato di provisioning corrente sul lato provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="acc02-144">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="acc02-145">**Stato circuito** indica lo stato sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="acc02-145">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="acc02-146">Per altre informazioni sullo stato di provisioning dei circuiti, vedere l'articolo relativo ai [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="acc02-146">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="acc02-147">Quando si crea un nuovo circuito ExpressRoute, il circuito ha lo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="acc02-147">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="acc02-148">Stato provider: Senza provisioning</span><span class="sxs-lookup"><span data-stu-id="acc02-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="acc02-149">Stato circuito: Abilitato</span><span class="sxs-lookup"><span data-stu-id="acc02-149">Circuit status: Enabled</span></span>

![Avvio del processo di provisioning](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="acc02-151">Il circuito passa allo stato seguente quando è in corso l'abilitazione da parte del provider di connettività:</span><span class="sxs-lookup"><span data-stu-id="acc02-151">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="acc02-152">Stato provider: Provisioning in corso</span><span class="sxs-lookup"><span data-stu-id="acc02-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="acc02-153">Stato circuito: Abilitato</span><span class="sxs-lookup"><span data-stu-id="acc02-153">Circuit status: Enabled</span></span>

<span data-ttu-id="acc02-154">Per poterlo usare, un circuito ExpressRoute deve avere lo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="acc02-154">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="acc02-155">Stato provider: Provisioning eseguito</span><span class="sxs-lookup"><span data-stu-id="acc02-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="acc02-156">Stato circuito: Abilitato</span><span class="sxs-lookup"><span data-stu-id="acc02-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="acc02-157">5. Controllare periodicamente lo stato e la condizione della chiave del circuito</span><span class="sxs-lookup"><span data-stu-id="acc02-157">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="acc02-158">Selezionare il circuito desiderato per visualizzare le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="acc02-158">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="acc02-159">Prima di continuare, controllare che **Stato provider** sia passato a **Provisioning eseguito**.</span><span class="sxs-lookup"><span data-stu-id="acc02-159">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![Stato del circuito e del provider](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="acc02-161">6. Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="acc02-161">6. Create your routing configuration</span></span>
<span data-ttu-id="acc02-162">Per istruzioni dettagliate, vedere l'articolo relativo alla [configurazione del routing per un circuito ExpressRoute](expressroute-howto-routing-portal-resource-manager.md) per creare e modificare i peering del circuito.</span><span class="sxs-lookup"><span data-stu-id="acc02-162">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acc02-163">Queste istruzioni si applicano solo ai circuiti creati con provider di servizi che offrono servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="acc02-163">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="acc02-164">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="acc02-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="acc02-165">7. Collegare una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-165">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="acc02-166">Collegare quindi una rete virtuale al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="acc02-166">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="acc02-167">Fare riferimento all'articolo [Collegare una rete virtuale a un circuito ExpressRoute](expressroute-howto-linkvnet-arm.md) quando si usa il modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="acc02-167">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="acc02-168">Ottenere lo stato di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-168">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="acc02-169">Selezionare un circuito per visualizzarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="acc02-169">You can view the status of a circuit by selecting it.</span></span> 

![Stato di un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="acc02-171">Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="acc02-172">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="acc02-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="acc02-173">È possibile eseguire le operazioni seguenti senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="acc02-173">You can do the following with no downtime:</span></span>

* <span data-ttu-id="acc02-174">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="acc02-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="acc02-175">Aumentare la larghezza di banda del circuito ExpressRoute, a condizione che sulla porta sia disponibile capacità.</span><span class="sxs-lookup"><span data-stu-id="acc02-175">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="acc02-176">Si noti che il downgrade della larghezza di banda di un circuito non è supportato.</span><span class="sxs-lookup"><span data-stu-id="acc02-176">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="acc02-177">Modificare il piano di misurazione da Dati a consumo a Dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="acc02-177">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="acc02-178">Si noti che la modifica del piano di misurazione da Dati senza limiti a Dati a consumo non è supportata.</span><span class="sxs-lookup"><span data-stu-id="acc02-178">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="acc02-179">È possibile abilitare e disabilitare l'opzione *Consenti operazioni classiche*.</span><span class="sxs-lookup"><span data-stu-id="acc02-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="acc02-180">Per altre informazioni su limiti e limitazioni, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="acc02-180">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="acc02-181">Per modificare un circuito ExpressRoute, fare clic su **Configurazione**, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="acc02-181">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![Modificare il circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="acc02-183">È possibile modificare larghezza di banda, SKU e modello di fatturazione e consentire operazioni classiche nel pannello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="acc02-183">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acc02-184">Se la capacità sulla porta esistente non è sufficiente, potrebbe essere necessario ricreare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="acc02-184">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="acc02-185">Il circuito non può essere aggiornato se in tale posizione non è disponibile capacità aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="acc02-185">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="acc02-186">Non è possibile ridurre la larghezza di banda di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="acc02-186">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="acc02-187">Il downgrade della larghezza di banda richiede il deprovisioning del circuito ExpressRoute e quindi il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="acc02-187">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="acc02-188">La disabilitazione dell'operazione aggiuntiva premium può avere esito negativo se si usano più risorse di quelle consentite per il circuito standard.</span><span class="sxs-lookup"><span data-stu-id="acc02-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="acc02-189">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="acc02-190">È possibile eliminare il circuito ExpressRoute selezionando l'icona di **eliminazione** .</span><span class="sxs-lookup"><span data-stu-id="acc02-190">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="acc02-191">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="acc02-191">Note the following:</span></span>

* <span data-ttu-id="acc02-192">È necessario scollegare tutte le reti virtuali dal circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="acc02-192">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="acc02-193">Se l'operazione non riesce, controllare se sono presenti reti virtuali collegate al circuito.</span><span class="sxs-lookup"><span data-stu-id="acc02-193">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="acc02-194">Se lo stato di provisioning del provider del servizio del circuito ExpressRoute è **Provisioning in corso** o **Provisioning eseguito**, è necessario collaborare con il provider di servizi per eseguire il deprovisioning del circuito sul lato del provider.</span><span class="sxs-lookup"><span data-stu-id="acc02-194">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="acc02-195">Le risorse continueranno a essere riservate e la fatturazione continuerà a essere applicata finché il provider di servizi non avrà completato il deprovisioning del circuito e inviato una notifica a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="acc02-195">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="acc02-196">Se il provider di servizi ha eseguito il deprovisioning del circuito, ovvero lo stato di provisioning del provider di servizi è impostato su **Senza provisioning**, è possibile eliminare il circuito.</span><span class="sxs-lookup"><span data-stu-id="acc02-196">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="acc02-197">Non verrà più applicata la fatturazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="acc02-197">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="acc02-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acc02-198">Next steps</span></span>
<span data-ttu-id="acc02-199">Dopo aver creato il circuito, verificare di eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="acc02-199">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="acc02-200">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="acc02-201">Collegare la rete virtuale al circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acc02-201">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

