---
title: "aaaWhat è StorSimple Snapshot Manager? | Microsoft Docs"
description: "Descrive hello gestione Snapshot StorSimple, l'architettura e le funzionalità."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Un tooStorSimple introduzione gestione Snapshot

## <a name="overview"></a>Panoramica
Gestione Snapshot StorSimple è uno snap-in Microsoft Management Console (MMC) che semplifica la protezione dei dati e la gestione dei backup in un ambiente di Microsoft Azure StorSimple. Con gestione Snapshot StorSimple, è possibile gestire dati di Microsoft Azure StorSimple in data center di hello e nel cloud hello come una soluzione di archiviazione integrata singolo, pertanto semplificando i processi di backup e riducendo i costi.

Questa panoramica introduce hello gestione Snapshot StorSimple, ne descrive le funzionalità e viene illustrato il ruolo in Microsoft Azure StorSimple. 

Per una panoramica del sistema Microsoft Azure StorSimple intera hello, tra cui il dispositivo di StorSimple hello, servizio StorSimple Manager, gestione Snapshot StorSimple e adattatore StorSimple per SharePoint, vedere [StorSimple serie 8000: cloud ibrido soluzione di archiviazione](storsimple-overview.md). 

> [!NOTE]
> * Non è possibile utilizzare toomanage gestione Snapshot StorSimple Microsoft Azure StorSimple Virtual Array (noto anche come StorSimple locale dispositivi virtuali).
> * Se si intende il dispositivo StorSimple tooinstall StorSimple Update 2, che toodownload hello versione più recente di StorSimple Snapshot Manager e installarlo **prima di installare l'aggiornamento 2 di StorSimple**. la versione più recente Hello di StorSimple Snapshot Manager è compatibile con le versioni precedenti e funziona con tutte le versioni rilasciate di Microsoft Azure StorSimple. Se si utilizza una versione precedente di hello di StorSimple Snapshot Manager, sarà necessario tooupdate it (non è necessario versione precedente di hello toouninstall prima di installare una nuova versione di hello).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>Scopo e architettura di Gestione snapshot StorSimple
Gestione Snapshot StorSimple fornisce una console di gestione centrale che è possibile utilizzare toocreate coerente, le copie di backup temporizzati in locale e cloud dati. Ad esempio, è possibile utilizzare la console di hello per:

* Configurare, eseguire il backup ed eliminare volumi.
* Configurare il volume tooensure gruppi di dati di backup è coerente con l'applicazione.
* Gestire criteri di backup in modo che il backup dei dati venga eseguito in una pianificazione predeterminata.
* Creare locale e gli snapshot, che possono essere archiviati nel cloud hello e utilizzati per il ripristino di emergenza nel cloud.

Hello gestione Snapshot StorSimple recupera l'elenco di hello delle applicazioni registrate con il provider VSS hello in host hello. Quindi, backup coerenti con l'applicazione di toocreate, controlla volumi hello utilizzato da un'applicazione e vengono suggerite alcune tooconfigure gruppi di volumi. Gestione Snapshot StorSimple Usa questi volume gruppi toogenerate copie di backup coincidono con l'applicazione. (Coerenza con l'applicazione esiste quando tutti i relativi file e database sono sincronizzati e rappresentano lo stato true hello di un'applicazione hello in un momento specifico nel tempo). 

I backup di gestione Snapshot StorSimple consistere hello snapshot incrementali, che acquisiscono solo le modifiche di hello dopo l'ultimo backup hello. Di conseguenza, i backup richiedono meno spazio di archiviazione e possono essere creati e ripristinati rapidamente. Gestione Snapshot StorSimple Usa hello servizio Copia Shadow (VSS) di Windows Volume tooensure acquisizione di dati coerenti con l'applicazione. (Per ulteriori informazioni, visitare toohello integrazione con la sezione servizio Copia Shadow del Volume di Windows). Con Gestione snapshot StorSimple, è possibile creare pianificazioni di backup o eseguire backup immediati in base alle esigenze. Se è necessario toorestore dati da un backup, di StorSimple Snapshot Manager consente selezionare da un catalogo locale o snapshot cloud. StorSimple di Azure consente di ripristinare solo hello dati che sono necessario perché è necessaria, che evita ritardi nella disponibilità dei dati durante le operazioni di ripristino.)

