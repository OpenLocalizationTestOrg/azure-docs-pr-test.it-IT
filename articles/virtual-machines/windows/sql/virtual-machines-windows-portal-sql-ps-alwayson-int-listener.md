---
title: "Configurare i listener dei gruppi di disponibilità AlwaysOn - Microsoft Azure | Microsoft Docs"
description: "Configurare i listener dei gruppi di disponibilità nel modello di Azure Resource Manager usando un servizio di bilanciamento del carico interno con uno o più indirizzi IP."
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
ms.openlocfilehash: 74fa1e4c9cfa608a9a385f3dd82a0599fbcc421c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="c95bc-103">Configurare uno o più listener di gruppi di disponibilità AlwaysOn - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c95bc-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="c95bc-104">Questo argomento illustra come:</span><span class="sxs-lookup"><span data-stu-id="c95bc-104">This topic shows how to:</span></span>

* <span data-ttu-id="c95bc-105">Creare un servizio di bilanciamento del carico interno per gruppi di disponibilità di SQL Server usando i cmdlet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c95bc-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="c95bc-106">Aggiungere altri indirizzi IP a un servizio di bilanciamento del carico per più di un gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c95bc-106">Add additional IP addresses to a load balancer for more than one availability group.</span></span> 

<span data-ttu-id="c95bc-107">Un listener del gruppo di disponibilità è un nome di rete virtuale al quale si connettono i client per l'accesso ai database.</span><span class="sxs-lookup"><span data-stu-id="c95bc-107">An availability group listener is a virtual network name that clients connect to for database access.</span></span> <span data-ttu-id="c95bc-108">Nelle macchine virtuali di Azure, un servizio di bilanciamento del carico contiene l'indirizzo IP del listener.</span><span class="sxs-lookup"><span data-stu-id="c95bc-108">On Azure virtual machines, a load balancer holds the IP address for the listener.</span></span> <span data-ttu-id="c95bc-109">Il servizio di bilanciamento del carico indirizza il traffico all'istanza di SQL Server in ascolto nella porta probe.</span><span class="sxs-lookup"><span data-stu-id="c95bc-109">The load balancer routes traffic to the instance of SQL Server that is listening on the probe port.</span></span> <span data-ttu-id="c95bc-110">In genere, un gruppo di disponibilità usa un servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="c95bc-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="c95bc-111">Un servizio di bilanciamento del carico interno di Azure può ospitare uno o più indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c95bc-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="c95bc-112">Ogni indirizzo IP usa una porta probe specifica.</span><span class="sxs-lookup"><span data-stu-id="c95bc-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="c95bc-113">Questo documento illustra come usare PowerShell per creare un servizio di bilanciamento del carico o aggiungere indirizzi IP a un servizio di bilanciamento del carico esistente per i gruppi di disponibilità di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c95bc-113">This document shows how to use PowerShell to create a load balancer, or add IP addresses to an existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="c95bc-114">La possibilità di assegnare più indirizzi IP a un servizio di bilanciamento del carico interno è una novità di Azure ed è disponibile solo nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c95bc-114">The ability to assign multiple IP addresses to an internal load balancer is new to Azure and is only available in Resource Manager model.</span></span> <span data-ttu-id="c95bc-115">Per completare questa attività, è necessario un gruppo di disponibilità di SQL Server distribuito su macchine virtuali di Azure nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c95bc-115">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="c95bc-116">Entrambe le macchine virtuali di SQL Server devono appartenere allo stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c95bc-116">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="c95bc-117">È possibile usare il [modello Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) per creare automaticamente il gruppo di disponibilità in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c95bc-117">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span></span> <span data-ttu-id="c95bc-118">Questo modello crea automaticamente il gruppo di disponibilità, che include il servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="c95bc-118">This template automatically creates the availability group, including the internal load balancer for you.</span></span> <span data-ttu-id="c95bc-119">Se si preferisce, è possibile [configurare manualmente un gruppo di disponibilità AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="c95bc-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="c95bc-120">Per questo argomento è necessario che i gruppi di disponibilità siano già configurati.</span><span class="sxs-lookup"><span data-stu-id="c95bc-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="c95bc-121">Gli argomenti correlati includono:</span><span class="sxs-lookup"><span data-stu-id="c95bc-121">Related topics include:</span></span>

