---
title: aaaAzure reti virtuali e macchine virtuali di Windows | Documenti Microsoft
description: 'Esercitazione: gestire reti virtuali di Azure e macchine virtuali Windows con Azure PowerShell'
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
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Gestire reti virtuali di Azure e macchine virtuali Windows con Azure PowerShell

Le macchine virtuali di Azure usano la rete di Azure per la comunicazione di rete interna ed esterna. In questa esercitazione vengono create più macchine virtuali (VM) in una rete virtuale e viene configurata la connettività di rete tra di esse. Si apprenderà come:

> [!div class="checklist"]
> * Crea rete virtuale
> * Creare subnet di reti virtuali
> * Controllare il traffico di rete con gruppi di sicurezza di rete
> * Visualizzare le regole del traffico applicate

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>Creare la rete virtuale

Una rete virtuale è una rappresentazione della rete nel cloud hello. Una rete virtuale è un isolamento logico di hello sottoscrizione tooyour cloud di Azure dedicato. All'interno di una rete virtuale, si trova subnet, le regole per la connettività toothose subnet e connessioni da subnet toohello di hello macchine virtuali.

Prima di poter creare altre risorse di Azure, è necessario toocreate un gruppo di risorse con [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). esempio Hello crea un gruppo di risorse denominato *myRGNetwork* in hello *EastUS* percorso:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Una subnet è una risorsa figlio di una rete virtuale e consente di definire i segmenti degli spazi di indirizzi all'interno di un blocco CIDR, usando i prefissi degli indirizzi IP. Schede di rete possono essere aggiunte toosubnets e tooVMs connesso, fornisce la connettività per diversi carichi di lavoro.

Creare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Creare una rete virtuale denominata *myVNet* che usa *myFrontendSubnet* con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Creare la VM front-end

Per una macchina virtuale toocommunicate in una rete virtuale, è necessaria un'interfaccia di rete virtuale (NIC). Hello *myFrontendVM* è accessibile da hello internet, pertanto è necessario disporre anche di un indirizzo IP pubblico. 

Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Creare un'interfaccia di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Impostare username hello e una password per account di amministratore hello su hello VM con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Creare le macchine virtuali hello con [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface aggiungere](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), e [nuova AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>Installare il server Web

È possibile installare IIS in *myFrontendVM* usando una sessione Desktop remoto. È necessario tooget hello indirizzo IP pubblico del hello tooaccess VM è.

È possibile ottenere l'indirizzo IP pubblico hello del *myFrontendVM* con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). esempio Hello Ottiene hello di indirizzo IP per *myPublicIPAddress* creato in precedenza:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Prendere nota di questo indirizzo IP per poterlo usare nei passaggi successivi.

Comando che segue di hello utilizzare toocreate una sessione desktop remota con *myFrontendVM*. Sostituire  *<publicIPAddress>*  con indirizzo hello annotato in precedenza. Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di hello macchina virtuale.

```
mstsc /v:<publicIpAddress>
``` 

Ora che sono registrati nel troppo*myFrontendVM*, è possibile utilizzare una singola riga di PowerShell tooinstall IIS e abilitare il traffico web tooallow di hello firewall locale regola. Aprire un prompt dei comandi di PowerShell ed eseguire hello comando seguente:

Utilizzare [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello un'estensione personalizzata per l'installazione di server Web IIS hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Ora è possibile utilizzare hello pubblica IP indirizzo toobrowse toohello VM toosee hello sito IIS.

![Sito IIS predefinito](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Gestire il traffico interno

Un rete gruppo di sicurezza () contiene un elenco di regole di sicurezza che consentono o negano tooa tooresources connessi di rete del traffico tra reti virtuali. NSGs può essere associato toosubnets o singole schede di rete associata tooVMs. Viene eseguita l'apertura o chiusura di accesso tooVMs tramite porte utilizzando regole di gruppo. Alla creazione di *myFrontendVM*, la porta in ingresso 3389 è stata aperta automaticamente per la connettività RDP.

La comunicazione interna delle VM può essere configurata usando un gruppo di sicurezza di rete. In questa sezione viene illustrato come una subnet aggiuntiva in hello toocreate di rete e assegnare un tooallow tooit NSG una connessione da *myFrontendVM* troppo*myBackendVM* sulla porta 1433. subnet Hello viene quindi assegnato toohello VM al momento della creazione.

È possibile limitare il traffico interno troppo*myBackendVM* solo da *myFrontendVM* mediante la creazione di un gruppo per la subnet di back-end hello. esempio Hello crea una regola di gruppo denominata *myBackendNSGRule* con [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

Aggiungere un gruppo di sicurezza di rete denominato *myBackendNSG* con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Aggiungere la subnet back-end

Aggiungi *myBackEndSubnet* troppo*myVNet* con [Aggiungi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>Creare la VM back-end

hello toocreate modo più semplice di Hello VM back-end è tramite un'immagine di SQL Server. Solo in questa esercitazione crea hello VM al server di database hello, ma non fornisce informazioni sull'accesso a database hello.

Creare *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Impostare username hello e una password per account di amministratore hello nella macchina virtuale con Get-Credential hello:

```powershell
$cred = Get-Credential
```

Creare *myBackendVM*:

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

immagine di Hello utilizzata è installato SQL Server, ma non viene utilizzato in questa esercitazione. È incluso tooshow è illustrato come configurare il traffico web toohandle una macchina virtuale e la gestione di database toohandle una macchina virtuale.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è creato e protetto reti di Azure come macchine toovirtual correlati. 

> [!div class="checklist"]
> * Crea rete virtuale
> * Creare subnet di reti virtuali
> * Controllare il traffico di rete con gruppi di sicurezza di rete
> * Visualizzare le regole del traffico applicate

Spostare toohello toolearn esercitazione successiva sul monitoraggio di protezione dati su macchine virtuali tramite backup di Azure. .

> [!div class="nextstepaction"]
> [Eseguire il backup di macchine virtuali Windows in Azure](./tutorial-backup-vms.md)
