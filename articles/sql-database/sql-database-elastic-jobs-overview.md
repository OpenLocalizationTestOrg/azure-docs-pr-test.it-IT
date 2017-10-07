---
title: "database cloud di scalabilità orizzontale aaaManaging | Documenti Microsoft"
description: Vengono illustrate servizio processo di database elastico hello
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Gestione dei database cloud con scalabilità orizzontale
database partizionati di scalabilità orizzontale toomanage, hello **i processi di Database elastico** funzionalità Abilita (anteprima) è tooreliably eseguire uno script Transact-SQL (T-SQL) in un gruppo di database, tra cui:

* una raccolta personalizzata di database (illustrata di seguito)
* tutti i database in un [pool elastico](sql-database-elastic-pool.md)
* un set di partizioni, creato con la [libreria client dei database elastici](sql-database-elastic-database-client-library.md). 

## <a name="documentation"></a>Documentazione
* [Installare componenti dei processi di Database elastico hello](sql-database-elastic-jobs-service-installation.md). 
* [Introduzione a Processi di database elastico](sql-database-elastic-jobs-getting-started.md).
* [Creare e gestire processi tramite PowerShell](sql-database-elastic-jobs-powershell.md).
* [Creare e gestire database SQL di Azure con scalabilità orizzontale](sql-database-elastic-jobs-getting-started.md)

**I processi di Database elastici** è attualmente un servizio Cloud Azure ospitati cliente che rende possibile l'esecuzione di ad hoc e attività amministrative pianificate, dette hello **processi**. I processi, si può facilmente e gestire in modo affidabile i gruppi di grandi dimensioni di database di SQL Azure mediante l'esecuzione di operazioni amministrative tooperform gli script di Transact-SQL. 

![Servizio processo di database elastico][1]

## <a name="why-use-jobs"></a>Vantaggi offerti dai processi
**Manage**

Eseguire facilmente le modifiche dello schema, la gestione delle credenziali, gli aggiornamenti dei dati di riferimento, la raccolta dei dati sulle prestazioni o la raccolta dei dati di telemetria del tenant (cliente).

**Report**

Aggregare i dati di una raccolta di database SQL di Azure in una singola tabella di destinazione.

**Ridurre il sovraccarico**

In genere, è necessario connettersi tooeach database in modo indipendente in istruzioni Transact-SQL toorun di ordine o eseguire altre attività amministrative. Un processo gestisce attività hello registrazione nel database tooeach nel gruppo di destinazione hello. Anche definire, gestire e mantenere toobe script Transact-SQL eseguita in un gruppo di database SQL di Azure.

**Accounting**

I processi eseguiti hello script e log hello lo stato di esecuzione per ogni database. È anche disponibile la ripetizione automatica in caso di errori.

**Flessibilità**

Definire gruppi personalizzati di database SQL di Azure e pianificazioni per l'esecuzione di un processo.

> [!NOTE]
> Nel portale di Azure hello, solo un set ridotto di funzioni limitate tooSQL Azure elastico pool è disponibile. Utilizzare hello PowerShell APIs tooaccess hello completo delle funzionalità corrente.
> 
> 

## <a name="applications"></a>Applicazioni
* Eseguire attività amministrative, quali la distribuzione di un nuovo schema.
* Aggiornare i dati di riferimento, ad esempio informazioni di prodotto comuni tra tutti i database. Pianificare aggiornamenti automatici ogni giorno della settimana, dopo l'orario di lavoro.
* Ricompilare le prestazioni delle query tooimprove indici. Hello la ricompilazione può essere tooexecute configurata tra una raccolta di database su base periodica, ad esempio durante le fasce orarie.
* Raccogliere i risultati di query da un set di database in una tabella centrale su base costante. Le query di prestazioni possono essere eseguite continuamente e configurate tootrigger toobe di attività aggiuntive eseguite.
* Eseguire query di elaborazione dei dati con esecuzione prolungata in un set di database di grandi dimensioni, ad esempio hello raccolta di dati di telemetria di cliente. I risultati vengono raccolti in una tabella di destinazione singola per ulteriori analisi.

