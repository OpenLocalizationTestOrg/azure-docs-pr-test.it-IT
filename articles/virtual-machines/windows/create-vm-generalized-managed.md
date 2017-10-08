---
title: aaaCreate macchina virtuale da un'immagine di macchina virtuale gestita in Azure | Documenti Microsoft
description: Creare una macchina virtuale Windows da un'immagine di macchina virtuale gestita generalizzata usando Azure PowerShell, nel modello di distribuzione di gestione risorse di hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Creare una macchina virtuale da un'immagine gestita

È possibile creare più macchine virtuali da un'immagine di macchina virtuale gestita in Azure. Un'immagine di macchina virtuale gestita contiene hello informazioni necessarie toocreate una macchina virtuale, inclusi i dischi del sistema operativo e dati hello. Hello dischi rigidi virtuali che costituiscono l'immagine di hello, inclusi i dischi di hello del sistema operativo sia eventuali dischi dati, vengono archiviati come dischi gestiti. 


## <a name="prerequisites"></a>Prerequisiti

È necessario già toohave [creata un'immagine di macchina virtuale gestita](capture-image-resource.md) toouse per la creazione di hello nuova macchina virtuale. 

Assicurarsi di disporre di hello versioni più recenti dei moduli di AzureRM.Compute e AzureRM.Network PowerShell hello. Aprire un prompt dei comandi di PowerShell come amministratore ed eseguire hello successivo comando tooinstall li.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).



## <a name="collect-information-about-hello-image"></a>Raccogliere informazioni sull'immagine di hello

È innanzitutto necessario toogather le informazioni di base sull'immagine di hello e creare una variabile per l'immagine di hello. In questo esempio Usa un'immagine di macchina virtuale gestita denominata **myImage** ovvero hello in **myResourceGroup** gruppo di risorse in hello **occidentale Stati Uniti centro** percorso. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Crea rete virtuale
Creare reti virtuali hello e la subnet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).

1. Creare subnet hello. Questo esempio viene creata una subnet denominata **mySubnet** con prefisso di indirizzo hello **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Creare la rete virtuale hello. Questo esempio viene creata una rete virtuale denominata **myVnet** con prefisso di indirizzo hello **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Creare un indirizzo IP pubblico e un'interfaccia di rete

comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.

1. Creare un indirizzo IP pubblico. In questo esempio viene creato un indirizzo IP pubblico denominato **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Creare una scheda di rete hello. In questo esempio viene creata una scheda NIC denominata **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Creare gruppi di sicurezza di rete hello e una regola di RDP

toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza di rete (gruppo) che consente l'accesso RDP sulla porta 3389. 

In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389. Per ulteriori informazioni su NSGs, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Creare una variabile per la rete virtuale hello

Creare una variabile per la rete virtuale hello completata. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Ottenere le credenziali di hello per hello VM

Hello cmdlet riportato di seguito verrà aperta una finestra in cui è necessario specificare un nuovo toouse di nome e una password utente come account amministratore locale hello per accedere in remoto alle macchine Virtuali hello. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Variabili impostate per hello VM name, nome di computer e hello dimensioni di hello VM

1. Creare variabili per il nome di macchina virtuale hello e nome del computer. In questo esempio imposta come nome della macchina virtuale hello **myVM** e nome del computer hello come **myComputer**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Impostare dimensioni hello della macchina virtuale hello. Questo esempio crea una macchina virtuale con dimensione **Standard_DS1_v2**. Vedere hello [dimensioni delle macchine Virtuali](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentazione per ulteriori informazioni.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Aggiungere hello nome della macchina virtuale e configurazione della macchina virtuale toohello dimensioni.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Immagine di macchina virtuale hello set come immagine di origine per hello nuova macchina virtuale

Impostare l'immagine di origine hello usando un ID di hello dell'immagine di macchina virtuale hello gestito.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Impostare la configurazione del sistema operativo hello e aggiungere una scheda di rete hello.

Immettere un tipo di archiviazione hello (PremiumLRS o StandardLRS) e dimensioni hello del disco del sistema operativo hello. In questo esempio imposta il tipo di account hello troppo**PremiumLRS**, hello dimensioni disco troppo**128 GB** e memorizzazione nella cache del disco troppo**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Creare VM hello

Crea nuova macchina virtuale utilizzando la configurazione di hello che abbiamo creato e archiviato in hello hello **$vm** variabile.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Verificare che hello che è stata creata una macchina virtuale
Al termine, si dovrebbe essere hello macchina virtuale appena creata in hello [portale di Azure](https://portal.azure.com) in **Sfoglia** > **macchine virtuali**, o tramite hello seguenti Comandi di PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Passaggi successivi
vedere la nuova macchina virtuale con Azure PowerShell, toomanage [creare e gestire macchine virtuali di Windows con il modulo di Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

