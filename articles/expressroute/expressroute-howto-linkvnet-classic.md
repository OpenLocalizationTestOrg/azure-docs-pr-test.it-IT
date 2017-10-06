---
title: 'Collegare un circuito ExpressRoute di tooan rete virtuale: PowerShell: classico: Azure | Documenti Microsoft'
description: "Questo documento viene fornita una panoramica della modalità virtuale toolink reti circuiti tooExpressRoute (Vnet) utilizzando il modello di distribuzione classica hello e PowerShell."
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
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="3434a-103">Connettersi a un circuito ExpressRoute tooan di rete virtuale con PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="3434a-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3434a-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3434a-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="3434a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3434a-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="3434a-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3434a-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="3434a-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3434a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="3434a-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="3434a-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="3434a-109">In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure utilizzando il modello di distribuzione classica hello e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3434a-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="3434a-110">Reti virtuali possono essere nella stessa sottoscrizione hello o possono far parte di un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3434a-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="3434a-111">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="3434a-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="3434a-112">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="3434a-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="3434a-113">È necessario più recente dei moduli di Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="3434a-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="3434a-114">È possibile scaricare i moduli di PowerShell più recenti hello dalla sezione PowerShell di hello hello [pagina di download di Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3434a-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="3434a-115">Seguire le istruzioni hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per istruzioni dettagliate su come tooconfigure i moduli di Azure PowerShell hello toouse computer.</span><span class="sxs-lookup"><span data-stu-id="3434a-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="3434a-116">È necessario hello tooreview [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3434a-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="3434a-117">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="3434a-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="3434a-118">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e il provider di connettività abilitare circuito hello.</span><span class="sxs-lookup"><span data-stu-id="3434a-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="3434a-119">Assicurarsi di disporre del peering privato di Azure configurato per il circuito.</span><span class="sxs-lookup"><span data-stu-id="3434a-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="3434a-120">Vedere hello [Configura routing](expressroute-howto-routing-classic.md) articolo per le istruzioni di routing.</span><span class="sxs-lookup"><span data-stu-id="3434a-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="3434a-121">Verificare di peering privato di Azure è configurato hello peering BGP tra la rete e Microsoft sia attivo in modo che è possibile abilitare la connettività end-to-end.</span><span class="sxs-lookup"><span data-stu-id="3434a-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="3434a-122">È necessario disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="3434a-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="3434a-123">Seguire le istruzioni di hello troppo[configurare una rete virtuale per ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="3434a-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="3434a-124">È possibile collegare le reti virtuali di too10 tooan circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3434a-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="3434a-125">Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica.</span><span class="sxs-lookup"><span data-stu-id="3434a-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="3434a-126">È possibile collegare un maggior numero di reti virtuali tooyour circuito ExpressRoute o collegamento di reti virtuali in altre aree di natura geopolitiche se è stato abilitato il componente aggiuntivo di hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="3434a-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="3434a-127">Controllare hello [domande frequenti su](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.</span><span class="sxs-lookup"><span data-stu-id="3434a-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="3434a-128">Connettere una rete virtuale in hello circuito tooa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="3434a-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="3434a-129">È possibile collegare un circuito ExpressRoute di tooan rete virtuale tramite hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3434a-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="3434a-130">Verificare che tale gateway di rete virtuale hello viene creato ed è pronto per il collegamento prima di eseguire il cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="3434a-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="3434a-131">Connettere una rete virtuale in un circuito tooa sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="3434a-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="3434a-132">È possibile condividere un circuito ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="3434a-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="3434a-133">Hello nella figura seguente illustra un semplice schema di funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="3434a-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="3434a-134">Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3434a-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="3434a-135">Per distribuire i servizi, ma reparti hello possono condividere una singola ExpressRoute circuito tooconnect tooyour indietro locale rete, ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3434a-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="3434a-136">Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="3434a-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="3434a-137">Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="3434a-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="3434a-138">Gli addebiti di connettività e larghezza di banda per il circuito dedicato hello sarà proprietario del circuito ExpressRoute toohello applicato.</span><span class="sxs-lookup"><span data-stu-id="3434a-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="3434a-139">Tutte le reti virtuali condividono hello stessa larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="3434a-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="3434a-141">Amministrazione</span><span class="sxs-lookup"><span data-stu-id="3434a-141">Administration</span></span>
<span data-ttu-id="3434a-142">Hello *proprietario del circuito* è hello amministratore/coadministrator di sottoscrizione hello in cui hello ExpressRoute viene creato il circuito.</span><span class="sxs-lookup"><span data-stu-id="3434a-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="3434a-143">Hello proprietario del circuito può autorizzare gli amministratori/coadministrators di altre sottoscrizioni, cui viene fatto riferimento tooas *circuit utenti*, hello toouse dedicato circuito a cui sono proprietari.</span><span class="sxs-lookup"><span data-stu-id="3434a-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="3434a-144">Gli utenti del circuito che sono autorizzati toouse hello del ExpressRoute circuito possono collegano la rete virtuale di hello nella loro toohello sottoscrizione circuito ExpressRoute dopo che sono autorizzati.</span><span class="sxs-lookup"><span data-stu-id="3434a-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="3434a-145">proprietario del circuito Hello ha hello power toomodify e revocare le autorizzazioni per in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="3434a-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="3434a-146">Revoca l'autorizzazione comporterà tutti i collegamenti viene eliminati dalla sottoscrizione hello il cui accesso è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="3434a-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="3434a-147">Operazioni del proprietario del circuito</span><span class="sxs-lookup"><span data-stu-id="3434a-147">Circuit owner operations</span></span>

<span data-ttu-id="3434a-148">**Creazione di un'autorizzazione**</span><span class="sxs-lookup"><span data-stu-id="3434a-148">**Creating an authorization**</span></span>

<span data-ttu-id="3434a-149">proprietario del circuito Hello autorizza gli amministratori di hello di altre sottoscrizioni hello toouse specificato circuito.</span><span class="sxs-lookup"><span data-stu-id="3434a-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="3434a-150">Nell'esempio seguente di hello, messaggio per l'amministratore del circuito hello (Contoso IT) consente di messaggio per l'amministratore di un'altra sottoscrizione (Dev-Test) toolink backup circuito di toohello tootwo reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="3434a-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="3434a-151">messaggio per l'amministratore IT di Contoso ha abilitato specificando l'ID del Test di sviluppo Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="3434a-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="3434a-152">cmdlet di Hello non invia posta elettronica toohello specificato ID Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3434a-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="3434a-153">proprietario del circuito Hello deve tooexplicitly notificare hello di altri proprietario della sottoscrizione che hello autorizzazione è stato completato.</span><span class="sxs-lookup"><span data-stu-id="3434a-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="3434a-154">**Verifica delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="3434a-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="3434a-155">proprietario del circuito Hello è possibile esaminare tutte le autorizzazioni che vengono eseguite su un particolare circuito eseguendo hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3434a-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

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


<span data-ttu-id="3434a-156">**Aggiornamento delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="3434a-156">**Updating authorizations**</span></span>

<span data-ttu-id="3434a-157">proprietario del circuito Hello è possibile modificare le autorizzazioni utilizzando hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3434a-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="3434a-158">**Eliminazione delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="3434a-158">**Deleting authorizations**</span></span>

<span data-ttu-id="3434a-159">proprietario del circuito Hello può revocare/eliminazione utente toohello autorizzazioni eseguendo hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3434a-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="3434a-160">Operazioni dell'utente del circuito</span><span class="sxs-lookup"><span data-stu-id="3434a-160">Circuit user operations</span></span>

<span data-ttu-id="3434a-161">**Verifica delle autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="3434a-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="3434a-162">utente del circuito Hello è possibile esaminare le autorizzazioni utilizzando hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3434a-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

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

<span data-ttu-id="3434a-163">**Riscatto delle autorizzazioni dei collegamenti**</span><span class="sxs-lookup"><span data-stu-id="3434a-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="3434a-164">utente del circuito Hello è possibile eseguire il seguente cmdlet tooredeem hello un'autorizzazione del collegamento:</span><span class="sxs-lookup"><span data-stu-id="3434a-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="3434a-165">Eseguire questo comando nella sottoscrizione hello appena collegato per la rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="3434a-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="3434a-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3434a-166">Next steps</span></span>
<span data-ttu-id="3434a-167">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="3434a-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

