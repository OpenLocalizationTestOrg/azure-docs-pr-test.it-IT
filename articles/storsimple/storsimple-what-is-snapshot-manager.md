---
title: "Che cos’è Gestione snapshot StorSimple? | Microsoft Docs"
description: "Vengono descritti la Gestione snapshot StorSimple, la sua architettura e le sue funzionalità."
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
ms.openlocfilehash: 38c197c7bc57110b29b1d8cb789d5b7310823da2
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="an-introduction-to-storsimple-snapshot-manager"></a>Introduzione a StorSimple Snapshot Manager

## <a name="overview"></a>Panoramica
Gestione Snapshot StorSimple è uno snap-in Microsoft Management Console (MMC) che semplifica la protezione dei dati e la gestione dei backup in un ambiente di Microsoft Azure StorSimple. Con Gestione snapshot StorSimple è possibile gestire i dati di Microsoft Azure StorSimple nel datacenter e nel cloud come una singola soluzione di archiviazione integrata, in modo da semplificare i processi di backup e di ridurre i costi.

Questa panoramica introduce Gestione snapshot StorSimple, ne descrive le funzionalità e ne illustra il ruolo in Microsoft Azure StorSimple. 

Per una panoramica dell'intero sistema di Microsoft Azure StorSimple, tra cui il dispositivo StorSimple, il servizio StorSimple Manager, Gestione snapshot StorSimple e l'adattatore StorSimple per SharePoint, vedere [Serie 8000 StorSimple: una soluzione di archiviazione cloud ibrida](storsimple-overview.md). 

> [!NOTE]
> * Non è possibile usare Gestione Snapshot StorSimple per gestire gli array virtuali di Microsoft Azure StorSimple (noti anche come dispositivi virtuali StorSimple locali).
> * Se si prevede di installare l'aggiornamento 2 di StorSimple sul dispositivo StorSimple, assicurarsi di scaricare la versione più recente di StorSimple Snapshot Manager e installarla **prima di installare l'aggiornamento 2 di StorSimple**. La versione più recente di StorSimple Snapshot Manager è compatibile con le versioni precedenti e funziona con tutte le versioni rilasciate di Microsoft Azure StorSimple. Se si utilizza la versione precedente di StorSimple Snapshot Manager, è necessario aggiornarla (non è necessario disinstallare la versione precedente prima di installare la nuova versione).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>Scopo e architettura di Gestione snapshot StorSimple
Gestione snapshot StorSimple fornisce una console di gestione centrale che consente di creare copie di backup coerenti e temporizzate di dati locali e cloud. Ad esempio, è possibile utilizzare la console per:

* Configurare, eseguire il backup ed eliminare volumi.
* Configurare gruppi di volumi per assicurarsi che i dati di cui è stato eseguito il backup siano coerenti con l'applicazione.
* Gestire criteri di backup in modo che il backup dei dati venga eseguito in una pianificazione predeterminata.
* Creare snapshot locali e nel cloud, che possono essere archiviati nel cloud e usati per il ripristino di emergenza.

Snapshot Manager di StorSimple recupera l'elenco delle applicazioni registrate con il provider VSS nell'host. Per creare backup coerenti con l'applicazione, controlla quindi i volumi usati da un'applicazione e suggerisce i gruppi di volumi da configurare. Gestione snapshot StorSimple utilizza questi gruppi di volumi per generare copie di backup coerenti con l'applicazione. (La coerenza con l'applicazione esiste quando tutti i relativi file e database sono sincronizzati e rappresentano lo stato reale dell'applicazione in un momento specifico). 

I backup di Gestione snapshot StorSimple assumono la forma di snapshot incrementali, che acquisiscono solo le modifiche apportate dall'ultimo backup. Di conseguenza, i backup richiedono meno spazio di archiviazione e possono essere creati e ripristinati rapidamente. Gestione snapshot StorSimple utilizza il servizio Copia Shadow del volume di Windows per garantire che gli snapshot acquisiscano dati coerenti con l'applicazione. (Per ulteriori informazioni, andare alla sezione Integrazione con il servizio Copia Shadow del volume di Windows.) Con Gestione snapshot StorSimple, è possibile creare pianificazioni di backup o eseguire backup immediati in base alle esigenze. Se è necessario ripristinare i dati da un backup, Gestione snapshot StorSimple consente di effettuare una selezione da un catalogo di snapshot locali o cloud. Azure StorSimple consente di ripristinare solo i dati necessari quando sono necessari, evitando ritardi nella disponibilità dei dati durante le operazioni di ripristino.)

