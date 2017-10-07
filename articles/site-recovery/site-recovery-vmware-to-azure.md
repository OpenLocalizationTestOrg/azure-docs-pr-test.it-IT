---
title: aaaReplicate le macchine virtuali VMware tooAzure | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello che è necessario per la replica dei carichi di lavoro in esecuzione in macchine virtuali VMware tooAzure archiviazione"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>Replicare tooAzure di macchine virtuali VMware con il ripristino del sito

> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmware-to-azure.md)
> * [Azure classico](site-recovery-vmware-to-azure-classic.md)


In questo articolo viene descritto come tooreplicate locale tooAzure di macchine virtuali VMware, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Se si desidera toomigrate le macchine virtuali VMware tooAzure (solo failover), lettura [questo articolo](site-recovery-migrate-to-azure.md) toolearn altre.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Passaggi di distribuzione

Ecco cosa occorre toodo:

1. Verificare i prerequisiti e le limitazioni.
2. Configurare la rete e gli account di archiviazione di Azure.
3. Preparare hello nel computer locale che si desidera toodeploy come server di configurazione hello.
4. Preparare account VMware toobe utilizzato per l'individuazione automatica delle macchine virtuali e, facoltativamente, per l'installazione push del servizio di mobilità hello.
4. Creare un insieme di credenziali dei servizi di ripristino. insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.
5. Specificare origine, destinazione e impostazioni di replica.
6. Distribuire il servizio di mobilità hello in macchine virtuali desiderate tooreplicate.
7. Abilitare la replica per hello macchine virtuali.
7. Eseguire un toomake di failover di test che tutto funzioni come previsto.

## <a name="prerequisites"></a>Prerequisiti

**Requisiti di supporto** | **Dettagli**
--- | ---
**Azzurro** | Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).
**Server di configurazione locale** | È necessaria una VM VMware che esegue Windows Server 2012 R2 o versione successiva. Questo server viene configurato durante la distribuzione di Site Recovery.<br/><br/> Per il processo di hello predefinito server e server di destinazione master vengono installati anche in questa macchina virtuale. Quando le dimensioni, potrebbe essere necessario un server di elaborazione separato e dispone di hello stessi requisiti del server di configurazione hello.<br/><br/> Altre informazioni su questi componenti sono disponibili [qui](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Server VMware locali** | Uno o più server VMware vSphere, che eseguono la versione 6.0, 5.5 o 5.1 con gli ultimi aggiornamenti. I server devono trovarsi nella stessa rete del server di configurazione hello (o server di elaborazione separato) hello.<br/><br/> È consigliabile un vCenter host toomanage server che eseguono 6.0 o 5.5 con gli aggiornamenti più recenti di hello. Quando si distribuisce la versione 6.0, sono supportate solo le funzionalità disponibili nella versione 5.5.
**VM locali** | Macchine virtuali che si desidera tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e devono essere conformi con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Nella VM devono essere in esecuzione gli strumenti VMware.
**URL** | il server di configurazione di Hello deve accedere agli URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.<br/></br> Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).<br/><br/> Consenti a questo URL per il download di MySQL hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Servizio Mobility** | Deve essere installato in ogni VM replicata.




## <a name="limitations"></a>Limitazioni

