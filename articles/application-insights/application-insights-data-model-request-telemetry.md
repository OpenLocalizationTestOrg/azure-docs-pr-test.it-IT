---
title: aaaAzure modello dati di telemetria Insights di applicazione - richiesta di dati di telemetria | Documenti Microsoft
description: Modello di dati di Application Insights per la telemetria delle richieste
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>Telemetria delle richieste: modello di dati di Application Insights

Un elemento di dati di telemetria richiesta (in [Application Insights](app-insights-overview.md)) rappresenta hello sequenza logica di esecuzione generato da un'applicazione tooyour richiesta esterna. Ogni esecuzione della richiesta è identificato da univoco `ID` e `url` contenente tutti i parametri di esecuzione hello. È possibile raggruppare le richieste da logica `name` e definire hello `source` della richiesta. L'esecuzione del codice può restituire un campo `success` o `fail` e ha un campo `duration` specificato. Le esecuzioni con esito positivo e negativo possono essere ulteriormente raggruppate in base a `resultCode`. Ora di inizio per telemetria richiesta hello definito a livello di busta hello.

Richiesta di dati di telemetria supporta il modello di estendibilità standard hello utilizzando personalizzata `properties` e `measurements`.

## <a name="name"></a>Nome

Nome della richiesta di hello rappresenta richiesta hello tooprocess percorso del codice. Tooallow valore di cardinalità bassa meglio il raggruppamento delle richieste. Per le richieste HTTP rappresenta hello metodo HTTP e modello del percorso dell'URL come `GET /values/{id}` senza hello effettivo `id` valore.

Web di Application Insights SDK Invia nome richiesta "così com'è" con relativamente tooletter case. Raggruppamento sull'interfaccia utente è distinzione maiuscole/minuscole in modo `GET /Home/Index` viene conteggiata separatamente da `GET /home/INDEX` anche se spesso comportano hello stessa esecuzione azione e del controller. Hello motivo è che gli URL vengono in genere [tra maiuscole e minuscole](http://www.w3.org/TR/WD-html40-970708/htmlweb.html). È consigliabile toosee tutti `404` si sono verificate per gli URL hello digitati in maiuscolo. È possibile leggere ulteriori su richiesta nome raccolta da ASP.Net Web SDK in hello [post di blog](http://apmtips.com/blog/2015/02/23/request-name-and-url/).

Lunghezza massima: 1024 caratteri

## <a name="id"></a>ID

Identificatore dell'istanza di una chiamata di richiesta. Usato per la correlazione tra richiesta e altri elementi di telemetria. L'ID deve essere globalmente univoco. Per altre informazioni vedere la pagina relativa alla [correlazione](application-insights-correlation.md).

Lunghezza massima: 128 caratteri

## <a name="url"></a>Url

URL della richiesta con tutti i parametri di stringa di query.

Lunghezza massima: 2048 caratteri

## <a name="source"></a>Sorgente

Origine della richiesta di hello. Esempi sono la chiave di strumentazione hello del chiamante hello o l'indirizzo ip hello del chiamante hello. Per altre informazioni vedere la pagina relativa alla [correlazione](application-insights-correlation.md).

Lunghezza massima: 1024 caratteri

## <a name="duration"></a>Durata

Durata della richiesta in formato: `DD.HH:MM:SS.MMMMMM`. Deve essere un valore positivo e inferiore a `1000` giorni. Questo campo è obbligatorio, come dati di telemetria richiesta rappresenta l'operazione di hello con hello inizio e alla fine di hello.

## <a name="response-code"></a>Codice della risposta

Risultato dell'esecuzione di una richiesta. Codice di stato HTTP per le richieste HTTP. Potrebbe essere un valore `HRESULT` o un tipo di eccezione per altri tipi di richiesta.

Lunghezza massima: 1024 caratteri

## <a name="success"></a>Success

Indicazione di chiamata con esito positivo o con esito negativo. Questo campo è obbligatorio. Se non impostato in modo esplicito troppo`false` -considerata riuscita toobe richiesta. Impostare questo valore troppo`false` se l'operazione è stata interrotta da eccezione o ha restituito il codice di errore risultato.

Per le applicazioni web hello Application Insights definire richiesta come non riuscita durante il codice di risposta hello è meno hello `400` o troppo uguale`401`. Tuttavia vi sono casi quando questo mapping predefinito non corrisponde ad hello semantica dell'applicazione hello. Il codice di risposta `404` può indicare "Nessun record" e quindi fare parte del normale flusso. Può indicare anche un collegamento interrotto. Per hello collegamenti interrotti, è anche possibile implementare la logica più avanzata. È possibile contrassegnare i collegamenti interrotti come errori solo se tali collegamenti si trovano nello stesso sito analizzando referrer url hello. O contrassegnarli come errori quando si accede da applicazione per dispositivi mobili della società hello. Allo stesso modo `301` e `302` indica un errore quando si accede da client hello che non supporta il reindirizzamento.

Il codice `206` di contenuto parzialmente accettato può indicare un errore di una richiesta globale. L'endpoint di Application Insights riceve, ad esempio, un batch di elementi di telemetria come una singola richiesta. Restituisce `206` quando alcuni elementi in batch hello non sono stati elaborati correttamente. Velocità di incremento di `206` indica un problema che deve toobe analizzato. Una logica simile si applica troppo`207` più stati in cui potrebbe essere successo hello hello peggiore dei codici di risposta separato.

È possibile leggere ulteriori risultato della richiesta nel codice e codice di stato in hello [post di blog](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).

## <a name="custom-properties"></a>Proprietà personalizzate

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Misure personalizzate

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Passaggi successivi

- [Scrivere dati di telemetria della richiesta personalizzata](app-insights-api-custom-events-metrics.md#trackrequest)
- Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).
- Informazioni su come troppo[configurare ASP.NET Core](app-insights-asp-net.md) un'applicazione con Application Insights.
- Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.
