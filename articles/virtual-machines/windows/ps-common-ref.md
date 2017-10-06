---
title: comandi di PowerShell aaaCommon per macchine virtuali di Azure | Documenti Microsoft
description: "Comuni tooget i comandi di PowerShell è stata avviata la creazione e la gestione delle macchine virtuali Windows in Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Comandi di PowerShell comuni per la creazione e la gestione di macchine virtuali di Azure

Questo articolo vengono illustrate alcune delle hello che Azure PowerShell comandi che è possibile utilizzare toocreate e gestire le macchine virtuali nella sottoscrizione di Azure.  Per una guida più dettagliata con parametri e opzioni della riga di comando specifici, è possibile usare **Get-Help** come *comando*.

Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma nell'account tooyour.

Queste variabili potrebbero essere utile se più di uno dei comandi di hello in esecuzione in questo articolo:

- $location - percorso hello della macchina virtuale hello. È possibile utilizzare [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind un [area geografica](https://azure.microsoft.com/regions/) che funziona automaticamente.
- $myResourceGroup - nome hello hello del gruppo di risorse che contiene una macchina virtuale hello.
- $myVM - nome hello della macchina virtuale hello.

## <a name="create-a-vm"></a>Creare una macchina virtuale

| Attività | comando |
| ---- | ------- |
| Creare una configurazione di macchina virtuale |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) -VMName $myVM -VMSize "Standard_D1_v1"<BR></BR><BR></BR>configurazione della macchina virtuale Hello è usate toodefine o aggiornamento delle impostazioni per hello macchina virtuale. configurazione di Hello viene inizializzato con il nome di hello di hello macchina virtuale e il relativo [dimensioni](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Aggiungere le impostazioni di configurazione |$vm = [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) -VM $vm -Windows -ComputerName $myVM -Credential $cred -ProvisionVMAgent -EnableAutoUpdate<BR></BR><BR></BR>Le impostazioni di sistema operativo [credenziali](https://technet.microsoft.com/library/hh849815.aspx) vengono aggiunti l'oggetto di configurazione toohello che in precedenza è stato creato mediante New-AzureRmVMConfig. |
| Aggiungere un'interfaccia di rete |$vm = [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) -VM $vm -Id $nic.Id<BR></BR><BR></BR>Una macchina virtuale deve avere un [interfaccia di rete](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate in una rete virtuale. È inoltre possibile utilizzare [Get AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve un oggetto di interfaccia di rete esistente. |
| Specificare un'immagine della piattaforma |$vm = [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) -VM $vm -PublisherName "nome_publisher" -Offer "offerta_publisher" -Skus "sku_prodotto" -Version "più_recente"<BR></BR><BR></BR>[Immagine informazioni](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) viene aggiunto l'oggetto di configurazione toohello che in precedenza è stato creato mediante New-AzureRmVMConfig. oggetto Hello restituito da questo comando viene utilizzato solo quando si imposta toouse disco hello del sistema operativo di un'immagine della piattaforma. |
| Impostare toouse disco del sistema operativo di un'immagine della piattaforma |$vm = [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" -CreateOption FromImage<BR></BR><BR></BR>nome Hello del disco del sistema operativo hello e il relativo percorso nel [archiviazione](../../storage/common/storage-powershell-guide-full.md) viene aggiunto l'oggetto di configurazione toohello creato in precedenza. |
| Impostare un'immagine generalizzata di toouse disco del sistema operativo |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk.{guid}.vhd" -VhdUri "https://mystore1.blob.core.windows.net/vhds/disk_name.vhd" -CreateOption FromImage -Windows<BR></BR><BR></BR>nome Hello del disco del sistema operativo hello, hello posizione dell'immagine di origine hello e del disco hello in [archiviazione](../../storage/common/storage-powershell-guide-full.md) viene aggiunto l'oggetto di configurazione toohello. |
| Impostare un'immagine specializzata di toouse disco del sistema operativo |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/" -CreateOption Attach -Windows |
| Creare una macchina virtuale |[New-AzureRmVM]() -ResourceGroupName $myResourceGroup -Location $location -VM $vm<BR></BR><BR></BR>Tutte le risorse vengono create in un [gruppo di risorse](../../azure-resource-manager/powershell-azure-resource-manager.md). Prima di eseguire questo comando, eseguire New-AzureRmVMConfig, Set-AzureRmVMOperatingSystem, Set-AzureRmVMSourceImage, Add-AzureRmVMNetworkInterface e Set-AzureRmVMOSDisk. |

## <a name="get-information-about-vms"></a>Visualizzare le informazioni sulle VM

| Attività | Comando |
| ---- | ------- |
| Elencare le macchine virtuali in una sottoscrizione |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Elencare le macchine virtuali in un gruppo di risorse |Get-AzureRmVM -ResourceGroupName $myResourceGroup<BR></BR><BR></BR>tooget gruppi di un elenco di risorse nella sottoscrizione, utilizzare [Get AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Visualizzare informazioni su una macchina virtuale |Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM |

## <a name="manage-vms"></a>Gestire le macchine virtuali
| Attività | Comando |
| --- | --- |
| Avviare una macchina virtuale |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Arrestare una macchina virtuale |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Riavviare una macchina virtuale in esecuzione |[Restart-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Eliminare una macchina virtuale |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Generalizzare una macchina virtuale |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM -Generalized<BR></BR><BR></BR>È necessario eseguire questo comando prima di eseguire Save-AzureRmVMImage. |
| Acquisire una macchina virtuale |[Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) -ResourceGroupName $myResourceGroup -VMName $myVM -DestinationContainerName "myImageContainer" -VHDNamePrefix "myImagePrefix" -Path "C:\filepath\filename.json"<BR></BR><BR></BR>Una macchina virtuale deve essere [preparato, arrestare e generalizzato](prepare-for-upload-vhd-image.md) toocreate toobe usata un'immagine. Prima di eseguire questo comando, eseguire Set-AzureRmVm. |
| Aggiornare una macchina virtuale |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) -ResourceGroupName $myResourceGroup -VM $vm<BR></BR><BR></BR>Ottenere la configurazione macchina virtuale corrente hello utilizzando Get-AzureRmVM, modificare le impostazioni di configurazione nell'oggetto macchina virtuale hello e quindi eseguire questo comando. |
| Aggiungere un tooa disco dati VM |[Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) -VM $vm -Name "myDataDisk" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" -LUN # -Caching ReadWrite -DiskSizeinGB # -CreateOption Empty<BR></BR><BR></BR>Utilizzare l'oggetto macchina virtuale di Get-AzureRmVM tooget hello. Specificare il numero LUN hello e dimensioni di hello del disco hello. Eseguire l'aggiornamento AzureRmVM tooapply hello configurazione modifiche toohello macchina virtuale. disco Hello aggiunti non inizializzato. |
| Rimuovere un disco dati da una macchina virtuale |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) -VM $vm -Name "myDataDisk"<BR></BR><BR></BR>Utilizzare l'oggetto macchina virtuale di Get-AzureRmVM tooget hello. Eseguire l'aggiornamento AzureRmVM tooapply hello configurazione modifiche toohello macchina virtuale. |
| Aggiungere un tooa estensione VM |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) -ResourceGroupName $myResourceGroup -Location $location -VMName $myVM -Name "extensionName" -Publisher "publisherName" -Type "extensionType" -TypeHandlerVersion "#.#" -Settings $Settings -ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Eseguire questo comando con hello appropriato [informazioni di configurazione](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) per estensione hello che si desidera tooinstall. |
| Rimuovere un'estensione di macchina virtuale |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) -ResourceGroupName $myResourceGroup -Name "extensionName" -VMName $myVM |

## <a name="next-steps"></a>Passaggi successivi
* Vedere i passaggi di base per la creazione di una macchina virtuale in hello [creare una macchina virtuale Windows usando Gestione risorse e PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

