---
title: aaaPricing & fatturazione - App Azure per la logica | Documenti Microsoft
description: Informazioni sul funzionamento dei prezzi e della fatturazione per App per la logica di Azure.
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Modello di determinazione prezzi delle app per la logica
Azure App per la logica consente tooscale ed eseguire flussi di lavoro di integrazione nel cloud hello.  Di seguito sono informazioni dettagliate sulla fatturazione e i piani tariffari per App per la logica di hello.
## <a name="consumption-pricing"></a>Prezzi a consumo
Le nuove app per la logica create usano un piano a consumo. Con modello tariffario consumo logica App hello, si paga solo per ciò che si utilizza.  In caso di piano a consumo, le app per la logica non sono soggette a limitazione.
Viene misurato il consumo per tutte le azioni eseguite durante un'esecuzione di un'istanza dell'app per la logica.
### <a name="what-are-action-executions"></a>Informazioni sulle esecuzioni di azioni
Ogni passaggio in una definizione di applicazione logica è un'azione, che include i trigger, i passaggi del flusso di controllo come condizioni, gli ambiti, cicli for each, fino a quando i cicli, chiama tooconnectors e chiamate di azioni toonative.
I trigger sono azioni speciali che vengono progettati tooinstantiate una nuova istanza di un'app di logica quando si verifica un evento specifico.  Esistono numerosi comportamenti diversi per i trigger, che possono influire sulla modalità è a consumo hello logica app.
* **Polling trigger** -trigger esegue continuamente il polling di un endpoint finché riceve un messaggio che soddisfa i criteri di hello per la creazione di un'istanza di un'app di logica.  è possibile configurare l'intervallo di polling Hello in trigger hello in Progettazione applicazione logica hello.  Ogni richiesta di poll, anche se non determina la creazione di un'istanza di un'app per la logica, viene conteggiata come esecuzione di azione.
* **Trigger Webhook** -il trigger è in attesa di un toosend client è una richiesta su un particolare endpoint.  Ogni richiesta inviata toohello webhook endpoint viene considerato come un'esecuzione dell'azione. Richiesta di Hello e hello trigger HTTP Webhook sono entrambi trigger webhook.
* **Trigger di ricorrenza** -trigger crea un'istanza di applicazione logica hello in base a intervallo di ricorrenza hello configurata nel trigger hello.  Ad esempio, un trigger di ricorrenza può essere configurato toorun ogni tre giorni o persino ogni minuto.

Esecuzioni dei trigger possono essere visualizzate nel pannello della risorsa App per la logica hello in hello parte della cronologia di Trigger.

Per tutte le azioni eseguite, riuscite o non riuscite, viene misurato il consumo come esecuzione di un'azione.  Azioni che sono state ignorate a causa di tooa condizione non viene raggiunto o che non è stata eseguita perché hello logica app terminato prima del completamento non vengono conteggiati come esecuzioni di azione.

Azioni eseguite all'interno di cicli vengono conteggiate per ogni iterazione del ciclo di hello.  Ad esempio, un'unica azione in un ciclo for each lo scorrimento di un elenco di 10 elementi vengono conteggiati come numero hello di elementi nell'elenco di hello (10) moltiplicato per il numero di hello di azioni nel ciclo hello (1) più uno per avvio hello del ciclo di hello , che, in questo esempio, sarebbe (10 * 1) + 1 = 11 esecuzioni di azione.
Per le app per la logica disabilitate non possono essere create nuove istanze. Di conseguenza, mentre sono disabilitate, non viene effettuato alcun addebito.  Tenere presente che dopo la disabilitazione di un'app logica potrebbe richiedere un po' di tempo per hello istanze tooquiesce prima completamente disabilitata.
### <a name="integration-account-usage"></a>Utilizzo dell'account di integrazione
Inclusi nell'utilizzo in base al consumo è un [account integrazione](logic-apps-enterprise-integration-create-integration-account.md) per l'esplorazione e sviluppo a scopo di test consentono di hello toouse [B2B/EDI](logic-apps-enterprise-integration-b2b.md) e [elaborazione XML](logic-apps-enterprise-integration-xml.md)funzionalità delle app di logica senza alcun costo aggiuntivo. Sono in grado di toocreate un massimo di un account per ogni area e archiviare backup too10 contratti e le 25 mappe. Non sono previsti limiti per schemi, certificati e partner ed è possibile caricare tutti quelli necessari.

Inoltre toohello inclusione degli account di integrazione con il consumo, si possono inoltre creare integration standard account con il contratto di servizio di App logica standard e senza questi limiti. Per altre informazioni, vedere la pagina relativa ai [prezzi di Azure](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="app-service-plans"></a>Piani di servizio app
App per la logica creata in precedenza che fanno riferimento a un piano di servizio App continua toobehave come prima. In base al piano hello scelto, vengono limitati dopo hello prescritte esecuzioni giornaliere vengono superate, ma vengono fatturate usando misuratore di esecuzione azione hello.
I clienti EA che dispongono di un piano di servizio App nella propria sottoscrizione, il quale non è associato in modo esplicito hello logica App toobe, ottiene il vantaggio di quantità hello incluso.  Ad esempio, se si dispone di un piano di servizio App Standard sottoscrizione EA e dell'applicazione una logica di hello stessa sottoscrizione quindi che non sono addebitata per 10.000 esecuzioni di azione al giorno (vedere la seguente tabella). 

Piani di servizio app ed esecuzioni di azioni giornaliere consentite:
|  | Gratuito/Condiviso/Basic | Standard | Premium |
| --- | --- | --- | --- |
| Esecuzioni di azioni al giorno |200 |10.000 |50.000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>Convertire dal piano di servizio App prezzi tooConsumption
un'applicazione di logica che dispone di un servizio App piano associato toochange modello consumo tooa, Rimuovi hello riferimento toohello piano di servizio App nella definizione di App per la logica di hello.  Questa modifica può essere eseguita con un cmdlet di PowerShell tooa chiamata:`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>Prezzi
Per informazioni sui prezzi, vedere [Prezzi di App per la logica](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="next-steps"></a>Passaggi successivi
* [Informazioni su App per la logica][whatis]
* [Creare la prima app per la logica][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

