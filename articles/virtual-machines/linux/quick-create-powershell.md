---
title: Avvio rapido - aaaAzure creare VM PowerShell | Documenti Microsoft
description: Apprendere toocreate una macchine virtuali Linux con PowerShell
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a>Creare una macchina virtuale Linux con PowerShell

modulo di Azure PowerShell Hello è toocreate utilizzato e gestire risorse di Azure dalla riga di comando di PowerShell hello o negli script. Questa guida descrive l'utilizzo di una macchina virtuale in esecuzione il server Ubuntu toodeploy modulo di Azure PowerShell hello. Dopo aver distribuito il server di hello, viene creata una connessione SSH e viene installato un server Web NGINX.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

Questa Guida introduttiva richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

Infine, una chiave SSH pubblica con nome hello *id_rsa.pub* deve toobe archiviati in hello *.ssh* directory del profilo utente Windows. Per informazioni dettagliate sulla creazione delle chiavi SSH per Azure, vedere [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Creare chiavi SSH per Azure).

## <a name="log-in-tooazure"></a>Accedi tooAzure

Accedere alla sottoscrizione di Azure con hello tooyour `Login-AzureRmAccount` comando e seguire hello le direzioni.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse di Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>Creare risorse di rete

Creare una rete virtuale, una subnet e un indirizzo IP pubblico. Queste risorse sono la macchina virtuale utilizzati tooprovide rete connettività toohello e connetterla toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

Creare un gruppo di sicurezza di rete e una regola del gruppo di sicurezza di rete. gruppo di sicurezza di rete Hello protegge una macchina virtuale hello utilizzando le regole in entrata e in uscita. In questo caso viene creata una regola in entrata per la porta 22 che consente le connessioni SSH in ingresso. È anche necessario toocreate una regola in entrata per la porta 80, che consente il traffico web in ingresso.

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

Creare una scheda di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) per la macchina virtuale hello. scheda di rete Hello connette hello macchina virtuale tooa subnet, il gruppo di sicurezza di rete e indirizzo IP pubblico.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Crea macchina virtuale

Creare una configurazione di macchina virtuale. Questa configurazione include le impostazioni di hello utilizzate quando si distribuisce una macchina virtuale hello, ad esempio un'immagine, dimensioni e l'autenticazione di configurazione della macchina virtuale.

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

Creare una macchina virtuale hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Connettere la macchina toovirtual

Una volta completata la distribuzione di hello, creare una connessione SSH con la macchina virtuale hello.

Hello utilizzare [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) comando tooreturn hello indirizzo IP pubblico della macchina virtuale hello.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Da un sistema con SSH installato, macchina virtuale di tooconnect toohello comando che segue di hello utilizzato. Se l'utilizzo in Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) può essere utilizzato toocreate hello connessione. 

```bash 
ssh <Public IP Address>
```

Quando richiesto, nome utente di accesso hello è *azureuser*. Se durante la creazione di chiavi SSH è stata immessa una passphrase, è necessario anche questo tooenter.


## <a name="install-nginx"></a>Installare NGINX

Seguente hello utilizzare origini dei pacchetti tooupdate script bash e installare il pacchetto NGINX più recente di hello. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>Pagina iniziale di visualizzazione hello NGIX

Con NGINX installato e la porta 80 è aperta nella VM da hello Internet, è possibile utilizzare un browser web la scelta tooview hello NGINX pagina iniziale predefinita. Impossibile verificare toouse hello indirizzo IP pubblico che descritto in precedenza pagina predefinita di toovisit hello. 

![Sito NGINX predefinito](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non è più necessario, è possibile utilizzare hello [Remove AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web. toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali Linux.

> [!div class="nextstepaction"]
> [Esercitazioni per le macchine virtuali di Linux in Azure](./tutorial-manage-vm.md)
