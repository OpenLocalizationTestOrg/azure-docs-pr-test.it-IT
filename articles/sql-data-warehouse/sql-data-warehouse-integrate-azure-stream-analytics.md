---
title: aaaUse Analitica di flusso di Azure con SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per l'uso di Analisi di flusso di Azure con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Usare Analisi di flusso di Azure con SQL Data Warehouse
Analitica di flusso di Azure è un servizio completamente gestito che fornisce l'elaborazione a bassa latenza, elevata disponibilità e scalabile di eventi complessi nel flusso di dati nel cloud hello. È possibile nozioni di base hello leggendo [tooAzure introduzione Analitica flusso][Introduction tooAzure Stream Analytics]. Sarà possibile apprendere come una soluzione end-to-end con flusso Analitica seguendo toocreate hello [iniziare a usare Azure flusso Analitica] [ Get started using Azure Stream Analytics] esercitazione.

In questo articolo si apprenderà come toouse database Azure SQL Data Warehouse come sink di output per i processi di flusso Analitica.

## <a name="prerequisites"></a>Prerequisiti
In primo luogo, eseguire i passaggi hello hello [iniziare a usare Azure flusso Analitica] [ Get started using Azure Stream Analytics] esercitazione.  

1. Creare un input dell'hub eventi
2. Configurare e avviare l'applicazione di generazione di eventi
3. Eseguire il provisioning di un processo di Analisi dei flussi
4. Specificare la query e l'input del processo

Creare quindi un database di Azure SQL Data Warehouse

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Specificare l'output del processo: database di Azure SQL Warehouse
### <a name="step-1"></a>Passaggio 1
Selezionare il processo di flusso Analitica **OUTPUT** dall'alto hello della pagina hello e quindi fare clic su **Aggiungi OUTPUT**.

### <a name="step-2"></a>Passaggio 2
Selezionare il Database SQL e fare clic su Avanti.

![][add-output]

### <a name="step-3"></a>Passaggio 3
Immettere i seguenti valori nella pagina successiva hello hello:

* *Alias di output*: immettere un nome descrittivo per l'output del processo.
* *Sottoscrizione*
  * Se il database di SQL Data Warehouse è in hello stessa sottoscrizione come processo di flusso Analitica hello, selezionare Usa Database SQL dalla sottoscrizione corrente.
  * Se il database è in una sottoscrizione diversa, selezionare Usare il database SQL da un'altra sottoscrizione.
* *Database*: specificare il nome di hello di un database di destinazione.
* *Nome del server*: specificare il nome di server hello per database hello è stato specificato. È possibile utilizzare hello portale di Azure classico toofind questo.

![][server-name]

* *Nome utente*: specificare il nome utente hello di un account che disponga di autorizzazioni di scrittura per il database di hello.
* *Password*: specificare la password di hello per hello l'account utente specificato.
* *Tabella*: specificare il nome di hello della tabella di destinazione hello nel database di hello.

![][add-database]

### <a name="step-4"></a>Passaggio 4
Fare clic su hello controllo pulsante tooadd l'output del processo e tooverify Analitica di flusso che può connettersi toohello database.

![][test-connection]

Quando il database di toohello hello connessione ha esito positivo, si vedrà una notifica nella parte inferiore di hello del portale hello. È possibile fare clic su Verifica connessione nel database di hello inferiore tootest hello connessione toohello.

## <a name="next-steps"></a>Passaggi successivi
Per una panoramica dell'integrazione, vedere [Panoramica dell'integrazione di SQL Data Warehouse][SQL Data Warehouse integration overview].

Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
