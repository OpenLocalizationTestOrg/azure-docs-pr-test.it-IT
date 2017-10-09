---
title: aaaReprotect da sito locale di Azure tooan | Documenti Microsoft
description: "Dopo il failover di macchine virtuali tooAzure, è possibile avviare un toobring failback locale tooon macchine virtuali indietro. Informazioni su come tooreprotect prima un failback."
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
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Ricrea la protezione da sito locale di Azure tooan



## <a name="overview"></a>Panoramica
Questo articolo viene descritto come tooreprotect Azure da sito locale tooan Azure le macchine virtuali. Seguire le istruzioni di hello in questo articolo, quando si è pronti toofail nuovamente le macchine virtuali VMware o i server fisici Windows/Linux dopo che hai eseguito il failover da hello locale del sito tooAzure (come descritto in [VMware replica virtuale le macchine e i server fisici tooAzure con Azure Site Recovery](site-recovery-failover.md)).

> [!WARNING]
> Non è possibile eseguire nuovamente dopo aver [completare la migrazione](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), spostare un gruppo di risorse tooanother macchina virtuale o eliminare una macchina virtuale di Azure.


Al termine di una nuova protezione e hello macchine virtuali protette sta eseguendo la replica, è possibile avviare un failback sulla hello macchine virtuali toobring li toohello nel sito locale.

Registrare commenti o domande alla fine di hello di questo articolo o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Per una rapida panoramica, guardare hello seguente video sulla modalità toofail failover da Azure tooan sito locale.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>Prerequisiti
Quando si preparano tooreprotect le macchine virtuali, richiedere o provare a hello alcune azioni preliminari seguenti:

* Se un server vCenter gestisce hello le macchine virtuali che si desidera toofail in, accertarsi di avere hello [delle autorizzazioni necessarie](site-recovery-vmware-to-azure-classic.md) per l'individuazione delle macchine virtuali nel server vCenter.

  > [!WARNING]
  > Se sono presenti hello snapshot locale master hello o destinazione macchina virtuale ha esito negativo di una nuova protezione. È possibile eliminare gli snapshot hello nella destinazione master hello prima di procedere tooreprotect. gli snapshot Hello nella macchina virtuale hello vengono uniti automaticamente durante un processo di riprotezione.

* Prima di eseguire il failback, creare due componenti aggiuntivi:

  * **Server di elaborazione**: hello [server di elaborazione](site-recovery-vmware-setup-azure-ps-resource-manager.md) riceve dati dalla macchina virtuale hello protetti in Azure e invia dati toohello nel sito locale. Una rete a bassa latenza è necessaria tra il server di elaborazione hello e macchina virtuale protetta hello. Di conseguenza, è possibile avere un server di elaborazione locale se si usa una connessione Azure ExpressRoute o un server di elaborazione basato su Azure e una VPN.
  
  * **Server di destinazione master**: il server di destinazione master hello riceve i dati di failback. server di gestione locale Hello creata dispone di un server di destinazione master installato per impostazione predefinita. A seconda di volume hello del traffico di failback, tuttavia, potrebbe essere necessario toocreate un server di destinazione master separata per il failback.
    * [Per una macchina virtuale Linux è necessario un server di destinazione master Linux](site-recovery-how-to-install-linux-master-target.md).
    * Per una macchina virtuale Windows è necessario un server di destinazione master Windows. È possibile utilizzare nuovamente hello processo master e server di destinazione computer locali.

    la destinazione master Hello ha altri prerequisiti elencati in [toocheck operazioni comuni in una destinazione master prima di riprotezione](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).

* Quando si esegue un failback, è necessario un server di configurazione locale. Durante il failback, macchina virtuale hello deve esistere nel database del server di configurazione hello. In caso contrario, il failback ha esito negativo. 

> [!IMPORTANT]
> Assicurarsi di pianificare backup regolari del server di configurazione. Se si verifica un'emergenza, ripristinare il server di hello con l'indirizzo IP stesso in modo che funzioni failback hello.

