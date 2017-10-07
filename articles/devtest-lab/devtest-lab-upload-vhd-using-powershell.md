---
title: disco rigido virtuale aaaUpload file tooAzure DevTest Labs tramite PowerShell | Documenti Microsoft
description: Caricare l'account di archiviazione del toolab file disco rigido virtuale con PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>Caricare l'account di archiviazione del toolab file disco rigido virtuale con PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

In Azure DevTest Labs, i file VHD possono essere utilizzato toocreate immagini personalizzate, che sono utilizzati tooprovision le macchine virtuali. Hello passaggi seguenti consentono l'utilizzo di PowerShell tooupload account di archiviazione del laboratorio di tooa file disco rigido virtuale. Dopo aver caricato il file VHD, hello [passaggi successivi sezione](#next-steps) elenca alcuni articoli che illustrano come un'immagine personalizzata da hello toocreate caricamento del file di disco rigido virtuale. Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Istruzioni dettagliate

esempio Hello passaggi di percorso di caricamento di un disco rigido virtuale del file tooAzure DevTest Labs tramite PowerShell. 

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.

1. Elenco dei laboratori hello selezionare lab desiderato hello.  

1. Nel pannello del lab hello, selezionare **configurazione**. 

1. Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.

1. In hello **immagini personalizzate** pannello selezionare **+ Aggiungi**. 

1. In hello **immagine personalizzata** pannello seleziona **VHD**.

1. In hello **VHD** pannello seleziona **caricare un disco rigido virtuale con PowerShell**.

    ![Carica un file VHD con PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. In hello **carica un'immagine con PowerShell** blade, editor di testo tooa PowerShell script copia hello generato.

1. Modificare hello **LocalFilePath** parametro di hello **Add-AzureVhd** cmdlet toopoint toohello percorso del file di disco rigido virtuale che si desidera tooupload hello.

1. Al prompt di PowerShell, eseguire hello **Add-AzureVhd** cmdlet (con hello modificato **LocalFilePath** parametro).

> [!WARNING] 
> 
> processo Hello di caricamento di un file VHD può essere lungo a seconda delle dimensioni di hello del file VHD hello e la velocità della connessione.

## <a name="next-steps"></a>Passaggi successivi

- [Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD utilizzando hello portale di Azure](devtest-lab-create-template.md)
- [Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
