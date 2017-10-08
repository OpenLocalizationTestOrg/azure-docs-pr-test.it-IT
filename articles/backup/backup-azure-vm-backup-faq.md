---
title: domande frequenti su Backup di VM aaaAzure | Documenti Microsoft
description: "Risposte alle domande toocommon sul: la modalità di funzionamento di backup di macchina virtuale di Azure, limitazioni e le conseguenze quando toopolicy modifiche si verificano"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: backup di macchine virtuali di Azure, ripristino di macchine virtuali di Azure, criteri di backup
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Domande su hello servizio Backup di VM di Azure
In questo articolo ha risposte toocommon domande toohelp comprendere rapidamente i componenti di Backup di Azure VM hello. In alcune delle risposte hello, sono disponibili articoli toohello collegamenti con informazioni complete. È anche possibile pubblicare domande sul servizio Azure Backup hello in hello [forum di discussione](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurare il backup
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Gli insiemi di credenziali di Servizi di ripristino supportano le macchine virtuali in modalità classica o quelle basate su Resource Manager? <br/>
Gli insiemi di credenziali di Servizi di ripristino supportano entrambi modelli.  È possibile eseguire il backup di una macchina virtuale classica (creato nel portale classico hello) o un tooa di VM Resource Manager (creato nel portale di Azure hello) dell'insieme di credenziali di servizi di ripristino.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Quali configurazioni non sono supportate da servizio Backup delle macchine virtuali di Azure?
Vedere i [sistemi operativi supportati](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) e le [limitazioni del backup di macchine virtuali](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm).

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Perché non è possibile visualizzare la macchina virtuale nella configurazione guidata del backup?
Nella configurazione guidata del backup, Backup di Azure elenca soltanto le macchine virtuali che:
* Non è già protetto, è possibile verificare lo stato del backup hello di una macchina virtuale passando tooVM blade e il controllo sullo stato di Backup dal Menu impostazioni del pannello hello. Altre informazioni su come troppo[controllare lo stato del backup di una macchina virtuale](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* Appartiene toosame area come macchina virtuale

## <a name="backup"></a>Backup
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>Il processo di backup su richiesta seguirà la stessa pianificazione di conservazione dei backup pianificati?
No. Periodo di mantenimento hello toospecify è necessario per un processo di backup su richiesta. Per impostazione predefinita, i backup attivati dal portale vengono conservati per 30 giorni. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>Di recente è stata abilitata la Crittografia dischi di Azure in alcune macchine virtuali. I backup continueranno toowork?
Sono necessarie autorizzazioni di toogive per Azure Backup service tooaccess insieme di credenziali chiave. Per concedere tali autorizzazioni in PowerShell, è possibile seguire la procedura descritta nella sezione relativa all'*abilitazione del backup* nella documentazione di [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>Eseguita la migrazione di dischi di dischi di toomanaged una macchina virtuale. I backup continueranno toowork?
Sì, i backup si integrano completamente e non toore necessità-configurare il backup. 

## <a name="restore"></a>Ripristino
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Come scegliere tra il ripristino dei dischi e il ripristino completo della macchina virtuale?
Il ripristino completo di una macchina virtuale di Azure è un modo per avere un'opzione di creazione rapida per la macchina virtuale ripristinata. Ripristinare una macchina virtuale modifica i nomi di hello dei dischi, contenitori di dischi, gli indirizzi IP pubblici, l'interfaccia di rete i nomi utilizzati per l'univocità delle risorse di recupero creati come parte della creazione della macchina virtuale. Verranno inoltre aggiunti non hello VM tooavailability set. 

Usare i dischi di ripristino per eseguire queste operazioni:
* Personalizzare hello macchina virtuale che viene creato dal punto di configurazione di tempo, ad esempio la modifica delle dimensioni di hello dalla configurazione del backup
* Aggiungere le configurazioni di cui non sono presenti al momento di hello del backup 
* Convenzione di denominazione controllo hello per le risorse create recupero
* Aggiungere VM tooavailability set
* Avere una configurazione che è possibile ottenere soltanto usando PowerShell o la definizione di un modello dichiarativo.

## <a name="manage-vm-backups"></a>Gestire i backup delle macchine virtuali
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>Cosa accade quando si modificano criteri di backup in una o più macchine virtuali?
Quando un nuovo criterio viene applicato in macchine virtuali, pianificazione e alla conservazione dei nuovi criteri hello verrà seguite. Se viene estesa memorizzazione, punti di ripristino esistenti verranno contrassegnati tookeep loro in base ai nuovi criteri. Se conservazione viene ridotto, vengono contrassegnate per l'eliminazione nel processo di pulizia successivo hello e verranno eliminate. 
