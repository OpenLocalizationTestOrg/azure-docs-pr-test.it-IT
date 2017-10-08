---
title: immagini di macchina virtuale con Azure PowerShell hello personalizzate aaaCreate | Documenti Microsoft
description: 'Esercitazione: creare un''immagine di macchina virtuale personalizzata utilizzando hello Azure PowerShell.'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Creare un'immagine personalizzata di una VM di Azure con PowerShell

Le immagini personalizzate sono come le immagini di marketplace, ma si possono creare autonomamente. Immagini personalizzate possono essere utilizzati toobootstrap configurazioni, ad esempio il precaricamento di applicazioni, configurazioni dell'applicazione e altre configurazioni del sistema operativo. In questa esercitazione viene creata un'immagine personalizzata di una macchina virtuale di Azure. Si apprenderà come:

> [!div class="checklist"]
> * Eseguire Sysprep e generalizzare le macchine virtuali
> * Creare un'immagine personalizzata
> * Creare una VM da un'immagine personalizzata
> * Elenco di tutte le immagini di hello nella sottoscrizione
> * Eliminare un'immagine

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Prima di iniziare

passaggi di Hello riportati di seguito in dettaglio come tootake una macchina virtuale esistente e attivare i dati in un oggetto personalizzato riutilizzabile immagine che si possono usare toocreate nuove istanze di macchina virtuale.

esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente. Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente. Quando il lavoro esercitazione hello, sostituire il gruppo di risorse di hello e VM nomi dove necessario.

## <a name="prepare-vm"></a>Preparare la VM

toocreate un'immagine di una macchina virtuale, è necessario tooprepare hello VM da hello generalizzazione macchina virtuale, la deallocazione e quindi contrassegnare origine hello VM come generalizzata in Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalizzare hello macchina virtuale di Windows tramite Sysprep

Sysprep consente di rimuovere tutte le informazioni sull'account personale, tra le altre cose e lo prepara hello macchina toobe utilizzato come immagine. Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).


1. Connessione macchina virtuale toohello.
2. Aprire una finestra del prompt dei comandi hello come amministratore. Modificare anche le directory hello*%windir%\system32\sysprep*, quindi eseguire *sysprep.exe*.
3. In hello **System Preparation Tool** nella finestra di dialogo *immettere sistema Out-of-Box guidata*e assicurarsi che tale hello *Generalize* casella di controllo è selezionata.
4. In **Opzioni di arresto** selezionare *Arresta il sistema* e fare clic su **OK**.
5. Al termine di Sysprep, arresta macchina virtuale hello. **Non si riavvia hello VM**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Rilasciare e contrassegnare hello VM come generalizzato

toocreate un'immagine, hello VM deve toobe deallocato e contrassegnati come generalizzata in Azure.

Hello deallocata VM utilizzando [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Impostare lo stato di hello della macchina virtuale hello troppo`-Generalized` utilizzando [Set AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Creare l'immagine di hello

Ora è possibile creare un'immagine di macchina virtuale hello utilizzando [New AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) e [New AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage). esempio Hello crea un'immagine denominata *myImage* da una macchina virtuale denominata *myVM*.

Ottenere una macchina virtuale hello. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Creare una configurazione immagine hello.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Creare l'immagine di hello.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Creare macchine virtuali da immagini hello

Dopo aver creato un'immagine, è possibile creare nuove macchine virtuali dall'immagine hello. Creazione di una macchina virtuale da un'immagine personalizzata è molto simile toocreating una macchina virtuale usando un'immagine del Marketplace. Quando si utilizza un'immagine del Marketplace, è necessario tooinformation sull'immagine di hello, provider di immagini, offerta, SKU e versione. Con un'immagine personalizzata, è sufficiente tooprovide hello ID della risorsa immagine personalizzata hello. 

In hello lo script seguente, si crea una variabile *$image* toostore informazioni sull'utilizzo di immagine personalizzata hello [Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) e quindi si utilizza [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)e specificare l'ID di hello utilizzando hello *$image* variabile appena creata. 

script di Hello crea una macchina virtuale denominata *myVMfromImage* dal nostro immagine personalizzata in un nuovo gruppo di risorse denominato *myResourceGroupFromImage* in hello *Stati Uniti occidentali* percorso.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Gestione delle immagini 

Di seguito sono riportati alcuni esempi di attività di immagine di gestione comuni e come toocomplete loro tramite PowerShell.

Elencare tutte le immagini per nome.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Eliminare un'immagine. In questo esempio elimina hello immagine denominata *myOldImage* da hello *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stata creata un'immagine di macchina virtuale personalizzata. Si è appreso come:

> [!div class="checklist"]
> * Eseguire Sysprep e generalizzare le macchine virtuali
> * Creare un'immagine personalizzata
> * Creare una VM da un'immagine personalizzata
> * Elenco di tutte le immagini di hello nella sottoscrizione
> * Eliminare un'immagine

Spostare toohello Avanti toolearn esercitazione sulle macchine virtuali a disponibilità elevata come.

> [!div class="nextstepaction"]
> [Creare VM a disponibilità elevata](tutorial-availability-sets.md)



