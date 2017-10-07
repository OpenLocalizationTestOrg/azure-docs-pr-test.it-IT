---
title: aaaOverview degli insiemi di credenziali di servizi di ripristino | Documenti Microsoft
description: Una panoramica e un confronto tra gli insiemi di credenziali di Servizi di ripristino e gli insiemi di credenziali di Backup di Azure.
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Panoramica di insiemi di credenziali di Servizi di ripristino

Questo articolo descrive le funzionalità di hello di un insieme di credenziali di servizi di ripristino. Un insieme di credenziali di Servizi di ripristino è un'entità di archiviazione di Azure che ospita i dati. dati Hello sono in genere le copie di dati o informazioni di configurazione per macchine virtuali (VM), i carichi di lavoro, server o workstation. Un insieme di credenziali di servizi di ripristino è una versione di hello Gestione risorse di un insieme di credenziali di Backup. Microsoft incoraggia gli archivi di servizi di ripristino toouse e tooconvert insiemi di credenziali di servizi tooRecovery insiemi di credenziali di qualsiasi Backup.

## <a name="what-is-a-recovery-services-vault"></a>Informazioni sull'insieme di credenziali di Servizi di ripristino

Un insieme di credenziali di servizi di ripristino è che un'entità di archiviazione online in Azure utilizzata toohold dati, ad esempio copie di backup, i punti di ripristino e i criteri di backup. È possibile utilizzare i dati di backup toohold gli insiemi di credenziali di servizi di ripristino per diversi servizi di Azure, ad esempio le macchine virtuali IaaS (Linux o Windows) e database SQL di Azure. Gli insiemi di credenziali di Servizi di ripristino supportano System Center DPM, Windows Server, server di Backup di Azure e altro ancora. Gli archivi di servizi di ripristino rendono tooorganize semplice ai dati di backup, riducendo l'overhead di gestione.

All'interno di una sottoscrizione di Azure è possibile creare un numero qualsiasi di insiemi di credenziali di Servizi di ripristino.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Confronto tra gli insiemi di credenziali di Servizi di ripristino e gli insiemi di credenziali di Backup

Gli archivi di servizi di ripristino basati su modello di gestione risorse di Azure hello di Azure, mentre gli insiemi di credenziali di Backup sono basate sul modello di gestione di servizi di Azure hello. Quando si aggiorna un archivio di Backup dell'insieme di credenziali tooa servizi di ripristino, i dati di backup hello rimangono durante e dopo il processo di aggiornamento hello. Gli insiemi di credenziali di Servizi di ripristino offrono le funzionalità non disponibili per gli insiemi di credenziali di Backup, ad esempio:

- **Dati di backup sicura toohelp funzionalità avanzati**: insiemi di credenziali con servizi di ripristino, Backup di Azure fornisce sicurezza i backup nel cloud tooprotect funzionalità. Queste funzionalità di sicurezza garantiscono la protezione dei backup e ripristinano i dati in modo sicuro dai backup nel cloud anche se i server di produzione e di backup vengono compromessi. [Altre informazioni](backup-azure-security-feature.md)

- **Monitoraggio centralizzato per l'ambiente IT ibrido**: con gli insiemi di credenziali di Servizi di ripristino, è possibile monitorare non solo le [macchine virtuali IaaS di Azure](backup-azure-manage-vms.md) ma anche le [risorse locali](backup-azure-manage-windows-server.md#manage-backup-items) da un portale centrale. [Altre informazioni](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **Controllo degli accessi in base al ruolo o RBAC** : il controllo degli accessi in base al ruolo consente un controllo della gestione degli accessi con granularità fine in Azure. [Azure fornisce diversi ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md), e il Backup di Azure ha tre [punti di ripristino di ruoli predefiniti toomanage](backup-rbac-rs-vault.md). Gli archivi di servizi di ripristino sono compatibili con RBAC, che limita i backup e ripristino accesso toohello definito set di ruoli utente. [Altre informazioni](backup-rbac-rs-vault.md)

