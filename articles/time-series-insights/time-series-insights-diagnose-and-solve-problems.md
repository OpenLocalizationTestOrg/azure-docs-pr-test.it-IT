---
title: aaaDiagnose e risolvere i problemi | Documenti Microsoft
description: Questa esercitazione sono trattati come toodiagnose e risolvere i problemi nell'ambiente di tempo serie Insights
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Diagnosticare e risolvere i problemi nell'ambiente Time Series Insights

## <a name="i-dont-see-my-data"></a>Non vengono visualizzati i dati
Ecco alcuni motivi per cui potrebbero non essere visibili i dati nell'ambiente in hello [portale Azure ora serie Insights](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>L'origine evento non dispone di dati in formato JSON
Azure Time Series Insights al momento supporta solo i dati in formato JSON. Per alcuni esempi di dati in formato JSON, vedere [Forme JSON supportate](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Quando l'origine evento è stato registrato, non è stato fornito chiave hello che dispone dell'autorizzazione necessaria hello
* Per un hub IoT, è necessario chiave hello tooprovide con **servizio connettersi** autorizzazione.

   ![Autorizzazione di connessione al servizio hub IoT](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Come mostrato nella precedente immagine, hello uno dei criteri di hello **iothubowner** e **servizio** funzionerà, perché entrambi hanno **servizio connettersi** autorizzazione.
* Per un hub di eventi, è necessario chiave hello tooprovide con **ascolto** autorizzazione.

   ![Autorizzazione di ascolto per l'hub eventi](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Come mostrato nella precedente immagine, hello uno dei criteri di hello **leggere** e **gestire** funzionerà, perché entrambi hanno **ascolto** autorizzazione.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Hello fornito gruppo di consumer non è esclusivo tooTime serie Insights
Per un hub IoT o un hub eventi, durante la registrazione è necessario per gruppo di consumer hello toospecify che deve essere utilizzato per la lettura dei dati. Questo gruppo di consumer non deve essere condiviso. Se viene condiviso, hub eventi sottostante hello disconnette automaticamente uno dei lettori di hello in modo casuale.

## <a name="i-see-my-data-but-theres-a-lag"></a>I dati vengono visualizzati, ma c'è un ritardo
Ecco i motivi perché si potrebbe vedere parziale dei dati nell'ambiente in hello [portale ora serie Insights](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>L'ambiente è in fase di limitazione
Hello limite viene applicato in base a tipo SKU e la capacità dell'ambiente hello. Tutte le origini di eventi nell'ambiente di hello condividono questa capacità. Se l'origine evento hello per l'evento o l'hub IoT sono push dei dati oltre i limiti di hello applicato, vedere la limitazione delle richieste e un ritardo.

Hello seguente diagramma mostra un ambiente di Insights di serie di tempo che dispone di una SKU di S1 e una capacità di 3. È consentito l'ingresso di 3 milioni di eventi al giorno.

![Capacità corrente dello SKU dell'ambiente](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Si supponga che questo ambiente è l'inserimento messaggi da un hub eventi con velocità in ingresso hello mostrato nel seguente diagramma hello:

![Velocità di ingresso di esempio per un hub eventi](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Come illustrato nel diagramma hello, frequenza in ingresso giornaliero hello è ~ 67,000 messaggi. Questa velocità si traduce approssimativamente messaggi too46 ogni minuto. Se ogni messaggio di hub eventi è bidimensionale tooa singolo evento di Insights di serie di tempo, questo ambiente non rileva Nessuna limitazione. Se ogni messaggio di evento hub eventi tempo serie Insights too100 bidimensionale, quindi 4.600 eventi devono essere caricamento ogni minuto. Un ambiente SKU S1 con una capacità pari a 3 consente l'ingresso di soli 2.100 eventi al minuto (1 milione di eventi al giorno = 700 eventi al minuto in 3 unità = 2.100 eventi al minuto). Di conseguenza viene visualizzato un intervallo di scadenza toothrottling. 

Per una descrizione generale di come funziona la logica di appiattimento, vedere [Forme JSON supportate](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Procedure consigliate
ritardo di hello toofix, hello aumento della capacità SKU dell'ambiente. Per ulteriori informazioni, vedere [come tooscale ambiente ora serie Insights](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>Il push dei dati cronologici sta causando lentezza nell'ingresso
Se ci si connette a un'origine evento esistente, è probabile che l'hub IoT o l'hub eventi contenga già dati. Avvio estrazione dei dati dall'inizio di hello del periodo di memorizzazione di messaggi dell'origine evento hello così hello dell'ambiente. 

Questo comportamento è il comportamento predefinito di hello e non può essere sottoposto a override. È possibile coinvolgere la limitazione delle richieste e potrebbe richiedere un po' di tempo toocatch backup sull'inserimento di dati cronologici.

#### <a name="recommended-steps"></a>Procedure consigliate
ritardo di hello toofix, hello take alla procedura seguente:
1. Aumentare hello SKU capacità toohello valore massimo consentito (10 in questo caso). Dopo aver hello viene aumentata, il processo di ingresso hello avvia recuperando molto più veloce. È possibile visualizzare rapidità con cui sta recuperando tramite grafico disponibilità hello in hello [portale ora serie Insights](https://insights.timeseries.azure.com). Vengono addebitati i hello maggiore capacità.
2. Dopo il ritardo di hello viene aggiornato, ridurre la frequenza in ingresso normale hello SKU capacità tooyour indietro.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>L'impostazione del *nome della proprietà Timestamp* dell'origine evento non funziona
Verificare che hello nome e valore siano conformi alle regole toohello:
* nome della proprietà timestamp Hello _tra maiuscole e minuscole_.
* valore della proprietà timestamp Hello provenienti dall'origine evento, come una stringa JSON, deve avere il formato di hello _AAAA-MM-ggTHH. FFFFFFFK_. Un esempio di tale stringa è "2008-04-12T12:53Z".
