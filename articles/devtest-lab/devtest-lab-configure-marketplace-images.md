---
title: impostazioni delle immagini aaaConfigure Azure Marketplace in Azure DevTest Labs | Documenti Microsoft
description: Specificare le immagini di Azure Marketplace che possono essere usate per la creazione di una VM in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Configurare le impostazioni dell'immagine di Azure Marketplace in Azure DevTest Labs
DevTest Labs supporta la creazione macchine virtuali basate su immagini di Azure Marketplace a seconda della modalità di configurazione di Azure Marketplace toobe di immagini usato nell'ambiente lab. In questo articolo illustra come toospecify che, se presente, le immagini di Azure Marketplace possono essere utilizzati durante la creazione di macchine virtuali in un ambiente lab. In questo modo si garantisce che il team dispone solo di immagini di Marketplace toohello di accesso che necessarie. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Selezionare le immagini di Azure Marketplace consentite per la creazione di una macchina virtuale
1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello. 
4. Nel pannello del lab hello, selezionare **criteri di configurazione e**.
5. Nel pannello **Configuration and policies** (Configurazione e criteri) di lab in **Virtual Machine Bases** (Basi della macchina virtuale) selezionare **Marketplace images** (Immagini Marketplace).
6. Specificare se si desidera che tutti hello Azure Marketplace completo immagini toobe disponibili per l'utilizzo come base di una nuova macchina virtuale. Se si seleziona **Sì**, quindi tutte le immagini di Azure Marketplace hello che soddisfano tutte hello seguenti criteri sono consentite in hello lab:
   
   * immagine di Hello crea una singola macchina virtuale, **e**
   * immagine di Hello Usa le macchine virtuali di Azure Resource Manager tooprovision, **e**
   * immagine di Hello non richiede l'acquisto di un piano di licenze aggiuntive
     
    Se non si desidera alcun toobe immagini consentito, o si desidera toospecify le immagini possono essere utilizzati, selezionare **n**.
     
     ![Opzione tooallow tutti Marketplace immagini toobe utilizzati come immagini di base per le macchine virtuali](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. Se si seleziona **n** toohello precedente passaggio hello **immagini consentiti/Seleziona tutti** casella di controllo è abilitato. 
   È possibile utilizzare questa opzione insieme hello ricerca tooquickly selezionare o deselezionare tutti gli elementi di hello visualizzati nell'elenco di hello.
   * Selezionare le immagini di Azure Marketplace hello desiderate tooallow per la creazione di VM singolarmente selezionando la casella di controllo corrispondente per l'immagine.
   * Senza selezionare alcun elemento dall'elenco hello se non vuoi tooallow qualsiasi toobe immagini di Azure Marketplace usati nel lab hello.
   
    ![È possibile specificare quali immagini di Azure Marketplace possono essere usate come immagini di base per le macchine virtuali](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato come immagini di Azure Marketplace sono consentite durante la creazione di una macchina virtuale, hello è troppo[aggiungere un ambiente lab tooyour VM](devtest-lab-add-vm-with-artifacts.md).