* [<span data-ttu-id="c95bc-122">Configurare i gruppi di disponibilità AlwaysOn nelle VM di Azure (GUI)</span><span class="sxs-lookup"><span data-stu-id="c95bc-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="c95bc-123">Configurare una connessione da VNet a VNet tramite Azure Resource Manager e PowerShell</span><span class="sxs-lookup"><span data-stu-id="c95bc-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-the-windows-firewall"></a><span data-ttu-id="c95bc-124">Configurare Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="c95bc-124">Configure the Windows Firewall</span></span>
<span data-ttu-id="c95bc-125">Configurare Windows Firewall per consentire l'accesso a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c95bc-125">Configure the Windows Firewall to allow SQL Server access.</span></span> <span data-ttu-id="c95bc-126">Le regole del firewall consentono le connessioni TCP alle porte usate dall'istanza di SQL Server e al probe di listener.</span><span class="sxs-lookup"><span data-stu-id="c95bc-126">The firewall rules allow TCP connections to the ports use by the SQL Server instance, and the listener probe.</span></span> <span data-ttu-id="c95bc-127">Per informazioni dettagliate, vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="c95bc-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="c95bc-128">Creare una regola in entrata per la porta SQL Server e per la porta probe.</span><span class="sxs-lookup"><span data-stu-id="c95bc-128">Create an inbound rule for the SQL Server port and for the probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="c95bc-129">Script di esempio: creare un servizio di bilanciamento del carico interno con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c95bc-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="c95bc-130">Se il gruppo di disponibilità è stato creato con il [modello Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), il bilanciamento del carico interno è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="c95bc-130">If you created your availability group with the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), the internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="c95bc-131">Il seguente script di PowerShell crea un servizio di bilanciamento del carico interno, configura le regole di bilanciamento del carico e imposta un indirizzo IP per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-131">The following PowerShell script creates an internal load balancer, configures the load balancing rules, and sets an IP address for the load balancer.</span></span> <span data-ttu-id="c95bc-132">Per eseguire lo script, aprire Windows PowerShell ISE e copiare lo script nel riquadro Script.</span><span class="sxs-lookup"><span data-stu-id="c95bc-132">To run the script, open Windows PowerShell ISE, and paste the script in the Script pane.</span></span> <span data-ttu-id="c95bc-133">Usare `Login-AzureRMAccount` per l'accesso a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c95bc-133">Use `Login-AzureRMAccount` to log in to PowerShell.</span></span> <span data-ttu-id="c95bc-134">Se si dispone di più sottoscrizioni di Azure, usare `Select-AzureRmSubscription ` per impostare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c95bc-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` to set the subscription.</span></span> 

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

$LBProbeName ="ILBPROBE_$ListenerPort"       # The Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # The Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for the front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for the back-end configuration

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

## <span data-ttu-id="c95bc-135"><a name="Add-IP"></a> Script di esempio: aggiungere un indirizzo IP a un servizio di bilanciamento del carico esistente con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c95bc-135"><a name="Add-IP"></a> Example script: Add an IP address to an existing load balancer with PowerShell</span></span>
<span data-ttu-id="c95bc-136">Per usare più di un gruppo di disponibilità, aggiungere un altro indirizzo IP al bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-136">To use more than one availability group, add an additional IP address to the load balancer.</span></span> <span data-ttu-id="c95bc-137">Ogni indirizzo IP richiede la sua regola di bilanciamento, la sua porta probe e la sua porta front-end.</span><span class="sxs-lookup"><span data-stu-id="c95bc-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="c95bc-138">La porta front-end è quella usata dalle applicazioni per connettersi all'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c95bc-138">The front-end port is the port that applications use to connect to the SQL Server instance.</span></span> <span data-ttu-id="c95bc-139">Gli indirizzi IP per i diversi gruppi di disponibilità possono usare la stessa porta front-end.</span><span class="sxs-lookup"><span data-stu-id="c95bc-139">IP addresses for different availability groups can use the same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="c95bc-140">Per i gruppi di disponibilità di SQL Server, ogni indirizzo IP richiede una porta probe specifica.</span><span class="sxs-lookup"><span data-stu-id="c95bc-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="c95bc-141">Ad esempio, se un indirizzo IP su un servizio di bilanciamento del carico usa la porta probe 59999, nessun altro indirizzo IP in tale servizio di bilanciamento del carico può usare la porta probe 59999.</span><span class="sxs-lookup"><span data-stu-id="c95bc-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="c95bc-142">Per informazioni sui limiti del servizio di bilanciamento del carico, vedere **IP front-end privato per ogni servizio di bilanciamento del carico** in [Limiti relativi alle reti - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="c95bc-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="c95bc-143">Per informazioni sui limiti dei gruppi di disponibilità, vedere [Restrizioni (gruppi di disponibilità)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="c95bc-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="c95bc-144">Lo script seguente aggiunge un nuovo indirizzo IP a un servizio di bilanciamento del carico esistente.</span><span class="sxs-lookup"><span data-stu-id="c95bc-144">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="c95bc-145">Il servizio di bilanciamento del carico interno usa la porta del listener per la porta front-end di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-145">The ILB uses the listener port for the load balancing front-end port.</span></span> <span data-ttu-id="c95bc-146">Questa porta può essere la porta su cui SQL Server è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="c95bc-146">This port can be the port that SQL Server is listening on.</span></span> <span data-ttu-id="c95bc-147">Per le istanze predefinite di SQL Server, la porta è la numero 1433.</span><span class="sxs-lookup"><span data-stu-id="c95bc-147">For default instances of SQL Server, the port is 1433.</span></span> <span data-ttu-id="c95bc-148">La regola di bilanciamento del carico per un gruppo di disponibilità richiede un indirizzo IP mobile (Direct Server Return), quindi la porta back-end corrisponde alla porta front-end.</span><span class="sxs-lookup"><span data-stu-id="c95bc-148">The load balancing rule for an availability group requires a floating IP (direct server return) so the back-end port is the same as the front-end port.</span></span> <span data-ttu-id="c95bc-149">Aggiornare le variabili per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="c95bc-149">Update the variables for your environment.</span></span> 

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

## <a name="configure-the-listener"></a><span data-ttu-id="c95bc-150">Configurare il listener</span><span class="sxs-lookup"><span data-stu-id="c95bc-150">Configure the listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-the-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="c95bc-151">Impostare la porta del listener in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="c95bc-151">Set the listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="c95bc-152">Avviare SQL Server Management Studio e connettersi alla replica primaria.</span><span class="sxs-lookup"><span data-stu-id="c95bc-152">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="c95bc-153">Passare a **Disponibilità elevata AlwaysOn** | **Gruppi di disponibilità** | **Listener gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="c95bc-153">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="c95bc-154">Viene visualizzato il nome del listener creato in Gestione Cluster di Failover.</span><span class="sxs-lookup"><span data-stu-id="c95bc-154">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="c95bc-155">Fare clic con il pulsante destro del mouse sul nome del listener e quindi su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="c95bc-155">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="c95bc-156">Nella casella **Porta** specificare il numero di porta per il listener del gruppo di disponibilità usando il valore di $EndpointPort usato in precedenza (l'impostazione predefinita era 1433), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c95bc-156">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="c95bc-157">Testare la connessione al listener</span><span class="sxs-lookup"><span data-stu-id="c95bc-157">Test the connection to the listener</span></span>

<span data-ttu-id="c95bc-158">Per testare la connessione:</span><span class="sxs-lookup"><span data-stu-id="c95bc-158">To test the connection:</span></span>

1. <span data-ttu-id="c95bc-159">Usare RDP per connettersi a un'istanza di SQL Server che si trova nella stessa rete virtuale, ma non è proprietaria della replica.</span><span class="sxs-lookup"><span data-stu-id="c95bc-159">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="c95bc-160">Può trattarsi dell'altra istanza di SQL Server nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c95bc-160">This can be the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="c95bc-161">Usare l'utilità **sqlcmd** per testare la connessione.</span><span class="sxs-lookup"><span data-stu-id="c95bc-161">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="c95bc-162">Lo script seguente, ad esempio, stabilisce una connessione **sqlcmd** alla replica primaria tramite il listener con l'autenticazione di Windows:</span><span class="sxs-lookup"><span data-stu-id="c95bc-162">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="c95bc-163">Se il listener usa una porta diversa da quella predefinita (1433), specificare la porta nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="c95bc-163">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="c95bc-164">Il seguente comando sqlcmd, ad esempio, si connette a un listener nella porta 1435:</span><span class="sxs-lookup"><span data-stu-id="c95bc-164">For example, the following sqlcmd command connects to a listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="c95bc-165">La connessione SQLCMD si connette automaticamente a qualsiasi istanza di SQL Server ospiti la replica primaria.</span><span class="sxs-lookup"><span data-stu-id="c95bc-165">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="c95bc-166">Verificare che la porta specificata sia aperta nel firewall di entrambe le istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c95bc-166">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="c95bc-167">Per entrambi i server è necessaria una regola in ingresso per la porta TCP usata.</span><span class="sxs-lookup"><span data-stu-id="c95bc-167">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="c95bc-168">Per altre informazioni, vedere [Aggiungere o modificare una regola del firewall](http://technet.microsoft.com/library/cc753558.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c95bc-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="c95bc-169">Linee guida e limitazioni</span><span class="sxs-lookup"><span data-stu-id="c95bc-169">Guidelines and limitations</span></span>
<span data-ttu-id="c95bc-170">Tenere presente le linee guida seguenti per il listener del gruppo di disponibilità in Azure con il servizio di bilanciamento del carico interno:</span><span class="sxs-lookup"><span data-stu-id="c95bc-170">Note the following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="c95bc-171">Con un servizio di bilanciamento del carico interno è possibile accedere al listener solo dalla stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c95bc-171">With an internal load balancer, you only access the listener from within the same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="c95bc-172">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="c95bc-172">For more information</span></span>
<span data-ttu-id="c95bc-173">Per altre informazioni, vedere [Configurare manualmente i gruppi di disponibilità AlwaysOn nelle VM di Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="c95bc-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="c95bc-174">Cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="c95bc-174">PowerShell cmdlets</span></span>
<span data-ttu-id="c95bc-175">Usare i seguenti cmdlet PowerShell per creare un servizio di bilanciamento del carico interno per le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c95bc-175">Use the following PowerShell cmdlets to create an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="c95bc-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) crea un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="c95bc-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) crea una configurazione IP per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="c95bc-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) crea una regola di configurazione per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="c95bc-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) crea una configurazione di pool di indirizzi per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="c95bc-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) crea una configurazione di probe per un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c95bc-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="c95bc-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) rimuove un bilanciamento del carico da un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c95bc-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
