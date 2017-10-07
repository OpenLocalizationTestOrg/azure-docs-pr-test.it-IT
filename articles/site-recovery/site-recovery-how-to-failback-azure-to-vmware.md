---
title: toofail aaaHow da Azure tooVMware | Documenti Microsoft
description: "Dopo il failover di macchine virtuali tooAzure, è possibile avviare un failback toobring macchine virtuali indietro tooon locale. Informazioni sui passaggi di hello per la modalità toofail eseguire il backup."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Fail tooan Azure da sito locale

In questo articolo viene descritto come toofail eseguire il backup delle macchine virtuali da macchine virtuali di Azure toohello nel sito locale. Seguire le istruzioni hello toofail questo articolo backup di macchine virtuali VMware o i server fisici Windows/Linux dopo che hai eseguito il failover da hello locale del sito tooAzure utilizzando hello [VMware replicare le macchine virtuali e fisici tooAzure server con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) esercitazione.

> [!WARNING]
> Se dispone di [completato la migrazione](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)risorsa tooanother della macchina virtuale spostata hello gruppo o eliminato hello macchina virtuale di Azure, non è possibile eseguire il failback in seguito.

> [!NOTE]
> Se il failover delle macchine virtuali VMware non è possibile eseguire il failback tooa Hyper-v host.

## <a name="overview-of-failback"></a>Panoramica del failback
Ecco come funziona il failback. Dopo aver eseguito il failover tooAzure, non si tooyour indietro nel sito locale in alcune fasi:

