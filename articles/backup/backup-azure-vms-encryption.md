---
title: aaaBackup e ripristino crittografati macchine virtuali con Backup di Azure
description: In questo articolo illustra i backup di hello ed esperienza di ripristino per le macchine virtuali crittografata con la crittografia del disco di Azure.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>La modalità di crittografia delle macchine virtuali con Azure Backup tooback backup e ripristino
In questo articolo illustra passaggi toobackup e ripristino di macchine virtuali tramite Backup di Azure. Fornisce anche informazioni sugli scenari supportati, i prerequisiti e i passaggi per la risoluzione dei problemi per i casi di errore.

## <a name="supported-scenarios"></a>Scenari supportati
> [!NOTE]
> * L'operazione di backup e ripristino di macchine virtuali crittografate è supportata solo per le macchine virtuali distribuite da Resource Manager. Non è supportata per le macchine virtuali classiche. <br>
> * È supportata per le macchine virtuali Windows e Linux tramite la crittografia del disco di Azure, che sfrutta hello settore caratteristica standard di BitLocker di Windows e funzionalità di data mining Crypt di Linux tooprovide crittografia dei dischi. <br>
> * Questa operazione è supportata solo per le macchine virtuali crittografate usando entrambe le chiavi di crittografia BitLocker e Key. Non è supportata per le macchine virtuali crittografate usando solo la chiave di crittografia BitLocker. <br>
>
>