![Architettura di Gestione snapshot StorSimple](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**Architettura di Gestione snapshot StorSimple** 

## <a name="support-for-multiple-volume-types"></a>Supporto per più tipi di volume
È possibile usare Gestione Snapshot StorSimple tooconfigure hello ed eseguire il backup dei seguenti tipi di volumi hello: 

* **Volumi di base** : un volume di base è una singola partizione su un disco di base. 
* **Volumi semplici** : un volume semplice è un volume dinamico contenente lo spazio su disco da un singolo disco dinamico. Un volume semplice è costituito da una singola area su un disco o hello di più aree collegate insieme sullo stesso disco. (È possibile creare volumi semplici solo sui dischi dinamici). I volumi semplici non sono a tolleranza di errore.
* **Volumi dinamici** : un volume dinamico è un volume creato su un disco dinamico. I dischi dinamici utilizzano le informazioni di tootrack un database su volumi contenuti nei dischi dinamici di un computer. 
* **Volumi dinamici con mirroring** – volumi dinamici con mirroring si basano sull'architettura RAID 1 hello. Con RAID 1 i dati identici vengono scritti su due o più dischi, creando un set con mirroring. Una richiesta di lettura può quindi essere gestita da qualsiasi disco contenente hello richiesta dei dati.
* **Volumi condivisi cluster** : con i volumi condivisi cluster (CSV), più nodi in un cluster di failover possono contemporaneamente leggere o scrivere toohello stesso disco. Failover dal nodo di un nodo tooanother può verificarsi rapidamente, senza dover modificare la proprietà dell'unità o di montaggio, scollegamento e rimozione di un volume. 

> [!IMPORTANT]
> Non combinare volumi condivisi cluster e non condivisi nello hello stesso snapshot. La combinazione di volumi condivisi cluster e volumi non condivisi cluster in uno stesso snapshot non è supportata. 
> 
> 

È possibile utilizzare Gestione Snapshot StorSimple toorestore interi gruppi di volumi o clonare singoli volumi e ripristinare singoli file.

* [Volumi e gruppi di volumi](#volumes-and-volume-groups) 
* [Tipi e criteri di backup](#backup-types-and-backup-policies) 

Per ulteriori informazioni sulle funzionalità di gestione Snapshot StorSimple e toouse, vedere [interfaccia utente di gestione Snapshot StorSimple](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Volumi e gruppi di volumi
Con Gestione snapshot StorSimple è possibile creare volumi, quindi configurarli in gruppi di volumi. 

Gestione Snapshot StorSimple Usa volume gruppi toocreate copie di backup coincidono con l'applicazione. Coerenza con l'applicazione esiste quando tutti i relativi file e database sono sincronizzati e rappresentano lo stato true hello di un'applicazione in un momento specifico nel tempo. Gruppi di volumi (che sono anche noti come *gruppi coerenza*) costituiscono la base hello di un backup o di processo di ripristino.

Gruppi di volumi non sono hello come contenitori di volumi. Un contenitore di volumi contiene uno o più volumi che condividono un account di archiviazione cloud e altri attributi, come la crittografia e il consumo della larghezza di banda. Un contenitore di volumi singolo può contenere un massimo di volumi StorSimple too256 con thin provisioning. Per ulteriori informazioni sui contenitori dei volumi, andare troppo[gestire i contenitori di volumi](storsimple-manage-volume-containers.md). Gruppi di volumi sono raccolte di volumi di configurare le operazioni di backup toofacilitate. Se si selezionano due volumi che appartengono a contenitori del volume toodifferent, inserirli in un singolo gruppo di volumi e quindi creare un criterio di backup per il gruppo di volumi, ogni volume verrà sottoposti a backup hello appropriato contenitore del volume, utilizzando l'archiviazione appropriato hello account.

> [!NOTE]
> Tutti i volumi in un gruppo di volumi devono provenire da un singolo provider di servizi cloud.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Integrazione con il servizio Copia Shadow del volume di Windows
Gestione Snapshot StorSimple Usa dati coerenti con l'applicazione di servizio Copia Shadow (VSS) di Windows Volume toocapture hello. VSS facilita la coerenza delle applicazioni mediante la comunicazione con creazione di hello toocoordinate applicazioni che riconoscono VSS di snapshot incrementali. VSS assicura che hello le applicazioni siano temporaneamente inattive o inattivo, quando vengono eseguiti gli snapshot. 

implementazione di gestione Snapshot StorSimple Hello di VSS funziona con SQL Server e volumi NTFS generici. il processo di Hello è come segue: 

1. Richiedente, che è in genere una gestione dei dati e la soluzione di protezione (ad esempio Gestione Snapshot StorSimple) o un'applicazione di backup, richiama VSS e richiede informazioni toogather dal software writer hello nell'applicazione di destinazione hello.
2. Contatti VSS hello tooretrieve componente writer una descrizione dei dati di hello. writer di Hello restituisce descrizione hello di hello toobe di dati sottoposti a backup. 
3. Segnala a VSS writer tooprepare hello un'applicazione hello per il backup. Hello writer prepara i dati di hello per il backup completando le transazioni aperte, l'aggiornamento di log delle transazioni e così via e quindi comunica a VSS.
4. VSS indica al writer hello dati dell'applicazione di tootemporarily stop hello archiviano e assicurarsi che non vengano scritti dati toohello volume durante la creazione di copie shadow hello. Questo passaggio garantisce la coerenza dei dati e richiede non più di 60 secondi.
5. VSS indica la copia shadow hello provider toocreate hello. I provider, che possono essere software - o basato su hardware, gestire volumi hello che sono attualmente in esecuzione e creare copie shadow di questi su richiesta. provider di Hello Crea copia shadow hello e notifica VSS dopo averlo completato.
6. Contatti hello writer toonotify hello applicazione VSS che può riprendere i/o e inoltre che i/o è stata sospesa correttamente durante replicata tooconfirm copiare creazione. 
7. Se la copia hello ha esito positivo, VSS restituisce hello richiedente toohello di percorso della copia. 
8. Se durante la creazione di copie shadow hello scrittura di dati, quindi hello backup risulterà incoerente. VSS Elimina copia shadow hello e notifica il richiedente hello. Hello richiedente può ripetere il processo di backup hello automaticamente o notificare tooretry amministratore hello in un secondo momento.

Vedere hello seguente illustrazione.

![Processo VSS](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Processo del Servizio Copia Shadow del volume di Windows** 

## <a name="backup-types-and-backup-policies"></a>Tipi e criteri di backup
Con gestione Snapshot StorSimple, è possibile eseguire il backup dei dati e archiviarli localmente e nel cloud hello. È possibile usare Gestione Snapshot StorSimple tooback dei dati immediatamente oppure è possibile utilizzare toocreate un criterio di backup una pianificazione per eseguire automaticamente i backup. Criteri di backup consentono anche toospecify quanti snapshot verranno conservati. 

### <a name="backup-types"></a>Tipi di backup
È possibile usare Gestione Snapshot StorSimple toocreate hello seguenti tipi di backup:

* **Gli snapshot locali** : gli snapshot locali sono copie punto nel tempo dei dati di volume archiviati nel dispositivo StorSimple hello. In genere, questo tipo di backup può essere creato e ripristinato rapidamente. È possibile utilizzare uno snapshot locale come copia di backup locale.
* **Gli snapshot cloud** : gli snapshot Cloud sono copie punto nel tempo dei dati di volume archiviati nel cloud hello. Uno snapshot cloud equivale tooa snapshot replicato su un sistema di archiviazione fuori sede diversi. Gli snapshot cloud sono particolarmente utili negli scenari di ripristino di emergenza.

### <a name="on-demand-and-scheduled-backups"></a>Backup su richiesta e pianificati
Con gestione Snapshot StorSimple, è possibile avviare una sola volta toobe backup creato immediatamente, oppure è possibile utilizzare tooschedule un criterio di backup ricorrenti di operazioni di backup.

Un criterio di backup è un set di regole automatizzate che è possibile utilizzare backup regolari tooschedule. Un criterio di backup consente di toodefine hello frequenza e i parametri per la creazione di snapshot di un gruppo di volumi specifico. È possibile utilizzare le date di inizio e di scadenza toospecify criteri, orari, frequenze e requisiti di conservazione, per locali e snapshot cloud. Un criterio viene applicato immediatamente dopo averlo definito. 

È possibile utilizzare Gestione Snapshot StorSimple tooconfigure o riconfigurare i criteri di backup quando necessario. 

Configurare le seguenti informazioni per ogni criterio di backup creati hello:

* **Nome** : nome univoco di hello di hello selezionata dei criteri di backup.
* **Tipo** : hello tipo di criterio di backup; snapshot locale o di uno snapshot nel cloud.
* **Gruppo di volumi** : hello volume gruppo toowhich hello selezionato criteri di backup viene assegnato.
* **Conservazione** : numero di copie di backup tooretain hello. Se si seleziona hello **tutti** casella, tutte le copie di backup vengono mantenute fino a quando non viene raggiunto hello il numero massimo di copie di backup per volume, in cui hello punto criteri avrà esito negativo e generare un messaggio di errore. In alternativa, è possibile specificare un numero di backup tooretain (compreso tra 1 e 64).
* **Data** – data hello creazione dei criteri di backup hello.

Per informazioni sulla configurazione dei criteri di backup, andare troppo[toocreate usare Gestione Snapshot StorSimple e gestire criteri di backup](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Monitoraggio e gestione del processo di backup
È possibile utilizzare Gestione Snapshot StorSimple toomonitor hello e gestire i processi di backup imminenti, pianificati e completati. Inoltre, gestione Snapshot StorSimple offre un catalogo di backup too64 completato. È possibile utilizzare toofind catalogo hello e ripristinare volumi o i singoli file. 

Per informazioni sul monitoraggio dei processi di backup, andare troppo[tooview usare Gestione Snapshot StorSimple e gestire i processi di backup](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni, vedere [utilizzando Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Scaricare [Gestione snapshot StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

