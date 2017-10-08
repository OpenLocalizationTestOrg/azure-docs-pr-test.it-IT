---
title: Panoramica della soluzione serie 8000 aaaStorSimple | Documenti Microsoft
description: Descrive la suddivisione in livelli di StorSimple, dispositivo hello, dispositivo virtuale, servizi e la gestione dell'archiviazione e introduce termini chiave utilizzati in StorSimple.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>Serie 8000 StorSimple: una soluzione di archiviazione cloud ibrida
## <a name="overview"></a>Panoramica
Benvenuti tooMicrosoft StorSimple di Azure, una soluzione di archiviazione integrata che gestisce le attività tra dispositivi locali e l'archiviazione cloud di Microsoft Azure. StorSimple è una soluzione di rete (SAN) area di archiviazione efficiente, conveniente e facilmente gestibile che elimina molti problemi hello e spese associate enterprise archiviazione e protezione dei dati. Usa hello proprietaria dispositivo StorSimple serie 8000, si integra con servizi cloud e fornisce un set di strumenti di gestione per una semplice visualizzazione di tutti gli archivi dell'organizzazione, inclusa l'archiviazione cloud. (informazioni sulla distribuzione di StorSimple hello pubblicate sul sito Web di Microsoft Azure hello applica tooStorSimple solo dispositivi della serie 8000. Se si utilizza un dispositivo serie 5000 o 7000 StorSimple, andare troppo[StorSimple Guida](http://onlinehelp.storsimple.com/).)

