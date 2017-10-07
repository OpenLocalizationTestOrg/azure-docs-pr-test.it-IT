---
title: aaaFail nuovamente le macchine virtuali VMware da Azure nel portale classico hello | Documenti Microsoft
description: Informazioni sulle toohello indietro nel sito locale dopo il failover di macchine virtuali VMware e server fisici tooAzure con esito negativo.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Eseguire il backup le macchine virtuali VMware e server fisici toohello nel sito locale (portale classico)
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portale di Azure classico](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portale di Azure classico (Legacy)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

In questo articolo viene descritto come toofail eseguire il backup delle macchine virtuali di Azure da sito locale toohello Azure. Seguire le istruzioni di hello in questo articolo, quando si è pronti toofail nuovamente le macchine virtuali VMware o i server fisici Windows/Linux dopo che hai eseguito il failover da hello locale del sito tooAzure usando questa [esercitazione](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Panoramica
Questo diagramma mostra l'architettura di failback hello per questo scenario.

Utilizzare questa architettura quando il server di elaborazione di hello è locale e si usa ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Utilizzare questa architettura quando il server di elaborazione hello è in Azure e si dispone di una VPN o una connessione ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

elenco completo di hello toosee delle porte e diagramma architechture di failback hello vedere toohello immagine riportata di seguito

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Funzionamento del failback:

* Dopo aver eseguito il failover tooAzure, non si tooyour indietro nel sito locale in alcune fasi:
  * **Fase 1**: proteggere nuovamente hello macchine virtuali di Azure in modo che inizino a replicare le macchine virtuali tooVMware nascosto in esecuzione nel sito locale. Abilitazione di una nuova protezione Sposta hello macchina virtuale in un gruppo protezione dati di failback è stato creato automaticamente quando si originariamente creato il gruppo di protezione di hello failover. Se è stato aggiunto il piano di ripristino failover tooa gruppo protezione dati gruppo di protezione dati hello failback è stato automaticamente anche aggiunto toohello piano.  Durante la riprotezione specificare come eseguire il tooplan toofail.
  * **Fase 2**: dopo la replica da sito locale tooyour le macchine virtuali di Azure, si esegue un'esito negativo su toofail da Azure.
  * **Fase 3**: dopo che i dati ha eseguito nuovamente, si ricrea la protezione hello le macchine virtuali in locale che è stato eseguito il backup, in modo che inizino tooAzure di replica.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Il failback toohello percorso originale o alternativo
Se è stato eseguito il failover una VM VMware è possibile eseguire il backup toohello stessa macchina virtuale di origine se esiste ancora locale. In questo scenario solo le modifiche delta di hello non verranno eseguiti nuovamente. Si noti che:

* Se è stato eseguito il failover server fisici, quindi eseguire il failback è sempre tooa nuova VM VMware.
  * Prima di eseguire il failback di una computer fisico, ricordare che
  * Computer fisico protetti, verrà ripristinato come una macchina virtuale durante il failover da Azure tooVMware
  * Verificare che si scopre di almeno un server di destinazione Master insieme toowhich di host ESX/ESXi necessarie hello è necessario toofailback.
* Se non è nuovo, è necessario toohello originale VM hello segue:

  * Se hello macchina virtuale è gestito da un server vCenter host ESX di destinazione Master hello necessario archivio dati di accesso toohello macchine virtuali.
  * Se è in un host ESX hello VM ma non è gestito da vCenter quindi il disco rigido hello di hello VM deve essere in un archivio dati accessibile dall'host del MT hello.
  * Se la macchina virtuale è in un host ESX e non utilizza vCenter è necessario completare l'individuazione dell'host ESX hello di hello MT prima ricrea la protezione. Questa opzione è valida anche per il failback di server fisici.
  * Un'altra opzione (se hello locale esiste macchina virtuale) è toodelete prima eseguire un failback. Il failback verrà quindi creare una nuova macchina virtuale sulla hello stesso host come host ESX di destinazione master hello.
* Quando i dati di hello failback tooan percorso alternativo sarà ripristinato toohello stesso archivio dati e hello stesso host ESX utilizzato dal server di destinazione master locale hello.

## <a name="prerequisites"></a>Prerequisiti
* È necessario un ambiente VMware in ordine toofail le macchine virtuali VMware e di server fisici. In mancanza di back-tooa server fisico non è supportata.
* Nel toofail ordine nuovamente è necessario avere creato una rete di Azure quando si imposta inizialmente la protezione. Il failback richiede una connessione VPN o ExpressRoute da hello Azure rete in cui hello macchine virtuali di Azure sono toohello si trova nel sito locale.
* Se le macchine virtuali hello desideri tooare di back-toofail gestiti da un server vCenter, è necessario assicurarsi di che disporre delle autorizzazioni di hello necessario per l'individuazione delle macchine virtuali in vCenter server toomake. [Altre informazioni](site-recovery-vmware-to-azure-classic.md).
* Se in una macchina virtuale sono presenti snapshot la riprotezione avrà esito negativo. È possibile eliminare gli snapshot hello o dischi hello.
* Prima eseguire il failback è necessario toocreate un numero di componenti:
  * **Creare un server di elaborazione in Azure**. Si tratta di una macchina virtuale di Azure, è necessario toocreate e continuare l'esecuzione durante il failback. È possibile eliminare la macchina hello dopo aver completato il failback.
  * **Creare un server di destinazione master**: server di destinazione master hello Invia e riceve i dati di failback. server di gestione di Hello è creata in locale dispone di un server di destinazione master installato per impostazione predefinita. A seconda di volume hello del traffico di backup non riuscito, tuttavia, potrebbe essere necessario toocreate un server di destinazione master separata per il failback.
  * Se si desidera toocreate un server di destinazione master aggiuntive in esecuzione in Linux, è necessario tooset backup hello VM Linux prima di installare il server di destinazione master hello, come descritto di seguito.
* Quando si esegue un failback, è necessario un server di configurazione locale. Durante il failback, macchina virtuale hello deve esistere nel database del server Configuration hello, in mancanza di cui eseguire il failback non si abbia esito positivo. Assicurarsi pertanto di pianificare backup regolari del server. In caso di emergenza, sarà necessario toorestore con hello stesso indirizzo IP in modo che funzionino failback.

## <a name="set-up-hello-process-server-in-azure"></a>Configurare il server di elaborazione hello in Azure
È necessario tooinstall un server di elaborazione in Azure in modo da macchine virtuali di Azure hello può inviare i server di destinazione master locale tooon indietro hello dati.

1. Nel portale di Site Recovery hello > **server di configurazione** selezionare tooadd un nuovo server di elaborazione.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Specificare un nome di server di processo e immettere un nome e una password da utilizzare tooconnect toohello macchina virtuale di Azure come amministratore. In **Server di configurazione** selezionare server di gestione locale hello e specificare hello Azure in cui hello devono essere distribuiti i server di elaborazione di rete. Deve trattarsi di rete hello in cui si trovano le macchine virtuali di Azure hello. Specificare l'indirizzo IP dalla subnet selezionare hello e iniziare la distribuzione.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Verrà attivato un server di elaborazione hello toodeploy processo

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Dopo aver hello server di elaborazione viene distribuito in Azure è possibile accedere utilizzando le credenziali di hello specificato. Hello al primo accesso nella finestra di dialogo server hello processo verrà eseguito. Tipo di indirizzo IP hello hello locale del server di gestione e la passphrase. Lasciare l'impostazione della porta 443 hello. È anche possibile lasciare hello porta 9443 predefinita per la replica dei dati a meno che non specificamente modificato questa impostazione quando si configura server di gestione locale hello.

   > [!NOTE]
   > server Hello non saranno visibili in **proprietà della macchina virtuale**. È visibile solo in hello **server** scheda hello toowhich di server di gestione è stato registrato. Può richiedere circa 10-15 minuti per hello processo server tooappear.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Impostare hello destinazione master server locale
server di destinazione master Hello riceve i dati di failback hello. Un server di destinazione master viene installato automaticamente nel server di gestione locale hello ma sta failback una grande quantità di dati, potrebbe essere necessario tooset di un server di destinazione master aggiuntive. Procedere come segue:

> [!NOTE]
> Se si desidera tooinstall un server di destinazione master in Linux, seguire le istruzioni hello nella procedura successiva hello.
>
>

1. Se si installa il server di destinazione master hello in Windows, aprire pagina avvio rapido hello da hello macchina virtuale in cui si sta installando il server di destinazione master hello e scaricare i file di installazione hello per la procedura guidata di installazione unificata di Azure Site Recovery hello.
2. Eseguire l'installazione e nella **prima di iniziare** selezionare **aggiungere processo aggiuntivo server tooscale distribuzione**.
3. Creazione guidata hello completo in hello allo stesso modo, si ha quando si [configurare il server di gestione di hello](site-recovery-vmware-to-azure-classic.md). In hello **i dettagli di configurazione Server** , specificare l'indirizzo IP di hello del server di destinazione master e un hello tooaccess passphrase macchina virtuale.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Impostato come server di destinazione master hello una VM Linux
tooset di server di gestione di hello in esecuzione il server di destinazione master hello come una macchina virtuale, occorre tooinstall hello cento Linux) 6.6 S minima del sistema operativo, recuperare gli ID SCSI hello per ogni disco rigido SCSI, installare alcuni pacchetti aggiuntivi e applicare alcune modifiche personalizzate.

#### <a name="install-centos-66"></a>Installare CentOS 6.6
1. Installare il sistema operativo minimo di hello 6.6 CentOS nel server di gestione di hello macchina virtuale. Mantenere hello ISO in un sistema di hello avvio e l'unità DVD. Ignora hello media test, selezionare l'inglese alla lingua hello, selezionare **base dispositivi di archiviazione**, verificare che hello unità disco rigido non dispone di tutti i dati importanti e fare clic su **Sì**, rimuovere tutti i dati. Immettere il nome host hello hello del server di gestione e selezionare la scheda di rete server hello.  In hello **modifica sistema** finestra di dialogo selezionare * * connettersi automaticamente * * e aggiungere un indirizzo IP statico, rete e le impostazioni DNS. Specificare un fuso orario e un server di gestione radice password tooaccess hello.
2. Quando richiesto il tipo di installazione hello si desidera selezionare **creare Layout personalizzati** come partizione di hello. Dopo aver fatto clic su **Avanti** select **Gratuito** e fare clic su Crea. Creare **/**, **/var/crash** e **/home partitions** con **FS Type:** **ext4**. Creare una partizione di scambio hello come **tipo ADFS: scambio**.
3. Se vengono rilevati dispositivi preesistenti viene visualizzato un messaggio di avviso. Fare clic su **formato** unità hello tooformat con le impostazioni della partizione hello. Fare clic su **scrittura modificare toodisk** tooapply le modifiche alle partizioni di hello.
4. Selezionare **caricatore di avvio installazione** > **Avanti** caricatore di avvio tooinstall hello nella partizione radice hello.
5. Al termine dell'installazione, fare clic su **Riavvia**.

#### <a name="retrieve-hello-scsi-ids"></a>Recuperare gli ID SCSI hello
1. Dopo l'installazione di recuperare gli ID SCSI hello per ogni disco rigido SCSI nella macchina virtuale hello. toodo questo Arresta il server di gestione di hello macchina virtuale, nell'hello VM proprietà in VMware, fare clic sulla voce VM hello > **Modifica impostazioni** > **opzioni**.
2. Selezionare **Avanzate** > **Generale** e fare clic su **Parametri di configurazione**. Questa opzione sarà de-active quando hello macchina è in esecuzione. toomake it hello active macchina deve essere arrestata.
3. Se hello riga **disco. EnableUUID** esiste assicurarsi hello è impostato troppo**True** (maiuscole / minuscole). Se è già è possibile annullare e testare il comando SCSI hello all'interno di un sistema operativo guest dopo che viene avviato.
4. Se la riga hello non esistente fare clic su **Aggiungi riga** – e aggiungerla con hello **True** valore. Non usare le virgolette doppie.

#### <a name="install-additional-packages"></a>Installare pacchetti aggiuntivi
Si sarà necessario toodownload e installare alcuni pacchetti aggiuntivi.

1. Verificare che il server di destinazione master hello sia connesso toohello internet.
2. Eseguire toodownload questo comando e installare i 15 pacchetti dal repository CentOS hello: **yum # installare – y xfsprogs perl lsscsi rsync wget kexec-strumenti**.
3. Se si proteggono macchine di origine hello sono in esecuzione Linux wit Reiser XFS del file system per la radice di hello o avviare dispositivo, allora è necessario scaricare e installare pacchetti aggiuntivi, come indicato di seguito:

   * # <a name="cd-usrlocal"></a>cd /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Applicare modifiche personalizzate
Eseguire hello seguenti modifiche personalizzate tooapply dopo avere acquisito i passaggi di post-installazione completa di hello e i pacchetti hello installati:

1. Copiare toohello binario di hello RHEL 6-64 unificata agente VM. Eseguire questo comando toountar hello binario: **tar – zxvf<file name>**
2. Autorizzazioni di toogive questo comando di esecuzione: **# chmod 755./ApplyCustomChanges.sh**
3. Eseguire script hello: **./ApplyCustomChanges.sh #**. È consigliabile eseguire solo script hello, una volta. Riavviare il server di hello dopo hello script viene eseguito correttamente.

## <a name="run-hello-failback"></a>Eseguire il failback hello
### <a name="reprotect-hello-azure-vms"></a>Riproteggere hello macchine virtuali di Azure
1. Nel portale di Site Recovery hello > **macchine** scheda selezionare hello macchina virtuale che è stato eseguito il failover e fare clic su **riproteggere**.
2. In **Server di destinazione Master** e **Server di elaborazione** selezionare server di destinazione master locale hello e server di elaborazione hello macchina virtuale di Azure.
3. Selezionare l'account di hello che è configurato per la connessione toohello macchina virtuale.
4. Selezionare versione failback hello del gruppo protezione dati hello. Se, ad esempio hello macchina virtuale è protetta in PG1, è necessario tooselect PG1_Failback.
5. Se si desidera toorecover tooan un percorso alternativo, selezionare l'unità di conservazione hello e l'archivio dati configurato per il server di destinazione master hello. Quando non si toohello indietro locale sito hello le macchine virtuali VMware nel piano di protezione di failback hello utilizzerà hello stesso archivio dati come server di destinazione master hello. Se si desidera toorecover hello replica macchina virtuale di Azure toohello stesso locale VM hello locale VM deve già essere in hello stesso archivio dati come hello master server di destinazione. Se non è presente alcuna macchina virtuale in locale, ne viene creata una nuova durante la riprotezione.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Dopo aver fatto clic **OK** toobegin riprotezione un processo inizia tooreplicate hello macchina virtuale da sito locale toohello Azure. È possibile monitorare lo stato di avanzamento hello in hello **processi** scheda.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Eseguire un failover toohello nel sito locale
Dopo hello nuova VM spostata toohello failback versione del gruppo protezione dati e viene aggiunto automaticamente il piano di ripristino toohello utilizzato per hello failover tooAzure se è presente.

1. In hello **piani di ripristino** piano di ripristino selezionare hello pagina contenente il gruppo di failback hello e fare clic su **Failover** > **Failover non pianificato**.
2. In **conferma Failover** controllare la direzione del failover hello (tooAzure) e selezionare il punto di ripristino hello da toouse per il failover hello (versione più recente). Se è stata abilitata **Multi-VM** durante la configurazione delle proprietà di replica è possibile ripristinare app più recente toohello o un punto di ripristino coerenti con l'arresto anomalo del sistema. Fare clic su hello segno di spunta toostart hello failover.
3. Durante il failover, il ripristino del sito verrà arrestato hello macchine virtuali di Azure. Dopo aver verificato che il failback completata come previsto, è possibile per controllare tale hello che macchine virtuali di Azure è state arrestate nel modo previsto.

### <a name="reprotect-hello--on-premises-site"></a>Ricrea la protezione da sito locale hello
Il failback al termine dei dati saranno in hello nel sito locale, ma non protetto. tooAzure replica toostart nuovamente hello seguenti:

1. Nel portale di Site Recovery hello > **macchine** hello selezionare le macchine virtuali non sono stato nuovamente e fare clic su scheda **riproteggere**.
2. Dopo aver verificato che tooAzure replica funziona come previsto, è possibile eliminare hello macchine virtuali di Azure (attualmente non è in esecuzione) che non sono state nuovamente in Azure.

### <a name="common-issues-in-failback"></a>Problemi comuni di failback
1. Se si esegue l'individuazione di vCenter con utente di sola lettura e la protezione delle macchine virtuali, il processo funziona e il failover viene eseguito. In fase di hello di Riprotezione, non riuscirà perché non possono essere individuati archivi dati hello. Come un sintomo non si vedranno archivi dati hello elencati proteggendo nuovamente. tooresolve, è possibile aggiornare le credenziali di hello vCenter con l'account appropriato che dispone delle autorizzazioni e ritentare il processo di hello. [Altre informazioni](site-recovery-vmware-to-azure-classic.md)
2. Quando si failback una VM Linux ed eseguirlo in locale, verrà visualizzato il pacchetto di gestione di rete hello viene disinstallato dal computer hello. Questo avviene perché quando viene recuperato il hello VM in Azure, il pacchetto di gestione di rete hello viene rimosso.
3. Quando una macchina virtuale è configurata con l'indirizzo IP statico e failover tooAzure, indirizzo IP hello viene acquisito tramite DHCP. Quando si esegue il failover locale tooOn indietro, hello VM continua l'indirizzo IP toouse DHCP tooacquire hello. Sarà necessario accesso toomanually macchina hello e l'indirizzo IP di hello set di backup tooStatic indirizzo se necessario.
4. Se si usa l'edizione gratuita di ESXi 5.5 o di vSphere 6 Hypervisor, sarà possibile effettuare il failover, ma non eseguire il failback. Sarà possibile devono tooupgrade tooeither licenza di valutazione tooenable failback.

## <a name="failing-back-with-expressroute"></a>Eseguire il failback con ExpressRoute
È possibile eseguire il failback usando una connessione VPN o Azure ExpressRoute. Se si desidera seguente hello nota di toouse ExpressRoute:

* ExpressRoute deve essere configurate in hello rete virtuale di Azure toowhich origine failover macchine su e in cui le macchine virtuali di Azure si trovano dopo il failover hello.
* I dati sono replicati tooan account di archiviazione di Azure in un endpoint pubblico. È necessario configurare peering pubblico di ExpressRoute con hello destinazione data center per il ripristino del sito replica toouse ExpressRoute.
