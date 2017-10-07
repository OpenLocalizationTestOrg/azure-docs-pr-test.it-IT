---
title: aaaFailback le macchine virtuali VMware da Azure tooon locale | Documenti Microsoft
description: Informazioni sulle toohello indietro nel sito locale dopo il failover di macchine virtuali VMware e server fisici tooAzure con esito negativo.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Eseguire il backup le macchine virtuali VMware e server fisici toohello nel sito locale


Questo articolo viene descritto come toofailback Azure da sito locale toohello Azure le macchine virtuali. Seguire le istruzioni di hello qui quando si è pronti toofail eseguire macchine virtuali VMware o i server fisici Windows o Linux dopo avere protetto i computer usando questo nuovo [riferimento](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Se si utilizza il portale di Azure classico di hello, consultare tooinstructions indicato [qui](site-recovery-failback-azure-to-vmware-classic.md) per l'architettura di tooAzure avanzata VMware e [qui](site-recovery-failback-azure-to-vmware-classic-legacy.md) per architettura legacy hello

## <a name="overview"></a>Panoramica
diagrammi Hello in questa sezione mostrano l'architettura di failback hello per questo scenario.

Quando si utilizza una connessione Azure ExpressRoute hello Server di elaborazione è locale, è possibile utilizzare questa architettura:

![Diagramma dell'architettura per ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Quando hello Server di elaborazione è in Azure e si dispone di una VPN o una connessione ExpressRoute, questa architettura:

![Diagramma dell'architettura per VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Per un elenco completo delle porte e diagramma dell'architettura di failback hello, vedere toohello seguente immagine:

![Failover-Failback - Elenco di tutte le porte](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Dopo aver eseguito il failover tooAzure, non si tooyour indietro nel sito locale in tre fasi:

* **Fase 1**: proteggere nuovamente hello macchine virtuali di Azure in modo che inizino a replicare le macchine virtuali VMware toohello indietro che sono in esecuzione nel sito locale.
* **Fase 2**: dopo le macchine virtuali di Azure vengono replicati tooyour nel sito locale, eseguire un failover toofail nuovamente da Azure.
* **Fase 3**: dopo che i dati ha eseguito nuovamente, si ricrea la protezione hello le macchine virtuali in locale che è stato eseguito il backup, in modo che inizino tooAzure di replica.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Non riuscire toohello indietro nel percorso originale o un percorso alternativo
Dopo aver eseguito su una VM VMware, è possibile eseguire il backup toohello stessa macchina virtuale di origine se esiste ancora locale. In questo scenario, solo i delta di hello è stati eseguiti nuovamente.

Se è stato eseguito il failover server fisici, il failback è sempre tooa nuova VM VMware. Prima di eseguire il failback di una computer fisico, ricordare che:
* Un computer fisico protetto, verrà ripristinato come una macchina virtuale quando è stato eseguito il failover da Azure tooVMware. Un computer fisico di Windows Server 2008 R2 SP1, se è protetto e il failover tooAzure, non è possibile eseguire nuovamente. Un computer Windows Server 2008 R2 SP1 che ha avviato come una macchina virtuale locale sarà in grado di toofail back.
* Verificare che almeno un server di destinazione master individuare insieme hello gli host ESX/ESXi toofail è necessario eseguire il backup per.

Se non si riesce toohello posteriore seguenti hello di macchina virtuale originale, sono necessari:

* VM hello è gestito da un server vCenter, hello host ESX della destinazione master devono avere l'archivio dati di accesso toohello macchine virtuali.
* Se hello macchina virtuale si trova in un host ESX, ma non è gestito da vCenter, disco rigido hello di hello VM deve essere in un archivio dati è accessibile dall'host del MT hello.
* Se la macchina virtuale si trova in un host ESX e non utilizza vCenter, è necessario completare l'individuazione dell'host ESX hello di hello MT prima ricrea la protezione. Questa opzione è valida anche per il failback di server fisici.
* Un'altra opzione (se hello locale esiste macchina virtuale) è toodelete prima eseguire un failback. Il failback quindi crea una nuova macchina virtuale su hello stesso host come host ESX di destinazione master hello.

Quando non è un percorso alternativo tooan indietro, dati hello sono ripristinato toohello stesso archivio dati e hello stesso host ESX utilizzato dal server di destinazione master locale hello.

## <a name="prerequisites"></a>Prerequisiti
* toofail back le macchine virtuali VMware e server fisici, è necessario un ambiente VMware. In mancanza di back-tooa server fisico non è supportata.
* toofail nuovamente, è necessario avere creato una rete di Azure quando si imposta inizialmente la protezione. Il failback richiede una connessione VPN o ExpressRoute da hello Azure rete in cui hello macchine virtuali di Azure sono toohello si trova nel sito locale.
* Se hello macchine virtuali che si desidera toofail il tooare gestiti da un server vCenter, assicurarsi di disporre di autorizzazioni hello necessario per l'individuazione delle macchine virtuali in vCenter server. Per ulteriori informazioni, vedere [VMware replicare le macchine virtuali e server fisici tooAzure con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
* Se in una macchina virtuale sono presenti snapshot, la riprotezione ha esito negativo. È possibile eliminare gli snapshot hello o dischi hello.
* Prima di eseguire il failback, creare i componenti seguenti:
  * **Creare un server di elaborazione in Azure**. Questo componente è una macchina virtuale di Azure da creare e lasciare in esecuzione durante il failback. È possibile eliminare hello VM dopo il failback è stato completato.
  * **Creare un server di destinazione master**: server di destinazione master hello Invia e riceve i dati di failback. server di gestione di Hello è creata in locale dispone di un server di destinazione master che viene installato per impostazione predefinita. A seconda di volume hello del traffico di failback, tuttavia, potrebbe essere necessario toocreate un server di destinazione master separata per il failback.
  * un server di destinazione master aggiuntive che viene eseguito su Linux, toocreate impostare hello VM Linux prima di installare il server di destinazione master hello, come descritto più avanti.
* Quando si esegue un failback, è necessario un server di configurazione locale. Durante il failback, macchina virtuale hello deve esistere nel database del server di configurazione hello. Se il database del server di configurazione hello non contiene nessuna macchina virtuale, non sarà possibile effettuare il failback. Assicurarsi pertanto di pianificare backup regolari del server. In caso di emergenza, è necessario toorestore con l'indirizzo IP stesso in modo che il failback funziona hello.
* Impostazione disk.enableUUID=true hello in **parametri di configurazione** del database master hello destinazione macchina virtuale in VMware. Se questa riga non esiste, aggiungerla Questa impostazione è obbligatorio tooprovide un file di disco (VMDK) macchina virtuale di toohello identificatore univoco universale (UUID) coerente in modo che si è installato correttamente.
* Tenere in considerazione un "Master server di destinazione non può essere archiviazione vMotioned" condizione, che può causare toofail failback hello. Hello VM non è risultata perché i dischi di hello non vengono apportati tooit disponibili.
* Aggiungere un'unità, chiamata un'unità di conservazione, nel server di destinazione master hello. Aggiungere un disco e formattare unità hello.

## <a name="failback-policy"></a>Criteri di failback
tooreplicate indietro tooon sedi locali, è necessario un criterio di failback. criteri di Hello viene creato automaticamente quando si crea un criterio di direzione in avanti, e viene associato automaticamente al server di configurazione hello. Non è modificabile. criteri di Hello sono hello seguendo le impostazioni di replica:

* Soglia RPO: 15 minuti
* Conservazione del punto di ripristino: 24 ore
* Frequenza di snapshot coerenti con l'applicazione: 60 minuti

 ![Impostazioni di replica di un criterio di failback hello](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Configurare un server di elaborazione in Azure
Installare un Server di elaborazione in Azure in modo che le macchine virtuali di Azure hello può inviare hello dati back-toohello locale server di destinazione master.

Se si protegge le macchine virtuali come risorse classiche (hello recuperato VM in Azure è una macchina virtuale che è stata creata utilizzando il modello di distribuzione classica hello), è necessario un Server di elaborazione in Azure. Se è stato ripristinato hello le macchine virtuali con Azure Resource Manager come tipo di distribuzione hello, hello Server di elaborazione necessario Gestione risorse come tipo di distribuzione hello. Hello tipo di distribuzione è selezionato per hello Azure rete virtuale che si distribuisce hello Server di elaborazione.

1. In **insieme di credenziali** > **impostazioni** > **del sito di ripristino infrastruttura** (in **gestire**) > **Server di configurazione** (in **per VMware e i computer fisici**), selezionare il server di configurazione di hello.
2. Fare clic su **Server di elaborazione**.

  ![Pulsante Server di elaborazione](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Scegliere toodeploy hello Server di elaborazione come **distribuire un Server di elaborazione in Azure il failback**.
4. Selezionare sottoscrizione hello che sono stati ripristinati hello macchine virtuali.
5. Selezionare hello rete di Azure che sono stati ripristinati hello macchine virtuali. Server di elaborazione esigenze toobe nella stessa rete in modo che hello ripristinare le macchine virtuali e hello processo Server può comunicare hello Hello.
6. Se si seleziona un *modello di distribuzione classica* di rete, creare una macchina virtuale tramite hello Azure Marketplace e quindi installare Server di elaborazione hello in essa contenuti.

 ![finestra di Hello "Aggiungi Server di elaborazione"](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Come si creano hello Server di elaborazione, prestare seguente toohello attenzione:
 * nome Hello dell'immagine di hello è *V2 Server di Microsoft Azure Site Recovery processo*. Selezionare **classico** come modello di distribuzione hello.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Hello Server di elaborazione in base toohello le istruzioni di installazione in [VMware replicare le macchine virtuali e server fisici tooAzure con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
7. Se si seleziona hello *Gestione risorse* Azure di rete, distribuire Server di elaborazione hello fornendo hello le seguenti informazioni:

  * nome Hello hello del gruppo di risorse che si desidera toodeploy hello server
  * nome Hello del server di hello
  * Un nome utente e una password per l'accesso al server toohello
  * account di archiviazione Hello che si desidera toodeploy hello server
  * subnet Hello e interfaccia di rete hello che si desidera tooconnect tooit
   >[!NOTE]
   >È necessario creare [interfaccia di rete](../virtual-network/virtual-networks-multiple-nics.md) (NIC) e selezionarlo durante la distribuzione dei Server di elaborazione hello.

    ![Immettere le informazioni nella finestra di dialogo "Aggiungi Server di elaborazione" hello](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. Fare clic su **OK**. Questa azione avvia un processo che crea una macchina virtuale di tipo distribuzione di gestione delle risorse durante l'installazione di Server di elaborazione hello. tooregister hello toohello server di configurazione, il programma di installazione di hello esecuzione all'interno di hello macchina virtuale seguendo le istruzioni hello [VMware replicare le macchine virtuali e server fisici tooAzure con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md). Viene generato anche un hello toodeploy processo Server di elaborazione.

  Hello processo Server è elencato in hello **server di configurazione** > **associata server** > **i server di elaborazione** scheda.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Hello Server di elaborazione non è visibile in **proprietà della macchina virtuale**. È visibile solo nell'hello **server** scheda nel server di gestione di hello che viene registrato. Che può richiedere 10 minuti too15 hello tooappear di Server di elaborazione.


## <a name="set-up-hello-master-target-server-on-premises"></a>Impostare hello destinazione master server locale
server di destinazione master Hello riceve i dati di failback hello. server Hello viene installato automaticamente nel server di gestione locale hello, ma se si sta failback eccessiva di dati, potrebbe essere necessario tooset di un server di destinazione master aggiuntive. tooset di uno schema sono destinate a server locale, hello seguenti:

> [!NOTE]
> tooset di un server di destinazione master in Linux, ignorare toohello nella procedura successiva. Utilizzare solo CentOS 6.6 minima del sistema operativo come hello del sistema operativo di destinazione master.

1. Se si sta configurando il server di destinazione master hello in Windows, aprire pagina avvio rapido di hello dalla macchina virtuale che si sta installando il server di destinazione master hello in hello.
2. Scaricare il file di installazione hello per la procedura guidata di installazione unificata di Azure Site Recovery hello.
3. Eseguire l'installazione di hello e, in **prima di iniziare**selezionare **aggiungere ulteriori server di elaborazione tooscale distribuzione**.
4. Creazione guidata hello completo in hello allo stesso modo, si ha quando si [configurare il server di gestione di hello](site-recovery-vmware-to-azure-classic.md). In hello **i dettagli di configurazione Server** pagina, specificare l'indirizzo IP di hello del server di destinazione master hello e immettere un hello tooaccess passphrase macchina virtuale.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Impostato come server di destinazione master hello una VM Linux
tooset di server di gestione di hello in esecuzione il server di destinazione master hello come una VM Linux, installare il sistema operativo minimo di hello 6.6 CentOS. Successivamente, recuperare gli ID SCSI hello per ogni disco rigido SCSI, installare alcuni pacchetti aggiuntivi e applicare alcune modifiche personalizzate.

#### <a name="install-centos-66"></a>Installare CentOS 6.6

1. Installare il sistema operativo minimo di hello 6.6 CentOS nel server di gestione di hello macchina virtuale. Mantenere hello ISO in un'unità DVD e hello sistema di avvio. Ignorare il test di hello media. Selezionare **inglese** come linguaggio di hello, selezionare **base dispositivi di archiviazione**, verificare che hello unità disco rigido non dispone di tutti i dati importanti, fare clic su **Sì**e ignorare tutti i dati. Immettere il nome host hello hello del server di gestione e selezionare una scheda di rete server hello.  In hello **modifica sistema** nella finestra di dialogo **connettersi automaticamente**, quindi aggiungere un indirizzo IP statico, rete e le impostazioni DNS. Specificare un fuso orario. tooaccess hello server di gestione, immettere la password radice hello.
2. Quando viene chiesto di selezionare il tipo di installazione desiderato, selezionare **creare Layout personalizzati** come partizione di hello. Fare clic su **Avanti**. Selezionare **Gratuito** e quindi fare clic su **Crea**. Creare **/**, **/var/crash** e **/home partitions** con **FS Type:** **ext4**. Creare una partizione di scambio hello come **tipo ADFS: scambio**.
3. Se vengono rilevati dispositivi preesistenti viene visualizzato un messaggio di avviso. Fare clic su **formato** unità hello tooformat con le impostazioni della partizione hello. Fare clic su **scrittura modificare toodisk** tooapply le modifiche alle partizioni di hello.
4. Selezionare **caricatore di avvio installazione** > **Avanti** caricatore di avvio tooinstall hello nella partizione radice hello.
5. Installazione di hello termine, fare clic su **riavviare**.

#### <a name="retrieve-hello-scsi-ids"></a>Recuperare gli ID SCSI hello

1. Dopo l'installazione di hello, recuperare gli ID SCSI hello per ogni disco rigido SCSI nella macchina virtuale hello. toodo arresto in tal caso, il server di gestione di hello macchina virtuale. In proprietà macchina virtuale di hello in VMware, fare clic sul movimento VM hello > **Modifica impostazioni** > **opzioni**.
2. Selezionare **Avanzate** > **Generale** e quindi fare clic su **Parametri di configurazione**. Questa opzione è disponibile quando hello macchina è in esecuzione. Per toobe opzione hello disponibili, è necessario arrestare la macchina hello.
3. Effettuare una delle seguenti hello:
 * Se hello riga **disco. EnableUUID** esiste, verificare che il valore di hello è impostato troppo**True** (maiuscole / minuscole). Se il valore di hello è già impostato tooTrue, è possibile annullare e testare il comando SCSI hello all'interno di un sistema operativo guest dopo che viene avviato.
 * Se hello riga **disco. EnableUUID** non esiste, fare clic su **Aggiungi riga**e quindi aggiungerlo con hello **True** valore. Non usare le virgolette doppie.

#### <a name="install-additional-packages"></a>Installare pacchetti aggiuntivi
Scaricare e installare pacchetti aggiuntivi.

1. Verificare che il server di destinazione master hello sia connesso toohello Internet.
2. toodownload e installare 15 pacchetti dal repository CentOS hello, eseguire questo comando: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Se il computer di origine hello si proteggono è in esecuzione Linux con un Reiser o XFS file system per il dispositivo di avvio o radice hello, scaricare e installare pacchetti aggiuntivi, come indicato di seguito:

   * \# cd /usr/local
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \# rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \# wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \# rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#YUM installare multipath di BizTalk mapper dispositivo (pacchetti nel server di destinazione master hello a percorsi multipli per tooenable obbligatorio)

#### <a name="apply-custom-changes"></a>Applicare modifiche personalizzate
Dopo aver completato i passaggi di post-installazione hello e i pacchetti hello installato, è possibile applicare le modifiche personalizzate eseguendo hello seguenti:

1. Copiare toohello binario di hello RHEL 6-64 unificata agente VM. hello toountar binario, eseguire questo comando: `tar –zxvf <file name>`.
2. autorizzazioni toogive, eseguire questo comando: `# chmod 755 ./ApplyCustomChanges.sh`.
3. Esecuzione hello seguenti script: `# ./ApplyCustomChanges.sh`. Eseguirlo una sola volta. Dopo l'operazione viene eseguita correttamente, riavviare il server di hello.

## <a name="run-hello-failback"></a>Eseguire il failback hello
### <a name="reprotect-hello-azure-vms"></a>Riproteggere hello macchine virtuali di Azure
1. In **insieme di credenziali**nella **gli elementi replicati**, hello macchina virtuale che è stato eseguito il failover e quindi scegliere **riproteggere**.
2. Nel pannello hello, è possibile vedere che direzione hello di protezione **locale tooOn Azure** è già selezionato.
3. In **Server di destinazione Master** e **Server di elaborazione**, selezionare server di destinazione master locale hello e hello Azure VM processo Server.
4. Archivio dati selezionare hello che si desidera che i dischi hello toorecover locale. Utilizzare questa opzione quando hello locale viene eliminata e non è necessario toocreate nuovi dischi. Ignorare l'opzione hello se hello dischi esistono già, ma è comunque necessario toospecify un valore.
5. Utilizzare punti hello toostop di unità di conservazione in momento hello VM è replicate indietro tooon locale. Di seguito si elencano alcuni criteri di un'unità di conservazione. Senza questi criteri, hello non sia presente per il server di destinazione master hello.

  * Il volume non deve essere in uso per altri scopi (destinazione di replica e così via).
  * Il volume non deve essere in modalità di blocco
  * Il volume non deve essere il volume della cache. (l'installazione di destinazione master hello non presenti in tale volume. Hello Server di elaborazione più master volume di installazione personalizzata di destinazione non è idoneo per volume di conservazione. In questo caso, hello installati Server di elaborazione più volume di destinazione master è il volume della cache di hello della destinazione master hello.)
  * tipo di Hello volume file system non deve essere FAT e FAT32.
  * capacità del volume Hello deve essere diverso da zero.
  * volume di conservazione predefinito Hello per Windows è il volume di R.
  * volume di conservazione predefinito Hello per Linux è /mnt/retention.

6. criteri di failback Hello viene selezionato automaticamente.
7. Dopo aver fatto clic **OK** toobegin riprotezione, un processo inizia tooreplicate hello macchina virtuale da sito locale toohello Azure. È possibile monitorare lo stato di avanzamento hello in hello **processi** scheda.

Se si desidera toorecover tooan un percorso alternativo, selezionare l'unità di conservazione hello e l'archivio dati che vengono configurate per il server di destinazione master hello. Quando si esegue il sito locale toohello indietro, hello le macchine virtuali VMware nel piano di protezione di failback hello utilizzare hello stesso archivio dati come server di destinazione master hello. Se si desidera toorecover hello replica macchina virtuale di Azure toohello stesso locale VM, hello locale VM deve già essere in hello stesso archivio dati come server di destinazione master hello. Se non è presente alcuna macchina virtuale in locale, ne viene creata una nuova durante la riprotezione.

![Selezionare "Azure tooon sedi" nel menu a discesa hello](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

È anche possibile eseguire la riprotezione a livello di piano di ripristino. Se si dispone di un gruppo di replica, è possibile riproteggerlo solo usando un piano di ripristino. Quando ricrea la protezione tramite un piano di ripristino, utilizzare i valori precedenti hello per ogni computer protetto.

> [!NOTE]
> Gruppi di replica devono essere protetti con hello stessa destinazione master. In caso di riprotezione con server di destinazione master diversi, non è possibile determinare un punto temporale.

### <a name="run-a-failover-toohello-on-premises-site"></a>Eseguire un failover toohello nel sito locale
Dopo che riproteggere hello VM, è possibile avviare un failover da Azure tooon locale.

1. Nella pagina elementi replicati hello macchina virtuale hello e quindi scegliere **Failover non pianificato**.
2. In **conferma Failover**verificare direzione del failover hello (da Azure) e quindi selezionare il punto di ripristino hello che si desidera toouse per il failover hello (hello più recente o punto di ripristino più recente coerente con l'applicazione hello). Si verifica un punto di ripristino coerenti con l'app prima punto più recente di hello nel tempo e causerà una perdita di dati.
3. Durante il failover, il ripristino del sito viene arrestato hello macchine virtuali di Azure. Dopo avere controllato che il failback è stato completato come previsto, è possibile controllare tooensure che hello macchine virtuali di Azure è state arrestate nel modo previsto.

### <a name="reprotect-hello-on-premises-site"></a>Ricrea la protezione da sito locale hello
Dopo il failback è stato completato, commit hello macchina virtuale tooensure che hello macchine virtuali recuperate in Azure vengono eliminati. toodo in tal caso, fare doppio clic su elemento hello protetti e quindi fare clic su **Commit**. Questa azione avvia un processo che rimuove hello precedente ripristinato le macchine virtuali in Azure.

Una volta completato il commit di hello, i dati devono essere nuovamente nel sito locale di hello, ma non essere protetto. tooAzure replica toostart nuovamente, hello seguenti:

1. In **insieme di credenziali**nella **impostazione** > **gli elementi replicati**, selezionare le macchine virtuali hello che non sono stato nuovamente e quindi fare clic su **riproteggere**.
2. Assegnare il valore di hello del Server di elaborazione che deve toobe utilizzato toosend dati back-tooAzure hello.
3. Fare clic su **OK**.

Una volta completata una nuova protezione hello, hello VM replica tooAzure indietro ed è possibile eseguire un failover.

### <a name="resolve-common-failback-issues"></a>Risolvere i problemi comuni di failback
* Se si esegue l'individuazione di vCenter con utente di sola lettura e la protezione delle macchine virtuali, il processo funziona e il failover viene eseguito. Durante una nuova protezione, il failover non riesce perché non possono essere individuati archivi dati hello. Come un sintomo, si noterà non archivi dati hello elencate durante una nuova protezione. tooresolve questo problema, è possibile aggiornare le credenziali di vCenter hello con un account appropriato disponga delle autorizzazioni e ritentare il processo di hello. Per ulteriori informazioni, vedere [VMware replicare le macchine virtuali e server fisici tooAzure con Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* Quando si failback una VM Linux ed eseguirlo in locale, è possibile visualizzare che il pacchetto di gestione di rete hello è stato disinstallato dal computer hello. La disinstallazione si verifica perché il pacchetto di gestione di rete hello viene rimosso quando viene recuperato hello VM in Azure.
* Quando una macchina virtuale è configurata con un indirizzo IP statico e failover tooAzure, indirizzo IP hello viene acquisito tramite DHCP. Quando si esegue il failover locale tooon indietro, hello VM continua l'indirizzo IP toouse DHCP tooacquire hello. Accedi toohello macchina e, se necessario, impostare hello tooa indietro statico indirizzo manualmente.
* Se si usa l'edizione gratuita di ESXi 5.5 o di vSphere 6 Hypervisor, sarà possibile eseguire il failover, ma non eseguire il failback. failback tooenable, licenza di valutazione del programma di aggiornamento tooeither.
* Se è Impossibile raggiungere il server di configurazione hello dal Server di elaborazione hello, controllare i server di configurazione toohello connettività da computer server di configurazione toohello Telnet sulla porta 443. È anche possibile provare a server di configurazione hello tooping dal computer Server di elaborazione hello. Un Server di elaborazione deve essere un heartbeat quando è connesso toohello server di configurazione.
* Se si sta tentando di toofail tooan indietro alternativo vCenter, assicurarsi che il nuovo vCenter venga individuato e il server di destinazione master hello inoltre viene individuato. Un tipico sintomo è che hello archivi di dati non sono accessibili o visibili in hello **riproteggere** la finestra di dialogo.
* Un computer WS2008R2SP1 è protetto come una macchina fisica locale non è possibile eseguire nuovamente da Azure tooon locale.

## <a name="fail-back-with-expressroute"></a>Eseguire il failback con ExpressRoute
È possibile eseguire il failback usando una connessione VPN o ExpressRoute. Se si desidera toouse una connessione ExpressRoute, tenere presente esempio hello:

* connessione ExpressRoute Hello deve essere configurata nella rete virtuale di Azure che failover delle macchine di origine hello tooand hello hello macchine virtuali di Azure in cui si trova dopo il failover hello.
* I dati sono replicati tooan account di archiviazione di Azure in un endpoint pubblico. toouse una connessione ExpressRoute, impostare il peering pubblico di ExpressRoute con data center di destinazione hello per la replica di Site Recovery.
