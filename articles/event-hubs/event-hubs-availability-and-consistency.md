---
title: aaaAvailability e la coerenza in hub eventi di Azure | Documenti Microsoft
description: "La quantità massima di hello tooprovide di disponibilità e la coerenza con gli hub di eventi di Azure partizioni."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Disponibilità e coerenza nell'Hub eventi

## <a name="overview"></a>Panoramica
Azure hub eventi Usa un [partizionamento modello](event-hubs-features.md#partitions) tooimprove disponibilità e la parallelizzazione all'interno di un hub singolo evento. Ad esempio, un hub eventi include quattro partizioni, se uno di tali partizioni viene spostato da un server tooanother in un'operazione di bilanciamento del carico, possono comunque inviare e ricevere tre altre partizioni. Consente, inoltre, con più partizioni toohave simultanea di più lettori l'elaborazione dei dati, migliorare la velocità effettiva aggregata. Informazioni sulle implicazioni hello di partizionamento e l'ordinamento in un sistema distribuito è un aspetto di fondamentale importanza della progettazione della soluzione.

toohelp spiegare compromesso hello tra l'ordinamento e la disponibilità, vedere hello [teorema di CAP](https://en.wikipedia.org/wiki/CAP_theorem), noto anche come Teorema di Brewer. Questo teorema viene scelta hello tra la coerenza, disponibilità e tolleranza di partizione.

Il teorema di Brewer definisce coerenza e disponibilità come segue:
* Tolleranza di partizione: hello capacità di un toocontinue di sistema di elaborazione dei dati l'elaborazione dei dati, anche se si verifica un errore della partizione.
* Disponibilità: un nodo non di errore restituisce una risposta accettabile in un periodo ragionevole di tempo, senza errori o timeout.
* Coerenza: un'operazione di lettura è garantita la scrittura di più recente hello tooreturn per un determinato client.

## <a name="partition-tolerance"></a>Tolleranza di partizione
L'Hub eventi si basa su un modello di dati partizionato. È possibile configurare il numero di hello di partizioni nell'hub eventi durante l'installazione, ma non è possibile modificare questo valore in un secondo momento. Poiché è necessario utilizzare le partizioni con hub eventi, è necessario toomake una decisione sulla disponibilità e la coerenza dell'applicazione.

## <a name="availability"></a>Disponibilità
Hello tooget modo più semplice avviato con hub eventi è il comportamento predefinito di toouse hello. Se si crea un nuovo `EventHubClient` e utilizzare hello `Send` (metodo), gli eventi vengono automaticamente distribuiti tra partizioni nell'hub eventi. Questo comportamento, per la maggior quantità hello di tempo.

Per i casi di utilizzo che richiedono massime hello tempo di attività, questo modello è preferito.

## <a name="consistency"></a>Coerenza
In alcuni scenari, può essere importante hello ordinamento degli eventi. Ad esempio, si consiglia il tooprocess sistema back-end, un comando di aggiornamento prima di un comando di eliminazione. In questo caso, è possibile impostare la chiave di partizione hello un evento o utilizzare un `PartitionSender` tooonly oggetto inviare eventi tooa determinata partizione. In modo da garantire che, quando questi eventi vengono letti dalla partizione hello, in cui vengono letti nell'ordine.

Con questa configurazione, tenere presente che se hello partizione specifica toowhich che mittente non è disponibile, si riceverà una risposta di errore. Come un punto di confronto, se non si dispone di una partizione singola tooa di affinità, hello servizio hub eventi invia l'evento toohello partizione successiva formattata disponibile.

Una possibile soluzione tooensure, ordinamento, ottimizzando inoltre ora, sarebbe tooaggregate eventi durante l'applicazione di elaborazione di eventi. Hello questo tooaccomplish modo più semplice è toostamp l'evento con una proprietà con numero sequenza personalizzato. Hello di codice seguente viene illustrato un esempio:

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

In questo esempio invia l'evento tooone delle partizioni disponibili hello nell'hub eventi e imposta il numero di sequenza corrispondente hello dall'applicazione. Questa soluzione richiede toobe stato mantenuto dall'applicazione di elaborazione, ma consente i mittenti un endpoint che è più probabile toobe disponibili.

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica del servizio Hub eventi](event-hubs-what-is-event-hubs.md)
* [Creare un hub eventi](event-hubs-create.md)
