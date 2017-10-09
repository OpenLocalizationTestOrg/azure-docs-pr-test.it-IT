---
title: un disco rigido virtuale di Windows da Azure aaaDownload | Documenti Microsoft
description: Scaricare un disco rigido virtuale di Windows utilizzando hello portale di Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Scaricare un disco rigido virtuale Linux da Azure

In questo articolo viene illustrato come toodownload un [Windows disco rigido virtuale (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello di file da Azure tramite il portale di Azure. 

Macchine virtuali (VM) in uso Azure [dischi](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) come un toostore sul posto del sistema operativo, applicazioni e dati. Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo. disco del sistema operativo Hello viene inizialmente creato da un'immagine e il disco di sistema operativo hello e immagine hello sono dischi rigidi virtuali archiviati in un account di archiviazione di Azure. Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali.

## <a name="stop-hello-vm"></a>Arrestare VM hello

Un disco rigido virtuale non può essere scaricato da Azure se è collegato tooa in esecuzione sulla macchina virtuale. È necessario toodownload VM hello toostop un disco rigido virtuale. Se si desidera toouse un disco rigido virtuale come un [immagine](tutorial-custom-images.md) toocreate altre macchine virtuali con nuovi dischi, utilizzare [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello contenuto nel file hello del sistema operativo e quindi arrestare la macchina virtuale hello. hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, solo necessario toostop e deallocare hello macchina virtuale.

toouse hello VHD come toocreate un'immagine con altre macchine virtuali, completare questi passaggi:

1.  Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com/).
2.  [Connettersi toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  Nella macchina virtuale hello, finestra hello prompt dei comandi come amministratore.
4.  Modificare anche le directory hello*%windir%\system32\sysprep* ed eseguire sysprep.exe.
5.  Nella finestra di dialogo Utilità preparazione sistema hello, selezionare **immettere sistema Out-of-Box guidata**e assicurarsi che **Generalize** è selezionata.
6.  In Opzioni di arresto selezionare **Arresta il sistema** e quindi fare clic su **OK**. 

hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, completare questi passaggi:

1.  Menu hello Hub hello portale di Azure, fare clic su **macchine virtuali**.
2.  Selezionare hello VM hello elenco.
3.  Nel Pannello di hello per hello VM, fare clic su **arrestare**.

    ![Arrestare la macchina virtuale](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Generare l'URL SAS

file di disco rigido virtuale hello toodownload, è necessario toogenerate un [firma di accesso condiviso (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Quando viene generato l'URL di hello, un'ora di scadenza viene assegnata toohello URL.

1.  Dal menu hello del pannello hello hello VM, fare clic su **dischi**.
2.  Selezionare il disco del sistema operativo hello per hello macchina virtuale e quindi fare clic su **esportare**.
3.  Impostare l'ora di scadenza di hello dell'URL hello troppo*36000*.
4.  Fare clic su **Genera URL**.

    ![Generare l'URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> Data di scadenza Hello è aumentato da hello predefinito tooprovide tempo sufficiente toodownload hello di grandi dimensioni file VHD per un sistema operativo Windows Server. È possibile prevedere un file di disco rigido virtuale contenente tootake di sistema operativo Windows Server hello toodownload ore diverse a seconda della connessione. Se si scarica un disco rigido virtuale per un disco dati, l'ora predefinita hello è sufficiente. 
> 
> 

## <a name="download-vhd"></a>Scaricare il disco rigido virtuale

1.  In URL hello che è stato generato, fare clic su file VHD hello di Download.

    ![Scaricare il disco rigido virtuale](./media/download-vhd/export-download.png)

2.  Potrebbe essere necessario tooclick **salvare** nel download di hello browser toostart hello. il nome predefinito Hello per file di disco rigido virtuale hello è *abcd*.

    ![Fare clic su Salva nel browser hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come troppo[caricare un tooAzure file disco rigido virtuale](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Creare dischi gestiti da dischi non gestiti in un account di archiviazione](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [Gestire i dischi di Azure con PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

