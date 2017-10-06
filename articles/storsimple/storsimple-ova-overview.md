---
title: Panoramica di Azure StorSimple Virtual Array aaaMicrosoft | Documenti Microsoft
description: "Viene descritto hello Array virtuale StorSimple, una soluzione di archiviazione integrata che gestisce le attività tra un array virtuale locale e l'archiviazione cloud di Microsoft Azure."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Introduzione toohello Array virtuale StorSimple
## <a name="overview"></a>Panoramica
Microsoft Azure StorSimple Virtual Array Hello è una soluzione di archiviazione integrata che gestisce le attività tra un array virtuale locale in esecuzione in un hypervisor e l'archiviazione cloud di Microsoft Azure. array virtuale Hello è un file efficiente, conveniente e facilmente gestibile server o una soluzione server iSCSI che elimina molti problemi hello e spese associate enterprise archiviazione e protezione dei dati. array virtuale Hello è particolarmente adatta per scenari con office/filiali remote.

In questo argomento viene fornita una panoramica della matrice virtuale hello: di seguito sono riportate altre risorse:

* Per le procedure consigliate, vedere [Procedure consigliate per l'array virtuale StorSimple](storsimple-ova-best-practices.md).
* Per una panoramica dei dispositivi della serie StorSimple 8000 hello, andare troppo[StorSimple serie 8000: una soluzione di cloud ibrido](storsimple-overview.md). 
* Per informazioni sui dispositivi serie 5000 o 7000 StorSimple hello, andare troppo[StorSimple la Guida in linea](http://onlinehelp.storsimple.com/).

array virtuale Hello supporta iSCSI hello o un protocollo Server Message Block (SMB). Viene eseguito in base all'infrastruttura esistente di hypervisor e fornisce funzionalità di ripristino di emergenza, backup nel cloud, ripristino rapido, ripristino a livello di elemento e cloud toohello suddivisione in livelli.

Hello nella tabella seguente sono riepilogate hello importanti caratteristiche di hello Array virtuale StorSimple.

| Funzionalità | Array virtuale StorSimple |
| --- | --- |
| Requisiti di installazione |Viene usata un'infrastruttura di virtualizzazione (Hyper-V o VMware) |
| Disponibilità |Nodo singolo |
| Capacità totale (incluso il cloud) |Backup too64 TB di capacità utilizzabile per array virtuale |
| Capacità locale |390 GB too6.4 TB di capacità utilizzabile per array virtuale (necessità tooprovision 500 GB too8 TB di spazio su disco) |
| Protocolli nativi |iSCSI o SMB |
| Obiettivo del tempo di ripristino (RTO) |iSCSI: meno di 2 minuti indipendentemente dalle dimensioni |
| Obiettivo del punto di ripristino (RPO) |Backup giornalieri e backup su richiesta |
| Suddivisione in livelli di archiviazione |Usa riscaldare toodetermine mapping quali dati devono essere collegati a livelli in o out |
| Supporto |Infrastruttura di virtualizzazione supportato dal fornitore hello |
| Prestazioni |Variabile in base all'infrastruttura sottostante |
| Mobilità dei dati |Ripristinare toohello stesso dispositivo o a livello di elemento recupero (file server) |
| Livelli di archiviazione |Archiviazione hypervisor locale e cloud |
| Dimensione della condivisione |A più livelli: backup too20 TB; aggiunto in locale: backup too2 TB |
| Dimensioni del volume |A più livelli: 500 GB too5 TB; aggiunto in locale: 50 GB too500 GB |
| Dimensioni del volume |A più livelli: backup too5 TB; aggiunto in locale: backup too500 GB |
| Snapshot |Coerenza in caso di arresto anomalo |
| Ripristino a livello di elemento |Sì. Gli utenti possono ripristinare dalle condivisioni |

## <a name="why-use-storsimple"></a>Vantaggi dell'uso di StorSimple
StorSimple si connette utenti e i server di archiviazione tooAzure in minuti, senza modifiche dell'applicazione.

Hello nella tabella seguente descrive alcuni dei vantaggi principali di hello tale hello soluzione fornisce la matrice virtuale StorSimple.

| Funzionalità | Vantaggi |
| --- | --- |
| Integrazione trasparente |array virtuale Hello supporta hello iSCSI o protocollo SMB hello. lo spostamento dei dati di Hello tra livelli locale hello e cloud hello è semplice e trasparente toohello utente. |
| Riduzione dei costi di archiviazione |Con StorSimple, eseguire il provisioning sufficiente spazio di archiviazione locale toomeet le richieste correnti per i dati di hello usato più di frequente. Mentre le necessità di archiviazione crescono, StorSimple suddivide i dati meno utilizzati in livelli in un'archiviazione cloud a costi contenuti. Hello deduplicati e dati compressi prima di inviare cloud toohello toofurther ridurre i requisiti di archiviazione e di spesa. |
| Gestione dell'archiviazione semplificata |StorSimple consente una gestione centralizzata nel cloud hello utilizzando Gestione dispositivi StorSimple toomanage più dispositivi. |
| Miglioramento del ripristino di emergenza e della conformità |StorSimple facilita il ripristino di emergenza più veloce ripristinando immediatamente hello metadati e dati hello in base alle esigenze. Le normali operazioni possono quindi continuare con un'interruzione minima. |
| Mobilità dei dati |Cloud toohello a più livelli è possibile accedere da altri siti per scopi di ripristino e migrazione di dati. Si noti che è possibile ripristinare i dati solo toohello virtuale matrice originale. È tuttavia possibile utilizzare disaster recovery funzionalità toorestore hello intera matrice virtuale tooanother array virtuale. |

## <a name="storsimple-workload-summary"></a>Riepilogo dei carichi di lavoro di StorSimple

Di seguito è riportato un riepilogo dei carichi di lavoro StorSimple supportati.

|Scenario     |Carico di lavoro     |Supportato      |Restrizioni               |
|-------------|-------------|---------------|---------------------------|
|Collaborazione ROBO |Condivisione di file     |Sì      |Vedere [limiti massimi per file server](storsimple-ova-limits.md).<br></br>Vedere [requisiti di sistema per le versioni supportate di SMB](storsimple-ova-system-requirements.md).| Tutte le versioni     |

## <a name="workflows"></a>Flussi di lavoro
Hello Array virtuale StorSimple è particolarmente adatto per hello flussi di lavoro seguente:

* [Gestione dell'archiviazione basata su cloud](#cloud-based-storage-management)
* [Backup indipendente dalla posizione](#location-independent-backup)
* [Protezione dati e ripristino di emergenza](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>Gestione dell'archiviazione basata su cloud
È possibile utilizzare il servizio di gestione di dispositivi StorSimple hello in esecuzione in Azure toomanage portale dati archiviati nei dispositivi più hello e in più posizioni. Questo è particolarmente utile in scenari di succursali distribuite. Si noti che è necessario creare istanze separate di matrici virtuali toomanage servizio gestione di dispositivi StorSimple hello e i dispositivi StorSimple fisici. Si noti inoltre che array virtuale hello ora utilizza nuovo portale di Azure hello anziché hello portale di Azure classico.

![Gestione dell'archiviazione basata su cloud](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Backup indipendente dalla posizione
Con array virtuale hello, gli snapshot cloud forniscono una copia indipendente dalla posizione, in un momento di un volume o condivisione. Gli snapshot cloud sono abilitati per impostazione predefinita e non possono essere disabilitati. Tutti i volumi e condivisioni sono eseguire il backup in hello stessa fase tramite un singolo criterio di backup giornaliero ed eseguire il backup ad hoc aggiuntive quando necessario.

### <a name="data-protection-and-disaster-recovery"></a>Protezione dati e ripristino di emergenza
array virtuale Hello supporta hello seguenti scenari di ripristino di emergenza e la protezione dati:

* **Ripristino di un volume o condivisione** : utilizzare hello ripristino come nuovo flusso di lavoro toorecover un volume o condivisione. Utilizzare questo approccio toorecover hello intero volume o condivisione file.
* **Ripristino a livello di elemento** – condivisioni consentono l'accesso semplificato toorecent backup. È possibile ripristinare un singolo file facilmente da una speciale *con estensione backup* cartella disponibile nel cloud hello. Questa funzionalità di ripristino è gestita dall'utente e non è richiesto alcun intervento amministrativo.
* **Ripristino di emergenza** : utilizzare hello toorecover funzionalità di failover di tutti i volumi o condivisioni tooa nuova matrice virtuale. Creare hello nuova matrice virtuale e registrarlo con il servizio di gestione di dispositivi StorSimple hello, quindi eseguire il failover array virtuale originale hello. array virtuale nuovo Hello quindi presuppone che le risorse di hello il provisioning. 

## <a name="storsimple-virtual-array-components"></a>Componenti dell'array virtuale StorSimple
array virtuale Hello include hello seguenti componenti:

* [Array virtuale.](#virtual-array) Un dispositivo di archiviazione cloud ibrido basato su una macchina virtuale sottoposta a provisioning nell'ambiente virtualizzato o in hypervisor.  
* [Servizio di gestione di dispositivi StorSimple](#storsimple-device-manager-service) : estensione di hello portale di Azure che consente di gestire uno o più dispositivi StorSimple da una singola interfaccia web che è possibile accedere da località geografiche diverse. È possibile utilizzare toocreate servizio di gestione di dispositivi StorSimple hello e gestire i servizi, visualizzare e gestire avvisi e i dispositivi e gestire volumi, condivisioni e gli snapshot esistenti.
* [Interfaccia utente web locale](#local-web-user-interface) : un'interfaccia utente basata sul web che è usato tooconfigure hello in modo che possa connettersi la rete locale toohello e quindi registrare il dispositivo hello con il servizio di gestione di dispositivi StorSimple hello. 
* [Interfaccia della riga di comando](#command-line-interface) : un'interfaccia di Windows PowerShell che è possibile utilizzare toostart una sessione di supporto nell'array virtuale hello.
  Hello nelle sezioni seguenti viene descritto ciascuno di questi componenti in modo più dettagliato e illustrano come soluzione hello organizza i dati, alloca spazio di archiviazione e facilita la gestione dell'archiviazione e protezione dei dati.

### <a name="virtual-array"></a>Array virtuale
array virtuale Hello è una soluzione di archiviazione a nodo singolo che fornisce archiviazione primaria, gestisce le comunicazioni con l'archiviazione cloud e consente di sicurezza hello tooensure e la riservatezza di tutti i dati archiviati nel dispositivo hello.

array virtuale Hello è disponibile in un modello che è disponibile per il download. array virtuale Hello ha una capacità massima di 6,4 TB nel dispositivo di hello (con un requisito di archiviazione sottostante di 8 TB) e tra 64 TB di archiviazione cloud. 

array virtuale Hello è hello seguenti caratteristiche:

* È conveniente. Usa l'infrastruttura di virtualizzazione esistente e può essere distribuito in un  hypervisor Hyper-V o VMware esistente.
* Si trova nel Data Center hello e può essere configurato come un server di iSCSI o un file server. 
* È integrato con il cloud hello.
* I backup vengono archiviati nel cloud hello, che possono facilitare il ripristino di emergenza e semplificano il ripristino a livello di elemento (ILR). 
* È possibile applicare array virtuale toohello gli aggiornamenti, esattamente come verrebbero applicati tooa di dispositivo fisico.

> [!NOTE]
> Non è possibile espandere un array virtuale. È pertanto importante tooprovision adeguata archiviazione quando si crea una matrice virtuale hello. 
> 
> 

### <a name="storsimple-device-manager-service"></a>Servizio Gestione dispositivi StorSimple
Microsoft Azure StorSimple offre un'interfaccia utente basata sul web, servizio di gestione di dispositivi StorSimple, che consente di si toocentrally hello gestire spazi di archiviazione StorSimple. È possibile utilizzare hello tooperform servizio StorSimple Manager di dispositivi di hello seguenti attività:

* Gestire più StorSimple Virtual Array da un singolo servizio. 
* Configurare e gestire le impostazioni di sicurezza per gli array virtuali StorSimple. (Crittografia nel cloud hello è dipendente da Microsoft Azure API).
* Configurare le credenziali dell'account di archiviazione e le proprietà.
* Configurare e gestire volumi o condivisioni.
* Eseguire il backup e il ripristino dei dati in volumi o condivisioni.
* Monitorare le prestazioni.
* Rivedere le impostazioni di sistema e identificare possibili problemi.

Utilizzare hello dispositivo StorSimple Manager servizio tooperform amministrazione quotidiana della matrice virtuale.

Per ulteriori informazioni, visitare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Interfaccia utente Web locale
array virtuale Hello include un'interfaccia utente basata sul web che viene utilizzata per la configurazione monouso e registrazione del dispositivo hello con hello del servizio di gestione di dispositivi StorSimple. È possibile usarlo tooshut verso il basso e riavviare array virtuale hello, eseguire i test diagnostici, aggiornare il software, modifica password di amministratore del dispositivo hello, consente di visualizzare i registri di sistema e contattare il supporto Microsoft toofile una richiesta di servizio. 

Per informazioni sull'utilizzo hello dell'interfaccia utente basata sul web, andare troppo[utilizzare hello tooadminister di interfaccia utente basata sul web l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Interfaccia della riga di comando
interfaccia di Windows PowerShell incluso Hello consente tooinitiate una sessione di supporto con il supporto Microsoft in modo che essi consentono di individuare e risolvere i problemi che potrebbero verificarsi nell'array virtuale.

## <a name="storage-management-technologies"></a>Tecnologie di gestione dell'archiviazione
Inoltre array virtuale toohello e altri componenti, hello StorSimple soluzione utilizza hello software tecnologie tooprovide accesso rapido tooimportant dati seguenti, ridurre il consumo di archiviazione e protezione i dati archiviati nella matrice virtuale:

* [Suddivisione automatica in livelli dell'archiviazione](#automatic-storage-tiering) 
* [Condivisioni e volumi aggiunti in locale](#locally-pinned-shares-and-volumes)
* [La deduplicazione e compressione per i dati a più livelli o sottoposti a backup toohello cloud](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Backup pianificati e su richiesta](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>Suddivisione automatica in livelli dell'archiviazione
array virtuale Hello Usa una nuova suddivisione in livelli dati di toomanage archiviati meccanismo su cloud di matrice e hello virtuale hello. Sono disponibili solo due livelli: archiviazione di cloud array virtuale locale hello e Azure. Hello Array virtuale StorSimple organizza automaticamente i dati in livelli hello in base a una mappa di calore, che tiene traccia dei dati tooother utilizzo, l'età e relazioni correnti. I dati che sono più attivi (migliori) vengono archiviati in locale, mentre meno dati attivi e inattivi vengono automaticamente migrati toohello cloud. (Tutti i backup vengono archiviati nel cloud hello). StorSimple ordina e riorganizza i dati e le assegnazioni delle risorse di archiviazione in base ai cambiamenti dei modelli di utilizzo. Alcune informazioni, ad esempio, possono diventare meno attive nel corso del tempo. Appena sarà progressivamente meno attivo, è a più livelli out toohello cloud. Se gli stessi dati diventano nuovamente attivi, è a più livelli in toohello array di archiviazione.

Viene garantito uno spazio a livello locale per i dati di una particolare condivisione a livelli o un volume specifico (circa il 10% di spazio disponibile totale hello per tale condivisione o volume). Mentre in questo modo si riduce hello disponibili risorse di archiviazione hello virtual array per la condivisione o volume, assicura che il collegamento per una condivisione o volume a livelli non influirà sulle esigenze di suddivisione in livelli hello delle altre condivisioni o volumi. Pertanto un carico di lavoro occupato in una condivisione o volume non è possibile forzare tutti i cloud di toohello altri carichi di lavoro. 

![Suddivisione automatica in livelli dell'archiviazione](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> È possibile specificare un volume aggiunto in locale, nel qual caso i dati hello rimangono nell'array virtuale hello e non sono mai a livelli toohello cloud. Per ulteriori informazioni, visitare troppo[aggiunto in locale i volumi e condivisioni](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>Condivisioni e volumi aggiunti in locale
È possibile creare condivisioni e volumi appropriati come aggiunti in locale. Questa funzionalità garantisce che i dati necessari per le applicazioni critiche rimangono nella matrice virtuale hello e non sono mai a livelli toohello cloud. Condivisioni aggiunti in locale e i volumi sono hello seguenti caratteristiche: 

* Non sono le latenze toocloud del soggetto o problemi di connettività.
* Traggono ugualmente vantaggio dalle funzionalità di backup cloud e ripristino di emergenza di StorSimple.

È possibile ripristinare una condivisione o un volume aggiunti in locale come fossero a livelli o una condivisione o un volume a livelli come aggiunti in locale. 

Per ulteriori informazioni sui volumi aggiunti in locale, andare troppo[utilizzare volumi toomanage servizio di gestione di dispositivi StorSimple hello](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>La deduplicazione e compressione per i dati a più livelli o sottoposti a backup toohello cloud
StorSimple Usa tecniche di deduplicazione e i dati compressione toofurther ridurre i requisiti di archiviazione nel cloud hello. La deduplicazione riduce hello quantità totale di dati archiviati eliminando la ridondanza nel set di dati archiviato hello. In base alle informazioni, StorSimple ignora dati hello invariata e acquisizioni hello solo le modifiche. Inoltre, StorSimple riduce hello di dati archiviati identificando e rimuovendo informazioni duplicate. 

> [!NOTE]
> Dati archiviati nell'array virtuale hello non sono deduplicati o compresso. Tutti la deduplicazione e compressione si verifica poco prima dell'invio dei dati hello toohello cloud.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Backup pianificati e su richiesta
Funzionalità di protezione dati di StorSimple consentono toocreate i backup su richiesta. Inoltre, una pianificazione di backup predefinita garantisce il backup dei dati ogni giorno. I backup vengono eseguiti sotto forma di hello di snapshot incrementali, che vengono archiviati nel cloud hello. Gli snapshot, che consente di registrare solo le modifiche di hello dopo l'ultimo backup hello, possono essere creati e ripristinati rapidamente. Questi snapshot possono essere estremamente importanti in scenari di ripristino di emergenza perché sostituire i sistemi di archiviazione secondaria (ad esempio il backup su nastro) e consentono di toorestore dati tooyour Data Center o tooalternate siti se necessario.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come troppo[preparare portale array virtuale hello](storsimple-virtual-array-deploy1-portal-prep.md).

