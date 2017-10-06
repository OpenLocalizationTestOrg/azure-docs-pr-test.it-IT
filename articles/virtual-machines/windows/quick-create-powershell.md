---
title: Avvio rapido - aaaAzure creare PowerShell VM di Windows | Documenti Microsoft
description: Apprendere toocreate una macchina virtuale di Windows con PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Creare una macchina virtuale Windows con PowerShell

modulo di Azure PowerShell Hello è toocreate utilizzato e gestire risorse di Azure dalla riga di comando di PowerShell hello o negli script. Questa guida descrive l'utilizzo di PowerShell toocreate e macchina virtuale di Azure che esegue Windows Server 2016. Una volta completata la distribuzione, è connettersi toohello server e installare IIS.  

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

Questa Guida introduttiva richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>Accedi tooAzure

Accedere alla sottoscrizione di Azure con hello tooyour `Login-AzureRmAccount` comando e seguire hello le direzioni.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse di Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Creare risorse di rete

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Creare una rete virtuale, una subnet e un indirizzo IP pubblico. 
Queste risorse sono la macchina virtuale utilizzati tooprovide rete connettività toohello e connetterla toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Creare un gruppo di sicurezza di rete e una regola del gruppo di sicurezza di rete. 
gruppo di sicurezza di rete Hello protegge una macchina virtuale hello utilizzando le regole in entrata e in uscita. In questo caso viene creata una regola in entrata per la porta 3389 che consente connessioni desktop remoto in ingresso. È anche necessario toocreate una regola in entrata per la porta 80, che consente il traffico web in ingresso.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Creare una scheda di rete per la macchina virtuale hello. 
Creare una scheda di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) per la macchina virtuale hello. scheda di rete Hello connette hello macchina virtuale tooa subnet, il gruppo di sicurezza di rete e indirizzo IP pubblico.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Crea macchina virtuale

Creare una configurazione di macchina virtuale. Questa configurazione include le impostazioni di hello utilizzate quando si distribuisce una macchina virtuale hello, ad esempio un'immagine, dimensioni e l'autenticazione di configurazione della macchina virtuale. Quando si esegue questo passaggio vengono chieste le credenziali. i valori Hello immesse siano configurati come nome utente hello e una password per la macchina virtuale hello.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Creare una macchina virtuale hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Connettere la macchina toovirtual

Una volta completata la distribuzione di hello, creare una connessione desktop remoto con la macchina virtuale hello.

Hello utilizzare [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) comando tooreturn hello indirizzo IP pubblico della macchina virtuale hello. Prendere nota dell'indirizzo IP per la connessione tooit con la connettività di web browser tootest in un passaggio successivo.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Comando che segue di hello utilizzare toocreate una sessione desktop remota con la macchina virtuale hello. Sostituire l'indirizzo IP hello con hello *publicIPAddress* della macchina virtuale. Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di macchine virtuali hello.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Installare IIS tramite PowerShell

Ora che è stato effettuato in toohello macchina virtuale di Azure, è possibile utilizzare una singola riga di PowerShell tooinstall IIS e abilitare il traffico web tooallow di hello firewall locale regola. Aprire un prompt dei comandi di PowerShell ed eseguire hello comando seguente:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Hello Visualizza la pagina iniziale di IIS

Con IIS installato e la porta 80 è aperta nella VM da hello Internet, è possibile utilizzare un browser web la pagina iniziale tooview scelte hello predefinita IIS. Essere certi hello toouse *publicIpAddress* descritto in precedenza pagina predefinita di toovisit hello. 

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non è più necessario, è possibile utilizzare hello [Remove AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web. toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali di Windows.

> [!div class="nextstepaction"]
> [Esercitazioni per le macchine virtuali di Windows in Azure](./tutorial-manage-vm.md)