## <a name="prerequisites"></a>Prerequisiti
1. La macchina virtuale è stata crittografata tramite [Crittografia dischi di Azure](../security/azure-security-disk-encryption.md). Sono state usate sia la chiave di crittografia BitLocker che la chiave di crittografia Key.
2. È stato creato l'archivio di servizi di ripristino e la replica di archiviazione impostata utilizzando i passaggi indicati nell'articolo hello [preparare l'ambiente per il backup](backup-azure-arm-vms-prepare.md).
3. Backup di Azure è stato assegnato [insieme di credenziali chiave tooaccess autorizzazioni](#provide-permissions-to-azure-backup) contenente le chiavi, per i segreti crittografati macchine virtuali.

## <a name="backup-encrypted-vm"></a>Backup di macchine virtuali crittografate
Utilizzare hello obiettivo di backup tooset i passaggi seguenti, definire i criteri, configurare gli elementi e i backup dei trigger.

### <a name="configure-backup"></a>Configurare il backup
1. Se è già aperto un insieme di credenziali di servizi di ripristino, eseguire il passaggio di toonext. Se non è aperto un insieme di credenziali di servizi di ripristino, ma nel portale di Azure, nel menu Hub hello hello fare clic su **Sfoglia**.

   * Nell'elenco di hello delle risorse, digitare **servizi di ripristino**.
   * Si inizia a digitare, hello filtri di elenco in base all'input. Quando viene visualizzata l'opzione, fare clic su **Insiemi di credenziali dei servizi di ripristino**.

      ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino. Hello l'elenco degli insiemi di credenziali di servizi di ripristino, selezionare un insieme di credenziali.

     Apre il dashboard di Hello insieme di credenziali selezionato.
2. Hello elenco di elementi visualizzato in insieme di credenziali, fare clic su **Backup** blade di Backup tooopen hello.

      ![Pannello Backup aperto](./media/backup-azure-vms-encryption/select-backup.png)
3. Nel Pannello di hello Backup, fare clic su **obiettivo Backup** blade di tooopen hello obiettivo di Backup.

      ![Pannello Scenario aperto](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Nel Pannello di hello obiettivo di Backup, impostare **in cui viene eseguito il carico di lavoro** tooAzure e **cosa si desidera toobackup** tooVirtual computer, quindi fare clic su **OK**.

   Chiude il pannello di obiettivo di Backup Hello e apre Pannello criteri di Backup hello.

   ![Pannello Scenario aperto](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Nel Pannello di criteri di Backup hello, selezionare criterio di backup hello desiderata tooapply toohello insieme di credenziali, quindi scegliere **OK**.

      ![Selezionare il criterio di backup](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    dettagli di Hello del criterio predefinito di hello sono elencati in dettagli hello. Se si desidera toocreate un criterio, selezionare **Crea nuovo** dal menu a discesa hello. Quando si fa clic su **OK**, criteri di backup hello sono associato all'insieme di credenziali hello.

    Scegliere quindi hello tooassociate di macchine virtuali con insieme di credenziali hello.
6. Scegliere le macchine virtuali tooassociate con hello specificato criteri e fare clic su crittografato hello **OK**.

      ![Selezionare le macchine virtuali crittografate](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Questa pagina viene visualizzato un messaggio sull'insieme di credenziali chiave che macchine virtuali associate toohello crittografato selezionate. Servizio di backup richiede l'accesso in sola lettura toohello chiavi e segreti nell'insieme di credenziali chiave hello. Usa queste chiave toobackup autorizzazioni e segreto, insieme a hello associate macchine virtuali. **È necessario assegnare le autorizzazioni toobackup servizio tooaccess chiave dell'insieme di credenziali per i backup toowork**. È possibile fornire queste autorizzazioni usando [i passaggi indicati nella seguente sezione hello](#provide-permissions-to-azure-backup).

      ![Messaggio delle macchine virtuali crittografate](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Ora che è stato definito tutte le impostazioni per l'insieme di credenziali hello, nel Pannello di hello Backup fare clic su Abilita Backup nella parte inferiore di hello della pagina hello. Abilitare il Backup consente di distribuire insieme di credenziali toohello hello criteri e le macchine virtuali hello.
8. Hello fase successiva in preparazione installa agente VM hello o effettua hello che agente VM è installato. toodo hello stesso, utilizzare i passaggi di hello indicati nell'articolo hello [preparare l'ambiente per il backup](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Attivazione del processo di backup
Utilizzare i passaggi di hello indicati nell'articolo hello [insieme di credenziali dei servizi macchine virtuali di Azure Backup toorecovery](backup-azure-arm-vms.md) tootrigger processo di backup.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Continuare i backup delle macchine virtuali per cui l'operazione è già stata eseguita con la crittografia abilitata  
Se si dispone di macchine virtuali già da eseguire il backup nell'insieme di credenziali di ripristino services e sono state abilitate per la crittografia in un secondo momento, è necessario assegnare le autorizzazioni toobackup servizio tooaccess chiave dell'insieme di credenziali per i backup toocontinue. È possibile fornire queste autorizzazioni usando [i passaggi nella sezione hello](#provide-permissions-to-azure-backup) o usando PowerShell passaggi indicati in **abilitare il Backup** sezione [documentazione di PowerShell](backup-azure-vms-automation.md). 

## <a name="provide-permissions-tooazure-backup"></a>Fornire le autorizzazioni tooAzure Backup
Utilizzare hello seguendo i passaggi tooprovide autorizzazioni rilevanti tooAzure tooaccess chiave insieme di credenziali Backup ed eseguire il backup di macchine virtuali crittografate:
1. Selezionare **Altri servizi** e cercare **Insiemi di credenziali delle chiavi**.

    ![Cercare l'insieme di credenziali delle chiavi](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. Elenco degli insiemi di credenziali chiave hello selezionare hello insieme di credenziali chiave associate VM crittografato, che deve toobe eseguito il backup.

     ![Selezionare l'insieme di credenziali delle chiavi](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Fare clic su **Criteri di accesso** e quindi su **Aggiungi nuovo**.

    ![Aggiungere un criterio di accesso](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Fare clic su **selezionare entità** e tipo **servizio di gestione di Backup** nella barra di ricerca hello. 

    ![Cercare un servizio di backup](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Selezionare **Backup Management Service** e fare clic sul pulsante Seleziona.

    ![Selezionare un servizio di backup](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Selezionare **Backup di Azure** nell'elenco a discesa Configura dal modello. Autorizzazioni hello necessarie le autorizzazioni di chiave di pre-compilazione e Secret autorizzazioni elenco a discesa. 

    ![Selezionare Backup di Azure](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. Fare clic su **OK**. Si noti che la voce Backup Management Service viene aggiunta nel pannello Criteri di accesso. 

    ![Criteri di accesso del servizio di backup](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. Fare clic su **Salva**. Questa query fornirà hello necessarie autorizzazioni tooAzure Backup.

    ![Criteri di accesso del servizio di backup](./media/backup-azure-vms-encryption/save-access-policy.png)

Dopo avere fornito le autorizzazioni, è possibile procedere con l'abilitazione del backup per le VM crittografate.

## <a name="restore-encrypted-vm"></a>Ripristinare una macchina virtuale crittografata
toorestore crittografati VM, prima di utilizzare dischi di ripristinare i passaggi indicati nella sezione **ripristino backup dischi** in [ripristino configurazione di macchina virtuale scegliendo](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Successivamente, è possibile utilizzare una delle seguenti opzioni hello:
* Utilizzare i passaggi di PowerShell hello indicati in [creare una macchina virtuale da dischi ripristinati](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate completo macchina virtuale da dischi ripristinati.
* OR [Usa modello generato come parte del ripristino di dischi](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate macchine virtuali da dischi ripristinati. I modelli possono essere usati solo per i punti di recupero creati dopo il 26 aprile 2017.

## <a name="troubleshooting-errors"></a>Risoluzione dei problemi
| Operazione | Dettagli errore | Risoluzione |
| --- | --- | --- |
| Backup |Convalida non riuscita perché la macchina virtuale è crittografata con il solo BEK. I backup possono essere abilitati solo per le macchine virtuali crittografate con BEK e KEK. |Le macchine virtuali devono essere crittografate usando BEK e KEK. Prima decrittografare hello VM e crittografarla con BEK e KEK. Abilitare il backup dopo che la macchina virtuale è stata crittografata usando BEK e KEK. Altre informazioni su come è possibile [decrittografare e crittografare hello VM](../security/azure-security-disk-encryption.md)  |
| Ripristino |Non è possibile ripristinare una macchina virtuale crittografata se l'insieme di credenziali delle chiavi associato alla macchina in questione non esiste. |Creare l'insieme di credenziali delle chiavi usando [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md). Vedere l'articolo hello [ripristinare la chiave dell'insieme di credenziali chiave e il segreto tramite Azure Backup](backup-azure-restore-key-secret.md) toorestore chiave e il segreto in tal caso non presente. |
| Ripristino |Non è possibile ripristinare una macchina virtuale crittografata se chiavi e segreti associati con la macchina virtuale in questione non esistono. |Vedere l'articolo hello [ripristinare la chiave dell'insieme di credenziali chiave e il segreto tramite Azure Backup](backup-azure-restore-key-secret.md) toorestore chiave e il segreto in tal caso non presente. |
| Ripristino |Servizio di backup non dispone di autorizzazione tooaccess risorse nella sottoscrizione. |Come indicato in precedenza, ripristinare prima di tutto i dischi seguendo la procedura illustrata nella sezione **Ripristino dei dischi sottoposti a backup** in [Scelta di una configurazione di ripristino per la macchina virtuale](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Dopo aver, tale utente PowerShell troppo[creare una macchina virtuale da dischi ripristinati](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Backup | Servizio di Backup Azure non dispone di sufficienti autorizzazioni tooKey insieme di credenziali per Backup di crittografati macchine virtuali | La macchina virtuale deve essere crittografata mediante la chiave di crittografia BitLocker e la chiave di crittografia delle chiavi. In seguito, il backup deve essere abilitato.  Servizio di backup deve essere fornito queste autorizzazioni usando [i passaggi indicati nella precedente sezione hello](#provide-permissions-to-azure-backup) o utilizzando i passaggi di PowerShell indicati in hello **abilitare la protezione** sezione di hello PowerShell documentazione [tooback cmdlet AzureRM.RecoveryServices.Backup utilizzare backup di macchine virtuali](backup-azure-vms-automation.md#back-up-azure-vms). |  
