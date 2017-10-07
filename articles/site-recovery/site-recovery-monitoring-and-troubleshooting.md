---
title: aaaMonitor e risolvere i problemi di protezione per i server fisici e macchine virtuali | Documenti Microsoft
description: Azure Site Recovery coordina la replica di hello, failover e ripristino delle macchine virtuali situato su tooAzure server locale o un Data Center secondario. Utilizzare questo toomonitor articolo e risolvere i problemi di protezione del sito di Virtual Machine Manager o Hyper-V.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>Monitorare e risolvere i problemi di protezione per le macchine virtuali e i server fisici
Questo monitoraggio e risoluzione dei problemi consente di Guida si apprenderà come stato di replica tootrack e risolvere i problemi di tecniche per Azure Site Recovery.

## <a name="understand-hello-components"></a>Comprendere i componenti di hello
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>Distribuzione del sito della macchina virtuale VMware o del server fisico per la replica tra ambiente locale e Azure
tooset il ripristino di database tra una macchina virtuale VMware di on-premise o server fisico e Azure, è necessario tooset hello configurazione server, server di destinazione master, e il processo server componenti nella macchina virtuale o server. Quando si abilita la protezione per il server di origine di hello, Azure Site Recovery consente di installare funzionalità di App per dispositivi mobili hello del servizio App di Microsoft Azure. Dopo un'interruzione del servizio locale e hello origine server failover tooAzure, i clienti devono tooset backup di un server di elaborazione in Azure e un server di destinazione master nel server di origine locale toorebuild hello in locale.

