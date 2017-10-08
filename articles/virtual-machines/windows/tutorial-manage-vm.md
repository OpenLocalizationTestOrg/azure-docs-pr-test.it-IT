---
title: aaaCreate e gestire macchine virtuali di Windows con hello modulo Azure PowerShell | Documenti Microsoft
description: 'Esercitazione: creare e gestire le macchine virtuali Windows con hello modulo Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Creare e gestire le macchine virtuali Windows con hello modulo Azure PowerShell

Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile. Questa esercitazione illustra gli elementi di base della distribuzione di una macchina virtuale di Azure, ad esempio la selezione delle dimensioni di una VM, la selezione dell'immagine di una VM e la distribuzione di una VM. Si apprenderà come:

> [!div class="checklist"]
> * Creare e connettersi tooa VM
> * Selezionare e usare le immagini di una macchina virtuale
> * Visualizzare e usare macchine virtuali di dimensioni specifiche
> * Ridimensionare una VM
> * Visualizzare e comprendere lo stato di una macchina virtuale

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. 

Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. Il gruppo di risorse deve essere creato prima della macchina virtuale. In questo esempio, un gruppo di risorse denominato *myResourceGroupVM* viene creato in hello *EastUS* area. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

gruppo di risorse Hello viene specificato durante la creazione o modifica di una macchina virtuale, che può essere visualizzata in questa esercitazione.

## <a name="create-virtual-machine"></a>Crea macchina virtuale

Una macchina virtuale deve essere connesso tooa rete virtuale. Comunicare con la macchina virtuale hello tramite un indirizzo IP pubblico a una scheda di interfaccia di rete.

### <a name="create-virtual-network"></a>Creare una rete virtuale

Creare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Creare una rete virtuale con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Creare un indirizzo IP pubblico

Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Creare una scheda di interfaccia di rete

Creare una scheda di interfaccia di rete con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Creare un gruppo di sicurezza di rete

Un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) di Azure consente di controllare il traffico in ingresso e in uscita per una o più macchine virtuali. Le regole di un gruppo di sicurezza di rete consentono o impediscono il traffico di rete su una porta specifica o un intervallo di porte. Queste regole possono includere un prefisso dell'indirizzo di origine, in modo che solo il traffico proveniente da un'origine specificata possa comunicare con una macchina virtuale. server Web a IIS hello tooaccess che si sta installando, è necessario aggiungere una regola di gruppo in ingresso.

utilizzare una regola di gruppo in ingresso, toocreate [Aggiungi AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). esempio Hello crea una regola di gruppo denominata *myNSGRule* che consente di aprire la porta *3389* per la macchina virtuale hello:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

