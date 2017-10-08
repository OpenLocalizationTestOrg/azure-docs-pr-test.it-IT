---
title: una macchina virtuale Windows in Azure aaaCustomize | Documenti Microsoft
description: Informazioni su come toouse hello estensione script personalizzata e l'insieme di credenziali chiave toocustomize macchine virtuali di Windows in Azure
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
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a>Come toocustomize una macchina virtuale Windows Azure
in genere desiderata tooconfigure virtuali (VM) in modo rapido e coerenza, qualche forma di automazione. Un comune toocustomize approccio una macchina virtuale di Windows è toouse [Custom Script di estensione per Windows](extensions-customscript.md). In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Utilizzare tooinstall estensione Script personalizzata hello IIS
> * Creare una macchina virtuale che utilizza l'estensione dello Script personalizzata hello
> * Consente di visualizzare un sito IIS in esecuzione dopo l'applicazione di estensione hello

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="custom-script-extension-overview"></a>Panoramica dell'estensione script personalizzata
Estensione dello Script personalizzata Hello Scarica ed esegue gli script nelle macchine virtuali di Azure. Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione. Gli script possono essere scaricati da GitHub o di archiviazione di Azure o forniti toohello portale di Azure in fase di esecuzione di estensione.

estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.

È possibile utilizzare l'estensione dello Script personalizzata hello con le macchine virtuali Linux e Windows.


## <a name="create-virtual-machine"></a>Crea macchina virtuale
Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). esempio Hello crea un gruppo di risorse denominato *myResourceGroupAutomate* in hello *EastUS* percorso:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

Impostare un amministratore di nome utente e password per le macchine virtuali hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Ora è possibile creare hello macchina virtuale con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Crea componenti di rete virtuale hello necessario, la configurazione del sistema operativo hello, Hello seguente e quindi crea una macchina virtuale denominata *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

Richiede alcuni minuti per le risorse di hello e toobe macchina virtuale creata.


## <a name="automate-iis-install"></a>Automatizzare l'installazione IIS
Utilizzare [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello estensione Script personalizzata. Hello estensione esecuzioni `powershell Add-WindowsFeature Web-Server` tooinstall hello server Web IIS e quindi hello aggiornamenti *Default.htm* pagina tooshow hello hostname di hello VM:

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a>Testare il sito Web
Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa. sito Hello viene visualizzato, inclusi hello nome host della macchina virtuale hello tale bilanciamento del carico hello distribuite tooas traffico nel seguente esempio hello:

![Esecuzione del sito Web IIS](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato automatizzato hello IIS è installato in una macchina virtuale. Si è appreso come:

> [!div class="checklist"]
> * Utilizzare tooinstall estensione Script personalizzata hello IIS
> * Creare una macchina virtuale che utilizza l'estensione dello Script personalizzata hello
> * Consente di visualizzare un sito IIS in esecuzione dopo l'applicazione di estensione hello

Spostare toolearn esercitazione successiva toohello come toocreate immagini di macchina virtuale personalizzate.

> [!div class="nextstepaction"]
> [Creare un'immagine di VM personalizzata](./tutorial-custom-images.md)
