---
title: un'immagine personalizzata da una macchina virtuale Azure DevTest Labs in aaaCreate | Documenti Microsoft
description: Informazioni su come un'immagine personalizzata in Azure DevTest Labs da una macchina virtuale con provisioning toocreate hello portale di Azure
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>Creare un'immagine personalizzata da una VM

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>Istruzioni dettagliate

È possibile creare un'immagine personalizzata da una macchina virtuale di provisioning e successivamente usare tale toocreate immagine personalizzata macchine virtuali identiche. Hello alla procedura seguente viene illustrato come toocreate immagine personalizzata da una macchina virtuale:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.

1. Elenco dei laboratori hello selezionare lab desiderato hello.  

1. Nel pannello del lab hello, selezionare **macchine virtuali**.
 
1. In hello **macchine virtuali** pannello selezionare hello VM da cui si desidera toocreate immagine personalizzata di hello.

1. Nel pannello hello della macchina virtuale, selezionare **Crea immagine personalizzata (VHD)**.

    ![Voce di menu Crea immagine personalizzata](./media/devtest-lab-create-template/create-custom-image.png)

1. In hello **Crea immagine** pannello, immettere un nome e una descrizione per l'immagine personalizzata. Queste informazioni vengono visualizzate nell'elenco di hello di base quando si crea una macchina virtuale.

    ![Pannello Crea immagine personalizzata](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. Consente di indicare se è stato eseguito sysprep nella macchina virtuale hello. Se non è stato eseguito sysprep hello in hello macchina virtuale, specificare se si desidera eseguire quando una macchina virtuale viene creata da questa immagine personalizzata di sysprep.

1. Selezionare **OK** quando toocreate termine hello immagine personalizzata.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Post di blog correlati

- [Custom images or formulas? (Immagini personalizzate o formule?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copia di immagini personalizzate tra istanze di Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Passaggi successivi

- [Aggiungere un ambiente lab tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
