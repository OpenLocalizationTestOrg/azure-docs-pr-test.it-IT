---
title: aaaHow tooload bilanciare macchine virtuali di Windows in Azure | Documenti Microsoft
description: "Informazioni su come toouse hello Azure caricare bilanciamento toocreate un'applicazione a elevata disponibilità e sicura tra tre macchine virtuali di Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Come tooload bilanciare macchine virtuali Windows in Azure toocreate applicazioni a disponibilità elevata
Il bilanciamento del carico offre un livello più elevato di disponibilità distribuendo le richieste in ingresso tra più macchine virtuali. In questa esercitazione apprendere hello diversi componenti del servizio di bilanciamento del carico di Azure hello che distribuisce il traffico e garantire disponibilità elevata. Si apprenderà come:

> [!div class="checklist"]
> * Creare un servizio di bilanciamento del carico di Azure
> * Creare un probe di integrità per il servizio di bilanciamento del carico
> * Creare regole del traffico di bilanciamento del carico
> * Utilizzare toocreate estensione Script personalizzata hello un sito IIS di base
> * Creare macchine virtuali e collegare bilanciamento del carico tooa
> * Visualizzare un bilanciamento del carico in azione
> * Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Panoramica di Azure Load Balancer
Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre. Un probe di integrità di bilanciamento del carico consente di monitorare una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM.

Definire una configurazione IP front-end che contenga uno o più indirizzi IP pubblici. Questa configurazione IP front-end consente il toobe di applicazioni e del servizio di bilanciamento del carico accessibile tramite Internet hello. 

Le macchine virtuali connesse tooa bilanciamento del carico utilizzando la scheda di interfaccia di rete virtuale (NIC). toodistribute traffico toohello macchine virtuali, un pool di indirizzi back-end contiene indirizzi IP hello di hello virtuale (NIC) connesse toohello bilanciamento del carico.

flusso di hello toocontrol del traffico, definire regole di bilanciamento del carico per porte specifiche e protocolli che eseguono il mapping delle macchine virtuali tooyour.


## <a name="create-azure-load-balancer"></a>Creare un Azure Load Balancer
Questa sezione descrive come è possibile creare e configurare ciascun componente del servizio di bilanciamento del carico hello. Per poter creare un servizio di bilanciamento del carico è prima necessario creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). esempio Hello crea un gruppo di risorse denominato *myResourceGroupLoadBalancer* in hello *EastUS* percorso:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Creare un indirizzo IP pubblico
tooaccess l'app in hello Internet, è necessario un indirizzo IP pubblico di bilanciamento del carico hello. Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). esempio Hello crea un indirizzo IP pubblico denominato *myPublicIP* in hello *myResourceGroupLoadBalancer* gruppo di risorse:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Creare un servizio di bilanciamento del carico
Creare un indirizzo IP di front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). esempio Hello crea un indirizzo IP di front-end denominato *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Creare un pool di indirizzi back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). esempio Hello crea un pool di indirizzi back-end denominato *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

A questo punto, creare bilanciamento del carico hello con [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). esempio Hello crea un bilanciamento del carico denominato *myLoadBalancer* utilizzando hello *myPublicIP* indirizzo:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Creare un probe di integrità
tooallow hello bilanciamento toomonitor hello stato di caricamento dell'app, utilizzare un probe di integrità. probe di integrità Hello dinamicamente aggiunge o rimuove le macchine virtuali dalla rotazione di bilanciamento del carico hello in base alle loro controlli toohealth di risposta. Per impostazione predefinita, una macchina virtuale viene rimosso dalla distribuzione del servizio di bilanciamento del carico hello dopo due tentativi consecutivi non riusciti a intervalli di 15 secondi. Un probe di integrità viene creato in base a un protocollo o una specifica pagina di controllo integrità per l'app. 

Hello di esempio seguente crea un probe TCP. È anche possibile creare probe HTTP personalizzati per i controlli di integrità con granularità fine. Quando si utilizza un probe HTTP personalizzato, è necessario creare pagina di controllo di integrità hello, ad esempio *healthcheck.aspx*. probe Hello deve restituire un **HTTP 200 OK** risposta per l'host hello carico bilanciamento tookeep hello nella rotazione.

