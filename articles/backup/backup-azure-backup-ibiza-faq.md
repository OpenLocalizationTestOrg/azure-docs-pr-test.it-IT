---
title: domande frequenti sull'insieme di credenziali di servizi aaaRecovery | Documenti Microsoft
description: Questa versione di hello domande frequenti su supporta la versione di anteprima pubblica hello di hello servizio Azure Backup. Le risposte toofrequently domande frequenti sull'agente di backup hello, backup e conservazione, ripristino, sicurezza e altre domande comuni su hello soluzione di Backup di Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: soluzione di backup; servizio di backup
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Insieme di credenziali di Servizi di ripristino: domande frequenti
Questo articolo fornisce l'insieme di credenziali di informazioni specifiche tooRecovery Services e integra hello [domande frequenti su Backup di Azure](backup-azure-backup-faq.md). Hello domande frequenti su Backup di Azure fornisce set completo di hello di domande e risposte su hello servizio Azure Backup.  

È possibile porre domande su Backup di Azure in hello Disqus sezione di questo articolo o di un articolo correlato. È anche possibile pubblicare domande sul servizio Azure Backup hello in hello [forum di discussione](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Gli insiemi di credenziali di Servizi di ripristino sono basati su Resource Manager. Gli insiemi di credenziali di Backup (modalità classica) sono ancora supportati? <br/>
Sì, gli insiemi di credenziali di Backup sono ancora supportati. Creare gli insiemi di credenziali di Backup in hello [portale classico](https://manage.windowsazure.com). Creare gli insiemi di credenziali di servizi di ripristino in hello [portale di Azure](https://portal.azure.com). Tuttavia è consigliabile si toocreate recovery services insieme di credenziali come tutti i futuri miglioramenti sarà disponibile solo nell'insieme di credenziali di servizi di ripristino.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>È possibile eseguire la migrazione un archivio di servizi di ripristino di Backup dell'insieme di credenziali tooa? <br/>
Purtroppo, non al momento non è possibile migrare hello contenuto di un tooa insieme di credenziali di Backup che dell'insieme di credenziali di servizi di ripristino. Questa funzionalità verrà presto aggiunta, ma non è disponibile nell'anteprima pubblica.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Gli insiemi di credenziali di Servizi di ripristino supportano le macchine virtuali in modalità classica o quelle basate su Resource Manager? <br/>
Gli insiemi di credenziali di Servizi di ripristino supportano entrambi modelli.  È possibile eseguire il backup di una macchina virtuale creata nel portale classico di hello (che si trovano le macchine virtuali in modalità classica) o una macchina virtuale creato nel portale di Azure, che sono Gestione risorse di base, hello servizi di ripristino tooa insieme di credenziali.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>È stato eseguito il backup delle macchine virtuali in modalità classica nell'insieme di credenziali per il backup. Ora si desidero toomigrate macchine virtuali dalla modalità di gestione tooResource modalità classica.  Come è possibile eseguirne il backup nell'insieme di credenziali di Servizi di ripristino?
I backup di macchine virtuali classiche nell'insieme di credenziali di backup non verranno migrato automaticamente toorecovery services insieme di credenziali durante la migrazione di macchine virtuali hello da tooResource classico in modalità di gestione. Per la migrazione di backup di macchine virtuali, seguire questa procedura:

1. Nell'insieme di credenziali backup andare troppo**elementi protetti** e selezionare hello macchina virtuale. Fare clic su [Arresta protezione](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Lasciare *deselezionata* l'opzione **Elimina i dati di backup associati**.
2. In hello [portale di Azure](https://portal.azure.com), visitare toohello **estensioni** menu per hello VM e disinstallare hello **VMSnapshot/VMSnapshotLinux** estensione.
3. Eseguire la migrazione di macchine virtuali hello dalla modalità di gestione tooResource modalità classica. Assicurarsi che archiviazione e rete corrispondente macchina toovirtual siano anche modalità Manager tooResource migrati.
4. Creare un insieme di credenziali di servizi di ripristino e configurare i backup su hello migrazione macchina virtuale utilizzando **Backup** azione nella parte superiore del dashboard dell'insieme di credenziali. Altre informazioni su come troppo[abilitare il backup nell'archivio di servizi di ripristino](backup-azure-vms-first-look-arm.md)
