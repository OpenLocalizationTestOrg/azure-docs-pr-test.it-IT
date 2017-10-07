---
title: Database - aaaSQL ottimizzazione automatica | Documenti Microsoft
description: Database SQL analizza query SQL e automaticaly adatta toouser del carico di lavoro.
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Ottimizzazione automatica

Database SQL di Azure è un servizio dati completamente gestito che consente di monitorare le query hello che vengono eseguite sul database hello e automaticamente possono migliorare le prestazioni del carico di lavoro hello. Database SQL di Azure dispone di un meccanismo di intelligence predefinite che è possibile ottimizzare e migliorare le prestazioni delle query da adattare dinamicamente il carico di lavoro di hello database tooyour automaticamente. Ottimizzazione automatica nel Database SQL di Azure potrebbe essere una delle funzionalità più importanti hello che è possibile abilitare sulle prestazioni del Database SQL di Azure toooptimize delle query.

Vedere l'articolo per la procedura hello troppo[abilitare la regolazione automatica](sql-database-automatic-tuning-enable.md) utilizzando hello portale di Azure.

## <a name="why-automatic-tuning"></a>Perché optare per l'ottimizzazione automatica?

Una delle attività principali di hello in Amministrazione classica di database esegue il monitoraggio del carico di lavoro di hello, identificazione critici SQL esegue una query, gli indici devono essere aggiunti tooimprove prestazioni di indici utilizzato di rado. Database SQL di Azure fornisce una visione dettagliata query hello e gli indici che è necessario toomonitor. Il monitoraggio costante dei database è tuttavia un'attività complessa e tediosa, in particolare quando sono coinvolti molti database. Gestisce un numero elevato di database potrebbe essere impossibile toodo in modo efficiente anche tutti gli strumenti disponibili e i rapporti forniti da Database SQL di Azure e portale di Azure. Invece di monitoraggio e ottimizzazione del database manualmente, è possibile delegare alcuni hello di monitoraggio e ottimizzazione azioni tooAzure Database SQL utilizzando le funzionalità di ottimizzazione automatica. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Come funziona l'ottimizzazione automatica

Database SQL di Azure dispone di un processo di analisi e monitoraggio delle prestazioni continua costantemente conoscenza hello caratteristica del carico di lavoro e identifica potenziali problemi e i miglioramenti.

![Processo di ottimizzazione automatica](./media/sql-database-automatic-tuning/tuning-process.png)

Questa consente al processo toodynamically Database SQL di Azure adattare il carico di lavoro tooyour individuando quali indici e i piani potrebbero migliorare le prestazioni dei carichi di lavoro e gli indici selezionati influire sui carichi di lavoro. In base ai risultati raccolti, l'ottimizzazione automatica applica le azioni di ottimizzazione che consentono di migliorare le prestazioni del carico di lavoro. Inoltre, i Database SQL di Azure monitora costantemente prestazioni dopo qualsiasi modifica apportata dal tooensure di ottimizzazione automatica che è possibile migliorare le prestazioni del carico di lavoro. Qualsiasi azione che non introduce miglioramenti delle prestazioni viene annullata automaticamente. Il processo di verifica è una funzionalità chiave che assicura che qualsiasi modifica apportata dall'ottimizzazione automatica non diminuisca le prestazioni di hello del carico di lavoro.

Nel database SQL di Azure sono disponibili due contesti di ottimizzazione automatica:

 -  **Gestione automatica degli indici** che consente di identificare gli indici da aggiungere al database e quelli che è consigliabile rimuovere.
 -  **Correzione automatica dei piani** (presto disponibile, già presente in SQL Server 2017) che consente di identificare i piani problematici e correggere i problemi di prestazioni dei piani SQL.

## <a name="automatic-index-management"></a>Gestione automatica degli indici

Nel database SQL di Azure la gestione degli indici è semplice perché il database SQL di Azure raccoglie informazioni sul carico di lavoro e assicura che i dati vengano indicizzati sempre in modo ottimale. La progettazione appropriata degli indici è fondamentale per ottenere prestazioni ottimali del carico di lavoro e la gestione automatica degli indici risulta utile per ottimizzare gli indici. La gestione automatica degli indici possibile correggere i problemi di prestazioni nel database in modo non corretto indicizzati, o gestire e migliorare gli indici lo schema del database esistente hello. 

### <a name="why-do-you-need-index-management"></a>Utilità della gestione degli indici

