---
title: aaaPrepare macchine tooset ripristino di emergenza tra aree di Azure dopo la migrazione tooAzure tramite il ripristino del sito | Documenti Microsoft
description: In questo articolo viene descritto come tooprepare macchine tooset ripristino di emergenza tra aree di Azure dopo la migrazione tooAzure tramite Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Replicare macchine virtuali di Azure tooanother area dopo la migrazione tooAzure tramite Azure Site Recovery

>[!NOTE]
> La replica di Azure Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.

## <a name="overview"></a>Panoramica

In questo articolo consente di macchine virtuali di Azure per preparare la replica tra due aree di Azure dopo che questi computer sono stati migrati da un tooAzure ambiente locale con Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Ripristino di emergenza e conformità
Oggi più le aziende stanno spostando tooAzure i carichi di lavoro. Con le aziende lo spostamento di produzione critici in locale tooAzure i carichi di lavoro, configurare il ripristino di emergenza per questi carichi di lavoro è obbligatorio per la conformità e toosafeguard contro le interruzioni in un'area di Azure.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Preparazione delle macchine migrate per la replica
tooprepare della migrazione di macchine per la configurazione di replica tooanother area di Azure:

1. Completare la migrazione.
2. Installare l'agente di Azure, se necessario hello.
3. Rimuovere il servizio di mobilità hello.  
4. Riavviare hello macchina virtuale.

Questi passaggi sono descritti in dettaglio nelle sezioni che seguono hello.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Passaggio 1: Eseguire la migrazione dei carichi di lavoro in esecuzione su macchine virtuali Hyper-V, le macchine virtuali VMware e toorun server fisici in macchine virtuali di Azure

tooset la replica di backup ed eseguire la migrazione locale Hyper-V, VMware e carichi di lavoro fisici tooAzure, seguire hello passi in hello [IaaS di Azure di eseguire la migrazione di macchine virtuali tra le aree di Azure con Azure Site Recovery](site-recovery-migrate-to-azure.md) articolo. 

Dopo la migrazione, è non necessario toocommit o eliminare un failover. Selezionare, invece, hello **completare la migrazione** opzione per ogni computer si desidera toomigrate:
1. In **elementi replicati**, fare doppio clic su hello macchina virtuale e fare clic su **completare la migrazione**. Fare clic su **OK** passaggio hello toocomplete. È possibile monitorare i progressi nelle proprietà di hello macchina virtuale mediante il monitoraggio di processo di migrazione completa hello in **i processi di ripristino del sito**.
2. Hello **completare la migrazione** azione completa il processo di migrazione hello, rimuove la replica per macchina hello e viene arrestata la fatturazione di Site Recovery per la macchina hello.

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Passaggio 2: Installare l'agente VM di Azure hello nella macchina virtuale hello
Hello Azure [agente VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) deve essere installato nella macchina virtuale hello per hello Site Recovery estensione toowork e toohelp proteggere hello macchina virtuale.

>[!IMPORTANT]
>A partire dalla versione 9.7.0.0, nelle macchine virtuali di Windows, il programma di installazione di hello mobilità servizio installa anche hello più recente disponibile agente VM di Azure. Sulla migrazione, macchina virtuale hello soddisfi i prerequisiti per l'utilizzo di qualsiasi estensione della macchina virtuale, inclusi l'estensione Site Recovery hello l'installazione dell'agente. toobe esigenze di Hello macchina virtuale di Azure agente installato manualmente solo se il servizio di mobilità installato hello hello migrazione macchina è 9,6 o versione precedente.

Hello nella tabella seguente fornisce informazioni aggiuntive sull'installazione dell'agente VM hello e convalida che è stato installato:

| **Operazione** | **Windows** | **Linux** |
| --- | --- | --- |
| L'installazione dell'agente VM hello |Scaricare e installare hello [agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). È necessario installazione hello toocomplete privilegi di amministratore. |Installare più recente hello [agente Linux](../virtual-machines/linux/agent-user-guide.md). È necessario installazione hello toocomplete privilegi di amministratore. Si consiglia di installare l'agente di hello dal proprio archivio di distribuzione. Abbiamo *non è consigliabile* installa agente VM Linux hello direttamente da GitHub.  |
| Convalida di installazione dell'agente VM hello |1. Sfoglia cartella C:\WindowsAzure\Packages toohello hello macchina virtuale di Azure. Dovrebbe essere file WaAppAgent.exe hello. <br>2. Fare clic sul file hello, andare troppo**proprietà**, quindi selezionare hello **dettagli** hello scheda **versione prodotto** campo deve essere 2.6.1198.718 o versione successiva. |N/D |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Passaggio 3: Rimuovere hello servizio di mobilità dalla hello migrazione di macchine virtuali

Se la migrazione dei computer VMware locali o dei server fisici in Windows/Linux, è necessario toomanually installazione/disinstallazione hello servizio di mobilità dalla macchina virtuale migrata hello.

>[!IMPORTANT]
>Questo passaggio non è necessario per tooAzure stata eseguita la migrazione di macchine virtuali Hyper-V.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Disinstallare il servizio di mobilità hello in una macchina virtuale di Windows Server
Utilizzare uno dei hello seguente servizio di mobilità hello toouninstall metodi in un computer Windows Server.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Disinstallare tramite l'interfaccia utente di Windows hello
1. Nel Pannello di controllo hello, selezionare **programmi**.
2. Selezionare **Microsoft Azure Site Recovery Mobility Service/Master Target server** (Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master) e fare clic su **Disinstalla**.

##### <a name="uninstall-at-a-command-prompt"></a>Disinstallare dal prompt dei comandi
1. Aprire una finestra del Prompt dei comandi come amministratore.
2. servizio di mobilità di hello di toouninstall, eseguire il comando seguente hello:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Disinstallare il servizio di mobilità hello in un computer Linux
1. Sul server Linux, accedere come utente **Root**.
2. In un terminal, andare troppo/utente/locale/ripristino automatico di sistema.
3. servizio di mobilità di hello di toouninstall, eseguire il comando seguente hello:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Passaggio 4: Riavviare hello VM

Dopo avere disinstallato il servizio di mobilità hello, riavvio hello VM prima di configurare replica tooanother area di Azure.


## <a name="next-steps"></a>Passaggi successivi
- Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).
- Altre informazioni sulle [indicazioni di connettività di rete per la replica delle macchine virtuali di Azure](site-recovery-azure-to-azure-networking-guidance.md).
