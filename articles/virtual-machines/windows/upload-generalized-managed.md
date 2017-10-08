---
title: una macchina virtuale Azure gestito da un disco rigido virtuale generalizzato locale aaaCreate | Documenti Microsoft
description: Caricare un tooAzure disco rigido virtuale generalizzato e usarlo toocreate nuove macchine virtuali, nel modello di distribuzione di gestione risorse di hello.
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Caricare un disco rigido virtuale generalizzato e usarlo toocreate nuove macchine virtuali in Azure

In questo argomento illustra tooupload PowerShell utilizzando un disco rigido virtuale di un tooAzure macchina virtuale generalizzata, creare un'immagine da VHD hello e creare una nuova macchina virtuale da quell'immagine. È possibile caricare un disco rigido virtuale esportato da uno strumento di virtualizzazione locale o da un altro cloud. Utilizzando [dischi gestiti](managed-disks-overview.md) per hello semplifica la gestione delle macchine Virtuali hello nuova macchina virtuale e fornisce una migliore disponibilità quando hello VM viene inserito in un set di disponibilità. 

Se si desidera toouse uno script di esempio, vedere [tooupload script tooAzure un disco rigido virtuale di esempio e creare una nuova macchina virtuale](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Prima di iniziare

- Prima di caricare qualsiasi tooAzure disco rigido virtuale, è necessario seguire [preparare un tooAzure tooupload Windows VHD o VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Revisione [pianificare la migrazione di hello di dischi tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) prima di avviare la migrazione troppo[dischi gestiti](managed-disks-overview.md).
- Assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello. Eseguire hello seguenti comando tooinstall.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalizzare hello macchina virtuale di Windows tramite Sysprep

Sysprep consente di rimuovere tutte le informazioni sull'account personale, tra le altre cose e lo prepara hello macchina toobe utilizzato come immagine. Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).

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
6. Al termine di Sysprep, arresta macchina virtuale hello. Non riavviare hello macchina virtuale.



## <a name="log-in-tooazure"></a>Accedi tooAzure
Se si dispone già di PowerShell versione 1.4 o versione successiva installato, leggere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

1. Aprire Azure PowerShell e accedere tooyour account Azure. Una finestra popup viene aperto per si tooenter le credenziali dell'account Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Ottenere l'ID sottoscrizione hello per le sottoscrizioni disponibili.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Set hello sottoscrizione corretta utilizzando l'ID di sottoscrizione hello. Sostituire  *<subscriptionID>*  con ID hello hello correggere sottoscrizione.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Ottenere l'account di archiviazione hello
È necessario un account di archiviazione nell'immagine di macchina virtuale di Azure toostore hello caricato. È possibile usare un account di archiviazione esistente o crearne uno nuovo. 

Se si utilizzerà hello VHD toocreate un disco gestito per una macchina virtuale, posizione dell'account di archiviazione hello deve essere nello stesso percorso hello in cui si creano hello macchina virtuale.

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

    un gruppo di risorse denominato toocreate **myResourceGroup** in hello **Stati Uniti orientali** area, digitare:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse utilizzando hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    I valori validi -SkuName validi sono:
   
   * **Standard_LRS**: archiviazione con ridondanza locale. 
   * **Standard_ZRS**: archiviazione con ridondanza della zona.
   * **Standard_GRS**: archiviazione con ridondanza geografica. 
   * **Standard_RAGRS**: archiviazione con ridondanza geografica e accesso in lettura. 
   * **Premium_LRS**: archiviazione con ridondanza locale Premium. 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Caricare l'account di archiviazione tooyour hello disco rigido virtuale

Hello utilizzare [Aggiungi AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) contenitore cmdlet tooupload hello VHD tooa nell'account di archiviazione. In questo esempio caricamenti hello file *myVHD.vhd* da *"dischi rigidi C:\Users\Public\Documents\Virtual\"*  tooa account di archiviazione denominato *mystorageaccount*in hello *myResourceGroup* gruppo di risorse. sarà inseriti file Hello contenitore hello denominato *mycontainer* e sarà il nuovo nome di file hello *myUploadedVHD.vhd*.

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

La connessione di rete e delle dimensioni di hello del file di disco rigido virtuale, questo comando potrebbe richiedere qualche minuto toocomplete

Salvare hello **URI di destinazione** percorso toouse in seguito se si prevede un disco gestito toocreate o una nuova macchina virtuale utilizzando hello caricati disco rigido virtuale.

### <a name="other-options-for-uploading-a-vhd"></a>Altre opzioni per il caricamento di un disco rigido virtuale
 
 
È inoltre possibile caricare un account di archiviazione tooyour disco rigido virtuale utilizzando uno dei seguenti hello:

- [AzCopy](http://aka.ms/downloadazcopy)
- [API Copy Blob di Archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Caricamento di BLOB in Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)
- [Materiale di riferimento dell'API REST del servizio di importazione/esportazione dell'archiviazione](https://msdn.microsoft.com/library/dn529096.aspx)
-   È consigliabile usare il servizio di importazione/esportazione se il tempo di caricamento stimato è maggiore di 7 giorni. È possibile utilizzare [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) ora hello tooestimate dall'unità di dimensioni e il trasferimento di dati. 
    Importazione/esportazione può essere utilizzato l'account di archiviazione standard tooa toocopy. Sarà necessario toocopy dall'account di archiviazione toopremium archiviazione standard usando uno strumento come AzCopy.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Creare un'immagine da hello caricata disco rigido virtuale 

Creare un'immagine gestita tramite il disco rigido virtuale del sistema operativo generalizzato. Sostituire i valori hello con informazioni personali.


1.  Innanzitutto, impostare i parametri comuni di hello:

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Creare l'immagine di hello utilizzando il disco rigido virtuale generalizzato di sistema operativo.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Crea rete virtuale
Creare reti virtuali hello e la subnet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).

1. Creare subnet hello. Questo esempio viene creata una subnet denominata *mySubnet* con prefisso di indirizzo hello *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Creare la rete virtuale hello. Questo esempio viene creata una rete virtuale denominata *myVnet* con prefisso di indirizzo hello *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Creare un indirizzo IP pubblico e un'interfaccia di rete

comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.

1. Creare un indirizzo IP pubblico. In questo esempio viene creato un indirizzo IP pubblico denominato *myPip*. 
   
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

In questo esempio viene creato un gruppo di sicurezza di rete denominato *myNsg* contenente una regola denominata *myRdpRule* che consente il traffico RDP sulla porta 3389. Per ulteriori informazioni su NSGs, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

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

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Aggiungere hello nome della macchina virtuale e configurazione della macchina virtuale toohello dimensioni.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Immagine di macchina virtuale hello set come immagine di origine per hello nuova macchina virtuale

Impostare l'immagine di origine hello usando un ID di hello dell'immagine di macchina virtuale hello gestito.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Impostare la configurazione del sistema operativo hello e aggiungere una scheda di rete hello.

Immettere un tipo di archiviazione hello (PremiumLRS o StandardLRS) e dimensioni hello del disco del sistema operativo hello. In questo esempio imposta il tipo di account hello troppo*PremiumLRS*, hello dimensioni disco troppo*128 GB* e memorizzazione nella cache del disco troppo*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Creare VM hello

Creare una nuova macchina virtuale utilizzando la configurazione di hello archiviati in hello hello **$vm** variabile.

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

toosign tooyour nuova macchina virtuale, toohello Sfoglia VM in hello [portale](https://portal.azure.com), fare clic su **Connetti**e il file desktop remoto aprire hello. Utilizzare le credenziali dell'account hello del toosign macchina virtuale originale tooyour nuova macchina virtuale. Per ulteriori informazioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

