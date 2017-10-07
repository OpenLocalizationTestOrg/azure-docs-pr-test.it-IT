---
title: aaaAzure Premium Bus di servizio e di messaggistica Standard prezzo livelli Panoramica | Documenti Microsoft
description: Livelli di messaggistica Standard e Premium del bus di servizio
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Livelli di messaggistica Standard e Premium del bus di servizio

La messaggistica del bus di servizio, che include entità come code e argomenti, unisce funzionalità di messaggistica aziendale a una semantica di pubblicazione-sottoscrizione completa a livello di cloud. Messaggistica del Bus di servizio viene utilizzata come backbone comunicazione hello per molte soluzioni di cloud sofisticate.

Hello *Premium* livello di messaggistica del Bus di servizio risolve le richieste dei clienti comuni attorno alla scala, prestazioni e disponibilità per applicazioni di importanza strategica. Anche se il set di funzionalità hello è quasi identico, questi due livelli di messaggistica del Bus di servizio sono progettate tooserve diversi casi d'uso.

Alcune differenze di alto livello vengono evidenziati in hello nella tabella seguente.

| Premium | Standard |
| --- | --- |
| Velocità effettiva elevata |Velocità effettiva variabile |
| Prestazioni prevedibili |Latenza variabile |
| Prezzi fissi |Prezzi variabili in base all'uso |
| Carico di lavoro di possibilità tooscale su e giù |N/D |
| Dimensione del messaggio di too1 MB |Dimensione del messaggio too256 KB |

**Messaggistica Premium del Bus di servizio** fornisce l'isolamento delle risorse a livello di CPU e memoria hello in modo che ogni carico di lavoro del cliente viene eseguita in isolamento. Questo contenitore di risorse viene chiamato *unità di messaggistica*. Ad ogni spazio dei nomi Premium viene allocata almeno un'unità di messaggistica. È possibile acquistare 1, 2 o 4 unità di messaggistica per ogni spazio dei nomi Premium del bus di servizio. Un singolo carico di lavoro o un'entità può estendersi su più unità di messaggistica e il numero di hello di unità di messaggistica può essere cambiato quando è necessario, anche se la fatturazione è previsto un addebito frequenza di 24 ore oppure ogni giorno. il risultato di Hello è prestazioni prevedibili e ripetibile per la soluzione basata sul Bus di servizio.

Non solo le prestazioni sono più prevedibili e disponibili, ma anche più veloci. Messaggistica Premium del Bus di servizio si basa sul motore di archiviazione hello introdotta in [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/). Con la messaggistica Premium, sono molto più veloce con il livello Standard hello ottenere prestazioni ottimali.

## <a name="premium-messaging-technical-differences"></a>Differenze tecniche della messaggistica Premium

Hello nelle sezioni seguenti vengono illustrano alcune differenze tra i livelli di messaggistica Standard e Premium.

### <a name="partitioned-queues-and-topics"></a>Code e argomenti partizionati

Le code e gli argomenti partizionati sono supportati nella messaggistica Premium. Queste entità sono in effetti sempre partizionate e non possono essere disabilitate. Tuttavia, Premium partizionare code e argomenti non funzionano hello esattamente come in hello livelli Standard e Basic di messaggistica del Bus di servizio. Non messaggistica Premium Usa SQL come archivio dati e non ha hello concorrenza possibili risorsa associata a una piattaforma condivisa. Di conseguenza, il partizionamento non è necessario tooimprove prestazioni. Inoltre, il numero di partizioni hello è stato modificato da 16 partizioni nella messaggistica Standard partizioni too2 Premium. Con due partizioni garantisce la disponibilità e un numero più appropriato per l'ambiente di runtime di hello Premium. 

Con la messaggistica Premium, quando si specificano dimensioni hello di un'entità con [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), che le dimensioni sono suddiviso equamente tra partizioni hello 2, a differenza di [Standard partizionata entità](service-bus-partitioning.md#standard) in cui hello dimensione totale è 16 volte hello dimensioni specificate. 

Per altre informazioni sul partizionamento, vedere [Code e argomenti partizionati](service-bus-partitioning.md).

### <a name="express-entities"></a>Entità Express

Dato che la messaggistica Premium viene eseguita in un ambiente di runtime completamente isolato, le entità Express non sono supportate negli spazi dei nomi Premium. Per ulteriori informazioni sulla funzionalità express hello, vedere hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) proprietà.

Se si dispone di codice in esecuzione con tooport Standard di messaggistica e si desidera il livello Premium toohello, assicurarsi che hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) impostata troppo**false** (valore predefinito di hello).

## <a name="get-started-with-premium-messaging"></a>Introduzione alla messaggistica Premium

Introduzione a messaggistica Premium è molto semplice e il processo di hello toothat simile di messaggistica Standard. Iniziare [creando uno spazio dei nomi](service-bus-create-namespace-portal.md). Assicurarsi di selezionare **Premium** in **Piano tariffario**.

![create-premium-namespace][create-premium-namespace]

È anche possibile creare [spazi dei nomi Premium usando i modelli di Azure Resource Manager](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).


## <a name="next-steps"></a>Passaggi successivi

toolearn più sulla messaggistica del Bus di servizio, vedere hello seguenti argomenti.

* [Introducing Azure Service Bus Premium Messaging](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/) (Introduzione alla messaggistica Premium del bus di servizio di Azure, post di blog)
* [Introducing Azure Service Bus Premium Messaging](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging) (Introduzione alla messaggistica Premium del bus di servizio di Azure, Channel9)
* [Panoramica della messaggistica del bus di servizio](service-bus-messaging-overview.md)
* [Come le code del Bus di servizio toouse](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
