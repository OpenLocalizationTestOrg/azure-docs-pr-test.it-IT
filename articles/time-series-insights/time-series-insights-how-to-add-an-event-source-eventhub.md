---
title: aaaHow tooadd un ambiente di Azure ora serie Insights Hub eventi evento origine tooyour | Documenti Microsoft
description: Questa esercitazione sono trattati come un evento tooadd origine tooan connesso Hub eventi tooyour ora serie Insights ambiente
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
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>Come tooadd un'origine evento Hub eventi

Questa esercitazione sono trattati come toouse hello tooadd portale Azure un'origine evento che legge da un ambiente di tempo serie Insights tooyour Hub eventi.

## <a name="prerequisites"></a>Prerequisiti

Sono stati creati un Hub eventi e scrive gli eventi tooit. Per altre informazioni sugli hub eventi, vedere <https://azure.microsoft.com/services/event-hubs/>

> [Gruppi di consumer] Ogni origine di eventi tempo serie Insights deve toohave il proprio gruppo di consumer dedicato che non viene condiviso con qualsiasi altro utente. Se più lettori utilizzano gli eventi da hello nello stesso gruppo di consumer, tutti i visualizzatori sono probabilmente toosee errori. Si noti che è presente anche un limite di 20 gruppi di utenti per Hub eventi. Per informazioni dettagliate, vedere hello [Guida per programmatori hub eventi](../event-hubs/event-hubs-programming-guide.md).

## <a name="choose-an-import-option"></a>Scegliere un'opzione di importazione

le impostazioni di Hello per origine evento hello possono essere immesse manualmente o un hub di eventi può essere selezionato da hub di eventi hello che sono disponibili tooyou.
In hello **opzione di importazione** selettore, scegliere una delle seguenti opzioni hello:

* Specificare le impostazioni dell'hub eventi manualmente
* Usare un hub eventi dalle sottoscrizioni disponibili

### <a name="select-an-available-event-hub"></a>Selezionare un hub eventi disponibile

Hello nella tabella seguente illustra ciascuna opzione nella scheda nuova origine evento hello con la relativa descrizione quando si seleziona un Hub di eventi disponibili come un'origine evento:

| Nome proprietà | DESCRIZIONE |
| --- | --- |
| Nome origine evento | nome Hello dell'origine evento. Questo nome deve essere univoco all'interno dell'ambiente Time Series Insights.
| Sorgente | Scegliere **Hub eventi** toocreate un'origine evento Hub eventi.
| ID sottoscrizione | Selezionare una sottoscrizione di hello in cui è stato creato l'hub eventi.
| Spazio dei nomi del bus di servizio | Selezionare lo spazio dei nomi Service Bus hello contiene hello Hub eventi.
| Nome hub eventi | Selezionare il nome di hello di hello Hub eventi.
| Nome criteri hub eventi | Selezionare i criteri di accesso condiviso hello, che possono essere creati nella scheda Configura dell'Hub eventi hello. Tutti i criteri di accesso condiviso dispongono di un nome e di autorizzazioni impostati, nonché di chiavi di accesso. Hello condiviso criteri di accesso per l'origine evento *deve* hanno **leggere** autorizzazioni.
| Gruppo di consumer dell'hub eventi | Hello gruppo di Consumer tooread eventi di hello Hub eventi. È altamente consigliabile toouse un gruppo di consumer dedicato per l'origine evento.

### <a name="provide-event-hub-settings-manually"></a>Specificare le impostazioni dell'hub eventi manualmente

Hello nella tabella seguente illustra ogni proprietà nella scheda nuova origine evento hello con la relativa descrizione quando si immettono le impostazioni manualmente:

| Nome proprietà | DESCRIZIONE |
| --- | --- |
| Nome origine evento | nome Hello dell'origine evento. Questo nome deve essere univoco all'interno dell'ambiente Time Series Insights.
| Sorgente | Scegliere **Hub eventi** toocreate un'origine evento Hub eventi.
| ID sottoscrizione | sottoscrizione di Hello in cui è stato creato l'hub eventi.
| Gruppo di risorse | sottoscrizione di Hello in cui è stato creato l'hub eventi.
| Spazio dei nomi del bus di servizio | Uno spazio dei nomi Service Bus è un contenitore per un set di entità di messaggistica. Quando si crea un nuovo Hub eventi, viene inoltre creato uno spazio dei nomi Service Bus.
| Nome hub eventi | nome Hello dell'Hub di eventi. Quando è stato creato l'hub eventi gli è stato assegnato anche un nome specifico
| Nome criteri hub eventi | criteri di accesso condiviso Hello, che possono essere creati nella scheda Configura dell'Hub eventi hello. Tutti i criteri di accesso condiviso dispongono di un nome e di autorizzazioni impostati, nonché di chiavi di accesso. Hello condiviso criteri di accesso per l'origine evento *deve* hanno **leggere** autorizzazioni.
| Chiave criteri hub eventi | chiave di accesso condiviso Hello usata tooauthenticate accesso toohello Bus di servizio spazio dei nomi. Tipo hello chiave primaria o secondaria qui.
| Gruppo di consumer dell'hub eventi | Hello gruppo di Consumer tooread eventi di hello Hub eventi. È altamente consigliabile toouse un gruppo di consumer dedicato per l'origine evento.

## <a name="next-steps"></a>Passaggi successivi

1. Aggiungere un ambiente di tooyour criteri di accesso ai dati [dati definire criteri di accesso](time-series-insights-data-access.md)
1. L'ambiente in hello accedere [ora serie Insights portale](https://insights.timeseries.azure.com)