toocreate un probe di integrità TCP, utilizzare [Aggiungi AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). esempio Hello crea un probe di integrità denominato *myHealthProbe* che consente di monitorare ogni macchina virtuale:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Aggiorna bilanciamento del carico hello con [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Creare una regola di bilanciamento del carico
Una regola di bilanciamento del carico è toodefine utilizzato come il traffico è toohello distribuita le macchine virtuali. Definire una configurazione IP front-end di hello per il traffico in ingresso hello e hello back-end pool tooreceive hello traffico IP, con origine necessari hello e porta di destinazione. toomake che solo le macchine virtuali integro ricevano il traffico, è inoltre definire toouse probe di integrità hello.

Creare una regola di bilanciamento del carico con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). esempio Hello crea una regola di bilanciamento del carico denominata *myLoadBalancerRule* e consente di bilanciare il traffico sulla porta *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Aggiorna bilanciamento del carico hello con [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Configurare la rete virtuale
Prima di distribuire alcune macchine virtuali e possibile eseguire il servizio di bilanciamento del test, creare hello che supporta le risorse di rete virtuale. Per ulteriori informazioni sulle reti virtuali, vedere hello [gestire reti virtuali di Azure](tutorial-virtual-network.md) esercitazione.

### <a name="create-network-resources"></a>Creare risorse di rete
Creare una rete virtuale con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). esempio Hello crea una rete virtuale denominata *myVnet* con *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Creare una regola per il gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), quindi creare un gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Aggiungi subnet hello rete sicurezza gruppo toohello con [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e quindi aggiornare la rete virtuale di hello con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

esempio Hello crea una regola di gruppo di sicurezza di rete denominata *myNetworkSecurityGroup* e lo applica troppo*mySubnet*:

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

Vengono create schede di interfaccia di rete virtuale con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello esempio crea tre schede di rete virtuale. (Una scheda di rete virtuale per ogni macchina virtuale viene creato per l'app in hello seguendo i passaggi). È possibile creare macchine virtuali e schede di rete virtuali aggiuntive in qualsiasi momento e aggiungerli toohello servizio di bilanciamento del carico:

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Creare macchine virtuali
disponibilità elevata di hello tooimprove dell'app, posizionare le macchine virtuali in un set di disponibilità.

Creare un set di disponibilità con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). esempio Hello crea un set denominato di disponibilità *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Impostare un amministratore di nome utente e password per le macchine virtuali hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Ora è possibile creare le macchine virtuali hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hello seguente esempio crea tre macchine virtuali:

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Accetta toocreate di pochi minuti e configurare tutte le tre macchine virtuali.

### <a name="install-iis-with-custom-script-extension"></a>Installare IIS con l'estensione dello script personalizzata
Nell'esercitazione precedente su [come una macchina virtuale Windows toocustomize](tutorial-automate-vm-deployment.md), si è appreso come tooautomate personalizzazione con hello Custom Script di estensione per Windows. È possibile utilizzare hello stesso approccio tooinstall e configurare IIS sulle macchine virtuali.

Utilizzare [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello estensione Script personalizzata. Hello estensione esecuzioni `powershell Add-WindowsFeature Web-Server` tooinstall hello server Web IIS e quindi hello aggiornamenti *Default.htm* pagina tooshow hello hostname di hello VM:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Testare il bilanciamento del carico
Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa. sito Hello viene visualizzato, inclusi hello nome host della macchina virtuale hello tale bilanciamento del carico hello distribuite tooas traffico nel seguente esempio hello:

![Esecuzione del sito Web IIS](./media/tutorial-load-balancer/running-iis-website.png)

servizio di bilanciamento del carico hello toosee distribuire il traffico tra tutte le tre macchine virtuali in esecuzione l'app, è possibile forza aggiornamento web browser.


## <a name="add-and-remove-vms"></a>aggiunta e rimozione di VM
È possibile la manutenzione tooperform hello macchine virtuali in esecuzione l'app, ad esempio l'installazione di aggiornamenti del sistema operativo. toodeal con un aumento del traffico tooyour app, potrebbe essere necessario tooadd altre macchine virtuali. In questa sezione illustra come tooremove o aggiungere una macchina virtuale dal servizio di bilanciamento del carico hello.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Rimuovere una macchina virtuale dal servizio di bilanciamento del carico hello
Ottenere l'interfaccia di rete di hello con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), quindi set hello *LoadBalancerBackendAddressPools* proprietà di hello NIC virtuale troppo*$null*. Infine, aggiornare NIC virtuale hello:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

servizio di bilanciamento del carico hello toosee distribuire il traffico tra hello altre due macchine virtuali in esecuzione l'app è possibile forza aggiornamento web browser. È ora possibile eseguire la manutenzione in hello macchina virtuale, ad esempio l'installazione degli aggiornamenti del sistema operativo o l'esecuzione di un riavvio della VM.

### <a name="add-a-vm-toohello-load-balancer"></a>Aggiungere un bilanciamento del carico VM toohello
Dopo che esegue la manutenzione delle macchine Virtuali, o se è necessario tooexpand capacità, impostare hello *LoadBalancerBackendAddressPools* proprietà toohello NIC virtuale hello *BackendAddressPool* da [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Ottieni bilanciamento del carico hello:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è creato un servizio di bilanciamento del carico e collegato tooit macchine virtuali. Si è appreso come:

> [!div class="checklist"]
> * Creare un servizio di bilanciamento del carico di Azure
> * Creare un probe di integrità per il servizio di bilanciamento del carico
> * Creare regole del traffico di bilanciamento del carico
> * Utilizzare toocreate estensione Script personalizzata hello un sito IIS di base
> * Creare macchine virtuali e collegare bilanciamento del carico tooa
> * Visualizzare un bilanciamento del carico in azione
> * Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico

Spostare toolearn esercitazione successiva toohello come reti VM toomanage.

> [!div class="nextstepaction"]
> [Gestire le VM e le reti virtuali](./tutorial-virtual-network.md)
