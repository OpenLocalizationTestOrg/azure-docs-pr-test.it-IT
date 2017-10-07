---
title: Esercitazioni di ripristino di emergenza Database aaaSQL | Documenti Microsoft
description: Altre informazioni e procedure consigliate per l'utilizzo di keep toohelp di Database SQL di Azure tooperform disaster recovery drill le interruzioni toofailures resilienti applicazioni aziendali critiche di importanza.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Esercitazione per il ripristino di emergenza
È consigliabile verificare periodicamente la conformità delle applicazioni per il flusso di lavoro di ripristino. Comportamento dell'applicazione hello verifica e le implicazioni dell'interruzione di perdite e/o hello dati prevede che il failover è buona norma engineering. Inoltre, questa verifica è richiesta dalla maggior parte degli standard del settore come parte della certificazione di continuità aziendale.

L'esercitazione per il ripristino di emergenza prevede l'esecuzione delle attività seguenti:

* Simulazione dell'interruzione del livello dati
* Ripristino
* Convalida dell'integrità dell'applicazione dopo il ripristino

A seconda di come si [progettato l'applicazione per la continuità aziendale](sql-database-business-continuity.md), drill hello tooexecute di hello del flusso di lavoro può variare. Di seguito sono riportati alcuni suggerimenti hello condurre un'analisi di ripristino di emergenza nel contesto di hello del Database SQL di Azure.

## <a name="geo-restore"></a>Ripristino geografico
tooprevent hello potenziale perdita di dati durante l'esecuzione di un'analisi di ripristino di emergenza, è consigliabile eseguire drill hello usando un ambiente di test mediante la creazione di una copia dell'ambiente di produzione hello e l'uso del flusso di lavoro failover dell'applicazione hello tooverify.

#### <a name="outage-simulation"></a>Simulazione dell'interruzione del servizio
toosimulate hello interruzione, è possibile eliminare o rinominare il database di origine hello. Ciò causa un errore di connettività dell'applicazione.

#### <a name="recovery"></a>Ripristino
* Eseguire ripristino a livello geografico hello del database hello in un server diverso, come descritto [qui](sql-database-disaster-recovery.md).
* Modifica hello applicazione configurazione tooconnect toohello ripristinato del database e seguire hello [configurare un database dopo il ripristino](sql-database-disaster-recovery.md) ripristino hello toocomplete della Guida.

#### <a name="validation"></a>Convalida
* Hello completo drill verificando il ripristino post integrità applicazione hello (incluse le stringhe di connessione, gli account di accesso, il test delle funzionalità di base o altra parte le convalide delle procedure conclusioni standard dell'applicazione).

## <a name="geo-replication"></a>Replica geografica
Per un database che è protetta tramite drill di replica geografica hello esercizio prevede toohello il failover pianificato del database secondario. Hello failover pianificato assicura che hello primario e i database secondari hello rimangano sincronizzati quando il cambio di ruolo hello. A differenza di hello failover non pianificato, questa operazione non produce una perdita di dati, in modo drill hello possono essere eseguite nell'ambiente di produzione hello.

#### <a name="outage-simulation"></a>Simulazione dell'interruzione del servizio
interruzione di hello toosimulate, è possibile disabilitare l'applicazione web hello o macchina virtuale connessa toohello database. Di conseguenza gli errori di connettività hello per i client web hello.

#### <a name="recovery"></a>Ripristino
* Assicurarsi che configurazione dell'applicazione hello in hello ripristino di emergenza area punti toohello ex secondario che diventa hello accessibile completamente nuovo database primario.
* Eseguire [failover pianificato](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) un nuovo database primario del database secondario hello toomake
* Seguire hello [configurare un database dopo il ripristino](sql-database-disaster-recovery.md) ripristino hello toocomplete della Guida.

#### <a name="validation"></a>Convalida
* Hello completo drill verificando il ripristino post integrità applicazione hello (incluse le stringhe di connessione, gli account di accesso, il test delle funzionalità di base o altra parte le convalide delle procedure conclusioni standard dell'applicazione).

## <a name="next-steps"></a>Passaggi successivi
* toolearn sugli scenari di continuità aziendale, vedere [gli scenari di continuità](sql-database-business-continuity.md)
* toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md)
* toolearn sull'utilizzo di backup automatico per il ripristino, vedere [ripristinare un database dai backup avviate dal servizio hello](sql-database-recovery-using-backups.md)
* toolearn sulle opzioni di ripristino più veloce, vedere [replica geografica attiva](sql-database-geo-replication-overview.md)  
