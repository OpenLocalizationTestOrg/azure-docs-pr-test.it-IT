---
title: API di tabelle del database di aaaIntroduction tooAzure Cosmos | Documenti Microsoft
description: Informazioni su come utilizzare Azure Cosmos DB toostore e grandi volumi di query di dati per valori di chiave con bassa latenza hello diffusi OSS MongoDB APIs.
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Introduzione tooAzure DB Cosmos: API di tabella

[Azure Cosmos DB](introduction.md) è il servizio di database multimodello distribuito a livello globale di Microsoft per applicazioni cruciali. DB Cosmos Azure fornisce [distribuzione globale di chiavi in mano](distribute-data-globally.md), [scalabilità elastica di velocità effettiva e l'archiviazione](partition-data.md) latenze millisecondo in tutto il mondo, a una cifra a percentile 99th hello, [cinque livelli di coerenza ben definiti](consistency-levels.md)e garantisce la disponibilità elevata, tutti i backup da [SLA leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB Cosmos [automaticamente i dati di indici](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) senza toodeal con la gestione dello schema e indice. Si tratta di un database multimodello che supporta modelli di dati di documenti, coppie chiave-valore, grafi e colonne. 

![API di archiviazione tabelle di Azure e Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

DB Cosmos Azure fornisce hello tabella API (anteprima) per applicazioni che richiedono un archivio chiave-valore con una velocità effettiva elevata, prestazioni prevedibili, distribuzione globale e schema flessibile. Hello tabella API fornisce hello stessa funzionalità di archiviazione tabelle di Azure, ma sfrutta i vantaggi hello hello Azure Cosmos del motore di database. 

È possibile continuare toouse archiviazione tabelle di Azure per le tabelle con archiviazione elevate e minori requisiti di velocità effettiva. Azure DB Cosmos introduce anche il supporto per le tabelle con ottimizzazione per la memoria in un aggiornamento futuro ed esistenti e nuove tabelle di Azure, gli account di archiviazione saranno aggiornati tooAzure DB Cosmos.

## <a name="premium-and-standard-table-apis"></a>API di tabella Premium e Standard
Se si utilizza archiviazione tabelle di Azure, si otterranno i seguenti vantaggi tramite lo spostamento di anteprima di "tabella premium" tooAzure Cosmos DB hello:

|  | Archiviazione tabelle di Azure | Azure Cosmos DB: archiviazione tabelle (anteprima) |
| --- | --- | --- |
| Latency | Veloce, senza limiti superiori per la latenza | Latenza cifra millisecondi per le letture e scritture, supportato da < latenza di 10 ms legge e < 15 ms Latenza scrive in percentile 99th hello, la scala, in qualsiasi punto della HelloWorld |
| Velocità effettiva | Altamente scalabile, ma senza modello di velocità effettiva dedicato. Le tabelle hanno un limite di scalabilità di 20.000 operazioni al secondo | Altamente scalabile con [velocità effettiva riservata dedicata per tabella](request-units.md), supportata da contratti di servizio. Non esiste un limite superiore di velocità effettiva per gli account, che supportano oltre 10 milioni di operazioni al secondo per tabella |
| Distribuzione globale | Singola area con un'area di lettura secondaria leggibile facoltativa per la disponibilità elevata. Non è possibile avviare il failover | [Distribuzione globale di chiavi in mano](distribute-data-globally.md) da uno too30 + aree, supporto per [failover manuale e automatico](regional-failover.md) in qualsiasi momento, ovunque nel mondo di hello |
| Indicizzazione | Solo indice primario in PartitionKey e RowKey. Nessun indice secondario | Indicizzazione automatica e completa su tutte le proprietà, nessuna gestione degli indici |
| Query | L'esecuzione di query usa l'indice per la chiave primaria ed esegue l'analisi negli altri casi. | Le query possono trarre vantaggio dall'indicizzazione automatica sulle proprietà, per query con durata ridotta. Il motore di database di Azure Cosmos DB è in grado di supportare aggregazioni, ricerca geospaziale e ordinamento. |
| Coerenza | Elevata nell'area primaria, possibile con un'area secondaria | [Cinque livelli di coerenza ben definiti](consistency-levels.md) tootrade off disponibilità, latenza, velocità effettiva e la coerenza in base alle esigenze dell'applicazione |
| Prezzi | Ottimizzati per l'archiviazione  | Ottimizzati per la velocità effettiva |
| Contratti di servizio | Disponibilità del 99,9% | disponibilità del 99,99% all'interno di una singola area e possibilità tooadd altre aree per una maggiore disponibilità. [Contratti di servizio completi leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/) che regolano la disponibilità generale |

## <a name="how-tooget-started"></a>La modalità di avvio tooget

Creare un account Azure Cosmos DB hello [portale di Azure](https://portal.azure.com)e iniziare a utilizzare il nostro [avvio rapido per l'API di tabella usando .NET](create-table-dotnet.md). 

## <a name="next-steps"></a>Passaggi successivi

Ecco alcuni puntatori tooget, che è stato avviato:
* [Compilare un'applicazione .NET usando hello tabella API](create-table-dotnet.md)
* [Sviluppo con hello tabella API in .NET](tutorial-develop-table-dotnet.md)
* [Dati della tabella query utilizzando hello tabella API](tutorial-query-table.md)
* [La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello tabella API](tutorial-global-distribution-table.md)
* [Azure Cosmos DB Table API SDK per .NET](table-sdk-dotnet.md)
