---
title: "aaaConfigure sempre sul listener – Microsoft Azure | Documenti Microsoft"
description: "Configurare i listener del gruppo di disponibilità nel modello di gestione risorse di Azure hello, utilizzando un servizio di bilanciamento del carico interno con uno o più indirizzi IP."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="8d695-103">Configurare uno o più listener di gruppi di disponibilità AlwaysOn - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8d695-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="8d695-104">Questo argomento illustra come:</span><span class="sxs-lookup"><span data-stu-id="8d695-104">This topic shows how to:</span></span>

* <span data-ttu-id="8d695-105">Creare un servizio di bilanciamento del carico interno per gruppi di disponibilità di SQL Server usando i cmdlet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d695-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="8d695-106">Aggiungere ulteriore IP indirizzi tooa bilanciamento del carico per più di un gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="8d695-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="8d695-107">Un listener del gruppo di disponibilità è un nome di rete virtuale che i client si connettono toofor accesso al database.</span><span class="sxs-lookup"><span data-stu-id="8d695-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="8d695-108">Nelle macchine virtuali di Azure, un bilanciamento del carico contiene l'indirizzo IP hello per listener hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="8d695-109">le route del servizio di bilanciamento carico di Hello traffico toohello istanza di SQL Server che è in ascolto sulla porta probe hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="8d695-110">In genere, un gruppo di disponibilità usa un servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="8d695-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="8d695-111">Un servizio di bilanciamento del carico interno di Azure può ospitare uno o più indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="8d695-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="8d695-112">Ogni indirizzo IP usa una porta probe specifica.</span><span class="sxs-lookup"><span data-stu-id="8d695-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="8d695-113">Questo documento illustra come toouse PowerShell toocreate un bilanciamento del carico, o aggiungere gli indirizzi IP tooan bilanciamento del carico esistente per gruppi di disponibilità di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8d695-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="8d695-114">Hello possibilità tooassign bilanciamento del carico interno tooan gli indirizzi IP più tooAzure nuovo ed è disponibile nel modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="8d695-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="8d695-115">toocomplete questa attività, è necessario toohave distribuito un gruppo di disponibilità di SQL Server in macchine virtuali nel modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d695-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="8d695-116">Entrambe le macchine virtuali di SQL Server deve appartenere toohello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="8d695-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="8d695-117">È possibile utilizzare hello [modello Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically creare il gruppo di disponibilità di hello in Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d695-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="8d695-118">Questo modello crea automaticamente il gruppo di disponibilità hello, tra cui bilanciamento del carico interno hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="8d695-119">Se si preferisce, è possibile [configurare manualmente un gruppo di disponibilità AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="8d695-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="8d695-120">Per questo argomento è necessario che i gruppi di disponibilità siano già configurati.</span><span class="sxs-lookup"><span data-stu-id="8d695-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="8d695-121">Gli argomenti correlati includono:</span><span class="sxs-lookup"><span data-stu-id="8d695-121">Related topics include:</span></span>

