---
title: "limiti di capacità del Data Warehouse aaaSQL | Documenti Microsoft"
description: I valori massimi per le connessioni, i database, le tabelle e le query per SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>Limiti di capacità di SQL Data Warehouse
Hello nelle tabelle seguenti sono i valori massimi di hello consentiti per i vari componenti di Azure SQL Data Warehouse.

## <a name="workload-management"></a>Gestione del carico di lavoro
| Categoria | Descrizione | Massima |
|:--- |:--- |:--- |
| [Unità Data Warehouse (DWU)][Data Warehouse Units (DWU)] |Max DWU per un singolo SQL Data Warehouse |6000 |
| [Unità Data Warehouse (DWU)][Data Warehouse Units (DWU)] |Max DWU per un singolo SQL server |6000 per impostazione predefinita<br/><br/> Per impostazione predefinita, ogni computer SQL server (ad esempio myserver.database.windows.net) prevede una Quota di DTU di 45,000 che consente backup too6000 DWU. Questa quota è semplicemente un limite di sicurezza. È possibile aumentare la quota da [la creazione di un ticket di supporto] [ creating a support ticket] e selezionando *Quota* come tipo di richiesta hello.  le DTU, è necessario moltiplicare toocalculate hello 7.5 per totale hello DWU necessari. È possibile visualizzare il consumo di DTU corrente dal pannello hello SQL server nel portale di hello. Il database sia in pausa e riavviato conteggiati per la quota di DTU hello. |
| Connessione del database |Sessioni simultanee aperte |1024<br/><br/>È supportato un massimo di connessioni attive 1024, ognuno dei quali può inviare i database di SQL Data Warehouse tooa le richieste in hello contemporaneamente. Si noti che non esistono limiti sul numero di hello di query che possono essere effettivamente eseguite contemporaneamente. Quando viene superato il limite di concorrenza hello, hello richiesta viene inviata in una coda interna in cui è in attesa toobe elaborati. |
| Connessione del database |Memoria massima per le istruzioni preparate |20 MB |
| [Gestione del carico di lavoro][Workload management] |Numero massimo di query simultanee |32<br/><br/> Per impostazione predefinita, SQL Data Warehouse può eseguire un massimo di 32 query simultanee e mette in coda le query rimanenti.<br/><br/>è possibile ridurre il livello di concorrenza Hello quando gli utenti vengono assegnati tooa classe di risorse superiore o quando SQL Data Warehouse è configurato con DWU bassa. Alcune query, ad esempio le query DMV, sono sempre consentiti toorun. |
| [Tempdb][Tempdb] |Dimensioni massime del database Tempdb |399 GB per DW100. Pertanto, in Tempdb DWU1000 è too3.99 dimensioni TB |

## <a name="database-objects"></a>Oggetti di database
| Categoria | Descrizione | Massima |
|:--- |:--- |:--- |
| Database |Dimensioni massime |240 TB compressi su disco<br/><br/>Questo spazio è indipendente di spazio di tempdb o di log e pertanto questo spazio è dedicato toopermanent tabelle.  La compressione stimata per columnstore cluster è 5X.  La compressione consente hello database toogrow tooapproximately 1 PB quando tutte le tabelle sono columnstore cluster (tipo di tabella predefinito hello). |
| Tabella |Dimensioni massime |60 TB compressi su disco |
| Tabella |Tabelle per database |2 miliardi |
| Tabella |Colonne per tabella |1024 colonne |
| Tabella |Byte per colonna |Dipende dalla colonna [tipo di dati][data type].  Il limite è 8000 per i tipi di dati char, 4000 per nvarchar o 2 GB per i tipi di dati MAX. |
| Tabella |Byte per riga, dimensioni definite |8060 byte<br/><br/>Hello numero di byte per ogni riga viene calcolato in hello esattamente come è per SQL Server con la compressione di pagina. Ad esempio SQL Server, SQL Data Warehouse supporta l'archiviazione di overflow della riga che consente di **colonne a lunghezza variabile** toobe inserito all'esterno di righe. Quando le righe di lunghezza variabile vengono inviate all'esterno di righe, solo i radice di 24 byte viene archiviata nel record principale hello. Per ulteriori informazioni, vedere hello [Overflow della riga di dati superiore a 8 KB] [ Row-Overflow Data Exceeding 8 KB] articolo di MSDN. |
| Tabella |Partizioni per tabella |15.000<br/><br/>Per prestazioni elevate, è consigliabile ridurre al minimo il numero di hello di partizioni è necessario mentre ancora supportare i requisiti aziendali. Come hello aumentare del numero di partizioni, il sovraccarico di hello per Data Definition Language (DDL) e aumentano e comporta una riduzione delle prestazioni di operazioni (Data Manipulation Language). |
| Tabella |Caratteri per valore limite della partizione. |4000 |
| Indice |Indici non in cluster per tabella. |999<br/><br/>Si applica solo a tabelle toorowstore. |
| Indice |Indici in cluster per tabella. |1<br><br/>Applica le tabelle rowstore e columnstore tooboth. |
| Indice |Dimensioni della chiave indice. |900 byte.<br/><br/>Si applica solo gli indici toorowstore.<br/><br/>Se i dati esistenti di hello nelle colonne hello non superino i 900 byte quando viene creato l'indice di hello, è possibile creare indici in colonne varchar con una dimensione massima di più di 900 byte. Tuttavia, l'inserimento in un secondo momento o azioni UPDATE eseguite su colonne hello che causano hello dimensioni totali tooexceed 900 byte avranno esito negativo. |
| Indice |Colonne chiave per indice. |16<br/><br/>Si applica solo gli indici toorowstore. Gli indici columnstore in cluster includono tutte le colonne. |
| Statistiche |Dimensioni di hello combinare i valori di colonna. |900 byte. |
| Statistiche |Colonne per oggetto statistiche. |32 |
| Statistiche |Statistiche create per le colonne per tabella. |30.000 |
| Stored procedure |Livello massimo di annidamento. |8 |
| View |Colonne per vista |1.024 |

