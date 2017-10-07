---
title: le formule aaaManage in Azure DevTest Labs toocreate macchine virtuali | Documenti Microsoft
description: Informazioni su come tooupdate e rimuovere le formule Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Gestire le formule di Azure DevTest Labs

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

Questo articolo illustra come toocreate una formula da una base (immagine personalizzata, un'immagine del Marketplace o un'altra formula) o una macchina virtuale esistente. Questo articolo illustra inoltre la gestione delle formule esistenti.

## <a name="create-a-formula"></a>Creare una formula
Chiunque disponga di DevTest Labs *utenti* autorizzazioni è macchine virtuali in grado di toocreate utilizzando una formula come base. Esistono due modi toocreate formule: 

* Da una base - utilizzare quando si desidera toodefine tutte le caratteristiche di hello della formula hello.
* Da un ambiente lab esistente VM - utilizzare questa opzione quando si desidera toocreate una formula in base alle impostazioni di hello di una macchina virtuale esistente.

Per altre informazioni sull'aggiunta di utenti e autorizzazioni, vedere [Aggiungere proprietari e utenti in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Creare una formula di base
Hello alla procedura seguente illustra il processo di hello di creazione di una formula da un'immagine personalizzata, un'immagine del Marketplace o da un'altra formula.

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.

3. Elenco dei laboratori hello selezionare lab desiderato hello.  

4. Nel pannello del lab hello, selezionare **formule (base riutilizzabile)**.
   
    ![Menu Formula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. In hello **formule** pannello seleziona **+ Aggiungi**.
   
    ![Aggiungere una formula](./media/devtest-lab-create-formulas/add-formula.png)

6. In hello **scegliere una base** base selezionare hello (immagine personalizzata, un'immagine del Marketplace o formula) da cui si desidera formula hello toocreate pannello.
   
    ![Elenco base](./media/devtest-lab-create-formulas/base-list.png)

7. In hello **creare formula** pannello specificare hello seguenti valori:
   
    * **Nome formula** : immettere un nome per la formula. Questo valore viene visualizzato nell'elenco di hello di immagini di base quando si crea una macchina virtuale. nome Hello viene convalidato durante la digitazione e, se non è valido, un messaggio significa requisiti hello per un nome valido.
    * **Descrizione** : immettere una descrizione significativa per la formula. Questo valore è disponibile dal menu di scelta rapida della formula hello quando si crea una macchina virtuale.
    * **Nome utente** - Immettere un nome utente a cui siano concessi i privilegi di amministratore.
    * **Password** - immettere - o selezionare dall'elenco a discesa hello - valore associata al segreto hello (password) che si desidera toouse per utente specificato hello. Per ulteriori informazioni su segreti hello, vedere [Azure DevTest Labs: archivio segreto personale](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Tipo di disco di macchina virtuale** : specificare l'unità disco rigido (disco rigido) o l'archiviazione su disco di tipo tooindicate di unità SSD (Solid-State) è consentita per le macchine virtuali hello eseguito il provisioning con questa immagine di base.
    * * * Macchina virtuale dimensioni * * - selezionare uno degli elementi di hello predefinito che specificano le dimensioni del disco rigido hello di hello VM toocreate core del processore hello e dimensioni della RAM. 
    * **Elementi** -tooopen selezionare hello **aggiungere elementi** pannello, in cui selezionare e configurare hello elementi che si desidera tooadd toohello immagine di base. Per altre informazioni sugli elementi, vedere [Gestire elementi di macchine virtuali in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Impostazioni avanzate** -tooopen selezionare hello **avanzate** pannello in cui configurare hello seguenti impostazioni:
        * **Rete virtuale** -è necessario specificare hello rete virtuale.
        * **Subnet** -specificare la subnet hello desiderato.    
        * **Configurazione degli indirizzi IP** -specificare se si desidera che gli indirizzi IP condiviso, privata o pubblica hello. Per altre informazioni sugli indirizzi IP condivisi, vedere [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md) (Informazioni sugli indirizzi IP condivisi in Azure Devtest Labs).
        * **Rendere questa macchina claimable** -effettua una macchina "claimable" significa che sarà non assegnato proprietà in fase di creazione di hello. Gli utenti saranno possibile macchina di hello tootake in grado di proprietà ("attestazioni") nel pannello del lab hello.     
    * **Immagine** -questo campo consente di visualizzare nome dell'immagine di base hello selezionato nel pannello precedente hello. 
     
       ![Crea formula](./media/devtest-lab-create-formulas/create-formula.png)

8. Selezionare **crea** formula hello toocreate.

9. Quando la formula hello è stata creata, viene visualizzato nell'elenco hello hello **formule** blade.

### <a name="create-a-formula-from-a-vm"></a>Creare una formula da una VM
Hello passaggi seguenti consentono di eseguire il processo di hello di creazione di una formula basata su una macchina virtuale esistente. 

> [!NOTE]
> toocreate una formula da una macchina virtuale, hello VM deve essere stato creato dopo il 30 marzo 2016. 
> 
> 

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello.  
4. Nel lab di hello **Panoramica** pannello selezionare hello VM da cui si desidera formula hello toocreate.
   
    ![Macchine virtuali di lab](./media/devtest-lab-create-formulas/my-vms.png)
5. Nel pannello hello della macchina virtuale, selezionare **creare formula (base riutilizzabile)**.
   
    ![Crea formula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. In hello **creare formula** pannello, immettere un **nome** e **descrizione** per la nuova formula.
   
    ![Pannello Crea formula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Selezionare **OK** formula hello toocreate.

## <a name="modify-a-formula"></a>Modificare una formula
toomodify una formula, seguire questi passaggi:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello.  
4. Nel pannello del lab hello, selezionare **formule (base riutilizzabile)**.
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. In hello **formule Lab** blade, formula hello selezionare desiderato toomodify.
6. In hello **aggiorna formula** pannello hello lo si desidera modificare e selezionare **aggiornamento**.

## <a name="delete-a-formula"></a>Eliminare una formula
toodelete una formula, seguire questi passaggi:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello.  
4. Lab hello **impostazioni** pannello seleziona **formule**.
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. In hello **formule Lab** blade, hello selezionare i puntini di sospensione toohello destra della formula hello desiderato toodelete.
   
    ![Menu Formula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. Selezionare il menu di scelta rapida della formula hello **eliminare**.
   
    ![Menu di scelta rapida Formula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Selezionare **Sì** toohello finestra di dialogo Conferma eliminazione.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Post di blog correlati
* [Custom images or formulas? (Immagini personalizzate o formule?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato una formula da utilizzare durante la creazione di una macchina virtuale, hello è troppo[aggiungere un ambiente lab tooyour VM](devtest-lab-add-vm-with-artifacts.md).

