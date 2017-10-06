---
title: un laboratorio tooa claimable VM Azure DevTest Labs aaaAdd | Documenti Microsoft
description: Informazioni su come tooadd un lab tooa claimable macchina virtuale in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Aggiungere un ambiente lab claimable tooa VM in Azure DevTest Labs
Si aggiunge un claimable lab tooa macchina virtuale in un simile toohow modo si [aggiungere una macchina virtuale standard](devtest-lab-add-vm.md) : da un *base* in un [immagine personalizzata](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), o [un'immagine del Marketplace](devtest-lab-configure-marketplace-images.md). In questa esercitazione illustra hello tooadd portale Azure utilizzando un laboratorio VM tooa claimable di DevTest Labs e illustra il processo di hello di che un utente avrà seguito tooclaim hello VM.

> [!NOTE]
> Se si distribuiscono le macchine virtuali lab tramite [modelli di gestione risorse di Azure](devtest-lab-create-environment-from-arm.md), è possibile creare macchine virtuali claimable impostazione hello **allowClaim** tootrue proprietà nella sezione proprietà hello.
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>Passaggi tooadd un laboratorio tooa claimable VM Azure DevTest Labs
1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
1. Selezionare lab hello hello elenco di esercitazioni in cui si desidera toocreate hello claimable macchina virtuale.  
1. Nel lab di hello **Panoramica** pannello seleziona **+ Aggiungi**.  

    ![Pulsante Aggiungi VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. In hello **scegliere una base** pannello, selezionare un valore di base per hello macchina virtuale.
1. In hello **macchina virtuale** pannello, immettere un nome per la macchina virtuale nuova hello in hello **nome della macchina virtuale** casella di testo.

    ![Pannello Lab VM (VM lab)](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Immettere un **nome utente** che vengono concessi privilegi di amministratore nella macchina virtuale hello.  
1. Se si desidera toouse una password archiviati nel [archivio segreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)selezionare **utilizzano un segreto salvato**e specificare un valore di chiave corrispondente tooyour segreto (password). In caso contrario, immettere una password nel campo di testo hello etichettata **digitare un valore**.
1. Hello **il tipo di disco di macchina virtuale** determina il tipo di disco di archiviazione è consentito per le macchine virtuali hello in lab hello.
1. Selezionare **dimensioni della macchina virtuale** e selezionare una delle hello predefiniti elementi che specificano le dimensioni del disco rigido hello di hello VM toocreate core del processore hello e dimensioni della RAM.
1. Selezionare **elementi** e hello elenco di elementi, selezionare e configurare hello elementi che si desidera tooadd toohello immagine di base. Se si è nuovo tooDevTest Labs o configurazione degli elementi, vedere toohello [aggiungere un tooa artefatto esistente VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sezione e quindi tornare qui al termine.
1. Selezionare **impostazioni avanzate** opzioni di scadenza e le opzioni di rete della macchina virtuale di tooconfigure hello. In **attestazione opzioni**, scegliere **Sì** macchina hello toomake claimable.

  ![Scegliere toomake hello claimable macchina virtuale.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. Se si desidera tooview o copiare il modello di gestione risorse di Azure hello, fare riferimento toohello [modello salvare Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) sezione e tornare qui al termine.
1. Selezionare **crea** tooadd hello specificato lab toohello macchina virtuale.
1. Pannello lab Hello Visualizza lo stato di hello della creazione della macchina virtuale di hello - innanzitutto come **creazione**, quindi come **esecuzione** dopo hello macchina virtuale è stata avviata.


## <a name="using-a-claimable-vm"></a>Usare una macchina virtuale a disposizione degli utenti

Un utente può richiedere qualsiasi macchina virtuale dall'elenco di hello di "Macchine virtuali Claimable" effettuando una delle operazioni seguenti:

* Elenco di hello di "Macchine virtuali Claimable" nella parte inferiore di hello del pannello della panoramica del lab hello, fare clic su una delle macchine virtuali di hello nell'elenco di hello e scegliere **macchina attestazione**.

 ![Richiedere una specifica macchina virtuale a disposizione degli utenti.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* Nella parte superiore di hello di hello **Panoramica** pannello, scegliere **qualsiasi attestazione**. Una macchina virtuale casuale viene assegnata dall'elenco di hello di claimable macchine virtuali.

 ![Richiedere una macchina virtuale a disposizione degli utenti.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


Quando una macchina virtuale viene richiesta da un utente, questa viene spostata in alto nell'elenco "My virtual machines" (Le mie macchine virtuali) e non è più disponibile per un altro utente.

## <a name="next-steps"></a>Passaggi successivi
* Una volta hello VM è stato creato, è possibile connettersi toohello VM selezionando **Connetti** nel pannello hello della macchina virtuale.
* Esplorare hello [raccolta di modelli di DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
