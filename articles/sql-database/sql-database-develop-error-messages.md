---
title: codici di errore aaaSQL - errore di connessione del database | Documenti Microsoft
description: 'Informazioni sui codici di errore SQL per le applicazioni client del database SQL, ad esempio errori di connessione comuni del database, problemi di copia del database ed errori generali. '
keywords: codice di errore sql, accesso sql, errore di connessione del database, codici di errore sql
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>Codici di errore SQL per le applicazioni client del database SQL: errore di connessione e altri problemi del database
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


Questo articolo elenca i codici di errore di SQL per le applicazioni client del database SQL, inclusi errori di connessione del database, errori temporanei (noti anche come guasti temporanei), errori di governance delle risorse, errori di copia del database, errori relativi al pool elastico e altri errori. La maggior parte delle categorie sono tooAzure particolare Database SQL e non si applicano tooMicrosoft SQL Server.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>Errori di connessione del database, guasti e altri errori temporanei
Hello nella tabella seguente vengono illustrati i codici di errore SQL hello per errori di perdita della connessione e altri errori temporanei che possono verificarsi durante l'applicazione tenta tooaccess Database SQL. Per ottenere esercitazioni introduttive su come tooconnect tooAzure Database SQL, vedere [la connessione di Database SQL tooAzure](sql-database-libraries.md).

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>Errori di connessione del database ed errori temporanei più comuni
Hello dell'infrastruttura di Azure è hello possibilità toodynamically riconfigurare i server quando si verificano i carichi di lavoro pesante in hello servizio Database SQL.  Questo comportamento dinamico potrebbe causare il client toolose programma relativo tooSQL connessione Database. Questo tipo di errore è chiamato *errore temporaneo*.

È consigliabile che il programma client dispone di logica di ripetizione tentativi in modo che è stato possibile ristabilire la connessione dopo aver dato hello errori temporanei ora toocorrect stesso.  È consigliabile attendere 5 secondi prima di riprovare. Nuovo tentativo dopo un ritardo inferiore a 5 secondi rischi in termini di servizio cloud di hello impegnativo. Per ogni tentativo successivo ritardo hello aumentino in modo esponenziale, backup tooa massimo di 60 secondi.

Gli errori temporanei manifesto in genere come uno dei seguenti messaggi di errore dai programmi client hello:

* Il database &lt;nome_db&gt; nel server &lt;istanza_Azure&gt; non è attualmente disponibile. Ripetere connessione hello in un secondo momento. Se hello problema persiste, contattare il supporto tecnico e fornire loro ID di traccia di sessione hello &lt;session_id&gt;
* Il database &lt;nome_db&gt; nel server &lt;istanza_Azure&gt; non è attualmente disponibile. Ripetere connessione hello in un secondo momento. Se hello problema persiste, contattare il supporto tecnico e fornire loro ID di traccia di sessione hello &lt;session_id&gt;. (Microsoft SQL Server, Errore: 40613)
* Una connessione esistente chiusa forzatamente dall'host remoto hello.
* System.Data.Entity.Core.EntityCommandExecutionException: Si è verificato un errore durante l'esecuzione della definizione di comando hello. Vedere l'eccezione interna hello per informazioni dettagliate. ---> System.Data.SqlClient.SqlException: si è verificato un errore a livello di trasporto quando si ricevono risultati dal server hello. (provider: provider di sessione, errore: 19 - impossibile usare la connessione fisica)
* Un database secondario di tentativo tooa connessione non riuscita perché database hello è in corso di hello di reconfguration ed è occupato, l'applicazione di nuove pagine durante centro hello di un transation attivo sul database primario hello. 

Per esempi di codice relativi alla logica di ripetizione dei tentativi, vedere:

* [Raccolte di connessioni per database SQL e SQL Server](sql-database-libraries.md) 
* [Errori di connessione toofix azioni e gli errori temporanei nel Database SQL](sql-database-connectivity-issues.md)

Una discussione di hello *il periodo di blocco* per i client che usano ADO.NET è disponibile in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

