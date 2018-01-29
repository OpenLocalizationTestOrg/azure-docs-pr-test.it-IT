---
title: Monitoraggio in Database di Azure per MySQL | Microsoft Docs
description: Questo articolo illustra le metriche di monitoraggio e avviso per Database di Azure per MySQL, che includono statistiche relative a CPU, limiti, archiviazione e connessioni.
services: mysql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 10/24/2017
ms.openlocfilehash: 9af447d54faa8ee96e4b79beb274b437eea57626
ms.sourcegitcommit: b979d446ccbe0224109f71b3948d6235eb04a967
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2017
---
# <a name="monitoring-in-azure-database-for-mysql"></a>Monitoraggio in Database di Azure per MySQL
Il monitoraggio dei dati relativi ai server facilita la risoluzione dei problemi e l'ottimizzazione per il carico di lavoro. Database di Azure per MySQL offre varie metriche che consentono di ottenere informazioni approfondite sul comportamento delle risorse che supportano il server MySQL. 

## <a name="metrics"></a>Metrica
Tutte le metriche di Azure hanno una frequenza di un minuto e offrono una cronologia di 30 giorni. 

È possibile configurare avvisi in base alle metriche. Per indicazioni dettagliate, vedere l'articolo su come [configurare gli avvisi](howto-alert-on-metric.md). 

Le altre attività includono la configurazione di azioni automatiche, l'esecuzione di analisi avanzate e l'archiviazione della cronologia. Per altre informazioni, vedere [Panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

### <a name="list-of-metrics"></a>Elenco delle metriche
Per Database di Azure per MySQL sono disponibili le metriche seguenti:

|Metrica|Nome visualizzato per la metrica|Unità|Descrizione|
|---|---|---|---|---|
|cpu_percent|Percentuale CPU|Percentuale|Percentuale di CPU in uso.|
|compute_limit|Limite unità di calcolo|Numero|Numero massimo di unità di calcolo del server.|
|compute_consumption_percent|Compute Unit percentage (Percentuale unità di calcolo)|Percentuale|Percentuale di unità di calcolo usata rispetto al massimo del server.|
|memory_percent|Percentuale memoria|Percentuale|Percentuale di memoria in uso.|
|io_consumption_percent|IO percent (Percentuale IO)|Percentuale|Percentuale di I/O in uso.|
|storage_percent|Percentuale archiviazione|Percentuale|Percentuale di spazio di archiviazione usata rispetto al massimo del server.|
|storage_used|Uso archiviazione|Byte|Quantità di spazio di archiviazione in uso. Lo spazio di archiviazione usato dal servizio include file di database, log delle transazioni e log del server.|
|storage_limit|Limite archiviazione|Byte|Spazio di archiviazione massimo per il server.|
|active_connections|Total active connections (Numero totale di connessioni attive)|Numero|Numero di connessioni al server attive.|
|connections_failed|Total failed connections (Numero totale di connessioni non riuscite)|Numero|Numero di connessioni al server non riuscite.|


> [!NOTE]
> Un'unità di calcolo è costituita da memoria e CPU. La percentuale delle unità di calcolo è data da max(memory%, cpu%). Esaminare i grafici relativi a memoria e CPU per individuare quale dei due elementi contribuisce alle modifiche nella percentuale delle unità di calcolo. Per altre informazioni, vedere l'articolo relativo alle [unità di calcolo](concepts-compute-unit-and-storage.md).

## <a name="next-steps"></a>Passaggi successivi
- Per indicazioni dettagliate, vedere l'articolo su come [configurare gli avvisi](howto-alert-on-metric.md). 
- Per altre informazioni sull'accesso alle metriche e la relativa esportazione con il portale di Azure, l'API REST o l'interfaccia della riga di comando, vedere [Panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).
