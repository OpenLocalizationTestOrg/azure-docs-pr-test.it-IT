---
title: procedure consigliate aaaBest per Array virtuale StorSimple | Documenti Microsoft
description: Le procedure consigliate hello per distribuire e gestire hello Array virtuale StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>Procedure consigliate per l'array virtuale StorSimple
## <a name="overview"></a>Panoramica
Array virtuale Microsoft Azure StorSimple è una soluzione di archiviazione integrata che consente di gestire le attività di archiviazione tra un dispositivo virtuale locale eseguito in un hypervisor e la risorsa di archiviazione cloud di Microsoft Azure. Array virtuale StorSimple è una matrice fisici serie conveniente, efficiente toohello alternativo 8000. array virtuale Hello può eseguire sull'infrastruttura esistente di hypervisor supporta hello iSCSI sia protocolli SMB hello ed è ideale per scenari con office/filiali remote. Per ulteriori informazioni sulle soluzioni di StorSimple hello, andare troppo[Panoramica di Microsoft Azure StorSimple](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx).

Questo articolo vengono illustrate procedure consigliate hello implementate durante l'installazione iniziale di hello, distribuzione e gestione di hello Array virtuale StorSimple. Queste procedure consigliate per fornire indicazioni convalidati per l'installazione di hello e la gestione della matrice virtuale. In questo articolo è indirizzato verso hello IT, amministratori di distribuire e gestire hello matrici virtuali nei centri dati.

È consigliabile una verifica periodica di hello best practices toohelp verificare che il dispositivo è ancora conforme quando vengono apportate modifiche toohello il programma di installazione o operazione di flusso. In caso di problemi durante l'implementazione di queste procedure consigliate relative all'array virtuale, [Contattare il supporto tecnico Microsoft](storsimple-virtual-array-log-support-ticket.md) per assistenza.

## <a name="configuration-best-practices"></a>Procedure consigliate per la configurazione
Queste procedure consigliate per coprire le linee guida relative hello necessario toobe seguito durante l'installazione iniziale di hello e la distribuzione di matrici virtuale hello. Queste procedure consigliate per includere tali toohello correlati al provisioning della macchina virtuale hello, le impostazioni di criteri di gruppo, il ridimensionamento, impostazione hello di rete, configurare gli account di archiviazione e la creazione di condivisioni e volumi per hello array virtuale. 

### <a name="provisioning"></a>Provisioning
Array virtuale StorSimple è una macchina virtuale (VM), il provisioning in hypervisor hello (Hyper-V o VMware) del server host. Durante il provisioning di macchina virtuale hello, verificare che l'host è in grado di toodedicate sufficienti risorse. Per ulteriori informazioni, visitare troppo[requisiti minimi](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision una matrice.

Implementare hello seguono le procedure consigliate durante il provisioning di array virtuale hello:

|  | Hyper-V | VMware |
| --- | --- | --- |
| **Tipo di macchina virtuale** |**Generazione 2** per l'uso con Windows Server 2012 o versione successiva e un'immagine *VHDX* . <br></br> **Generazione 1** per l'uso con Windows Server 2008 o versione successiva e un'immagine *VHD* . |Quando si usa un'immagine *VMDK* , usare macchine virtuali versione da 8 a 11. |
| **Tipo di memoria** |Configurare come **memoria statica**. <br></br> Non utilizzare hello **memoria dinamica** opzione. | |
| **Tipo di disco dati** |Effettuare il provisioning come **espansione dinamica**.<br></br> **dimensioni fisse** richiedono molto tempo. <br></br> Non utilizzare hello **differenze** opzione. |Hello utilizzare **con thin provisioning** opzione. |
| **Modifica dei dischi dati** |L'espansione o la riduzione non è consentita. Toodo un tentativo comporta pertanto hello perdita di tutti i dati locali hello sul dispositivo. |L'espansione o la riduzione non è consentita. Toodo un tentativo comporta pertanto hello perdita di tutti i dati locali hello sul dispositivo. |

### <a name="sizing"></a>Ridimensionamento
Quando si ridimensionano l'Array virtuale StorSimple, prendere in considerazione hello seguenti fattori:

* Prenotazione locale per volumi o condivisioni. Circa 12% di spazio di hello è riservato a livello locale di hello per ogni volume a livelli di provisioning o la condivisione. Circa 10% di spazio hello è riservata anche per un volume aggiunto in locale per il file system.
* Sovraccarico di snapshot. Circa 15% di spazio a livello locale hello è riservato per gli snapshot.
* Necessità di ripristini. Se l'operazione Ripristina come una nuova operazione di ridimensionamento devono tener conto spazio hello necessario per il ripristino. Eseguire il ripristino è tooa condivisione o volume di hello stessa dimensione.
* È necessario allocare una parte del buffer per un'eventuale crescita imprevista.

