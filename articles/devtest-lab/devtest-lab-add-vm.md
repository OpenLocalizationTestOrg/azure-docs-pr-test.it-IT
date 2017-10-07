---
title: un laboratorio di tooa VM Azure DevTest Labs aaaAdd | Documenti Microsoft
description: Informazioni su come tooadd un lab tooa macchina virtuale in Azure DevTest Labs
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
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>Aggiungere un ambiente lab tooa VM in Azure DevTest Labs
Se è già stata [creata la prima VM](devtest-lab-create-first-vm.md), l'operazione è stata eseguita con un'[immagine di marketplace](devtest-lab-configure-marketplace-images.md) precaricata. A questo punto, se si desidera tooadd successive le macchine virtuali tooyour lab, è anche possibile scegliere un *base* in un [immagine personalizzata](devtest-lab-create-template.md) o [formula](devtest-lab-manage-formulas.md). In questa esercitazione illustra l'utilizzo hello tooadd portale Azure un ambiente lab tooa VM in DevTest Labs.

In questo articolo mostra anche come toomanage hello elementi per una macchina virtuale nell'ambiente lab.

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>Passaggi tooadd un laboratorio di tooa VM Azure DevTest Labs
1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
1. Elenco dei laboratori hello selezionare lab hello in cui si desidera toocreate hello VM.  
1. Nel lab di hello **Panoramica** pannello seleziona **+ Aggiungi**.  

    ![Pulsante Aggiungi VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. In hello **scegliere una base** pannello, selezionare un valore di base per hello macchina virtuale.
1. In hello **macchina virtuale** pannello, immettere un nome per la macchina virtuale nuova hello in hello **nome della macchina virtuale** casella di testo.

    ![Pannello Lab VM (VM lab)](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. Immettere un **nome utente** che vengono concessi privilegi di amministratore nella macchina virtuale hello.  
1. Se si desidera toouse una password archiviati nel [archivio segreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)selezionare **utilizzano un segreto salvato**e specificare un valore di chiave corrispondente tooyour segreto (password). In caso contrario, immettere una password nel campo di testo hello etichettata **digitare un valore**.
1. Hello **il tipo di disco di macchina virtuale** determina il tipo di disco di archiviazione è consentito per le macchine virtuali hello in lab hello.
1. Selezionare **dimensioni della macchina virtuale** e selezionare una delle hello predefiniti elementi che specificano le dimensioni del disco rigido hello di hello VM toocreate core del processore hello e dimensioni della RAM.
1. Selezionare **elementi** e - hello elenco di elementi - selezionare e configurare hello elementi che si desidera tooadd toohello immagine di base.
    **Nota:** Labs tooDevTest nuovo o di configurazione degli elementi, fare riferimento toohello [aggiungere un tooa artefatto esistente VM](#add-an-existing-artifact-to-a-vm) sezione e quindi tornare qui al termine.
1. Selezionare **impostazioni avanzate** opzioni di scadenza e le opzioni di rete della macchina virtuale di tooconfigure hello. 

   tooset un'opzione di scadenza, scegliere toospecify icona di calendario hello una data in cui hello VM verrà eliminata automaticamente.  Per impostazione predefinita, hello VM non ha scadenza. 
1. Se si desidera tooview o copiare il modello di gestione risorse di Azure hello, fare riferimento toohello [modello salvare Azure Resource Manager](#save-azure-resource-manager-template) sezione e tornare qui al termine.
1. Selezionare **crea** tooadd hello specificato lab toohello macchina virtuale.
1. Pannello lab Hello Visualizza lo stato di hello della creazione della macchina virtuale di hello - innanzitutto come **creazione**, quindi come **esecuzione** dopo hello macchina virtuale è stata avviata.

> [!NOTE]
> [Aggiungere una macchina virtuale di claimable](devtest-lab-add-claimable-vm.md) viene illustrato come toomake hello claimable macchina virtuale in modo che sia disponibile per l'utilizzo da qualsiasi utente nell'ambiente lab hello.
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>Aggiungere un tooa artefatto esistente VM
Durante la creazione di una macchina virtuale, è possibile aggiungere elementi esistenti. Ogni esercitazione include gli elementi dal Repository di artefatti pubblica DevTest Labs hello e gli elementi che è stato creato e aggiunto tooyour proprietari Repository di artefatti.

* Azure DevTest Labs *elementi* consentono di specificare *azioni* che vengono eseguite quando viene eseguito il provisioning hello macchina virtuale, ad esempio l'esecuzione di script di Windows PowerShell, l'esecuzione di comandi Bash e installazione del software.
* Elemento *parametri* consentono di personalizzare l'elemento hello per un determinato scenario

toodiscover toocreate elementi, vedere hello articolo [Scopri tooauthor i propri elementi per utilizzano con DevTest Labs](devtest-lab-artifact-author.md).

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
1. Selezionare lab hello contenente VM hello con cui si desidera toowork hello elenco di esercitazioni.  
1. Selezionare **Macchine virtuali**.
1. Seleziona hello desiderato macchina virtuale.
1. Selezionare **Elementi**. 
1. Selezionare **Apply artifacts** (Applica elementi).
1. In hello **applicare elementi** blade, elemento selezionare hello desiderato tooadd toohello macchina virtuale.
1. In hello **Aggiungi elemento** pannello, immettere i valori dei parametri hello richiesto ed eventuali parametri facoltativi che è necessario.  
1. Selezionare **Aggiungi** tooadd hello artefatto e restituire toohello **applicare elementi** blade.
1. Continuare ad aggiungere gli elementi necessari per la macchina virtuale.
1. Dopo aver aggiunto gli elementi, è possibile [modificare hello ordine in cui hello vengono eseguiti gli elementi](#change-the-order-in-which-artifacts-are-run). È possibile inoltre tornare troppo[consente di visualizzare o modificare un elemento](#view-or-modify-an-artifact).
1. Una volta aggiunti tutti gli elementi, selezionare **Applica**

## <a name="change-hello-order-in-which-artifacts-are-run"></a>Modificare l'ordine di hello in cui vengono eseguiti gli elementi
Per impostazione predefinita, le azioni di artefatti hello hello vengono eseguite in ordine hello in cui vengono aggiunti toohello VM. Hello passaggi seguenti viene illustrato come toochange hello ordine in cui hello vengono eseguiti gli elementi.

1. Nella parte superiore di hello di hello **applicare elementi** blade, collegamento selezionare hello che indica il numero di hello di elementi che sono stati aggiunti toohello macchina virtuale.
   
    ![Numero di elementi inseriti tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. In hello **selezionati elementi** pannello, trascinamento della selezione elementi hello in hello desiderato dell'ordine. **Nota:** nel caso di problemi con il trascinamento di elementi di hello, assicurarsi che si trascina dal lato sinistro di artefatto hello hello. 
1. Selezionare **OK** al termine dell'operazione.  

## <a name="view-or-modify-an-artifact"></a>visualizzare o modificare un elemento
Hello passaggi seguenti viene illustrato come tooview o modificare i parametri di hello di un elemento:

1. Nella parte superiore di hello di hello **applicare elementi** blade, collegamento selezionare hello che indica il numero di hello di elementi che sono stati aggiunti toohello macchina virtuale.
   
    ![Numero di elementi inseriti tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. In hello **selezionati elementi** blade, elemento selezionare hello che desidera tooview o modificare.  
1. In hello **Aggiungi elemento** pannello, apportare le eventuali modifiche necessarie e selezionare **OK** tooclose hello **Aggiungi elemento** blade.
1. Selezionare **OK** tooclose hello **selezionati elementi** blade.

## <a name="save-azure-resource-manager-template"></a>Save Azure Resource Manager template
Un modello di gestione risorse di Azure fornisce toodefine una modalità dichiarativa per una distribuzione ripetibile. Hello alla procedura seguente viene illustrato come toosave hello modello di gestione risorse di Azure per hello macchina virtuale da creare.
Dopo il salvataggio, è possibile utilizzare il modello di gestione risorse di Azure hello troppo[distribuire nuove macchine virtuali con Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).

1. In hello **macchina virtuale** pannello seleziona **modello ARM vista**.
2. In hello **modello di visualizzazione Azure Resource Manager** blade, testo modello selezionare hello.
3. Copiare negli Appunti toohello di hello testo selezionato.
4. Selezionare **OK** tooclose hello **pannello visualizzazione modello di gestione risorse di Azure**.
5. Aprire un editor di testo.
6. Incolla il testo modello hello dagli Appunti hello.
7. Salvare il file hello per un uso successivo.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Passaggi successivi
* Una volta hello VM è stato creato, è possibile connettersi toohello VM selezionando **Connetti** nel pannello hello della macchina virtuale.
* Informazioni su come troppo[creare elementi personalizzati per le VM di DevTest Labs](devtest-lab-artifact-author.md).
* Esplorare hello [raccolta di modelli di DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
