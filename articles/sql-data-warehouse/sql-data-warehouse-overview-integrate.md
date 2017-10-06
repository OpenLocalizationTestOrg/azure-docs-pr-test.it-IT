---
title: soluzioni aaaBuild integrate con SQL Data Warehouse | Documenti Microsoft
description: 'Strumenti e partner con soluzioni che interagiscono con SQL Data Warehouse. '
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Utilizzare altri servizi con SQL Data Warehouse
Inoltre tooits principali funzionalità, SQL Data Warehouse consente agli utenti tooleverage molti hello altri servizi in Azure visualizzato.  Nello specifico, abbiamo adottato attualmente toodeeply integrarlo seguente hello passaggi:

* Power BI
* Data factory di Azure
* Azure Machine Learning
* Analisi di flusso di Azure

Stiamo tooconnect con più servizi hello ecosistema di Azure.

## <a name="power-bi"></a>Power BI
Integrazione di Power BI permette di potenza di calcolo di hello tooleverage di SQL Data Warehouse con reporting dinamico hello e visualizzazione di Power BI. L’integrazione di Power BI include attualmente:

* **Connessione diretta**: una connessione più avanzata con caratteristiche logiche SQL Data Warehouse.  Questo fornisce un'analisi veloce su vasta scala.
* **Apri in Power BI**: pulsante 'Apri in Power BI' hello passa tooPower informazioni istanza BI, consentendo una connessione più semplice.

Vedere [integrazione con Power BI](sql-data-warehouse-integrate-power-bi.md) o hello [documentazione di Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) per ulteriori informazioni.

## <a name="azure-data-factory"></a>Data factory di Azure
Data Factory di Azure offre agli utenti un toocreate piattaforma gestita che Extract-Load complessi delle pipeline.  Integrazione di SQL Data Warehouse con Data Factory di Azure include seguente hello:

* **Stored procedure**: orchestrare esecuzione hello di stored procedure in SQL Data Warehouse.
* **Copia**: dati di utilizzo ADF toomove in SQL Data Warehouse.  Questa operazione è possibile utilizzare meccanismo di spostamento dei dati standard del file ADF o copre PolyBase in hello. 

Vedere [integrazione con Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) o hello [documentazione di Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) per ulteriori informazioni.

## <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning è un servizio analitica completamente gestito che consente agli utenti i modelli più complessi toocreate sfruttando un ampio set di strumenti di previsione.  SQL Data Warehouse è supportato come un'origine e di destinazione per questi modelli con hello seguenti funzionalità:

* **Lettura dati:** Guida i modelli su larga scala mediante T-SQL su SQL Data Warehouse.
* **Scrittura di dati:** il Commit delle modifiche da qualsiasi modello di eseguire il backup tooSQL Data Warehouse.

Vedere [integrazione con Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) o hello [documentazione di Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) per ulteriori informazioni.

## <a name="azure-stream-analytics"></a>Analisi di flusso di Azure
L’Analisi dei flussi di Azure è un'infrastruttura complessa, completamente gestita per l'elaborazione e l'utilizzo di dati degli eventi generati da Hub eventi di Azure.  Integrazione con SQL Data Warehouse consente la trasmissione toobe dati elaborati in modo efficace e archiviato insieme ai dati relazionali, consentendo più approfondita, più avanzate di analisi.  

* **Output del processo:** Analitica di flusso di output invia i processi direttamente tooSQL Data Warehouse.

Vedere [integrazione con Azure flusso Analitica](sql-data-warehouse-integrate-azure-stream-analytics.md) o hello [documentazione di Azure flusso Analitica](https://azure.microsoft.com/documentation/services/stream-analytics/) per ulteriori informazioni.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