- **Protezione di tutte le configurazioni delle macchine virtuali di Azure**: gli insiemi di credenziali di Servizi di ripristino proteggono le macchine virtuali basate su Resource Manager tra cui i dischi Premium, i dischi gestiti e le macchine virtuali crittografate. L'aggiornamento di un tooa insieme di credenziali di Backup servizi di ripristino archivio offre hello opportunità tooupgrade le macchine virtuali basate su gestione di tooResource macchine virtuali basate su Service Manager. Durante l'aggiornamento dell'insieme di credenziali di hello, è possibile mantenere i punti di ripristino della macchina virtuale basata su Service Manager e configurare la protezione per hello aggiornato di macchine virtuali (abilitato per Resource Manager). [Altre informazioni](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **Ripristino immediato per le macchine virtuali IaaS**: insiemi di credenziali di servizi di ripristino utilizzando, è possibile ripristinare file e cartelle da una VM IaaS senza ripristinare hello intera macchina virtuale, che consente di tempi di ripristino. Il ripristino immediato per le macchine virtuali IaaS è disponibile sia per le macchine virtuali Windows che Linux. [Altre informazioni](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Gestione degli archivi i servizi di ripristino nel portale di hello
Creazione e la gestione degli insiemi di credenziali di servizi di ripristino nel portale di Azure hello è semplice perché hello servizio di Backup è integrato nel pannello delle impostazioni di Azure hello. Questa integrazione significa che è possibile creare o gestire un insieme di credenziali di servizi di ripristino *nel contesto di hello del servizio di destinazione hello*. Ad esempio punti di ripristino di hello tooview per una macchina virtuale, selezionarla e fare clic su **Backup** nel pannello impostazioni hello. verrà visualizzata la VM toothat specifico di Hello informazioni di backup. Nel seguente esempio, hello **ContosoVM** hello nome della macchina virtuale hello. **ContosoVM demovault** nome hello di hello insieme di credenziali di servizi di ripristino. Non è necessario il nome hello tooremember dell'insieme di credenziali di servizi di ripristino hello che archivia i punti di ripristino hello, è possibile accedere a queste informazioni dalla macchina virtuale hello.  

![Macchina virtuale con i dettagli dell'insieme di credenziali dei servizi di ripristino](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Se più server sono protetti mediante hello insieme di credenziali di servizi di ripristino stesso, potrebbe essere più logico toolook in hello che insieme di credenziali di servizi di ripristino. È possibile cercare tutti gli archivi di servizi di ripristino nella sottoscrizione hello e sceglierne uno dall'elenco di hello.

Hello nelle sezioni seguenti contengono collegamenti tooarticles che illustrano come toouse servizi di ripristino di un insieme di credenziali in ogni tipo di attività.

### <a name="back-up-data"></a>Dati di backup
- [Backup di una macchina virtuale di Azure](backup-azure-vms-first-look-arm.md)
- [Backup di Windows Server o della workstation di Windows](backup-try-azure-backup-in-10-mins.md)
- [Eseguire il backup di DPM i carichi di lavoro tooAzure](backup-azure-dpm-introduction.md)
- [Preparare tooback dei carichi di lavoro tramite il Server di Backup di Azure](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>Gestire i punti di ripristino
- [Gestire i backup delle macchine virtuali di Azure](backup-azure-manage-vms.md)
- [Gestione di file e cartelle](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Ripristinare i dati dall'insieme di credenziali hello
- [Ripristinare singoli file da una macchina virtuale di Azure](backup-azure-restore-files-from-vm.md)
- [Ripristinare una macchina virtuale di Azure](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>Insieme di credenziali hello sicura
- [Protezione dei dati di backup cloud negli insiemi di credenziali di Servizi di ripristino](backup-azure-security-feature.md)



## <a name="next-steps"></a>Passaggi successivi
Utilizzare hello articolo per la seguente:</br>
[Eseguire il backup di una macchina virtuale IaaS](backup-azure-arm-vms-prepare.md)</br>
[Eseguire il backup del server di Backup di Azure](backup-azure-microsoft-azure-backup.md)</br>
[Eseguire il backup di Windows Server](backup-configure-vault.md)