Creare hello NSG utilizzando *myNSGRule* con [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Aggiungi subnet toohello NSG hello nella rete virtuale di hello con [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Rete virtuale hello di Update con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Crea macchina virtuale

Per la creazione di una macchina virtuale sono disponibili diverse opzioni, ad esempio l'immagine del sistema operativo, il ridimensionamento del disco e le credenziali amministrative. In questo esempio viene creata una macchina virtuale con un nome di *myVM* in esecuzione hello più recente di Windows Server 2016 Datacenter.

Impostare username hello e una password per account di amministratore hello nella macchina virtuale hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Creare la configurazione iniziale per la macchina virtuale hello con hello [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Aggiungi configurazione macchina virtuale con hello del sistema operativo informazioni toohello [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Aggiungere hello immagine informazioni toohello configurazione della macchina virtuale con [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Aggiungere hello del sistema operativo disco impostazioni toohello configurazione della macchina virtuale con [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Aggiungi hello scheda di rete creato in precedenza toohello configurazione della macchina virtuale con [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Creare una macchina virtuale hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>Connettersi tooVM

Una volta completata la distribuzione di hello, creare una connessione desktop remoto con la macchina virtuale hello.

Eseguire i seguenti comandi tooreturn hello indirizzo IP pubblico della macchina virtuale hello hello. Prendere nota dell'indirizzo IP per la connessione tooit con la connettività di web browser tootest in un passaggio successivo.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

Comando che segue di hello utilizzare toocreate una sessione desktop remota con la macchina virtuale hello. Sostituire l'indirizzo IP hello con hello *publicIPAddress* della macchina virtuale. Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di macchine virtuali hello.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>Informazioni sulle immagini delle VM

Hello Azure marketplace include molte immagini di macchine virtuali che possono essere utilizzati toocreate una nuova macchina virtuale. Nei passaggi precedenti hello, una macchina virtuale è stata creata utilizzando l'immagine di Windows Server 2016-Datacenter hello. In questo passaggio, il modulo di PowerShell hello è marketplace hello toosearch usato per altre immagini di Windows, che può anche come base per nuove macchine virtuali. Questo processo costituito da ricerca di server di pubblicazione hello, offerta e nome dell'immagine hello (Sku). 

Hello utilizzare [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) comando tooreturn un elenco degli editori di immagine.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Hello utilizzare [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn un elenco di offerte di immagine. Con questo comando, hello ha restituito l'elenco viene filtrato nel server di pubblicazione specificato hello. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) comando quindi filtrerà tooreturn di nome di server di pubblicazione e offerta hello un elenco di nomi di immagini.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Queste informazioni possono essere utilizzati toodeploy una macchina virtuale con un'immagine specifica. In questo esempio imposta il nome di immagine hello sull'oggetto VM hello. Vedere esempi precedenti toohello in questa esercitazione per la procedura di distribuzione completa.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>Informazioni sulle dimensioni delle VM

Una dimensione di macchina virtuale determina la quantità hello delle risorse di calcolo, ad esempio memoria, CPU e GPU che vengono apportate una macchina virtuale disponibile toohello. Macchine virtuali devono toobe creato con una dimensione appropriata per hello prevede che il carico di lavoro. Se aumenta il carico di lavoro, è possibile ridimensionare una macchina virtuale esistente.

### <a name="vm-sizes"></a>Dimensioni delle VM

Hello nella tabella seguente classifica le dimensioni in casi di utilizzo.  

| Tipo                     | Dimensioni           |    Descrizione       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Scopo generico         |DSv2, Dv2, DS, D, Av2, A0-7| Rapporto equilibrato tra CPU e memoria. La soluzione ideale per sviluppo / test e le soluzioni di applicazioni e dati toomedium di piccole dimensioni.  |
| Ottimizzate per il calcolo      | Fs, F             | Rapporto elevato tra CPU e memoria. Soluzione idonea per applicazioni con livelli medi di traffico, dispositivi di rete e processi batch.        |
| Ottimizzate per la memoria       | GS, G, DSv2, DS, Dv2, D   | Rapporto elevato tra memoria e core. Ideale per i database relazionali, cache toolarge medium e analitica in memoria.                 |
| Ottimizzate per l'archiviazione       | Ls                | I/O e velocità effettiva del disco elevati. Ideale per Big Data, database SQL e NoSQL.                                                         |
| GPU           | NV, NC            | VM specializzate ottimizzate per livelli intensivi di rendering della grafica ed editing di video.       |
| Prestazioni elevate | H, A8-11          | Le VM con CPU più potenti, con interfacce di rete ad alta velocità effettiva opzionali (RDMA). 


### <a name="find-available-vm-sizes"></a>Trovare le dimensioni delle macchine virtuali disponibili

toosee un elenco di macchine Virtuali di dimensioni disponibili in una determinata area, usare hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>Ridimensionare una VM

Dopo la distribuzione di una macchina virtuale, può essere ridimensionato tooincrease o ridurre l'allocazione delle risorse.

Prima di ridimensionamento di una macchina virtuale, controllare se hello dimensione desiderata è disponibile in cluster della macchina virtuale corrente hello. Hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando restituisce un elenco di dimensioni. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

Se lo si desidera hello dimensione è disponibile, hello VM può essere ridimensionata da uno stato acceso, ma che è stato riavviato durante l'operazione di hello.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Se hello dimensioni desiderate non è in cluster corrente hello, hello VM esigenze toobe deallocato prima operazione di ridimensionamento hello può verificarsi. Si noti che quando hello VM viene acceso nuovamente, vengono rimossi tutti i dati su disco temporaneo hello e indirizzo IP pubblico hello modificare a meno che non viene utilizzato un indirizzo IP statico. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>Stati di alimentazione di una macchina virtuale

Una macchina virtuale di Azure può avere uno dei diversi stati di alimentazione. Questo stato rappresenta lo stato corrente di hello di hello VM dal punto di vista hello di hello hypervisor. 

### <a name="power-states"></a>Stati di alimentazione

| Stato di alimentazione | Descrizione
|----|----|
| Avvio in corso | Indica la macchina virtuale hello viene avviata. |
| In esecuzione | Indica che la macchina virtuale hello è in esecuzione. |
| Arresto in corso | Indica che la macchina virtuale hello è stata arrestata. | 
| Arrestato | Indica che la macchina virtuale hello è stata arrestata. Si noti che le macchine virtuali in stato arrestato hello continuerà a essere addebitati.  |
| Deallocazione | Indica che la macchina virtuale hello è in corso deallocazione. |
| Deallocato | Indica che la macchina virtuale hello è stata completamente rimossa dall'hypervisor hello ma è ancora disponibile nel piano di controllo hello. Macchine virtuali in stato deallocato hello non essere addebitati. |
| - | Indica che lo stato di alimentazione hello della macchina virtuale hello è sconosciuto. |

### <a name="find-power-state"></a>Trovare lo stato di alimentazione

stato di hello tooretrieve di una determinata macchina virtuale, utilizzare hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando. Essere toospecify che un nome valido per una macchina virtuale e un gruppo di risorse. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Output:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Attività di gestione

Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale. Inoltre, è consigliabile toocreate script tooautomate attività ripetitive o complesse. Utilizzo di PowerShell di Azure, molte attività comuni di gestione può essere eseguita dalla riga di comando hello o negli script.

### <a name="stop-virtual-machine"></a>Arrestare la macchina virtuale

Arrestare e deallocare una macchina virtuale con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Se si desidera una macchina virtuale di hello tookeep in uno stato di provisioning, utilizzare il parametro - StayProvisioned hello.

### <a name="start-virtual-machine"></a>Avviare la macchina virtuale

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Eliminare un gruppo di risorse

Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono illustrate la creazione e la gestione di VM di base, ad esempio:

> [!div class="checklist"]
> * Creare e connettersi tooa VM
> * Selezionare e usare le immagini di una macchina virtuale
> * Visualizzare e usare macchine virtuali di dimensioni specifiche
> * Ridimensionare una VM
> * Visualizzare e comprendere lo stato di una macchina virtuale

Spostare toohello toolearn esercitazione successiva su dischi di macchina virtuale.  

> [!div class="nextstepaction"]
> [Creare e gestire dischi di macchine virtuali](./tutorial-manage-data-disk.md)
