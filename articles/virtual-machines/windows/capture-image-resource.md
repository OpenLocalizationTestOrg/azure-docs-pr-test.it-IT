---
title: aaaCreate un'immagine gestita in Azure | Documenti Microsoft
description: "Creare un'immagine gestita di un disco rigido virtuale o una macchina virtuale generalizzati in Azure. Le immagini può essere utilizzati toocreate più macchine virtuali che usano dischi gestiti."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Creare un'immagine gestita di una macchina virtuale generalizzata in Azure

È possibile creare una risorsa immagine gestita da una macchina virtuale generalizzata archiviata come disco gestito o come disco non gestito in un account di archiviazione. Hello immagine può quindi essere utilizzato toocreate più macchine virtuali. 


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


## <a name="create-a-managed-image-in-hello-portal"></a>Creare un'immagine gestita nel portale di hello 

1. Aprire hello [portale](https://portal.azure.com).
2. Fare clic su hello toocreate sul segno più di una nuova risorsa.
3. Nella ricerca di filtro hello, digitare **immagine**.
4. Selezionare **immagine** dai risultati di hello.
5. In hello **immagine** pannello, fare clic su **crea**.
6. In **nome**, digitare un nome per l'immagine di hello.
7. Se si dispone di più di una sottoscrizione, selezionare hello corretta in da hello **sottoscrizione** elenco a discesa.
7. In **gruppo di risorse** selezionare **Crea nuovo** e digitare un nome o selezionare **da esistente** e selezionare un toouse gruppo di risorse dall'elenco a discesa hello.
8. In **percorso**, scegliere il percorso di hello del gruppo di risorse.
9. In **tipo di sistema operativo** selezionare il tipo di hello del sistema operativo Windows o Linux.
11. In **blob di archiviazione**, fare clic su **Sfoglia** toolook per hello VHD nell'archiviazione Azure.
12. In **Tipo di account** scegliere Standard_LRS o Premium_LRS. Il tipo Standard usa unità disco rigido, mente l'account Premium usa unità SSD. Entrambi usano l'archiviazione con ridondanza locale.
13. In **la cache del disco** selezionare hello disco appropriato, opzione di memorizzazione nella cache. opzioni di Hello sono **Nessuno**, **Read-only** e **lettura/scrittura**.
14. Facoltativo: È possibile anche aggiungere un'immagine di toohello disco dati esistente, fare clic su **+ Aggiungi disco di dati**.  
15. Dopo aver completato le selezioni, fare clic su **Crea**.
16. Dopo aver creato l'immagine di hello, verrà visualizzato come un **immagine** risorsa nell'elenco di hello delle risorse nel gruppo di risorse hello scelto.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Creare un'immagine gestita di una macchina virtuale tramite PowerShell

Creazione di un'immagine direttamente da hello che VM assicura che l'immagine hello include tutti i dischi di hello associati hello macchina virtuale, compresi hello disco del sistema operativo e qualsiasi disco dati.


Prima di iniziare, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello. Eseguire hello seguenti comando tooinstall.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).


1. Creare alcune variabili.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. Verificare che hello che VM è stato deallocato.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Impostare lo stato di hello della macchina virtuale hello troppo**generalizzato**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Ottenere una macchina virtuale hello. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Creare una configurazione immagine hello.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Creare l'immagine di hello.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Creare un'immagine gestita di un disco rigido virtuale tramite PowerShell

Creare un'immagine gestita tramite il disco rigido virtuale del sistema operativo generalizzato.


1.  Innanzitutto, impostare i parametri comuni di hello:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Hello Step\deallocate macchina virtuale.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Contrassegnare hello VM come generalizzato.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Creare l'immagine di hello utilizzando il disco rigido virtuale generalizzato di sistema operativo.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Creare un'immagine gestita da uno snapshot tramite PowerShell

È anche possibile creare un'immagine gestita da uno snapshot del disco rigido virtuale da una macchina virtuale generalizzata hello.

    
1. Creare alcune variabili. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Ottenere snapshot di hello.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Creare una configurazione immagine hello.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Creare l'immagine di hello.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Passaggi successivi
- È ora possibile [creare una macchina virtuale dall'immagine gestito hello generalizzato](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

