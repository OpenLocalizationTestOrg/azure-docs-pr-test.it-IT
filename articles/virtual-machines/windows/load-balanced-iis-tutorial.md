---
title: "aaaTutorial - compilazione di applicazioni a disponibilità elevata in macchine virtuali di Azure | Documenti Microsoft"
description: "Informazioni su come toocreate un'applicazione a elevata disponibilità e sicura tra tre macchine virtuali di Windows con un bilanciamento del carico in Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Creare un'applicazione con un servizio di bilanciamento del carico a disponibilità elevata in macchine virtuali Windows in Azure

In questa esercitazione è creare un'applicazione a disponibilità elevata resilienti toomaintenance eventi. app Hello utilizza un bilanciamento del carico, un set di disponibilità e tre macchine virtuali di Windows (VM). In questa esercitazione viene installato IIS, sebbene sia possibile utilizzare questa esercitazione toodeploy un framework di applicazioni diverso utilizzando hello linee guida e i componenti di un'elevata disponibilità stesso. 

## <a name="step-1---azure-prerequisites"></a>Passaggio 1: Prerequisiti di Azure

toocomplete questa esercitazione, assicurarsi di avere installato più recente hello [Azure PowerShell](/powershell/azure/overview) modulo.

Innanzitutto, accedi tooyour sottoscrizione di Azure con il comando account di accesso AzureRmAccount hello e seguire hello le direzioni.

```powershell
Login-AzureRmAccount
```

Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. Prima di poter creare altre risorse di Azure, è necessario toocreate un gruppo di risorse con [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` area: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Passaggio 2: Creare un set di disponibilità

Le macchine virtuali possono essere create in domini logici di errore e di aggiornamento. Ogni dominio logico rappresenta una parte dell'hardware nel Data Center di Azure sottostante hello. Quando si creano due o più VM, le risorse di calcolo e di archiviazione vengono distribuite in tali domini. Questa distribuzione mantiene la disponibilità di hello dell'app se un componente hardware necessità di manutenzione. I set di disponibilità consentono di definire questi domini logici di errore e di aggiornamento.

Creare un set di disponibilità con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). esempio Hello crea un set denominato di disponibilità `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>Passaggio 3: Creare il servizio di bilanciamento del carico

Un servizio di bilanciamento del carico di Azure distribuisce il traffico tra un set di VM definite usando regole di bilanciamento del carico. Un probe di integrità esegue il monitoraggio di una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM.

### <a name="create-public-ip-address"></a>Creare un indirizzo IP pubblico

tooaccess l'app in hello Internet, assegnare un bilanciamento del carico toohello indirizzo IP pubblico. Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). esempio Hello crea un indirizzo IP pubblico denominato `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Creare un servizio di bilanciamento del carico

Creare un indirizzo IP di front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). esempio Hello crea un indirizzo IP di front-end denominato `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Creare un pool di indirizzi back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). esempio Hello crea un pool di indirizzi back-end denominato `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

A questo punto, creare bilanciamento del carico hello con [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). esempio Hello crea un bilanciamento del carico denominato `myLoadBalancer` utilizzando hello `myPublicIP` indirizzo:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Creare un probe integrità

tooallow hello bilanciamento toomonitor hello stato di caricamento dell'app, utilizzare un probe di integrità. probe di integrità Hello dinamicamente aggiunge o rimuove le macchine virtuali dalla rotazione di bilanciamento del carico hello in base alle loro controlli toohealth di risposta. Per impostazione predefinita, una macchina virtuale viene rimosso dalla distribuzione del servizio di bilanciamento del carico hello dopo due tentativi consecutivi non riusciti a intervalli di 15 secondi.

Creare un probe integrità con [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). esempio Hello crea un probe di integrità denominato `myHealthProbe` che consente di monitorare ogni macchina virtuale:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Creare le regole del bilanciamento del carico

Una regola di bilanciamento del carico è toodefine utilizzato come il traffico è toohello distribuita le macchine virtuali.