### <a name="transient-fault-error-codes"></a>Codici di errore degli errori temporanei
Hello gli errori seguenti sono temporanei e devono essere riprovati nella logica dell'applicazione 

| Codice di errore | Gravità | Descrizione |
| ---:| ---:|:--- |
| 4060 |16 |Impossibile aprire il database "%. & #x2a; ls" richiesto dall'account di accesso hello. Hello accesso non riuscito. |
| 40197 |17 |servizio di Hello ha rilevato un errore durante l'elaborazione della richiesta. Riprova più tardi. Codice di errore %d.<br/><br/>Si riceverà il messaggio di errore quando il servizio hello verso il basso di scadenza toosoftware o gli aggiornamenti hardware, errori hardware o altri problemi di failover. codice di errore Hello (%d) incorporato nel messaggio di errore 40197 fornisce informazioni aggiuntive sul tipo di hello di errore o failover che si è verificato. Alcuni esempi di errore hello codici sono incorporati nel messaggio di errore 40197 sono 40020, 40143, 40166 e 40540.<br/><br/>Server di Database SQL tooyour riconnessione automaticamente si connetterà tooa copia integra del database. L'applicazione deve rilevare l'errore 40197, log hello incorporato codice di errore (%d) all'interno di messaggio per la risoluzione dei problemi e ritentare la connessione di Database tooSQL fino a quando non sono disponibili risorse hello e la connessione viene ristabilita. |
| 40501 |20 |servizio Hello è attualmente occupato. Ripetere la richiesta hello dopo 10 secondi. ID evento imprevisto: %ls. Codice: %d.<br/><br/>*Nota:* per altre informazioni, vedere:<br/>• [Limiti delle risorse del database SQL di Azure](sql-database-resource-limits.md). |
| 40613 |17 |Il database '%.&#x2a;ls' nel server '%.&#x2a;ls' non è attualmente disponibile. Ripetere connessione hello in un secondo momento. Se hello problema persiste, contattare il supporto tecnico e fornire loro hello sessione ID traccia '%. & #x2a; ls'. |
| 49918 |16 |Impossibile elaborare una richiesta. Richiesta non è sufficiente tooprocess risorse.<br/><br/>servizio Hello è attualmente occupato. Riprovare più tardi richiesta hello. |
| 49919 |16 |Il processo non può creare o aggiornare la richiesta. Troppe operazioni di creazione o aggiornamento in corso per "%ld" della sottoscrizione.<br/><br/>servizio Hello è occupato nell'elaborazione di più di creare o aggiornare le richieste di sottoscrizione o il server. Le richieste al momento sono bloccate per l'ottimizzazione delle risorse. Eseguire la query [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) per le operazioni in sospeso. Attendere che le richieste di creazione o aggiornamento in sospeso siano complete o cancellare una delle richieste in sospeso e ripetere la richiesta in un secondo momento. |
| 49920 |16 |Impossibile elaborare una richiesta. Troppe operazioni di creazione o aggiornamento in corso per "%ld" della sottoscrizione.<br/><br/>servizio Hello è occupato nell'elaborazione di più richieste per questa sottoscrizione. Le richieste al momento sono bloccate per l'ottimizzazione delle risorse. Eseguire la query [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) per lo stato delle operazioni. Attendere che le richieste in sospeso siano complete o cancellare una delle richieste in sospeso e ripetere la richiesta in un secondo momento. |
| 4221 |16 |Account di accesso secondario tooread attesa toolong 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING' non riuscita. replica di Hello non è disponibile per l'account di accesso perché mancano le versioni delle righe per le transazioni in transito quando la replica hello è stata riciclata. Hello problema può essere risolto tramite il rollback o eseguire il commit di transazioni attive di hello nella replica primaria hello. Le occorrenze di questa condizione possono essere ridotto, evitando di transazioni di scrittura lungo in hello primario. |

## <a name="database-copy-errors"></a>Errori di copia del database
Hello gli errori seguenti può essere rilevato durante la copia di un database nel Database di SQL Azure. Per altre informazioni, vedere [Copiare un database SQL di Azure](sql-database-copy.md).