Indici velocizzare alcune delle query che recuperano i dati dalle tabelle di hello; Tuttavia, può rallentare le query hello aggiornamento dei dati. È necessario toocarefully analizzare quando toocreate un indice e le colonne che è necessario tooinclude in hello indice. Alcuni indici potrebbero non essere più necessari dopo un certo periodo di tempo. Pertanto, è necessario tooperiodically identificare ed eliminare gli indici hello non portare i vantaggi. Se si ignora hello indici inutilizzati, avrebbe ridotto la prestazione delle query hello aggiornamento dei dati senza alcun vantaggio per le query hello che leggono i dati. Gli indici inutilizzati influire sulle prestazioni complessive del sistema hello perché altri aggiornamenti necessaria la registrazione non necessaria.

Ricerca set ottimale di hello di indici che consentono di migliorare le prestazioni delle query hello leggere i dati delle tabelle che hanno un impatto minimo per gli aggiornamenti, potrebbe essere necessario analysis continua e complessi.

Database SQL di Azure Usa intelligenti e regole avanzate di analizzare le query, identificare gli indici che sarebbero ottimali per i carichi di lavoro corrente e gli indici di hello potrebbero essere rimossa. Database SQL di Azure consente di disporre di un set minimo necessario di indici che ottimizzare le query hello che leggono i dati, con un impatto ridotto a icona hello sul hello altre query.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>Come tooidentify indici toobe tale esigenza modificata nel database?

Il database SQL di Azure semplifica il processo di gestione degli indici. Anziché operazione laboriosa hello di analisi del carico di lavoro manuale e il monitoraggio di indice, Database SQL di Azure analizza il carico di lavoro, consente di identificare query hello che potrebbe essere eseguita più velocemente con un nuovo indice e identifica gli indici inutilizzati o duplicati. Per altre informazioni sull'identificazione degli indici che devono essere modificati, vedere [Find index recommendations in Azure portal](sql-database-advisor-portal.md) (Trovare raccomandazioni per gli indici nel portale di Azure).

### <a name="automatic-index-management-considerations"></a>Considerazioni sulla gestione automatica degli indici

Se si ritiene che le regole predefinite di hello miglioramento delle prestazioni di hello del database, si potrebbe gestire database SQL di Azure automaticamente gli indici.

Azioni richieste toocreate indici necessarie nei database di SQL Azure potrebbero utilizzare risorse e temporaneamente le prestazioni del carico di lavoro. impatto hello toominimize della creazione dell'indice sulle prestazioni del carico di lavoro, Database SQL di Azure Trova finestra ora appropriato hello per qualsiasi operazione di gestione dell'indice. Ottimizzazione azione viene posticipato se hello database risorse tooexecute il carico di lavoro e avviato durante hello database dispone di sufficienti risorse inutilizzate che possono essere utilizzate per attività di manutenzione hello. Una funzionalità importante nella gestione automatica dell'indice è una verifica di azioni di hello. Quando il Database SQL di Azure crea o Elimina indice, un processo di monitoraggio consente di analizzare le prestazioni di tooverify il carico di lavoro che l'azione di hello miglioramento delle prestazioni di hello. Se non introducono miglioramenti significativi: azione hello viene immediatamente ripristinato. In questo modo, il database SQL di Azure garantisce che le azioni automatiche non influiscano negativamente sulle prestazioni del carico di lavoro. Gli indici creati tramite l'ottimizzazione automatica sono trasparenti per un'operazione di manutenzione hello schema sottostante hello. Le modifiche dello schema, ad esempio l'eliminazione o ridenominazione delle colonne non sono bloccate dalla presenza di hello degli indici creati automaticamente. Gli indici creati automaticamente dal database SQL di Azure vengono eliminati immediatamente in seguito all'eliminazione di tabelle o colonne correlate.

## <a name="automatic-plan-choice-correction"></a>Correzione automatica del piano

La correzione automatica del piano è una nuova funzionalità di ottimizzazione automatica aggiunta in SQL Server 2017 CTP2.0 che identifica i piani SQL con comportamento errato. Questa opzione di ottimizzazione automatica sarà presto disponibile nel database SQL di Azure. Per altre informazioni, vedere [Ottimizzazione automatica in SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Passaggi successivi

- ottimizzazione in Database SQL di Azure e consentire automatico automatica tooenable funzionalità di ottimizzazione completamente gestire il carico di lavoro, vedere [abilitare la regolazione automatica](sql-database-automatic-tuning-enable.md).
- toouse di ottimizzazione manuale, è possibile esaminare [le indicazioni nel portale di Azure di ottimizzazione](sql-database-advisor-portal.md) e applicare manualmente hello varianti che migliorano le prestazioni delle query.
