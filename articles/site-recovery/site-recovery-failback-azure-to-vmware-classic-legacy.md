---
title: aaaFail nuovamente le macchine virtuali VMware da Azure nel portale legacy classico hello | Documenti Microsoft
description: "In questo articolo viene descritto come back toofail una macchina virtuale VMware che è stata replicata tooAzure con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Eseguire il backup le macchine virtuali VMware e server fisici da tooVMware Azure con Azure Site Recovery (legacy)
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-failback-azure-to-vmware.md)
> * [Portale di Azure classico](site-recovery-failback-azure-to-vmware-classic.md)
> * [Portale di Azure classico (Legacy)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

Questo articolo viene descritto come toofail indietro le macchine virtuali VMware e server fisici Windows/Linux da sito locale di Azure tooyour dopo che è stato replicato da locale sito tooAzure utilizzando [Azure Site Recovery?](site-recovery-overview.md).

In questo articolo viene descritta una configurazione obsoleta e non deve essere usato per nuovi insiemi di credenziali.

## <a name="architecture"></a>Architettura
Il diagramma rappresenta uno scenario di failover e failback hello. linee blu Hello sono connessioni hello utilizzate durante il failover. le righe rosse Hello sono connessioni hello utilizzate durante il failback. le linee di Hello con frecce discutere hello internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Prima di iniziare
* È necessario aver eseguito il failover delle VM VMware o dei server fisici e che questi vengano eseguiti in Azure.
* Si noti che è possibile solo eseguire il backup le macchine virtuali VMware e server fisici Windows/Linux da macchine virtuali di Azure tooVMware nel sito primario di hello locale.  Se si sta riesce nuovamente un computer fisico, failover tooAzure convertirà tooan macchina virtuale di Azure e il failback tooVMware convertirà tooa VM VMware.

Ecco come configurare il failback:

1. **Impostare i componenti di failback**: È necessario tooset di un server di vContinuum in locale e scegliere i server di configurazione toohello VM in Azure. Verrà inoltre configuri un server di elaborazione come server di destinazione master locale toohello indietro di macchina virtuale di Azure toosend dati. Registrare il server di elaborazione hello con server di configurazione hello gestita hello failover. e installare un server di destinazione master locale. Se è necessario un server di destinazione master Windows, questo viene configurato automaticamente durante l'installazione di vContinuum. Se è necessario Linux è necessario tooset, configurarlo manualmente in un server distinto.
2. **Abilitare la protezione e il failback**: dopo aver configurato i componenti di hello, in vContinuum, occorre tooenable protezione per il failover di macchine virtuali di Azure. Si verrà eseguito un controllo di conformità in hello macchine virtuali ed eseguire un failover da sito locale di Azure tooyour. Al termine il failback in modo che inizino replica tooAzure si riproteggere macchine locali.

## <a name="step-1-install-vcontinuum-on-premises"></a>Passaggio 1: Installare vContinuum in locale
Si sarà necessario tooinstall vContinuum un server locale e scegliere i server di configurazione toohello.

1. [Scaricare vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).
2. Quindi scaricare hello [vContinuum aggiornamento](http://go.microsoft.com/fwlink/?LinkID=533813) versione.
3. Installare una versione più recente di hello di vContinuum. In hello **iniziale** pagina fare clic su **Avanti**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Hello prima pagina della procedura guidata hello specificare l'indirizzo IP del server CX hello e porta del server CX hello. Selezionare **Use HTTPS**.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Trovare l'indirizzo IP del server di configurazione hello in hello **Dashboard** scheda hello del server di configurazione macchina virtuale in Azure.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Trovare il server di configurazione hello HTTPS la porta pubblica su hello **endpoint** scheda hello del server di configurazione macchina virtuale in Azure.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. In hello **CS Passphrase dettagli** pagina specificare la passphrase hello annotato verso il basso quando è stato registrato il server di configurazione di hello. Se non si ricorda Archivia **c:\\programmi (x86)\\InMage sistemi\\privata\\connection.passphrase** nel server di configurazione hello macchina virtuale.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. In hello **Seleziona posizione di destinazione** pagina specificare dove desidera tooinstall hello vContinuum server e fare clic su **installare**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Al termine dell'installazione, è possibile avviare vContinuum.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>Passaggio 2: Installare un server di elaborazione in Azure
È necessario tooinstall un server di elaborazione in Azure in modo che hello macchine virtuali in Azure possono inviare i server di destinazione master locale hello dati tooan indietro.

1. In hello **server di configurazione** pagina in Azure, tooadd selezionare un nuovo server di elaborazione.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. Specificare il nome di un server di processo e una macchina virtuale di toohello tooconnect di nome e una password come amministratore. Selezionare hello configurazione server toowhich si desidera tooregister hello processo server. Deve trattarsi di hello nello stesso server in uso tooprotect ed eseguire il failover le macchine virtuali.
3. Specificare hello Azure in cui hello devono essere distribuiti i server di elaborazione di rete. Deve essere hello stessa rete come server di configurazione hello. Specificare un indirizzo IP univoco dalla subnet selezionata e avviare la distribuzione.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Server di elaborazione hello toodeploy trigger è un processo.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Dopo aver distribuito il server di elaborazione hello in Azure è possibile accedere ai server hello utilizzando le credenziali di hello specificato. Registrare il server di elaborazione hello in hello allo stesso modo è stato registrato hello processo server locale.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> server Hello registrati durante il failback non saranno visibili in proprietà macchina virtuale in Site Recovery. Sono visibili in hello solo **server** scheda hello toowhich di server di configurazione per cui sono registrati. Può richiedere circa 10-15 minuti fino a quando non sono hello processo server viene visualizzato nella scheda hello.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>Passaggio 3: Installare un server di destinazione master in locale
A seconda del sistema operativo macchine virtuali di origine, è necessario tooinstall Linux o un server di destinazione master Windows locale.

### <a name="deploy-a-windows-master-target-server"></a>Distribuire un server di destinazione master Windows
Una destinazione master Windows è già in bundle nel programma di installazione di vContinuum. Quando si installa vContinuum hello, un server master viene distribuito in hello nello stesso computer e server di configurazione toohello registrati.

1. distribuzione toobegin, creare un oggetto vuoto del computer locale nell'host ESX hello in cui si desidera toorecover hello macchine virtuali di Azure.
2. Verificare che esistono almeno due dischi collegati toohello VM: uno viene utilizzato per sistema operativo hello e altri hello viene utilizzato per l'unità di conservazione hello.
3. Installazione del sistema operativo hello.
4. Installare hello vContinuum nel server di hello. Ciò consente inoltre di completare l'installazione del server di destinazione master hello.

### <a name="deploy-a-linux-master-target-server"></a>Distribuire un server di destinazione master Linux
1. distribuzione toobegin, creare un oggetto vuoto del computer locale nell'host ESX hello in cui si desidera toorecover hello macchine virtuali di Azure.
2. Verificare che esistono almeno due dischi collegati toohello VM: uno viene utilizzato per sistema operativo hello e altri hello viene utilizzato per l'unità di conservazione hello.
3. Installazione del sistema operativo Linux hello. sistema di destinazione master Linux Hello non deve utilizzare LVM radice o memorizzazione spazi di archiviazione. Server di destinazione master Linux configurata tooavoid LVM partizioni e dischi per impostazione predefinita.
4. Partizioni che è possibile creare:

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Eseguire prima di iniziare l'installazione di destinazione master hello hello passaggi di post installazione seguenti:

#### <a name="post-os-installation-steps"></a>Procedure di successive all’installazione del sistema operativo
tooget hello ID SCSI per ogni disco rigido SCSI in una macchina virtuale Linux, abilitare il parametro hello "disco. EnableUUID = TRUE "come indicato di seguito:

1. Arrestare la macchina virtuale.
2. Fare clic sulla voce di hello VM nel pannello sinistro hello > **Modifica impostazioni**.
3. Fare clic su hello **opzioni** scheda. Selezionare **Avanzate\>Generale ** > **Parametri di configurazione**. Hello **parametri di configurazione** opzione è disponibile solo quando hello macchina viene arrestata.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Controllare se esiste una riga con il valore **disk.EnableUUID** . Se è stato impostato troppo, quindi**False** impostare troppo**True** (non maiuscole / minuscole). Se esiste ed è impostato tootrue, fare clic su **Annulla** e testare il comando SCSI hello all'interno del sistema operativo guest di hello dopo che viene avviato. Se non esiste, fare clic su **Add Row**(Aggiungi riga).
5. Aggiungi disco. EnableUUID in hello **nome** colonna. Impostare il relativo valore come TRUE. Non aggiungere hello sopra i valori con virgolette doppie.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Scaricare e installare pacchetti aggiuntivi di hello
Nota: Assicurarsi che il sistema hello abbia la connettività internet prima del download e installazione di pacchetti aggiuntivi di hello.

\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools

Il comando scarica questi 15 pacchetti dal repository CentOS 6.6 e li installa:

bc-1.06.95-1.el6.x86\_64.rpm

busybox-1.15.1-20.el6.x86\_64.rpm

elfutils-libs-0.158-3.2.el6.x86\_64.rpm

kexec-tools-2.0.0-280.el6.x86\_64.rpm

lsscsi-0.23-2.el6.x86\_64.rpm

lzo-2.03-3.1.el6\_5.1.x86\_64.rpm

perl-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm

perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm

perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm

perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-version-0.77-136.el6\_6.1.x86\_64.rpm

rsync-3.0.6-12.el6.x86\_64.rpm

snappy-1.1.0-1.el6.x86\_64.rpm

wget-1.12-5.el6\_6.1.x86\_64.rpm

Se il computer di origine hello utilizza Reiser o XFS filesystem per dispositivo di avvio o radice hello, pacchetti seguenti devono scaricati e installati in tooprotection precedente di destinazione master Linux.

\# cd /usr/local

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm

\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm

#### <a name="apply-custom-configuration-changes"></a>Applicare le modifiche di configurazione personalizzate
Prima di applicare tali modifiche assicurarsi aver completato la sezione precedente di hello, attenersi alla seguente procedura:

1. Copiare hello RHEL 6-64 unificata agente binario toohello appena creata del sistema operativo.
2. Eseguire questo comando toountar hello binario: **tar - zxvf \<nome File\>**
3. Autorizzazioni di toogive questo comando di esecuzione: \# **./ApplyCustomChanges.sh chmod 755**
4. Eseguire script hello: ** \# ./ApplyCustomChanges.sh**. Eseguire script hello una sola volta nel server di hello. Riavviare il server di hello dopo l'esecuzione di script hello.

### <a name="install-hello-linux-server"></a>Installare i server Linux hello
1. [Scaricare](http://go.microsoft.com/fwlink/?LinkID=529757) file di installazione di hello.
2. Copiare toohello file hello macchina virtuale di destinazione Master Linux utilizzando un'utilità client sftp di propria scelta. In alternativa è possibile accedere a una macchina virtuale di destinazione master Linux hello e utilizzare wget toodownload hello pacchetto di installazione dal collegamento fornito
3. Accedere al hello Linux destinazione master server macchina virtuale usando un ssh client desiderato
4. Se si è connessi toohello Azure rete in cui è distribuito il server di destinazione master Linux attraverso una connessione VPN quindi utilizzare l'indirizzo IP interno per il server hello che è possibile trovare nella macchina virtuale **Dashboard** scheda e porta 22 tooconnect toohello Linux master utilizzando Secure Shell Server di destinazione.
5. Se si esegue la connessione server di destinazione master Linux toohello tramite una connessione internet pubblico utilizzare indirizzo IP virtuale pubblico di hello Linux master server di destinazione (da macchine virtuali hello **Dashboard** scheda) e hello endpoint pubblico creato per ssh toologin toohello Linux servder.
6. Estrarre i file hello dall'archivio tar hello compresso con gzip Linux destinazione master Server programma di installazione eseguendo: *"tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6-64"* dalla directory hello che contiene i file di programma di installazione hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Se la modifica è estratto hello installer tooa diverse directory dei file sono stati estratti toohello contenuto hello toowhich della directory dell'archivio tar hello. Da questo percorso di directory eseguire "sudo ./install.sh".

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. Quando richiesto toochoose un ruolo primario seleziona **2 (schema di destinazione)**. Lasciare hello altre opzioni di installazione interattivo i valori predefiniti.
9. Attendere che l'installazione toocontinue e hello tooappear di interfaccia di configurazione Host. utilità di configurazione dell'Host di destinazione master Linux hello Server Hello è un'utilità della riga di comando. Non ridimensionare hello ssh finestra Utilità client. Utilizzare prova freccia chiavi tooselect prova **globale** opzione, quindi premere INVIO sulla tastiera.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. Nel campo hello **IP** immettere l'indirizzo IP interno hello hello del server di configurazione (è possibile trovarlo in hello **Dashboard** scheda hello del server di configurazione macchina virtuale) e premere INVIO. Nel campo **Port** immettere **22** e premere INVIO.
11. Lasciare **Use HTTPS** impostato su **Yes** e premere INVIO.
12. Immettere la Passphrase generata nel server di configurazione hello hello. Se si utilizza un client PUTTY da una macchina virtuale Windows macchina toossh toohello Linux è possibile utilizzare MAIUSC + INS toopaste hello contenuto degli Appunti hello. Copiare hello Passphrase toohello locale negli Appunti utilizzando Ctrl-C e utilizzare MAIUSC + INS toopaste è. Premere INVIO.
13. Utilizzare tooquit chiave toonavigate di hello freccia destra e premere INVIO. Attendere toocomplete di installazione.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Se per qualche motivo non è riuscita tooregister il server di configurazione Linux toohello server di destinazione master non è dunque eseguendo l'host di utilità di configurazione da /usr/local/ASR/Vx/bin/hostconfigcli (è prima necessario toothis le autorizzazioni di accesso tooset Directory eseguendo chmod come utente con privilegi avanzato).

#### <a name="validate-master-target-registration"></a>Convalidare la registrazione di destinazione master
È possibile convalidare tale hello server di destinazione master è stato registrato correttamente il server di configurazione toohello nell'insieme di credenziali di Azure Site Recovery > **Server di configurazione** > **i dettagli del Server**.

> [!NOTE]
> Dopo la registrazione di server di destinazione master hello, se si ricevono errori di configurazione che hello macchina virtuale potrebbe essere stata eliminata da Azure o che gli endpoint non sono configurati correttamente, infatti, sebbene hello venga rilevata configurazione di destinazione master da hello Azure dndpoints quando la destinazione master hello è distribuita in Azure, ciò non accade per on-premise destinazione master server locale. Dato che non ci saranno conseguenze per il failback, è possibile ignorare questi errori.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>Passaggio 4: Proteggere hello macchine virtuali toohello nel sito locale
Prima di eseguire il failover, è necessario tooprotect macchine virtuali toohello nel sito locale.

### <a name="before-you-begin"></a>Prima di iniziare
Quando una macchina virtuale è stata eseguita il failover tooAzure, aggiunge un'unità temporanea extra per file di paging. Si tratta di un'unità aggiuntiva che non è in genere necessaria per le macchine virtuali di cui è stato effettuato il failover poiché dispone già di un'unità dedicata per il file di paging. Prima di iniziare la protezione delle macchine virtuali hello inversa, è necessario assicurarsi che l'unità viene portata offline in modo che non vengono protette. Procedere come segue:

1. Aprire Gestione Computer e selezionare la gestione dell'archiviazione in modo che elenca macchina di hello dischi toohello collegato e non in linea.
2. Selezionare i computer collegati toohello disco temporaneo di hello e scegliere toobring non in linea.

### <a name="protect-hello-vms"></a>Proteggere le macchine virtuali hello
1. Nel portale di Azure hello, controllare gli stati di hello di hello tooensure di macchina virtuale che sta sottoposta a failover.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. Avviare vContinuum sul computer.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Fare clic su **nuovo gruppo protezione dati** e selezionare tipo di sistema di hello operazione, il
4. Nella finestra Nuovo hello aprire hello seleziona **tipo di sistema operativo** > **Ottieni dettagli** per hello macchine virtuali desiderate toofail nuovamente. In **i dettagli del server primario**, identificare e selezionare hello macchine virtuali che si desidera tooprotect. Macchine virtuali sono elencate sotto il nome di host di vCenter hello in cui erano prima del failover.
5. Quando si seleziona una macchina virtuale di tooprotect (e ha già eseguito il failover tooAzure) una finestra popup contenente due voci per la macchina virtuale hello. Questo avviene perché il server di configurazione di hello rileva due istanze di hello tooit di macchine virtuali registrate. È necessario voce hello tooremove per hello locali di macchina virtuale in modo che è possibile proteggere hello VM corretta. tooidentify hello Azure VM voce corretta qui, è possibile accedere ai hello macchina virtuale di Azure e andare tooC:\Program file (x86) \Microsoft Azure Site Recovery\Application Data\etc. In drscout.conf file hello, identificare l'ID dell'host hello. Nella finestra di dialogo vContinuum hello lasciare hello per cui è possibile trovare ID host hello in hello macchina virtuale. Eliminare tutte le altre voci. hello tooselect correggere VM è possibile fare riferimento tooits l'indirizzo IP. Hello IP indirizzo intervallo locale verrà essere hello VM locale.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. Server vCenter hello arrestare la macchina virtuale di hello. È anche possibile eliminare le macchine virtuali hello in locale.
7. Specificare quindi hello locale MT server toowhich desiderato tooprotect hello macchine virtuali. toodo, toohello vCenter server toowhich desiderato toofail nuovamente di connettersi.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. Server di destinazione master hello selezionare basati su hello host toowhich desiderato hello toorecover macchina virtuale.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Forniscono opzioni di replica hello per ognuna delle macchine virtuali hello. toodo questo è necessario tooselect prova ripristino lato dell'archivio dati toowhich prova le macchine virtuali verranno ripristinate. tabella Hello riepiloga diverse opzioni hello tooprovide è necessario per ogni macchina virtuale.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Opzione** | **Opzione consigliata** |
   | --- | --- |
   |  Process server IP address |Selezionare il server di elaborazione hello distribuito in Azure |
   |  Dimensioni di memorizzazione in MB | |
   |  Valore di memorizzazione |1 |
   |  Giorni o ore |Days |
   |  Consistency interval |1 |
   |  Select target datastore |Hello archivio dati disponibile nel sito di ripristino hello. archivio dati Hello deve avere spazio sufficiente ed host ESX toohello disponibili in cui si desidera macchina virtuale di toorestore hello. |
10. Configurare le proprietà che hello macchina virtuale verranno acquisita dopo il failover da sito locale tooon hello. in hello nella tabella seguente sono riepilogate le proprietà di Hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Proprietà** | **Dettagli** |
    | --- | --- |
    | Network configuration |Per ogni scheda di rete rilevato, selezionarla e fare clic su **modifica** indirizzo IP di tooconfigure hello il failback per la macchina virtuale hello. |
    | Configurazione hardware |Specificare hello CPU e memoria hello per hello macchina virtuale. Impostazioni possono essere applicati tooall hello macchine virtuali che si sta tentando di tooprotect. tooidentify hello valori corretti per hello CPU e memoria, è possibile fare riferimento a dimensioni del ruolo VM IAAS toohello e visualizzare hello numero di core e memoria assegnata. |
    | Nome visualizzato |Dopo il failback tooon locale, è possibile rinominare le macchine virtuali hello come appaiono nell'inventario vCenter hello. nome predefinito Hello è nome host macchina virtuale hello. nome della macchina virtuale hello tooidentify, è possibile fare riferimento toohello elenco di macchine Virtuali nel gruppo protezione dati hello. |
    | Configurazione NAT |Illustrato in dettaglio di seguito |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>Configurare le impostazioni NAT
1. tooenable protezione delle macchine virtuali hello, due canali di comunicazione necessario toobe stabilita. primo canale Hello è tra una macchina virtuale hello e server di elaborazione hello. Questo canale raccoglie i dati di hello da hello macchina virtuale e lo invia toohello server di elaborazione che invia quindi hello server di destinazione master toohello di dati. Se il server di elaborazione di hello e hello toobe di macchina virtuale protetto si trovano in hello stessa rete virtuale di Azure, sarà necessario impostazioni NAT toouse. In caso contrario, specificare le impostazioni NAT. Consente di visualizzare l'indirizzo IP pubblico hello hello del server di elaborazione in Azure.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. secondo canale Hello è compreso tra il server di elaborazione di hello e server di destinazione master hello. opzione toouse NAT Hello o non a seconda che si utilizza una connessione VPN in base o la comunicazione su hello internet. Non selezionare NAT se si usa una VPN, ma solo se si usa una connessione Internet.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Se non sono state eliminate di macchine virtuali di on-premise hello come specificato e se l'archivio dati hello sono toostill indietro errori contiene hello precedente VMDK, sarà necessario tooensure tale failback hello macchina virtuale viene creata in una nuova posizione. toodo questo hello seleziona **avanzate** impostazioni e specificare un alternativo tooin toorestore cartella **le impostazioni del nome cartella**. Lasciare hello altre opzioni con le impostazioni predefinite. Applicare hello cartella nome delle impostazioni tooall hello server.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Eseguire una verifica della preparazione tooensure che le macchine virtuali hello sono pronti toobe protetto locale tooon indietro.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Attendere che toocomplete. Se è stato in tutte le macchine virtuali è possibile specificare un nome per il piano di protezione hello. Quindi fare clic su **Proteggi** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. È possibile monitorare l'avanzamento in vContinuum.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Dopo il passaggio di hello **l'attivazione del piano di protezione** al termine, è possibile monitorare protezione della macchina virtuale nel portale di Site Recovery hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. È possibile visualizzare lo stato esatto hello utilizzando facendo clic su hello macchina virtuale e il monitoraggio dello stato di avanzamento.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Preparare il piano di failback hello
È possibile preparare un piano di failback utilizzando vContinuum in modo che un'applicazione hello può essere toohello indietro non riuscito nel sito locale in qualsiasi momento. Questi piani di ripristino sono molto simili piani di ripristino toohello in Site Recovery.

1. Avviare vContinuum e selezionare **Manage plans** > **Recover**. È possibile visualizzare l'elenco di tutti i piani di hello che sono stati utilizzati toofail su macchine virtuali. È possibile utilizzare hello stesso piani toorecover.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Selezionare il piano di protezione hello e tutte le macchine virtuali che si desidera toorecover in essa contenuti hello. Quando si seleziona ogni macchina virtuale è possibile visualizzare ulteriori dettagli, tra cui hello destinazione ESX server e disco di macchina virtuale di origine hello. Fare clic su **Avanti** toobegin hello procedura guidata Ripristina e selezionare le macchine virtuali hello desiderato toorecover.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. È possibile recuperare in base alle opzioni più ma si consiglia di usare **Tag più recente** e selezionare **applica per tutte le macchine virtuali** tooensure che i dati più recenti dalla macchina virtuale hello hello verrà utilizzato.
4. Eseguire hello **controllo di conformità.** Verrà verificato se i parametri di destra hello sono ripristino VM tooenable configurato. Fare clic su **Avanti** se tutti i controlli di hello hanno esito positivo. In caso contrario controllare il registro hello e risolvere gli errori di hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. In **configurazione della macchina virtuale** assicurarsi che le impostazioni di ripristino hello siano impostate correttamente. Se si desidera, è possibile modificare le impostazioni della VM hello.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Esaminare l'elenco di hello di macchine virtuali che verranno recuperati e specificare un ordine di ripristino. Si noti che le macchine virtuali siano elencate usando nome host del computer hello. Potrebbe essere difficile toomap hello computer nome toohello macchina virtuale dell'host.
   i nomi di hello toomap, le macchine virtuali passare toohello **Dashboard** in Azure e verificare il nome host hello macchina virtuale.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Specificare un nome per il piano e selezionare **Recover later**. È consigliabile toorecover in un secondo momento perché la protezione iniziale hello potrebbe non essere completa.
8. Fare clic su **ripristinare** toosave hello piano trigger hello recupero o se è stata selezionata toorecover ora e non in un secondo momento. È possibile controllare hello ripristino stato toosee se è stato salvato del piano di hello.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Ripristinare le macchine virtuali
Dopo aver creato il piano di hello, è possibile ripristinare le macchine virtuali hello. Prima di archiviare tale hello virtuale macchine hanno completato la sincronizzazione. Se lo stato della replica indica OK protezione hello viene completata e soglia RPO hello è stata soddisfatta. È possibile verificare l'integrità in proprietà macchina virtuale hello.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Disattivare hello macchine virtuali di Azure prima di iniziare il ripristino di hello. In questo modo non vi è alcun cervello split e che gli utenti potranno accedere solo una copia di un'applicazione hello.

1. Avviare hello salvato piano. Selezionare vContinuum **monitoraggio** hello piani. Elenca tutti i piani di hello che sono stati eseguiti.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Piano selezionare hello in **ripristino** e fare clic su **avviare**. È possibile monitorare il ripristino. Dopo che siano attivate le macchine virtuali in cui è possibile connettersi toothem in vCenter.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>Proteggere tooAzure dopo il failback
Dopo aver completato il failback è opportuno macchine virtuali di hello tooprotect nuovamente. Procedere come segue:

1. Verificare che funzionino hello macchine virtuali locali e che le applicazioni siano raggiungibili.
2. Nel portale di Azure Site Recovery hello, selezionare le macchine virtuali hello ed eliminarli. Selezionare la protezione di hello toodisable delle macchine virtuali hello. In questo modo che le macchine virtuali hello non più protetti.
3. In Azure eliminare hello eseguito il failover delle macchine virtuali di Azure
4. Eliminare la macchina virtuale precedente di hello nel vSpehere. Si tratta di macchine virtuali di hello che precedentemente non riuscito su tooAzure.
5. Nel portale di Site Recovery hello proteggere hello macchine virtuali che è stato recentemente eseguito il failover. Dopo che siano protetti è possibile aggiungerle tooa piano di ripristino.

## <a name="next-steps"></a>Passaggi successivi
* [Conoscenza](site-recovery-vmware-to-azure-classic.md) la replica di macchine virtuali VMware e server fisici tooAzure mediante la distribuzione di hello avanzata.
