---
title: aaaOverview di Azure ora serie Insights | Documenti Microsoft
description: Introduzione tooAzure Insight serie ora, un nuovo servizio per analitica dei dati di ora serie e le soluzioni IoT
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>Informazioni su Azure Time Series Insights

Azure Insights serie di tempo è un servizio cloud gestita con componenti di archiviazione, analitica e visualizzazione che rendono facilmente tooingest, archiviare, esplorare e analizzare contemporaneamente anche su miliardi di eventi. Time Series Insights offre una visualizzazione globale dei dati e permette di convalidare rapidamente le soluzioni IoT ed evitare costosi tempi di inattività per i dispositivi, semplificando l'individuazione di tendenze nascoste e anomalie e l'esecuzione di analisi delle cause radice in tempo quasi reale. Tempo serie Insights inserisce i dati della serie temporale da gestori eventi (ad esempio gli hub IoT o hub eventi), dati hello di indici e Ritira i dati in base ai criteri di memorizzazione configurabile. Gli utenti di utilizzare dati hello tramite un'intuitiva UX o API REST di Query.

![Panoramica di Time Series Insights](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Scenari principali

* Monitorare e convalidare le soluzioni IoT in pochi minuti.
* Visualizzare e analizzare dati IoT su larga scala.
* Accelerare l'analisi della causa radice e del rilevamento anomalie.
* Creare una visualizzazione globale di più dispositivi, stabilimenti e dati.

## <a name="capabilities-and-benefits"></a>Funzionalità e vantaggi

* **Facile tooget avviato**: Azure ora serie Insights non richiede alcuna preparazione iniziale dei dati ed è molto veloci. Connettere toobillions di eventi nell'IoT Hub di Azure o Hub eventi in minuti. Una volta connessi, visualizzare e interagire con i dati del sensore in secondi tooquickly convalidare le soluzioni IoT. Approfondimenti serie ora è facile toouse; è possibile interagire con i dati senza scrivere una singola riga di codice.  Non vi è alcuna nuova toolearn linguaggio; Tempo serie Insights fornisce una superficie query granulare e testo libero per gli utenti esperti e quindi l'esplorazione per tutti.

* **In prossimità di informazioni in tempo reale**: Insights serie ora in grado di acquisire centinaia di milioni di eventi sensore al giorno, con una latenza di un minuto, in modo da poter reagire toochanges rapidamente. Time Series Insights consente di ottenere informazioni dettagliate sui dati dei sensori permettendo di trovare rapidamente tendenze e anomalie e di eseguire analisi complesse della causa radice evitando i costi dovuti ai tempi di inattività. Abilitando cross-correlazione tra i dati in tempo reale e cronologici, ora serie Insights consente di sbloccare nascoste le tendenze nei dati hello.

* **Compilare soluzioni personalizzate**: è possibile incorporare i dati di Azure Time Series Insights nelle applicazioni esistenti o creare nuove soluzioni personalizzate con le API REST di Time Series Insights. Creazione e la condivisione personalizzate visualizzazioni che è possibile condividere ad altri utenti tooexplore le individuazioni.

* **Scalabilità**: tempo serie Insights è progettato toosupport IoT su larga scala. In anteprima, è possibile in ingresso da too100 milioni di 1 milione di eventi al giorno, con un periodo di memorizzazione predefinito span di 31 giorni. È possibile visualizzare e analizzare i flussi dei dati attivi in tempo quasi reale, oltre a grandi quantità di dati cronologici. Procedendo, velocità in ingresso e conservazione aumenterà tooaccommodate scala enterprise in continua evoluzione.

## <a name="time-series-insights-glossary"></a>Glossario di Time Series Insights

* **Ambiente**: un ambiente è una risorsa di Azure con capacità di inserimento e archiviazione.  I clienti di effettuare il provisioning ambienti tramite hello portale di Azure con la capacità necessaria.
* **Origine evento**: un'origine evento deriva da un gestore eventi, ad esempio Hub eventi di Azure.  Tempo serie Insights si connette direttamente tooEvent origini, l'inserimento di flusso di dati hello senza scrivere alcun codice. Time Series Insights supporta attualmente gli hub eventi di Azure e gli hub IoT di Azure.
* **Dati di riferimento**: Insights serie ora offre agli utenti hello possibilità toojoin dati della serie temporale con dati di riferimento.  I dati di riferimento possono includere i metadati sui dispositivi o altri dati statici che vengono modificati raramente. Tempo serie Insights unisce i dati di riferimento di hello con flussi di dati, consentendo agli utenti toovisualize e analizzare i dati in tempo quasi reale.
