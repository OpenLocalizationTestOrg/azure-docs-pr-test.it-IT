---
title: aaaBack le macchine virtuali di Azure | Documenti Microsoft
description: Individuare, registrare e il backup dell'insieme di credenziali di macchine virtuali di Azure tooa recovery services.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup della macchina virtuale; eseguire il backup della macchina virtuale; backup e ripristino di emergenza; backup di vm di ARM
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Eseguire il backup di macchine virtuali di Azure insieme di credenziali di servizi di ripristino tooa
> [!div class="op_single_selector"]
> * [Eseguire il backup dell'insieme di credenziali di macchine virtuali tooRecovery servizi](backup-azure-arm-vms.md)
> * [Eseguire il backup dell'insieme di credenziali tooBackup macchine virtuali](backup-azure-vms.md)
>
>

In questo articolo illustra in dettaglio come insieme di credenziali tooback backup di macchine virtuali di Azure (distribuzione di gestione risorse e distribuito classica) tooa servizi di ripristino. La maggior parte del lavoro hello per il backup di macchine virtuali è preparazione hello. Prima di poter eseguire il backup o proteggere una macchina virtuale, è necessario completare hello [prerequisiti](backup-azure-arm-vms-prepare.md) tooprepare l'ambiente per la protezione delle macchine virtuali. Dopo aver completato i prerequisiti di hello, è possibile avviare gli snapshot tootake di hello operazione di backup della macchina virtuale.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

Per ulteriori informazioni, vedere gli articoli di hello in [pianificazione dell'infrastruttura di backup di VM in Azure](backup-azure-vms-introduction.md) e [macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="triggering-hello-backup-job"></a>Attivazione hello processo di backup
i criteri di backup Hello associato hello che insieme di credenziali di servizi di ripristino definiscono la frequenza e quando viene eseguito l'operazione di backup hello. Per impostazione predefinita, hello prima pianificati backup corrisponde hello iniziale. Fino a quando non si verifica il backup iniziale hello, hello ultimo stato di Backup su hello **i processi di Backup** pannello viene visualizzato come **avviso (backup iniziale in sospeso)**.

![Backup in sospeso](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

A meno che il backup iniziale è scadenza toobegin imminente, è consigliabile eseguire **Esegui backup**. Hello procedura riportata di seguito viene avviato dal dashboard di hello insieme di credenziali. Questa procedura viene utilizzato per l'esecuzione di processo di backup iniziale hello dopo aver completato tutti i prerequisiti. Se è già stato eseguito il processo di backup iniziale di hello, questa procedura non è disponibile. Hello associati criteri di backup determinano il processo di backup successivo di hello.  

toorun hello iniziale processo di backup:

1. Nel dashboard dell'insieme di credenziali hello, fare clic sul numero hello in **elementi Backup**, oppure fare clic su hello **elementi Backup** riquadro. <br/>
  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hello **elementi Backup** apre blade.

  ![Elementi di backup](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. In hello **elementi Backup** blade, elemento selezionare hello.

  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hello **elementi Backup** viene aperto l'elenco. <br/>

  ![Processo di backup attivato](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. In hello **elementi Backup** fare clic sui puntini di sospensione hello **...**  menu di scelta rapida tooopen hello.

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu.png)

  viene visualizzato il menu di scelta rapida Hello.

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Nel menu di scelta rapida hello, fare clic su **Backup ora**.

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  verrà visualizzata la finestra di Backup ora pannello Hello.

  ![Mostra pannello hello Esegui Backup](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Nel pannello Esegui Backup hello fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.

  ![impostare hello ultimo giorno hello Esegui Backup viene mantenuto un punto di ripristino](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Le notifiche di distribuzione consentono di sapere che è possibile monitorare lo stato di avanzamento hello del processo di hello nella pagina processi di Backup hello e processo di backup hello è stato attivato. A seconda delle dimensioni di hello della macchina virtuale, la creazione di backup iniziale hello potrebbe richiedere qualche minuto.

6. lo stato di hello tooview o di una traccia di backup iniziale hello, nel dashboard dell'insieme di credenziali hello in hello **i processi di Backup** fare clic su riquadro **In corso**.

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Apre il pannello di processi di Backup Hello.

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  In hello **i processi di Backup** pannello, è possibile visualizzare lo stato di hello di tutti i processi. Controllare se il processo di backup hello per la macchina virtuale è ancora in corso o ha terminato. Al termine di un processo di backup, lo stato di hello è *completato*.

  > [!NOTE]
  > Come parte dell'operazione di backup hello, hello servizio Backup di Azure esegue un'estensione di backup toohello comando in ogni macchina virtuale di tooflush tutti scrive e creare uno snapshot coerenza.
  >
  >

## <a name="troubleshooting-errors"></a>Risoluzione dei problemi
Se si verificano problemi durante il backup la macchina virtuale, vedere hello [articolo sulla risoluzione dei problemi di VM](backup-azure-vms-troubleshoot.md) per assistenza.

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato protetto della macchina virtuale, vedere hello seguente toolearn articoli sulle attività di gestione delle macchine Virtuali e come toorestore macchine virtuali.

* [Gestire e monitorare il backup delle macchine virtuali di Azure](backup-azure-manage-vms.md)
* [Ripristino di macchine virtuali](backup-azure-arm-restore-vms.md)
