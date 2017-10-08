---
title: una macchina virtuale Windows da un VHD in Azure specializzato aaaCreate | Documenti Microsoft
description: Creare una nuova macchina virtuale Windows collegando un disco specializzato gestito come disco del sistema operativo hello utilizzo nel modello di distribuzione di gestione risorse di hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Creare una macchina virtuale Windows da un disco specializzato

Creare una nuova macchina virtuale collegando un disco specializzato gestito come disco del sistema operativo hello tramite Powershell. Un disco specializzato è una copia del disco rigido virtuale (VHD) da una macchina virtuale esistente che gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale. 

Quando si utilizza un toocreate VHD specializzata di una nuova macchina virtuale, hello nuova macchina virtuale mantiene il nome del computer hello hello macchina virtuale originale. Vengono mantenute anche altre informazioni specifiche del computer e, in alcuni casi, queste informazioni duplicate possono causare problemi. Quando si copia una VM, tenere presente quali tipi di informazioni specifiche del computer vengono usate dalle applicazioni.

Sono disponibili due opzioni:
* [Caricare un VHD](#option-1-upload-a-specialized-vhd)
* [Copiare una VM di Azure esistente](#option-2-copy-an-existing-azure-vm)

Questo argomento viene illustrato come toouse dischi gestiti. Se è presente una distribuzione legacy che richiede l'uso di un account di archiviazione, vedere [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md) (Creare una VM da un disco rigido virtuale specializzato in un account di archiviazione)

## <a name="before-you-begin"></a>Prima di iniziare
Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Opzione 1: Caricare un disco rigido virtuale specializzato

È possibile caricare hello che disco rigido virtuale da una VM specializzata creato con uno strumento di virtualizzazione locale, come Hyper-V, o una macchina virtuale esportata da un altro cloud.

### <a name="prepare-hello-vm"></a>Preparare hello VM
Se si intende toouse hello file VHD come-è toocreate una nuova macchina virtuale, verificare hello operazioni viene completata. 
  
  * [Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Non** generalizzare hello macchina virtuale con Sysprep.
  * Rimuovere eventuali strumenti di virtualizzazione guest e gli agenti installati in hello VM (ad esempio strumenti di VMware).
  * Assicurarsi di hello macchina virtuale è configurata toopull il relativo indirizzo IP e le impostazioni DNS attraverso DHCP. Ciò garantisce che il server hello ottenga un indirizzo IP all'interno di hello rete virtuale al momento dell'avvio. 


### <a name="get-hello-storage-account"></a>Ottenere l'account di archiviazione hello
È necessario uno spazio di archiviazione account in Azure toostore hello caricato disco rigido virtuale. È possibile usare un account di archiviazione esistente o crearne uno nuovo. 

account di archiviazione disponibili hello tooshow, digitare:

```powershell
Get-AzureRmStorageAccount
```

Se si desidera toouse un account di archiviazione esistente, procedere toohello [hello caricamento VHD](#upload-the-vhd-to-your-storage-account) sezione.

Se è necessario un account di archiviazione toocreate, seguire questi passaggi:

1. È necessario il nome di hello hello del gruppo di risorse in cui deve essere creato l'account di archiviazione hello. toofind out tutti i gruppi di risorse hello nella sottoscrizione di tipo sono:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    un gruppo di risorse denominato toocreate *myResourceGroup* in hello *Stati Uniti occidentali* area, digitare:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Creare un account di archiviazione denominato *mystorageaccount* in questo gruppo di risorse utilizzando hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Caricare l'account di archiviazione tooyour hello disco rigido virtuale 
Hello utilizzare [Aggiungi AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) contenitore cmdlet tooupload hello VHD tooa nell'account di archiviazione. In questo esempio caricamenti hello file *myVHD.vhd* da `"C:\Users\Public\Documents\Virtual hard disks\"` tooa account di archiviazione denominato *mystorageaccount* in hello *myResourceGroup* gruppo di risorse. file Hello viene archiviato nel contenitore hello denominato *mycontainer* e sarà il nuovo nome di file hello *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Se ha esito positivo, si otterrà una risposta simile toothis simile:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

La connessione di rete e delle dimensioni di hello del file di disco rigido virtuale, questo comando potrebbe richiedere qualche minuto toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Creare un disco gestito da hello disco rigido virtuale

Creare un disco gestito da hello specializzato di disco rigido virtuale in cui l'account di archiviazione utilizzando [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Questo esempio viene utilizzato **myOSDisk1** per il nome del disco hello, inserisce hello disco *StandardLRS* archiviazione e utilizza *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* come hello URI per l'origine hello disco rigido virtuale.

Creare un nuovo gruppo di risorse per hello nuova macchina virtuale.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Creare nuovo disco del sistema operativo hello da hello caricato disco rigido virtuale. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Opzione 2: Copiare una VM di Azure esistente

È possibile creare una copia di una macchina virtuale che utilizza dischi gestiti da creare uno snapshot di hello VM, quindi utilizza tale toocreate snapshot un nuovo gestito disco e una nuova macchina virtuale.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Creare uno snapshot del disco del sistema operativo hello

È possibile acquisire uno snapshot di un'intera VM (tutti i dischi inclusi) o solo di un singolo disco. Hello passaggi seguenti viene illustrato come tootake uno snapshot di appena hello del sistema operativo disco di macchina virtuale utilizzando hello [New AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet. 

Impostare alcuni parametri. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Ottenere l'oggetto macchina virtuale hello.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Ottenere il nome del disco hello del sistema operativo.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Creare hello snapshot configurazione. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Creare snapshot hello.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Se si prevede di toouse hello snapshot toocreate una macchina virtuale che deve toobe a prestazioni elevate, utilizzare il parametro hello `-AccountType Premium_LRS` con il comando New-AzureRmSnapshot hello. il parametro Hello Crea snapshot hello in modo che viene archiviato come un disco gestito Premium. I dischi gestiti Premium sono più costosi di quelli Standard. Pertanto è necessario assicurarsi che occorre Premium prima di utilizzare il parametro hello.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Creare un nuovo disco da snapshot hello

Creare un disco gestito da hello snapshot utilizzando [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Questo esempio viene utilizzato *myOSDisk* per il nome del disco hello.

Creare un nuovo gruppo di risorse per hello nuova macchina virtuale.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Impostare il nome del disco hello del sistema operativo. 

```powershell
$osDiskName = 'myOsDisk'
```

Disco gestito hello creato.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Creare hello nuova macchina virtuale 

Creare una rete e altri toobe risorse macchina virtuale utilizzato da hello nuova macchina virtuale.

### <a name="create-hello-subnet-and-vnet"></a>Creare reti virtuali e la subNet hello

Creare reti virtuali hello e la subNet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).

Creare subNet hello. Questo esempio viene creata una subnet denominata **mySubNet**, nel gruppo di risorse hello **myDestinationResourceGroup**, e set hello prefisso di indirizzo di subnet troppo**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Creare una rete virtuale hello. In questo esempio imposta hello toobe nome di rete virtuale **myVnetName**, hello percorso troppo**Stati Uniti occidentali**, e hello prefisso dell'indirizzo per la rete virtuale hello troppo**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Creare gruppi di sicurezza di rete hello e una regola di RDP
toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza che consente l'accesso RDP sulla porta 3389. Poiché hello VHD per hello nuova macchina virtuale è stato creato da una macchina virtuale specializzata esistente, è possibile utilizzare un account dalla macchina virtuale di origine hello per RDP.

In questo esempio imposta hello Nome gruppo troppo**myNsg** e hello RDP troppo nome regola**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Per ulteriori informazioni sugli endpoint e le regole di gruppo, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Creare un indirizzo IP pubblico e NIC
comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.

Creare l'indirizzo IP pubblico hello. In questo esempio, nome dell'indirizzo IP pubblico hello è troppo**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Creare una scheda di rete hello. In questo esempio, il nome di interfaccia di rete hello è impostato troppo**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Nome della macchina virtuale hello e le dimensioni

In questo esempio imposta hello nome della macchina virtuale troppo*myVM* e hello VM dimensioni troppo*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Aggiungere hello NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Aggiungere il disco del sistema operativo hello 

Aggiungere hello del sistema operativo disco toohello configurazione tramite [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk). In questo esempio imposta dimensioni hello del disco hello troppo*128 GB* e collega disco gestito di hello come un *Windows* disco del sistema operativo.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Completare hello VM 

Creare hello VM utilizzando [New AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurazioni che abbiamo appena creato.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Se il comando ha esito positivo, viene visualizzato un output simile al seguente:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Verificare che hello che è stata creata una macchina virtuale
È consigliabile vedere hello appena creato VM in hello [portale di Azure](https://portal.azure.com), in **Sfoglia** > **macchine virtuali**, oppure utilizzando hello seguente PowerShell comandi:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Passaggi successivi
toosign tooyour nuova macchina virtuale, toohello Sfoglia VM in hello [portale](https://portal.azure.com), fare clic su **Connetti**e il file desktop remoto aprire hello. Utilizzare le credenziali dell'account hello del toosign macchina virtuale originale tooyour nuova macchina virtuale. Per ulteriori informazioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md).

