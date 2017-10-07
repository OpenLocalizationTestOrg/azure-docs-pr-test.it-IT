---
title: dati aaaSync (anteprima) | Documenti Microsoft
description: "Questa panoramica è un'introduzione all'anteprima di sincronizzazione dati SQL di Azure."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>Sincronizzare i dati tra più database cloud e locali con la sincronizzazione dati SQL

Sincronizzazione dati SQL è un servizio basato su Database SQL di Azure che consente di sincronizzare dati hello selezionati bidirezionale tra più database SQL e le istanze di SQL Server.

Sincronizzazione dati è basata il concetto di hello di un gruppo di sincronizzazione. Un gruppo di sincronizzazione è un gruppo di database che si desidera toosynchronize.

Un gruppo di sincronizzazione è hello le proprietà seguenti:

-   Hello **dello Schema di sincronizzazione** descrive la sincronizzazione dei dati.

-   Hello **direzione di sincronizzazione** può essere bidirezionale o possano essere trasmessi solo in una direzione. Vale a dire hello direzione di sincronizzazione può essere *Hub tooMember* o *tooHub membro*, o entrambi.

-   Hello **intervallo sincronizzazione** è la frequenza con cui viene eseguita la sincronizzazione.

-   Hello **criteri di risoluzione dei conflitti** è un criterio a livello di gruppo, che può essere *prevale l'Hub* o *wins membro*.

Sincronizzazione dati viene utilizzata una data toosynchronize topologia hub e spoke. Per definire uno dei database hello in gruppo hello come hello Database Hub. Hello altri database hello sono database membri. Sincronizzazione si verifica solo tra hello Hub e ai singoli membri.
-   Hello **Database Hub** deve essere un Database SQL di Azure.
-   Hello **database membri** può essere il database SQL, database di SQL Server locali o istanze di SQL Server in macchine virtuali di Azure.
-   Hello **sincronizzazione Database** contiene i metadati di hello e log per il Database di sincronizzazione dati di sincronizzazione. hello ha toobe un Database SQL di Azure si trova in hello stessa area hello Database Hub. Hello sincronizzazione Database viene creato dall'utente e i clienti di proprietà.