## <a name="elastic-database-jobs-end-to-end"></a>Processi di database elastici: end-to-end
1. Installare hello **i processi di Database elastico** componenti. Per altre informazioni, vedere [Installazione dei processi di database elastici](sql-database-elastic-jobs-service-installation.md). Se si verifica un errore di installazione di hello, vedere [come toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Utilizzare PowerShell APIs tooaccess hello ulteriori funzionalità, ad esempio la creazione di raccolte di database personalizzati, aggiungendo le pianificazioni e/o la raccolta di set di risultati. Portale di hello utilizzare per l'installazione semplice e creazione/monitoraggio dei processi limitato tooexecution contro un **pool elastico**. 
3. Creare le credenziali crittografate per l'esecuzione del processo e [aggiungere database tooeach utente (o ruolo) di hello hello gruppo](sql-database-security-overview.md).
4. Creare un script T-SQL che possono essere eseguite in ogni database nel gruppo hello idempotente. 
5. Seguire questi processi toocreate passaggi utilizzando hello portale di Azure: [creazione e gestione dei processi di Database elastico](sql-database-elastic-jobs-create-and-manage.md). 
6. In alternativa, usare script di PowerShell: [Creare e gestire processi di database elastici del database SQL tramite PowerShell (anteprima)](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>Script idempotenti
deve essere script Hello [idempotente](https://en.wikipedia.org/wiki/Idempotence). In altre parole, "idempotente" significa che se script hello ha esito positivo e viene eseguito di nuovo, hello stesso risultato si verifica. Uno script potrebbe non riuscire a causa di problemi di rete tootransient. In tal caso, il processo di hello tenterà automaticamente di ripetere script hello in esecuzione un numero di volte prima di desisting preimpostato. Uno script idempotente ha hello stesso risultato anche se è stato correttamente eseguito due volte. 

Una semplice strategia è tootest esistenza hello di un oggetto prima di averlo creato.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

Analogamente, uno script deve essere in grado di tooexecute correttamente eseguendo i test in modo logico per e tutte le condizioni di fronteggiare rileva.

## <a name="failures-and-logs"></a>Errori e log
Se uno script non riesce dopo diversi tentativi, il processo di hello registra l'errore hello e continua. Termine di un processo, ovvero un'esecuzione in tutti i database nel gruppo di hello, è possibile controllare l'elenco dei tentativi non riusciti. i file di registro Hello dettagli script difettoso toodebug. 

## <a name="group-types-and-creation"></a>Tipi di gruppo e creazione
Esistono due tipi di gruppi: 

1. Set di partizioni
2. Gruppi personalizzati

Gruppi di set di partizioni vengono creati utilizzando hello [strumenti di Database elastico](sql-database-elastic-scale-introduction.md). Quando si crea un gruppo di set di partizioni, i database vengono aggiunti o rimossi dal gruppo hello automaticamente. Ad esempio, una nuova partizione verrà automaticamente nel gruppo di hello quando si aggiunge mappa partizioni toohello. Un processo può quindi essere eseguito su gruppo di hello.

Gruppi personalizzati, in hello invece, sono definiti rigidamente. È necessario aggiungere o rimuovere i database in modo esplicito dai gruppi personalizzati. Se viene eliminato un database nel gruppo di hello, processo hello tenterà script hello toorun database hello risultante in un eventuale errore. Gruppi creati mediante hello portale di Azure attualmente sono gruppi personalizzati. 

## <a name="components-and-pricing"></a>Componenti e prezzi
Hello seguenti componenti interagiscono toocreate un servizio Cloud di Azure che consente l'esecuzione ad hoc di processi di amministrazione. componenti Hello installati e configurati automaticamente durante l'installazione, nella sottoscrizione. È possibile identificare i servizi di hello come essi hanno hello stesso generato automaticamente nome. nome Hello è univoco, è costituito da prefisso "edj hello" seguito da caratteri generate in modo casuale 21.

* **Servizio Cloud di Azure**: i processi di database elastico (anteprima) viene recapitato come un Cloud di Azure ospitati cliente tooperform esecuzione del servizio di hello attività richieste. Dal portale di hello, servizio hello è distribuito e ospitato nella sottoscrizione di Microsoft Azure. servizio predefinito distribuito Hello viene eseguito con almeno hello due ruoli di lavoro per la disponibilità elevata. dimensioni predefinite Hello di ogni ruolo di lavoro (ElasticDatabaseJobWorker) viene eseguito in un'istanza di A0. Per informazioni sui prezzi, vedere [Servizi cloud Prezzi](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Database SQL di Azure**: servizio di hello utilizza un Database di SQL Azure noto come hello **database del controllo** toostore tutti i metadati del processo hello. livello di servizio predefinito Hello è un S0. Per informazioni sui prezzi, vedere [Database SQL Prezzi](https://azure.microsoft.com/pricing/details/sql-database/).
* **Azure Service Bus**: è un Bus di servizio di Azure per il coordinamento di hello lavoro all'interno di hello servizio Cloud di Azure. Vedere [Bus di servizio Prezzi](https://azure.microsoft.com/pricing/details/service-bus/).
* **Archiviazione di Azure**: viene utilizzato un account di archiviazione Azure toostore diagnostica output di registrazione nell'evento hello che un problema richiede un'ulteriore debug (vedere [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](../cloud-services/cloud-services-dotnet-diagnostics.md)). Per informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>Funzionano dei processi di database elastico
1. Un database SQL di Azure viene designato come **database di controllo** per l'archiviazione di tutti i dati di stato e i metadati.
2. database del controllo Hello avviene mediante hello **servizio processi** tooexecute processi toolaunch e tenere traccia.
3. Due diversi ruoli comunicano con i database di controllo hello: 
   * Controller: Determina quali processi richiedono hello tooperform attività richiesta di processo e i processi non riusciti di tentativi tramite la creazione di nuove attività di processo.
   * Esecuzione dell'attività di processo: Esegue attività di processo hello.

### <a name="job-task-types"></a>Tipi di attività di processo
Sono disponibili più tipi di attività di processo che eseguono l'esecuzione di processi:

* ShardMapRefresh: Query hello toodetermine mappa partizioni tutti i database hello utilizzati come partizioni
* ScriptSplit: Script di hello divisioni tra le istruzioni 'Vai' in batch
* ExpandJob: Crea processi figlio per ogni database da un processo destinato a un gruppo di database
* ScriptExecution: Esegue uno script su un particolare database utilizzando le credenziali definite
* Dacpac: Si applica un file DACPAC tooa particolare database utilizzando le credenziali specifiche

## <a name="end-to-end-job-execution-work-flow"></a>Flusso di lavoro completo di esecuzione del processo
1. Utilizza hello portale o API di PowerShell hello, un processo viene inserito un hello **database del controllo**. processo Hello ha richiesto l'esecuzione di uno script Transact-SQL rispetto a un gruppo di database utilizzando le credenziali specifiche.
2. controller Hello identifica il nuovo processo di hello. Attività di processo vengono create ed eseguito script hello toosplit e database del gruppo di toorefresh hello. Infine, un nuovo processo creato ed eseguito tooexpand hello processo e crea di nuovo figlio processi in cui ogni processo figlio è hello tooexecute specificato uno script Transact-SQL per un singolo database nel gruppo di hello.
3. controller Hello identifica hello creato i processi figlio. Per ogni processo, il controller hello crea e genera uno script di hello tooexecute attività processo in un database. 
4. Dopo aver completato tutte le attività di processo, controller hello Aggiorna lo stato di completamento tooa processi hello. 
   In qualsiasi momento durante l'esecuzione del processo, hello API PowerShell può essere utilizzato tooview hello stato corrente dell'esecuzione del processo. Sempre restituito da hello APIs di PowerShell sono rappresentati in UTC. Se si desidera, una richiesta di annullamento può essere toostop avviato da un processo. 

## <a name="next-steps"></a>Passaggi successivi
[Installare i componenti di hello](sql-database-elastic-jobs-service-installation.md), quindi [creare e aggiungere un log nel database tooeach nel gruppo di hello di database](sql-database-manage-logins.md). toofurther della creazione del processo e gestione delle informazioni, vedere [la creazione e gestione dei processi di database elastico](sql-database-elastic-jobs-create-and-manage.md). Vedere anche [Introduzione a Processi di database elastico](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


