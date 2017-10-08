---
title: evento aaaReal-tempo di elaborazione con l'elaborazione degli eventi di flusso Analitica | Documenti Microsoft
description: "Informazioni su come un set di servizi di Azure è in grado di interagire per consentire l’elaborazione e l’analisi in tempo reale degli eventi."
keywords: elaborazione in tempo reale, elaborazione di eventi, architettura di riferimento
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Architettura di riferimento: elaborazione di eventi in tempo reale con Analisi di flusso di Microsoft Azure
architettura di riferimento per l'elaborazione con Azure Analitica di flusso di eventi in tempo reale di Hello è previsto tooprovide generico linee guida per la distribuzione di una piattaforma in tempo reale come una soluzione di elaborazione del flusso di servizio (PaaS) con Microsoft Azure.

## <a name="summary"></a>Riepilogo
Tradizionalmente, soluzioni analitica sono basate sulle funzionalità, ad esempio ETL (extract, transform, load) e data warehouse, in cui i dati sono stored tooanalysis precedente. Modifica di requisiti, inclusi i dati più rapidamente in arrivo sono push questo limite di toohello modello esistente. anche se non è una nuova funzionalità, approccio hello non è stato ampiamente adottato nei tutti i settori verticali Hello possibilità tooanalyze dati mobile toostorage precedente di flussi sono una soluzione. 

Microsoft Azure fornisce un catalogo esteso di tecnologie di analisi in grado di supportare una matrice di scenari di soluzioni e requisiti diversi. Selezione toodeploy quali servizi di Azure per una soluzione end-to-end può rappresentare un problema dato breadth hello delle offerte. In questo documento è progettato toodescribe hello funzionalità e l'interoperabilità di hello vari servizi di Azure che supportano una soluzione flusso di eventi. Vengono inoltre illustrati alcuni degli scenari di hello in cui i clienti possono trarre vantaggio da questo tipo di approccio.

## <a name="contents"></a>Sommario
* Sunto
* Introduzione tooReal fase Analitica
* Proposta di valore dei dati in tempo reale in Azure
* Scenari comuni per l’analisi in tempo reale
* Architettura e componenti
  * Origini dati
  * Livello di integrazione dei dati
  * Livello di analisi in tempo reale
  * Livello di archiviazione dei dati
  * Livello presentazione / consumo
* Conclusioni

**Autore:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation

**Pubblicato:** gennaio 2015

**Revisione:** 1.0

**Download:** [Elaborazione di eventi in tempo reale con Analisi dei flussi di Microsoft Azure](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