1. [Riproteggere](site-recovery-how-to-reprotect.md) hello macchine virtuali in Azure, in modo che inizino tooreplicate tooVMware le macchine virtuali nel sito locale. Come parte di questo processo, è necessario:
    1. Configurare una destinazione master locale: la destinazione master Windows per le macchine virtuali Windows e la [destinazione master Linux](site-recovery-how-to-install-linux-master-target.md) per le macchine virtuali Linux.
    2. Configurare un [server di elaborazione](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Avviare la [riprotezione](site-recovery-how-to-reprotect.md). Verrà disattivare la macchina virtuale locale, hello e sincronizzare hello Azure dati della macchina virtuale con hello dischi in locale.
5. Dopo la replica da sito locale tooyour le macchine virtuali in Azure, si avvia un'esito negativo su da sito locale toohello Azure.

Dopo che i dati ha eseguito nuovamente, si ricrea la protezione hello locale le macchine virtuali non è stato, in modo che inizino tooreplicate tooAzure.

Per una rapida panoramica, guardare hello seguente video sulla modalità toofail failover da Azure tooan sito locale.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>Percorso originale o alternativo toohello indietro di esito negativo

Se è stato eseguito il failover una macchina virtuale VMware, è possibile eseguire il backup toohello stesso locale macchina virtuale di origine se è ancora presente. In questo scenario, vengono nuovamente replicate solo le modifiche di hello. Questo scenario è noto come ripristino nel percorso originale. Se non esiste una macchina virtuale locale di hello, hello risulta ripristino in un percorso alternativo.

> [!NOTE]
> È possibile solo eseguire il failback toohello originale vCenter e server di configurazione. Non è possibile distribuire un server di configurazione ed eseguire il failback usandolo. Inoltre, è possibile aggiungere un nuovo server di configurazione toohello esistente da vCenter e il failback in vCenter nuovo hello.

#### <a name="original-location-recovery"></a>Ripristino del percorso originale

Se non si riesce macchina virtuale originale toohello indietro, hello le condizioni seguenti è necessario:
* Macchina virtuale hello è gestito da un server vCenter, quindi hello host ESX della destinazione master devono avere l'archivio dati della macchina virtuale toohello di accesso.
* Se la macchina virtuale hello è in un host ESX, ma non è gestito da vCenter, quindi hello disco rigido della macchina virtuale hello deve essere in un archivio dati host di tale hello master del database di destinazione può accedere.
* Se la macchina virtuale è in un host ESX e non utilizzare vCenter, è necessario completare l'individuazione dell'host ESX hello della destinazione master hello prima ricrea la protezione. Questa opzione è valida anche per il failback di server fisici.
* È possibile eseguire il backup tooa rete di archiviazione virtuale (vSAN) o un disco basato su dispositivo raw mapping (RDM) se i dischi hello già presenti e macchina virtuale di toohello connesso in locale.

#### <a name="alternate-location-recovery"></a>Ripristino del percorso alternativo
Se non esiste alcun macchina virtuale di hello locale prima di riprotezione di macchina virtuale hello, scenario hello viene chiamato un ripristino in un percorso alternativo. flusso di lavoro riprotezione Hello crea macchina virtuale locale di hello nuovamente. Verrà anche eseguito un download completo dei dati.

* Quando non è un percorso alternativo tooan indietro, macchina virtuale hello sarà ripristinato toohello stesso host ESX in cui hello viene distribuito il server di destinazione master. Hello archivio dati che ha utilizzato il disco di hello toocreate sarà hello stesso archivio dati selezionato al momento riprotezione di macchina virtuale hello.
* È possibile eseguire nuovamente solo tooa di macchina virtuale file di sistema (VMFS) archivio dati. Con vSAN o RDM, la riprotezione e il failback avranno esito negativo.
* Riprotezione comporta un trasferimento di dati iniziale di grandi dimensioni che è seguito da modifiche hello. Questo processo esiste una macchina virtuale hello non esiste in locale. dati completi Hello devono toobe replicato di nuovo. La riprotezione impiegherà quindi più tempo rispetto al ripristino nel percorso originale.
* Non è possibile eseguire nuovamente toovSAN RDM basata o dischi. In un archivio dati VMFS è possibile creare solo nuovi dischi VMDK.

Un computer fisico, quando è stato eseguito il failover tooAzure, è possibile eseguire il backup solo di una macchina virtuale VMware (anche noto tooas P2A2V). Questo flusso rientra nel ripristino in un percorso alternativo hello.

* Un server fisico di Windows Server 2008 R2 SP1, se è protetto e il failover tooAzure, non è possibile eseguire nuovamente.
* Verificare che si scopre di almeno una destinazione master hello e server necessari host ESX/ESXi host toowhich occorre toofail nuovamente.

## <a name="have-you-completed-reprotection"></a>Verificare se la riprotezione è stata completata.
Prima di procedere, hello completo riproteggere passaggi in modo che le macchine virtuali hello in uno stato replicato, è possibile avviare un failover tooan indietro nel sito locale. Per ulteriori informazioni, vedere [come tooreprotect da Azure tooon sedi](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Prerequisiti

* Quando si esegue un failback, è necessario un server di configurazione locale. Durante il failback, macchina virtuale hello deve esistere nel database del server di configurazione hello o il failback non riuscita. Assicurarsi quindi di pianificare backup regolari del server. Se si è verificato un problema grave, sarà necessario toorestore hello server con hello stesso indirizzo IP per il failback toowork.
* server di destinazione master Hello non deve avere uno snapshot prima di attivare il failback.

## <a name="steps-toofail-back"></a>Passaggi toofail indietro

> [!IMPORTANT]
> Prima di iniziare il failback, assicurarsi di aver completato una nuova protezione di macchine virtuali hello. macchine virtuali di Hello devono trovarsi in uno stato protetto e lo stato di integrità deve essere **OK**. macchine virtuali di tooreprotect hello, leggere [come tooreprotect](site-recovery-how-to-reprotect.md).

1. In hello elementi replicati pagina, selezionare la macchina virtuale di hello e pulsante destro del mouse tooselect **Failover non pianificato**.
2. In **conferma Failover**verificare direzione del failover hello (da Azure) e quindi selezionare punto di ripristino hello (versione più recente o coerenti con l'app più recente hello) i cui toouse per il failover hello. punto consistente di Hello app si trova dietro il punto più recente di hello nel tempo e comporta una perdita di dati.
3. Durante il failover, il ripristino del sito viene arrestato hello le macchine virtuali in Azure. Dopo avere controllato che il failback è stata completata correttamente, è possibile verificare che le macchine virtuali hello in Azure è state arrestate.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>punto di ripristino toowhat è possibile eseguire le macchine virtuali indietro hello?

Durante il failback, disporre di due opzioni toofail hello backup/ripristino della macchina virtuale piano.

Se si seleziona il punto di hello più recenti elaborato nel tempo, tutte le macchine virtuali saranno sottoposte a failover tootheir più recente disponibile punto nel tempo. Nel caso in cui è presente un gruppo di replica nel piano di ripristino hello, ogni macchina virtuale hello del gruppo di replica verrà eseguito il failover tooits indipendenti ultimo punto nel tempo.

Non è possibile eseguire il failback di una macchina virtuale finché non ha almeno un punto di recupero. Non è possibile eseguire il failback di un piano di ripristino finché tutte le macchine virtuali non hanno almeno un punto di recupero.

> [!NOTE]
> Il punto di recupero più recente è un punto di recupero coerente con l'arresto anomalo.

Se si seleziona punto di ripristino coerenti con l'applicazione hello, un singola macchina virtuale di failback ripristinerà tooits ultimo punto di ripristino coerenti con l'applicazione disponibile. In caso di hello un piano di ripristino con un gruppo di replica, ogni gruppo di replica consente di ripristinare tooits punto di ripristino disponibile più comuni.
Si noti che i punti di recupero coerenti con l'applicazione possono essere indietro nel tempo e potrebbero verificarsi perdite di dati.

### <a name="what-happens-toovmware-tools-post-failback"></a>Cosa accade strumenti tooVMware post failback?

Durante il failover tooAzure, non è possibile eseguire gli strumenti VMware hello hello macchina virtuale di Azure. In caso di una macchina virtuale di Windows, ripristino automatico di sistema disabilita gli strumenti VMware hello durante il failover. In caso di macchina virtuale Linux, ripristino automatico di sistema consente di disinstallare gli strumenti VMware hello durante il failover.

Durante il failback della macchina virtuale di Windows hello, gli strumenti VMware hello vengono nuovamente abilitati al momento il failback. Analogamente, per una macchina virtuale linux, gli strumenti VMware hello vengono reinstallati computer hello durante il failback.

## <a name="next-steps"></a>Passaggi successivi

Al termine del processo di failback, è necessario toocommit hello tooensure di macchina virtuale di ripristino le macchine virtuali in Azure vengono eliminati.

### <a name="commit"></a>Commit
Commit è obbligatorio tooremove hello failover la macchina virtuale da Azure.
Fare doppio clic su elemento hello protetti e quindi fare clic su **Commit**. Un processo rimuoverà hello eseguito il failover delle macchine virtuali in Azure.

### <a name="reprotect-from-on-premises-tooazure"></a>Ricrea la protezione da locale tooAzure

Al termine del commit, la macchina virtuale in hello nel sito locale, ma non essere protetto. toostart tooreplicate tooAzure nuovamente, hello seguenti:

1. In **insieme di credenziali** > **impostazione** > **gli elementi replicati**, selezionare hello macchine virtuali che non è stato nuovamente e quindi fare clic su ** Riproteggere**.
2. Assegnare il valore di hello hello del server di elaborazione che deve toobe utilizzato toosend dati back-tooAzure.
3. Fare clic su **OK** processi di riprotezione toobegin hello.

> [!NOTE]
> Dopo l'avvio di una macchina virtuale locale, comporta un tempo per l'agente di hello del server di configurazione tooregister toohello indietro (verso l'alto too15 minuti). Durante questo periodo, riproteggere ha esito negativo e restituisce un messaggio di errore indicante che l'agente di hello non è installato. Attendere alcuni minuti e ripetere l'operazione di riprotezione.

Dopo hello riproteggere al termine del processo, macchina virtuale hello replica tooAzure indietro ed è possibile eseguire un failover.

## <a name="common-issues"></a>Problemi comuni
Assicurarsi che vCenter hello è in uno stato di connessione prima di eseguire un failback. In caso contrario, la disconnessione di dischi e collegando tali toohello indietro macchina virtuale avrà esito negativo.
