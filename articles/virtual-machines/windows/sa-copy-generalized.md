---
title: aaaCreate un'immagine non gestita di una macchina virtuale generalizzata in Azure | Documenti Microsoft
description: "Creare un'immagine di unmanged di un generalizzato toocreate toouse macchina virtuale di Windows più copie di una macchina virtuale in Azure."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Come immagine di toocreate una macchina virtuale di non gestita da una macchina virtuale di Azure

In questo articolo illustra l'uso degli account di archiviazione. È consigliabile usare dischi e immagini anziché un account di archiviazione. Per altre informazioni, vedere [Acquisire un'immagine gestita di una macchina virtuale generalizzata in Azure](capture-image-resource.md).

In questo articolo illustra come toouse Azure PowerShell toocreate un'immagine di una macchina virtuale generalizzata di Azure utilizzando un account di archiviazione. È quindi possibile utilizzare hello immagine toocreate un'altra macchina virtuale. immagine di Hello include disco del sistema operativo hello e i dischi dati hello sono macchina virtuale toohello associata. immagine di Hello non include le risorse di rete virtuale hello, pertanto è necessario tooset tali risorse quando si crea hello nuova macchina virtuale. 

## <a name="prerequisites"></a>Prerequisiti
È necessario toohave Azure PowerShell versione 1.0 o versioni successive. Se non è ancora installato PowerShell, leggere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per i passaggi di installazione.

## <a name="generalize-hello-vm"></a>Generalizzare hello VM 
In questa sezione illustra come toogeneralize la macchina virtuale di Windows per l'utilizzo come immagine. Generalizzazione di una macchina virtuale rimuove tutte le informazioni sull'account personale, tra le altre cose e prepara hello macchina toobe utilizzato come immagine. Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Assicurarsi che i ruoli del server hello in esecuzione sul computer hello sono supportati da Sysprep. Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Se si sta caricando tooAzure il disco rigido virtuale per hello prima volta, assicurarsi di avere [preparato la macchina virtuale](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep. 
> 
> 

È anche possibile generalizzare una VM Linux utilizzando `sudo waagent -deprovision+user` e quindi usare PowerShell toocapture hello macchina virtuale. Per informazioni sull'utilizzo di hello CLI toocapture una macchina virtuale, vedere [come toogeneralize e acquisire una macchina virtuale Linux utilizzando hello Azure CLI ](../linux/capture-image.md).


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

## <a name="log-in-tooazure-powershell"></a>Accedi tooAzure PowerShell
1. Aprire Azure PowerShell e accedere tooyour account Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Una finestra popup viene aperto per si tooenter le credenziali dell'account Azure.
2. Ottenere l'ID sottoscrizione hello per le sottoscrizioni disponibili.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Set hello sottoscrizione corretta utilizzando l'ID di sottoscrizione hello.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Deallocare hello macchina virtuale e impostare hello stato toogeneralized
1. Deallocare risorse VM hello.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Hello *stato* per Ciao VM hello Azure portal cambia da **arrestato** troppo**arrestato (deallocato)**.
2. Impostare lo stato di hello della macchina virtuale hello troppo**generalizzato**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Controllare lo stato di hello di hello macchina virtuale. Hello **OSState/generalizzate** sezione per hello macchina virtuale deve disporre di hello **DisplayStatus** impostare troppo**macchina virtuale generalizzata**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Creare l'immagine di hello

Creare un'immagine di macchina virtuale non gestita nel contenitore di archiviazione di destinazione hello tramite questo comando. Hello immagine è creata in hello stesso account di archiviazione come hello macchina virtuale originale. Hello `-Path` parametro consente di salvare una copia del modello di hello JSON per il computer locale tooyour hello origine macchina virtuale. Hello `-DestinationContainerName` parametro è il nome di hello del contenitore di hello che si desidera toohold le immagini. Se il contenitore di hello non esiste, viene creato automaticamente.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
È possibile ottenere hello URL dell'immagine dal modello di file JSON hello. Passare toohello **risorse** > **storageProfile** > **osDisk** > **immagine**  >  **uri** sezione per il percorso completo di hello dell'immagine. Hello URL dell'immagine di hello è simile: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
È inoltre possibile verificare hello URI nel portale di hello. immagine di Hello è copiato tooa contenitore denominato **sistema** nell'account di archiviazione. 

## <a name="create-a-vm-from-hello-image"></a>Creare una macchina virtuale dall'immagine hello

Ora è possibile creare uno o più macchine virtuali dall'immagine di hello non gestito.

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
Hello PowerShell seguente completa le configurazioni di macchina virtuale hello e utilizza l'immagine non gestito come origine di hello per una nuova installazione hello.

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>Verificare che hello che è stata creata una macchina virtuale
Al termine, si dovrebbe essere hello macchina virtuale appena creata in hello [portale di Azure](https://portal.azure.com) in **Sfoglia** > **macchine virtuali**, o tramite hello seguenti Comandi di PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Passaggi successivi
vedere la nuova macchina virtuale con Azure PowerShell, toomanage [gestire macchine virtuali tramite Gestione risorse di Azure e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