![Distribuzione del sito VMware o fisico per la replica tra ambiente locale e Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Distribuzione del sito Virtual Machine Manager per la replica tra siti locali
tooset il ripristino di database tra due posizioni in locale, è necessario toodownload hello Azure Site Recovery provider e installarlo nel server Virtual Machine Manager hello. provider di Hello deve tooensure connettività Internet che tutte le operazioni che vengono attivate dal portale di Azure hello hello ottengano operazioni locale tooon tradotti.

![Distribuzione del sito Virtual Machine Manager per la replica tra siti locali](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Distribuzione del sito Virtual Machine Manager per la replica tra le sedi locali e Azure
Quando si configura il ripristino del database tra le sedi locali e Azure, è necessario disporre di provider di Azure Site Recovery toodownload hello e installarlo nel server Virtual Machine Manager hello. È inoltre necessario tooinstall hello Azure Recovery Services Agent, che deve toobe installato in ogni host Hyper-V. Per altre informazioni [approfondire qui](site-recovery-hyper-v-azure-architecture.md).

![Distribuzione del sito Virtual Machine Manager per la replica tra le sedi locali e Azure](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Distribuzione del sito Hyper-V per la replica tra sedi locali e Azure
Questo processo è simile tooVirtual Machine Manager la distribuzione. Hello unica differenza è che il provider di Azure Site Recovery hello e agente di servizi di ripristino di Azure viene installato nell'host di Hyper-V hello stesso. [Altre informazioni](site-recovery-hyper-v-azure-architecture.md) .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Monitorare le operazioni di configurazione, protezione e ripristino
Ogni operazione di Azure Site Recovery sia controllata e monitorata in hello **processi** scheda. Per qualsiasi configurazione, protezione o errore di ripristino, visitare toohello **processi** scheda e cercare gli errori.

![filtro non riuscita Hello nella scheda processi hello](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Se gli errori di hello **processi** scheda, fare clic su processo hello e fare clic su **i dettagli dell'errore** per tale processo.

![pulsante di Hello i dettagli dell'errore](media/site-recovery-monitoring-and-troubleshooting/image4.png)

i dettagli dell'errore Hello consentirà di identificare una causa e l'indicazione per problema hello.

![Finestra di dialogo che mostra i dettagli dell'errore per un processo specifico](media/site-recovery-monitoring-and-troubleshooting/image5.png)

Nell'esempio precedente hello, un'altra operazione in corso sembra toobe causando toofail configurazione di protezione hello. Risolvere il problema di hello in base alle raccomandazioni di hello e quindi fare clic su **RESART** tooinitiate hello riprovare.

![Nella scheda processi hello pulsante Hello.](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Hello **riavviare** opzione non è disponibile per tutte le operazioni. Se un'operazione non dispone di hello **riavviare** opzione, tornare alla schermata precedente oggetto toohello e ripetere nuovamente l'operazione di hello. È possibile annullare eventuali processi che sono in corso mediante hello **Annulla** pulsante.

![pulsante Annulla Hello](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Monitorare l'integrità della replica per le macchine virtuali
È possibile utilizzare i provider di Azure Site Recovery hello Azure tooremotely portale monitoraggio per ognuna delle entità hello protetto. Fare clic su **Elementi protetti** e quindi fare clic su **Cloud VMM** o **Gruppi di protezione**. Hello **cloud VMM** scheda è disponibile solo per le distribuzioni che sono basate su Virtual Machine Manager. Per altri scenari, le entità protetta hello sono hello **gruppi protezione dati** scheda.

![opzioni di Hello cloud VMM e i gruppi protezione dati](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Fare clic su un'entità protetta in hello rispettivi cloud o protezione gruppo toosee che tutte le operazioni disponibili vengono visualizzate nel riquadro inferiore di hello.

![Opzioni disponibili per un'entità protetta selezionata](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Come illustrato nella schermata precedente hello, integrità della macchina virtuale hello è **critico**. È possibile fare clic su hello **i dettagli dell'errore** pulsante in caso di errore hello inferiore toosee hello. In base a hello **cause** e **indicazione**, risolvere il problema di hello.

![pulsante di Hello i dettagli dell'errore](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Errori e indicazioni contenute nella finestra di dialogo Dettagli dell'errore hello](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Se eventuali operazioni attive in corso o non è riuscita, visitare toohello **processi** visualizzazione come indicato errore hello tooview precedente per un processo specifico.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Risoluzione dei problemi di Hyper-V a livello locale
Connettersi toohello locale Hyper-V manager console macchina virtuale selezionare hello e visualizzare hello integrità di replica.

![Stato di replica tooview opzione nella console di gestione di Hyper-V: hello](media/site-recovery-monitoring-and-troubleshooting/image12.png)

In questo caso **Integrità della replica** è **Critica**. Fare clic sulla macchina virtuale hello e quindi fare clic su **replica** > **Visualizza stato di replica** dettagli hello toosee.

![Stato della replica per una macchina virtuale specifica](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Se la replica viene sospesa per la macchina virtuale hello, fare clic sulla macchina virtuale hello e quindi fare clic su **replica** > **Riprendi replica**.

![Opzione di replica tooresume nella console di gestione di Hyper-V: hello](media/site-recovery-monitoring-and-troubleshooting/image19.png)

Se una macchina virtuale viene eseguita la migrazione di un nuovo host Hyper-V che si trova all'interno del cluster hello o un computer autonomo e host Hyper-V hello è stata configurata tramite Azure Site Recovery, la replica per la macchina virtuale hello non interessata. Verificare che hello nuovo Hyper-V host soddisfi tutti i prerequisiti di hello e viene configurato tramite Azure Site Recovery.

### <a name="event-log"></a>Registro eventi
| Origini eventi | Dettagli |
| --- |:--- |
| **Registri applicazioni e servizi/Microsoft/VirtualMachineManager/Server/Admin** (server Virtual Machine Manager) |Fornisce tootroubleshoot registrazione utile molti problemi di Virtual Machine Manager diverso. |
| **Registri applicazioni e servizi/MicrosoftAzureRecoveryServices/Replication** (host Hyper-V) |Fornisce tootroubleshoot registrazione utile molti problemi di agente servizi di ripristino di Microsoft Azure. <br/> ![Posizione dell'origine evento Replication per l'host Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Registri applicazioni e servizi/Microsoft/Azure Site Recovery/Provider/Operational** (host Hyper-V) |Fornisce la registrazione utile tootroubleshoot molti problemi di servizio di Microsoft Azure Site Recovery. <br/> ![Posizione dell'origine evento Operational per l'host Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Registri applicazioni e servizi/Microsoft/Windows/Hyper-V-VMMS/Admin** (host Hyper-V) |Fornisce la registrazione utile tootroubleshoot molti problemi di gestione di macchine virtuali Hyper-V. <br/> ![Posizione dell'origine evento Virtual Machine Manager per l'host Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Opzioni di registrazione per la replica Hyper-V
Vengono registrati tutti gli eventi che riguardano la replica tooHyper-V in Hyper-V-VMMS hello\\accesso amministratore si trova in registri applicazioni e servizi\\Microsoft\\Windows. Inoltre, è possibile abilitare un registro analitico per hello servizio Virtual Machine Management di Hyper-V. tooenable questo log, verificare innanzitutto hello analitico e Debug registra visualizzabile nel Visualizzatore eventi hello. Aprire il Visualizzatore eventi e quindi fare clic su **Visualizza** > **Visualizza registri analitici e di debug**.

![Hello opzione Visualizza registri analitici e di Debug](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Un registro analitico è visibile in **Hyper-V-VMMS**.

![log analitico Hello nell'albero di Visualizzatore eventi hello](media/site-recovery-monitoring-and-troubleshooting/image15.png)

In hello **azioni** riquadro, fare clic su **Attiva registro**. Dopo l'attivazione viene visualizzato in **Performance Monitor** come **sessione di traccia eventi** in **Insiemi agenti di raccolta dati**.

![Sessioni di traccia di eventi nella struttura ad albero di hello Performance Monitor](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview hello informazioni raccolte, arrestare innanzitutto la sessione di traccia hello disabilitando log hello. Salva log di hello e aprirla nuovamente nel Visualizzatore eventi o utilizzare altri strumenti tooconvert come desiderato.

## <a name="reach-out-for-microsoft-support"></a>Contattare il supporto Microsoft
### <a name="log-collection"></a>Raccolta registri
Per la protezione del sito di Virtual Machine Manager, fare riferimento troppo[raccolta di Azure Site Recovery tramite lo strumento di supporto diagnostica della piattaforma (SDP)](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect hello necessari i log.

Per la protezione del sito Hyper-V, scaricare il [strumento](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) ed eseguirlo in hello Hyper-V host toocollect hello Registra.

Per gli scenari di server VMware/fisici, fare riferimento troppo[raccolta di log di Azure Site Recovery per VMware e la protezione del sito fisico](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect hello necessari i log.

strumento di Hello raccoglie i log di hello in locale in una sottocartella denominata in modo casuale in % LocalAppData%\ElevatedDiagnostics.

![Procedure di esempio illustrate dalla protezione dei siti Hyper-V.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Aprire un ticket di supporto
raggiungere un ticket di supporto per Azure Site Recovery, tooraise tooAzure supporto tramite l'URL in <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>Articoli della Knowledge Base
* [Modalità di protezione delle macchine virtuali che è state eseguite il failover o eseguirne la migrazione tooAzure lettera di unità hello toopreserve per](http://support.microsoft.com/kb/3031135)
* [Come toomanage locale dell'utilizzo della larghezza di banda di rete protezione tooAzure](https://support.microsoft.com/kb/3056159)
* [Errore di Azure Site Recovery: "risorsa di cluster hello trovato" quando si tenta di protezione tooenable per una macchina virtuale](http://support.microsoft.com/kb/3010979)
* [Hyper-V Replica Troubleshooting Guide](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx) (Guida alla risoluzione dei problemi relativi alla replica Hyper-V)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Errori più comuni di Azure Site Recovery e relative soluzioni
Di seguito sono elencati gli errori comuni e le relative soluzioni. Ogni errore è documentato in una pagina separata del wiki.

### <a name="general"></a>Generale
* <span style="color:green;">NUOVO</span> [Processi con esito negativo con l’errore "un'operazione è in corso". Errore 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">NUOVO</span> [processi non riusciti con errore "Server non è connesso toohello Internet". Errore 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Configurazione
* [server Virtual Machine Manager Hello non può essere registrato a causa di errore interno tooan. Per ulteriori informazioni sull'errore hello, vedere Visualizzazione processi toohello nel portale di Site Recovery hello. Eseguire il programma di installazione nuovo server di hello tooregister.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Una connessione non può essere stabilita toohello Gestione ripristino Hyper-V insieme di credenziali. Verificare le impostazioni del proxy hello o riprovare più tardi.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Configurazione
* [Non è possibile toocreate gruppo protezione dati: si è verificato un errore durante il recupero dell'elenco di hello del server.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Cluster host Hyper-V contiene almeno una scheda di rete statica oppure nessuna scheda connessa è toouse configurato DHCP.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Virtual Machine Manager non dispone delle autorizzazioni toocomplete un'azione.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [Non è possibile selezionare account di archiviazione hello sottoscrizione hello durante la configurazione di protezione.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Protezione
* <span style="color:green;">NUOVO</span> [Abilita protezione esito negativo con errore "Impossibile configurare la protezione per la macchina virtuale hello". Errore 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">NUOVO</span> [Abilita protezione esito negativo con errore "Impossibile abilitare la protezione per la macchina virtuale hello." Errore 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">NUOVO</span> [errore di migrazione in tempo reale 23848 - macchina virtuale hello verrà spostata usando il tipo Live toobe. L'operazione potrebbe interrompere lo stato di protezione ripristino hello della macchina virtuale hello.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [L'abilitazione della protezione non è riuscita perché l'agente non è installato nel computer host.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [A causa di risorse di calcolo toolow - Impossibile trovare un host adatto per la macchina virtuale di replica hello.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Impossibile trovare un host adatto per la macchina virtuale di replica hello - scadenza toono rete logica associata.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Impossibile connettersi a computer host di replica toohello - connessione non può essere stabilita.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Ripristino
* Virtual Machine Manager non è possibile completare l'operazione host hello:
  * [Eseguire il failover toohello selezionato un punto di ripristino per la macchina virtuale: accesso generale negato.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Hyper-V toofail non riuscita su toohello selezionato il punto di ripristino per la macchina virtuale: operazione interrotta.  Provare un punto di ripristino più recente. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Una connessione con server hello non è stato stabilito (0x00002EFD).
    * [Hyper-V non è stato possibile tooenable la replica inversa per la macchina virtuale.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Hyper-V non è stato possibile tooenable replica per la macchina virtuale di macchina virtuale.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [Impossibile eseguire il commit del failover per la macchina virtuale.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [il piano di ripristino di Hello contiene macchine virtuali che non sono pronte per il failover pianificato.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [macchina virtuale Hello non è pronta per il failover pianificato.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [La macchina virtuale non è in esecuzione e non è spenta.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [Si è verificata un'operazione fuori banda in una macchina virtuale e il failover del commit non è riuscito.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Failover di test
  * [Impossibile avviare il failover perché il failover di test è in corso.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">NUOVO</span> Failover timeout con 'task PreFailoverWorkflow WaitForScriptExecutionTaskTimeout' a causa delle impostazioni di configurazione toohello hello il gruppo di sicurezza di rete associato a hello macchina virtuale o hello subnet toowhich hello macchina a cui appartiene. Fare riferimento troppo['task PreFailoverWorkflow WaitForScriptExecutionTaskTimeout'](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) per informazioni dettagliate.

### <a name="configuration-server-process-server-master-target"></a>Server di configurazione, server di elaborazione, server master di destinazione
* [host ESXi Hello in cui hello PS/CS è ospitato come una macchina virtuale ha esito negativo con una schermata di morte viola.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Risoluzione dei problemi del desktop remoto dopo il failover
* Molti clienti hanno dovuto affrontare problemi tooconnect toohello failover macchina virtuale in Azure. [Risoluzione dei problemi tooRDP documento in una macchina virtuale hello hello di utilizzare](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Aggiunta di un indirizzo IP pubblico in una macchina virtuale di Resource Manager
Se hello **Connetti** pulsante nel portale di hello è inattivo e non si è connessi tooAzure tramite una connessione VPN da sito a sito o di Express Route, è necessario toocreate e assegnare alla macchina virtuale un indirizzo IP pubblico per poter utilizzare remoto Shell desktop/condivisi. È quindi possibile aggiungere un indirizzo IP pubblico nell'interfaccia di rete hello della macchina virtuale hello.  

![Aggiunta di un indirizzo IP pubblico nell'interfaccia di rete hello del failover macchina virtuale](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
