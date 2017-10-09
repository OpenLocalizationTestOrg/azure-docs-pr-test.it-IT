---
title: un disco dati da una VM Linux - Azure aaaDetach | Documenti Microsoft
description: Informazioni toodetach un disco dati da una macchina virtuale in Azure utilizzando CLI 2.0 o hello portale di Azure.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Funzionamento dei dischi toodetach un tipo di dati da una macchina virtuale di Linux

Quando non è più necessario un disco dati è una macchina virtuale tooa collegato, è possibile scollegarlo facilmente. Rimuove il disco hello dalla macchina virtuale hello, ma non rimuove dall'archivio. 

> [!WARNING]
> Se si scollega un disco, questo non viene automaticamente eliminato. Se è stato richiesto tooPremium archiviazione, si continuerà tooincur i costi di archiviazione per il disco di hello. Per ulteriori informazioni, vedere troppo[prezzi e fatturazione quando si utilizza l'archiviazione Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing). 
> 
> 

Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.  

## <a name="detach-a-data-disk-using-cli-20"></a>Scollegare un disco dati tramite l'interfaccia della riga di comando 2.0

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.


## <a name="detach-a-data-disk-using-hello-portal"></a>Scollegare un disco dati tramite il portale di hello
1. Nell'hub portale hello, selezionare **macchine virtuali**.
2. Selezionare macchina virtuale hello che ha il disco dati hello toodetach desiderato e fare clic su **arrestare** toodeallocate hello macchina virtuale.
3. Nel pannello macchine virtuali di hello, selezionare **dischi**.
4. Nella parte superiore di hello di hello **dischi** pannello seleziona **modifica**.
5. In hello **dischi** pannello toohello a destra del disco dati hello che si desidera toodetach, fare clic su hello ![immagine del pulsante scollegamento](./media/detach-disk/detach.png) pulsante Disconnetti.
5. Una volta rimosso il disco di hello, fare clic su Salva nella parte superiore di hello del pannello hello.
6. Nel Pannello di hello macchina virtuale, fare clic su **Panoramica** e quindi fare clic su hello **avviare** pulsante nella parte superiore di hello di hello toorestart di hello pannello VM.

Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.








## <a name="next-steps"></a>Passaggi successivi
Se si desidera disco dati di hello tooreuse, è sufficiente [collegarlo tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

