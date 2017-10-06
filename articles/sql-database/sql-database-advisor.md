---
title: indicazioni aaaPerformance - Database SQL di Azure | Documenti Microsoft
description: "Hello Database SQL di Azure vengono forniti consigli per i database di SQL che può migliorare le prestazioni di query corrente."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>Raccomandazioni per le prestazioni

Database SQL di Azure apprende e si adatta all'applicazione e vengono forniti consigli personalizzati consentendo prestazioni hello toomaximize dei database SQL. Le prestazioni vengono valutate continuamente analizzando la cronologia relativa all'utilizzo del database SQL. consigli Hello forniti sono basati su un modello di carico di lavoro univoco del database e migliorare le prestazioni.

> [!NOTE]
> Il modo consigliato per usare le raccomandazioni prevede l'abilitazione della funzionalità di 'Ottimizzazione automatica' nel database. Per altri dettagli, vedere [Ottimizzazione automatica](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Raccomandazioni relative alla creazione di indici
Database SQL di Azure in modo continuo consente di monitorare le query hello in esecuzione e identifica gli indici di hello che potrebbe migliorare le prestazioni di hello. Dopo aver raccolto dati sufficienti per confermare la mancanza di un determinato indice, verrà creata una nuova raccomandazione **Crea indice**. Periodo di tempo, potrebbe avere confidenza compilazioni di Database SQL Azure tramite la stima indice hello miglioramento delle prestazioni. A seconda di miglioramento delle prestazioni stimato hello, raccomandazioni vengono classificate come alta, Media o bassa. 

Gli indici creati usando le raccomandazioni vengono sempre contrassegnati come indici auto_created. È possibile scoprire quali indici sono auto_created esaminando la vista sys.indexes. Gli indici creati automaticamente non bloccano i comandi ALTER/RENAME. Se si tenta di colonna hello toodrop dotato di un indice automaticamente su di esso, hello comando passa automaticamente hello creato l'indice viene quindi eliminato con il comando hello anche. Comando ALTER/RINOMINA hello colonne indicizzate bloccano indici normali.

Una volta creare hello viene applicata l'indicazione di un indice, Database SQL di Azure verranno confrontate le prestazioni delle query hello con hello linea di base. Se il nuovo indice introdotti miglioramenti delle prestazioni di hello, indicazione verrà contrassegnata come esito positivo e report di impatto sarà disponibile. In caso di indice hello non offrire i vantaggi di hello, verrà ripristinato automaticamente. In questo modo il Database di SQL Azure garantisce che utilizzando indicazioni solo migliorare le prestazioni del database hello.

Qualsiasi **Crea indice** raccomandazione è Backoff criteri che non consentono l'applicazione hello dell'indicazione se utilizzo di DTU di database o il pool di hello è superiore all'80% 20 minuti o se l'archiviazione hello è superiore al 90% di utilizzo. In questo caso, la raccomandazione hello verrà posticipata.

## <a name="drop-index-recommendations"></a>Raccomandazioni relative all'eliminazione di indici
Un indice mancante, Database SQL di Azure in modo continuo toodetecting analizza inoltre prestazioni hello di indici esistente. Se un indice è inutilizzato, il database SQL di Azure proporrà di eliminarlo. L'eliminazione di un indice è consigliabile in due casi:
* L'indice è un duplicato di un altro indice (include colonna, schema di partizione e filtri identici)
* L'indice risulta inutilizzato per un periodo prolungato (93 giorni)

Indicazioni relative agli indici di rilascio anche passare attraverso la verifica di hello dopo l'implementazione. Se un miglioramento delle prestazioni di hello report impatto hello sarà disponibile. Se viene invece rilevata una riduzione delle prestazioni, la raccomandazione verrà annullata.


## <a name="parameterize-queries-recommendations"></a>Raccomandazioni relative alla creazione di query con parametri
**Parametrizzare le query** indicazioni vengono visualizzati quando si dispone di uno o più query che vengono costantemente ricompilata ma finisce con hello stesso piano di esecuzione di query. Questa condizione apre tooapply un'opportunità forzata, che consentirà di piani di query toobe memorizzati nella cache e riutilizzati in hello futura miglioramento delle prestazioni e ridurre l'utilizzo delle risorse. 