**Limitazione** | **Dettagli**
--- | ---
**Azzurro** | Gli account di archiviazione e rete devono essere in hello stessa area dell'insieme di credenziali di hello<br/><br/> Se si utilizza un account di archiviazione premium, è necessario anche uno standard di archiviare i log di replica toostore account<br/><br/> Non è possibile replicare gli account toopremium centrale e meridionale.
**Server di configurazione locale** | Le schede delle VM VMware devono essere di tipo VMXNET3. In caso contrario, [installare questo aggiornamento](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Deve essere installato vSphere PowerCLI 6.0.<br/><br> macchina Hello non deve essere un controller di dominio. macchina di Hello deve essere un indirizzo IP statico.<br/><br/> nome host Hello deve essere di 15 caratteri o meno, e il sistema operativo deve essere in lingua inglese.
**VMware** | In vCenter 6.0 sono supportate solo le funzionalità della versione 5.5. Site Recovery non supporta le nuove funzionalità di vCenter e vSphere 6.0 come cross-vCenter vMotion, Virtual Volumes e Storage DRS.
**Macchine virtuali** | Verificare le [limitazioni delle VM di Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Non è possibile replicare VM con dischi crittografati o con avvio UEFI/EFI.<br/><br> I cluster di dischi condivisi non sono supportati. Se l'origine hello VM con gruppo NIC, viene convertito tooa singola scheda di rete dopo il failover.<br/><br/> Se le macchine virtuali dispongono di un disco iSCSI, il ripristino del sito converte i file di disco rigido virtuale tooa dopo il failover. Destinazione iSCSI hello può essere raggiunta in hello macchina virtuale di Azure, si connette tooit e vede e hello disco rigido virtuale. In questo caso, è possibile disconnettere destinazione iSCSI hello.<br/><br/> Se si desidera che la coerenza tra più macchine tooenable, che consente alle macchine virtuali in esecuzione hello stesso carico di lavoro toobe recuperati dati coerenti con l'insieme tooa punto, aprire la porta 20004 in hello macchina virtuale.<br/><br/> Windows deve essere installato nell'unità C hello. disco del sistema operativo Hello deve essere base e non dinamici. disco dati Hello può essere dinamica.<br/><br/> Il file /etc/hosts Linux nelle macchine virtuali devono contenere voci che mappa gli indirizzi tooIP nome host locale hello associati a tutte le schede di rete. Hello nome host, i punti di montaggio, nome del dispositivo, i percorsi di sistema e i nomi di file (/ e così via; in /usr.) deve essere solo in inglese.<br/><br/> Sono supportati tipi specifici di [archiviazione Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).<br/><br/>Creare o impostare **disk.enableUUID=true** nelle impostazioni di VM hello. In questo modo un toohello UUID coerenza VMDK, in modo che installa correttamente e assicura che le modifiche delta solo locale tooon indietro trasferiti durante il failback, senza la replica completa.

## <a name="set-up-azure"></a>Configurare Azure

1. [Configurare una rete di Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Le VM di Azure create dopo il failover verranno inserite in questa rete.
    - È possibile configurare una rete in modalità classica o [Resource Manager](../resource-manager-deployment-model.md).

2. Configurare un [account di archiviazione di Azure](../storage/storage-create-storage-account.md#create-a-storage-account) per i dati replicati.
    - account di Hello può essere standard o [premium](../storage/storage-premium-storage.md).
    - È possibile configurare un account in modalità classica o Resource Manager.

3. [Preparare un account](#prepare-for-automatic-discovery-and-push-installation) nel server vCenter hello o host vSphere, in modo che il ripristino del sito può rilevare automaticamente le macchine virtuali VMware.

## <a name="prepare-hello-configuration-server"></a>Preparare il server di configurazione di hello

1. Installare Windows Server 2012 R2 o versione successiva in una VM VMware.
2. Verificare che disponga di hello macchina virtuale nell'URL di accesso toohello [prerequisiti](#prerequisites).
3. Installare [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Preparare l'individuazione automatica e l'installazione push

- **Preparare un account per l'individuazione automatica**: server di elaborazione di Site Recovery hello individua automaticamente le macchine virtuali. toodo, credenziali esigenze il ripristino del sito che possono accedere al server vCenter e host ESXi vSphere.

    1. toouse un account dedicato, creare un ruolo (a livello di vCenter hello, con questi [autorizzazioni](#vmware-account-permissions). Assegnare un nome all'account, ad esempio **Azure_Site_Recovery**.
    2. Quindi, creare un utente nel server host/vCenter di vSphere hello e assegnare hello ruolo toohello utente. Questo account utente viene specificato durante la distribuzione di Site Recovery.

- **Preparare un hello toopush account servizio di mobilità**: se si desidera toopush hello mobilità servizio tooVMs, è necessario un account che può essere utilizzato da hello processo server tooaccess hello macchina virtuale. account di Hello viene utilizzato solo per l'installazione push hello. È possibile usare un account di dominio o locale:

    - Per Windows, se non si utilizza un account di dominio, è necessario il controllo di accesso remoto nel computer locale hello toodisable. toodo, in hello registrare in **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, aggiungere una voce DWORD hello **LocalAccountTokenFilterPolicy**, con un valore pari a 1.
    - Se si desidera una voce del Registro di sistema di hello tooadd per Windows da CLI, digitare:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Per Linux, account hello devono essere radice nel server di hello origine Linux.

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Selezionare l'obiettivo di protezione hello

Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.

1. Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.
2. In hello risorsa Menu, fare clic su **Site Recovery** > **passaggio 1: preparare l'infrastruttura** > **obiettivi della protezione dati**.

    ![Scegliere gli obiettivi](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. In **obiettivi della protezione dati**selezionare **tooAzure** > **Sì, con VMware vSphere Hypervisor**.

    ![Scegliere gli obiettivi](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Configurare il server di configurazione di hello, registrarla nell'insieme di credenziali hello e individuare le macchine virtuali.

1. Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Origine**.
2. Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.

    ![Impostare l'origine](./media/site-recovery-vmware-to-azure/set-source1.png)
3. In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.
4. Scaricare i file di installazione di hello installazione unificata di Site Recovery.
5. Scaricare la chiave di registrazione dell'insieme di credenziali di hello. che sarà necessaria quando si esegue l'Installazione unificata. chiave di Hello è valida per cinque giorni dopo la generazione è.

   ![Impostare l'origine](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Eseguire l'Installazione unificata di Site Recovery

Seguito hello prima di avviare, quindi eseguire il programma di installazione unificata tooinstall hello configurazione server, il server di elaborazione hello e il server di destinazione master hello.
    - Ottenere una breve panoramica video

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Nel server di configurazione hello VM, verificare che l'orologio di sistema hello è sincronizzato con un [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deve corrispondere. Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.
    - Eseguire l'installazione come amministratore locale nel server di configurazione hello macchina virtuale.
    - Assicurarsi che sia abilitato TLS 1.0 su hello macchina virtuale.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> può anche essere installato il server di configurazione di Hello [dalla riga di comando hello](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Aggiungere account hello per l'individuazione automatica

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>Connettere i server tooVMware

Connettere host ESXi toovSphere o server vCenter, le macchine virtuali VMware toodiscover.

- Se si aggiunge il server vCenter hello o host vSphere con un account senza privilegi di amministratore nel server di hello, account hello necessita di questi privilegi abilitati:
    - Datacenter (Data center), Datastore (Archivio dati), Folder (Cartella), Host, Network (Rete), Resource (Risorsa), Virtual machine (Macchina virtuale) e vSphere Distributed Switch (Switch distribuito vSphere).
    - server vCenter Hello necessita di autorizzazioni di viste di archiviazione.
- Quando si aggiungono server VMware, può richiedere 15 minuti o più per tali tooappear nel portale di hello.
macchine virtuali toodiscover Azure Site Recovery tooallow in esecuzione nell'ambiente locale, è necessario tooconnect il Server VMware vCenter o l'host ESXi vSphere con il ripristino del sito.

Selezionare **+ vCenter** toostart la connessione a un server VMware vCenter o un host VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Il ripristino del sito si connette a server tooVMware hello utilizzando le impostazioni specificate e individua le macchine virtuali.

## <a name="set-up-hello-target"></a>Impostare la destinazione di hello

Prima configurare un ambiente di destinazione hello, verificare di disporre di un [account di archiviazione di Azure e rete](#set-up-azure)

1. Fare clic su **Prepare infrastruttura** > **destinazione**, e selezionare hello sottoscrizione di Azure da toouse.
2. Specificare se per la destinazione deve essere usato il modello di distribuzione classica o Resource Manager.
3. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

   ![Destinazione](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Se è stata creata una rete o un account di archiviazione, fare clic su **+ account di archiviazione** o **+ rete**, toocreate un inline di account o rete di gestione risorse.

## <a name="set-up-replication-settings"></a>Configurare le impostazioni di replica

Ottenere una rapida panoramica video prima di iniziare:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate nuovi criteri di replica, fare clic su **dell'infrastruttura di Site Recovery** > **criteri di replica** > **+ criterio di replica**.
2. In **Creare i criteri di replica** specificare un nome per i criteri.
3. In **soglia RPO**, specificare il limite RPO hello. Questo valore specifica la frequenza con cui vengono creati punti di ripristino dei dati. Se la replica continua supera questo limite, viene generato un avviso.
4. In **conservazione del punto di ripristino**, specificare per quanto tempo (in ore) è un intervallo di conservazione hello per ogni punto di ripristino. Macchine virtuali replicate possono essere ripristinati tooany punto in una finestra. Backup too24 conservazione ore è supportata per i computer replicati archiviazione toopremium e 72 ore per l'archiviazione standard.
5. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Fare clic su **OK** criteri hello toocreate.

    ![Criteri di replica](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Quando si crea un nuovo criterio associata automaticamente con il server di configurazione di hello. Per impostazione predefinita vengono creati automaticamente criteri corrispondenti per il failback. Ad esempio, se hello criterio di replica è **rep criteri** verrà utilizzato come criterio di failback hello **rep-criteri-failback**. Questi criteri non vengono usati fino a quando non si avvia un failback da Azure.  



## <a name="plan-capacity"></a>Pianificare la capacità

1. Dopo aver configurato l'infrastruttura di base è possibile passare alla pianificazione della capacità e valutare se sono necessarie altre risorse. [Altre informazioni](site-recovery-plan-capacity-vmware.md).
2. Dopo aver pianificato la capacità, scegliere **Sì** in **È stata completata la pianificazione della capacità?**

   ![Pianificazione della capacità](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparare le VM per la replica

servizio di mobilità Hello deve essere installato in tutte le macchine virtuali VMware che si desidera tooreplicate. È possibile installare il servizio di mobilità hello in diversi modi:

1. Installare con un'installazione push dal server di elaborazione hello. Questo metodo è necessario tooprepare toouse di macchine virtuali.
2. Installazione con strumenti di distribuzione come System Center Configuration Manager o Automation DSC per Azure.
3.  Installazione manuale.

[Altre informazioni](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Abilitare la replica

Prima di iniziare:

- L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.
- Quando si aggiungono o si modificano le macchine virtuali, può richiedere too15 minuti o più per effetto tootake modifiche e per essi tooappear nel portale di hello.
- È possibile controllare l'ora di ultimo individuato hello per le macchine virtuali in **server di configurazione** > **ultimo contatto in**.
- tooadd macchine virtuali senza attendere l'individuazione pianificata hello, evidenziazione hello del server di configurazione (non selezionata), fare clic su **aggiornamento**.
- Se una macchina virtuale viene preparata per l'installazione push, il server di elaborazione hello installa automaticamente il servizio di mobilità hello quando si abilita la replica.


### <a name="exclude-disks-from-replication"></a>Escludere dischi dalla replica

Per impostazione predefinita, vengono replicati tutti i dischi in un computer. È possibile escludere dischi dalla replica. Ad esempio non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato ogni volta che un computer o applicazione viene riavviata (ad esempio pagefile.sys o tempdb di SQL Server).

### <a name="replicate-vms"></a>Replicare le VM

Prima di iniziare, guardare una rapida panoramica video

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**.
2. In **origine**, selezionare il server di configurazione di hello.
3. In **Tipo di computer** selezionare **Macchine virtuali**.
4. In **vCenter/vSphere Hypervisor**, selezionare i server vCenter hello che gestisce host vSphere hello, o host hello.
5. Selezionare il server di elaborazione hello. Se è ancora stato creato alcun server di elaborazione aggiuntive, questo sarà il server di configurazione di hello. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. In **destinazione**, selezionare la sottoscrizione hello e hello gruppo di risorse in cui si desidera hello toocreate failover le macchine virtuali. Scegliere modello di distribuzione hello che si desidera toouse in Azure (classica o risorsa management), per eseguire il failover le macchine virtuali hello.


7. Selezionare l'account di archiviazione di Azure hello desiderato toouse per la replica dei dati. Se non si desidera toouse un account già stato configurato, è possibile creare uno nuovo.

8. Si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure, quando vengono creati dopo il failover. Selezionare **Configura ora per macchine virtuali selezionate**, tooapply hello rete impostazione tooall macchine selezionate per la protezione. Selezionare **configurare successivamente** tooselect hello Azure rete al computer. Se non si desidera toouse una rete esistente, è possibile crearne uno.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. In **proprietà** > **configurare proprietà**, selezionare account hello che verrà usato da hello processo server tooautomatically installare il servizio Mobility hello computer hello.
11. Per impostazione predefinita, vengono replicati tutti i dischi. Fare clic su **tutti i dischi** e cancellare tutti i dischi non si desidera tooreplicate. Fare quindi clic su **OK**. È possibile impostare proprietà aggiuntive delle VM in un secondo momento.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. In **le impostazioni di replica** > **configurare le impostazioni di replica**, verificare che hello si seleziona il criterio di replica corretto. Se si modifica un criterio, le modifiche saranno tooreplicating applicato macchina e toonew macchine.
12. Abilitare **la coerenza tra più macchine** se si desidera toogather macchine in un gruppo di replica e specificare un nome per il gruppo di hello. Fare quindi clic su **OK**. Si noti che:

    * I computer in gruppi di replica vengono replicati insieme e hanno punti di ripristino condivisi coerenti con l'arresto anomalo del sistema e coerenti con l'app in caso di failover.
    * È consigliabile raggruppare le macchine virtuali e i server fisici in modo da rispecchiare i carichi di lavoro. Abilitazione della coerenza tra più macchine può influire sulle prestazioni del carico di lavoro e deve essere utilizzato solo se sono in esecuzione macchine hello stesso carico di lavoro ed è necessaria la coerenza.

    ![Abilitare la replica](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Fare clic su **Abilita la replica**. È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito hello macchina è pronta per il failover.

### <a name="view-and-manage-vm-properties"></a>Visualizzare e gestire le proprietà della macchina virtuale

È consigliabile verificare le proprietà della VM hello e apportare le modifiche è necessario.

1. Fare clic su **gli elementi replicati** > e selezionare hello macchina. Hello **Essentials** pannello mostra le informazioni sulle impostazioni computer e lo stato.
2. In **proprietà**, è possibile visualizzare la replica e le informazioni di failover per hello macchina virtuale.
3. In **di calcolo e rete** > **calcolo proprietà**, è possibile specificare dimensioni delle macchine Virtuali di Azure hello nome e di destinazione. Modificare hello Nome toocomply con [requisiti Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se è necessario.
4. Modificare le impostazioni per la rete di destinazione hello, subnet e indirizzi IP che verranno assegnato toohello macchina virtuale di Azure:

   - È possibile impostare l'indirizzo IP di destinazione hello.

    - Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP.
    - Se si imposta un indirizzo che non è disponibile al momento del failover, il failover non riesce.
    - Hello stesso indirizzo IP di destinazione è utilizzabile per il failover di test, se è disponibile in rete di failover di test hello hello indirizzo.

   - numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello:

     - Se il numero di hello di schede di rete nel computer di origine hello hello uguale o minore, hello numero di schede consentite per le dimensioni del computer di destinazione hello, allora destinazione hello avrà hello origine hello stesso numero di schede.
     - Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per le dimensioni di destinazione hello, dimensione massima dei hello destinazione verrà utilizzato.
     - Ad esempio, se un computer di origine dispone di due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, nel computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.     
   - Se più schede di rete nella macchina virtuale hello verranno tutti connettono toohello stessa rete.
   - Se macchina virtuale hello ha più schede di rete hello prima uno nell'elenco di hello diventa hello *predefinito* scheda di rete nella macchina virtuale di Azure hello.
4. In **dischi**, è possibile visualizzare hello macchina virtuale del sistema operativo e dati hello dischi che verranno replicati.

#### <a name="managed-disks"></a>Dischi gestiti

In **di calcolo e rete** > **calcolo proprietà**, è possibile impostare "Utilizzo dischi gestiti" impostazione troppo "Sì" per hello VM se si desidera tooattach dischi gestiti tooyour macchina in tooAzure di failover. Dischi gestiti semplifica la gestione disco per le macchine virtuali IaaS di Azure per la gestione degli account di archiviazione hello associati hello dischi di macchina virtuale. Altre informazioni su [Managed Disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - I dischi gestiti sono macchina virtuale creata e associata toohello solo su tooAzure un failover. Per abilitare la protezione, i dati da computer locali continueranno tooreplicate toostorage account.  Dischi gestiti possono essere creati solo per macchine virtuali distribuite mediante il modello di distribuzione Gestione risorse di hello.  

   - Quando si imposta "Utilizzo dischi gestiti" troppo "Yes", solo set di disponibilità nel gruppo di risorse hello con set di "Utilizzo dischi gestiti" troppo "Yes" saranno disponibili per la selezione. In questo modo le macchine virtuali con dischi gestiti può essere solo parte del set di disponibilità con il set di proprietà "Utilizzare gestito dischi" troppo "Yes". Assicurarsi di creare set di disponibilità con il set di proprietà "Dischi utilizzare gestito" in base a dischi toouse preventivo gestiti in caso di failover.  Analogamente, quando si imposta "Utilizzo dischi gestiti" troppo "No", solo i set di disponibilità nel gruppo di risorse hello con proprietà "Utilizzo dischi gestiti" impostare troppo "No" saranno disponibili per la selezione. [Altre informazioni sui dischi gestiti e i set di disponibilità](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Se l'account di archiviazione hello usato per la replica è stata crittografata con la crittografia del servizio di archiviazione in qualsiasi punto nel tempo, creazione di dischi gestiti durante il failover avrà esito negativo. È possibile impostare "Utilizzo dischi gestiti" troppo "No" e quindi ripetere il failover o disabilitare la protezione per la macchina virtuale hello e proteggerlo tooa account di archiviazione che non è abilitata in qualsiasi punto nel tempo la crittografia del servizio di archiviazione.
  > [Altre informazioni su Crittografia del servizio di archiviazione e dischi gestiti](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Eseguire un failover di test


Dopo aver configurato tutti gli elementi, eseguire una toomake di failover di test che tutto funzioni come previsto. Ottenere una rapida panoramica video prima di iniziare
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail su un singolo computer, in **impostazioni** > **elementi replicati**, fare clic su hello VM > **+ Test Failover** icona.

    ![Failover di test](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. toofail sul ripristino di un piano, in **impostazioni** > **piani di ripristino**, piano hello rapida > **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).  

1. In **Failover di Test**selezionare hello Azure rete toowhich macchine virtuali di Azure saranno connesse dopo il failover viene eseguito.

1. Fare clic su **OK** toobegin hello failover. È possibile monitorare i progressi facendo clic su hello VM tooopen le relative proprietà o in hello **Failover di Test** processo nel nome dell'insieme di credenziali > **impostazioni** > **processi**  >  **i processi di ripristino del sito**.

1. Al termine del processo di failover di hello, inoltre deve essere in grado di replica hello toosee macchina di Azure vengono visualizzati nel portale di Azure hello > **macchine virtuali**. È necessario verificare che tale hello VM sia dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.

1. Se si [preparate per le connessioni dopo il failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure.

1. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note**, registrare e salvare eventuali commenti associati hello test failover. Questa operazione eliminerà le macchine virtuali hello creati durante il failover di test.

[Altre informazioni](site-recovery-test-failover-to-azure.md) sui failover di test.


## <a name="vmware-account-permissions"></a>Autorizzazioni dell'account VMware

Il ripristino del sito deve tooVMware di accesso per hello processo server tooautomatically individuare le macchine virtuali e per il failover e failback di macchine virtuali.

- **Eseguire la migrazione**: se si desidera solo toomigrate le macchine virtuali VMware tooAzure, senza mai failback essi, è possibile utilizzare un account di VMware con un ruolo di sola lettura. Un ruolo di questo tipo può eseguire il failover, ma non arrestare i computer di origine protetti. Ciò non è necessario per la migrazione.
- **Replicare/Ripristina**: se si desidera account hello di toodeploy replica completa (replicate, failover, eseguire il failback) deve essere in grado di toorun operazioni quali la creazione e la rimozione di dischi, accensione e così via di macchine virtuali.
- **Individuazione automatica**: è necessario almeno un account di sola lettura.


**Attività** | **Account/ruolo necessario** | **Autorizzazioni** | **Dettagli**
--- | --- | --- | ---
**Individuazione automatica delle VM VMware da parte del server di elaborazione** | È necessario almeno un utente di sola lettura | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = sola lettura | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** dell'oggetto, gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti).
**Failover** | È necessario almeno un utente di sola lettura | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = sola lettura | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti) dell'oggetto.<br/><br/> È utile ai fini della migrazione, ma non per la replica completa, il failover e il failback.
**Failover e failback** | È consigliabile creare un ruolo (Azure_Site_Recovery) con le autorizzazioni necessarie hello e quindi assegnare hello ruolo tooa VMware utente o gruppo | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = Azure_Site_Recovery<br/><br/> Datastore (Archivio dati) -> Allocate space (Alloca spazio), Browse datastore (Sfoglia archivio dati), Low level file operations (Operazioni file di livello basso), Remove file (Rimuovi file), Update virtual machine files (Aggiorna file macchina virtuale)<br/><br/> Network (Rete) -> Network assign (Assegnazione rete)<br/><br/> Risorse -> pool tooresource assegnare macchina virtuale, eseguire la migrazione spenta macchina virtuale, eseguire la migrazione nella macchina virtuale è spenta<br/><br/> Tasks (Attività) -> Create task (Crea attività), Update task (Aggiorna attività)<br/><br/> Virtual machine (Macchina virtuale) -> Configuration (Configurazione)<br/><br/> Virtual machine (Macchina virtuale) -> Interact (Interagisci) -> Answer question (Rispondi alla domanda), Device connection (Connessione dispositivo), Configure CD media (Configura supporto CD), Configure floppy media (Configura supporto floppy), Power off (Spegni), Power on (Accendi), VMware tools install (Installazione strumenti VMware)<br/><br/> Virtual machine (Macchina virtuale) -> Inventory (Inventario) -> Create (Crea), Register (Registra), Unregister (Annulla registrazione)<br/><br/> Virtual machine (Macchina virtuale) -> Provisioning -> Allow virtual machine download (Consenti download macchina virtuale), Allow virtual machine files upload (Consenti upload file macchina virtuale)<br/><br/> Macchina virtuale -> Snapshots -> Remove snapshots | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** dell'oggetto, gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti).


## <a name="next-steps"></a>Passaggi successivi

Dopo la replica configurazione e in esecuzione, quando si verifica un'interruzione del servizio si esegue il failover tooAzure e macchine virtuali di Azure vengono create dai dati hello replicato. È quindi possibile accedere carichi di lavoro e le App in Azure, fino a quando non è la posizione primaria tooyour indietro quando vengono restituite le operazioni di toonormal.

- [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e come toorun li.
- [Altre informazioni](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers) per eseguire la migrazione di computer invece della replica e del failback.
- [Conoscenza failback](site-recovery-failback-azure-to-vmware.md), toofail back e replicare macchine virtuali di Azure, eseguire il backup del sito primario locale toohello.

## <a name="third-party-software-notices-and-information"></a>Informazioni e comunicazioni sul software di terze parti
Do Not Translate or Localize

software Hello e in esecuzione nel firmware hello prodotto Microsoft o servizio è basato su o integra materiale proveniente dai hello progetti elencati sotto (collettivamente, "terze parti Code").  Microsoft è hello autore originale non di hello codice di terze parti.  copyright originale Hello e la licenza, in cui Microsoft ha ricevuto tale codice di terze parti, sono set specificato di seguito.

informazioni di Hello nella sezione si riferisce il codice di terze parti componenti dei progetti hello elencati di seguito. Such licenses and information are provided for informational purposes only.  Questo codice di terze parti è in corso tooyou relicensed da Microsoft in termini di hello prodotto o servizio Microsoft di licenza software Microsoft.  

informazioni di Hello nella sezione B sono per quanto riguarda i componenti del codice di terze parti che vengono eseguiti tooyou disponibili da Microsoft in condizioni di licenza originale hello.

è possibile trovare completo del file Hello in hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