* Set hello `disk.EnableUUID=true` impostazione nei parametri di configurazione hello della macchina virtuale di destinazione master hello in VMware. Se questa riga non esiste, aggiungerla Questa impostazione è obbligatorio tooprovide un disco di macchina virtuale toohello (VMDK) UUID coerenza in modo che monta correttamente.

* *Non è possibile utilizzare vMotion di archiviazione nel server di destinazione master hello*. Ciò può provocare toofail failback hello. Impossibile avviare macchina virtuale Hello hello i dischi non sono disponibili tooit. tooprevent questo problema, escludere i server di destinazione master hello dall'elenco di vMotion.

* Aggiungere un nuovo server di destinazione master toohello unità: un'unità di conservazione. Aggiungere una nuova unità hello formato e disco.


### <a name="frequently-asked-questions"></a>Domande frequenti

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>Perché necessario una VPN S2S o un sito locale di ExpressRoute connessione tooreplicate dati toohello back?
Mentre la replica da locale tooAzure può verificarsi su hello Internet o una connessione con il peering pubblico, una nuova protezione e il failback di ExpressRoute richiedono un da sito a sito (S2S) dati tooreplicate VPN. Fornire rete hello in modo che le macchine virtuali sottoposte a failover hello in Azure può raggiungere i server di configurazione di on-premise hello (ping). È anche possibile distribuire un server di elaborazione in hello Azure rete della macchina virtuale di hello sottoposte a failover. Questo server di elaborazione deve inoltre essere in grado di toocommunicate con server di configurazione di on-premise hello.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>Quando installare un server di elaborazione in Azure


Hello le macchine virtuali in Azure che si desidera tooreprotect inviare server di elaborazione tooa dati di replica. Configurare la rete in modo che le macchine virtuali hello in Azure può raggiungere il server di elaborazione hello.

È possibile distribuire un server di elaborazione in Azure o usare hello esistente server di elaborazione usato durante il failover. tooconsider punto importante Hello è hello latenza dei dati hello toosend da hello le macchine virtuali nel server di elaborazione toohello Azure.