StorSimple Usa [tiering di archiviazione](#automatic-storage-tiering) toomanage i dati archiviati in vari supporti di archiviazione. working set corrente di Hello è archiviata in locale nel (SSD), i dati utilizzati meno frequentemente vengono archiviati in unità disco rigido (HDD) e i dati di archiviazione viene inseriti toohello cloud. Inoltre, StorSimple utilizza la deduplicazione e la quantità di hello tooreduce la compressione di archiviazione dati hello utilizza. Per ulteriori informazioni, visitare troppo[deduplicazione e compressione](#deduplication-and-compression). Per le definizioni di altri termini e concetti chiave utilizzati nella documentazione di serie StorSimple 8000 hello, andare troppo[terminologia di StorSimple](#storsimple-terminology) alla fine di hello di questo articolo.

Inoltre toostorage gestione, funzionalità di protezione dati di StorSimple abilitare si toocreate su richiesta e i backup pianificati e archiviarlo in cloud localmente o in hello. I backup vengono eseguiti sotto forma di hello di snapshot incrementali, il che significa che può essere creati e ripristinati rapidamente. Gli snapshot cloud possono essere estremamente importanti in scenari di ripristino di emergenza perché sostituire i sistemi di archiviazione secondaria (ad esempio il backup su nastro) e consentono di toorestore dati tooyour Data Center o tooalternate siti se necessario.

![icona video](./media/storsimple-overview/video_icon.png) Guardare video hello per tooMicrosoft una rapida introduzione StorSimple di Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>Vantaggi dell'uso di StorSimple
Hello nella tabella seguente vengono descritti alcuni dei vantaggi chiave hello che fornisce a Microsoft Azure StorSimple.

| Funzionalità | Vantaggi |
| --- | --- |
| Integrazione trasparente |Utilizza strutture di archiviazione di hello iSCSI protocollo tooinvisibly collegamento dati. Questo assicura che i dati archiviati nel cloud hello, in Data Center hello, o su server remoti appaiano toobe archiviati in un'unica posizione. |
| Riduzione dei costi di archiviazione |Alloca sufficiente locale o cloud le richieste correnti di archiviazione toomeet ed estende la memoria cloud solo quando necessario. Riduce ulteriormente i requisiti di archiviazione e spese eliminando le versioni ridondanti di hello stessi dati (deduplicazione) e utilizzando la compressione. |
| Gestione dell'archiviazione semplificata |Fornisce tooconfigure strumenti di amministrazione del sistema e gestire i dati archiviati in locale, in un server remoto e nel cloud hello. Inoltre, è possibile gestire backup e ripristino di funzioni da uno snap-in Microsoft Management Console (MMC).|
| Miglioramento del ripristino di emergenza e della conformità |Non richiede tempi eccessivi per il ripristino. Ripristina invece i dati quando è necessario. Le normali operazioni possono quindi continuare con un'interruzione minima. Inoltre, è possibile configurare pianificazioni di backup toospecify di criteri e conservazione dei dati. |
| Mobilità dei dati |Dati caricati tooMicrosoft accessibili da altri siti a scopo di ripristino e migrazione di servizi cloud di Azure. Inoltre, è possibile utilizzare dispositivi di StorSimple tooconfigure StorSimple Cloud nelle macchine virtuali (VM) in esecuzione in Microsoft Azure. Hello macchine virtuali quindi possibile utilizzare dati di dispositivi virtuali tooaccess archiviati a scopo di test o ripristino. |
| Continuità aziendale |Consente di 5000 7000 StorSimple serie utenti toomigrate dispositivo serie di dati tooa StorSimple 8000. |
| Disponibilità in hello portale di Azure per enti pubblici |StorSimple è disponibile nel portale di Azure per enti pubblici hello. Per ulteriori informazioni, vedere [distribuire il dispositivo StorSimple locale nel portale amministrativo hello](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Disponibilità e protezione dei dati |Hello StorSimple serie 8000 supporta zona ridondanti archiviazione (ZRS), in aggiunta tooLocally archiviazione ridondante (LRS) e archiviazione con ridondanza geografica (GRS). Fare riferimento troppo[questo articolo sulle opzioni di ridondanza di archiviazione di Azure](https://azure.microsoft.com/documentation/articles/storage-redundancy/) per i dettagli di ridondanza della zona. |
| Supporto per applicazioni critiche |Il cloud consente di StorSimple di identificare i volumi appropriati come aggiunto in locale che a sua volta consente ai dati necessari per le applicazioni critiche non toohello a più livelli. I volumi aggiunti in locale non sono le latenze toocloud del soggetto o problemi di connettività. Per ulteriori informazioni sui volumi aggiunti in locale, vedere [utilizzare volumi toomanage servizio di gestione di dispositivi StorSimple hello](storsimple-8000-manage-volumes-u2.md). |
| Bassa latenza e alte prestazioni |È possibile creare dispositivi cloud che sfruttano ad alte prestazioni hello, bassa latenza funzionalità di archiviazione premium di Azure. Per altre informazioni sulle appliance cloud Premium StorSimple, vedere [Distribuire e gestire un'appliance cloud StorSimple in Azure](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>Componenti di StorSimple
Hello soluzioni di Microsoft Azure StorSimple include hello seguenti componenti:

* **Dispositivo Microsoft Azure StorSimple** : array di archiviazione ibrida locale contenente unità SSD e unità disco rigido, oltre a controller ridondanti e funzionalità di failover automatico. controller Hello gestire l'archiviazione a più livelli, il posizionamento attualmente usati (o hot) dati nell'archiviazione locale (in hello dispositivo o in locale server), durante lo spostamento di dati utilizzati meno frequentemente toohello nel cloud.
* **StorSimple Appliance di Cloud** : anche noto come hello dispositivo virtuale StorSimple, si tratta di una versione software del dispositivo StorSimple hello che replica l'architettura di hello e la maggior parte delle funzionalità del dispositivo di archiviazione ibrido fisico hello. Hello StorSimple Appliance di Cloud viene eseguito in un singolo nodo in una macchina virtuale di Azure. I dispositivi virtuali Premium, che sfruttano i vantaggi dell'archiviazione Premium di Azure, sono disponibili nell'aggiornamento 2 e versioni successive.
* **Servizio di gestione di dispositivi StorSimple** : estensione del portale di Azure che consente di gestire un dispositivo StorSimple o StorSimple Appliance di Cloud da una singola interfaccia web hello. È possibile utilizzare toocreate servizio di gestione di dispositivi StorSimple hello e gestire i servizi, visualizzare e gestire i dispositivi, visualizzare gli avvisi, gestire i volumi e visualizzare e gestire criteri di backup e catalogo di backup hello.
* **Windows PowerShell per StorSimple** : un'interfaccia della riga di comando che è possibile utilizzare toomanage hello dispositivo StorSimple. Windows PowerShell per StorSimple include funzionalità che consentono di tooregister dispositivo StorSimple, configurare l'interfaccia di rete hello sul dispositivo, installare alcuni tipi di aggiornamento, risolvere i problemi del dispositivo per l'accesso alla sessione di supporto hello e modificare hello stato del dispositivo. È possibile accedere Windows PowerShell per StorSimple toohello connette la console seriale o tramite la comunicazione remota di Windows PowerShell.
* **Cmdlet di Azure PowerShell StorSimple** : una raccolta di cmdlet di Windows PowerShell che consentono di attività di migrazione e a livello di servizio tooautomate dalla riga di comando hello. Per ulteriori informazioni su hello cmdlet di Azure PowerShell per StorSimple, visitare toohello [riferimento ai cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **Gestione Snapshot StorSimple** : uno snap-in MMC che utilizza gruppi di volumi e backup coerenti con l'applicazione toogenerate del servizio Copia Shadow del Volume di Windows hello. Inoltre, è possibile usare clone e gestione Snapshot StorSimple toocreate pianificazioni di backup o ripristinare volumi.
* **Adattatore StorSimple per SharePoint** : uno strumento che estende in modo trasparente la protezione dati e archiviazione di Microsoft Azure StorSimple tooSharePoint Server farm, rendendo l'archiviazione StorSimple visualizzabile e gestibile dal hello centrale di SharePoint Portale di amministrazione.

diagramma di Hello seguente fornisce una panoramica dell'architettura di Microsoft Azure StorSimple hello e componenti.

![Architettura di StorSimple](./media/storsimple-overview/overview-big-picture.png)

Hello nelle sezioni seguenti viene descritto ciascuno di questi componenti in modo più dettagliato e illustrano come soluzione hello organizza i dati, alloca spazio di archiviazione e facilita la gestione dell'archiviazione e protezione dei dati. ultima sezione Hello fornisce definizioni di alcuni dei termini importanti hello e componenti correlati tooStorSimple concetti e la gestione.

## <a name="storsimple-device"></a>Dispositivo StorSimple
dispositivo di Microsoft Azure StorSimple Hello è un array di archiviazione ibrido locale che fornisce archiviazione primaria e toodata accesso iSCSI archiviati al suo interno. Gestisce la comunicazione con l'archiviazione cloud e consente di sicurezza hello tooensure e la riservatezza di tutti i dati archiviati in soluzioni di Microsoft Azure StorSimple hello.

dispositivo StorSimple Hello include unità SSD e HDD unità disco rigido, nonché il supporto per il failover automatico e di clustering. Contiene un processore condiviso, uno spazio di archiviazione condiviso e due controller con mirroring. Ciascun controller fornisce seguente hello:

* Computer host di connessione tooa
* Backup toosix rete porte tooconnect toohello rete locale (LAN)
* Monitoraggio hardware
* Memoria NVRAM (Non-Volatile Random Access Memory), per mantenere le informazioni anche in caso di interruzione dell'alimentazione
* Compatibile con cluster aggiornamento toomanage di aggiornamenti software nei server in un cluster di failover in modo che gli aggiornamenti di hello minima o alcun effetto sulla disponibilità del servizio
* Servizio cluster, con funzionamento analogo a quello di un cluster back-end, in grado di fornire disponibilità elevata e ridurre al minimo gli effetti negativi provocati da un eventuale errore o disconnessione di un'unità disco rigido o SSD

Solo uno dei due controller è sempre attivo. Se il controller attivo hello ha esito negativo, il secondo controller di hello diventa attiva automaticamente.

Per ulteriori informazioni, visitare troppo[StorSimple componenti hardware e lo stato](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>Appliance cloud StorSimple
È possibile utilizzare toocreate StorSimple appliance cloud che consente di replicare hello architettura e le funzionalità di dispositivo di archiviazione ibrido fisico hello. Hello StorSimple Appliance di Cloud (noto anche come dispositivo virtuale StorSimple Buongiorno) viene eseguito in un singolo nodo in una macchina virtuale di Azure. Un'appliance cloud può essere creata solo in una macchina virtuale di Azure e non in un dispositivo StorSimple o in un server locale.

dispositivo cloud Hello è hello seguenti caratteristiche:

* Si comporta come un dispositivo fisico e può offrire una iSCSI macchine toovirtual interfaccia nel cloud hello.
* È possibile creare un numero illimitato di accessori cloud in cloud hello e attivarli e disattivare in base alle esigenze.
* Consente di simulare ambienti locali in scenari di ripristino di emergenza, sviluppo e test ed è in grado di facilitare il recupero a livello di elementi dai backup.

Hello StorSimple Appliance di Cloud è disponibile in due modelli: dispositivo hello 8010: spazio (precedentemente noto come modello hello 1100) e hello 8020 dispositivo. dispositivo 8010 Hello ha una capacità massima di 30 TB. dispositivo 8020 Hello, che sfrutta i vantaggi di archiviazione premium di Azure, ha una capacità massima di 64 TB. Nei livelli locali l'archiviazione Premium di Azure archivia i dati all'interno di unità SSD, mentre l'archiviazione Standard archivia i dati in unità disco rigido. Si noti che è necessario disporre di una risorsa di archiviazione premium di Azure storage account toouse premium. Per ulteriori informazioni sull'archiviazione premium, visitare troppo[archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro di macchina virtuale Azure](../storage/common/storage-premium-storage.md).

Per ulteriori informazioni su StorSimple Appliance di Cloud hello, andare troppo[distribuire e gestire un dispositivo StorSimple per Cloud in Azure](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>Servizio Gestione dispositivi StorSimple
Microsoft Azure StorSimple offre un'interfaccia utente basata sul web (servizio di gestione di dispositivi StorSimple Buongiorno) che consente di toocentrally gestire Data Center e l'archiviazione cloud. È possibile utilizzare hello tooperform servizio StorSimple Manager di dispositivi di hello seguenti attività:

* Configurare le impostazioni di sistema per i dispositivi StorSimple.
* Configurare e gestire le impostazioni di sicurezza per i dispositivi StorSimple.
* Configurare le credenziale e le proprietà cloud.
* Configurare e gestire volumi su un server.
* Configurare gruppi di volumi.
* Eseguire il backup e il ripristino dei dati.
* Monitorare le prestazioni.
* Rivedere le impostazioni di sistema e identificare possibili problemi.

È possibile utilizzare tooperform servizio di gestione di dispositivi StorSimple hello tutte le attività amministrative ad eccezione di quelli che richiedono l'inattività tempo, ad esempio la configurazione iniziale e l'installazione degli aggiornamenti del sistema.

Per ulteriori informazioni, visitare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>Windows PowerShell per StorSimple 
Windows PowerShell per StorSimple fornisce un'interfaccia della riga di comando che è possibile utilizzare toocreate e gestire il servizio Microsoft Azure StorSimple hello e configurare e monitorare i dispositivi StorSimple. Si tratta di un'interfaccia della riga di comando basata su Windows PowerShell, che include cmdlet dedicati per la gestione del dispositivo StorSimple. Windows PowerShell per StorSimple offre funzionalità che consentono di:

* Registrare un dispositivo.
* Configurare l'interfaccia di rete hello in un dispositivo.
* Installare determinati tipi di aggiornamento.
* Risolvere i problemi del dispositivo l'accesso alla sessione di supporto hello.
* Modificare lo stato del dispositivo hello.

È possibile accedere a Windows PowerShell per StorSimple da una console seriale (in un host computer connesso direttamente toohello dispositivo) o in modalità remota tramite la comunicazione remota di Windows PowerShell. Si noti che alcune Windows PowerShell per StorSimple attività, ad esempio la registrazione iniziale del dispositivo, può essere eseguita solo sulla console seriale hello.

Per ulteriori informazioni, visitare troppo[utilizzare Windows PowerShell per StorSimple tooadminister dispositivo](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>i cmdlet PowerShell di azure StorSimple
i cmdlet di PowerShell Azure StorSimple Hello sono un insieme di cmdlet di Windows PowerShell che consentono di tooautomate a livello di servizio e le attività di migrazione dalla riga di comando hello. Per ulteriori informazioni su hello cmdlet di Azure PowerShell per StorSimple, visitare toohello [riferimento ai cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>Gestione snapshot StorSimple
Gestione Snapshot StorSimple è uno snap-in Microsoft Management Console (MMC) che è possibile utilizzare toocreate coerente, in un momento copie di backup locale e nel cloud i dati. Hello snap-in viene eseguito in un host basato su Windows Server. Gestione snapshot StorSimple può essere usato per:

* Configurare, eseguire il backup ed eliminare volumi.
* Configurare il volume tooensure gruppi di dati di backup è coerente con l'applicazione.
* Gestire criteri di backup in modo che i dati vengano eseguito il backup su una pianificazione predeterminata e archiviati in una posizione designata (in locale o nel cloud hello).
* Ripristinare volumi e singoli file.

I backup vengono acquisiti come snapshot, registrare solo le modifiche di hello poiché hello ultimo snapshot e che richiede molto meno spazio di archiviazione di backup completi. A seconda delle necessità, è possibile creare pianificazioni dei backup o eseguire backup immediati. Inoltre, è possibile utilizzare Gestione Snapshot StorSimple tooestablish i criteri di conservazione che controllano il numero di snapshot verrà salvato. Se è necessario successivamente toorestore dati da un backup, di StorSimple Snapshot Manager consente selezionare dal catalogo di hello locale o snapshot cloud. 

Se si verifica un'emergenza o se è necessario toorestore dati per un altro motivo, gestione Snapshot StorSimple ripristinarlo in modo incrementale quando è necessario. Il ripristino dei dati non è necessario arrestare intero sistema hello mentre si ripristina un file, sostituzione di un componente o lo spostamento del sito tooanother operazioni.

Per ulteriori informazioni, visitare troppo[che cos'è StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>Adattatore StorSimple per SharePoint
Microsoft Azure StorSimple include hello adattatore StorSimple per SharePoint, un componente opzionale che estende in modo trasparente le farm di server tooSharePoint funzionalità StorSimple archiviazione e protezione dei dati. l'adattatore Hello funziona con un provider di archiviazione Blob remoti (RBS) e funzionalità di SQL Server RBS hello, consentendo di toomove BLOB tooa server supportato dal sistema di Microsoft Azure StorSimple hello. Microsoft Azure StorSimple quindi Archivia i dati BLOB hello in locale o cloud hello, in base all'utilizzo.

Hello adattatore StorSimple per SharePoint è gestito da nel portale di amministrazione centrale SharePoint hello. Di conseguenza, gestione di SharePoint rimane centralizzata e tutta l'archiviazione viene visualizzato toobe nella farm di SharePoint hello.

Per ulteriori informazioni, visitare troppo[adattatore StorSimple per SharePoint](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Tecnologie di gestione dell'archiviazione
Inoltre toohello dedicato dispositivo StorSimple, il dispositivo virtuale e altri componenti, Microsoft Azure StorSimple Usa hello software tecnologie tooprovide accesso rapido toodata e tooreduce consumo di archiviazione seguenti:

* [Suddivisione automatica in livelli dell'archiviazione](#automatic-storage-tiering) 
* [Thin provisioning](#thin-provisioning) 
* [Deduplicazione e compressione](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>Suddivisione automatica in livelli dell'archiviazione
Microsoft Azure StorSimple organizza automaticamente i dati in livelli logici in base alle informazioni sull'utilizzo corrente, l'età e dati tooother della relazione. I dati più attivi vengono archiviati in locale, mentre è meno attivo e inattivi dati vengono automaticamente migrati toohello cloud. Hello seguente diagramma illustra questo approccio di archiviazione.

![Livelli di archiviazione di StorSimple](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

accesso rapido tooenable, StorSimple archivia dati molto attivi (hot data) su unità SSD nel dispositivo StorSimple hello. Archivia invece i dati usati occasionalmente (warm data) nelle unità disco rigido nel dispositivo hello o nei server datacenter hello. Sposta i dati di backup, i dati inattivi e i dati mantenuti per archiviazione o conformità a scopo toohello cloud. 

> [!NOTE]
> In Update 2 o versioni successive, è possibile specificare un volume aggiunto in locale, nel qual caso hello dati rimangono nel dispositivo locale hello e non a livelli toohello cloud. 


StorSimple ordina e riorganizza i dati e le assegnazioni delle risorse di archiviazione in base ai cambiamenti dei modelli di utilizzo. Alcune informazioni, ad esempio, possono diventare meno attive nel corso del tempo. Appena sarà progressivamente meno attivo, viene eseguita la migrazione da tooHDDs unità SSD e quindi toohello cloud. Se gli stessi dati diventano nuovamente attivi, è il dispositivo di archiviazione toohello indietro migrati.

processo di suddivisione in livelli di archiviazione Hello avviene nel modo seguente:

1. Un amministratore di sistema configura un account di archiviazione cloud di Microsoft Azure.
2. messaggio per l'amministratore utilizza hello seriale console e hello dispositivo StorSimple Manager servizio (in esecuzione in hello portale di Azure) tooconfigure hello dispositivo e file server, la creazione di criteri di protezione di volumi e i dati. Il computer locale (ad esempio file server) usa il dispositivo StorSimple di hello Internet Small Computer System Interface (iSCSI) tooaccess hello.
3. Inizialmente, StorSimple archivia i dati nel livello SSD veloce di hello del dispositivo hello.
4. Come hello approcci capacità del livello SSD, StorSimple deduplicates comprime i blocchi di dati meno recenti hello e li sposta livello HDD toohello.
5. Come hello capacità approcci del livello HDD, StorSimple crittografa i blocchi di dati meno recenti hello e li invia in modo sicuro toohello account di archiviazione di Microsoft Azure tramite HTTPS.
6. Microsoft Azure crea più repliche dei dati hello nel proprio centro dati e in un Data Center remoto, assicurandosi che i dati hello possano essere ripristinati in caso di emergenza.
7. Quando il server di file hello richiede dati archiviati nel cloud hello, StorSimple restituisce facilmente e archivia una copia nel livello SSD hello del dispositivo StorSimple hello.

#### <a name="how-storsimple-manages-cloud-data"></a>In che modo StorSimple gestisce i dati del cloud

StorSimple deduplicates i dati dei clienti in tutti gli snapshot hello e dati primario hello (dati scritti dall'host). Durante la deduplicazione è molto utile per migliorare l'efficienza di archiviazione, rende domanda hello "che cos'è nel cloud hello" complicato. Hello dati primaria a più livelli e dei dati dello snapshot hello sovrappongano tra loro. Un singolo blocco di dati nel cloud hello può essere utilizzato come dati primaria a più livelli e anche fare riferimento più snapshot. Ogni snapshot nel cloud garantisce che una copia di tutti i dati in un momento hello è bloccata in cloud hello fino a quando non viene eliminato lo snapshot.

Dati viene eliminati solo dal cloud hello quando sono non presenti dati toothat riferimenti. Ad esempio, se è uno snapshot cloud di tutti i dati di hello che nel dispositivo StorSimple hello e quindi eliminare alcuni dati primari, si vedrà hello _dati primario_ eliminare immediatamente. Hello _cloud dati_ che include i dati a più livelli di hello e hello backup, rimane hello stesso. In questo modo è uno snapshot ancora riferimento ai dati di cloud hello. Dopo il cloud hello snapshot viene eliminato e snapshot a cui fa riferimento hello stessi dati, Elimina il consumo del cloud. Prima di rimuovere i dati cloud, è necessario controllare che non esistano altre snapshot che ancora fanno riferimento a tali dati. Questo processo è denominato _operazione di garbage collection_ e un servizio in background è in esecuzione sul dispositivo hello. Rimozione di dati di cloud non è immediata come servizio di raccolta garbage hello Cerca altri riferimenti a dati toothat prima dell'eliminazione di hello. velocità di Hello di garbage collection dipende dal numero totale di hello di snapshot e dati totale hello. In genere, hello cloud pulitura dei dati in meno di una settimana.


### <a name="thin-provisioning"></a>Thin provisioning
Thin provisioning è una tecnologia di virtualizzazione in cui archiviazione disponibili risultano tooexceed di risorse fisiche. Anziché riservare in anticipo sufficiente spazio di archiviazione, StorSimple Usa tooallocate di provisioning thin sufficiente spazio toomeet corrente. natura elastica di Hello dell'archiviazione cloud facilita questo approccio perché StorSimple può aumentare o diminuire cloud archiviazione toomeet cambiare della domanda.

> [!NOTE]
> Non viene eseguito il thin provisioning dei volumi aggiunti in locale. Spazio di archiviazione allocato tooa solo locale volume viene eseguito il provisioning nella sua interezza quando si crea il volume di hello.


### <a name="deduplication-and-compression"></a>Deduplicazione e compressione
Microsoft Azure StorSimple Usa tecniche di deduplicazione e toofurther la compressione dei dati è possibile ridurre i requisiti di archiviazione.

La deduplicazione riduce hello quantità totale di dati archiviati eliminando la ridondanza nel set di dati archiviato hello. In base alle informazioni, StorSimple ignora dati hello invariata e acquisizioni hello solo le modifiche. Inoltre, StorSimple riduce hello di dati archiviati identificando e rimuovendo le informazioni. 

> [!NOTE]
> I dati sui volumi aggiunti in locale non sono deduplicati o compressi. Tuttavia, i backup dei volumi aggiunti in locale sono deduplicati e compressi.


## <a name="storsimple-workload-summary"></a>Riepilogo dei carichi di lavoro di StorSimple
Un riepilogo dei carichi di lavoro StorSimple hello supportato è inserito sotto.

| Scenario | Carico di lavoro | Supportato | Restrizioni | Versione |
| --- | --- | --- | --- | --- |
| Collaborazione |Condivisione di file |Sì | |Tutte le versioni |
| Collaborazione |Condivisione di file distribuita |Sì | |Tutte le versioni |
| Collaborazione |SharePoint |Sì* |Supportata solo con i volumi aggiunti in locale |Aggiornamento 2 e successivi |
| Archiviazione |Archiviazione di file semplice |Sì | |Tutte le versioni |
| Virtualizzazione |Macchine virtuali |Sì* |Supportata solo con i volumi aggiunti in locale |Aggiornamento 2 e successivi |
| Database |SQL |Sì* |Supportata solo con i volumi aggiunti in locale |Aggiornamento 2 e successivi |
| Sorveglianza video |Sorveglianza video |Sì* |È supportato quando il dispositivo StorSimple sia dedicato solo toothis carico di lavoro |Aggiornamento 2 e successivi |
| Backup |Backup di destinazione primario |Sì* |È supportato quando il dispositivo StorSimple sia dedicato solo toothis carico di lavoro |Aggiornamento 3 e successivi |
| Backup |Backup di destinazione secondario |Sì* |È supportato quando il dispositivo StorSimple sia dedicato solo toothis carico di lavoro |Aggiornamento 3 e successivi |

*Sì&amp;#42;: devono essere applicate le restrizioni e le linee guida per la soluzione.*

Hello seguendo i carichi di lavoro non è supportato da dispositivi della serie StorSimple 8000. Se distribuiti in StorSimple, questi carichi di lavoro comportano una configurazione non supportata.

* Diagnostica per immagini
* Exchange
* VDI
* Oracle
* SAP
* Big Data
* Distribuzione di contenuti
* Avvio da SCSI

Ecco un elenco dei componenti dell'infrastruttura di hello StorSimple è supportato.

| Scenario | Carico di lavoro | Supportato | Restrizioni | Versione |
| --- | --- | --- | --- | --- |
| Generale |Express Route |Sì | |Tutte le versioni |
| Generale |DataCore FC |Sì* |Supportato con DataCore SANsymphony |Tutte le versioni |
| Generale |DFSR |Sì* |Supportata solo con i volumi aggiunti in locale |Tutte le versioni |
| Generale |Indicizzazione |Sì* |Per i volumi a più livelli, è supportata solo l'indicizzazione dei metadati (nessun dato).<br>Per i volumi aggiunti in locale, è supportata l'indicizzazione completa. |Tutte le versioni |
| Generale |Anti-virus |Sì* |Per i volumi a più livelli, è supportata solo l'analisi in apertura e in chiusura.<br> Per i volumi aggiunti in locale, è supportata l'analisi completa. |Tutte le versioni |

*Sì&amp;#42;: devono essere applicate le restrizioni e le linee guida per la soluzione.*

Ecco un elenco di altri prodotti software che vengono usati con soluzioni toobuild StorSimple.

| Tipo di carico di lavoro | Software usato con StorSimple | Versioni supportate|Collegamento Guida toosolution| 
| --- | --- | --- | --- |
| Destinazione backup |Veeam |Veeam 9 e versioni successive |[StorSimple come destinazione di backup con Veeam](storsimple-configure-backup-target-veeam.md)|
| Destinazione backup |Veritas Backup Exec |Backup Exec 16 e versioni successive |[StorSimple come destinazione di backup con Backup Exec](storsimple-configure-backup-target-using-backup-exec.md)|
| Destinazione backup |Veritas NetBackup |NetBackup 7.7.x e versioni successive  |[StorSimple come destinazione di backup con NetBackup](storsimple-configure-backuptarget-netbackup.md)|
| Condivisione globale file <br></br> Collaborazione |Talon  |[StorSimple con Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>Terminologia di StorSimple
Prima di distribuire la soluzione di Microsoft Azure StorSimple, che è consigliabile consultare seguente hello termini e definizioni.

### <a name="key-terms-and-definitions"></a>Termini e definizioni chiave
| Termine (acronimo o abbreviazione) | Descrizione |
| --- | --- |
| record di controllo di accesso |Un record associato a un volume nel dispositivo StorSimple di Microsoft Azure che determina quali host possono connettersi tooit. determinazione di Hello è basata su iSCSI hello nome qualificato di hello host (contenuto in hello ACR) che si connette il dispositivo di StorSimple tooyour. |
| AES-256 |Un algoritmo Advanced Encryption Standard (AES) a 256 bit per la crittografia dei dati durante lo spostamento tooand dal cloud hello. |
| dimensioni delle unità di allocazione |Hello quantità minima di spazio su disco che può essere allocata toohold un file dei sistemi di file di Windows. Se un file di dimensioni non è un multiplo delle dimensioni di cluster hello, lo spazio aggiuntivo deve essere file hello toohold utilizzato (backup toohello multiplo successivo delle dimensioni di cluster hello) conseguente perdita di spazio e frammentazione del disco rigido hello. <br>Hello consigliabile in quanto funziona bene con algoritmi di deduplicazione hello AUS per i volumi StorSimple di Azure è di 64 KB. |
| suddivisione in livelli di archiviazione automatizzata |Spostamento automatico di dati meno attivi dall'unità SSD tooHDDs e quindi tooa livello cloud hello e abilitazione della gestione di tutta la memoria da un'interfaccia utente centrale. |
| catalogo di backup |Raccolta di backup, in genere correlati dal tipo di applicazione hello che è stato utilizzato. Questa raccolta viene visualizzata nel Pannello di catalogo di Backup hello di hello interfaccia utente del servizio gestione di dispositivi StorSimple. |
| file del catalogo di backup |Un file contenente un elenco di snapshot disponibili attualmente archiviati nel database di backup hello di StorSimple Snapshot Manager. |
| criterio di backup |Selezione di volumi, tipo di backup e orari che consentono backup toocreate una pianificazione predefinita. |
| BLOB (Binary Large Object) |Raccolta di dati binari archiviati come singola entità in un sistema di gestione database. I BLOB sono in genere immagini, audio o altri oggetti multimediali, anche se a volte il codice eseguibile binario viene archiviato come BLOB. |
| CHAP (Challenge Handshake Authentication Protocol) |Protocollo utilizzato peer hello tooauthenticate di una connessione, in base a peer hello la condivisione di una password o un segreto. CHAP può essere unidirezionale o reciproco. Con CHAP unidirezionale, destinazione hello autentica un iniziatore. L'autenticazione CHAP reciproca è necessario che destinazione hello autentichi iniziatore hello e tale iniziatore hello autentica la destinazione hello. |
| clone |Copia duplicata di un volume. |
| CaaT (Cloud as a Tier) |Archiviazione cloud integrata come livello nell'architettura di archiviazione hello in modo che tutti gli archivi visualizzato toobe parte della rete di archiviazione di un enterprise. |
| provider di servizi cloud  (CSP) |Provider di servizi di cloud computing. |
| snapshot cloud |Copia dei dati di volume archiviati nel cloud hello punto nel tempo. Uno snapshot cloud equivale tooa snapshot replicato su un sistema di archiviazione fuori sede diversi. Gli snapshot cloud sono particolarmente utili negli scenari di ripristino di emergenza. |
| chiave di crittografia di archiviazione cloud |Una password o una chiave utilizzata dai dati StorSimple dispositivo tooaccess crittografato hello inviati dal cloud toohello di dispositivo. |
| aggiornamento compatibile con cluster |La gestione degli aggiornamenti software nei server in un cluster di failover in modo che gli aggiornamenti di hello minima o alcun effetto sulla disponibilità del servizio. |
| percorso dati |Raccolta di unità funzionali che eseguono operazioni di elaborazione dei dati interconnessi. |
| disattivare |Azione definitiva che interruzioni hello connessione tra il dispositivo di StorSimple hello e hello associati servizio cloud. Gli snapshot cloud del dispositivo hello permangono dopo questo processo e possono essere clonati o utilizzati per il ripristino di emergenza. |
| mirroring disco |Replica dei volumi di disco logico su disco rigido separato unità in tempo reale tooensure la disponibilità continua. |
| mirroring disco dinamico |Replica di volumi di dischi logici su dischi dinamici. |
| dischi dinamici |Un formato di volume su disco che utilizza hello toostore dischi Manager (LOGICI) e gestione i dati tra più dischi fisici. I dischi dinamici può essere ingrandita tooprovide più spazio libero. |
| Chassis EBOD (Extended Bunch of Disks) |Chassis secondario del dispositivo Microsoft Azure StorSimple che contiene dischi rigidi aggiuntivi per un maggiore spazio di archiviazione. |
| fat provisioning |Provisioning di archiviazione tradizionale in cui archiviazione, lo spazio viene allocato in base alle esigenze previste (ed è in genere maggiore hello attualmente necessario). Vedere anche *thin provisioning*. |
| unità disco rigido |Un'unità che utilizza i dati di toostore rotazione piatti. |
| risorsa di archiviazione cloud ibrida |Architettura di archiviazione che utilizza risorse locali e fuori sede, inclusa l'archiviazione cloud. |
| iSCSI (Internet Small Computer System Interface) |Standard di rete per l'archiviazione basata sul protocollo IP per collegare le apparecchiature o le strutture di archiviazione dei dati. |
| iniziatore iSCSI |Componente software che consente a un computer host in esecuzione sulla rete di archiviazione esterna basata su iSCSI tooan tooconnect Windows. |
| nome qualificato iSCSI (IQN) |Nome univoco che identifica una destinazione o un iniziatore iSCSI. |
| destinazione iSCSI |Componente software che fornisce sottosistemi di dischi iSCSI centralizzati nelle reti di archiviazione. |
| archiviazione live |Un approccio di archiviazione in cui i dati di archiviazione sono accessibili tutto il tempo hello (non viene memorizzato fuori sede su nastro, ad esempio). Microsoft Azure StorSimple utilizza l'archiviazione live. |
| volume aggiunto in locale |un volume che si trova sul dispositivo hello e non è mai a livelli toohello cloud. |
| snapshot locale |Copia dei dati di volume archiviati nel dispositivo Microsoft Azure StorSimple hello punto nel tempo. |
| Microsoft Azure StorSimple |Una potente soluzione composta da un dispositivo di archiviazione Data Center e il software che consente tooleverage le organizzazioni IT archiviazione cloud come se fosse l'archiviazione Data Center. StorSimple consente di semplificare la protezione e la gestione dei dati riducendo contemporaneamente i costi. soluzione Hello consolida primario archiviazione, archiviazione, backup e ripristino (ripristino di emergenza) attraverso l'integrazione perfetta con cloud hello. Combinando l'archiviazione SAN con la gestione dati nel cloud in una piattaforma di livello professionale, i dispositivi StorSimple garantiscono velocità, semplicità e affidabilità per tutte le esigenze di archiviazione. |
| modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) |Pertanto, i componenti hardware del dispositivo StorSimple è composta da hello alimentatori e hello ventola di raffreddamento hello modulo di alimentazione e raffreddamento di nome. enclosure principale di Hello del dispositivo hello ha due PCM da 764 w, mentre hello chassis EBOD ha due PCM da 580 w. |
| chassis principale |Chassis principale del dispositivo StorSimple che contiene i controller della piattaforma dell'applicazione hello. |
| obiettivo tempo di ripristino (RTO, Recovery Time Objective) |quantità massima di Hello di tempo che deve trascorrere prima che un processo di business o un sistema venga completamente ripristinato dopo un'emergenza. |
| SAS (Serial Attached SCSI) |Tipo di unità disco rigido. |
| chiave DEK del servizio |Una chiave resa disponibile tooany nuovo dispositivo di StorSimple registrati con il servizio di gestione di dispositivi StorSimple hello. i dati di configurazione Hello trasferiti tra il servizio di gestione di dispositivi StorSimple hello e hello viene crittografati con una chiave pubblica e quindi possono essere decrittografati solo sul dispositivo hello utilizzando una chiave privata. Chiave DEK del servizio consente hello servizio tooobtain la chiave privata per la decrittografia. |
| chiave di registrazione del servizio |Una chiave che consente di registrare il dispositivo di StorSimple hello con hello del servizio di gestione di dispositivi StorSimple in modo che appaia nella hello portale di Azure per altre azioni di gestione. |
| SCSI (Small Computer System Interface) |Set di standard per connettere fisicamente i computer e passare i dati da uno all'altro. |
| unità SSD |Disco senza componenti mobili, ad esempio un'unità flash. |
| archiviazione di Azure |Un set di credenziali di accesso collegato tooyour account di archiviazione per un provider del servizio cloud specificato. |
| Adattatore StorSimple per SharePoint |Un componente di Microsoft Azure StorSimple che estende in modo trasparente la protezione dati e archiviazione StorSimple tooSharePoint server farm. |
| Servizio Gestione dispositivi StorSimple |Un'estensione di hello portale di Azure che consente di toomanage i StorSimple di Azure in locale e i dispositivi virtuali. |
| Gestione snapshot StorSimple |Snap-in di Microsoft Management Console (MMC) per la gestione di operazioni di backup e ripristino in Microsoft Azure StorSimple. |
| Esegui backup |Una funzionalità che consente di hello utente tootake un backup interattivo di un volume. È un modo alternativo di eseguire un backup manuale di un volume come tootaking anziché un backup automatico tramite un criterio definito. |
| Thin provisioning |Un metodo per ottimizzare l'efficienza di hello con cui hello viene utilizzato lo spazio di archiviazione disponibile nei sistemi di archiviazione. Nel thin provisioning archiviazione hello viene allocato tra più utenti in base hello spazio minimo richiesto da ogni utente in qualsiasi momento. Vedere anche *fat provisioning*. |
| suddivisione in livelli |Disposizione dei dati in raggruppamenti logici basati sull'utilizzo corrente, l'età e dati tooother della relazione. StorSimple organizza automaticamente i dati in livelli. |
| volume |Aree di archiviazione logiche presentate sotto forma di hello di unità. I volumi StorSimple corrispondono toohello volumi montati dall'host di hello, ad esempio quelli individuati tramite l'utilizzo di hello di iSCSI e un dispositivo StorSimple. |
| contenitore del volume |Raggruppamento di volumi e le impostazioni di hello applicabili toothem. Tutti i volumi nel dispositivo StorSimple sono raggruppati in contenitori di volumi. Le impostazioni di contenitore di volumi includono gli account di archiviazione, le impostazioni di crittografia per i dati inviati toocloud con chiavi di crittografia associata e la larghezza di banda usata per le operazioni che riguardano il cloud hello. |
| gruppo di volumi |In Gestione Snapshot StorSimple, un gruppo di volumi è una raccolta di elaborazione di volumi configurati toofacilitate backup. |
| Servizio Copia Shadow del volume (VSS) |Un servizio del sistema operativo Windows Server che facilita la coerenza delle applicazioni mediante la comunicazione con creazione di hello toocoordinate applicazioni che riconoscono VSS di snapshot incrementali. VSS assicura che le applicazioni di hello siano temporaneamente inattive quando vengono eseguiti gli snapshot. |
| Windows PowerShell per StorSimple  |Un'interfaccia della riga di comando basata su Windows PowerShell utilizzato toooperate e gestire il dispositivo StorSimple. Pur mantenendo alcune delle funzionalità di base hello di Windows PowerShell, questa interfaccia ha altri cmdlet dedicati che sono pensati per la gestione di un dispositivo StorSimple. |

## <a name="next-steps"></a>Passaggi successivi
Informazioni sulla [sicurezza di StorSimple](storsimple-8000-security.md).

