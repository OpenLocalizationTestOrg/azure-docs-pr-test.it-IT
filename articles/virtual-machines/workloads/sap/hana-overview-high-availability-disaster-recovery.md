---
title: "ripristino di emergenza e disponibilità aaaHigh di SAP HANA in Azure (istanze di grandi dimensioni) | Documenti Microsoft"
description: "Implementare la disponibilità elevata e pianificare il ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>Disponibilità elevata e ripristino di emergenza di SAP HANA (istanze di grandi dimensioni) in Azure 

La disponibilità elevata e il ripristino di emergenza sono aspetti importanti per l'esecuzione di uno o più server SAP HANA di importanza critica in Azure (istanze di grandi dimensioni). È importante toowork con SAP, l'integratore di sistema, o Microsoft tooproperly architect e implementare hello strategia destra elevata-disponibilità/ripristino di emergenza. È inoltre importante tooconsider obiettivo del punto di ripristino hello e obiettivo tempo di ripristino, che sono tooyour specifico ambiente.

## <a name="high-availability"></a>Disponibilità elevata

Microsoft supporta metodi di disponibilità elevata di SAP HANA "out della casella hello," che includono:

- **Replica di archiviazione:** hello tooreplicate possibilità di sistema di archiviazione percorso di tutti i dati tooanother (all'interno, o separatamente, hello stesso Data Center). SAP HANA funziona in modo indipendente da questo metodo.
- **Replica DFS HANA:** hello replica di tutti i dati nel sistema SAP HANA di SAP HANA tooa distinto. obiettivo tempo di ripristino Hello è ridotta a icona tramite la replica dei dati a intervalli regolari. SAP HANA supporta le modalità in memoria e sincrone sincrone, asincrone (consigliata solo per SAP HANA tutti i sistemi all'interno di hello stesso Data Center o meno di 100 KM distanza). Nella struttura corrente di hello di indicatori di grandi dimensioni istanza HANA, replica DFS HANA è utilizzabile per la disponibilità elevata.
- **Host con failover automatico:** un toouse soluzione-recupero da errori locali come una replica toosystem alternativo. Quando il nodo principale hello diventa non disponibile, uno o più nodi di SAP HANA standby sono configurati in modalità di scalabilità orizzontale e SAP HANA automaticamente eseguito il failover tooanother nodo.

Per ulteriori informazioni sulla disponibilità elevata di SAP HANA, vedere le seguenti informazioni SAP hello:

- [SAP HANA High-Availability Whitepaper](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html) (White paper sulla disponibilità elevata di SAP HANA)
- [SAP HANA Administration Guide](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf) (Guida all'amministrazione di SAP HANA)
- [SAP Academy Video on SAP HANA System Replication](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication) (Video della SAP Academy sulla replica di sistema di SAP HANA)
- [SAP Support Note #1999880 - FAQ on SAP HANA System Replication](https://bcs.wdf.sap.corp/sap/support/notes/1999880) (Nota di supporto SAP 1999880 - Domande frequenti sulla replica di sistema di SAP HANA)
- [SAP Support Note #2165547 - SAP HANA Backup and Restore within SAP HANA System Replication Environment](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726) (Nota di supporto SAP 2165547 - Backup e ripristino di SAP HANA nell'ambiente di replica di sistema di SAP HANA)
- [SAP Support Note #1984882 - Using SAP HANA System Replication for Hardware Exchange with Minimum/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226) (Nota di supporto SAP 1984882 - Uso della replica di sistema di SAP HANA per la sostituzione di hardware con tempo di inattività minimo o nullo)

## <a name="disaster-recovery"></a>Ripristino di emergenza

SAP HANA in Azure (istanze di grandi dimensioni) è disponibile in due aree di Azure all'interno di un'area geopolitica. Tra indicatori di grandi dimensioni istanza due di hello di due aree diverse è una connettività di rete diretto per la replica dei dati durante il ripristino di emergenza. replica Hello dei dati di hello è basato l'infrastruttura di archiviazione. la replica di Hello non viene eseguita per impostazione predefinita. Viene eseguito per le configurazioni del cliente hello ordinati il ripristino di emergenza hello. Nella finestra di progettazione corrente hello, replica DFS HANA non utilizzabile per il ripristino di emergenza.

Tuttavia, il vantaggio di tootake hello ripristino di emergenza, è necessario toostart toodesign hello rete connettività toohello due diverse aree di Azure. toodo in tal caso, non è presente una connessione del circuito ExpressRoute di Azure locale l'area principale di Azure e un'altra connessione circuito dall'area di ripristino di emergenza tooyour locale. Questa misura consente di gestire le situazioni in cui si verifica un problema all'interno di un'intera area di Azure, inclusa la posizione di un router MSEE (Microsoft Enterprise Edge).

Come seconda misura, è possibile connettere tutte le reti virtuali di Azure che si connettono tooSAP HANA in Azure (istanze di grandi dimensioni) in uno dei hello aree tooboth di tali circuiti ExpressRoute. Questa misura consente di risolvere un caso in cui solo una delle posizioni MSEE hello che si connette il percorso locale con Azure va fuori servizio.

Hello figura seguente viene illustrata la configurazione ottimale di hello per il ripristino di emergenza:

![Configurazione ottimale per il ripristino di emergenza](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

Hello caso ottimale per una configurazione di ripristino di emergenza di rete hello è toohave due circuiti ExpressRoute da on-premise toohello due diverse aree di Azure. Un circuito passa tooregion #1 in esecuzione un'istanza di produzione. circuito ExpressRoute secondo Hello passa tooregion #2, alcune istanze HANA non di produzione in esecuzione. (Questo è importante se un'intera regione di Azure, tra cui hello MSEE e indicatore di grandi dimensioni-istanza, viene disattivato griglia hello).

Come seconda misura, hello diverse reti virtuali è connessa toohello circuiti ExpressRoute diversi che sono connessi tooSAP HANA in Azure (istanze di grandi dimensioni). È possibile ignorare percorso hello in cui un MSEE ha esito negativo oppure è possibile ridurre l'obiettivo del punto di ripristino hello per il ripristino di emergenza, come illustrato più avanti.

Hello requisiti successivi per l'installazione di ripristino di emergenza sono:

- È necessario ordinare SAP HANA per gli SKU di Azure (istanze di grandi dimensioni) di hello stesso dimensioni di SKU di produzione e di distribuirli nell'area di ripristino di emergenza hello. Queste istanze possono essere utilizzati toorun test, sandbox o QA HANA istanze.
- È necessario ordinare un profilo di ripristino di emergenza per ciascuna del SAP HANA per gli SKU di Azure (istanze di grandi dimensioni) che si desidera toorecover nel sito di ripristino di emergenza hello, se necessario. Questa azione comporta l'allocazione toohello di volumi di archiviazione, che sono di replica di archiviazione hello dalla propria area di produzione nell'area di ripristino di emergenza hello hello.

Una volta soddisfatti hello precedenti requisiti, è la replica di archiviazione di responsabilità toostart hello. In un'infrastruttura di archiviazione hello utilizzata per SAP HANA in Azure (istanze di grandi dimensioni), base hello della replica di archiviazione è snapshot di archiviazione. replica di ripristino di emergenza hello toostart, è necessario tooperform:

- Uno snapshot del LUN di avvio, come descritto in precedenza.
- Uno snapshot dei volumi correlati a HANA, come descritto in precedenza.

Dopo aver eseguito questi snapshot, una replica iniziale dei volumi hello viene effettuato il seeding hello in volumi in cui sono associati al profilo di ripristino di emergenza nell'area di ripristino di emergenza hello.

Successivamente, in cui ogni ora viene utilizzato con snapshot di archiviazione più recente di hello delta hello tooreplicate che sviluppano su volumi di archiviazione hello.

obiettivo del punto di ripristino Hello che è possibile ottenere con questa configurazione è di 60 minuti too90. un ripristino migliore tooachieve obiettivo del punto in caso di ripristino di emergenza hello, copia hello HANA backup log delle transazioni da SAP HANA in Azure (istanze di grandi dimensioni) toohello altre aree di Azure. tooachieve questo obiettivo del punto di ripristino, hello seguenti:

1. Eseguire il backup delle transazioni HANA hello accedere come spesso possibile troppo/hana / / backup del log.
2. Copiare i backup del log delle transazioni hello quando sono finiti tooan macchina virtuale di Azure (VM), ovvero in una rete virtuale connessa toohello SAP HANA nel server di Azure (istanze di grandi dimensioni).
3. Dalla macchina virtuale, copiare hello backup tooa macchina virtuale che risiede in una rete virtuale nell'area di ripristino di emergenza hello.
4. Mantenere i backup del log di transazione hello in tale area nel hello VM.

In caso di emergenza, dopo aver distribuito il profilo di ripristino di emergenza hello in un server effettivo, copiare i backup del log delle transazioni hello hello VM toohello SAP HANA in Azure (istanze di grandi dimensioni) è ora server primario di hello nell'area di ripristino di emergenza hello, e ripristinare tali backup. Il ripristino è possibile perché lo stato di hello di HANA su dischi di ripristino di emergenza hello è quello di uno snapshot HANA. Si tratta di punto di offset hello per ulteriori operazioni di ripristino di backup del log delle transazioni.

## <a name="backup-and-restore"></a>Backup e ripristino

Uno dei database toooperating aspetti più importanti di hello consiste nel garantire database hello può essere protetti da vari eventi irreversibili. Questi eventi possono essere causati da niente da errori dell'utente toosimple calamità naturali.

Backup di database, con toorestore possibilità hello è tooany punto nel tempo (ad esempio prima che un utente eliminato i dati critici), consente il ripristino stato di tooa più vicino possibile toohello presentava prima che si è verificato interruzioni hello.

Per ottenere risultati ottimali, è necessario eseguire due tipi di backup:

- Backup del database
- Backup dei log delle transazioni

Inoltre toofull il backup del database eseguito a livello di applicazione, è possibile anche più accurato eseguendo il backup con snapshot di archiviazione. Esecuzione di backup del log è anche importante per il ripristino di database hello (tooempty hello log delle transazioni già eseguito il commit e).

SAP HANA in Azure (istanze di grandi dimensioni) offre due opzioni di backup e ripristino:

- Eseguire il backup e il ripristino manualmente. Dopo avere calcolato tooensure spazio su disco sufficiente, eseguire backup completi di database e del log tramite i metodi di backup su disco (toothose dischi). Nel corso del tempo, hello backup vengono copiati tooan account di archiviazione di Azure (dopo aver configurato un server di file basati su Azure con archiviazione virtualmente illimitata) o usare un insieme di credenziali di Azure Backup o archiviazione di Azure ignoto. Un'altra opzione è toouse uno strumento di protezione dati di terze parti, ad esempio Commvault, i backup di hello toostore dopo che sono copiati tooa account di archiviazione. Hello DIY opzione di backup può essere necessario per i dati che devono essere archiviati per periodi più lunghi per scopi di controllo di conformità e toobe.
- Utilizzare hello di backup e ripristino delle funzionalità che hello infrastruttura sottostante di SAP HANA in Azure (istanze di grandi dimensioni) fornisce. Questa opzione soddisfa hello necessario per i backup e rende backup manuali quasi obsoleta (eccetto in cui sono necessari per motivi di conformità i backup di dati). rest Hello di indirizzi di questa sezione hello backup e ripristino delle funzionalità offerte con HANA (istanze di grandi dimensioni).

> [!NOTE]
> tecnologia di snapshot Hello utilizzata dall'infrastruttura sottostante di hello di HANA (istanze di grandi dimensioni) presenta una dipendenza per gli snapshot di SAP HANA. Gli snapshot di SAP HANA non funzionano in combinazione con i contenitori di database multi-tenant SAP HANA. Di conseguenza, questo metodo di backup non può essere utilizzato toodeploy SAP HANA Multitenant Database contenitori.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Uso degli snapshot di archiviazione di SAP HANA in Azure (istanze di grandi dimensioni)

infrastruttura di archiviazione Hello sottostante SAP HANA in Azure (istanze di grandi dimensioni) supporta la nozione di hello di uno snapshot di archiviazione dei volumi. Backup e ripristino di un determinato volume sono supportate con hello seguenti considerazioni:

- In alternativa ai backup del database, vengono creati regolarmente snapshot di archiviazione dei volumi.
- snapshot di archiviazione Hello avvia uno snapshot di SAP HANA prima dell'esecuzione di snapshot di archiviazione hello. Lo snapshot di SAP HANA è il punto di installazione hello per ripristini di log finale dopo il ripristino dello snapshot di archiviazione hello.
- A un punto in cui viene eseguito correttamente snapshot archiviazione hello hello snapshot di SAP HANA hello viene eliminato.
- Backup del log vengono creati di frequente e archiviati nel volume di backup di log hello o in Azure.
- Se è necessario ripristinare il database di hello tooa determinato punto nel tempo, viene effettuata una richiesta tooMicrosoft supporto tecnico di Azure (interruzione produzione) o SAP HANA in Gestione servizi di Azure toorestore tooa alcuni snapshot di archiviazione (ad esempio, un pianificato ripristino di un sistema sandbox tooits lo stato originale).
- snapshot di SAP HANA Hello che è incluso nello snapshot di archiviazione hello è un punto di offset per l'applicazione di backup del log che sono state eseguite e archiviato dopo hello archiviazione dello snapshot.
- Questi backup del log toorestore hello database back-tooa determinato punto nel tempo.

Backup hello specificando\_nome crea uno snapshot di hello seguenti volumi:

- hana/data
- hana/log
- hana/log\_backup (montato come backup in hana/log)
- hana/shared

### <a name="storage-snapshot-considerations"></a>Considerazioni sugli snapshot di archiviazione

>[!NOTE]
>Gli snapshot di archiviazione _non_ vengono forniti gratuitamente perché richiedono l'allocazione di spazio di archiviazione aggiuntivo.

meccanismo specifico di Hello di snapshot di archiviazione per SAP HANA in Azure (istanze di grandi dimensioni) include:

- Uno snapshot di archiviazione specifico (in hello momento quando questa viene eliminata) utilizza molto spazio di archiviazione.
- Modifiche del contenuto dei dati e il contenuto di hello nei dati di SAP HANA cambiano i file nel volume di archiviazione hello, snapshot hello deve toostore hello originale bloccare i contenuti.
- snapshot di archiviazione Hello aumenta le dimensioni. snapshot hello più Hello esiste, hello maggiore hello archiviazione snapshot diventa.
- Hello altre modifiche apportate toohello volume del database SAP HANA nel corso della durata hello di uno snapshot di archiviazione, diventa hello maggiore hello sull'utilizzo di spazio di snapshot di archiviazione hello.

SAP HANA in Azure (istanze di grandi dimensioni) viene fornito con le dimensioni di un volume fisso per il volume di dati e di log di SAP HANA hello. Esecuzione di snapshot dei volumi mostro nello spazio nel volume, pertanto gli snapshot di archiviazione responsabilità tooschedule (all'interno di hello SAP HANA sul processo di Azure [istanze di grandi dimensioni]).

Hello nelle sezioni seguenti vengono forniscono informazioni per l'esecuzione di questi snapshot, inclusi i consigli generali:

- Se l'hardware hello in grado di sostenere 255 snapshot per ogni volume, si consiglia di restare ben di sotto di questo numero.
- Prima di eseguire snapshot di archiviazione, monitorare e tenere traccia dello spazio libero.
- Numero inferiore di hello di snapshot di archiviazione in base allo spazio libero. Potrebbe essere necessario numero hello toolower di snapshot da mantenere oppure potrebbe essere necessario volumi hello tooextend. È possibile ordinare ulteriore spazio di archiviazione in unità di 1 TB.
- Durante determinate attività, come lo spostamento di dati in SAP HANA con strumenti di migrazione del sistema (R3load o la funzionalità per il ripristino di backup di database SAP HANA), è consigliabile non creare snapshot di archiviazione. (Se viene eseguita la migrazione di un sistema in un nuovo sistema SAP HANA, gli snapshot di archiviazione non è necessario eseguire toobe.)
- Durante una riorganizzazione più estesa delle tabelle di SAP HANA, evitare di creare snapshot di archiviazione, se possibile.
- Gli snapshot di archiviazione sono una funzionalità di ripristino di emergenza hello tooengaging dei prerequisiti di SAP HANA in Azure (istanze di grandi dimensioni).

### <a name="setting-up-storage-snapshots"></a>Configurazione degli snapshot di archiviazione

1. Assicurarsi che Perl sia installato nel sistema operativo Linux di hello server hello HANA (istanze di grandi dimensioni).
2. Modificare/e così via ssh/ssh\_riga hello di configurazione tooadd _Mac hmac-sha1_.
3. Creare un account utente per il backup di SAP HANA sul nodo principale di hello per ogni istanza di SAP HANA che eseguono (se applicabile).
4. il client di SAP HANA HDB Hello deve essere installato in tutti i server (istanze di grandi dimensioni) di SAP HANA.
5. Server hello prima SAP HANA (istanze di grandi dimensioni) di ogni area, una chiave pubblica è necessario creare hello tooaccess sottostante l'infrastruttura di archiviazione che controlla la creazione di snapshot.
6. Copiare script hello azure\_hana\_backup.pl dal percorso toohello /script di **hdbsql** di installazione di SAP HANA hello.
7. Hello copia HANABackupDetails.txt file toohello /script stesso percorso come hello script Perl.
8. Modificare il file HANABackupDetails.txt hello necessarie per le specifiche del cliente appropriato hello.

### <a name="step-1-install-sap-hana-hdbclient"></a>Passaggio 1: Installare il client HBD di SAP HANA

Hello Linux installato in SAP HANA in Azure (istanze di grandi dimensioni) include cartelle hello e script di snapshot di archiviazione di SAP HANA tooexecute necessario per scopi di backup e ripristino di emergenza. Tuttavia, è il tooinstall responsabilità SAP HANA HDBclient durante l'installazione di SAP HANA. (Microsoft installa hello HDBclient né SAP HANA).

### <a name="step-2-change-etcsshsshconfig"></a>Passaggio 2: Modificare /etc/ssh/ssh\_config

Modificare /etc/ssh/ssh\_config aggiungendo la riga _MACs hmac-sha1_ come indicato di seguito:
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>Passaggio 3: Creare una chiave pubblica

In hello prima SAP HANA nel server di Azure (istanze di grandi dimensioni) in ogni area di Azure, creare un'infrastruttura di archiviazione hello tooaccess toobe di chiave pubblica utilizzata in modo che è possibile creare snapshot. la chiave pubblica di Hello garantisce che una password non è necessario toosign nel servizio di archiviazione toohello e che le credenziali di password non vengono mantenute. In Linux nel server di hello SAP HANA (istanze di grandi dimensioni), eseguire hello chiave pubblica hello toogenerate di comando seguente:
```
  ssh-keygen –t dsa –b 1024
```
nuova posizione Hello è _/root/.ssh/id\_dsa.pub. Non immettere una passphrase effettiva, altrimenti sarà necessario tooenter hello passphrase ogni volta che accedi. In alternativa, premere **invio** due volte tooremove hello immettere passphrase requisito per l'accesso.

Verificare che la chiave pubblica hello è stato corretto come previsto modificando too/root/.ssh/ cartelle e quindi eseguendo hello toomake **ls** comando. Se hello chiave è presente, è possibile copiarlo eseguendo hello comando seguente:

![La chiave pubblica viene copiata eseguendo questo comando](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

A questo punto, contattare SAP HANA sulla gestione dei servizi di Azure e fornire hello chiave. addetto al servizio Hello utilizza hello tooregister di chiave pubblica in hello sottostante l'infrastruttura di archiviazione.

### <a name="step-4-create-an-sap-hana-user-account"></a>Passaggio 4: Creare un account utente SAP HANA

In SAP HANA Studio creare un account utente SAP HANA a scopo di backup. Questo account deve disporre di hello seguenti privilegi: _Backup Admin_ e _lettura catalogo_. In questo esempio, il nome utente hello SCADMIN viene creato.

![Creazione di un utente in HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>Passaggio 5: Autorizzare l'account utente di SAP HANA hello

Autorizzare l'account utente di SAP HANA hello (toobe usati da script hello senza richiedere l'autorizzazione ogni volta che viene eseguito uno script hello). comando SAP HANA Hello `hdbuserstore` consente di creare una chiave utente SAP HANA, che viene archiviata in uno o più nodi di SAP HANA hello. chiave utente Hello consente inoltre di hello utente tooaccess SAP HANA senza password toomanage da all'interno di hello scripting processo che si parlerà più avanti.

>[!IMPORTANT]
>Esecuzione hello il seguente comando come `_root_`. In caso contrario, script hello non può funzionare correttamente.

Immettere hello `hdbuserstore` comando come segue:

![Immettere il comando di hdbuserstore hello](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

Nel seguente esempio, in cui utente hello è SCADMIN01 e il nome host hello è lhanad01, hello hello è:
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Gestire tutti gli script da un singolo server per le istanze HANA con scalabilità orizzontale. In questo esempio hello chiave SAP HANA che scadmin01 deve essere modificata per ogni host in modo che rifletta l'host di hello chiave toohello correlati. Vale a dire, account di SAP HANA backup hello è modificato con numero di istanza hello di hello HANA DB, **lhanad**. chiave Hello deve avere privilegi amministrativi nell'host di hello a che viene assegnato, e utente di backup di hello per scalabilità orizzontale deve disporre di istanze SAP HANA tooall diritti di accesso.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>Passaggio 6: Copiare gli elementi dalla cartella /script hello

Esempio hello copia gli elementi da hello/script directory di lavoro toohello cartella (incluso nell'immagine gold hello dell'installazione di hello) per **hdbsql**. Per le installazioni correnti di HANA, la directory è /hana/shared/D01/exe/linuxx86\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Copiare i seguenti elementi se sono in esecuzione di scalabilità orizzontale hello o OLAP:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
file HANABackupCustomerDetails.txt Hello è modificabile come indicato di seguito per una distribuzione con scalabilità verticale. Si tratta di file di configurazione e controllo hello per hello dello script eseguito snapshot di archiviazione hello. Si dovrebbe avere ricevuto hello _nome del Backup di archiviazione_ e _l'indirizzo IP di archiviazione_ da SAP HANA sulla gestione dei servizi di Azure quando le istanze sono state distribuite. Non è possibile modificare la sequenza di hello, ordinamento o la spaziatura delle variabili di hello o hello script non viene eseguita correttamente.

Per una distribuzione con scalabilità verticale, i file di configurazione hello deve essere simile:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Per una configurazione con scalabilità orizzontale, file di HANABackupCustomerDetailsBW.txt hello deve essere simile:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>Attualmente, solo il nodo 1 dettagli vengono utilizzati in script hello effettivo HANA archiviazione dello snapshot. È consigliabile testare tooor di accesso da tutti i nodi HANA in modo che, se il nodo di backup master di hello dovesse cambia, aver già verificato che un altro nodo può richiedere al suo posto modificando i dettagli di hello nel nodo 1.

toocheck per le configurazioni di hello corretto nel file di configurazione hello o istanze HANA toohello connettività appropriato, eseguire uno dei seguenti script hello:
- Per una configurazione con scalabilità verticale (indipendente dal carico di lavoro SAP):

 ```
testHANAConnection.pl
```
- Per una configurazioni con scalabilità orizzontale:

 ```
testHANAConnectionBW.pl
```

Assicurarsi di che quell'istanza HANA master hello dispone di server di accesso richiesto tooall HANA. Sono disponibili non sono presenti script toohello parametri, ma è necessario completare hello appropriato HANABackupCustomerDetails HANABackupCustomerDetailsBW file per hello script toorun correttamente. Poiché vengono restituiti codici di errore solo hello shell comandi, non è possibile per hello script tooerror controllare ogni istanza. Anche in questo caso, script hello fornire alcuni commenti utili per si toodouble un controllo.

script di hello toorun:
```
 ./testHANAConnection.pl
```
 Se lo script hello Ottiene correttamente la stato hello dell'istanza HANA hello, viene visualizzato un messaggio che connessione HANA hello ha avuto esito positivo.

È disponibile anche un secondo tipo di script è possibile utilizzare toosign possibilità toocheck hello HANA istanza del server master in archiviazione toohello. Prima di eseguire azure hello\_hana\_backup (\_bw) PL script, è necessario eseguire script successivo hello. Se un volume contiene Nessuno snapshot, è Impossibile toodetermine volume hello è semplicemente vuoto o non esiste un ssh hello tooobtain errore dettagli dello snapshot. Per questo motivo, script hello esegue due passaggi:

- Verifica che tale console archiviazione hello è accessibile.
- Crea uno snapshot di test, o fittizio, per ogni volume di ogni istanza HANA.

Per questo motivo, l'istanza HANA hello è incluso come argomento. Nuovamente, non è possibile tooprovide errori per la connessione di archiviazione hello, ma vengono forniti alcuni script hello suggerimenti se hello esecuzione ha esito negativo.

Hello script viene eseguito come:
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
Oppure viene eseguito nel modo seguente:
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
script di Hello Visualizza anche un messaggio che si è in grado di toosign in modo appropriato tenant archiviazione tooyour distribuito, è organizzato in base a numeri di hello unità logica (LUN) che vengono utilizzati dalle istanze del server hello che si è proprietari.

Prima di eseguire hello prima archiviazione basata su snapshot backup, eseguire hello Avanti script toomake tale configurazione hello sia corretto.

Dopo aver eseguito questi script, è possibile eliminare gli snapshot hello eseguendo:
```
./removeTestStorageSnapshot.pl <hana instance>
```
Or
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>Passaggio 7: Eseguire snapshot su richiesta

Eseguire snapshot su richiesta (e pianificare snapshot regolari utilizzando cron) come descritto di seguito.

Per le configurazioni con scalabilità verticale, eseguire lo script seguente hello:
```
./azure_hana_backup.pl lhanad01 customer 20
```
Per le configurazioni di scalabilità orizzontale, eseguire lo script seguente hello:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
script di scalabilità orizzontale Hello esegue alcune ulteriori toomake verifica che tutti i server HANA accessibili e tutte le istanze HANA appropriato lo stato restituiscono dell'istanza di hello prima di procedere con la creazione di snapshot di SAP HANA o archiviazione.

Hello gli argomenti seguenti è necessario:

- backup che richiedono istanza HANA Hello.
- prefisso di snapshot Hello per snapshot di archiviazione hello.
- numero di Hello di snapshot toobe conservati per prefisso specifico hello.

```
./azure_hana_backup.pl lhanad01 customer 20
```

l'esecuzione di Hello dello script hello Crea snapshot di archiviazione hello in questi tre fasi distinte:

- Eseguire uno snapshot HANA.
- Eseguire uno snapshot di archiviazione.
- Rimuovere snapshot HANA hello.

Eseguire script hello effettuando una chiamata da hello HDB cartella eseguibile che è stato copiato. Si esegue il backup almeno hello in seguito volumi, ma anche esegue il backup di qualsiasi volume con nome di istanza SAP HANA esplicito hello nel nome del volume hello.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
periodo di memorizzazione Hello rigorosamente viene amministrato, con il numero di hello di snapshot inviato come parametro quando si esegue uno script di hello (ad esempio, 20, illustrato in precedenza). Pertanto, hello tempo è una funzione del periodo di hello hello e esecuzione il numero di snapshot nella chiamata di hello dello script hello. Se hello numero di snapshot vengono conservati hello di supera vengono denominate come un parametro nella chiamata di hello dello script hello, hello lo snapshot meno recente di archiviazione di questa etichetta (in questo caso precedente, _personalizzato_) viene eliminato prima che sia un nuovo snapshot eseguito. Ciò significa che il numero di hello che è possibile assegnare come ultimo parametro della chiamata di hello hello è il numero di hello è possibile utilizzare toocontrol hello numero di snapshot.

>[!NOTE]
>Non appena si modifica l'etichetta di hello, hello inizia il conteggio nuovamente.

È necessario tooinclude hello HANA nome dell'istanza che viene fornita da SAP HANA sulla gestione dei servizi di Azure come argomento, se creano snapshot in ambienti a più nodi. In ambienti a nodo singolo, è sufficiente nome hello di hello SAP HANA nell'unità di Azure (istanze di grandi dimensioni), ma è comunque consigliabile nome dell'istanza HANA hello.

Inoltre, è possibile eseguire il backup volumes\LUNs avvio utilizzando hello stesso script. È necessario eseguire il backup del volume di avvio almeno una volta quando si esegue HANA per la prima volta, anche se è consigliabile pianificare backup settimanali o nelle ore notturne per tale volume tramite cron. Invece di aggiungere il nome di un'istanza di SAP HANA, inserire _avvio_ come hello argomento nello script hello come indicato di seguito:
```
./azure_hana_backup boot customer 20
```
Hello stesso criterio di conservazione è offerta toohello anche il volume di avvio. Utilizzare snapshot su richiesta, come descritto in precedenza, per casi speciali, ad esempio durante un aggiornamento di pacchetto (EHP) SAP funzionalità avanzata, o quando è necessario toocreate uno snapshot di archiviazione distinti.

Si consiglia di snapshot di archiviazione tooperform pianificata utilizzando cron e si consiglia di utilizzare hello stesso script per tutti i backup e alle esigenze di ripristino di emergenza (modifica hello script input toomatch hello vari ha richiesto tempi di backup). Gli snapshot sono tutti pianificati in modo diverso in cron, in base alla frequenza di esecuzione: oraria, ogni 12 ore, giornaliera o settimanale. pianificazione cron Hello è progettato toocreate snapshot di archiviazione che corrispondono a hello illustrata in precedenza memorizzazione l'assegnazione di etichette per il backup fuori sede a lungo termine. script di Hello include comandi tooback includere tutti i volumi di produzione, a seconda della relativa frequenza di richiesta (file di dati e di log vengono eseguito il backup ogni ora, mentre il volume di avvio hello viene eseguito il backup giornaliero).

le voci di Hello in hello cron script seguente eseguito ogni ora hello decimo minuto, ogni 12 ore hello decimo minuto e ogni giorno hello decimo minuto. cron Hello i processi vengono creati in modo che un solo snapshot di archiviazione di SAP HANA ha luogo durante qualsiasi ora specifica, in modo che hello orari e giornalieri i backup non vengono eseguiti in hello che la stessa ora (12:10 AM). toohelp ottimizzare la creazione dello snapshot e la replica, SAP HANA sulla gestione dei servizi di Azure fornisce hello i backup di tempo per toorun è consigliato.

Hello predefinito cron /etc/crontab di pianificazione è il seguente:
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
Nelle istruzioni di cron precedente hello, volumi HANA hello (senza il volume di avvio) ottenere snapshot con etichetta hello ogni ora. Di questi snapshot, ne vengono mantenuti 66. Inoltre, vengono mantenuti 14 snapshot con etichetta di hello 12 ore. Si possono avere snapshot orari per tre giorni, oltre a snapshot ogni 12 ore per altri quattro giorni, ovvero un'intera settimana di snapshot.

Pianificazione all'interno di cron può risultare difficile, perché solo uno script deve essere eseguito in qualsiasi momento specifico, a meno che non vengono scaglionati in script hello da alcuni minuti. Se si desidera i backup giornalieri per la conservazione a lungo termine, un snapshot viene mantenuto insieme a uno snapshot di 12 ore (con un conteggio di conservazione di ogni sette) o snapshot oraria hello è tootake sfalsate 10 minuti in un secondo momento. Un solo snapshot viene mantenuto nel volume di produzione hello.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
le frequenze di Hello elencate di seguito sono riportati esempi di solo. tooderive il numero ottimale di snapshot, utilizzare hello seguenti criteri:

- Requisiti dell'obiettivo tempo di ripristino per il ripristino temporizzato.
- Utilizzo dello spazio.
- Requisiti dell'obiettivo punto di ripristino e dell'obiettivo tempo di ripristino per un ripristino di emergenza potenziale.
- Eventuale esecuzione di backup completi del database HANA sui dischi. Ogni volta che un backup completo del database su dischi, o _backint_ l'interfaccia, viene eseguita, hello l'esecuzione di snapshot di archiviazione non riesce. Se si prevede di backup completi del database tooexecute nella parte superiore di snapshot di archiviazione, assicurarsi che l'esecuzione di hello di snapshot di archiviazione è disabilitato durante l'operazione.

>[!IMPORTANT]
> utilizzo di Hello di snapshot di archiviazione per i backup di SAP HANA è valido solo quando vengono eseguiti gli snapshot hello in combinazione con i backup del log SAP HANA. Questi log backup necessario toobe toocover in grado di hello periodi di tempo tra gli snapshot di archiviazione hello. Se è stato impostato un toousers impegno di un punto nel tempo di ripristino di 30 giorni, è necessario hello segue:

- Possibilità tooaccess uno snapshot di archiviazione di 30 giorni precedenti.
- Backup di log contigui su hello ultimi 30 giorni.

Intervallo di hello di backup del log, creare uno snapshot del volume di backup del log hello anche. Tuttavia, essere tooperform che backup regolari dei log in modo che sia possibile:

- Sono dei backup del log contigui hello necessari i ripristini temporizzati in tooperform.
- Impedire l'esaurimento dello spazio volume di log di SAP HANA hello.

Uno degli ultimi passaggi hello è tooschedule registri di backup SAP HANA in SAP HANA Studio. destinazione backup del log di SAP HANA di Hello è hana hello appositamente creato o di log\_volume di backup con il punto di montaggio hello del /hana/log/backups.

![Pianificare i log di backup di SAP HANA in SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

È possibile scegliere backup con una frequenza maggiore di ogni 15 minuti. Alcuni utenti eseguono il backup dei log ogni minuto, ma è sconsigliato impostare una frequenza _superiore_ a 15 minuti.

passaggio finale Hello è tooperform basato su file di backup (dopo l'installazione iniziale di hello di SAP HANA) toocreate una singola voce di backup che deve essere presente nel catalogo di backup hello. In caso contrario SAP HANA non può avviare i backup del log specificato.

![Immettere un toocreate backup basati su file un singolo backup](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Monitoraggio numero hello e le dimensioni degli snapshot sul volume disco hello

In un volume di archiviazione specifico, è possibile monitorare il numero di hello di snapshot e l'utilizzo dell'archiviazione hello di snapshot. Hello `ls` non mostra il comando file o directory snapshot hello. Tuttavia, hello comando del sistema operativo Linux `du` avviene, hello seguenti comandi:

- `du –sh .snapshot`fornisce un totale di tutti gli snapshot all'interno di directory snapshot hello.
- `du –sh --max-depth=1`Elenca tutti gli snapshot vengono salvati nella cartella .snapshot hello e le dimensioni di hello di ogni snapshot.
- `du –hc`fornisce dimensioni totali di hello utilizzata da tutti gli snapshot.

Utilizzare questi comandi toomake assicurarsi che gli snapshot hello vengono eseguiti e archiviati non utilizzano tutti gli archivi di hello nei volumi di hello.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>Riducendo il numero di hello di snapshot in un server

Come spiegato in precedenza, è possibile ridurre il numero di hello di alcune etichette di snapshot archiviati. Hello ultimi due parametri di hello comando tooinitiate uno snapshot sono un numero di etichetta e hello di snapshot di cui si desidera tooretain.
```
./azure_hana_backup.pl lhanad01 customer 20
```
Nell'esempio precedente hello etichetta snapshot hello è _cliente_ e hello numero di snapshot con toobe questa etichetta mantenuti è _20_. Quando si risponde toodisk sull'utilizzo di spazio, è possibile che si desideri numero hello tooreduce di snapshot archiviato. Consente di Hello numero hello tooreduce di snapshot è script hello toorun con hello ultimo parametro set too5:
```
./azure_hana_backup.pl lhanad01 customer 5
```
Come risultato di esecuzione dello script hello con questa impostazione, il numero di hello di snapshot, tra cui hello nuova risorsa di archiviazione dello snapshot, è _5_.

 >[!NOTE]
 > Questo script consente di ridurre il numero di hello di snapshot solo se allo snapshot precedente più recente di hello è più di un'ora precedente. script Hello non elimina gli snapshot sono meno di un'ora fa.

Queste restrizioni sono una funzionalità opzionale di ripristino di emergenza correlate toohello offerte.

Se non si desidera più toomaintain un set di snapshot con tale prefisso, è possibile eseguire lo script hello con _0_ come hello memorizzazione numero tooremove tutti gli snapshot corrispondente tale prefisso. La rimozione di tutti gli snapshot possono tuttavia influire sulla funzionalità hello del ripristino di emergenza.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>Ripristino di snapshot HANA più recente toohello

In caso di hello che si verifichi un scenario di produzione verso il basso, il processo di hello di ripristino da uno snapshot di archiviazione può essere avviato come un evento imprevisto di clienti con SAP HANA sulla gestione dei servizi di Azure. Un scenario di questo tipo imprevisto potrebbe essere una questione di urgenza elevati se i dati sono stati eliminati in produzione hello e sistema solo modo dati hello tooretrieve database di produzione toorestore hello.

In hello invece un punto nel tempo di ripristino potrebbe essere bassa urgenza e pianificato per i giorni in anticipo. È possibile pianificare questo ripristino con il team di gestione dei servizi SAP HANA in Azure anziché segnalare un problema ad alta priorità. Ad esempio, potrebbe essere pianificazione tootry un aggiornamento del software SAP hello applicando un nuovo pacchetto di funzionalità avanzata ed è quindi necessario eseguire il toorevert tooa snapshot che rappresenta lo stato di hello prima dell'aggiornamento hello EHP.

Prima di eseguire la richiesta di hello, è necessario toodo alcune attività di preparazione. SAP HANA team di gestione del servizio Azure può gestire la richiesta di hello e fornire volumi hello ripristinato. In seguito, è tooyou toorestore hello HANA database basato su snapshot hello. Ecco come tooprepare per hello richiesta:

>[!NOTE]
>L'interfaccia utente potrebbe variare da hello seguente schermate, a seconda di hello versione SAP HANA in uso.

1. Decidere quali toorestore snapshot. A meno che non viene richiesto, in caso contrario, verrebbe ripristinato solo il volume di dati/hana hello.

2. Arrestare l'istanza HANA hello.

 ![Arrestare l'istanza di hello HANA](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Smontare i volumi di dati hello in ogni nodo del database HANA. ripristino di Hello dello snapshot hello ha esito negativo se i volumi di dati hello non vengono smontati.

 ![Smontare i volumi di dati hello in ogni nodo del database HANA](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Aprire un ripristino di supporto tecnico di Azure richiesta tooinstruct hello di uno snapshot specifico.

 - Durante il ripristino di hello: SAP HANA sulla gestione dei servizi di Azure potrebbe richiedere di tooattend tooensure una conferenza telefonica che nessun dato è sentirsi persi.

 - Dopo il ripristino di hello: SAP HANA sulla gestione dei servizi Azure informa l'utente quando il ripristino di snapshot di archiviazione hello.

5. Una volta completato il processo di ripristino hello, reinstallare tutti i volumi di dati.

 ![Montare nuovamente tutti i volumi di dati](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. Selezionare le opzioni di ripristino in SAP HANA Studio, se vengono automaticamente viene visualizzata quando si riconnette tooHANA database tramite SAP HANA Studio. Hello esempio seguente viene illustrato un ripristino toohello ultimo HANA snapshot. Uno snapshot di archiviazione incorpora uno snapshot HANA e se si desidera ripristinare toohello snapshot di archiviazione più recente, dovrebbe essere snapshot HANA più recente di hello. (Se si desidera ripristinare gli snapshot di archiviazione tooolder, è necessario toolocate hello HANA basato su hello ora hello archiviazione snapshot dello snapshot.)

 ![Selezionare le opzioni di ripristino in SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Selezionare **Ripristina hello tooa dati specifici backup o archiviazione di snapshot del database**.

 ![finestra "Specifica del tipo di ripristino" Hello](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Scegliere **Specify backup without catalog** (Specifica il backup senza catalogo).

 ![finestra "Specifica del percorso di Backup" Hello](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. In hello **tipo destinazione** elenco, selezionare **Snapshot**.

 ![finestra "Specificare hello Backup tooRecover" Hello](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Fare clic su **fine** toostart il processo di ripristino hello.

 ![Fare clic su "Fine" processo di ripristino hello toostart](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. database HANA Hello viene ripristinato e recuperato snapshot HANA toohello che è incluso nello snapshot di archiviazione hello.

 ![Database HANA è snapshot HANA toohello ripristinato e recuperato](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Ripristino dello stato più recente di toohello

Hello seguente processo Ripristina snapshot HANA hello è incluso nello snapshot di archiviazione hello. Quindi, viene ripristinato hello transaction log backup toohello stato più recente del database hello prima del ripristino di snapshot di archiviazione hello.

>[!IMPORTANT]
>Prima di procedere assicurarsi di avere una catena contigua e completa di backup dei log delle transazioni. Senza questi backup, è possibile ripristinare lo stato corrente di hello del database hello.

1. Completare i passaggi 1-6 di hello precedenti procedura in "Recovering toohello snapshot più recente HANA."

2. Selezionare **ripristinare lo stato più recente di hello database tooits**.

 ![Selezionare "Ripristina allo stato più recente di hello database tooits"](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Specificare il percorso di hello hello più recente HANA di backup del log. percorso Hello deve toocontain tutti i backup di log delle transazioni HANA dallo stato più recente toohello hello HANA snapshot.

 ![Specificare il percorso di hello hello più recente HANA di backup del log](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Selezionare un backup come base dalla quale database hello toorecover. In questo esempio, si tratta di snapshot HANA hello incluse nello snapshot di archiviazione hello. (Un solo snapshot è elencato nella seguente schermata hello.)

 ![Selezionare un backup come base dalla quale database hello toorecover](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Crittografato hello **i backup differenziali di utilizzare** casella di controllo se non esistono delta tra hello snapshot HANA hello e allo stato più recente di hello.

 ![Casella di controllo "Utilizzare i backup differenziali" crittografato hello se è presente alcun delta](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Nella schermata di riepilogo hello, fare clic su **fine** toostart procedura di ripristino hello.

 ![Fare clic su "Fine" nella schermata di riepilogo hello](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>Recupero tooanother punto nel tempo
toorecover tooa punto nel tempo che intercorre tra snapshot HANA hello (incluso nello snapshot di archiviazione hello) e quella successiva alla hello HANA snapshot in fase di punto di ripristino, hello seguenti:

1. Assicurarsi di disporre di tutti i backup del log delle transazioni da hello HANA snapshot toohello ora in cui che si desidera toorecover.
2. Iniziare la procedura hello in "Recovering toohello allo stato più recente."
3. Nel passaggio 2 della procedura hello hello **Selezione tipo di ripristino** selezionare **seguente toohello database hello di ripristino temporizzato**, specificare hello punto nel tempo e quindi completare i passaggi 3-6.

## <a name="monitoring-hello-execution-of-snapshots"></a>Monitoraggio esecuzione hello di snapshot

È necessario l'esecuzione di hello toomonitor di snapshot di archiviazione. script di Hello che viene eseguito uno snapshot di archiviazione scrive file di output tooa e infine la salva toohello stesso percorso script Perl hello. Viene creato un file separato per ogni snapshot. output di Hello di ogni file mostra chiaramente hello diverse fasi che esegue script snapshot hello:

- Ricerca di volumi hello necessarie toocreate uno snapshot
- Ricerca di snapshot hello creati da questi volumi
- L'eliminazione di eventuale esistente snapshot toomatch hello numero di snapshot specificato
- Creazione di uno snapshot HANA
- Creazione di snapshot di archiviazione hello rispetto ai volumi hello
- L'eliminazione di snapshot HANA hello
- La ridenominazione più recente di hello snapshot troppo**,0**

parte più importante di Hello dello script hello è la seguente:
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
Da questo esempio è possibile vedere come i record di script hello hello creazione dello snapshot HANA hello. In caso di scalabilità orizzontale hello, questo processo viene avviato sul nodo principale hello. nodo principale Hello Avvia Creazione sincrona di hello di snapshot hello in ognuno dei nodi di lavoro hello. Quindi hello archiviazione dello snapshot. Dopo l'esecuzione corretta di hello di snapshot di archiviazione hello, snapshot HANA hello viene eliminato.
