---
title: un'immagine personalizzata Azure DevTest Labs da un file VHD aaaCreate | Documenti Microsoft
description: Informazioni su come un'immagine personalizzata in Azure DevTest Labs da un file di disco rigido virtuale tramite toocreate hello portale di Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>Creare un'immagine personalizzata da un file VHD

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Istruzioni dettagliate

Hello passaggi seguenti consentono di eseguire la creazione di un'immagine personalizzata da un file VHD utilizzando hello portale di Azure:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.

1. Elenco dei laboratori hello selezionare lab desiderato hello.  

1. Nel pannello del lab hello, selezionare **configurazione**. 

1. Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.

1. In hello **immagini personalizzate** pannello seleziona **+ Aggiungi**.

    ![Aggiungere un'immagine personalizzata](./media/devtest-lab-create-template/add-custom-image.png)

1. Immettere il nome di hello dell'immagine personalizzata hello. Questo nome viene visualizzato nell'elenco di hello di immagini di base durante la creazione di una macchina virtuale.

1. Immettere una descrizione hello dell'immagine personalizzata hello. Questa descrizione viene visualizzata nell'elenco di hello di immagini di base durante la creazione di una macchina virtuale.

1. Selezionare **VHD**.

1. Da hello **VHD** pannello, il file di disco rigido virtuale selezionare hello desiderato.

1. Selezionare **OK** tooclose hello **VHD** blade.

1. Selezionare **Configurazione sistema operativo**.

1. In hello **configurazione del sistema operativo** scheda, selezionare l'opzione **Windows** o **Linux**.

1. Se **Windows** è selezionata, specificare tramite la casella di controllo di hello se *Sysprep* è stato eseguito nel computer di hello. 

1. Selezionare **OK** tooclose hello **configurazione del sistema operativo** blade.

1. Selezionare **OK** toocreate immagine personalizzata di hello.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Post di blog correlati

- [Custom images or formulas? (Immagini personalizzate o formule?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copia di immagini personalizzate tra istanze di Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Passaggi successivi

- [Aggiungere un ambiente lab tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
