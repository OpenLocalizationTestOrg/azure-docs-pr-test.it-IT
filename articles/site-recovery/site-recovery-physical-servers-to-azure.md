---
title: aaaReplicate server fisici tooAzure | Documenti Microsoft
description: Viene descritto come toodeploy Azure Site Recovery tooorchestrate replica, il failover e ripristino di locale tooAzure server fisici Windows/Linux tramite hello portale di Azure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Replicare macchine fisiche tooAzure tramite il ripristino del sito


In questo articolo viene descritto come tooreplicate locale tooAzure computer fisici utilizzando il servizio di Azure Site Recovery hello hello portale di Azure.

Se si desidera toomigrate macchine fisiche tooAzure (solo failover), lettura [tooAzure con il ripristino del sito di migrazione](site-recovery-migrate-to-azure.md) toolearn altre.

Inviare commenti e domande nella parte inferiore di hello di questo articolo o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Prerequisiti

**Requisiti di supporto** | **Dettagli**
--- | ---
**Azure** | Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).
**Server di configurazione locale** | Computer locale (computer fisico o VM VMware) che esegue Windows Server 2012 R2 o versione successiva. Impostare il server di configurazione di hello durante la distribuzione di Site Recovery.<br/><br/> Per impostazione predefinita, vengono anche installati nel computer server di elaborazione hello e server di destinazione master. Quando le dimensioni, potrebbe essere necessario un server di elaborazione separato e dispone di hello stessi requisiti del server di configurazione hello.<br/><br/> Ulteriori informazioni su questi componenti in [configurare un ambiente di origine hello](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**VM locali** | Le macchine da tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) e conforme con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL** | il server di configurazione di Hello deve accedere agli URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che sia consentito tooAzure di comunicazione.<br/></br> Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e hello porta HTTPS (443).<br/></br> Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per la gestione di identità e controllo di accesso).<br/><br/> Consenti a questo URL per il download di MySQL hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Servizio Mobility** | Questo servizio viene installato in ogni computer si desidera tooreplicate.

## <a name="limitations"></a>Limitazioni