| Codice di errore | Gravità | Descrizione |
| ---:| ---:|:--- |
| 40635 |16 |Il client con indirizzo IP '%.&#x2a;ls' è temporaneamente disabilitato. |
| 40637 |16 |La creazione della copia del database è attualmente disabilitata. |
| 40561 |16 |Copia del database non riuscita. Uno dei database di origine o destinazione hello non esiste. |
| 40562 |16 |Copia del database non riuscita. database di origine Hello è stato eliminato. |
| 40563 |16 |Copia del database non riuscita. database di destinazione Hello è stato eliminato. |
| 40564 |16 |Copia di database non riuscita a causa di errore interno tooan. Rimuovere il database di destinazione e riprovare. |
| 40565 |16 |Copia del database non riuscita. Copia del database simultanee non più di 1 da hello stessa origine è consentito. Rimuovere il database di destinazione e riprovare in un secondo momento. |
| 40566 |16 |Copia di database non riuscita a causa di errore interno tooan. Rimuovere il database di destinazione e riprovare. |
| 40567 |16 |Copia di database non riuscita a causa di errore interno tooan. Rimuovere il database di destinazione e riprovare. |
| 40568 |16 |Copia del database non riuscita. Il database di origine non è più disponibile. Rimuovere il database di destinazione e riprovare. |
| 40569 |16 |Copia del database non riuscita. Il database di destinazione non è più disponibile. Rimuovere il database di destinazione e riprovare. |
| 40570 |16 |Copia di database non riuscita a causa di errore interno tooan. Rimuovere il database di destinazione e riprovare in un secondo momento. |
| 40571 |16 |Copia di database non riuscita a causa di errore interno tooan. Rimuovere il database di destinazione e riprovare in un secondo momento. |

## <a name="resource-governance-errors"></a>Errori di governance delle risorse
Hello seguenti errori è causato da un uso eccessivo delle risorse durante l'utilizzo di Database SQL di Azure. ad esempio:

* La transazione è rimasta aperta troppo a lungo.
* La transazione contiene troppi blocchi.
* L'applicazione utilizza una quantità eccessiva di memoria.
* L'applicazione utilizza una quantità eccessiva di spazio `TempDb` .

Argomenti correlati:

* Informazioni più dettagliate sono disponibili qui: [Limiti delle risorse del database SQL di Azure](sql-database-resource-limits.md)

| Codice di errore | Gravità | Descrizione |
| ---:| ---:|:--- |
| 10928 |20 |ID risorsa: %d. limite %s Hello per database hello è %d ed è stato raggiunto. Per altre informazioni, vedere [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637).<br/><br/>Hello ID risorsa indica risorsa hello che ha raggiunto il limite di hello. Per i thread di lavoro hello ID risorsa = 1. Per le sessioni, hello ID risorsa = 2.<br/><br/>*Nota:* per ulteriori informazioni su questo errore e come tooresolve, vedere:<br/>• [Limiti delle risorse del database SQL di Azure](sql-database-resource-limits.md). |
| 10929 |20 |ID risorsa: %d. garanzia di Hello %s minimo è %d, limite massimo è %d e utilizzo corrente di hello per database hello è %d. Tuttavia, server hello è attualmente troppo occupato toosupport richieste maggiore %d per questo database. Per altre informazioni, vedere [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637). Altrimenti, riprovare più tardi.<br/><br/>Hello ID risorsa indica risorsa hello che ha raggiunto il limite di hello. Per i thread di lavoro hello ID risorsa = 1. Per le sessioni, hello ID risorsa = 2.<br/><br/>*Nota:* per ulteriori informazioni su questo errore e come tooresolve, vedere:<br/>• [Limiti delle risorse del database SQL di Azure](sql-database-resource-limits.md). |
| 40544 |20 |database di Hello ha raggiunto la quota delle dimensioni. Partizionare o eliminare dati, eliminare indici o consultare la documentazione di hello per le soluzioni possibili. |
| 40549 |16 |La sessione è stata terminata a causa di una transazione a esecuzione prolungata. Provare ad abbreviare la transazione. |
| 40550 |16 |Hello sessione è stata terminata perché ha acquisito troppi blocchi. Provare a leggere o modificare meno righe in una singola transazione. |
| 40551 |16 |Hello sessione è stata terminata a causa di un numero eccessivo `TEMPDB` utilizzo. Provare a modificare l'utilizzo dello spazio di tabella temporanea di query tooreduce hello.<br/><br/>*Suggerimento:* se si usano oggetti temporanei, liberare spazio nel hello `TEMPDB` database rimuovendo oggetti temporanei Se non sono necessari per la sessione hello. |
| 40552 |16 |Hello sessione è stata terminata a causa di spazio di log di transazioni di dimensioni eccessive. Provare a modificare un numero inferiore di righe in una sola transazione.<br/><br/>*Suggerimento:* se si eseguono inserimenti bulk utilizzando hello `bcp.exe` utilità o hello `System.Data.SqlClient.SqlBulkCopy` classe, provare a utilizzare hello `-b batchsize` o `BatchSize` numero hello toolimit di opzioni di righe copiate toohello server in ogni transazione. Se si rigenera un indice con hello `ALTER INDEX` istruzione, provare a utilizzare hello `REBUILD WITH ONLINE = ON` opzione. |
| 40553 |16 |Hello sessione è stata terminata a causa di utilizzo eccessivo della memoria. Provare a modificare la query tooprocess meno righe.<br/><br/>*Suggerimento:* riducendo il numero di hello di `ORDER BY` e `GROUP BY` operazioni nel codice Transact-SQL consente di ridurre i requisiti di memoria hello della query. |

