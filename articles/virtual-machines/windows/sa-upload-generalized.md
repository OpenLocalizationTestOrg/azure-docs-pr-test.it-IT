---
title: "aaaUpload un toocreate VHD generalize più macchine virtuali in Azure | Documenti Microsoft"
description: Caricare un generalizzato VHD tooan Azure storage account toocreate toouse una macchina virtuale di Windows con modello di distribuzione di gestione risorse di hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>Caricare un toocreate di tooAzure di disco rigido virtuale generalizzato una nuova macchina virtuale

Questo argomento viene illustrato il caricamento di un account di archiviazione tooa generalizzato disco non gestito e quindi creare una nuova macchina virtuale utilizzando il disco caricato hello. Tutte le informazioni sull'account personale sono state rimosse da un'immagine di disco rigido virtuale generalizzato mediante Sysprep. 

Se si desidera toocreate una macchina virtuale da un disco rigido virtuale specializzato in un account di archiviazione, vedere [creare una macchina virtuale da un disco rigido virtuale specializzato](sa-create-vm-specialized.md).

In questo argomento viene illustrato l'utilizzo di account di archiviazione, è consigliabile che i clienti spostano i dischi gestiti toousing invece. Per una procedura completa di come tooprepare, caricare e creare una nuova macchina virtuale tramite dischi gestiti, vedere [crea una nuova macchina virtuale da un tooAzure generalizzato di disco rigido virtuale caricato utilizzando dischi gestiti](upload-generalized-managed.md).



## <a name="prepare-hello-vm"></a>Preparare hello VM

Tutte le informazioni sull'account personale sono state rimosse da un'immagine del disco rigido virtuale generalizzata tramite Sysprep. Se si prevede di hello toouse toocreate un'immagine disco rigido virtuale nuove macchine virtuali da, è necessario:
  
  * [Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md). 
  * Generalizzare una macchina virtuale hello tramite Sysprep

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Generalizzare una macchina virtuale Windows mediante Sysprep
In questa sezione illustra come toogeneralize la macchina virtuale di Windows per l'utilizzo come immagine. Sysprep consente di rimuovere tutte le informazioni sull'account personale, tra le altre cose e lo prepara hello macchina toobe utilizzato come immagine. Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Assicurarsi che i ruoli del server hello in esecuzione sul computer hello sono supportati da Sysprep. Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Se si esegue Sysprep prima di caricare il disco rigido virtuale tooAzure per hello prima volta, assicurarsi di avere [preparato la macchina virtuale](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep. 
> 
> 

1. Accedi toohello macchina virtuale di Windows.
2. Aprire una finestra del prompt dei comandi hello come amministratore. Modificare anche le directory hello**%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.
3. In hello **System Preparation Tool** nella finestra di dialogo **immettere sistema Out-of-Box guidata**e assicurarsi che tale hello **Generalize** casella di controllo è selezionata.
4. In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.
5. Fare clic su **OK**.
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Al termine di Sysprep, arresta macchina virtuale hello. 

> [!IMPORTANT]
> Non riavviare hello VM finché non si è fatto tooAzure di disco rigido virtuale hello caricamento o la creazione di un'immagine da hello macchina virtuale. Se accidentalmente hello VM Ottiene riavviato, eseguire Sysprep toogeneralize nuovamente.
> 
> 


## <a name="upload-hello-vhd"></a>Caricare hello disco rigido virtuale

Caricare hello VHD tooan account di archiviazione Azure.

### <a name="log-in-tooazure"></a>Accedi tooAzure
Se si dispone già di PowerShell versione 1.4 o versione successiva installato, leggere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

1. Aprire Azure PowerShell e accedere tooyour account Azure. Una finestra popup viene aperto per si tooenter le credenziali dell'account Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Ottenere l'ID sottoscrizione hello per le sottoscrizioni disponibili.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Set hello sottoscrizione corretta utilizzando l'ID di sottoscrizione hello. Sostituire `<subscriptionID>` con ID hello hello correggere sottoscrizione.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>Ottenere l'account di archiviazione hello
È necessario un account di archiviazione nell'immagine di macchina virtuale di Azure toostore hello caricato. È possibile usare un account di archiviazione esistente o crearne uno nuovo. 

account di archiviazione disponibili hello tooshow, digitare:

```powershell
Get-AzureRmStorageAccount
```

Se si desidera toouse un account di archiviazione esistente, procedere toohello [immagine di macchina virtuale di caricamento hello](#upload-the-vm-vhd-to-your-storage-account) sezione.

Se è necessario un account di archiviazione toocreate, seguire questi passaggi:

1. È necessario il nome di hello hello del gruppo di risorse in cui deve essere creato l'account di archiviazione hello. toofind out tutti i gruppi di risorse hello nella sottoscrizione di tipo sono:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    un gruppo di risorse denominato toocreate **myResourceGroup** in hello **Stati Uniti occidentali** area, digitare:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse utilizzando hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>Avviare il caricamento di hello 

Hello utilizzare [Aggiungi AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello tooa il contenitore di immagini nell'account di archiviazione. In questo esempio caricamenti hello file **myVHD.vhd** da `"C:\Users\Public\Documents\Virtual hard disks\"` tooa account di archiviazione denominato **mystorageaccount** in hello **myResourceGroup** gruppo di risorse. sarà inseriti file Hello contenitore hello denominato **mycontainer** e sarà il nuovo nome di file hello **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

La connessione di rete e delle dimensioni di hello del file di disco rigido virtuale, questo comando potrebbe richiedere qualche minuto toocomplete.


## <a name="create-a-new-vm"></a>Creare una nuova VM 

È possibile utilizzare hello caricato VHD toocreate una nuova macchina virtuale. 

### <a name="set-hello-uri-of-hello-vhd"></a>Impostare l'URI del disco rigido virtuale hello hello

Hello URI per hello toouse di disco rigido virtuale è in formato hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**con estensione vhd. In questo esempio hello disco rigido virtuale denominato **myVHD** viene nell'account di archiviazione hello **mystorageaccount** nel contenitore hello **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Crea rete virtuale
Creare reti virtuali hello e la subnet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).

1. Creare subnet hello. Hello esempio seguente viene creata una subnet denominata **mySubnet** nel gruppo di risorse hello **myResourceGroup** con prefisso di indirizzo hello **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Creare la rete virtuale hello. Hello seguente esempio viene creata una rete virtuale denominata **myVnet** in hello **Stati Uniti occidentali** posizione con prefisso di indirizzo hello **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Creare un indirizzo IP pubblico e un'interfaccia di rete
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

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Creare gruppi di sicurezza di rete hello e una regola di RDP
toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza che consente l'accesso RDP sulla porta 3389. 

In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389. Per ulteriori informazioni su NSGs, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Creare una variabile per la rete virtuale hello
Creare una variabile per la rete virtuale hello completata. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Creare VM hello
Hello script PowerShell riportato di seguito viene illustrato come tooset di configurazioni di macchina virtuale hello e utilizzare hello caricato l'immagine di macchina virtuale come origine di hello per una nuova installazione hello.



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>Verificare che hello che è stata creata una macchina virtuale
Al termine, si dovrebbe essere hello macchina virtuale appena creata in hello [portale di Azure](https://portal.azure.com) in **Sfoglia** > **macchine virtuali**, o tramite hello seguenti Comandi di PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Passaggi successivi
vedere la nuova macchina virtuale con Azure PowerShell, toomanage [gestire macchine virtuali tramite Gestione risorse di Azure e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