In base ai precedenti fattori hello, hello ridimensionamento requisiti può essere rappresentato da hello seguente equazione:

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

Hello esempi seguenti viene illustrato come è possibile ridimensionare un array virtuale in base alle esigenze.

#### <a name="example-1"></a>Esempio 1:
L'array virtuale, si desidera toobe in grado di

* Effettuare il provisioning di un volume o una condivisione a livelli di 2 TB.
* Effettuare il provisioning di un volume o una condivisione a livelli di 1 TB.
* Effettuare il provisioning di un volume o una condivisione aggiunta in locale di 300 GB.

Per hello precedente volumi o condivisioni, consentire di calcolare i requisiti di spazio hello a livello locale hello.

In primo luogo, per ogni volume o condivisione a livelli, prenotazione locale sarebbe uguale too12% delle dimensioni di volume o condivisione hello. Per volume o condivisione di hello aggiunto in locale, la prenotazione locale è 10% di hello in locale è bloccato (inoltre toohello provisioning dimensioni) dimensioni del volume o condivisione. In questo esempio sono necessari

* Prenotazione locale di 240 GB, per un volume o una condivisione a livelli di 2 TB.
* Prenotazione locale di 120 GB (per un volume o una condivisione a livelli di 1 TB).
* 330 GB per il volume aggiunto in locale o una condivisione (aggiunta di 10% delle dimensioni di prenotazione locale toohello il provisioning di 300 GB)

è Hello lo spazio totale richiesto a livello locale hello finora: 240 GB + 120 GB + 330 GB = 690 GB.

In secondo luogo, è necessario almeno una quantità di spazio a livello locale hello come una sola prenotazione maggiore hello. Nel caso in cui è necessario toorestore da uno snapshot nel cloud, viene utilizzato questo importo supplementare. In questo esempio, la prenotazione locale più grande di hello è 330 GB (inclusi prenotazione per il file system), quindi aggiungere tale toohello GB 690: 690 GB + 330 GB = 1020 GB.
Se sono stati eseguiti i ripristini successivi aggiuntivi, è sempre possibile liberare spazio su hello dall'operazione di ripristino precedente hello.

In terzo luogo, è necessario il 15% del totale locale spazio finora toostore snapshot locali, in modo che solo l'85% di esso sarà disponibile. In questo esempio saranno circa 1020 GB = 0,85&ast;TB del disco dati con provisioning. In tal caso, si sarebbe disco di dati di provisioning hello (1020&ast;(1/0.85)) = 1200 GB = 1,20 TB ~ 1,25 TB (arrotondamento quartile toonearest)

Considerando la crescita imprevista e i nuovi ripristini, è consigliabile effettuare il provisioning di un disco locale di circa 1,25-1,5 TB.

> [!NOTE]
> È inoltre consigliabile che tale disco locale hello il thin provisioning. Si consiglia quanto spazio ripristino hello è necessaria solo quando si desidera che i dati toorestore meno di cinque giorni. Ripristino a livello di elemento consente dati toorestore per hello ultimi cinque giorni senza hello spazio aggiuntivo per il ripristino.


#### <a name="example-2"></a>Esempio 2
L'array virtuale, si desidera toobe in grado di

* Effettuare il provisioning di un volume a livelli di 2 TB.
* Effettuare il provisioning di un volume aggiunto in locale di 300 GB.

In base al 12% della prenotazione di spazio locale per i volumi o le condivisioni a livelli e al 10% per i volumi o le condivisioni aggiunte in locale, sono necessari

* Prenotazione locale di 240 GB (per un volume o una condivisione a livelli di 2 TB).
* 330 GB per il volume aggiunto in locale o una condivisione (aggiunta di 10% di spazio di 300 GB provisioning toohello prenotazione locale)

È lo spazio totale richiesto a livello locale hello: 240 GB + 330 GB = 570 GB

Hello locale spazio minimo necessario per il ripristino è 330 GB.

15% del disco totale è snapshot toostore utilizzato in modo che solo 0.85 è disponibile. In tal caso, sono di dimensioni del disco hello (900&ast;(1/0.85)) = TB 1,06 ~ 1,25 TB (arrotondamento quartile toonearest)

