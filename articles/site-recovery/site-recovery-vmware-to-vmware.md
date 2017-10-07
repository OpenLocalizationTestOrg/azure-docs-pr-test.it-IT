---
title: aaaReplicate le macchine virtuali VMware o sito tooanother server fisici (portale di Azure classico) | Documenti Microsoft
description: Usare questo articolo tooreplicate Windows/Linux o macchine virtuali VMware server fisici tooa sito secondario con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>Replicare le macchine virtuali VMware in locale o sito secondario di server fisici tooa nel portale di Azure classico hello

## <a name="overview"></a>Panoramica
In Azure Site Recovery, InMage Scout fornisce la replica in tempo reale tra più siti VMware locali. InMage Scout è incluso nelle sottoscrizioni del servizio Azure Site Recovery. 

## <a name="prerequisites"></a>Prerequisiti
**Account Azure**: sarà necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). [Altre informazioni](https://azure.microsoft.com/pricing/details/site-recovery/) sui prezzi di Site Recovery.

## <a name="step-1-create-a-vault"></a>Passaggio 1: Creare un insieme di credenziali
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su Nuovo > Gestione > Backup e Site Recovery (OMS). In alternativa, è possibile fare clic su Esplora > Insieme di credenziali dei servizi di ripristino > Aggiungi.
3. In **nome** specificare un insieme di credenziali di nome descrittivo tooidentify hello. Se è disponibile più di una sottoscrizione, selezionarne una.
4. In **Gruppo di risorse** creare un nuovo gruppo di risorse o selezionarne uno esistente. Specificare i campi toocomplete necessaria un'area di Azure.
5. In **percorso**, selezionare hello area geografica per l'insieme di credenziali hello. aree toocheck supportati, vedere [dei prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Se si desidera tooquickly accesso hello archivio da hello Dashboard fare clic su toodashboard Pin e quindi fare clic su Crea.
7. nuovo insieme di credenziali Hello verranno visualizzati nel Dashboard hello > tutte le risorse, e in hello principali servizi di ripristino di insiemi di credenziali di blade.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Passaggio 2: Configurare hello insieme di credenziali e scaricare i componenti di InMage Scout
1. Nel Pannello di insiemi di credenziali di servizi di ripristino hello selezionare l'insieme di credenziali e fare clic su impostazioni.
2. In **Impostazioni** > **Guida introduttiva** fare clic su **Site Recovery** > Passaggio 1: **Preparare l'infrastruttura** > **Obiettivo di protezione**.
3. In **obiettivi della protezione dati** selezionare toorecovery sito e selezionare Sì, con VMware vSphere Hypervisor. Fare quindi clic su OK.
4. In **installazione Scout**, fare clic su download di toodownload InMage Scout 8.0.1 GA software e la registrazione di chiave. file di programma di installazione di Hello per tutti hello componenti necessari nel file ZIP scaricato hello.

## <a name="step-3-install-component-updates"></a>Passaggio 3: Installare gli aggiornamenti dei componenti
Informazioni più recenti hello [aggiornamenti](#updates). Installare i file di aggiornamento hello nei server in hello seguente ordine:

1. Server RX se è presente
2. Server di configurazione
3. Server di elaborazione
4. Server di destinazione master
5. Server vContinuum
6. Server di origine (sia Windows che Linux)

Installare gli aggiornamenti di hello come indicato di seguito:

1. Scaricare hello [aggiornare](https://aka.ms/asr-scout-update5) file con estensione zip. Questo file con estensione zip contiene hello i seguenti file:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * Bit per update4 dell'agente utente per RHEL5, OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Estrarre i file con estensione zip hello.<br>
3. **Per server RX hello**: copia **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** server RX toohello ed estrarre i file. In hello estratto cartella, eseguire **/installare**.<br>
4. **Per il server di server o il processo di configurazione hello**: copia **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello server di configurazione e i server di elaborazione. Fare doppio clic su toorun è.<br>
5. **Per il server di destinazione master Windows hello**: hello tooupdate unificata, l'agente copia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello server di destinazione master. Fare doppio clic toorun è. Si noti che hello agente unificata è anche il server di origine toohello applicabile se l'origine non viene aggiornata fino a: Update4. Si deve essere installato nel server di origine hello nonché, come descritto più avanti in questo elenco.<br>
6. **Per server vContinuum hello**: copia **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum server.  Assicurarsi che dopo averla chiusa guidata vContinuum hello. Fare doppio clic su toorun file hello.<br>
7. **Per il server di destinazione master Linux hello**: hello tooupdate unificata, l'agente copia **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello server di destinazione master ed estrarre i file. In hello estratto cartella, eseguire **/installare**.<br>
8. **Per server di origine di Windows hello**: agente di aggiornamento 5 tooinstall in origine non è necessario se l'origine è già presente in update4. Se è minore di update4, applicare l'agente di aggiornamento 5 hello.
hello tooupdate unificata, l'agente copia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello server di origine. Fare doppio clic toorun è. <br>
9. **Per server di origine Linux hello**: tooupdate hello unificata agente, copiare la versione corrispondente di agente utente file toohello Linux server ed estrarre i file. In hello estratto cartella, eseguire **/installare**.  Esempio: Per il server a 6.7 64 RHEL, copiare **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello server ed estrarre i file. In hello estratto cartella, eseguire **/installare**.

## <a name="step-4-set-up-replication"></a>Passaggio 4: Configurare la replica
1. Configurare la replica tra hello origine e destinazione VMware siti.
2. Per istruzioni, utilizzare hello documentazione InMage Scout che viene scaricata con il prodotto hello. In alternativa, è possibile accedere documentazione hello come indicato di seguito:

   * [Note sulla versione](https://aka.ms/asr-scout-release-notes)
   * [Matrice di compatibilità](https://aka.ms/asr-scout-cm)
   * [manuale dell'utente](https://aka.ms/asr-scout-user-guide)
   * [manuale dell'utente RX](https://aka.ms/asr-scout-rx-user-guide)
   * [Guida all'installazione rapida](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Aggiornamenti
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 Update 5
Scout Update 5 è un aggiornamento cumulativo. Include tutte le correzioni hello di aggiornamento 1 fino a: update4 e seguendo le nuove correzioni di bug e miglioramenti.
Correzioni aggiunte dal ripristino automatico di sistema Scout update4 tooupdate5 sono componenti di destinazione e vContinuum tooMaster specifico. Se tutti i server di origine, destinazione Master, Server di configurazione, Server di elaborazione e RX sono già in ASR Scout update4 quindi è necessario tooapply aggiornamento 5 solo nel server di destinazione Master. 

**Nuovo supporto della piattaforma**
* SUSE Linux Enterprise Server 11 Service Pack 4 (SP4)

> [!NOTE]
> SLES 11 SP4 a 64 bit **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** include il pacchetto Scout di base con disponibilità generale **InMage_Scout_Standard_8.0.1 GA.zip**. Scaricare il pacchetto Scout GA dal portale come indicato nel [passaggio 1](#step-1-create-a-vault).
>

**Correzioni di bug e miglioramenti**

* Maggiore affidabilità del supporto per cluster Windows
    * Talvolta fissa alcune hello P2V MSCS diventi dischi cluster RAW dopo il ripristino
    * Ripristino cluster MSCS P2V fixed-ha esito negativo a causa di mancata corrispondenza di ordine toodisk
    * Correzione di un problema per cui l'operazione di aggiunta di dischi al cluster MSCS non riesce a causa della mancata corrispondenza delle dimensioni dei dischi
    * Correzione di un problema per cui il controllo di conformità dei mapping del cluster MSCS di origine con LUN RDM non riesce per quanto riguarda la verifica delle dimensioni
    * Protezione del cluster fixed-singolo nodo ha esito negativo a causa il problema di mancata corrispondenza tooSCSI 
    * Fixed-riapplicare la protezione del server di cluster Windows P2V hello ha esito negativo se sono presenti dischi del cluster di destinazione. 
    
* Durante la protezione di failback, se selezionato MT non è presente nel hello stesso ESXi server come quella di hello protetto macchina di origine (durante la protezione in avanti), quindi vContinuum preleva MT errato hello durante il recupero di Failback e successivamente l'operazione di ripristino ha esito negativo.

> [!NOTE]
> 
> * Di sopra di correzioni cluster P2V sono applicabili tooonly tali cluster MSCS fisico appena protette con update5 Scout ripristino automatico di sistema. correzioni di cluster tooavail hello in hello è già protetta cluster MSCS P2V con aggiornamenti precedenti, è necessario toofollow hello passaggi di aggiornamento sono elencati nella sezione hello 12, aggiornamento protected tooScout di cluster di MSCS P2V Update5 di [versione Scout ASR Note sulla](https://aka.ms/asr-scout-release-notes).
> 
> * Riapplicare la protezione del fisico del cluster MSCS, è possibile riutilizzare i dischi di destinazione esistente solo se è in fase di hello di riprotezione, hello stesso set di dischi sono attivi in ogni cluster hello nodi come fossero quando inizialmente protetto. Se non esistono passaggi manuali come indicato nella sezione 12 di [note sulla versione di ripristino automatico di sistema Scout](https://aka.ms/asr-scout-release-notes) troppo spostare hello destinazione lato dischi toohello corretti dell'archivio dati percorso toore uso loro durante la protezione. Se si ricrea la protezione del cluster MSCS hello in modalità P2V senza seguire i passaggi di aggiornamento creerà nuovo disco nel server ESXi di destinazione hello. È necessario toomanually delete hello vecchi dischi dall'archivio dati hello.
> 
> * Ogni volta che origine SLES11 o SLES11 con qualsiasi server di service pack è stato riavviato correttamente, quindi uno deve contrassegnare manualmente hello **radice** disco coppie di replica per risincronizzare come non riceveranno notifiche in CX UI. Se non sono presenti ' contrassegno hello radice disco per la risincronizzazione, potrebbero verificarsi problemi di integrità (DI) di dati.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1 Update 4
Scout Update 4 è un aggiornamento cumulativo. Include tutte le correzioni hello di aggiornamento 1 fino a: update3 e seguendo le nuove correzioni di bug e miglioramenti.

**Nuovo supporto della piattaforma**

* È stato aggiunto il supporto per vCenter/vSphere 6.0, 6.1 e 6.2
* È stato aggiunto il supporto per i sistemi operativi Linux seguenti:
  * Red Hat Enterprise Linux (RHEL)7.0, 7.1 e 7.2
  * CentOS 7.0, 7.1 e 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> RHEL/CentOS 7 a 64 bit: **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** viene fornito nel pacchetto base Scout GA **InMage_Scout_Standard_8.0.1 GA.zip**. Scaricare il pacchetto Scout GA dal portale come indicato nel [passaggio 1](#step-1-create-a-vault).
>
>

**Correzioni di bug e miglioramenti**

* Arresto migliorato di gestione seguenti Linux OSes e tooprevent cloni problemi indesiderati risincronizzare.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* Per Linux, l'accesso completo della cartella delle autorizzazioni nella directory di installazione unificata agente sono ora limitato solo toohello utente locale.
* In Windows, si verifica il problema di timeout durante il rilascio di segnalibri di coerenza comuni distribuiti sulle applicazioni distribuite con carico elevato, come i cluster di SQL e SharePoint.
* Aggiunta della correzione relativa ai log nel programma di installazione di base di CX.
* Collegamento di download di VMware vCLI 6.0 viene aggiunto tooWindows installazione base di destinazione Master.
* Aggiunta di ulteriori controlli e log per le modifiche delle configurazioni di rete durante il failover e le esercitazioni sul ripristino di emergenza.
* Non sono segnalato toohello CX memorizzazione talvolta informazioni.  
* Per un cluster fisico, l'operazione di ridimensionamento del volume tramite la procedura guidata vContinuum non riesce se è stata eseguita la riduzione del volume di origine.
* Cluster di protezione non è riuscita con errore "Firma del disco hello toofind non riuscito" quando il disco di cluster è su disco PRDM.
* Arresto anomalo del server di trasporto cxps a causa di un'eccezione non compresa nell'intervallo.
* Ora è possibile ridimensionare il nome del server e le colonne IP nella pagina di installazione push della procedura guidata vContinuum.
* Miglioramenti dell'API RX
  * Fornisce i cinque punti di coerenza comuni disponibili più recenti (con tag Solo garantiti).
  * Fornisce i dettagli di capacità e lo spazio disponibile per tutti hello dispositivi protetti.
  * Fornisce lo stato del driver Scout nel server di origine.

> [!NOTE]
> * Il pacchetto base **InMage_Scout_Standard_8.0.1_GA.zip** ora contiene il file **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** del programma di installazione di base di CX aggiornato e il file **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe** del programma di installazione di base di Master di Windows. Per tutte le nuove installazioni, usare la nuova GA di CX e Windows Master Target.
> * Update 4 può essere applicato direttamente in 8.0.1 GA.
> * il server di configurazione di Hello e RX aggiornamenti non possono essere annullati dopo vengono applicati nel sistema hello.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery Scout 8.0.1 Update 3
Update 3 include seguente hello miglioramenti e correzioni di bug:

* il server di configurazione di Hello e RX insieme di credenziali Site Recovery toohello tooregister esito negativo quando sono dietro il proxy di hello.
* Hello numero di ore che hello obiettivo del punto di ripristino (RPO) non viene soddisfatta non viene aggiornato nel rapporto di stato hello.
* il server di configurazione di Hello non sincronizzato RX quando i dettagli sull'hardware ESX hello o dettagli rete contengono caratteri UTF-8.
* I controller di dominio di Windows Server 2008 R2 non tooboot dopo il ripristino.
* La sincronizzazione offline non funziona come previsto.
* Dopo il failover della macchina virtuale (VM), l'eliminazione della coppia di replica si blocca in hello CX UI per molto tempo e non è possibile completare il failback hello o operazione di ripresa.
* Generale sono state ottimizzate le operazioni di snapshot che vengono eseguite dal processo di verifica coerenza hello toohelp ridurre applicazione disconnette come i client SQL.
* prestazioni di Hello dello strumento di verifica coerenza hello (VACP.exe) sono stata migliorata grazie alla riduzione dell'utilizzo della memoria hello è necessaria per la creazione di snapshot in Windows.
* arresto anomalo del servizio di installazione push Hello quando password hello è maggiore di 16 caratteri.
* vContinuum non verifica e richiedere le nuove credenziali di vCenter quando vengono modificate le credenziali di hello.
* In Linux, gestione della cache di destinazione master hello (cachemgr) non scarica i file dal server di elaborazione hello, che comporta la limitazione della coppia di replica.
* Quando l'ordine di hello fisico failover cluster (MSCS) disco è non hello stesso in tutti i nodi di hello, la replica non è impostata per alcuni dei volumi del cluster hello.
  <br/>Si noti che tale cluster hello deve toobe protetta di nuovo tootake vantaggio di questa correzione.  
* La funzionalità SMTP non funziona come previsto dopo l'aggiornamento da 7.1 Scout tooScout 8.0.1 RX.
* Altre statistiche sono state aggiunte nel registro hello per tempo hello hello rollback operazione tootrack impiegato toocomplete è.
* È stato aggiunto il supporto per i sistemi operativi Linux nel server di origine hello:
  * Red Hat Enterprise Linux (RHEL) 6 Update 7
  * CentOS 6 Update 7
* Hello CX e dell'interfaccia utente RX può ora Visualizza notifica di hello per coppia hello, che entra in modalità di bitmap.
* Hello correzioni seguenti sono state aggiunte in ricezione:

| **Descrizione del problema** | **Procedure di implementazione** |
| --- | --- |
| Bypass dell'autorizzazione tramite manomissione dei parametri |Accesso limitato di utenti toonon-applicabile. |
| Richiesta intersito falsa |Concetto di token pagina implementato hello, che genera in modo casuale per ogni pagina. <br/>Con questa operazione, verrà visualizzato: <li> È presente una singola accesso istanza per hello stesso utente.</li><li>Aggiornamento della pagina non funziona, si verrà reindirizzati toohello dashboard.</li> |
| Caricamento di file dannosi |Estensioni di file con accesso limitato toocertain. Le estensioni consentite sono: 7z, aiff, asf, avi, bmp, csv, doc, docx, fla, flv, gif, gz, gzip, jpeg, jpg, log, mid, mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar, tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml e zip. |
| Scripting intersito persistente |Aggiunta di convalide dell'input. |

> [!NOTE]
> * Tutti gli aggiornamenti di Site Recovery sono cumulativi. Update 3 dispone di tutte le correzioni hello Update 1 e 2 di aggiornamento. Update 3 può essere applicato direttamente in 8.0.1 GA.
> * il server di configurazione di Hello e RX aggiornamenti non possono essere annullati dopo vengono applicati nel sistema hello.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 Update 2 (aggiornamento del 3 dicembre 15)
Le correzioni apportate in Update 2 includono:

* **Server di configurazione**: correzione di un problema che impediva funzionalità di controllo libero di hello 31 giorni lavorativi come previsto quando hello del server di configurazione è stato registrato in Site Recovery.
* **Agente unificata**: correzione di un problema in Update 1 che ha comportato l'aggiornamento di hello non viene installato nel server di destinazione master hello quando è stato aggiornato dalla versione 8.0 too8.0.1.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 Update 1
Update 1 include seguente hello nuove funzionalità e correzioni di bug:

* 31 giorni di protezione gratuita per istanza del server. In questo modo si tootest funzionalità o configurare un di prova.
  * Tutte le operazioni nel server di hello, inclusi il failover e failback, sono disponibili gratuitamente per hello 31 giorni prima, a partire dal hello un server prima di tutto è protetto con Scout ripristino del sito.
  * Da hello 32nd giorno in poi, ogni server protetti verrà addebitato con frequenza di hello istanza standard per il sito appartiene al cliente di Azure Site Recovery protezione tooa.
  * In qualsiasi momento, è disponibile nella pagina Dashboard hello dell'insieme di credenziali di Azure Site Recovery hello numero hello di server protetti che attualmente addebitati.
* Aggiunta del supporto per vCLI (vSphere Command-Line Interface) 5.5 Update 2.
* Aggiunto il supporto per i sistemi operativi Linux nel server di origine hello:
  * RHEL 6 Update 6
  * RHEL 5 Update 11
  * CentOS 6 Update 6
  * CentOS 5 Update 11
* Correzioni di bug tooaddress. hello seguenti problemi:
  * Registrazione dell'insieme di credenziali ha esito negativo per il server di configurazione hello o RX.
  * I volumi del cluster non vengono visualizzati come previsto quando le macchine virtuali vengono riprotette durante la ripresa.
  * Il failback non riesce se il server di destinazione master hello è ospitato in un altro server ESXi da macchine virtuali di produzione on-premise hello.
  * Autorizzazioni di file di configurazione vengono modificate quando si esegue l'aggiornamento too8.0.1, che influisce sulla protezione e le operazioni.
  * soglia di Hello la risincronizzazione non è applicata come previsto, con la conseguente tooinconsistent funzionamento della replica.
  * le impostazioni RPO Hello non vengono visualizzati correttamente nell'interfaccia di server di configurazione hello. il valore di dati non compresso Hello Mostra in modo errato il valore di hello compresso.
  * l'operazione di rimozione Hello non comporta l'eliminazione come previsto nella procedura guidata vContinuum hello e la replica non verrà eliminata dall'interfaccia di server di configurazione hello.
  * Nella procedura guidata vContinuum hello disco hello è selezionato automaticamente quando si fa clic **dettagli** nella visualizzazione disco hello durante la protezione delle macchine virtuali MSCS.
  * Durante l'hello fisica a virtuale (P2V) dello scenario, Servizi HP necessari, ad esempio CIMnotify e CqMgHost, non sono toomanual spostato nel ripristino della macchina virtuale. Questo causa tempo di avvio aggiuntivo.
  * Protezione delle macchine virtuali Linux non riesce quando sono presenti più di 26 dischi nel server di destinazione master hello.

## <a name="next-steps"></a>Passaggi successivi
Registra le domande che sono presenti hello [forum di servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