## <a name="elastic-pool-errors"></a>Errori relativi al pool elastico
Hello gli errori seguenti è correlati toocreating e utilizzo pool Elastics.

| ErrorNumber | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |pool elastico Hello ha raggiunto il limite di archiviazione. utilizzo dell'archiviazione Hello per pool elastico hello non può superare (%d) MB. |Limite di spazio del pool elastico in MB. |Il tentativo di database di tooa toowrite dati quando viene raggiunto il limite di archiviazione hello del pool elastico hello. |Prendere in considerazione le Dtu hello crescente di hello pool elastico se possibile in ordine tooincrease il limite di archiviazione, riduce lo spazio utilizzato da singoli database nel pool elastico hello hello o rimuovere i database dal pool elastico hello. |
| 10929 |EX_USER |garanzia di Hello %s minimo è %d, limite massimo è %d e utilizzo corrente di hello per database hello è %d. Tuttavia, server hello è attualmente troppo occupato toosupport richieste maggiore %d per questo database. Per assistenza, vedere [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) . Altrimenti, riprovare più tardi. |Numero minimo DTU per database. Numero massimo DTU per database |Hello numero totale di processi di lavoro (richieste) simultanei in tutti i database nel limite del pool hello tooexceed tentativo hello pool elastico. |. È consigliabile aumentare il limite di lavoro di hello Dtu del hello pool elastico se possibile in ordine tooincrease o rimuovere i database dal pool elastico hello. |
| 40844 |EX_USER |Il database '%ls' sul Server '%ls' è un database versione '%ls' in un pool elastico e non può avere una relazione di copia continua. |nome database, versione database, nome server |Viene emesso un comando StartDatabaseCopy per un database non premium in un pool elastico. |Presto disponibile |
| 40857 |EX_USER |Pool elastico non trovato per il server: '%ls', nome del pool elastico: '%ls'. |nome del server; nome del pool elastico |Il pool elastico specificato non esiste nel server specificato hello. |Fornire un nome pool elastico valido. |
| 40858 |EX_USER |Il pool elastico '%ls' esiste già nel server: '%ls' |nome del pool elastico, nome del server |Il pool elastico specificato esiste già nel server logico specificato hello. |Fornire un nuovo nome pool elastico. |
| 40859 |EX_USER |Il pool elastico non supporta il livello di servizio '%ls'. |livello di servizio del pool elastico |Il livello di servizio specificato non è supportato per il provisioning del pool elastico. |Specificare l'edizione corretta hello o lasciare il livello di servizio predefinito hello toouse vuoto livello servizio. |
| 40860 |EX_USER |La combinazione di pool elastico '%ls' e di obiettivo di servizio '%ls' non è valida. |nome pool elastico; nome obiettivo del livello di servizio |Il pool elastico e l’obiettivo del servizio possono essere specificati insieme solo se l’obiettivo di servizio viene specificato come 'ElasticPool'. |Specificare la combinazione corretta di pool elastico e obiettivo di servizio. |
| 40861 |EX_USER |edizione del database Hello ' %. *ls' non può essere diverso a livello di servizio del pool elastico hello, che è ' %.* ls'. |edizione del database, livello di servizio del pool elastico |edizione del database Hello è diverso rispetto a livello di servizio hello pool elastico. |Non specificare un'edizione del database che è diversa dal livello di servizio hello pool elastico.  Si noti il che edizione del database che hello toobe specificato non è necessario. |
| 40862 |EX_USER |Nome del pool elastico deve essere specificato se viene specificato l'obiettivo di servizio hello pool elastico. |Nessuno |L’obiettivo di servizio del pool elastico non identifica in modo univoco un pool elastico. |Specificare nome del pool elastico hello se si usa l'obiettivo di servizio hello pool elastico. |
| 40864 |EX_USER |Hello Dtu per il pool elastico hello deve essere pari ad almeno (%d) Dtu per il livello di servizio ' %. * ls'. |DTU per il pool elastico; livello di servizio del pool elastico. |Il tentativo di hello tooset Dtu per il pool elastico di hello inferiore al limite minimo hello. |Ripetere l'operazione di impostazione hello Dtu per hello pool elastico tooat limite minimo di hello minimi. |
| 40865 |EX_USER |Hello Dtu per il pool elastico hello non può superare (%d) Dtu per il livello di servizio ' %. * ls'. |DTU per il pool elastico; livello di servizio del pool elastico. |Il tentativo di hello tooset Dtu per il pool elastico di hello supera il limite massimo di hello. |Ripetere l'impostazione di Dtu hello per hello pool elastico toono maggiore del limite massimo di hello. |
| 40867 |EX_USER |Hello DTU massimo per database deve essere pari almeno (%d) per il livello di servizio ' %. * ls'. |numero massimo di DTU per database; livello di servizio del pool elastico |Il tentativo di hello tooset DTU massimo per database sotto hello il limite supportato. |È consigliabile utilizzare a livello di servizio del pool elastico hello che supporta l'impostazione di hello desiderato. |
| 40868 |EX_USER |Hello DTU massimo per database non può superare (%d) per il livello di servizio ' %. * ls'. |Numero massimo di DTU per database; livello di servizio del pool elastico. |Il tentativo di hello tooset DTU massimo per database oltre hello il limite supportato. |È consigliabile utilizzare a livello di servizio del pool elastico hello che supporta l'impostazione di hello desiderato. |
| 40870 |EX_USER |Hello minimo DTU per database non può superare (%d) per il livello di servizio ' %. * ls'. |numero minimo di DTU per database; livello di servizio del pool elastico. |Il tentativo di tooset hello valore DTU minimo per ogni database oltre hello il limite supportato. |È consigliabile utilizzare a livello di servizio del pool elastico hello che supporta l'impostazione di hello desiderato. |
| 40873 |EX_USER |numero di Hello di database (%d) e min DTU per database (%d) non può superare hello Dtu del pool elastico hello (%d). |Numero di database nel pool elastico; numero minimo di DTU per ogni database; DTU del pool elastico. |Il tentativo di toospecify valore DTU minimo per i database nel pool elastico hello che supera hello Dtu del pool elastico hello. |Hello Dtu del pool elastico hello, aumentare o diminuire hello minimo DTU per database oppure ridurre il numero di hello di database nel pool elastico hello. |
| 40877 |EX_USER |Impossibile eliminare un pool elastico, a meno che non contenga alcun database. |Nessuno |pool elastico Hello contiene uno o più database e pertanto non può essere eliminato. |. Rimuovere i database dal pool elastico di hello in ordine toodelete. |
| 40881 |EX_USER |Hello pool elastico ' %. * ls' ha raggiunto il limite di conteggio database.  limite del conteggio database Hello per pool elastico hello non può superare (%d) per un pool elastico con Dtu (%d). |Nome del pool elastico; limite di conteggio del database del pool elastico; DTU per pool di risorse. |Il tentativo di toocreate o aggiungere pool di database tooelastic quando è stato raggiunto il limite di conteggio database hello del pool elastico hello. |. È consigliabile aumentare il limite del database di hello Dtu del hello pool elastico se possibile in ordine tooincrease o rimuovere i database dal pool elastico hello. |
| 40889 |EX_USER |Dtu di Hello o il limite di archiviazione per pool elastico hello ' %. * ls' non può essere ridotto dal momento che non si forniscono spazio di archiviazione sufficiente per i database. |Nome del pool elastico. |Il tentativo di limite di archiviazione toodecrease hello del pool elastico di hello sotto l'utilizzo di archiviazione. |Provare a ridurre l'utilizzo dell'archiviazione di hello di singoli database nel pool elastico hello o Rimuovi database dal pool hello in ordine tooreduce Dtu o l'archiviazione limite. |
| 40891 |EX_USER |Hello minimo DTU per database (%d) non può superare hello valore DTU massimo per database (%d). |Numero minimo DTU per database; numero massimo DTU per database |Il tentativo di tooset hello valore DTU minimo per ogni database superiore hello DTU massimo per database. |Verificare hello valore DTU minimo per database non superi hello DTU massimo per database. |
| Da definire |EX_USER |dimensioni di archiviazione Hello per un singolo database in un pool elastico non possono superare le dimensioni massime hello consentite da ' %. * ls' del pool elastico a livello di servizio. |livello di servizio del pool elastico |le dimensioni massime per il database hello Hello superano le dimensioni massime hello consentite dal livello di servizio hello pool elastico. |Impostare le dimensioni massime del database hello entro i limiti di hello di hello le dimensioni massime consentite dal livello di servizio del pool elastico hello hello. |

