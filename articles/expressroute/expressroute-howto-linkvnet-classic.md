---
title: 'Collegamento di una rete virtuale a un circuito ExpressRoute: PowerShell: classico: Azure | Microsoft Docs'
description: Questo documento offre una panoramica sulle procedure di collegamento delle reti virtuali ai circuiti ExpressRoute usando il modello di distribuzione classico e PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 8df8a4c6ff0897c821e13248e0494b17e1a4992d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="db334-103">Collegare una rete virtuale a un circuito ExpressRoute usando PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="db334-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db334-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="db334-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="db334-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db334-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="db334-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="db334-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="db334-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="db334-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="db334-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="db334-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="db334-109">Questo articolo spiega come collegare le reti virtuali ai circuiti di Azure ExpressRoute usando il modello di distribuzione classico e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db334-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="db334-110">Le reti virtuali possono trovarsi nella stessa sottoscrizione o appartenere a un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="db334-110">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="db334-111">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="db334-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="db334-112">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="db334-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="db334-113">È necessario scaricare la versione più recente dei moduli di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db334-113">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="db334-114">È possibile scaricare i moduli di PowerShell più recenti dalla sezione relativa a PowerShell della [pagina Download di Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="db334-114">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="db334-115">Per istruzioni dettagliate sulla configurazione del computer per l'uso dei moduli di Azure PowerShell, seguire le istruzioni contenute in [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="db334-115">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="db334-116">Prima di procedere con la configurazione, è necessario verificare i [prerequisiti](expressroute-prerequisites.md), i [requisiti di routing](expressroute-routing.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="db334-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="db334-117">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="db334-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="db334-118">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo che il circuito venga abilitato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="db334-118">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="db334-119">Assicurarsi di disporre del peering privato di Azure configurato per il circuito.</span><span class="sxs-lookup"><span data-stu-id="db334-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="db334-120">Vedere l'articolo relativo alla [configurazione del routing](expressroute-howto-routing-classic.md) per istruzioni relative al routing.</span><span class="sxs-lookup"><span data-stu-id="db334-120">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="db334-121">Per abilitare la connettività end-to-end, assicurarsi che sia configurato il peering privato di Azure e sia attivo il peering BGP tra la rete e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db334-121">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="db334-122">È necessario disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="db334-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="db334-123">Seguire le istruzioni per [configurare una rete virtuale per ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="db334-123">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="db334-124">È possibile collegare fino a 10 reti virtuali a un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="db334-124">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="db334-125">Tutte le reti virtuali devono trovarsi nella stessa area geopolitica.</span><span class="sxs-lookup"><span data-stu-id="db334-125">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="db334-126">È possibile collegare un numero maggiore di reti virtuali al circuito ExpressRoute o collegare reti virtuali che non sono presenti in altre aree geopolitiche se è stato abilitato il componente aggiuntivo ExpressRoute Premium.</span><span class="sxs-lookup"><span data-stu-id="db334-126">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="db334-127">Per altre informazioni sul componente aggiuntivo Premium, vedere le [domande frequenti](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="db334-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="db334-128">Collegare una rete virtuale della stessa sottoscrizione a un circuito</span><span class="sxs-lookup"><span data-stu-id="db334-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="db334-129">È possibile collegare una rete virtuale a un circuito ExpressRoute usando il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="db334-129">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="db334-130">Prima di eseguire il cmdlet, assicurarsi che il gateway di rete virtuale sia stato creato e sia pronto per il collegamento.</span><span class="sxs-lookup"><span data-stu-id="db334-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="db334-131">Collegare una rete virtuale di un'altra sottoscrizione a un circuito</span><span class="sxs-lookup"><span data-stu-id="db334-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="db334-132">È possibile condividere un circuito ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="db334-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="db334-133">La figura seguente mostra un semplice schema del funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="db334-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="db334-134">Ciascuno dei cloud più piccoli nel cloud di grandi dimensioni viene usato per rappresentare le sottoscrizioni appartenenti a reparti diversi di un'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="db334-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="db334-135">Ciascun reparto dell'organizzazione può usare la propria sottoscrizione per distribuire i servizi, ma i reparti possono condividere un singolo circuito ExpressRoute per la connessione alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="db334-135">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="db334-136">Un singolo reparto (in questo esempio, IT) può possedere il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="db334-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="db334-137">Altre sottoscrizioni all'interno dell'organizzazione possono usare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="db334-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="db334-138">I costi relativi a connettività e larghezza di banda per il circuito dedicato saranno addebitati al proprietario del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="db334-138">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="db334-139">Tutte le reti virtuali condividono la stessa larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="db334-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="db334-141">Amministrazione</span><span class="sxs-lookup"><span data-stu-id="db334-141">Administration</span></span>
<span data-ttu-id="db334-142">Il *proprietario del circuito* è l'amministratore o il coamministratore della sottoscrizione in cui viene creato il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="db334-142">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="db334-143">Il proprietario del circuito può autorizzare gli amministratori o i coamministratori di altre sottoscrizioni, indicati come *utenti del circuito*, a usare il proprio circuito dedicato.</span><span class="sxs-lookup"><span data-stu-id="db334-143">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="db334-144">Gli utenti del circuito autorizzati a usare il circuito ExpressRoute dell'organizzazione possono collegare la rete virtuale della propria sottoscrizione al circuito ExpressRoute dopo aver ricevuto l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="db334-144">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="db334-145">Il proprietario del circuito ha la facoltà di modificare e revocare le autorizzazioni in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="db334-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="db334-146">La revoca dell'autorizzazione comporterà l'eliminazione di tutti i collegamenti dalla sottoscrizione di cui è stato revocato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="db334-146">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="db334-147">Operazioni del proprietario del circuito</span><span class="sxs-lookup"><span data-stu-id="db334-147">Circuit owner operations</span></span>

<span data-ttu-id="db334-148">**Creazione di un'autorizzazione**</span><span class="sxs-lookup"><span data-stu-id="db334-148">**Creating an authorization**</span></span>

<span data-ttu-id="db334-149">Il proprietario del circuito autorizza gli amministratori di altre sottoscrizioni a usare il circuito specificato.</span><span class="sxs-lookup"><span data-stu-id="db334-149">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="db334-150">Nell'esempio seguente l'amministratore del circuito (Contoso IT) abilita l'amministratore di un'altra sottoscrizione (sviluppo/test) per collegare fino a due reti virtuali al circuito.</span><span class="sxs-lookup"><span data-stu-id="db334-150">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="db334-151">L'amministratore di Contoso IT esegue l'abilitazione specificando l'ID Microsoft di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="db334-151">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="db334-152">Il cmdlet non invia messaggi di posta elettronica all'ID di Microsoft specificato.</span><span class="sxs-lookup"><span data-stu-id="db334-152">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="db334-153">Il proprietario del circuito deve indicare in modo esplicito al proprietario dell'altra sottoscrizione che l'autorizzazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db334-153">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="db334-154">**Verifica delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="db334-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="db334-155">Il proprietario del circuito può esaminare tutte le autorizzazioni rilasciate in un particolare circuito eseguendo il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="db334-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="db334-156">**Aggiornamento delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="db334-156">**Updating authorizations**</span></span>

<span data-ttu-id="db334-157">Il proprietario del circuito può modificare le autorizzazioni usando il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="db334-157">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="db334-158">**Eliminazione delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="db334-158">**Deleting authorizations**</span></span>

<span data-ttu-id="db334-159">Il proprietario del circuito può revocare o eliminare le autorizzazioni dell'utente eseguendo il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="db334-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="db334-160">Operazioni dell'utente del circuito</span><span class="sxs-lookup"><span data-stu-id="db334-160">Circuit user operations</span></span>

<span data-ttu-id="db334-161">**Verifica delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="db334-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="db334-162">L'utente del circuito può esaminare le autorizzazioni usando il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="db334-162">The circuit user can review authorizations by using the following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="db334-163">**Riscatto delle autorizzazioni dei collegamenti**</span><span class="sxs-lookup"><span data-stu-id="db334-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="db334-164">L'utente del circuito può eseguire il cmdlet seguente per riscattare un'autorizzazione di collegamento:</span><span class="sxs-lookup"><span data-stu-id="db334-164">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="db334-165">Eseguire questo comando nella sottoscrizione appena collegata per la rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="db334-165">Run this command in the newly linked subscription for the virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="db334-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db334-166">Next steps</span></span>
<span data-ttu-id="db334-167">Per altre informazioni su ExpressRoute, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="db334-167">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