Creare una regola di bilanciamento del carico con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). esempio Hello crea una regola di bilanciamento del carico denominata `myLoadBalancerRule` e consente di bilanciare il traffico sulla porta `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Aggiorna bilanciamento del carico hello con [Set AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Passaggio 4: Configurare la rete

Ogni macchina virtuale ha uno o più virtuale schede di rete (NIC) che si connettono tooa di rete virtuale. Questa rete virtuale è protetta toofilter traffico in base alle regole di accesso definito.

### <a name="create-virtual-network"></a>Creare una rete virtuale

Per prima cosa, configurare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). esempio Hello crea una subnet denominata `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooyour di connettività di rete tooprovide le macchine virtuali, creare una rete virtuale con [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). esempio Hello crea una rete virtuale denominata `myVnet` con `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Configurare la sicurezza di rete

Un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) di Azure consente di controllare il traffico in ingresso e in uscita per una o più macchine virtuali. Le regole di un gruppo di sicurezza di rete consentono o impediscono il traffico di rete su una porta specifica o un intervallo di porte. Queste regole possono includere un prefisso dell'indirizzo di origine, in modo che solo il traffico proveniente da un'origine specificata possa comunicare con una macchina virtuale.

tooallow web tooreach traffico l'app, creare una regola gruppo di sicurezza di rete con [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). esempio Hello crea una regola di gruppo di sicurezza di rete denominata `myNetworkSecurityGroupRule`:

```powershell
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
```

Creare un gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). esempio Hello crea un gruppo denominato `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Aggiungi subnet hello rete sicurezza gruppo toohello con [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Rete virtuale hello di Update con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Creare le schede di interfaccia di rete virtuali

Caricare una funzione di bilanciamento del carico con risorse di interfaccia di rete virtuale hello anziché hello VM effettivo. Hello NIC virtuale è connessa toohello bilanciamento del carico e quindi collegato tooa macchina virtuale.

Creare una scheda di interfaccia di rete virtuale con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello esempio crea tre schede di rete virtuale. (Una scheda di rete virtuale per ogni macchina virtuale creato per l'app in hello seguendo i passaggi):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>Passaggio 5 - Creare le macchine virtuali

Con hello tutti i componenti sul posto sottostante, è ora possibile creare toorun macchine virtuali a disponibilità elevata dell'app. 

Ottenere hello username e password necessari per l'account di amministratore hello nella macchina virtuale hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Creare le macchine virtuali hello con [New AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface aggiungere](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), e [nuova AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hello seguente esempio crea tre macchine virtuali:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Accetta diversi minuti toocreate e configurare tutte le tre macchine virtuali. Hello probe di integrità di bilanciamento del carico rileva automaticamente quando l'applicazione hello è in esecuzione in ogni macchina virtuale. Dopo l'applicazione hello è in esecuzione, regola di bilanciamento del carico hello avvia toodistribute traffico.

### <a name="install-hello-app"></a>Installare l'applicazione hello 

Le estensioni di macchina virtuale di Azure sono attività di configurazione macchina virtuale tooautomate utilizzato, ad esempio l'installazione di applicazioni e la configurazione del sistema operativo hello. Hello [estensione script personalizzato per Windows](./../virtual-machines-windows-extensions-customscript.md) è toorun usato qualsiasi script di PowerShell nella macchina virtuale hello. script Hello può essere archiviato in archiviazione di Azure, qualsiasi endpoint HTTP accessibile, o incorporato in configurazione dell'estensione script personalizzata hello. Quando si utilizza l'estensione script personalizzata hello, l'agente VM di Azure hello gestisce l'esecuzione dello script hello.

Utilizzare [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello un'estensione personalizzata. Hello estensione esecuzioni `powershell Add-WindowsFeature Web-Server` server Web IIS di hello tooinstall:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Test dell'app

Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). esempio Hello Ottiene hello di indirizzo IP per `myPublicIP` creato in precedenza:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Immettere l'indirizzo IP pubblico hello nel browser web tooa. Con hello NSG regola, viene visualizzato il sito Web IIS predefinito hello. 

![Sito IIS predefinito](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Passaggio 6 - Attività di gestione

È possibile la manutenzione tooperform hello macchine virtuali in esecuzione l'app, ad esempio l'installazione di aggiornamenti del sistema operativo. toodeal con un aumento del traffico tooyour app, potrebbe essere necessario tooadd altre macchine virtuali. In questa sezione illustra come tooremove o aggiungere una macchina virtuale dal servizio di bilanciamento del carico hello. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Rimuovere una macchina virtuale dal servizio di bilanciamento del carico hello

Rimuovere una macchina virtuale dal pool di indirizzi back-end hello reimpostando proprietà LoadBalancerBackendAddressPools hello hello scheda di rete.

Ottenere l'interfaccia di rete di hello con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Impostare la proprietà di LoadBalancerBackendAddressPools hello della scheda di interfaccia di rete hello troppo null$:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Aggiorna scheda di interfaccia di rete hello:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Aggiungere un bilanciamento del carico VM toohello

Dopo l'esecuzione della manutenzione di macchina virtuale o se è necessario tooexpand capacità, aggiunta hello NIC del pool di indirizzi back-end toohello VM di bilanciamento del carico hello.

Ottieni bilanciamento del carico hello:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Aggiungere pool di indirizzi back-end hello della scheda di interfaccia di rete toohello bilanciamento di carico hello:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Aggiorna scheda di interfaccia di rete hello:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Passaggi successivi

Esempi: [script di esempio di PowerShell per macchine virtuali di Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
