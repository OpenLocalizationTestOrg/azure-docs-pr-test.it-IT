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
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Configurare uno o più listener di gruppi di disponibilità AlwaysOn - Resource Manager
Questo argomento illustra come:

* Creare un servizio di bilanciamento del carico interno per gruppi di disponibilità di SQL Server usando i cmdlet PowerShell.
* Aggiungere ulteriore IP indirizzi tooa bilanciamento del carico per più di un gruppo di disponibilità. 

Un listener del gruppo di disponibilità è un nome di rete virtuale che i client si connettono toofor accesso al database. Nelle macchine virtuali di Azure, un bilanciamento del carico contiene l'indirizzo IP hello per listener hello. le route del servizio di bilanciamento carico di Hello traffico toohello istanza di SQL Server che è in ascolto sulla porta probe hello. In genere, un gruppo di disponibilità usa un servizio di bilanciamento del carico interno. Un servizio di bilanciamento del carico interno di Azure può ospitare uno o più indirizzi IP. Ogni indirizzo IP usa una porta probe specifica. Questo documento illustra come toouse PowerShell toocreate un bilanciamento del carico, o aggiungere gli indirizzi IP tooan bilanciamento del carico esistente per gruppi di disponibilità di SQL Server. 

Hello possibilità tooassign bilanciamento del carico interno tooan gli indirizzi IP più tooAzure nuovo ed è disponibile nel modello di gestione risorse. toocomplete questa attività, è necessario toohave distribuito un gruppo di disponibilità di SQL Server in macchine virtuali nel modello di gestione risorse di Azure. Entrambe le macchine virtuali di SQL Server deve appartenere toohello stesso set di disponibilità. È possibile utilizzare hello [modello Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically creare il gruppo di disponibilità di hello in Gestione risorse di Azure. Questo modello crea automaticamente il gruppo di disponibilità hello, tra cui bilanciamento del carico interno hello. Se si preferisce, è possibile [configurare manualmente un gruppo di disponibilità AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Per questo argomento è necessario che i gruppi di disponibilità siano già configurati.  

Gli argomenti correlati includono:

* [Configurare i gruppi di disponibilità AlwaysOn nelle VM di Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configurare una connessione da VNet a VNet tramite Azure Resource Manager e PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Configurare Windows Firewall hello
Configurare l'accesso a SQL Server tooallow hello Windows Firewall. regole del firewall Hello consentono di utilizzano le porte TCP connessioni toohello dall'istanza di SQL Server hello e un probe di listener hello. Per informazioni dettagliate, vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Creare una regola in entrata per hello porta SQL Server e per la porta probe hello.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Script di esempio: creare un servizio di bilanciamento del carico interno con PowerShell
> [!NOTE]
> Se è stato creato il gruppo di disponibilità con hello [modello Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), bilanciamento del carico interno hello è già stato creato. 
> 
> 

Hello script PowerShell seguente crea un servizio di bilanciamento del carico interno, configura le regole di bilanciamento del carico di hello e imposta un indirizzo IP di bilanciamento del carico hello. script di hello toorun, aprire Windows PowerShell ISE e incollare script hello nel riquadro di Script hello. Utilizzare `Login-AzureRMAccount` toolog in tooPowerShell. Se si dispone di più sottoscrizioni di Azure, utilizzare `Select-AzureRmSubscription ` sottoscrizione hello tooset. 

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

## <a name="Add-IP"></a>Script di esempio: aggiungere un IP indirizzo tooan esistente bilanciamento del carico con PowerShell
toouse più di un gruppo di disponibilità, è possibile aggiungere un bilanciamento del carico toohello indirizzi IP aggiuntivo. Ogni indirizzo IP richiede la sua regola di bilanciamento, la sua porta probe e la sua porta front-end.

porta front-end di Hello è porta hello utilizzati dalle applicazioni tooconnect toohello istanza di SQL Server. Gli indirizzi IP per possono utilizzare gruppi di disponibilità diverso hello stessa porta front-end.

> [!NOTE]
> Per i gruppi di disponibilità di SQL Server, ogni indirizzo IP richiede una porta probe specifica. Ad esempio, se un indirizzo IP su un servizio di bilanciamento del carico usa la porta probe 59999, nessun altro indirizzo IP in tale servizio di bilanciamento del carico può usare la porta probe 59999.

* Per informazioni sui limiti del servizio di bilanciamento del carico, vedere **IP front-end privato per ogni servizio di bilanciamento del carico** in [Limiti relativi alle reti - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Per informazioni sui limiti dei gruppi di disponibilità, vedere [Restrizioni (gruppi di disponibilità)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Hello script seguente aggiunge un nuovo IP indirizzo tooan bilanciamento del carico esistente. Hello ILB utilizza la porta di listener hello per le porte front-end di bilanciamento del carico di hello. È possibile porta hello che SQL Server è in ascolto su questa porta. Per le istanze predefinite di SQL Server, porta hello è 1433. regola per un gruppo di disponibilità di bilanciamento del carico di Hello richiede un indirizzo IP mobile (direct server restituito) è la porta back-end hello hello stesso come porta front-end hello. Aggiornare le variabili di hello per l'ambiente. 

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

## <a name="configure-hello-listener"></a>Configurare il listener hello

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>Impostare la porta di attesa hello in SQL Server Management Studio

1. Avviare SQL Server Management Studio e connettersi toohello la replica primaria.

1. Passare troppo**disponibilità elevata AlwaysOn** | **gruppi di disponibilità** | **listener del gruppo di disponibilità**. 

1. Viene visualizzato il nome del listener hello creati in Gestione Cluster di Failover. Il nome del listener hello destro e fare clic su **proprietà**.

1. In hello **porta** , specificare il numero di porta hello del listener del gruppo di disponibilità hello utilizzando hello $EndpointPort utilizzato in precedenza (1433 è predefinito hello), quindi fare clic su **OK**.

## <a name="test-hello-connection-toohello-listener"></a>Listener toohello connessione hello di test

connessione hello tootest:

1. RDP tooa SQL Server in hello stesso virtuale di rete, ma non non replica hello personalizzati. Questo può essere hello altro Server SQL cluster hello.

1. Utilizzare **sqlcmd** connessione hello tootest di utilità. Ad esempio, lo script seguente hello stabilisce un **sqlcmd** replica primaria toohello di connessione tramite il listener hello con l'autenticazione di Windows:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Se il listener di hello utilizza una porta diversa da hello predefinita (1433) di porta, specificare la porta hello nella stringa di connessione hello. Ad esempio, hello comando sqlcmd riportato di seguito si connette tooa listener a porta 1435: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

connessione SQLCMD Hello si connette automaticamente toowhichever istanza di SQL Server ospitata hello la replica primaria. 

> [!NOTE]
> Assicurarsi che sia aperta nel firewall hello di entrambi i server SQL porta hello specificata. Entrambi i server richiedono una regola in ingresso per hello la porta TCP in uso. Per altre informazioni, vedere [Aggiungere o modificare una regola del firewall](http://technet.microsoft.com/library/cc753558.aspx) . 
> 
> 

## <a name="guidelines-and-limitations"></a>Linee guida e limitazioni
Si noti hello indicazioni sul listener del gruppo di disponibilità in Azure tramite il bilanciamento del carico interno:

* Con un servizio di bilanciamento del carico interno, si accedere solo ai listener hello all'interno di hello stessa rete virtuale.


## <a name="for-more-information"></a>Per altre informazioni
Per altre informazioni, vedere [Configurare manualmente i gruppi di disponibilità AlwaysOn nelle VM di Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

## <a name="powershell-cmdlets"></a>Cmdlet PowerShell
Utilizzare hello seguendo i cmdlet di PowerShell toocreate un bilanciamento del carico interno per macchine virtuali di Azure.

* [New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) crea un bilanciamento del carico. 
* [New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) crea una configurazione IP per un bilanciamento del carico. 
* [New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) crea una regola di configurazione per un bilanciamento del carico. 
* [New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) crea una configurazione di pool di indirizzi per un bilanciamento del carico. 
* [New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) crea una configurazione di probe per un bilanciamento del carico.
* [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) rimuove un bilanciamento del carico da un gruppo di risorse di Azure.
