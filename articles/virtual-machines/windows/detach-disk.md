---
title: un disco dati da una macchina virtuale di Windows - Azure aaaDetach | Documenti Microsoft
description: Informazioni su un disco dati da una macchina virtuale in Azure tramite il modello di distribuzione di gestione risorse di hello toodetach.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Funzionamento dei dischi toodetach un tipo di dati da una macchina virtuale di Windows
Quando non è più necessario un disco dati è una macchina virtuale tooa collegato, è possibile scollegarlo facilmente. Rimuove il disco hello dalla macchina virtuale hello, ma non rimuove dall'archivio.

> [!WARNING]
> Se si scollega un disco, questo non viene automaticamente eliminato. Se è stato richiesto tooPremium archiviazione, si continuerà tooincur i costi di archiviazione per il disco di hello. Per ulteriori informazioni, vedere troppo[prezzi e fatturazione quando si utilizza l'archiviazione Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).
>
>

Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.

## <a name="detach-a-data-disk-using-hello-portal"></a>Scollegare un disco dati tramite il portale di hello
1. Nell'hub portale hello, selezionare **macchine virtuali**.
2. Selezionare macchina virtuale hello che ha il disco dati hello toodetach desiderato e fare clic su **arrestare** toodeallocate hello macchina virtuale.
3. Nel pannello macchine virtuali di hello, selezionare **dischi**.
4. Nella parte superiore di hello di hello **dischi** pannello seleziona **modifica**.
5. In hello **dischi** pannello toohello a destra del disco dati hello che si desidera toodetach, fare clic su hello ![immagine del pulsante scollegamento](./media/detach-disk/detach.png) pulsante Disconnetti.
5. Una volta rimosso il disco di hello, fare clic su Salva nella parte superiore di hello del pannello hello.
6. Nel Pannello di hello macchina virtuale, fare clic su **Panoramica** e quindi fare clic su hello **avviare** pulsante nella parte superiore di hello di hello toorestart di hello pannello VM.



Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.

## <a name="detach-a-data-disk-using-powershell"></a>Scollegare un disco dati tramite PowerShell
In questo esempio hello primo comando Ottiene hello macchina virtuale denominata **MyVM07** in hello **RG11** gruppo di risorse utilizzando il cmdlet Get-AzureRmVM hello. comando archivi hello macchina virtuale in hello Hello **$VirtualMachine** variabile.

Hello secondo comando rimuove il disco di dati hello denominato DataDisk3 dalla macchina virtuale hello.

comando finale Hello Aggiorna stato hello del processo di hello macchina virtuale toocomplete hello della rimozione di dischi dati hello.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

Per altre informazioni, vedere [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Passaggi successivi
Se si desidera disco dati di hello tooreuse, è sufficiente [collegarlo tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

