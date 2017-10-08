---
title: un ambiente di Azure ora serie Insights tooyour origine evento aaaAdd | Documenti Microsoft
description: In questa esercitazione, si connette un ambiente di tempo serie Insights tooyour origine evento
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Creare un'origine evento per l'ambiente di tempo serie Insights utilizzando portale Ibiza hello

Un'origine evento di Time Series Insights deriva da un gestore eventi, ad esempio Hub eventi di Azure. Tempo serie Insights si connette direttamente origini tooEvent, l'inserimento di flusso di dati hello senza richiedere agli utenti toowrite una singola riga di codice. Time Series Insights supporta attualmente gli hub eventi di Azure e gli hub IoT di Azure. In futuro hello, verranno aggiunte altre origini di eventi.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Passaggi tooadd un ambiente di tooyour origine evento

1.  Accedi toohello [portale Ibiza](https://portal.azure.com).
2.  Fare clic su "Tutte le risorse" nel menu hello sul lato sinistro di hello del portale Ibiza hello.
3.  Selezionare l'ambiente Time Series Insights.

  ![Creare origine evento di hello ora serie Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  Selezionare "Origini evento" e fare clic su "+ Aggiungi".

  ![Creare origine evento di Insights serie ora hello - dettagli](media/add-event-source/getstarted-create-event-source-2.png)

5.  Specificare il nome di hello dell'origine evento hello. Questo nome viene associato a tutti gli eventi provenienti dall'origine evento ed è disponibile in fase di query.
6.  Selezionare un hub eventi hello elenco di risorse Hub eventi nella sottoscrizione corrente hello. In caso contrario scegliere l'opzione di importazione "le impostazioni dell'Hub di eventi di fornire manualmente" toospecify un hub di eventi in un'altra sottoscrizione. Gli eventi devono essere pubblicati in formato JSON.
7.  Selezionare i criteri che dispone dell'autorizzazione in hub eventi hello lettura.
8.  Specificare il gruppo di consumer dell'hub eventi.

  > [!IMPORTANT]
  > Verificare che questo gruppo di consumer non venga usato da altri servizi, ad esempio un processo di Analisi di flusso o un altro ambiente Time Series Insights. Se il gruppo di consumer viene utilizzato da altri servizi, leggere influisce negativamente l'operazione per questo ambiente e hello altri servizi. Se si utilizza "$Default" come gruppo di consumer hello, può causare il riutilizzo toopotential dagli altri reader.

9.  Fare clic su "Crea".

Dopo la creazione dell'origine evento hello, ora serie Insights verrà automaticamente avviato il flusso di dati nel proprio ambiente.

## <a name="next-steps"></a>Passaggi successivi

* [Invio di eventi](time-series-insights-send-events.md) origine evento toohello
* Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)
