---
title: aaaService Bus con .NET e AMQP 1.0 | Documenti Microsoft
description: Uso del bus di servizio di Azure da .NET con AMQP
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>Uso del bus di servizio da .NET con AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>Download hello Service Bus SDK

Supporto di AMQP 1.0 è disponibile in hello Service Bus SDK versione 2.1 o successiva. È possibile assicurarsi di avere la versione più recente di hello scaricando i bit del Bus di servizio hello [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>Configurazione .NET applicazioni toouse AMQP 1.0

Per impostazione predefinita, libreria client .NET di Service Bus di hello comunica con il servizio Bus di servizio utilizzando un protocollo dedicato basato su SOAP hello. toouse AMQP 1.0 anziché protocollo predefinito hello è necessaria una configurazione esplicita nella stringa di connessione del Bus di servizio hello, come descritto nella sezione successiva hello. A parte questa modifica, il codice dell'applicazione rimane invariato quando si usa AMQP 1.0.

Nella versione corrente di hello, esistono alcune funzionalità dell'API che non sono supportate quando si usa AMQP. Queste funzionalità non supportate sono elencate più avanti nella sezione hello [non supportato di funzionalità, restrizioni e differenze di comportamento](#unsupported-features-restrictions-and-behavioral-differences). Inoltre, alcune delle impostazioni di configurazione avanzata hello hanno un significato diverso quando si usa AMQP.

### <a name="configuration-using-appconfig"></a>Configurazione mediante App.config

È buona norma applicazioni toouse hello app. config file toostore le impostazioni di configurazione. Per le applicazioni di Service Bus, è possibile utilizzare una stringa di connessione di App. config toostore hello Bus di servizio. Ecco un file App.config di esempio:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

valore di hello Hello `Microsoft.ServiceBus.ConnectionString` impostazione è una stringa di connessione hello Bus di servizio che viene utilizzato tooconfigure hello connessione tooService Bus. formato hello è come segue:

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Dove `[namespace]` e `SharedAccessKey` vengono ottenuti dal hello [portale di Azure] [ Azure portal] quando si crea uno spazio dei nomi del Bus di servizio. Per ulteriori informazioni, vedere [creare uno spazio dei nomi del Bus di servizio utilizzando il portale di Azure hello][Create a Service Bus namespace using hello Azure portal].

Quando si usa AMQP, aggiungere la stringa di connessione hello con `;TransportType=Amqp`. Questa notazione indica hello client libreria toomake relativo tooService connessione Bus mediante AMQP 1.0.

## <a name="message-serialization"></a>Serializzazione dei messaggi

Quando si utilizza il protocollo di predefinito hello, comportamento di serializzazione predefinito hello della libreria client .NET di hello è hello toouse [DataContractSerializer] [ DataContractSerializer] digitare tooserialize un [BrokeredMessage ] [ BrokeredMessage] istanza per il trasporto tra la libreria client di hello e hello servizio service Bus. Quando si utilizza la modalità di trasporto AMQP hello, libreria di hello client utilizza il sistema di tipi AMQP hello per la serializzazione di hello [messaggio negoziato] [ BrokeredMessage] in un messaggio AMQP. Questa serializzazione permette hello messaggio toobe ricevuto e interpretato da un'applicazione ricevente potenzialmente in esecuzione su una piattaforma diversa, ad esempio, un'applicazione Java che utilizza hello API JMS tooaccess Bus di servizio.

Quando si creano un [BrokeredMessage] [ BrokeredMessage] istanza, è possibile fornire un oggetto .NET come tooserve di costruttore toohello un parametro come corpo hello del messaggio hello. Per gli oggetti che possono essere tipi primitivi tooAMQP mappato, corpo hello viene serializzato in tipi di dati AMQP. Se l'oggetto hello non può essere mappato direttamente in un tipo primitivo AMQP. ovvero, un tipo personalizzato definito dall'applicazione hello e oggetto hello viene serializzato utilizzando hello [DataContractSerializer][DataContractSerializer], e hello serializzato byte vengono inviati in un messaggio data AMQP.

toofacilitate interoperabilità con client non .NET, usare solo i tipi .NET che possono essere serializzati direttamente in tipi AMQP per il corpo del messaggio hello hello. Hello nella tabella seguente illustra in dettaglio i tipi e hello corrispondente mapping toohello sistema di tipi AMQP.

| Tipo di oggetto del corpo .NET | Tipo AMQP mappato | Tipo di sezione del corpo AMQP |
| --- | --- | --- |
| bool |boolean |Valore AMQP |
| byte |ubyte |Valore AMQP |
| ushort |ushort |Valore AMQP |
| uint |uint |Valore AMQP |
| ulong |ulong |Valore AMQP |
| sbyte |byte |Valore AMQP |
| short |short |Valore AMQP |
| int |int |Valore AMQP |
| long |long |Valore AMQP |
| float |float |Valore AMQP |
| double |double |Valore AMQP |
| decimal |decimal128 |Valore AMQP |
| char |char |Valore AMQP |
| DateTime |timestamp |Valore AMQP |
| Guid |uuid |Valore AMQP |
| byte[] |binary |Valore AMQP |
| string |stringa |Valore AMQP |
| System.Collections.IList |list |Valore AMQP: gli elementi contenuti nella raccolta hello possono essere solo quelli definiti in questa tabella. |
| System.Array |array |Valore AMQP: gli elementi contenuti nella raccolta hello possono essere solo quelli definiti in questa tabella. |
| System.Collections.IDictionary |map |Valore AMQP: gli elementi contenuti nella raccolta hello possono essere solo quelli definiti in questa tabella. Nota: sono supportate solo le chiavi di stringa. |
| Uri |Stringa descritto (vedere hello nella tabella seguente) |Valore AMQP |
| Datetimeoffset |Tipo long descritto (vedere hello nella tabella seguente) |Valore AMQP |
| TimeSpan |Tipo long descritto (vedere l'esempio hello) |Valore AMQP |
| Flusso |binary |Dati AMQP (possono essere multipli). sezioni di dati Hello contengono hello byte non elaborati dall'oggetto flusso hello. |
| Altro oggetto |binary |Dati AMQP (possono essere multipli). Contiene file binario hello serializzata dell'oggetto hello che usa DataContractSerializer hello o un serializzatore fornito dall'applicazione hello. |

| Tipo di .NET | Tipo descritto AMQP mappato | Note |
| --- | --- | --- |
| Uri |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| Datetimeoffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Funzionalità non supportate, restrizioni e differenze di comportamento

Hello seguenti caratteristiche di hello API .NET del Bus di servizio non è attualmente supportata quando si usa AMQP:

* Transazioni
* Invio tramite destinazione del trasferimento

Esistono inoltre alcune piccole differenze di comportamento hello di hello API .NET del Bus di servizio quando si usa AMQP, protocollo predefinito toohello confrontati:

* Hello [OperationTimeout] [ OperationTimeout] proprietà viene ignorata.
* `MessageReceiver.Receive(TimeSpan.Zero)` viene implementato come `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Completamento di messaggi tramite il token di blocco solo scopo dei destinatari dei messaggi hello che inizialmente ha ricevuto messaggi hello.

## <a name="controlling-amqp-protocol-settings"></a>Controllo delle impostazioni del protocollo AMQP

Hello [API .NET](/dotnet/api/) esporre diverse impostazioni toocontrol hello il comportamento di hello protocollo AMQP:

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: controlli hello collegamento tooa credito iniziale applicato. valore predefinito di Hello è 0.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: dimensioni del fotogramma di controlli hello massima AMQP offerti durante la negoziazione di hello al momento dell'apertura di connessione. valore predefinito di Hello è 65.536 byte.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: se i trasferimenti batchable, questo valore determina il ritardo massimo di hello per le disposizioni di invio. Per impostazione predefinita, il valore viene ereditato dai mittenti/destinatari. Singolo mittente/destinatario può eseguire l'override predefinito hello, ovvero 20 millisecondi.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**: controlla se le connessioni AMQP vengono stabilite su una connessione SSL. valore predefinito di Hello è **true**.

## <a name="next-steps"></a>Passaggi successivi

Pronto più toolearn? Visitare hello seguenti collegamenti:

* [Panoramica di AMQP per il bus di servizio]
* [Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio]
* [AMQP nel bus di servizio per Windows Server]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Panoramica di AMQP per il bus di servizio]: service-bus-amqp-overview.md
[Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP nel bus di servizio per Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
