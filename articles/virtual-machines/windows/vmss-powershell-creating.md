---
title: "scalabilità della macchina virtuale aaaCreating imposta utilizzando i cmdlet di PowerShell | Documenti Microsoft"
description: "Introduzione alla creazione e alla gestione dei set di scalabilità delle macchine virtuali di Azure tramite i cmdlet di Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a>Creazione di set di scalabilità di macchine virtuali con i cmdlet di PowerShell
Questo articolo viene illustrato un esempio di come toocreate un scalabilità della macchina virtuale impostare (VMSS). Crea un set di scalabilità di tre nodi, con la rete e la risorsa di archiviazione associate.

## <a name="first-steps"></a>Primi passaggi
Verificare che si dispone di hello più recente di Azure PowerShell modulo necessari toomaintain toomake di avere i cmdlet di PowerShell hello e creare set di scalabilità.
Passare a strumenti da riga di comando toohello [qui](http://aka.ms/webpi-azps) per hello moduli di Azure più recenti disponibili.

toofind VMSS correlati cmdlet, usare la stringa di ricerca hello \*VMSS\*. Ad esempio _gcm *vmss*_

## <a name="creating-a-vmss"></a>Creazione di un set di scalabilità di macchina virtuale (VMSS)
#### <a name="create-resource-group"></a>Crea gruppo di risorse
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a>Creare la rete (rete virtuale/subnet)
#### <a name="subnet-specification"></a>Specifica della subnet
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a>Specifica della rete virtuale
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a>Creare una risorsa IP pubblica tooAllow accesso esterno
Questo sarà associato toohello bilanciamento del carico.

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a>Crea servizio di bilanciamento del carico
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a>Configurare il bilanciamento del carico
Creare la configurazione del Pool di indirizzi back-end, questo verrà condiviso da hello schede di rete di macchine virtuali hello in set di scalabilità hello.

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

Impostare la porta Probe con bilanciamento di carico, modificare le impostazioni di hello come appropriato per l'applicazione.

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

Creare un pool NAT in ingresso per la connettività indirizzato diretto (non con carico bilanciato) toohello macchine virtuali nella scala hello impostate tramite hello bilanciamento del carico. Si tratta toodemonstrate tramite RDP e potrebbe non essere necessario nell'applicazione.

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

Creare hello regola di con bilanciamento del carico, in questo esempio viene illustrato il carico delle 80 richieste porta bilanciamento del carico, utilizzando le impostazioni di hello nei passaggi precedenti.

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

Creare il bilanciamento del carico con la configurazione.

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

Controllare le impostazioni di LB, controllare carico bilanciato porta configurazioni, si noti che non si vedranno vengono create le regole NAT in ingresso finché hello macchine virtuali nel set di scalabilità hello.

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a>Configurazione e set di scalabilità di hello crea
Si noti che questo esempio di infrastruttura viene illustrato come distribuire tooset backup e il traffico web scala tra set di scalabilità hello ma hello immagini di macchine virtuali specificate qui non dispone dei servizi web installati.

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

Associare tooLoad NIC bilanciamento e Subnet

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

Creare la configurazione del set di scalabilità

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

Definire la configurazione del set di scalabilità

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

Ora è stato creato il set di scalabilità di hello. È possibile testare la connessione toohello singole macchine Virtuali tramite RDP in questo esempio:

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