## <a name="loads"></a>Operazioni di caricamento
| Categoria | Descrizione | Massima |
|:--- |:--- |:--- |
| Operazioni di caricamento di PolyBase |MB per riga |1<br/><br/>Carica Polybase sono tooloading limitato di righe sia minore di 1MB e non è possibile caricare tooVARCHR(MAX), nvarchar (max) o varbinary (max).<br/><br/> |

## <a name="queries"></a>Query
| Categoria | Descrizione | Massima |
|:--- |:--- |:--- |
| Query |Query in coda nelle tabelle utente |1000 |
| Query |Query simultanee nelle viste di sistema |100 |
| Query |Query in coda nelle viste di sistema |1000 |
| Query |Parametri massimi |2098 |
| Batch |Dimensione massima |65.536*4096 |
| Risultati SELECT |Colonne per riga |4096<br/><br/>Non è possibile avere più di 4096 colonne per ogni riga hello selezionare risultato. Non è garantito che si possa avere sempre 4096. Se il piano di query hello richiede una tabella temporanea, potrebbero applicarsi colonne 1024 hello per ogni tabella massima. |
| SELECT |Sottoquery nidificate |32<br/><br/>In un'istruzione SELECT non è possibile avere più di 32 sottoquery nidificate. Non è garantito che si possa averne sempre 32. Ad esempio, un JOIN può introdurre una sottoquery nel piano di query hello. numero di Hello di sottoquery può essere limitata anche dalla memoria disponibile. |
| SELECT |Colonne per JOIN |1024 colonne<br/><br/>Non è possibile avere più di 1024 colonne in hello JOIN. Non è garantito che si possa averne sempre 1024. Se il piano di JOIN hello richiede una tabella temporanea con più colonne risultato del JOIN hello, hello 1024 limite si applica la tabella temporanea toohello. |
| SELECT |Byte per le colonne GROUP BY. |8060<br/><br/>le colonne di Hello nella clausola GROUP BY hello possono avere un massimo di 8060 byte. |
| SELECT |Byte per le colonne ORDER BY |8060 byte.<br/><br/>le colonne di Hello nella clausola ORDER BY hello possono avere un massimo di 8060 byte. |
| Identificatori e costanti per istruzione |Numero di identificatori e costanti di riferimento. |65.535<br/><br/>SQL Data Warehouse limita il numero di hello identificatori e costanti che possono essere contenute in un'unica espressione di una query. Il limite è 65.535. Il superamento di questo numero genera un errore 8632 di SQL Server. Per altre informazioni, vedere [Errore interno: è stato raggiunto un limite di servizi di espressione][Internal error: An expression services limit has been reached]. |

## <a name="metadata"></a>Metadati
| Vista di sistema | Righe massime |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10.000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |Numero totale di processi di lavoro DMS per hello 1000 più recente di richieste SQL. |
| sys.dm_pdw_errors |10.000 |
| sys.dm_pdw_exec_requests |10.000 |
| sys.dm_pdw_exec_sessions |10.000 |
| sys.dm_pdw_request_steps |Numero totale di passaggi per le richieste SQL hello 1000 più recenti archiviati nel sys.dm_pdw_exec_requests. |
| sys.dm_pdw_os_event_logs |10.000 |
| sys.dm_pdw_sql_requests |Hello richieste più recenti 1000 SQL che vengono archiviate in sys.dm_pdw_exec_requests. |

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni di riferimento, vedere la [panoramica degli argomenti di riferimento di SQL Data Warehouse][SQL Data Warehouse reference overview].

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