* [<span data-ttu-id="8d695-122">Configurare i gruppi di disponibilità AlwaysOn nelle VM di Azure (GUI)</span><span class="sxs-lookup"><span data-stu-id="8d695-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="8d695-123">Configurare una connessione da VNet a VNet tramite Azure Resource Manager e PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d695-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="8d695-124">Configurare Windows Firewall hello</span><span class="sxs-lookup"><span data-stu-id="8d695-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="8d695-125">Configurare l'accesso a SQL Server tooallow hello Windows Firewall.</span><span class="sxs-lookup"><span data-stu-id="8d695-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="8d695-126">regole del firewall Hello consentono di utilizzano le porte TCP connessioni toohello dall'istanza di SQL Server hello e un probe di listener hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="8d695-127">Per informazioni dettagliate, vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="8d695-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="8d695-128">Creare una regola in entrata per hello porta SQL Server e per la porta probe hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="8d695-129">Script di esempio: creare un servizio di bilanciamento del carico interno con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d695-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="8d695-130">Se è stato creato il gruppo di disponibilità con hello [modello Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), bilanciamento del carico interno hello è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="8d695-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="8d695-131">Hello script PowerShell seguente crea un servizio di bilanciamento del carico interno, configura le regole di bilanciamento del carico di hello e imposta un indirizzo IP di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="8d695-132">script di hello toorun, aprire Windows PowerShell ISE e incollare script hello nel riquadro di Script hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="8d695-133">Utilizzare `Login-AzureRMAccount` toolog in tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d695-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="8d695-134">Se si dispone di più sottoscrizioni di Azure, utilizzare `Select-AzureRmSubscription ` sottoscrizione hello tooset.</span><span class="sxs-lookup"><span data-stu-id="8d695-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="8d695-135"><a name="Add-IP"></a>Script di esempio: aggiungere un IP indirizzo tooan esistente bilanciamento del carico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d695-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="8d695-136">toouse più di un gruppo di disponibilità, è possibile aggiungere un bilanciamento del carico toohello indirizzi IP aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="8d695-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="8d695-137">Ogni indirizzo IP richiede la sua regola di bilanciamento, la sua porta probe e la sua porta front-end.</span><span class="sxs-lookup"><span data-stu-id="8d695-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="8d695-138">porta front-end di Hello è porta hello utilizzati dalle applicazioni tooconnect toohello istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8d695-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="8d695-139">Gli indirizzi IP per possono utilizzare gruppi di disponibilità diverso hello stessa porta front-end.</span><span class="sxs-lookup"><span data-stu-id="8d695-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="8d695-140">Per i gruppi di disponibilità di SQL Server, ogni indirizzo IP richiede una porta probe specifica.</span><span class="sxs-lookup"><span data-stu-id="8d695-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="8d695-141">Ad esempio, se un indirizzo IP su un servizio di bilanciamento del carico usa la porta probe 59999, nessun altro indirizzo IP in tale servizio di bilanciamento del carico può usare la porta probe 59999.</span><span class="sxs-lookup"><span data-stu-id="8d695-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="8d695-142">Per informazioni sui limiti del servizio di bilanciamento del carico, vedere **IP front-end privato per ogni servizio di bilanciamento del carico** in [Limiti relativi alle reti - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="8d695-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="8d695-143">Per informazioni sui limiti dei gruppi di disponibilità, vedere [Restrizioni (gruppi di disponibilità)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="8d695-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="8d695-144">Hello script seguente aggiunge un nuovo IP indirizzo tooan bilanciamento del carico esistente.</span><span class="sxs-lookup"><span data-stu-id="8d695-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="8d695-145">Hello ILB utilizza la porta di listener hello per le porte front-end di bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="8d695-146">È possibile porta hello che SQL Server è in ascolto su questa porta.</span><span class="sxs-lookup"><span data-stu-id="8d695-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="8d695-147">Per le istanze predefinite di SQL Server, porta hello è 1433.</span><span class="sxs-lookup"><span data-stu-id="8d695-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="8d695-148">regola per un gruppo di disponibilità di bilanciamento del carico di Hello richiede un indirizzo IP mobile (direct server restituito) è la porta back-end hello hello stesso come porta front-end hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="8d695-149">Aggiornare le variabili di hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="8d695-149">Update hello variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a><span data-ttu-id="8d695-150">Configurare il listener hello</span><span class="sxs-lookup"><span data-stu-id="8d695-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="8d695-151">Impostare la porta di attesa hello in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="8d695-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="8d695-152">Avviare SQL Server Management Studio e connettersi toohello la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="8d695-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="8d695-153">Passare troppo**disponibilità elevata AlwaysOn** | **gruppi di disponibilità** | **listener del gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="8d695-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="8d695-154">Viene visualizzato il nome del listener hello creati in Gestione Cluster di Failover.</span><span class="sxs-lookup"><span data-stu-id="8d695-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="8d695-155">Il nome del listener hello destro e fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="8d695-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="8d695-156">In hello **porta** , specificare il numero di porta hello del listener del gruppo di disponibilità hello utilizzando hello $EndpointPort utilizzato in precedenza (1433 è predefinito hello), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d695-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="8d695-157">Listener toohello connessione hello di test</span><span class="sxs-lookup"><span data-stu-id="8d695-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="8d695-158">connessione hello tootest:</span><span class="sxs-lookup"><span data-stu-id="8d695-158">tootest hello connection:</span></span>

1. <span data-ttu-id="8d695-159">RDP tooa SQL Server in hello stesso virtuale di rete, ma non non replica hello personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8d695-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="8d695-160">Questo può essere hello altro Server SQL cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="8d695-161">Utilizzare **sqlcmd** connessione hello tootest di utilità.</span><span class="sxs-lookup"><span data-stu-id="8d695-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="8d695-162">Ad esempio, lo script seguente hello stabilisce un **sqlcmd** replica primaria toohello di connessione tramite il listener hello con l'autenticazione di Windows:</span><span class="sxs-lookup"><span data-stu-id="8d695-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="8d695-163">Se il listener di hello utilizza una porta diversa da hello predefinita (1433) di porta, specificare la porta hello nella stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="8d695-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="8d695-164">Ad esempio, hello comando sqlcmd riportato di seguito si connette tooa listener a porta 1435:</span><span class="sxs-lookup"><span data-stu-id="8d695-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="8d695-165">connessione SQLCMD Hello si connette automaticamente toowhichever istanza di SQL Server ospitata hello la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="8d695-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="8d695-166">Assicurarsi che sia aperta nel firewall hello di entrambi i server SQL porta hello specificata.</span><span class="sxs-lookup"><span data-stu-id="8d695-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="8d695-167">Entrambi i server richiedono una regola in ingresso per hello la porta TCP in uso.</span><span class="sxs-lookup"><span data-stu-id="8d695-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="8d695-168">Per altre informazioni, vedere [Aggiungere o modificare una regola del firewall](http://technet.microsoft.com/library/cc753558.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8d695-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="8d695-169">Linee guida e limitazioni</span><span class="sxs-lookup"><span data-stu-id="8d695-169">Guidelines and limitations</span></span>
<span data-ttu-id="8d695-170">Si noti hello indicazioni sul listener del gruppo di disponibilità in Azure tramite il bilanciamento del carico interno:</span><span class="sxs-lookup"><span data-stu-id="8d695-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="8d695-171">Con un servizio di bilanciamento del carico interno, si accedere solo ai listener hello all'interno di hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8d695-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="8d695-172">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="8d695-172">For more information</span></span>
<span data-ttu-id="8d695-173">Per altre informazioni, vedere [Configurare manualmente i gruppi di disponibilità AlwaysOn nelle VM di Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="8d695-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="8d695-174">Cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d695-174">PowerShell cmdlets</span></span>
<span data-ttu-id="8d695-175">Utilizzare hello seguendo i cmdlet di PowerShell toocreate un bilanciamento del carico interno per macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d695-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="8d695-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) crea un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8d695-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="8d695-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) crea una configurazione IP per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8d695-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="8d695-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) crea una regola di configurazione per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8d695-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="8d695-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) crea una configurazione di pool di indirizzi per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8d695-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="8d695-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) crea una configurazione di probe per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8d695-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="8d695-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) rimuove un bilanciamento del carico da un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d695-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
