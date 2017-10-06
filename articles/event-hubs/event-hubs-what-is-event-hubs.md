---
title: "aaaWhat è l'hub eventi di Azure e perché usarlo | Documenti Microsoft"
description: Panoramica e introduzione tooAzure hub eventi - inserimento di dati di telemetria a livello di Cloud di siti Web, applicazioni e dispositivi
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>Che cos'è Hub eventi?

Hub eventi di Azure è una piattaforma di streaming di dati estremamente scalabile e un servizio di inserimento degli eventi che consente di ricevere ed elaborare milioni di eventi al secondo. Hub eventi consente di elaborare e archiviare eventi, dati o dati di telemetria generati dal software distribuito e dai dispositivi. I dati inviati tooan hub di eventi possono essere trasformati e memorizzati tramite qualsiasi provider analitica in tempo reale o schede dell'invio in batch o dell'archiviazione. Con hello possibilità tooprovide [funzionalità di pubblicazione-sottoscrizione](https://msdn.microsoft.com/library/aa560414.aspx) con una latenza bassa e su larga scala, hub eventi funge da hello "on"Preparazione per Big Data.

## <a name="why-use-event-hubs"></a>Vantaggi dell'uso di Hub eventi

Gli eventi e le funzionalità di gestione della telemetria di Hub eventi sono particolarmente utili per:

* Strumentazione dell'applicazione
* Esperienza dell'utente o l'elaborazione del flusso di lavoro
* Scenari Internet of Things (IoT)

Hub eventi consente, ad esempio, il rilevamento del comportamento nelle app per dispositivi mobili, il traffico di informazioni da Web farm, l'acquisizione di eventi nei giochi per console e la raccolta di dati di telemetria da computer industriali, veicoli connessi o altri dispositivi.

## <a name="azure-event-hubs-overview"></a>Panoramica di Hub eventi di Azure

comune ruolo dell'hub eventi nell'architettura delle soluzioni Hello è hello "porta di ingresso" per una pipeline di eventi, chiamato un *inserimento eventi*. Strumento di inserimento di un evento è un componente o servizio che si trova tra i Publisher di eventi e di evento consumer toodecouple hello produzione di un flusso di eventi dal consumo hello di tali eventi. Hello nella figura seguente viene illustrata questa architettura:

![Hub eventi](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Hub eventi offre funzionalità di gestione del flusso di messaggi, ma presenta caratteristiche diverse da quelle dei servizi di messaggistica aziendale tradizionale. Le funzionalità di Hub eventi sono basate su scenari con velocità effettiva elevata ed elaborazione di eventi. Di conseguenza, hub eventi è diverso da [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaggistica e non implementa alcune delle funzionalità disponibili per hello [messaggistica del Bus di servizio](/azure/service-bus-messaging/) entità, ad esempio argomenti.

## <a name="event-hubs-features"></a>Funzionalità di Hub eventi

Hub eventi contiene hello seguenti elementi chiave:

- [**Produttori/i Publisher di eventi**](event-hubs-features.md#event-publishers): un'entità che invia l'hub di eventi tooan di dati. Un evento viene pubblicato tramite AMQP 1.0 o HTTPS.
- [**Acquisire**](event-hubs-features.md#capture): permette di hub di eventi toocapture flusso di dati e archiviarlo in un account di archiviazione Blob di Azure.
- [**Partizioni**](event-hubs-features.md#partitions): Abilita tooonly ogni consumer di leggere un sottoinsieme specifico o una partizione, di hello flusso di eventi.
- [**Token SAS**](event-hubs-features.md#sas-tokens): identifica e autentica publisher di eventi hello.
- [**Consumer eventi**](event-hubs-features.md#event-consumers): qualsiasi entità che legge i dati dell'evento da un hub eventi. I consumer eventi si connettono tramite AMQP 1.0. 
- [**Gruppi di consumer**](event-hubs-features.md#consumer-groups): fornisce ogni più utilizzo applicazione con una visualizzazione distinta del flusso di eventi hello, abilitare tali tooact consumer in modo indipendente.
- [**Unità elaborate**](event-hubs-features.md#capacity): unità di capacità pre-acquistate. Una singola partizione ha una scalabilità massima di 1 unità elaborata.

Per informazioni tecniche dettagliate su queste e altre funzionalità di hub eventi, vedere hello [panoramica delle caratteristiche degli hub di eventi](event-hubs-features.md). 

## <a name="next-steps"></a>Passaggi successivi

Per informazioni dettagliate sui prezzi di Hub eventi, vedere [Hub eventi Prezzi](https://azure.microsoft.com/pricing/details/event-hubs/).

Per ulteriori informazioni sugli hub di eventi, visitare hello seguenti collegamenti:

* Iniziare con un'[esercitazione di Hub eventi](event-hubs-dotnet-standard-getstarted-send.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)
* [Applicazioni di esempio che usano Hub eventi](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