Ogni query eseguita inizialmente in SQL Server deve toogenerate toobe compilato un piano di esecuzione. Ogni piano generato viene aggiunto toohello cache dei piani e le esecuzioni successive di hello stessa query è possibile riutilizzare il piano dalla cache di hello, eliminando hello necessità di ulteriore compilazione. 

Le applicazioni che inviano query, inclusi i valori senza parametri, possono provocare un overhead delle prestazioni tooa, dove per ogni query con valori di parametro diversi piano di esecuzione hello viene compilata nuovamente. In molti hello casi stesse query con parametri diversi, generano valori hello stessi piani di esecuzione, ma questi piani vengono aggiunti separatamente ancora toohello cache dei piani. Ricompilazione di piani di esecuzione utilizzare le risorse del database, incrementare hello durata ora e overflow hello piano di query causando cache dei piani toobe eliminato dalla cache di hello. Questo comportamento di SQL Server può essere modificato impostando l'opzione parameterization nel database di hello forzato hello. 

toohelp è stimare l'impatto di hello questa raccomandazione, vengono fornite con un confronto tra CPU effettiva hello hello e utilizzo previsto l'utilizzo della CPU (come se è stato applicato l'indicazione di hello). Inoltre risparmio tooCPU, la durata della query diminuisce per hello trascorso in compilazione. Sarà inoltre necessario molto meno overhead nella cache dei piani, consentendo di maggioranza di hello toostay nella cache dei piani e riutilizzare. È possibile applicare questa raccomandazione rapidamente e facilmente facendo clic su hello **applica** comando. 

Quando si applica questa raccomandazione, verrà attivata la parametrizzazione forzata in pochi minuti sul database e viene avviato il monitoraggio di processo che dura circa 24 ore hello. Dopo questo periodo, sarà possibile essere in grado di toosee hello convalida report che mostra l'utilizzo della CPU del database di 24 ore prima e dopo l'applicazione di raccomandazione hello. Preparazione del Database SQL dispone di un meccanismo di sicurezza che verrà automaticamente ripristinato raccomandazione hello applicato nel caso in cui è stata rilevata una regressione delle prestazioni.

## <a name="fix-schema-issues-recommendations"></a>Raccomandazioni relative alla correzione di problemi di schema
**Risolvere i problemi dello schema** indicazioni vengono visualizzati quando hello servizio Database SQL notifiche un'anomalia numero hello correlate allo schema di errori di SQL nel Database SQL di Azure in corso. In genere questa indicazione viene visualizzata quando il database rileva più errori correlati allo schema (nome di colonna non valido, nome di oggetto non valido e così via) nell'arco di un'ora.

"I problemi dello schema" sono una classe di errori di sintassi in SQL Server che si verificano quando non sono allineate hello definizioni di query SQL hello e hello hello dello schema del database. Ad esempio, una delle colonne hello prevede dalla query hello potrebbe essere manca nella tabella di destinazione hello o viceversa. 

Indicazione di "Correzione problema relativo allo schema" viene visualizzato quando il servizio di Database SQL di Azure rileva un'anomalia numero hello correlate allo schema di errori di SQL nel Database SQL di Azure in corso. Hello gli errori di hello illustrato nella tabella che sono correlati tooschema problemi seguenti:

| Codice di errore SQL | Message |
| --- | --- |
| 201 |La procedura o funzione '*' richiede il parametro '*', che non è stato specificato. |
| 207 |Il nome di colonna '*' non è valido. |
| 208 |Il nome di oggetto '*' non è valido. |
| 213 |Il nome della colonna o il numero dei valori specificati non corrisponde alla definizione della tabella. |
| 2812 |Non è stato possibile trovare la stored procedure '*'. |
| 8144 |Numero eccessivo di argomenti specificati per la procedura o la funzione *. |

## <a name="next-steps"></a>Passaggi successivi
Monitorare le raccomandazioni e continuare tooapply li toorefine prestazioni. I carichi di lavoro dei database sono dinamici e cambiano in modo continuo. Preparazione del Database SQL continua toomonitor e fornire indicazioni che possono potenzialmente migliorare le prestazioni del database. 

* Vedere [consigli relativi alle prestazioni nel portale di Azure hello](sql-database-advisor-portal.md) per i passaggi per la modalità consigli relativi alle prestazioni toouse in hello portale di Azure.
* Vedere [informazioni dettagliate prestazioni Query](sql-database-query-performance.md) toolearn sulle e visualizzazione hello impatto sulle prestazioni delle query top.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Archivio query](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md)