> [!NOTE]
> Se si utilizza un database locale, è necessario troppo[configurare un agente locale.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![Sincronizzare i dati tra database](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Quando la sincronizzazione dati toouse

Sincronizzazione dati è utile nei casi in cui i dati devono toobe tenuto aggiornato toodate tra diversi database SQL di Azure o i database di SQL Server. Ecco i casi di utilizzo principali hello per la sincronizzazione dati:

-   **Sincronizzazione dei dati ibrido:** con la sincronizzazione dei dati, è possibile mantenere i dati sincronizzati tra i database locali e le applicazioni di database SQL di Azure tooenable ibrido. Questa funzionalità può presentare ricorso toocustomers che prendono in considerazione lo spostamento toohello cloud e si desidera tooput alcune delle loro applicazione in Azure.

-   **Le applicazioni distribuite:** In molti casi, è utile tooseparate diversi carichi di lavoro in database diversi. Ad esempio, se si dispone di un database di produzione di grandi dimensioni, ma è anche necessario toorun un report o il carico di lavoro analitica per i dati, è utile toohave un secondo database per il carico di lavoro aggiuntivo. Questo approccio riduce l'impatto sulle prestazioni di hello sul carico di lavoro di produzione. È possibile utilizzare la sincronizzazione dati tookeep questi due database sincronizzati.

-   **Applicazioni distribuite a livello globale:** molte aziende sono estese a più aree, a volte anche in paesi diversi. latenza di rete, toominimize è migliore toohave chiudere i dati in un'area tooyou. Sincronizzazione dati, è possibile mantenere facilmente i database in aree geografiche in tutto il mondo hello sincronizzato.

Si sconsiglia di sincronizzazione dati per hello seguenti scenari:

-   Ripristino di emergenza

-   Scalabilità in lettura

-   ETL (tooOLAP OLTP)

-   Migrazione da tooAzure di SQL Server on-premise SQL Database

## <a name="how-does-data-sync-work"></a>Come funziona la sincronizzazione dati? 

-   **Rilevamento delle modifiche ai dati:** sincronizzazione dati tiene traccia delle modifiche tramite trigger di inserimento, aggiornamento ed eliminazione. le modifiche di Hello vengono registrate in una tabella laterale in database utente hello.

-   **Sincronizzazione dei dati:** il servizio di sincronizzazione dati è progettato in base a un modello hub-spoke. Hello Hub viene sincronizzato con ogni membro singolarmente. Le modifiche da hello Hub sono membro toohello scaricato e quindi le modifiche dal membro hello toohello caricato Hub.

-   **Risoluzione dei conflitti:** sincronizzazione dati offre due opzioni per la risoluzione dei conflitti, ovvero *Priorità hub* o *Priorità client*.
    -   Se si seleziona *prevale l'Hub*, le modifiche di hello nell'hub hello sovrascrivono sempre le modifiche nel membro hello.
    -   Se si seleziona *wins membro*, hello modifiche hello membro Sovrascrivi modifiche hub hello. Se è presente più di un membro, valore finale hello dipende innanzitutto viene sincronizzato il membro.

## <a name="limitations-and-considerations"></a>Limitazioni e considerazioni

### <a name="performance-impact"></a>Impatto sulle prestazioni
Sincronizzazione dati Usa inserirà, aggiornarla ed Elimina trigger tootrack modifiche. Crea tabelle nel database utente hello per il rilevamento delle modifiche. Queste attività di rilevamento delle modifiche hanno un impatto sul carico di lavoro del database. Valutare il livello di servizio e aggiornare se necessario.

### <a name="eventual-consistency"></a>Coerenza finale
Dato che la sincronizzazione dati è basata su trigger, la coerenza delle transazioni non è garantita. Microsoft garantisce che tutte le modifiche vengono apportate alla fine e che la sincronizzazione dati non causi perdite di dati.

### <a name="unsupported-data-types"></a>Tipi di dati non supportati

-   FileStream

-   Tipo definito dall'utente (UDT) SQL/CLR

-   XMLSchemaCollection (supportato da XML)

-   Cursor, Timestamp, Hierarchyid

### <a name="requirements"></a>Requisiti

-   Ogni tabella deve avere una chiave primaria.

-   Una tabella non può contenere una colonna identity che non è la chiave primaria di hello.

-   nomi di Hello di oggetti (database, tabelle e colonne) non possono contenere hello caratteri stampabili punto (.), parentesi quadra aperta ([), o parentesi quadra chiusa (]).

### <a name="limitations-on-service-and-database-dimensions"></a>Limitazioni alle dimensioni del servizio e del database

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **Dimensioni**                                                      | **Limite**              | **Soluzione alternativa**              |
| Numero massimo di gruppi di sincronizzazione a cui può appartenere qualsiasi database.       | 5                      |                             |
| Numero massimo di endpoint in un singolo gruppo di sincronizzazione              | 30                     | Creare più gruppi di sincronizzazione |
| Numero massimo di endpoint locali in un singolo gruppo di sincronizzazione. | 5                      | Creare più gruppi di sincronizzazione |
| Nomi di database, tabella, schema e colonna                       | 50 caratteri per nome |                             |
| Tabelle in un gruppo di sincronizzazione                                          | 500                    | Creare più gruppi di sincronizzazione |
| Colonne in una tabella in un gruppo di sincronizzazione                              | 1000                   |                             |
| Dimensioni delle righe di dati in una tabella                                        | 24 MB                  |                             |
| Intervallo minimo di sincronizzazione                                           | 5 minuti              |                             |

## <a name="common-questions"></a>Domande frequenti

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>Con quale frequenza sincronizzazione dati sincronizza i dati? 
frequenza minima di Hello è ogni cinque minuti.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>È possibile utilizzare toosync sincronizzazione dati tra database solo di SQL Server locale? 
Non direttamente. È possibile sincronizzare tra i database di SQL Server on-premise indirettamente, tuttavia, la creazione di un database Hub in Azure e quindi aggiungendo gruppo di sincronizzazione toohello database on-premise hello.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>È possibile utilizzare i dati di sincronizzazione dati tooseed del database di produzione database tooan vuoto e quindi mantenerli sincronizzati? 
Sì. Creare manualmente schema hello in hello nuovo database tramite script, da hello originale. Dopo la creazione dello schema di hello, aggiungere dati di hello tabelle tooa sincronizzazione gruppo toocopy hello e mantenerli sincronizzati.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>Perché vengono visualizzate tabelle che non risultano essere state create?  
Sincronizzazione dati crea tabelle laterali nel database utente per il rilevamento delle modifiche. Non eliminarle in quanto sono richieste per il funzionamento di sincronizzazione dati.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>Viene visualizzato un messaggio di errore che ha dichiarato "Impossibile inserire il valore di hello NULL nella colonna hello \<colonna\>. La colonna non ammette valori Null." Cosa significa e come risolvere errori di hello? 
Questo messaggio di errore indica uno dei due problemi seguenti di hello:
1.  Potrebbe essere presente una tabella priva di chiave primaria. toofix questo problema, aggiungere una tabelle hello tooall chiave primaria esegue la sincronizzazione.
2.  Potrebbe essere presente una clausola WHERE nell'istruzione CREATE INDEX. La sincronizzazione non è in grado di gestire questa condizione. toofix questo problema, rimuovere la clausola WHERE hello o apportare manualmente modifiche di hello tooall database. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>In che modo la sincronizzazione dati gestisce i riferimenti circolari? Vale a dire quando hello stessi dati viene sincronizzati in più gruppi di sincronizzazione e continua a cambiare di conseguenza?
La sincronizzazione dati non gestisce i riferimenti circolari. Essere tooavoid che li. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla sincronizzazione dati SQL, vedere:

-   [Introduzione alla sincronizzazione dati SQL](sql-database-get-started-sql-data-sync.md)

-   Completare PowerShell esempi che illustrano la modalità di sincronizzazione dati SQL tooconfigure:
    -   [Utilizzare PowerShell toosync tra più database SQL di Azure](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Utilizzare PowerShell toosync tra un Database SQL di Azure e un database locale di SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Scaricare la documentazione tecnica sincronizzazione dati SQL completezza hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Scaricare la documentazione delle API REST di sincronizzazione dati SQL hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

Per altre informazioni sul database SQL, vedere:

-   [Panoramica del database SQL](sql-database-technical-overview.md)

-   [Gestione del ciclo di vita del database](https://msdn.microsoft.com/library/jj907294.aspx)
