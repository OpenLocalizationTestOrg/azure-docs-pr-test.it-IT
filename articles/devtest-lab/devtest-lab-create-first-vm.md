---
title: aaaCreate la prima macchina virtuale in un ambiente lab in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come toocreate prima macchina virtuale in un ambiente lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>Creare la prima macchina virtuale in Azure DevTest Labs

Quando si inizialmente accedere DevTest Labs e toocreate la prima macchina virtuale, probabilmente a tale scopo, utilizzando una pre-caricato [un'immagine del marketplace base](devtest-lab-configure-marketplace-images.md). Successivamente, sarà anche in grado di toochoose da un [immagine personalizzata e una formula](devtest-lab-add-vm.md) durante la creazione di più macchine virtuali. 

In questa esercitazione illustra utilizzando hello tooadd portale Azure nel lab di tooa prima macchina virtuale di DevTest Labs.

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>I passaggi tooadd il lab di tooa prima di VM in Azure DevTest Labs
1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
1. Elenco dei laboratori hello selezionare lab hello in cui si desidera toocreate hello VM.  
1. Nel lab di hello **Panoramica** pannello seleziona **+ Aggiungi**.  

    ![Pulsante Aggiungi VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. In hello **scegliere una base** pannello Seleziona immagine un marketplace per hello macchina virtuale.
1. In hello **macchina virtuale** pannello, immettere un nome per la macchina virtuale nuova hello in hello **nome della macchina virtuale** casella di testo.

    ![Pannello Lab VM (VM lab)](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. Immettere un **nome utente** che vengono concessi privilegi di amministratore nella macchina virtuale hello.  
1. Immettere una password nel campo di testo hello etichettata **digitare un valore**.
1. Hello **il tipo di disco di macchina virtuale** determina il tipo di disco di archiviazione è consentito per le macchine virtuali hello in lab hello.
1. Selezionare **dimensioni della macchina virtuale** e selezionare una delle hello predefiniti elementi che specificano le dimensioni del disco rigido hello di hello VM toocreate core del processore hello e dimensioni della RAM.
1. Selezionare **elementi** e - hello elenco di elementi - selezionare e configurare hello elementi che si desidera tooadd toohello immagine di base.
    **Nota:** Labs tooDevTest nuovo o di configurazione degli elementi, fare riferimento toohello [aggiungere un tooa artefatto esistente VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sezione e quindi tornare qui al termine.
1. Selezionare **crea** tooadd hello specificato lab toohello macchina virtuale.

   Pannello lab Hello Visualizza lo stato di hello della creazione della macchina virtuale di hello - innanzitutto come **creazione**, quindi come **esecuzione** dopo hello macchina virtuale è stata avviata.

## <a name="next-steps"></a>Passaggi successivi
* Una volta hello VM è stato creato, è possibile connettersi toohello VM selezionando **Connetti** nel pannello hello della macchina virtuale.
* Estrarre [aggiungere un ambiente lab tooa VM](devtest-lab-add-vm.md) per informazioni più complete sull'aggiunta di macchine virtuali successive nell'ambiente lab.
* Esplorare hello [raccolta di modelli di DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).