**Limitazione** | **Dettagli**
--- | ---
**Azzurro** | Gli account di archiviazione e rete devono essere in hello stessa area dell'insieme di credenziali di hello.<br/><br/> Se si utilizza un account di archiviazione premium, è necessario anche uno standard di archiviare i log di replica toostore account.<br/><br/> Non è possibile replicare gli account toopremium centrale e meridionale.
**Server di configurazione locale** | Se si installa il server di configurazione di hello in una VM di VMware, hello il tipo di scheda di macchina virtuale deve essere VMXNET3. In caso contrario, [installare questo aggiornamento](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Se si usa una VM VMware, è necessario installarvi vSphere PowerCLI 6.0.<br/><br> macchina Hello non deve essere un controller di dominio.<br/><br/> macchina di Hello deve essere un indirizzo IP statico.<br/><br/> nome host Hello deve essere di 15 caratteri o meno, e del sistema operativo hello deve essere in lingua inglese.
**Computer replicati** | Verificare le [limitazioni delle VM di Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Se si desidera che la coerenza tra più macchine tooenable, che consente di computer che eseguono hello stesso carico di lavoro toobe ripristinati dati coerenti con l'insieme tooa punto, aprire la porta 20004 computer hello.<br/><br/> Sono supportati tipi specifici di [archiviazione Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).
**Failback** | Non è possibile eseguire dal computer fisico tooa Azure. Se si desidera toobe toofail in grado di back-tooon locale dopo il failover, è necessario un ambiente VMware in modo che è possibile eseguire il backup tooa VM VMware.


## <a name="set-up-azure"></a>Configurare Azure

1. [Configurare una rete di Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Le VM di Azure create dopo il failover verranno inserite in questa rete.

      b. È possibile configurare una rete in modalità classica o in [Resource Manager](../resource-manager-deployment-model.md).

2. Configurare un [account di archiviazione di Azure](../storage/storage-create-storage-account.md#create-a-storage-account) per i dati replicati.

    a. account di Hello può essere standard o [premium](../storage/storage-premium-storage.md).

    b. È possibile configurare un account in modalità classica o in Resource Manager.

## <a name="prepare-hello-configuration-server"></a>Preparare il server di configurazione di hello

1. Installare Windows Server 2012 R2 o versione successiva in un server fisico locale o una VM VMware.

2. Assicurarsi che il computer di hello abbia nell'URL di accesso toohello [prerequisiti](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Preparare l'installazione del servizio Mobility

Se si desidera toopush hello mobilità servizio tooa del computer fisico, è necessario un account che può essere usato da hello processo server tooaccess hello macchine. Hello account viene utilizzato solo per l'installazione push hello. È possibile usare un account di dominio o locale:

  - Per Windows, se non si utilizza un account di dominio, è necessario il controllo di accesso remoto nel computer locale hello toodisable. toodo questa operazione, nel Registro di sistema hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, aggiungere una voce DWORD hello **LocalAccountTokenFilterPolicy**, con un valore pari a 1. Se si desidera voce del Registro di sistema di hello tooadd per Windows da un'interfaccia della riga di comando, digitare:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Per Linux, account di hello deve essere un utente root nel server di hello origine Linux.


## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Selezionare l'obiettivo di protezione hello

Selezionare gli elementi si desidera tooreplicate e in cui si desidera tooreplicate per.

1. Fare clic su **Insiemi di credenziali dei servizi di ripristino** > **insiemi di credenziali**.
2. In hello **risorse** menu, fare clic su **Site Recovery** > **preparare l'infrastruttura** > **obiettivi della protezione dati**.

    ![Scegliere gli obiettivi](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. In **obiettivi della protezione dati**selezionare **tooAzure** > **non virtualizzato / altri**.


## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Configurare il server di configurazione di hello, registrarla nell'insieme di credenziali hello e individuare le macchine virtuali.

1. Fare clic su **Site Recovery** > **Preparare l'infrastruttura** > **Origine**.
2. Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.

    ![Impostare l'origine](./media/site-recovery-vmware-to-azure/set-source1.png)

3. In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.
4. Scaricare hello **installazione unificata di Site Recovery** file di installazione.
5. Scaricare hello **chiave di registrazione dell'insieme di credenziali**. che sarà necessaria quando si esegue l'Installazione unificata. chiave di Hello è valida per cinque giorni dopo la generazione è.

   ![Impostare l'origine](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Eseguire l'Installazione unificata di Site Recovery

Prima di iniziare, hello seguenti:

- Ottenere una breve panoramica video. (video di hello viene descritto come elabora le macchine virtuali VMware tooreplicate ma hello è simile per la replica del computer fisico.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Nel computer server di configurazione hello, verificare che l'orologio di sistema hello è sincronizzato con un [tempo server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.
- Eseguire l'installazione come amministratore locale nel computer server di configurazione hello.
- Assicurarsi che sia abilitato TLS 1.0 nel computer di hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> può anche essere installato il server di configurazione di Hello [dalla riga di comando hello](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello

Prima configurare un ambiente di destinazione hello, verificare di avere toomake un [account di archiviazione di Azure e rete](#set-up-azure).

1. Fare clic su **preparare l'infrastruttura** > **destinazione**, e selezionare hello sottoscrizione di Azure da toouse.
2. Specificare se per la destinazione deve essere usato il modello di distribuzione classica o di Resource Manager.
3. Il ripristino del sito controlla toomake certi di disporre di uno o più account di archiviazione di Azure compatibile e reti.

   ![Destinazione](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Se è stata creata una rete o un account di archiviazione, fare clic su **+ account di archiviazione** o **+ rete** toocreate un inline di account o rete di gestione risorse.

## <a name="set-up-replication-settings"></a>Configurare le impostazioni di replica

Prima di iniziare, visualizzare questa breve panoramica video. (video di hello viene descritto come elabora le macchine virtuali VMware tooreplicate ma hello è simile per la replica del computer fisico.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate nuovi criteri di replica, fare clic su **dell'infrastruttura di Site Recovery** > **criteri di replica** > **+ criterio di replica**.
2. In **Creare i criteri di replica** specificare un nome per i criteri.
3. In **soglia RPO**, specificare il limite RPO hello. Questo valore specifica la frequenza con cui vengono creati punti di ripristino dei dati. Se la replica continua supera questo limite, viene generato un avviso.
4. In **conservazione del punto di ripristino**, specificare per quanto tempo (in ore) è un intervallo di conservazione hello per ogni punto di ripristino. Macchine virtuali replicate possono essere ripristinati tooany punto in una finestra. Backup too24 conservazione ore è supportato per l'archiviazione replicata toopremium macchine. Backup too72 conservazione ore è supportato per l'archiviazione replicata toostandard macchine.
5. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Fare clic su **OK** criteri hello toocreate.

    ![Criteri di replica](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Quando si crea un nuovo criterio, è associata automaticamente a server di configurazione hello. Per impostazione predefinita vengono creati automaticamente criteri corrispondenti per il failback. Ad esempio, se hello criterio di replica è **rep criteri**, criteri di failback hello è **rep-criteri-failback**. Questi criteri non vengono usati fino a quando non si avvia un failback da Azure.  


## <a name="plan-capacity"></a>Pianificare la capacità

1. Dopo aver configurato l'infrastruttura di base è possibile passare alla pianificazione della capacità e valutare se sono necessarie altre risorse. [Altre informazioni](site-recovery-plan-capacity-vmware.md).
2. Dopo aver pianificato la capacità, scegliere **Sì** in **È stata completata la pianificazione della capacità?**

   ![Pianificazione della capacità](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Preparare le VM per la replica

Tutti i computer che si desidera tooreplicate devono essere installato servizio di mobilità di hello. È possibile installare il servizio di mobilità hello in diversi modi:

- Installare il servizio di hello con un'installazione push dal server di elaborazione hello. Questo metodo è necessario macchine tooprepare in anticipo toouse.
- Installare il servizio di hello utilizzando gli strumenti di distribuzione, ad esempio System Center Configuration Manager o di configurazione dello stato desiderato di automazione di Azure.
- Installare manualmente il servizio di hello.

[Altre informazioni](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Abilitare la replica

Prima di iniziare:

- L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.
- Quando si aggiungono o si modificano le macchine virtuali, può richiedere too15 minuti o più effetti tootake modifiche e per essi tooappear nel portale di hello.
- È possibile controllare l'ora di ultimo individuato hello per le macchine virtuali in **server di configurazione** > **ultimo contatto in**.
- tooadd macchine virtuali senza attendere l'individuazione pianificata hello, evidenziazione hello del server di configurazione (non selezionata), fare clic su **aggiornamento**.
- Se una macchina virtuale viene preparata per l'installazione push, il server di elaborazione hello installa automaticamente il servizio di mobilità hello quando si abilita la replica.
- Ottenere una breve panoramica video. (video di hello viene descritto come elabora le macchine virtuali VMware tooreplicate ma hello è simile per la replica del computer fisico.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Escludere dischi dalla replica

Per impostazione predefinita, vengono replicati tutti i dischi presenti in un computer. È possibile escludere dischi dalla replica. Ad esempio, non è possibile tooreplicate dischi con dati temporanei o dati che sono state aggiornate per ogni volta che un riavvio del computer o dell'applicazione (ad esempio, pagefile.sys o tempdb di SQL Server).

### <a name="replicate-vms"></a>Replicare le VM

1. Fare clic su **Eseguire la replica dell'applicazione** > **Origine**.
2. In **Origine** selezionare **Locale**.
3. In **percorso di origine**, selezionare il nome di server di hello configurazione.
4. In **Tipo di computer** selezionare **Computer fisici**.
5. In **server di elaborazione**, scegliere il server di elaborazione hello. Se è ancora stato creato alcun server di elaborazione aggiuntive, questo server è il server di configurazione di hello. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-physical-to-azure/chooseVM.png)

6. In **destinazione**selezionare hello **sottoscrizione** hello e **gruppo di risorse** in cui si desidera toocreate hello macchine virtuali di Azure dopo il failover. Scegliere hello distribuzione modello che si desidera toouse in Azure (classica o gestione delle risorse) per hello sottoposte a failover le macchine virtuali.

7. Selezionare l'account di archiviazione di Azure hello desiderato toouse per la replica dei dati. Se non si desidera toouse un account già stato configurato, è possibile creare uno nuovo.

8. Seleziona hello **rete Azure** e **Subnet** toowhich macchine virtuali di Azure connettersi dopo il failover. Selezionare **Configura ora per macchine virtuali selezionate** tooapply hello rete impostazione tooall macchine selezionate per la protezione. Selezionare **configurare successivamente** tooselect hello Azure rete al computer. Se non si desidera toouse una rete esistente, è possibile crearne uno.

    ![Abilitare la replica](./media/site-recovery-physical-to-azure/targetsettings.png)

9. In **macchine fisiche**, fare clic su **+ macchina fisica** e immettere hello **nome** e **indirizzo IP**. Scegliere hello del sistema operativo della macchina hello desiderato tooreplicate. Sono necessari alcuni minuti fino a quando i computer vengono individuati e visualizzati nell'elenco di hello.

    ![Abilitare la replica](./media/site-recovery-physical-to-azure/machineselect.png)

10. In **proprietà** > **configurare proprietà**, selezionare account hello toobe utilizzato da hello processo server tooautomatically installare il servizio Mobility hello computer hello.
11. Per impostazione predefinita, vengono replicati tutti i dischi. Fare clic su **tutti i dischi**e Cancella tutti i dischi non si desidera tooreplicate. Fare quindi clic su **OK**. È possibile impostare proprietà aggiuntive delle VM in un secondo momento.

    ![Abilitare la replica](./media/site-recovery-physical-to-azure/configprop.png)

12. In **le impostazioni di replica** > **configurare le impostazioni di replica**, verificare che hello si seleziona il criterio di replica corretto. Se si modifica un criterio, le modifiche vengono applicata toohello replica macchina e toonew macchine.
13. Abilitare **la coerenza tra più macchine** se si desidera toogather macchine in un gruppo di replica e specificare un nome per il gruppo di hello. Fare quindi clic su **OK**. Si noti che:

    a. I computer nei gruppi di replica vengono replicati insieme e hanno punti di ripristino condivisi coerenti con l'arresto anomalo del sistema e coerenti con l'app in caso di failover.

    b. È consigliabile raggruppare le macchine virtuali e i server fisici in modo da rispecchiare i carichi di lavoro. L'abilitazione della coerenza su più macchine virtuali può avere un impatto sulle prestazioni del carico di lavoro. Deve essere utilizzato solo se i computer sono in esecuzione hello stesso carico di lavoro ed è necessaria la coerenza.

    ![Abilitare la replica](./media/site-recovery-physical-to-azure/policy.png)

14. Fare clic su **Abilita la replica**. È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** processo viene eseguito, hello macchina è pronta per il failover.

Dopo aver abilitato la replica, hello servizio di mobilità è installato se si configura l'installazione push. Dopo aver hello servizio di mobilità push installato in un computer, un processo di protezione viene avviata e non riesce. Dopo l'errore hello, è necessario toomanually riavviare ogni macchina. Quindi, il processo di protezione hello ricomincia e viene eseguita la replica iniziale.


### <a name="view-and-manage-azure-vm-properties"></a>Visualizzare e gestire le proprietà delle VM di Azure

È consigliabile controllare le proprietà della VM hello e apportare le modifiche necessarie.

1. Fare clic su **gli elementi replicati**e selezionare hello macchina. Hello **Essentials** pannello mostra le informazioni sulle impostazioni computer e lo stato.
2. In **proprietà**, è possibile visualizzare la replica e le informazioni di failover per hello macchina virtuale.
3. In **di calcolo e rete** > **calcolo proprietà**, è possibile specificare dimensioni delle macchine Virtuali di Azure hello nome e di destinazione. Modificare hello Nome toocomply con [requisiti Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) se è necessario.
4. Modificare le impostazioni per la rete di destinazione hello, subnet e indirizzi IP assegnati toohello macchina virtuale di Azure:

    a. È possibile impostare l'indirizzo IP di destinazione hello.

    b.  Se non si fornisce un indirizzo, hello failover userà DHCP.

    c. Se si imposta un indirizzo che non è disponibile al momento del failover, il failover non riesce.

    d. Hello stesso indirizzo IP di destinazione è utilizzabile per il test failover se è disponibile in rete di failover di test hello hello indirizzo.

    e. numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello:

     - Se il numero di hello di schede di rete nel computer di origine hello hello uguale o minore, hello numero di schede consentite per le dimensioni del computer di destinazione hello, allora destinazione hello è hello origine hello stesso numero di schede.
     - Se il numero di hello di schede per la macchina virtuale di origine hello supera hello numero consentito per le dimensioni di destinazione hello, quindi massimo di dimensioni di destinazione hello viene utilizzato.
     - Ad esempio, se un computer di origine dispone di due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, il computer di destinazione di hello è due schede. Se il computer di origine di hello ha due schede di dimensioni di destinazione supportato hello supportano solo una, il computer di destinazione hello ha una sola scheda.     
   - Se macchina virtuale hello dispone di più schede di rete, tutte le connessione toohello stessa rete.
   - Se macchina virtuale hello ha più schede di rete, quindi hello prima uno nell'elenco di hello diventa hello *predefinito* scheda di rete nella macchina virtuale di Azure hello.
5. In **dischi**, è possibile vedere hello macchina virtuale del sistema operativo e i dischi dati hello che vengono replicati.

## <a name="run-a-test-failover"></a>Eseguire un failover di test

Dopo avere impostato backup completo, eseguire una toomake di failover di test che tutto funzioni come previsto. Guardare una rapida panoramica video prima di iniziare.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail su un singolo computer, in **impostazioni** > **elementi replicati**, fare clic su **failover di Test**.

    ![Failover di test](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. toofail sul ripristino di un piano, in **impostazioni** > **piani di ripristino**, piano hello rapida > **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).  
3. In **Failover di Test**selezionare hello Azure rete toowhich macchine virtuali di Azure sono connesse dopo il failover viene eseguito.
4. Fare clic su **OK** toobegin hello failover. È possibile monitorare lo stato di avanzamento facendo hello VM tooopen le relative proprietà o facendo clic su hello **Failover di Test** processo nel nome dell'insieme di credenziali > **impostazioni** > **processi**  >  **i processi di ripristino del sito**.
5. Al termine del failover hello, inoltre deve essere in grado di replica hello toosee macchina di Azure vengono visualizzati nel portale di Azure hello > **macchine virtuali**. Assicurarsi che tale hello VM sia di dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.
6. Se si [preparate per le connessioni dopo il failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure.
7. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note**, registrare e salvare eventuali commenti associati hello test failover. Questo passaggio consente di eliminare le macchine virtuali hello create durante il failover di test.

Per ulteriori informazioni, vedere hello [Test failover tooAzure](site-recovery-test-failover-to-azure.md) documento.

## <a name="next-steps"></a>Passaggi successivi

Dopo la replica configurazione e in esecuzione, quando si verifica un'interruzione del servizio si esegue il failover tooAzure e macchine virtuali di Azure vengono create dai dati hello replicato. È quindi possibile accedere carichi di lavoro e le App in Azure, fino a quando non è la posizione primaria tooyour indietro quando vengono restituite le operazioni di toonormal.

- [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e modalità toorun li.
- [Altre informazioni](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers) per eseguire la migrazione di computer invece della replica e del failback.
- Quando si replicano i computer fisici, è possibile solo eseguire il failback tooa VMware environment. [Informazioni sul failback](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Informazioni e comunicazioni sul software di terze parti
Do Not Translate or Localize

software Hello e in esecuzione nel firmware hello prodotto Microsoft o servizio è basato su o integra materiale proveniente dai hello progetti elencati sotto (collettivamente, "terze parti Code"). Microsoft non è autore hello di hello codice di terze parti. copyright originale Hello e la licenza, in cui Microsoft ha ricevuto tale codice di terze parti, sono set specificato di seguito.

informazioni di Hello nella sezione si riferisce il codice di terze parti componenti dei progetti hello elencati di seguito. Such licenses and information are provided for informational purposes only. Questo codice di terze parti è in corso tooyou relicensed da Microsoft in termini di hello prodotto o servizio Microsoft di licenza software Microsoft.  

informazioni di Hello nella sezione B sono per quanto riguarda i componenti del codice di terze parti che vengono eseguiti tooyou disponibili da Microsoft in condizioni di licenza originale hello.

completo del file Hello è reperibile in hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.