![Architettura di Gestione snapshot StorSimple](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**Architettura di Gestione snapshot StorSimple** 

## <a name="support-for-multiple-volume-types"></a>Supporto per più tipi di volume
È possibile utilizzare Gestione snapshot StorSimple, per configurare ed eseguire il backup dei tipi di volumi seguenti: 

* **Volumi di base** : un volume di base è una singola partizione su un disco di base. 
* **Volumi semplici** : un volume semplice è un volume dinamico contenente lo spazio su disco da un singolo disco dinamico. Un volume semplice è costituito da una singola area su un disco o da più aree collegate insieme sullo stesso disco. (È possibile creare volumi semplici solo sui dischi dinamici). I volumi semplici non sono a tolleranza di errore.
* **Volumi dinamici** : un volume dinamico è un volume creato su un disco dinamico. I dischi dinamici utilizzano un database per tenere traccia delle informazioni sui volumi contenuti nei dischi dinamici di un computer. 
* **Volumi dinamici con mirroring** : i volumi dinamici con mirroring si basano sull'architettura RAID 1. Con RAID 1 i dati identici vengono scritti su due o più dischi, creando un set con mirroring. Una richiesta di lettura può quindi essere gestita da qualsiasi disco contenente i dati richiesti.
* **Volumi condivisi cluster** : con i volumi condivisi cluster (CSV) più nodi in un cluster di failover possono leggere o scrivere contemporaneamente sullo stesso disco. Il failover da un nodo a un altro nodo può verificarsi rapidamente, senza necessità di modificare la proprietà dell'unità o di montare, smontare e rimuovere un volume. 

> [!IMPORTANT]
> Non combinare volumi condivisi cluster e volumi non condivisi cluster nello stesso snapshot. La combinazione di volumi condivisi cluster e volumi non condivisi cluster in uno stesso snapshot non è supportata. 
> 
> 

È possibile utilizzare Gestione snapshot StorSimple per ripristinare interi gruppi di volumi o clonare volumi singoli e recuperare file singoli.

* [Volumi e gruppi di volumi](#volumes-and-volume-groups) 
* [Tipi e criteri di backup](#backup-types-and-backup-policies) 

Per altre informazioni sulle funzionalità di Gestione snapshot StorSimple e su come usarle, vedere [Interfaccia utente di Gestione snapshot StorSimple](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Volumi e gruppi di volumi
Con Gestione snapshot StorSimple è possibile creare volumi, quindi configurarli in gruppi di volumi. 

Gestione snapshot StorSimple utilizza i gruppi di volumi per creare copie di backup coerenti con l'applicazione. La coerenza con l'applicazione esiste quando tutti i relativi file e database sono sincronizzati e rappresentano lo stato reale di un’applicazione in un momento specifico. I gruppi di volumi (anche noti come *Gruppi di coerenza*) sono alla base di un processo di backup o di ripristino.

I gruppi di volumi non corrispondono ai contenitori di volumi. Un contenitore di volumi contiene uno o più volumi che condividono un account di archiviazione cloud e altri attributi, come la crittografia e il consumo della larghezza di banda. Un contenitore di volumi singolo può contenere fino a 256 volumi StorSimple con thin provisioning. Per altre informazioni sui contenitori di volumi, andare a [Gestione dei contenitori di volumi](storsimple-manage-volume-containers.md). I gruppi di volumi sono raccolte di volumi configurate per facilitare le operazioni di backup. Se si selezionano due volumi che appartengono a contenitori di volumi diversi, inserirli in un singolo gruppo di volumi, quindi creare un criterio di backup per tale gruppo di volumi. Il backup di ciascun volume verrà eseguito nel contenitore di volumi appropriato, utilizzando l'account di archiviazione appropriato.

> [!NOTE]
> Tutti i volumi in un gruppo di volumi devono provenire da un singolo provider di servizi cloud.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Integrazione con il servizio Copia Shadow del volume di Windows
Gestione snapshot StorSimple utilizza il servizio Copia Shadow del volume di Windows (VSS) per acquisire dati coerenti con l'applicazione. VSS facilita la coerenza con l'applicazione comunicando con le applicazioni compatibili con VSS per coordinare la creazione di snapshot incrementali. VSS garantisce che quando vengono eseguiti gli snapshot le applicazioni siano temporaneamente inattive. 

L'implementazione di Gestione snapshot StorSimple di VSS funziona con SQL Server e i volumi NTFS generici. Il processo è il seguente: 

1. Un richiedente, in genere una soluzione di gestione e protezione dei dati (come Gestione snapshot StorSimple) o un'applicazione di backup, richiama VSS e richiede di raccogliere le informazioni dal software writer nell'applicazione di destinazione.
2. VSS contatta il componente writer per recuperare una descrizione dei dati. Il writer restituisce la descrizione dei dati da sottoporre a backup. 
3. VSS segnala al writer di preparare l'applicazione per il backup. Il writer prepara i dati per il backup completando le transazioni aperte, aggiornando i log delle transazioni e così via, quindi invia una notifica a VSS.
4. VSS indica al writer di arrestare temporaneamente gli archivi di dati dell'applicazione e di assicurarsi che non vengano scritti dati sul volume durante la creazione della copia shadow. Questo passaggio garantisce la coerenza dei dati e richiede non più di 60 secondi.
5. VSS indica al provider di creare la copia shadow. I provider, che possono essere basati su software o hardware, gestiscono i volumi attualmente in esecuzione e creano copie shadow di questi ultimi su richiesta. Il provider crea la copia shadow e invia una notifica a VSS quando viene completata.
6. VSS contatta il writer per inviare una notifica all'applicazione indicando che è possibile riprendere le operazioni di I/O e per verificare che queste ultime siano state sospese correttamente durante la creazione della copia shadow. 
7. Se la copia è stata creata correttamente, VSS restituisce il percorso della copia al richiedente. 
8. Se durante la creazione della copia shadow sono stati scritti dati, il backup sarà incoerente. VSS elimina la copia shadow e invia una notifica al richiedente. Il richiedente può ripetere il processo di backup automaticamente o inviare una notifica all'amministratore indicando di riprovare in un secondo momento.

Vedere la figura seguente.

![Processo VSS](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Processo del Servizio Copia Shadow del volume di Windows** 

## <a name="backup-types-and-backup-policies"></a>Tipi e criteri di backup
Con Gestione snapshot StorSimple è possibile eseguire il backup dei dati e archiviarlo in locale e nel cloud. È possibile utilizzare Gestione snapshot StorSimple per eseguire immediatamente il backup dei dati oppure è possibile utilizzare un criterio di backup per creare una pianificazione per eseguire i backup automaticamente. I criteri di backup consentono inoltre di specificare quanti snapshot verranno conservati. 

### <a name="backup-types"></a>Tipi di backup
È possibile utilizzare Gestione snapshot StorSimple per creare i tipi di backup seguenti:

* **Snapshot locali** : gli snapshot locali sono copie temporizzate dei dati del volume archiviati sul dispositivo StorSimple. In genere, questo tipo di backup può essere creato e ripristinato rapidamente. È possibile utilizzare uno snapshot locale come copia di backup locale.
* **Snapshot cloud** : gli snapshot Cloud sono copie temporizzate di dati del volume archiviati nel cloud. Uno snapshot cloud equivale a uno snapshot replicato su un diverso sistema di archiviazione fuori sede. Gli snapshot cloud sono particolarmente utili negli scenari di ripristino di emergenza.

### <a name="on-demand-and-scheduled-backups"></a>Backup su richiesta e pianificati
Con Gestione snapshot StorSimple è possibile avviare un backup unico da creare immediatamente oppure è possibile utilizzare un criterio di backup per pianificare operazioni di backup ricorrenti.

Un criterio di backup è un insieme di regole automatizzate che è possibile utilizzare per pianificare backup regolari. Un criterio di backup consente di definire la frequenza e i parametri per la creazione di snapshot di un gruppo di volumi specifico. È possibile utilizzare criteri per specificare le date di avvio e di scadenza, gli orari, le frequenze e i requisiti di conservazione, sia per gli snapshot locali sia per quelli cloud. Un criterio viene applicato immediatamente dopo averlo definito. 

È possibile utilizzare Gestione snapshot StorSimple per configurare o riconfigurare i criteri di backup quando necessario. 

Per ciascun criterio di backup creato vengono configurate le informazioni seguenti:

* **Nome** : il nome univoco del criterio di backup selezionato.
* **Tipo** : il tipo di criterio di backup (snapshot locale o cloud).
* **Gruppo di volumi** : il gruppo di volumi a cui è assegnato il criterio di backup selezionato.
* **Conservazione**: il numero di copie di backup da conservare. Se si seleziona la casella **Tutti**, tutte le copie di backup vengono conservate fino al raggiungimento del numero massimo di copie per volume. A questo punto il criterio avrà esito negativo e verrà generato un messaggio di errore. In alternativa, è possibile specificare un numero di backup da conservare (compreso tra 1 e 64).
* **Data** : la data di creazione del criterio di backup.

Per informazioni sulla configurazione dei criteri di backup, andare a [Utilizzo di Gestione snapshot StorSimple per creare e gestire i criteri di backup](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Monitoraggio e gestione del processo di backup
È possibile utilizzare Gestione snapshot StorSimple per monitorare e gestire i processi di backup imminenti, pianificati e completati. Gestione snapshot StorSimple fornisce inoltre un catalogo di fino a 64 backup completati. È possibile utilizzare il catalogo per individuare e ripristinare volumi o singoli file. 

Per informazioni sul monitoraggio dei processi di backup, andare a [Utilizzo di Gestione snapshot StorSimple per visualizzare e gestire i processi di backup](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sull' [utilizzo di StorSimple Snapshot Manager per amministrare la soluzione di StorSimple](storsimple-snapshot-manager-admin.md).
* Scaricare [Gestione snapshot StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

