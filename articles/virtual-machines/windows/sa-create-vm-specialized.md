---
title: aaaCreate macchina virtuale da un disco specializzato in Azure | Documenti Microsoft
description: Creare una nuova macchina virtuale collegando un disco specializzato non gestito, nel modello di distribuzione di gestione risorse di hello.
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Creare una VM da un disco rigido virtuale specializzato in un account di archiviazione

Creare una nuova macchina virtuale collegando un disco specializzato non gestito come disco del sistema operativo hello tramite Powershell. Un disco specializzato è una copia del disco rigido virtuale da una macchina virtuale esistente che gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale. 

Sono disponibili due opzioni:
* [Caricare un VHD](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Copiare hello VHD di una macchina virtuale di Azure esistente](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Prima di iniziare
Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello. Eseguire hello seguenti comando tooinstall.

```powershell
Install-Module AzureRM.Compute 
```
Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Opzione 1: Caricare un disco rigido virtuale specializzato

È possibile caricare hello che disco rigido virtuale da una VM specializzata creato con uno strumento di virtualizzazione locale, come Hyper-V, o una macchina virtuale esportata da un altro cloud.

### <a name="prepare-hello-vm"></a>Preparare hello VM
È possibile caricare un disco rigido virtuale specializzato creato usando una VM locale o un disco rigido virtuale esportato da un altro cloud. Un disco rigido virtuale specializzato gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale. Se si intende toouse hello file VHD come-è toocreate una nuova macchina virtuale, verificare hello operazioni viene completata. 
  
  * [Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Non** generalizzare hello macchina virtuale con Sysprep.
  * Rimuovere eventuali strumenti di virtualizzazione guest e gli agenti installati in hello VM (ad esempio strumenti di VMware).
  * Assicurarsi di hello macchina virtuale è configurata toopull il relativo indirizzo IP e le impostazioni DNS attraverso DHCP. Ciò garantisce che il server hello ottenga un indirizzo IP all'interno di hello rete virtuale al momento dell'avvio. 


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
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Caricare l'account di archiviazione tooyour hello disco rigido virtuale
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


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Opzione 2: Copiare hello disco rigido virtuale da una macchina virtuale di Azure esistente

È possibile copiare un account toouse di disco rigido virtuale tooanother archiviazione durante la creazione di una macchina virtuale nuova, duplicata.

### <a name="before-you-begin"></a>Prima di iniziare
Verificare quanto segue:

* Informazioni hello **gli account di archiviazione di origine e destinazione**. Per la macchina virtuale di origine hello, è necessario toohave hello archiviazione nomi account e contenitore. In genere, si sarà il nome di contenitore hello **dischi rigidi virtuali**. È inoltre necessario toohave un account di archiviazione di destinazione. Se non hai già uno, è possibile crearne uno usando portale hello (**più servizi** > gli account di archiviazione > Aggiungi) o tramite hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet. 
* Aver scaricato e installato hello [strumento AzCopy](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>Deallocare hello VM
Dealloca hello VM, che consente di liberare hello toobe di disco rigido virtuale copiato. 

* **Portale**: fare clic su  **Macchine virtuali** > **myVM** &gt; Stop (Termina)
* **PowerShell**: utilizzare [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocazione) hello macchina virtuale denominata **myVM** nel gruppo di risorse **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Hello **stato** per Ciao VM hello Azure portal cambia da **arrestato** troppo**arrestato (deallocato)**.

### <a name="get-hello-storage-account-urls"></a>Ottenere l'URL di account di archiviazione hello
È necessario hello gli URL di account di archiviazione di origine e destinazione hello. Hello URL simile a: `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Se si conosce già nome account e il contenitore di archiviazione hello, è possibile solo sostituire informazioni hello tra hello tra parentesi quadre toocreate l'URL. 

È possibile utilizzare hello portale di Azure o Azure Powershell tooget hello URL:

* **Portale**: fare clic su hello  **>**  per **più servizi** > **gli account di archiviazione**  >   *account di archiviazione* > **BLOB** e il file VHD di origine è probabilmente in hello **dischi rigidi virtuali** contenitore. Fare clic su **proprietà** per il contenitore di hello e copiare il testo hello etichetta **URL**. È necessario che gli URL di hello di contenitori di origine e di destinazione sia hello. 
* **PowerShell**: utilizzare [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) informazioni hello tooget per macchina virtuale denominata **myVM** nel gruppo di risorse hello **myResourceGroup**. Nei risultati di hello, Cerca in hello **profilo di archiviazione** sezione per hello **Vhd Uri**. prima parte di Hello di hello Uri hello URL toohello ed ultima parte hello hello Nome disco rigido virtuale del sistema operativo per hello macchina virtuale.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Ottiene le chiavi di accesso di hello archiviazione
Trova le chiavi di accesso hello per hello gli account di archiviazione di origine e di destinazione. Per altre informazioni sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../../storage/common/storage-create-storage-account.md).

* **Portale**: fare clic su **Altri servizi** > **Account di archiviazione** > *account di archiviazione* > **Chiavi di accesso**. Tasto di copia hello etichettata come **key1**.
* **PowerShell**: utilizzare [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello archiviazione chiave hello account di archiviazione **mystorageaccount** nel gruppo di risorse hello  **myResourceGroup**. Chiave di hello copia con l'etichetta **key1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Copiare hello disco rigido virtuale
È possibile copiare file da un account di archiviazione a un altro usando AzCopy. Per il contenitore di destinazione hello, se il contenitore di hello specificato non esiste, si verrà creato automaticamente. 

toouse AzCopy, aprire un prompt dei comandi nel computer locale e passare toohello cartella in cui è installato AzCopy. Sarà simile troppo*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*. 

toocopy tutti hello file all'interno di un contenitore, utilizzare hello **/S** passare. Può essere utilizzato toocopy hello disco rigido virtuale del sistema operativo e tutti i dischi di dati hello se sono presenti in hello stesso contenitore. Questo esempio viene illustrato come toocopy hello tutti i file nel contenitore hello **mysourcecontainer** nell'account di archiviazione **mysourcestorageaccount** toohello contenitore **mydestinationcontainer**  in hello **mydestinationstorageaccount** account di archiviazione. Sostituire i nomi di hello di account di archiviazione hello e di contenitori con valori personalizzati. Sostituire `<sourceStorageAccountKey1>` e `<destinationStorageAccountKey1>` con chiavi a propria scelta.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Se si vuole solo toocopy uno specifico VHD in un contenitore con più file, è possibile specificare anche il nome di file hello opzione /Pattern hello. In questo esempio, solo hello file denominato **myFileName.vhd** verranno copiati.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


Al termine verrà visualizzato un messaggio simile al seguente:

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Risoluzione dei problemi
* Quando si utilizza AZCopy, se viene visualizzato l'errore hello "Richiesta hello tooauthenticate Server non riuscita", verificare che il valore di hello dell'intestazione di autorizzazione hello è del formato corretto, inclusa la firma hello. Se si utilizza 2 di chiave o una chiave di archiviazione secondaria hello, provare a usare la chiave di archiviazione primario o al 1 ° hello.

## <a name="create-hello-new-vm"></a>Creare hello nuova macchina virtuale 

È necessario toocreate rete e altri toobe risorse macchina virtuale utilizzato da hello nuova macchina virtuale.

### <a name="create-hello-subnet-and-vnet"></a>Creare reti virtuali e la subNet hello

Creare reti virtuali hello e la subNet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).

1. Creare subNet hello. Questo esempio viene creata una subnet denominata **mySubNet**, nel gruppo di risorse hello **myResourceGroup**, e set hello prefisso di indirizzo di subnet troppo**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Creare una rete virtuale hello. In questo esempio imposta hello toobe nome di rete virtuale **myVnetName**, hello percorso troppo**Stati Uniti occidentali**, e hello prefisso dell'indirizzo per la rete virtuale hello troppo**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Creare un indirizzo IP pubblico e NIC
comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.

1. Creare l'indirizzo IP pubblico hello. In questo esempio, nome dell'indirizzo IP pubblico hello è troppo**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Creare una scheda di rete hello. In questo esempio, il nome di interfaccia di rete hello è impostato troppo**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Creare gruppi di sicurezza di rete hello e una regola di RDP
toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza che consente l'accesso RDP sulla porta 3389. Poiché hello disco rigido virtuale per la nuova macchina virtuale è stato creato da un oggetto esistente hello specializzato macchina virtuale, dopo aver creato hello VM, è possibile utilizzare un account esistente dalla macchina virtuale di origine hello che aveva toolog autorizzazione sull'utilizzo di RDP.
In questo esempio imposta hello Nome gruppo troppo**myNsg** e hello RDP troppo nome regola**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Per ulteriori informazioni sugli endpoint e le regole di gruppo, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Nome della macchina virtuale hello e le dimensioni

In questo esempio imposta hello nome della macchina virtuale troppo "myVM" e hello VM dimensione troppo "Standard_A2".
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Aggiungere hello NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Configurare un disco del sistema operativo hello

1. Impostare hello URI per hello disco rigido virtuale che è stato caricato o copiato. In questo esempio, i file di disco rigido virtuale denominato hello **myOsDisk.vhd** vengono mantenuti in un account di archiviazione denominato **myStorageAccount** in un contenitore denominato **myContainer**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Aggiungere il disco del sistema operativo hello. In questo esempio, quando viene creata hello disco del sistema operativo, hello termine "osDisk" è appened toohello nome toocreate hello del sistema operativo disco nome della macchina virtuale. In questo esempio specifica inoltre che il disco rigido virtuale basato su Windows deve essere collegato toohello macchina virtuale come disco di hello del sistema operativo.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

Facoltativo: Se si dispone di dischi dati che toobe necessità collegato toohello VM, aggiungere dischi dati hello utilizzando gli URL dei dischi rigidi virtuali dati hello e hello i numero di unità logica (Lun) appropriati.

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

Quando si utilizza un account di archiviazione, dati hello e gli URL del disco del sistema operativo simile al seguente: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. È possibile trovare nel portale di hello visualizzando contenitore di archiviazione di destinazione toohello, facendo clic su sistema operativo hello o disco rigido virtuale che è stato copiato, dati e quindi copiando il contenuto di hello dell'URL hello.


### <a name="complete-hello-vm"></a>Completare hello VM 

Creare hello VM utilizzando le configurazioni di hello che abbiamo appena creato.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
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
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Passaggi successivi
toosign tooyour nuova macchina virtuale, toohello Sfoglia VM in hello [portale](https://portal.azure.com), fare clic su **Connetti**e il file desktop remoto aprire hello. Utilizzare le credenziali dell'account hello del toosign macchina virtuale originale tooyour nuova macchina virtuale. Per ulteriori informazioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md).