Argomenti correlati:

* [Creare un pool elastico (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [Gestire un pool elastico (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [Creare un pool elastico (PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [Monitorare e gestire un pool elastico (PowerShell)](sql-database-elastic-pool-manage-powershell.md).

## <a name="general-errors"></a>Errori generali
gli errori seguenti Hello non rientra in tutte le categorie precedenti.

| Codice di errore | Gravità | Descrizione |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin> non è un nome valido perché contiene caratteri non validi. |
| 18452 |14 |Accesso non riuscito. Hello accesso proviene da un dominio non trusted e non può essere utilizzato con Windows authentication.%. & #x2a; ls (account di accesso di Windows non supportati in questa versione di SQL Server). |
| 18456 |14 |Accesso non riuscito per l'utente ' %. #x2a;ls'.%. & #x2a % ls. & #x2a; ls (hello accesso non riuscito per l'utente "%. & #x2a; ls". Impossibile modificare la password di Hello. La modifica della password durante l'accesso non è supportata in questa versione di SQL Server.) |
| 18470 |14 |Accesso non riuscito per l’utente '%.&#x2a;ls'. Motivo: account hello è disabled.%. & #x2a; ls |
| 40014 |16 |Più database non possono essere utilizzato in hello stessa transazione. |
| 40054 |16 |Le tabelle senza indice cluster non sono supportate in questa versione di SQL Server. Creare un indice cluster e riprovare. |
| 40133 |15 |Questa operazione non è supportata in questa versione di SQL Server. |
| 40506 |16 |Il SID specificato non è valido per questa versione di SQL Server. |
| 40507 |16 |Non è possibile richiamare '%.&#x2a;ls' con parametri in questa versione di SQL Server. |
| 40508 |16 |Istruzione USE non è supportato tooswitch tra database. Utilizzare un nuova connessione tooconnect tooa altro database. |
| 40510 |16 |L’istruzione '%.&#x2a;ls' non è supportata in questa versione di SQL Server. |
| 40511 |16 |La funzione predefinita '%.&#x2a;ls' non è supportata in questa versione di SQL Server. |
| 40512 |16 |La funzione deprecata '%ls' non è supportata in questa versione di SQL Server. |
| 40513 |16 |La variabile server '%.&#x2a;ls' non è supportata in questa versione di SQL Server. |
| 40514 |16 |'%ls non è supportato in questa versione di SQL Server. |
| 40515 |16 |Nome di riferimento toodatabase e/o server in '%. & #x2a; ls' non è supportata in questa versione di SQL Server. |
| 40516 |16 |Gli oggetti temporanei globali non sono supportati in questa versione di SQL Server. |
| 40517 |16 |L'opzione dell'istruzione o parola chiave '%.&#x2a;ls' non è supportata in questa versione di SQL Server. |
| 40518 |16 |Il comando DBCC '%.&#x2a;ls' non è supportato in questa versione di SQL Server. |
| 40520 |16 |La classe a protezione diretta '%S_MSG' non è supportata in questa versione di SQL Server. |
| 40521 |16 |Classe di entità a protezione diretta '% S_MSG' non è supportato nell'ambito del server hello in questa versione di SQL Server. |
| 40522 |16 |Il tipo di entità database '%.&#x2a;ls' non è supportato in questa versione di SQL Server. |
| 40523 |16 |La creazione dell’utente implicito '%.&#x2a;ls' non è supportata in questa versione di SQL Server. Creare in modo esplicito utente hello prima di utilizzarlo. |
| 40524 |16 |Il tipo di dati '%.&#x2a;ls' non è supportato in questa versione di SQL Server. |
| 40525 |16 |WITH '%.ls’ non è supportato in questa versione di SQL Server. |
| 40526 |16 |Il provider di set di righe '%.&#x2a;ls' non è supportato in questa versione di SQL Server. |
| 40527 |16 |I server collegati non sono supportati in questa versione di SQL Server. |
| 40528 |16 |Gli utenti non possono essere mappato toocertificates, chiavi asimmetriche o account di accesso di Windows in questa versione di SQL Server. |
| 40529 |16 |La funzione predefinita '%.&#x2a;ls' nel contesto di rappresentazione non è supportata in questa versione di SQL Server. |
| 40532 |11 |Impossibile aprire il server "%. & #x2a; ls" richiesto dall'account di accesso hello. Hello accesso non riuscito. |
| 40553 |16 |Hello sessione è stata terminata a causa di utilizzo eccessivo della memoria. Provare a modificare la query tooprocess meno righe.<br/><br/>*Nota:* riducendo il numero di hello di `ORDER BY` e `GROUP BY` operazioni nel codice Transact-SQL consente di ridurre i requisiti di memoria hello della query. |
| 40604 |16 |Impossibile non CREATE/ALTER DATABASE perché supererebbe la quota hello del server di hello. |
| 40606 |16 |Collegamento di database non supportato in questa versione di SQL Server. |
| 40607 |16 |Gli account di accesso Windows non sono supportati in questa versione di SQL Server. |
| 40611 |16 |È possibile definire un massimo di 128 regole firewall per i server. |
| 40614 |16 |L'indirizzo IP iniziale della regola firewall non può superare l'indirizzo IP finale. |
| 40615 |16 |Impossibile aprire il server '{0}' richiesto dall'account di accesso hello. Client con indirizzo IP '\\{1 \\}' server hello tooaccess non è consentito.  accesso tooenable, utilizzare hello portale Database SQL o eseguire sp_set_firewall_rule nel database master di hello toocreate una regola del firewall per l'indirizzo IP o un intervallo di indirizzi.  Potrebbe richiedere fino a toofive minuti per questo effetto tootake di modifica. |
| 40617 |16 |nome della regola firewall Hello che inizia con <rule name> è troppo lungo. La lunghezza massima è 128. |
| 40618 |16 |nome della regola firewall Hello non può essere vuoto. |
| 40620 |16 |Hello accesso non riuscito per l'utente "%. & #x2a; ls". Impossibile modificare la password di Hello. La modifica della password durante l'accesso non è supportata in questa versione di SQL Server. |
| 40627 |20 |Operazione in corso nel server '{0}' e nel database '{1}'. Attendere alcuni minuti prima di riprovare. |
| 40630 |16 |Convalida della password non riuscita. Hello password non soddisfa i requisiti dei criteri perché è troppo breve. |
| 40631 |16 |password Hello specificata è troppo lunga. password Hello deve contenere non più di 128 caratteri. |
| 40632 |16 |Convalida della password non riuscita. Hello password non soddisfa i requisiti dei criteri perché non è sufficientemente complessa. |
| 40636 |16 |Impossibile utilizzare un nome di database riservato '%.&#x2a;ls' in questa operazione. |
| 40638 |16 |L'ID sottoscrizione <id-sottoscrizione> non è valido. La sottoscrizione non esiste. |
| 40639 |16 |Richiesta non è conforme tooschema: <schema error>. |
| 40640 |20 |server Hello ha rilevato un'eccezione imprevista. |
| 40641 |16 |Hello specificato percorso non è valido. |
| 40642 |17 |server Hello è attualmente troppo occupato. Riprovare più tardi. |
| 40643 |16 |Hello è specificato il valore dell'intestazione x-ms-version non è valido. |
| 40644 |14 |Toohello di accesso non riusciti tooauthorize sottoscrizione specificata. |
| 40645 |16 |Il nome del server <servername> non può essere vuoto o null. Si può solo essere composto da lettere minuscole 'a'-'z', i numeri di hello 0-9 e trattino hello. trattino Hello non può generare oppure hello finale. |
| 40646 |16 |L’ID sottoscrizione non può essere vuoto. |
| 40647 |16 |Server nomeserver non disponibile per la sottoscrizione < id-sottoscrizione. |
| 40648 |17 |Esecuzione di un numero eccessivo di richieste. Riprovare più tardi. |
| 40649 |16 |È stato specificato un tipo di contenuto non valido. È supportato solo il codice XML o l’applicazione. |
| 40650 |16 |Sottoscrizione < id-sottoscrizione > non esiste o non è pronto per l'operazione di hello. |
| 40651 |16 |Impossibile eseguire server toocreate hello sottoscrizione < id-sottoscrizione > è disabilitata. |
| 40652 |16 |Impossibile spostare o creare il server. La sottoscrizione <id-sottoscrizione> supera la quota del server. |
| 40671 |17 |Errore di comunicazione tra il gateway hello e servizio di gestione di hello. Riprovare più tardi. |
| 40852 |16 |Impossibile aprire il database ' %. *ls' sul server ' %.* ls' richiesto dall'account di accesso di hello. Database di Access toohello è consentita solo con una stringa di connessione con sicurezza abilitata. tooaccess dal database, modificare il toocontain di stringhe di connessione sicura nel server hello FQDN -.database.windows "nome server".net deve essere un nome modificato too'server' database. `secure`. windows.net. |
| 45168 |16 |Ciao sistema SQL Azure è in condizioni di carico e sta fissando un limite superiore per le operazioni simultanee CRUD del database per un singolo server (ad esempio, creare database). server Hello specificato nel messaggio di errore hello ha superato il numero massimo di hello di connessioni simultanee. Riprovare. |
| 45169 |16 |Ciao sistema SQL azure è in condizioni di carico e sta fissando un limite superiore per il numero di hello di operazioni simultanee CRUD di una singola sottoscrizione (ad esempio, creare server). sottoscrizione Hello specificato errore hello messaggio ha superato il numero massimo di hello di connessioni simultanee e hello richiesta è stata negata. Riprovare. |

## <a name="related-links"></a>Collegamenti correlati
* [Funzionalità di database SQL di Azure](sql-database-features.md)
* [Limiti delle risorse del database SQL di Azure](sql-database-resource-limits.md)