Considerando l'eventuale crescita imprevista, è consigliabile effettuare il provisioning di un disco locale di 1,25-1,5 TB.

### <a name="group-policy"></a>Criteri di gruppo
Criteri di gruppo sono un'infrastruttura che consente di tooimplement configurazioni specifiche per gli utenti e computer. Impostazioni di criteri di gruppo sono contenute negli oggetti Criteri di gruppo (GPO), che sono collegato toohello seguenti contenitori di servizi di dominio Active Directory (AD DS): siti, domini o unità organizzative (OU). 

Se l'array virtuale appartiene al dominio, oggetti Criteri di gruppo può essere applicato tooit. Questi oggetti Criteri di gruppo è possibile installare applicazioni, ad esempio un software antivirus che può influire negativamente sulle operazione hello di hello Array virtuale StorSimple.

È quindi consigliabile:

* Assicurarsi che l'array virtuale sia nella propria unità organizzativa (OU) per Active Directory.
* Assicurarsi che nessun oggetti Criteri di gruppo (GPO) siano array virtuale tooyour applicato. È possibile bloccare l'ereditarietà tooensure che hello array virtuale (nodo figlio) non viene ereditato automaticamente oggetti Criteri di gruppo dall'oggetto padre hello. Per ulteriori informazioni, visitare troppo[bloccare l'ereditarietà](https://technet.microsoft.com/library/cc731076.aspx).

### <a name="networking"></a>Rete
configurazione di rete Hello per l'array virtuale viene eseguita tramite l'interfaccia utente web locale hello. Un'interfaccia di rete virtuale viene abilitata tramite hypervisor hello in cui viene eseguito il provisioning di array virtuale hello. Hello utilizzare [le impostazioni di rete](storsimple-virtual-array-deploy3-fs-setup.md) pagina indirizzo IP dell'interfaccia tooconfigure hello rete virtuale, subnet e gateway.  È anche possibile configurare i server DNS primario e secondario di hello, le impostazioni dell'ora e le impostazioni proxy opzionali per il dispositivo. La maggior parte della configurazione di rete hello è un'installazione singola. Hello revisione [StorSimple requisiti di rete](storsimple-ova-system-requirements.md#networking-requirements) array virtuale hello di toodeploying precedente.

Quando si distribuisce l'array virtuale, è consigliabile seguire queste procedure consigliate:

* Verificare che tale rete hello in cui hello array virtuale viene distribuita sempre con hello capacità toodedicate 5 della larghezza di banda Mbps Internet (o più).
  
  * Necessità di larghezza di banda Internet varia a seconda del caratteristiche del carico di lavoro e la frequenza di modifica hello.
  * modifica dei dati che può essere gestito Hello è direttamente proporzionale tooyour larghezza di banda Internet. Ad esempio, quando si esegue un backup, una larghezza di banda 5 Mbps può supportare una modifica dei dati di circa 18 GB in 8 ore. Con una larghezza di banda quattro volte maggiore (20 Mbps), è possibile gestire una modifica dei dati quadrupla (72 GB).
* Verificare toohello connettività Internet è sempre disponibile. Dispositivi di toohello connessioni Internet sporadici o non affidabili possono comportare una perdita di accesso toodata nel cloud hello e potrebbe causare una configurazione non supportata.
* Se si prevede di toodeploy il dispositivo come un server iSCSI:
  
  * È consigliabile disabilitare hello **ottenere automaticamente l'indirizzo IP** opzione (DHCP).
  * Configurare gli indirizzi IP statici. È necessario configurare un server DNS primario e secondario.
  * Se la definizione di più interfacce di rete nella matrice virtuale, solo hello prima interfaccia di rete (per impostazione predefinita, questa interfaccia è **Ethernet**) può raggiungere cloud hello. tipo di hello toocontrol di traffico, è possibile creare più interfacce di rete virtuale nell'array virtuale (configurato come server iSCSI) e connettersi a tali subnet toodifferent interfacce.
* toothrottle hello larghezza di banda cloud solo (usato dall'array virtuale hello), configurare la limitazione sul hello router o firewall di hello. Se si definisce la limitazione delle richieste nell'hypervisor, rallentamento tutti i protocolli di hello incluso iSCSI e SMB anziché semplicemente hello larghezza di banda cloud.
* Assicurarsi che sia abilitata la sincronizzazione dell'ora per hypervisor. Se con Hyper-V, selezionare l'array virtuale in Hyper-V Manager hello, andare troppo**impostazioni &gt; Integration Services**e assicurarsi che hello **sincronizzazione dell'ora** è selezionata.

### <a name="storage-accounts"></a>Account di archiviazione
L'array virtuale StorSimple può essere associato a un singolo account di archiviazione. Questo account di archiviazione potrebbe essere un account di archiviazione generato automaticamente un account di hello stessa sottoscrizione del servizio hello o un account di archiviazione relativi tooanother sottoscrizione. Per ulteriori informazioni, vedere come troppo[gestire gli account di archiviazione per l'array virtuale](storsimple-virtual-array-manage-storage-accounts.md).

Hello utilizzare seguenti indicazioni per gli account di archiviazione associati l'array virtuale.

* Durante il collegamento più array virtuale con un singolo account di archiviazione, è necessario includere la capacità massima hello (64 TB) di un array virtuale e la dimensione massima hello (500 TB) per un account di archiviazione. Limita il numero di hello di matrici virtuale ingrandita che può essere associato a tale tooabout di account di archiviazione 7.
* Quando creare un nuovo account di archiviazione
  
  * È consigliabile crearlo in hello area più vicina toohello office/succursale remota in cui è distribuito toominimize latenze l'Array virtuale StorSimple.
  * Tenere presente che non è possibile spostare un account di archiviazione tra aree diverse. Non è inoltre possibile spostare un servizio tra sottoscrizioni.
  * Utilizzare un account di archiviazione che implementa la ridondanza tra i Data Center hello. L'archiviazione con ridondanza geografica, l'archiviazione con ridondanza della zona e l'archiviazione con ridondanza locale sono tutte supportate per l'uso con l'array virtuale. Per ulteriori informazioni sui diversi tipi di hello di account di archiviazione, andare troppo[la replica di archiviazione di Azure](../storage/common/storage-redundancy.md).

### <a name="shares-and-volumes"></a>Condivisioni e volumi
Per l'array virtuale StorSimple è possibile effettuare il provisioning di condivisioni quando è configurato come un file server e di volumi quando è configurato come server iSCSI. procedure consigliate di Hello per la creazione di condivisioni e i volumi sono correlate il tipo di dimensione e hello toohello configurato.

#### <a name="volumeshare-size"></a>Dimensioni di volumi o condivisioni
Nell'array virtuale è possibile effettuare il provisioning di condivisioni quando è configurato come un file server e di volumi quando è configurato come server iSCSI. procedure consigliate per la creazione di condivisioni e volumi Hello toohello dimensioni correlate e hello tipo configurato. 

Tenere hello presente seguono le procedure consigliate durante il provisioning di condivisioni o volumi nel dispositivo virtuale.

* dimensione di Hello file dimensioni relativo toohello il provisioning di una condivisione a livelli può influire sulle prestazioni di suddivisione in livelli hello. L'utilizzo di file di grandi dimensioni può comportare il rallentamento della suddivisione in livelli. Quando si utilizzano file di grandi dimensioni, è consigliabile che file più grande di hello è minore di 3% delle dimensioni della condivisione hello.
* Un massimo di 16 volumi o condivisioni può essere creato nell'array virtuale hello. Per i limiti delle dimensioni hello di hello localmente bloccato e a livelli di volumi e delle condivisioni, si riferiscono sempre toohello [Array virtuale StorSimple limita](storsimple-ova-limits.md).
* Quando si crea un volume, fattore hello previsto utilizzo dei dati, nonché la crescita futura. volume Hello non può essere espanso in un secondo momento.
* Dopo aver creato il volume di hello, sarà possibile ridurre le dimensioni di hello del volume di hello in StorSimple.
* Quando la scrittura di tooa a più livelli di volume in StorSimple, quando i dati di volume hello raggiungono una determinata soglia (toohello relativo locale spazio riservato per il volume di hello), i/o hello sono limitato. Continuare toowrite toothis volume rallenta hello i/o in modo significativo. Sebbene non sia possibile scrivere tooa a livelli a volume oltre la capacità disponibile (non attivamente interrotta utente hello dalla scrittura oltrepassato la capacità di hello provisioning), viene visualizzato un effetto toohello notifica di avviso che è sovrascritta. Dopo aver visualizzato l'avviso hello, è necessario intraprendere misure correttive, ad esempio dati di volume hello di eliminazione (espansione del volume non è supportato).
* Per casi di utilizzo di ripristino di emergenza, come numero di hello di/volumi di condivisioni consentiti è 16 e hello massimo numero di condivisioni/volumi che possono essere elaborati in parallelo è 16, numero hello di condivisioni/volumi hanno influiscono sul RPO e RTO.

#### <a name="volumeshare-type"></a>Tipo di volumi o condivisioni
StorSimple supporta due tipi di volume o condivisione in base all'utilizzo di hello: aggiunto in locale e a livelli. I volumi aggiunti in locale e delle condivisioni sono stati sottoposti a thick provisioning mentre hello volumi a livelli e delle condivisioni con thin provisioning. Non è possibile convertire un volume aggiunto in locale o condivisione tootiered o *viceversa* dopo averlo creato.

È consigliabile implementare hello seguono le procedure consigliate durante la configurazione StorSimple. volumi o condivisioni:

* Identificare il tipo di volume hello in base ai carichi di lavoro hello che si desidera toodeploy prima di creare un volume. Usare volumi aggiunti in locale per i carichi di lavoro che richiedono garanzie locali per i dati, anche durante un'interruzione del servizio cloud, e latenze cloud basse. Dopo aver creato un volume nell'array virtuale, è possibile modificare il tipo di volume hello da tootiered aggiunti in locale o *viceversa*. Ad esempio, creare volumi aggiunti in locale quando si distribuiscono carichi di lavoro SQL o carichi di lavoro che ospitano macchine virtuali e usare invece volumi a livelli per carichi di lavoro di condivisione file.
* Selezionare l'opzione di hello per i dati dell'archivio usati di frequente quando si lavora con le dimensioni dei file di grandi dimensioni. Dimensioni del blocco deduplicazione maggiore di 512 KB viene utilizzata quando questa opzione è abilitata trasferimento dei dati di hello tooexpedite toohello cloud.

#### <a name="volume-format"></a>Formato del volume
Dopo aver creato i volumi StorSimple sul server iSCSI, è necessario tooinitialize e montaggio hello formato volumi. Questa operazione viene eseguita nel dispositivo StorSimple tooyour di hello host connesso. Procedure consigliate seguenti sono consigliate quando montaggio e formattazione di volumi nell'host di StorSimple hello.

* Eseguire una formattazione veloce in tutti i volumi StorSimple.
* Quando si formatta un volume StorSimple, usare dimensioni dell'unità di allocazione di 64 KB. Il valore predefinito è 4 KB. 64 KB AUS Hello è basato su test eseguiti internamente per carichi di lavoro StorSimple comuni e altri carichi di lavoro.
* Quando tramite hello StorSimple Array virtuale configurato come server iSCSI, non utilizzare i volumi con spanning o i dischi dinamici come questi volumi o dischi non sono supportati da StorSimple.

#### <a name="share-access"></a>Accesso alle condivisioni
Quando si creano condivisioni nel file server dell'array virtuale, seguire queste linee guida:

* Quando si crea una condivisione, assegnare un gruppo di utenti come amministratore della condivisione, invece di un singolo utente.
* È possibile gestire le autorizzazioni NTFS hello dopo la creazione di condivisione hello modificando condivisioni hello tramite Esplora risorse.

#### <a name="volume-access"></a>Accesso ai volumi
Quando si configurano i volumi iSCSI hello dell'Array virtuale StorSimple, è importante toocontrol accesso laddove necessario. toodetermine che ospitano i server possa accedere ai volumi, creare e associare i record di controllo di accesso (ACR) con i volumi StorSimple.

Utilizzare hello seguono le procedure consigliate quando si configura ACR per i volumi StorSimple:

* Associare sempre almeno un ACT a un volume.

* Quando si assegnano più di un volume di tooa ACR, verificare che il volume di hello non è esposta in modo in cui possono accedere contemporaneamente da più di un host non cluster. Se è stato assegnato più ACR tooa volume, un messaggio di avviso viene visualizzata per tooreview è la configurazione.

### <a name="data-security-and-encryption"></a>Sicurezza e crittografia dei dati
L'Array virtuale StorSimple include funzionalità di sicurezza e la crittografia di dati che garantiscono hello riservatezza e integrità dei dati. Quando si usano queste funzionalità, è opportuno seguire queste procedure consigliate: 

* Prima di hello dati vengono inviati dal cloud toohello array virtuale, è necessario definire una crittografia toogenerate chiave AES-256 crittografia dell'archiviazione cloud. Questa chiave non è necessaria se i dati vengono crittografati toobegin con. Hello chiave può essere generata e protetto con un sistema di gestione delle chiavi, ad esempio [insieme di credenziali chiave Azure](../key-vault/key-vault-whatis.md).
* Quando la configurazione di account di archiviazione hello tramite il servizio StorSimple Manager hello, assicurarsi di abilitare di hello SSL modalità toocreate un canale sicuro per la comunicazione di rete tra il dispositivo StorSimple e hello cloud.
* Le chiavi di rigenerare hello per gli account di archiviazione (tramite l'accesso del servizio di archiviazione di Azure hello) periodicamente tooaccount per qualsiasi modifica tooaccess basato su hello modificato elenco degli amministratori.
* L'array virtuale dati vengono compressi e deduplicati prima che venga inviato tooAzure. Non è consigliabile l'utilizzo di servizio di ruolo deduplicazione dati hello nell'host Windows Server.

## <a name="operational-best-practices"></a>Procedure operative consigliate
Hello procedure consigliate per sono linee guida da seguire durante l'operazione di array virtuale hello o gestione quotidiana hello. Queste procedure coprire determinate attività di gestione, ad esempio l'esecuzione di backup, ripristino da un set di backup, eseguire un failover, la disattivazione e l'eliminazione hello matrice, monitoraggio dell'utilizzo di sistema e integrità, e virus l'esecuzione di analisi nella matrice virtuale.

### <a name="backups"></a>Backup
backup dei dati di Hello nell'array virtuale cloud toohello in due modi, valore predefinito è automatico il backup giornaliero di hello intero dispositivo a partire dal 22:30 o tramite un backup su richiesta manuale. Per impostazione predefinita, il dispositivo di hello crea automaticamente gli snapshot cloud giornalieri di tutti i dati di hello che risiedono su di esso. Per ulteriori informazioni, visitare troppo[backup l'Array virtuale StorSimple](storsimple-virtual-array-backup.md).

Hello frequenza e conservazione associati backup predefiniti hello non può essere modificati, ma è possibile configurare ora hello in cui hello i backup giornalieri vengono avviati ogni giorno. Per configurare l'ora di inizio hello hello automatizzato backup, è consigliabile che:

* Pianificare i backup per le ore non di punta. L'ora di inizio del backup non deve coincidere con numerose operazioni di I/O dell'host.
* Avviare un backup su richiesta manuale durante la pianificazione tooperform un failover del dispositivo o una finestra di manutenzione preventiva toohello, dati hello tooprotect l'array virtuale.

### <a name="restore"></a>Ripristino
È possibile ripristinare da un set di backup in due modi: tooanother volume o condivisione file oppure eseguire un ripristino a livello di elemento (disponibile solo in un array virtuale configurato come un file server). Ripristino a livello di elemento consente un ripristino granulare di file e cartelle da un backup nel cloud di tutte le condivisioni hello toodo nel dispositivo StorSimple hello. Per ulteriori informazioni, visitare troppo[ripristinare da un backup](storsimple-virtual-array-clone.md).

Quando si esegue un ripristino, è possibile mantenere hello indicazioni presenti:

* L'array virtuale StorSimple non supporta il ripristino sul posto. Può tuttavia essere facilmente ottenuta da un processo in due passaggi: liberare spazio virtuale hello di matrice e quindi ripristinare tooanother volume o condivisione.
* Durante il ripristino da un volume locale, tenere ripristino hello presente sarà un'operazione a esecuzione prolungata. Se il volume di hello rapidamente potrebbe portare in linea, dati hello continuano toobe Alluminosilicato in background hello.
* tipo di volume Hello rimane uguale hello durante il processo di ripristino hello. Viene ripristinato un volume a livelli tooanother a livelli a volume e un volume aggiunto in locale tooanother volume aggiunto in locale.
* Quando durante il tentativo toorestore un volume o una condivisione da un set di backup, se il processo di ripristino di hello non riesce, un volume di destinazione o una condivisione può comunque creato nel portale di hello. È importante eliminare il volume di destinazione inutilizzati oppure condividere hello portale toominimize i futuri problemi causati da questo elemento.

### <a name="failover-and-disaster-recovery"></a>Failover e ripristino di emergenza
Un failover del dispositivo consente toomigrate i dati da un *origine* dispositivo in hello datacenter tooanother *destinazione* dispositivo si trova in hello stesso o in una posizione geografica diversa. failover del dispositivo Hello è per l'intero dispositivo hello. Durante il failover, i dati di cloud hello per dispositivo di origine hello cambiano toothat di proprietà del dispositivo di destinazione hello.

Per l'Array virtuale StorSimple, è possibile solo eseguire il failover array virtuale tooanother gestita da hello stesso servizio StorSimple Manager. Non è consentita un dispositivo di serie 8000 tooan failover o una matrice gestita da un altro servizio StorSimple Manager (di hello uno per dispositivo di origine hello). toolearn ulteriori informazioni su considerazioni sul failover hello, andare troppo[prerequisiti per il failover del dispositivo hello](storsimple-virtual-array-failover-dr.md).

Quando si esegue un'esito negativo su per l'array virtuale, tenere presente hello segue:

* Per un failover pianificato, è un consigliato di best practice tootake tutti hello volumi e delle condivisioni non in linea tooinitiating precedente hello failover. Seguire le istruzioni specifiche del sistema operativo di hello tootake hello volumi o condivisioni offline in hello host prima e quindi disconnettere quelli nel dispositivo virtuale.
* Per un file server ripristino di emergenza (ripristino di emergenza), è consigliabile unire in join hello toohello di dispositivo di destinazione nello stesso dominio come origine di hello in modo che le autorizzazioni di condivisione di hello vengono risolti automaticamente. Solo hello failover tooa dispositivo di destinazione nel dominio stesso è supportato in questa versione di hello.
* Una volta hello ripristino di emergenza è stato completato correttamente, il dispositivo di origine hello viene eliminato automaticamente. Se il dispositivo di hello non è più disponibile, hello macchina virtuale in cui è eseguito il provisioning nel sistema host hello è utilizzano risorse. Si consiglia di eliminare la macchina virtuale dal tooprevent sistema host eventuali addebiti da essere addebitati.
* Si noti che anche se ha esito negativo, il failover hello **dati hello sono sempre sicuro nel cloud hello**. Prendere in considerazione hello seguenti tre scenari in cui hello failover non è stata completata correttamente:
  
  * Si è verificato un errore nelle fasi iniziali di hello di hello failover, ad esempio quando vengono eseguite pre-verifiche hello ripristino di emergenza. In questo caso, il dispositivo di destinazione è ancora utilizzabile. È possibile riprovare a eseguire failover hello in hello stesso dispositivo di destinazione.
  * Si è verificato un errore durante il processo di failover effettivo hello. In questo caso, il dispositivo di destinazione hello è inutilizzabile. È necessario eseguire il provisioning e configurare un altro array virtuale di destinazione e usarlo per il failover.
  * Hello del failover è stato completato dopo che è stato eliminato il dispositivo di origine hello ma il dispositivo di destinazione hello presenta problemi e non è possibile accedere ai dati. dati Hello sono ancora sicuri nel cloud hello e possono essere facilmente recuperati mediante la creazione di un'altra matrice virtuale e quindi utilizzarlo come dispositivo di destinazione per hello ripristino di emergenza.

### <a name="deactivate"></a>Disattivare
Quando si disattiva un Array virtuale StorSimple, si server connessione hello tra hello dispositivo e il servizio StorSimple Manager corrispondente hello. La disattivazione è un'operazione **permanente** e non può essere annullata. Un dispositivo disattivato non può essere registrato con hello servizio StorSimple Manager nuovamente. Per ulteriori informazioni, visitare troppo[disattivare ed eliminare l'Array virtuale StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

Mantenere hello seguono le procedure consigliate in considerazione durante la disattivazione della matrice virtuale:

* Uno snapshot cloud di tutti i hello dati precedenti toodeactivating un dispositivo virtuale. Quando si disattiva un array virtuale, tutti i dati del dispositivo locale hello viene perso. Creare uno snapshot cloud consentirà toorecover dati in una fase successiva.
* Prima di disattivare un Array virtuale StorSimple, assicurarsi che toostop o eliminare i client e gli host che dipendono da tale dispositivo.
* Eliminare un dispositivo disattivato se non lo si usa più, in modo da evitare l'accumularsi di addebiti.

### <a name="monitoring"></a>Monitoraggio
tooensure che l'Array virtuale StorSimple è in uno stato integro continuo, è necessario toomonitor hello matrice e assicurarsi che si ricevano le informazioni dal sistema hello inclusi avvisi. toomonitor hello integrità complessiva della matrice virtuale hello, hello implementano procedure consigliate seguenti:

* Configurare l'utilizzo del disco hello tootrack monitoraggio del disco dati array virtuale come disco del sistema operativo hello. Se in esecuzione Hyper-V, è possibile utilizzare una combinazione di System Center Virtual Machine Manager (SCVMM) e System Center Operations Manager (SCOM) toomonitor gli host di virtualizzazione.
* Configurare le notifiche di posta elettronica in avvisi toosend array virtuale determinati livelli di utilizzo.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>Applicazioni di analisi antivirus e ricerca nell'indice
Un Array virtuale StorSimple può automaticamente di livello dati dal livello locale di hello toohello cloud di Microsoft Azure. Quando un'applicazione, ad esempio una ricerca nell'indice o un programma antivirus è tooscan utilizzati dati di hello archiviati in StorSimple, è necessario prestare tootake dati cloud hello ottenere accessibili e livello locale toohello nuovamente il pull.

È consigliabile implementare hello seguono le procedure consigliate quando si configura l'analisi di virus o ricerca indice hello nell'array virtuale:

* Disabilitare qualsiasi operazione di analisi completa configurata automaticamente.
* Per i volumi a livelli, configurare hello indice virus o ricerca analisi applicazione tooperform un'analisi incrementale. Questo potrebbe analizzare solo hello nuovi dati probabile che si trovano a livello locale hello. dati Hello cloud toohello a più livelli non avviene durante un'operazione incrementale.
* Verificare i filtri di ricerca corretta hello e vengono configurate in modo che vengano analizzati solo i tipi di hello previsto di file. Ad esempio, di immagini (JPEG, GIF e TIFF) e progettazione disegni non deve essere analizzato durante la ricompilazione dell'indice incrementale o completo hello.

Se si usa il processo di indicizzazione di Windows, seguire queste linee guida:

* Non utilizzare indicizzatore Windows hello per i volumi a livelli quando richiama grandi quantità di dati (TB) dal cloud hello Se indice hello deve toobe ricompilato frequentemente. La ricompilazione di indice hello verranno recuperati tutti i file tipi tooindex il relativo contenuto.
* Usare Windows hello l'indicizzazione di processo per i volumi aggiunti in locale come questa verrebbe accedere ai dati solo sull'indice di hello hello livelli locale toobuild (cloud hello dati non sarà accessibile).

### <a name="byte-range-locking"></a>Blocco di intervalli di byte
Le applicazioni possono bloccare un intervallo di byte specificato all'interno dei file hello. Se il blocco di intervallo di byte è abilitato in applicazioni hello che siano scrivendo tooyour StorSimple, quindi più livelli non funziona sull'array virtuale. Per toowork suddivisione in livelli hello, tutte le aree del file hello accede devono essere sbloccate. Il blocco di intervalli di byte non è supportato con i volumi a livelli nell'array virtuale.

Misure comprendono il blocco di intervalli di byte tooalleviate consigliate:

* Disattivare il blocco dell'intervallo di byte nella logica dell'applicazione.
* Uso localmente bloccato volumi (anziché a più livelli) per i dati di hello associati a questa applicazione. I volumi aggiunti in locale non livello in cloud hello.
* Quando tramite aggiunto in locale i volumi con blocco di intervalli di byte abilitato, volume hello possibile portare online prima di hello ripristino è stato completato. In questi casi, è necessario attendere hello ripristino toobe completo.

## <a name="multiple-arrays"></a>Più array
Più array virtuale potrebbe essere necessario tooaccount toobe distribuito per un ampio set di lavoro di dati che è Impossibile spill nel cloud hello pertanto influire sulle prestazioni di hello del dispositivo hello. In questi casi, è migliore tooscale dispositivi man mano che aumenta di hello working set. Questa operazione richiede uno o più toobe dispositivi aggiunti in data center di hello in locale. Quando si aggiungono dispositivi hello, è possibile:

* Hello Split corrente set di dati.
* Distribuire una nuova periferica toonew di carichi di lavoro.
* Se la distribuzione a più array virtuale, è consigliabile che dal bilanciamento del carico prospettiva, distribuire matrice hello tra gli host hypervisor diversi.
* Più array virtuali, se configurati come file server o server iSCSI, possono essere distribuiti in uno spazio dei nomi del file system distribuito. Per informazioni dettagliate, visitare troppo[Distributed File System Namespace soluzione Guida alla distribuzione di archiviazione Cloud ibrida](https://www.microsoft.com/download/details.aspx?id=45507). Replica DFS distribuita non è attualmente consigliabile per l'utilizzo con array virtuale hello. 

## <a name="see-also"></a>Vedere anche
Informazioni su come troppo[amministrare l'Array virtuale StorSimple](storsimple-virtual-array-manager-service-administration.md) tramite hello servizio StorSimple Manager.

