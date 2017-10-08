---
title: un ambiente Azure ora serie Insights aaaCreate | Documenti Microsoft
description: "In questa esercitazione si apprenderà come toocreate ambiente serie, connetterlo origine evento tooan e pronto tooanalyze i dati degli eventi in pochi minuti."
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Creare un nuovo ambiente di tempo serie Insights in hello portale di Azure

L'ambiente Time Series Insights è una risorsa di Azure con capacità di inserimento e archiviazione. I clienti di effettuare il provisioning ambienti tramite hello portale di Azure con capacità di hello necessario.

## <a name="steps-toocreate-hello-environment"></a>Ambiente di hello toocreate passaggi

Seguire questi passaggi toocreate l'ambiente:

1.  Accedi toohello [portale di Azure](https://portal.azure.com).
2.  Fare clic su hello sul segno più ("+") hello nell'angolo superiore sinistro.
3.  Cercare "Approfondite serie ora" nella casella di ricerca hello.

  ![Creare hello ora serie Insights ambiente](media/get-started/getstarted-create-environment1.png)

4.  Selezionare "Time Series Insights" e fare clic su "Crea".

  ![Crea gruppo di risorse Insights serie ora hello](media/get-started/getstarted-create-environment2.png)

5.  Specificare il nome dell'ambiente. Questo nome rappresenta ambiente hello in [explorer serie tempo](https://insights.timeseries.azure.com).
6.  Selezionare una sottoscrizione. Sceglierne una contenente l'origine evento. Tempo serie Insights può rilevare automaticamente IoT Hub di Azure e hello di risorse Hub eventi esistente nella stessa sottoscrizione.
7.  Selezionare o creare un gruppo di risorse. Un gruppo di risorse è una raccolta di risorse di Azure usate insieme.
8.  Selezionare un percorso di hosting. tooavoid lo spostamento dei dati tra data center, scegliere la posizione che contiene l'origine evento.
9.  Selezione di un piano tariffario.
10. Selezionare la capacità. È possibile modificare la capacità di un ambiente dopo la creazione.
11. Creare l'ambiente. È anche possibile aggiungere il dashboard di toohello di ambiente per facilitare l'accesso ogni volta che accedi.

  ![Creare hello ora serie Insights pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Passaggi successivi

* [Definire i criteri di accesso dati](time-series-insights-data-access.md) tooaccess l'ambiente in [ora serie Insights portale](https://insights.timeseries.azure.com)
* [Creare un'origine evento](time-series-insights-add-event-source.md)
* [Invio di eventi](time-series-insights-send-events.md) origine evento toohello
