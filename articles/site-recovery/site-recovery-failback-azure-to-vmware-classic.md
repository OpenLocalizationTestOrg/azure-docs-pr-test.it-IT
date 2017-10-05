---
title: Eseguire il failback di una macchina virtuale VMware da Azure nel portale classico | Documentazione Microsoft
description: Informazioni sul failback nel sito locale dopo il failover dei server fisici e delle macchine virtuali VMware in Azure.
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
ms.openlocfilehash: 82d5eb7fd13b1e9700a3e9bc2d30775e9c129749
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-to-the-on-premises-site-classic-portal"></a>Eseguire il failback di server fisici e macchine virtuali VMware nel sito locale (portale classico)
> [!div class="op_single_selector"]
> * [portale di Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portale di Azure classico](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portale di Azure classico (legacy)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Questo articolo descrive come eseguire il failback di macchine virtuali di Azure da Azure al sito locale. Seguire le istruzioni riportate in questo articolo per eseguire il failback delle macchine virtuali VMware o dei server fisici Windows/Linux dopo aver eseguito il failover dal sito locale in Azure seguendo questa [esercitazione](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Overview
Questo diagramma illustra l'architettura di failback per questo scenario.

Usare questa architettura quando il server di elaborazione è locale e si usa ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Usare questa architettura quando il server di elaborazione è in Azure e si dispone di una rete VPN o di una connessione ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Per vedere l'elenco completo delle porte e il diagramma che illustra l'architettura di failback, fare riferimento all'immagine sotto

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Funzionamento del failback:

* Dopo aver eseguito il failover in Azure, eseguire il failback nel sito locale procedendo come segue:
  * **Fase 1**: abilitare la riprotezione delle VM di Azure in modo che inizino la replica nelle macchine virtuali di VMware in esecuzione nel sito locale. Abilitando la riprotezione le macchine virtuali vengono spostate in un gruppo di protezione di failback creato automaticamente al momento della creazione del gruppo di protezione di failover originario. Se il gruppo di protezione di failover è stato aggiunto a un piano di ripristino, anche il gruppo di protezione di failback è stato aggiunto automaticamente al piano.  Durante la riprotezione viene specificato come pianificare il failback.
  * **Fase 2**: dopo la replica delle VM di Azure nel sito locale, eseguire un failover per il failback da Azure.
  * **Fase 3**: dopo aver eseguito il failback dei dati, abilitare la riprotezione delle macchine virtuali locali in cui è stato eseguito il failback, in modo che inizino la replica in Azure.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-to-the-original-or-alternate-location"></a>Eseguire il failback nella posizione originaria o in una posizione alternativa
Se è stato eseguito il failover di una macchina virtuale VMware è possibile eseguire il failback nella stessa macchina virtuale di origine, se è ancora presente in locale. In questo scenario viene eseguito il failback delle sole modifiche differenziali. Si noti che:

* Se è stato eseguito il failover di server fisici, il failback viene sempre eseguito in una nuova macchina virtuale VMware.
  * Prima di eseguire il failback di una computer fisico, ricordare che
  * Un computer fisico protetto viene restituito come macchina virtuale dopo aver effettuato il failover da Azure in VMware.
  * È necessario individuare almeno un server di destinazione master e gli host ESX/ESXi necessari per il failback.
* Se si esegue il failback nella macchina virtuale originaria è necessario quanto segue:

  * Se la macchina virtuale è gestita da un server vCenter, l'host ESX della destinazione master deve avere accesso all'archivio dati delle macchine virtuali.
  * Se la VM si trova in un host ESX ma non è gestita da vCenter, il relativo disco rigido deve trovarsi in un archivio dati accessibile da parte dell'host della destinazione master.
  * Se la macchina virtuale si trova in un host ESX e non usa vCenter, è necessario completare l'individuazione dell'host ESX della destinazione master prima di abilitare la riprotezione. Questa opzione è valida anche per il failback di server fisici.
  * Se è presente una macchina virtuale locale, è anche possibile eliminarla prima di eseguire il failback. Il failback crea quindi una nuova macchina virtuale nello stesso host dell'host ESX di destinazione master.
* Quando si esegue il failback in una posizione alternativa i dati vengono ripristinati nello stesso archivio dati e nello stesso host ESX usati dal server di destinazione master locale.

## <a name="prerequisites"></a>Prerequisiti
* Per eseguire il failback di server fisici e macchine virtuali VMware, è necessario un ambiente VMware. Il failback in un server fisico non è supportato.
* Per eseguire il failback è necessaria una rete di Azure creata al momento dell'impostazione iniziale della protezione. Il failback richiede una connessione VPN o ExpressRoute dalla rete di Azure in cui si trovano le macchine virtuali di Azure al sito locale.
* Se le macchine virtuali in cui si vuole eseguire il failback sono gestite da un server vCenter, assicurarsi di avere le autorizzazioni necessarie per l'individuazione di macchine virtuali nei server vCenter. [Altre informazioni](site-recovery-vmware-to-azure-classic.md).
* Se in una macchina virtuale sono presenti snapshot la riprotezione avrà esito negativo. È possibile eliminare gli snapshot o i dischi.
* Prima di eseguire il failback è necessario creare alcuni componenti:
  * **Creare un server di elaborazione in Azure**. Si tratta di una macchina virtuale di Azure che è necessario creare e lasciare in esecuzione durante il failback. È possibile eliminare la macchina al termine del failback.
  * **Creare un server di destinazione master**: il server di destinazione master invia e riceve i dati di failback. Nel server di gestione creato in locale è installato un server di destinazione master per impostazione predefinita. Tuttavia, a seconda del volume di traffico sottoposto a failback, potrebbe essere necessario creare un server di destinazione master separato per il failback.
  * Per creare un server di destinazione master aggiuntivo in esecuzione su Linux, è necessario configurare la macchina virtuale Linux prima di installare il server di destinazione master, come descritto di seguito.
* Quando si esegue un failback, è necessario un server di configurazione locale. Durante il failback, la macchina virtuale deve esistere nel database del server di configurazione, altrimenti il failback non avrà esito positivo. Assicurarsi pertanto di pianificare backup regolari del server. In caso di emergenza, è necessario ripristinare il server con lo stesso indirizzo IP in modo che il failback funzioni.

## <a name="set-up-the-process-server-in-azure"></a>Configurare il server di elaborazione in Azure
È necessario installare un server di elaborazione in Azure per permettere alle macchine virtuali di Azure di rinviare i dati al server di destinazione master locale.

1. Nel portale di Site Recovery selezionare **Server di configurazione** per aggiungere un nuovo server di elaborazione.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Specificare un nome per il server di elaborazione e immettere un nome e una password per connettersi alla macchina virtuale di Azure come amministratore. In **Server di configurazione** selezionare il server di gestione locale e specificare la rete di Azure in cui distribuire il server di elaborazione. La rete deve essere quella in cui si trovano le macchine virtuali di Azure. Specificare un indirizzo IP univoco dalla subnet selezionata e avviare la distribuzione.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Verrà attivato un processo di distribuzione del server di elaborazione.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Dopo che il server di elaborazione è stato distribuito in Azure, è possibile accedere al server usando le credenziali specificate. Al primo accesso viene visualizzata la finestra di dialogo del server di elaborazione. Digitare l'indirizzo IP e la passphrase del server di gestione locale. Lasciare la porta 443 come impostazione predefinita. È anche possibile lasciare la porta 9443 come impostazione predefinita per la replica dei dati a meno che questa impostazione non sia stata specificamente modificata durante la configurazione del server di gestione locale.

   > [!NOTE]
   > Il server non è visibile nelle **proprietà della macchina virtuale**, ma solo nella scheda **Server** del server di gestione in cui è stato registrato. Possono essere necessari circa 10-15 minuti perché il server di elaborazione venga visualizzato.
   >
   >

## <a name="set-up-the-master-target-server-on-premises"></a>Configurare il server di destinazione master in locale
Il server di destinazione master riceve i dati di failback. Un server di destinazione master viene installato automaticamente nel server di gestione locale, ma se si esegue il failback di una grande quantità di dati potrebbe essere necessario configurare un server di destinazione master aggiuntivo. Procedere come segue:

> [!NOTE]
> Per installare un server di destinazione master in Linux, seguire le istruzioni riportate nella procedura successiva.
>
>

1. Se si installa il server di destinazione master in Windows, aprire la pagina Avvio rapido dalla macchina virtuale in cui si sta installando il server di destinazione master e scaricare il file di installazione per l'installazione guidata unificata di Azure Site Recovery.
2. Eseguire la configurazione, quindi in **Prima di iniziare** selezionare **Add additional process servers to scale out deployment** (Aggiungere server di elaborazione per aumentare le istanze di distribuzione).
3. Completare la procedura guidata come per la [configurazione del server di gestione](site-recovery-vmware-to-azure-classic.md). Nella pagina **Dettagli del server di configurazione** specificare l'indirizzo IP del server di destinazione master e una passphrase per accedere alla macchina virtuale.

### <a name="set-up-a-linux-vm-as-the-master-target-server"></a>Configurare una macchina virtuale Linux come server di destinazione master
Per configurare il server di gestione che esegue il server di destinazione master come una macchina virtuale Linux è necessario installare il sistema operativo minimo CentOS 6.6, recuperare gli ID SCSI per ogni disco rigido SCSI, installare alcuni pacchetti aggiuntivi e applicare alcune modifiche personalizzate.

#### <a name="install-centos-66"></a>Installare CentOS 6.6
1. Installare il sistema operativo minimo CentOS 6.6 nella macchina virtuale del server di gestione. Lasciare l'immagine ISO in un'unità DVD e avviare il sistema. Ignorare il test dei supporti, selezionare Inglese (Stati Uniti) come lingua, selezionare **Dispositivi di archiviazione di base**, verificare che il disco rigido non contenga dati importanti e fare clic su **Sì**. Tutti i dati verranno rimossi. Immettere il nome host del server di gestione e selezionare la scheda di rete del server.  Nella finestra di dialogo **Modifica del sistema** selezionare ** Connetti automaticamente** e aggiungere un indirizzo IP statico, una rete e le impostazioni DNS. Specificare un fuso orario e una password radice per accedere al server di gestione.
2. Quando viene richiesto il tipo di installazione, selezionare **Crea layout personalizzato** come partizione. Dopo aver fatto clic su **Avanti** select **Gratuito** e fare clic su Crea. Creare **/**, **/var/crash** e **/home partitions** con **FS Type:** **ext4**. Creare la partizione di scambio con **FS Type: swap**.
3. Se vengono rilevati dispositivi preesistenti viene visualizzato un messaggio di avviso. Fare clic su **Formatta** per formattare l'unità con le impostazioni della partizione. Fare clic su **Scrivi modifica su disco** per applicare le modifiche della partizione.
4. Selezionare **Installa caricatore di avvio** > **Avanti** per installare il caricatore di avvio nella partizione radice.
5. Al termine dell'installazione, fare clic su **Riavvia**.

#### <a name="retrieve-the-scsi-ids"></a>Recuperare gli ID SCSI
1. Dopo l'installazione, recuperare gli ID SCSI per ogni disco rigido SCSI nella macchina virtuale. A tale scopo, arrestare la VM del server di gestione nelle proprietà della VM in VMware, fare clic con il pulsante destro del mouse sulla voce della VM > **Modifica impostazioni** > **Opzioni**.
2. Selezionare **Avanzate** > **Generale** e fare clic su **Parametri di configurazione**. Quando il computer è in esecuzione questa opzione è disattivata. Per attivarla è necessario arrestare il computer.
3. Se la riga **disk.EnableUUID** esiste, verificare che il valore sia impostato su **True**, con distinzione tra maiuscole e minuscole. Se il valore è già impostato su True, è possibile annullare e testare il comando SCSI in un sistema operativo guest dopo l'avvio.
4. Se la riga non esiste, fare clic su **Aggiungi riga** e aggiungerla impostando il valore su **True**. Non usare le virgolette doppie.

#### <a name="install-additional-packages"></a>Installare pacchetti aggiuntivi
È necessario scaricare e installare alcuni pacchetti aggiuntivi.

1. Assicurarsi che il server di destinazione master sia connesso a Internet.
2. Eseguire questo comando per scaricare e installare 15 pacchetti dal repository di CentOS: **# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools**.
3. Se le macchine di origine da proteggere eseguono Linux con il file system Reiser o XFS per il dispositivo di avvio o radice, è necessario scaricare e installare pacchetti aggiuntivi come indicato di seguito:

   * # <a name="cd-usrlocal"></a>cd /usr/local
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Applicare modifiche personalizzate
Per applicare modifiche personalizzate dopo aver completato i passaggi successivi all'installazione e aver installato i pacchetti, eseguire queste operazioni:

1. Copiare il file binario di RHEL 6-64 Unified Agent nella macchina virtuale. Eseguire questo comando per decomprimere il file binario: **tar –zxvf <file name>**
2. Eseguire questo comando per concedere le autorizzazioni: **#chmod 755 ./ApplyCustomChanges.sh**
3. Eseguire lo script: **# ./ApplyCustomChanges.sh**. Eseguire lo script solo una volta. Riavviare il server dopo l'esecuzione dello script.

## <a name="run-the-failback"></a>Eseguire il failback
### <a name="reprotect-the-azure-vms"></a>Abilitare la riprotezione delle macchine virtuali di Azure
1. Nel portale di Site Recovery > scheda **Computer** selezionare la VM di cui è stato eseguito il failover e fare clic su **Riproteggi**.
2. In **Server di destinazione master** e **Server di elaborazione** selezionare il server di destinazione master locale e il server di elaborazione della VM di Azure.
3. Selezionare l'account configurato per la connessione alla macchina virtuale.
4. Selezionare la versione del failback del gruppo di protezione. Ad esempio, se la macchina virtuale è protetta in PG1, è necessario selezionare PG1_Failback.
5. Per eseguire il ripristino in un percorso alternativo, selezionare l'unità di conservazione e l'archivio dati configurati per il server di destinazione master. Quando si esegue il failback al sito locale, le macchine virtuali VMware nel piano di protezione di failback usano lo stesso archivio dati del server di destinazione master. Per ripristinare la macchina virtuale di Azure di replica nella stessa macchina virtuale locale, quest'ultima deve già trovarsi nello stesso archivio dati del server di destinazione master. Se non è presente alcuna macchina virtuale in locale, ne viene creata una nuova durante la riprotezione.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Dopo aver fatto clic su **OK** per avviare la riprotezione, inizia un processo di replica della VM da Azure al sito locale. È possibile monitorare l'avanzamento nella scheda **Processi** .

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-to-the-on-premises-site"></a>Eseguire un failover nel sito locale
Dopo la riprotezione la macchina virtuale viene spostata nella versione di failback del relativo gruppo di protezione e viene aggiunta automaticamente all'eventuale piano di ripristino usato per il failover in Azure.

1. Nella pagina **Piani di ripristino** selezionare il piano di ripristino che contiene il gruppo di failback e fare clic su **Failover** > **Failover non pianificato**.
2. In **Conferma failover** verificare la direzione del failover (Azure) e selezionare il punto di ripristino da usare per il failover. Usare il più recente. Se nella configurazione delle proprietà della replica sono state abilitate **più VM**, è possibile ripristinare fino all'ultimo punto di ripristino coerente con l'app o l'arresto anomalo del sistema. Fare clic sul segno di spunta per avviare il failover.
3. Durante il failover, Site Recovery arresta le macchine virtuali di Azure. Assicurarsi che il failback sia stato completato e quindi verificare che le macchine virtuali di Azure siano state arrestate come previsto.

### <a name="reprotect-the--on-premises-site"></a>Riproteggere il sito locale
Al termine del failback i dati si trovano nuovamente nel sito locale, ma non sono protetti. Per avviare nuovamente la replica in Azure, eseguire queste operazioni:

1. Nel portale di Site Recovery > scheda **Computer** selezionare le VM di cui è stato eseguito il failback e fare clic su **Riproteggi**.
2. Dopo aver verificato il funzionamento della replica di Azure, in Azure è possibile eliminare le macchine virtuali di Azure (attualmente non in esecuzione) di cui è stato eseguito il failback.

### <a name="common-issues-in-failback"></a>Problemi comuni di failback
1. Se si esegue l'individuazione di vCenter con utente di sola lettura e la protezione delle macchine virtuali, il processo funziona e il failover viene eseguito. Al momento della riprotezione, si verificherà un errore poiché non è stato possibile individuare gli archivi dati. Non verranno quindi visualizzati gli archivi dati elencati durante la riprotezione. Per risolvere questo problema, è possibile aggiornare le credenziali di vCenter usando un account appropriato che abbia le autorizzazioni, quindi ripetere il processo. [Altre informazioni](site-recovery-vmware-to-azure-classic.md)
2. Quando si esegue il failback di una macchina virtuale Linux e l'esecuzione è locale, si noti che il pacchetto di gestione reti viene disinstallato dal computer. Quando la macchina virtuale viene infatti ripristinata in Azure, il pacchetto di gestione reti viene rimosso.
3. Se per la configurazione di una macchina virtuale viene usato un indirizzo IP statico e viene effettuato il failover in Azure, l'indirizzo IP viene acquisito tramite DHCP. Quando il failover viene effettuato di nuovo in locale, la macchina virtuale continua a usare il protocollo DHCP per acquisire l'indirizzo IP. Se necessario, accedere manualmente al computer e impostare l'indirizzo IP nell'indirizzo statico.
4. Se si usa l'edizione gratuita di ESXi 5.5 o di vSphere 6 Hypervisor, sarà possibile effettuare il failover, ma non eseguire il failback. Sarà necessario scegliere l'aggiornamento alla licenza di valutazione per abilitare il failback.

## <a name="failing-back-with-expressroute"></a>Eseguire il failback con ExpressRoute
È possibile eseguire il failback usando una connessione VPN o Azure ExpressRoute. Per usare ExpressRoute occorre tenere presente quanto segue:

* ExpressRoute deve essere configurato nella rete virtuale di Azure in cui viene eseguito il failover dei computer di origine e in cui si trovano le macchine virtuali di Azure dopo il failover.
* I dati vengono replicati in un account di archiviazione di Azure in un endpoint pubblico. È necessario configurare il peering pubblico in ExpressRoute specificando il data center di destinazione per consentire l'uso di ExpressRoute da parte della replica di Site Recovery.
