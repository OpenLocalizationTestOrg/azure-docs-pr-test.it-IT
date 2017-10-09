---
title: aaaHow tooadd un ambiente di Azure ora serie Insights IoT Hub evento origine tooyour | Documenti Microsoft
description: "Questa esercitazione sono trattati come tooadd un evento di origine che è connesso tooan ambiente ora serie Insights tooyour di IoT Hub"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>Come tooadd un'origine evento IoT Hub

Questa esercitazione sono trattati come toouse hello tooadd portale Azure un'origine evento che legge da un ambiente di tempo serie Insights tooyour IoT Hub.

## <a name="prerequisites"></a>Prerequisiti

Sono stati creati un IoT Hub e scrive gli eventi tooit. Per altre informazioni sugli hub IoT, vedere <https://azure.microsoft.com/services/iot-hub/>

> [Gruppi di consumer] Ogni origine di eventi tempo serie Insights deve toohave il proprio gruppo di consumer dedicato che non viene condiviso con qualsiasi altro utente. Se più lettori utilizzano gli eventi da hello nello stesso gruppo di consumer, tutti i visualizzatori sono probabilmente toosee errori. Per informazioni dettagliate, vedere hello [Guida per sviluppatori di IoT Hub](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Scegliere un'opzione di importazione

le impostazioni di Hello per origine evento hello possono essere immesse manualmente o un hub IoT può essere selezionato da hello IoT hub tooyou disponibili.
In hello **opzione di importazione** selettore, scegliere una delle seguenti opzioni hello:

* Specificare le impostazioni dell'hub IoT manualmente
* Usare un hub IoT delle sottoscrizioni disponibili

### <a name="select-an-available-iot-hub"></a>Selezionare un hub IoT disponibile

Hello seguente tabella viene descritta ciascuna opzione nella scheda nuova origine evento hello con la relativa descrizione quando si seleziona un IoT Hub disponibile come un'origine evento:

| Nome proprietà | DESCRIZIONE |
| --- | --- |
| Nome origine evento | nome Hello dell'origine evento. Questo nome deve essere univoco all'interno dell'ambiente Time Series Insights.
| Sorgente | Scegliere **IoT Hub** toocreate un'origine evento IoT Hub.
| ID sottoscrizione | Selezionare una sottoscrizione di hello in cui è stato creato l'hub IoT.
| Nome dell'hub IoT | Selezionare il nome di hello di hello IoT Hub.
| Nome criterio dell'hub IoT | Selezionare i criteri di accesso condiviso hello sono reperibile nella scheda Impostazioni IoT Hub hello. Tutti i criteri di accesso condiviso dispongono di un nome e di autorizzazioni impostati, nonché di chiavi di accesso. Hello condiviso criteri di accesso per l'origine evento *deve* hanno **servizio connettersi** autorizzazioni.
| Gruppo di consumer dell'hub IoT | Hello gruppo di Consumer tooread eventi di hello IoT Hub. È altamente consigliabile toouse un gruppo di consumer dedicato per l'origine evento.

### <a name="provide-iot-hub-settings-manually"></a>Specificare le impostazioni dell'hub IoT manualmente

Hello nella tabella seguente illustra ogni proprietà nella scheda nuova origine evento hello con la relativa descrizione quando si immettono le impostazioni manualmente:

| Nome proprietà | DESCRIZIONE |
| --- | --- |
| Nome origine evento | nome Hello dell'origine evento. Questo nome deve essere univoco all'interno dell'ambiente Time Series Insights.
| Sorgente | Scegliere **IoT Hub** toocreate un'origine evento IoT Hub.
| ID sottoscrizione | sottoscrizione di Hello in cui è stato creato l'hub IoT.
| Gruppo di risorse | sottoscrizione di Hello in cui è stato creato l'hub IoT.
| Nome dell'hub IoT | nome Hello dell'IoT Hub. Quando l'hub IoT è stato creato gli è stato anche assegnato un nome specifico
| Nome criterio dell'hub IoT | criteri di accesso condiviso Hello, che possono essere creati nella scheda Impostazioni IoT Hub hello. Tutti i criteri di accesso condiviso dispongono di un nome e di autorizzazioni impostati, nonché di chiavi di accesso. Hello condiviso criteri di accesso per l'origine evento *deve* hanno **servizio connettersi** autorizzazioni.
| Chiave criteri hub IoT | chiave di accesso condiviso Hello usata tooauthenticate accesso toohello Bus di servizio spazio dei nomi. Tipo hello chiave primaria o secondaria qui.
| Gruppo di consumer dell'hub IoT | Hello gruppo di Consumer tooread eventi di hello IoT Hub. È altamente consigliabile toouse un gruppo di consumer dedicato per l'origine evento.

## <a name="next-steps"></a>Passaggi successivi

1. Aggiungere un ambiente di tooyour criteri di accesso ai dati [dati definire criteri di accesso](time-series-insights-data-access.md)
1. L'ambiente in hello accedere [ora serie Insights portale](https://insights.timeseries.azure.com)