Se si dispone di una connessione ExpressRoute, configurare, è possibile utilizzare un locale server toosend processdataaccess perché la latenza di hello tra macchine virtuali hello e server di elaborazione hello è bassa.

 ![Diagramma dell'architettura per ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



Tuttavia, se si dispone solo di una VPN S2S, è consigliabile distribuire il server di elaborazione hello in Azure.

 ![Diagramma dell'architettura per VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


Tenere presente che la replica avviene solo tramite VPN S2S hello o hello peering della rete ExpressRoute privato. Assicurarsi che sia presente una larghezza di banda sufficiente nel canale di rete.

Per informazioni sull'installazione di un server di elaborazione basato su Azure, vedere [Gestire un server di elaborazione in esecuzione in Azure](site-recovery-vmware-setup-azure-ps-resource-manager.md).

> [!TIP]
> È consigliabile usare un server di elaborazione basato su Azure durante il failback. le prestazioni della replica Hello sono superiore se il server di elaborazione di hello è più vicino toohello la replica di macchina virtuale (macchina hello failover in Azure). Tuttavia, durante la prova di concept (POC) o dimostrazione, è possibile utilizzare server di elaborazione locale hello insieme a ExpressRoute con hello toocomplete peering privata più veloce di prova.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>Porte da aprire per i diversi componenti in modo che la riprotezione possa funzionare

![Porte per il failover e il failback](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>Server di destinazione master da usare per la riprotezione
Un server di destinazione master locale è obbligatorio tooreceive dati dal server di elaborazione hello e quindi scrivere il file VMDK della macchina virtuale locale di toohello. Se si devono proteggere macchine virtuali Windows, è necessario un server di destinazione master Windows. È possibile riutilizzare i server di elaborazione locale hello e di destinazione master<!-- !todo component -->. Per le macchine virtuali Linux, è necessario tooset di una destinazione master Linux di locali aggiuntive.


Per informazioni sull'installazione di un server di destinazione master, vedere:

* [Come Windows tooinstall master server di destinazione](site-recovery-vmware-to-azure.md)
* [Come tooinstall Linux master server di destinazione](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>I tipi di archivio dati supportati in host ESXi di hello locale durante il failback?

Supporta il ripristino del sito di Azure non riusciti attualmente, eseguire il backup solo tooa macchina virtuale file system (VMFS) o l'archivio dati rete vSAN. Un archivio dati NFS non è supportato. A causa di limitazione toothis, selezione dell'archivio dati hello in ingresso in hello riprotezione schermata è vuoto nel caso di hello di archivi dati NFS, o che mostra l'archivio dati vSAN hello ma non riesce durante il processo di hello. Se si intende toofail nuovamente, è possibile creare un archivio dati VMFS locale e non riuscire tooit indietro. Il failback causerà un download completo di hello VMDK.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>Toocheck operazioni comuni dopo aver completato l'installazione del server di destinazione master hello

* Se hello macchina virtuale è presente in locale in hello server vCenter, hello server di destinazione master deve accedere VMDK della macchina virtuale locale di toohello. L'accesso è necessario toowrite hello replicato dati toohello dischi della macchina virtuale. Verificare che l'archivio dati della macchina virtuale che hello locale sia montato in host hello master del database di destinazione con accesso in lettura/scrittura.

* Se hello virtual machine non è presente in locale nel server vCenter hello, hello servizio Site Recovery deve toocreate una nuova macchina virtuale durante una nuova protezione. Questa macchina virtuale viene creata in host ESX hello in cui si crea la destinazione master hello. Scegliere con attenzione, host ESX hello in modo che macchina virtuale di failback hello viene creata nell'host di hello che desidera.

* *Non è possibile utilizzare per il server di destinazione master hello Storage vMotion*. Ciò può provocare toofail failback hello. Impossibile avviare macchina virtuale Hello hello i dischi non sono disponibili tooit.

  > [!WARNING]
  > Se una destinazione master subisce un'attività di vMotion di archiviazione dopo una nuova protezione, dischi di macchine virtuali hello protetto destinazione master toohello collegato eseguire la migrazione di destinazione toohello hello vMotion attività. Se si tenta di toofail nuovamente in seguito, la disconnessione del disco hello non riesce perché non sono stati trovati dischi hello. Diventa quindi dischi hello toofind rigido negli account di archiviazione. È necessario toofind li manualmente e collegarli macchina virtuale toohello. Successivamente, macchina virtuale di hello locale può essere avviata.

* Aggiungere un conservazione unità tooyour esistente Windows server di destinazione master. Aggiungere una nuova unità hello formato e disco. unità di conservazione Hello è usato toostop hello punti nel tempo quando macchina virtuale hello vengono replicati toohello indietro nel sito locale. Di seguito sono elencati alcuni criteri relativi a un'unità di conservazione, Senza questi criteri, unità hello non verranno elencate per il server di destinazione master hello.

   * volume Hello non viene usato per altri scopi, ad esempio una destinazione di replica.

   * volume Hello non è in modalità di blocco.

   * volume Hello non è un volume della cache. installazione di destinazione master Hello non esiste in tale volume. volume di installazione personalizzata Hello per hello processo master e server di destinazione non è idoneo per un volume di conservazione. Quando il server di elaborazione di hello e di destinazione master vengono installati in un volume, hello è un volume della cache di destinazione master hello.

   * tipo di Hello file system del volume di hello non FAT o FAT32.

   * capacità del volume Hello è diverso da zero.

   * volume di conservazione predefinito Hello per Windows è il volume di hello R.

   * volume di conservazione predefinito Hello per Linux è /mnt/retention.

  > [!IMPORTANT]
  > Se si utilizza un computer server/configurazione del server di processo esistente o di una scala o di un processo master di server/server inviala, è necessario tooadd una nuova unità. nuova unità Hello deve soddisfare hello precedenti requisiti. Se l'unità di conservazione hello non è presente, non appare nell'elenco a discesa Selezione hello nel portale di hello. Dopo aver aggiunto una destinazione master in locale toohello unità, occupa too15 minuti per hello unità tooappear selezione hello nel portale di hello. È inoltre possibile aggiornare il server di configurazione di hello se unità hello non viene visualizzato dopo 15 minuti.

* Per una macchina virtuale Linux sottoposta a failover è necessario un server di destinazione master Linux. Per una macchina virtuale Windows sottoposta a failover è necessario un server di destinazione master Windows.

* Installare gli strumenti VMware nel server di destinazione master hello. Senza gli strumenti VMware hello, archivi dati hello in host ESXi hello master del database di destinazione non possono essere rilevato.

* Abilitare hello `disk.EnableUUID=true` parametro nella macchina virtuale di destinazione master hello utilizzando le proprietà di vCenter hello. <!-- !todo Needs link. -->

* la destinazione master Hello deve avere almeno un archivio dati VMFS associata. Se è presente nessuno, hello **Datastore** input nella pagina di riprotezione hello sarà vuota e non è possibile procedere.

* server di destinazione master Hello non possono avere snapshot su dischi hello. Se sono presenti snapshot, la riprotezione e il failback non riusciranno.

* la destinazione master Hello non può avere un controller SCSI Paravirtual. controller Hello può essere solo un controller di LSI Logic. Senza un controller LSI Logic, la riprotezione non riuscirà.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>Passaggi tooreprotect

> [!NOTE]
> Dopo l'avvio di una macchina virtuale in Azure, comporta un tempo per l'agente di hello del server di configurazione tooregister toohello indietro (verso l'alto too15 minuti). Durante questo periodo, una nuova protezione non riesce e un messaggio di errore indica che l'agente di hello non è installato. Attendere alcuni minuti e ripetere l'operazione di riprotezione.



1. In **insieme di credenziali** > **gli elementi replicati**, hello macchina virtuale in cui è stato eseguito il failover e quindi scegliere **riproteggere**. È anche possibile fare clic su hello computer e seleziona **riproteggere** dai pulsanti di comando hello.
2. Notare che direzione hello di protezione, nel pannello hello **locale tooOn Azure**, è già selezionato.
3. In **Server di destinazione Master** e **Server di elaborazione**, selezionare server di destinazione master locale hello e hello server di elaborazione.
4. Per **Datastore**, selezionare hello toowhich archivio dati si desidera toorecover hello dischi locali. Questa opzione viene utilizzata quando viene eliminata macchina virtuale locale di hello, ed è necessario toocreate nuovi dischi. Questa opzione viene ignorata se i dischi hello esistono già, ma è comunque necessario toospecify un valore.
5. Scegliere l'unità di conservazione hello.
6. criteri di failback Hello viene selezionato automaticamente.
7. Fare clic su **OK** toobegin riprotezione. Un processo inizia tooreplicate hello macchina virtuale Azure toohello nel sito locale. È possibile monitorare lo stato di avanzamento hello in hello **processi** scheda.

Se si desidera toorecover tooan percorso alternativo (quando viene eliminato macchina virtuale di hello locale), selezionare l'unità di conservazione hello e l'archivio dati che vengono configurate per il server di destinazione master hello. Quando si esegue il sito locale toohello indietro, hello VMware le macchine virtuali nel piano di protezione, hello failback utilizzare hello stesso archivio dati come hello master server di destinazione. Una nuova macchina virtuale viene quindi creata in vCenter.

Se si desidera una macchina virtuale di hello toorecover tooan Azure esistente locale macchina virtuale, hello di montaggio locale archivi dati della macchina virtuale con accesso in lettura/scrittura in host ESXi del server di destinazione master hello.
    ![Finestra di dialogo Riproteggi](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

È inoltre possibile proteggere di nuovo a livello di hello un piano di ripristino. Un gruppo di replica può essere riprotetto solo tramite un piano di ripristino. Quando ricrea la protezione tramite un piano di ripristino, è necessario valori hello tooprovide per ogni computer protetto.

> [!NOTE]
> Utilizzare hello stesso tooreprotect di server di destinazione master di un gruppo di replica. Se si utilizza un tooreprotect di server di destinazione master diverso un gruppo di replica, server hello non può fornire un punto comune nel tempo.

> [!NOTE]
> macchina virtuale di Hello locale è stata disattivata durante una nuova protezione. in modo da garantire la coerenza dei dati durante la replica. Non accendere hello macchina virtuale dopo il completamento di una nuova protezione.

Al termine di una nuova protezione hello, macchina virtuale hello verrà immesso uno stato protetto.

## <a name="next-steps"></a>Passaggi successivi

Una macchina virtuale hello ha immesso uno stato protetto, è possibile [avviare un failback](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back). 

il failback Hello verrà arrestato hello di macchina virtuale in Azure e macchina virtuale di avvio hello in locale. Prevedere tempi di inattività per un'applicazione hello. Scegliere un orario per il failback quando un'applicazione hello è in grado di tollerare i tempi di inattività.

## <a name="common-problems"></a>Problemi frequenti

* Se si utilizza un modello toocreate le macchine virtuali, assicurarsi che ogni macchina virtuale ha un proprio UUID per i dischi di hello. Se hello locale conflitti UUID della macchina virtuale con quello di destinazione master hello perché entrambi sono stati creati da hello stesso si verifica un errore di modello, una nuova protezione. Distribuire un'altra destinazione master che non è stata creata da hello stesso modello.

* Se si esegue l'individuazione di vCenter con utente di sola lettura e la protezione delle macchine virtuali, la protezione funziona e il failover viene eseguito. Durante una nuova protezione, il failover non riesce perché non possono essere individuati archivi dati hello. Il problema è che hello archivi dati non sono elencati durante una nuova protezione. tooresolve questo problema, è possibile aggiornare le credenziali di vCenter hello con un account appropriato che dispone di autorizzazioni, quindi ripetere il processo di hello. Per ulteriori informazioni, vedere [VMware replicare le macchine virtuali e server fisici tooAzure con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).

* Quando si il failback per una macchina virtuale Linux ed eseguirlo in locale, è possibile visualizzare che il pacchetto di gestione di rete hello è stato disinstallato dal computer hello. La disinstallazione si verifica perché il pacchetto di gestione di rete hello viene rimosso quando viene recuperato macchina virtuale hello in Azure.

* Quando una macchina virtuale Linux è configurata con un indirizzo IP statico e failover tooAzure, indirizzo IP hello viene acquisito da DHCP. Quando si esegue il failover tooon locale, macchina virtuale hello continua l'indirizzo IP toouse DHCP tooacquire hello. Manualmente Accedi toohello macchina e, se necessario, impostare hello tooa indietro statico indirizzo. Una macchina virtuale Windows può acquisire ancora l'IP statico.

* Se si usa l'edizione gratuita di ESXi 5.5 o di vSphere 6 Hypervisor, è possibile effettuare il failover, ma non eseguire il failback. failback tooenable, licenza di valutazione del programma di aggiornamento tooeither.

* Se è Impossibile raggiungere il server di configurazione hello dal server di elaborazione hello, utilizzare server di configurazione toohello connettività toocheck Telnet sulla porta 443. È anche possibile provare a server di configurazione tooping hello dal server di elaborazione hello. Un server di elaborazione deve essere un heartbeat quando è connesso toohello server di configurazione.

* Se si sta tentando di toofail tooan indietro alternativo vCenter, assicurarsi che la nuova vCenter e il server di destinazione master hello vengano individuati. Un tipico sintomo è che hello archivi di dati non sono accessibili o visibili in hello **riproteggere** la finestra di dialogo.

* Un server di Windows Server 2008 R2 SP1 è protetto come fisico server locale non è possibile eseguire dal sito locale tooan Azure.
