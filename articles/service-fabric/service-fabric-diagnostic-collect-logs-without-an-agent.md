---
title: aaaCollect log direttamente da un Azure Service Fabric processo del servizio | Microsoft Azure
description: Descrive le applicazioni possono inviare i log direttamente, come posizione centrale tooa Azure Application Insights o Elasticsearch, senza basarsi sull'agente di diagnostica di Azure di Service Fabric.
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Raccogliere log direttamente da un processo del servizio di Azure Service Fabric
## <a name="in-process-log-collection"></a>Raccolta di log nel processo
Applicazione di raccogliere i log di [l'estensione diagnostica Azure](service-fabric-diagnostics-how-to-setup-wad.md) è un'opzione valida per **Azure Service Fabric** servizi se set hello di log origini e destinazioni è ridotto, non cambiano spesso e non esiste rappresenta un mapping diretto tra origini hello e le destinazioni. In caso contrario, in alternativa, è toohave servizi inviano i log direttamente posizione centrale tooa. Questo processo è noto come **raccolta di log nel processo** e presenta diversi vantaggi potenziali:

* *Facilità di configurazione e distribuzione*

    * configurazione di Hello di raccolta dati di diagnostica è solo parte della configurazione del servizio hello. È facile tooalways keep "sincronizzato" con hello il resto dell'applicazione hello.
    * È facile ottenere la configurazione per ogni applicazione o servizio.
        * Raccolta di log basato su agenti richiede in genere una distribuzione separata e la configurazione dell'agente, diagnostica hello è un'attività amministrativa extra e una potenziale fonte di errori. Spesso è presente solo un'istanza dell'agente di hello consentito per ogni macchina virtuale (nodo) e la configurazione dell'agente hello viene condiviso tra tutte le applicazioni e servizi in esecuzione su tale nodo. 

* *Flessibilità*
   
    * un'applicazione Hello può inviare dati di hello ogni volta che è necessario toogo, purché vi è una libreria client che supporta il sistema di archiviazione dati hello di destinazione. È possibile aggiungere nuove destinazioni in base alle esigenze.
    * È possibile implementare complesse regole di acquisizione, filtro e aggregazione dati.
    * Raccolta di log basato su agenti è spesso limitata dalla sink dati hello che hello agente supporta. Alcuni agenti sono estendibili.

* *Contesto e accedere ai dati di applicazione toointernal*
   
    * sottosistema di diagnostica Hello in esecuzione nel processo di applicazioni o servizi hello possibile integrare facilmente le tracce di hello con informazioni contestuali.
    * Con la raccolta di log basato su agenti, hello devono essere inviati dati agente tooan tramite un meccanismo di comunicazione tra processi, ad esempio Event Tracing for Windows. Questo meccanismo può imporre limitazioni aggiuntive.

È possibile toocombine e trarre vantaggio da entrambi i metodi di raccolta. Infatti, potrebbe essere la soluzione migliore di hello per molte applicazioni. Basato su agenti di raccolta è una soluzione naturale per la raccolta dell'intero cluster toohello correlati registri e i singoli nodi del cluster. È molto più affidabile, rispetto alla raccolta di log in-process, problemi di avvio del servizio toodiagnose e arresti anomali del sistema. Con molti servizi in esecuzione all'interno di un cluster di Service Fabric, inoltre, ogni servizio esegue la propria raccolta di log in-process comporta molte connessioni in uscita dal cluster hello. È un numero elevato di connessioni in uscita sovraccarico per il sottosistema di rete hello e per la destinazione di log hello. Un agente come [**Diagnostica di Azure**](../cloud-services/cloud-services-dotnet-diagnostics.md) può raccogliere dati da più servizi e inviarli tutti tramite un numero limitato di connessioni, migliorando così la velocità effettiva. 

In questo articolo viene illustrata la modalità tooset di un processo nel log insieme utilizzando [ **libreria open source EventFlow**](https://github.com/Azure/diagnostics-eventflow). Altre librerie potrebbero essere utilizzate per hello stesso scopo, ma EventFlow ha il vantaggio di hello di che è stato progettato specificatamente per i servizi Service Fabric insieme e toosupport nel processo log. Utilizziamo [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) come destinazione di log hello. Sono supportate anche altre destinazioni, ad esempio [**Hub eventi**](https://azure.microsoft.com/services/event-hubs/) o [**Elasticsearch**](https://www.elastic.co/products/elasticsearch). È semplicemente una questione di installazione del pacchetto NuGet appropriato e la configurazione di destinazione hello nel file di configurazione EventFlow hello. Per altre informazioni sulle destinazioni di log diverse da Application Insights, vedere la [documentazione di EventFlow](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>Aggiunta di progetto di servizio Service Fabric tooa EventFlow libreria
I file binari di EventFlow sono disponibili come set di pacchetti NuGet. tooadd progetto del servizio Service Fabric tooa EventFlow, fare clic sul progetto in Esplora soluzioni hello hello e scegliere "Gestisci NuGet pacchetti". Cambia la scheda "Sfoglia" toohello e cercare "`Diagnostics.EventFlow`":

![Pacchetti NuGet di EventFlow nell'interfaccia utente di gestione pacchetti NuGet di Visual Studio][1]

servizio Hello hosting EventFlow deve includere pacchetti appropriati a seconda di hello origine e di destinazione per i log applicazioni hello. Aggiungere i seguenti pacchetti hello: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (toocapture dati dalla classe EventSource del servizio hello e da EventSources standard, ad esempio *ServiceFabric-Microsoft-Services* e *ServiceFabric-Microsoft-attori*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (si stabilirà una risorsa di Azure Application Insights tooan di toosend hello log)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (consente l'inizializzazione della pipeline EventFlow hello dalla configurazione del servizio Service Fabric e segnala eventuali problemi con l'invio di dati di diagnostica come report di integrità dell'infrastruttura di servizio)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`il pacchetto richiede hello servizio progetto tootarget .NET Framework 4.6 o versione successiva. Assicurarsi di impostare il framework di destinazione appropriata hello nelle proprietà del progetto prima di installare questo pacchetto. 

Dopo che tutti hello pacchetti installati, passaggio successivo hello è tooconfigure e abilitare EventFlow nel servizio hello.

## <a name="configuring-and-enabling-log-collection"></a>Configurazione e abilitazione della raccolta di log
Pipeline EventFlow, responsabile per l'invio di log di hello, viene creata da una specifica archiviata in un file di configurazione. Il pacchetto `Microsoft.Diagnostics.EventFlow.ServiceFabric` installa un file di configurazione di iniziale di EventFlow nella cartella `PackageRoot\Config` della soluzione. nome del file Hello è `eventFlowConfig.json`. Questo file di configurazione deve toobe modificato toocapture dati dal servizio predefinito hello `EventSource` classe e di servizio dati di Insights tooApplication di trasmissione.

> [!NOTE]
> Si presuppone che si ha familiarità con **Azure Application Insights** servizio e disporre di una risorsa di Application Insights pianificare toouse toomonitor il servizio Service Fabric. Per altre informazioni, vedere [Creare una risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md).

Aprire hello `eventFlowConfig.json` file nell'editor di hello e modifica il contenuto, come illustrato di seguito. Verificare che tooreplace hello ServiceEventSource nome e la chiave di strumentazione di Application Insights in base toocomments. 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> Hello ServiceEventSource del servizio è denominato valore hello hello proprietà Name di hello `EventSourceAttribute` toohello ServiceEventSource classe applicato. Tutto è specificato in hello `ServiceEventSource.cs` file, che fa parte del codice del servizio hello. Ad esempio, in hello seguente frammento di codice hello nome del codice hello ServiceEventSource è *MyCompany-Application1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Si noti che il file `eventFlowConfig.json` fa parte del pacchetto di configurazione del servizio. File toothis modifiche può essere inclusi in full o configurazione-solo gli aggiornamenti del servizio di hello, soggetto tooService aggiornamento controlli di integrità e il rollback automatico nel caso di errore di aggiornamento. Per altre informazioni, vedere [Aggiornamento delle applicazioni di Service Fabric](service-fabric-application-upgrade.md).

passaggio finale Hello è tooinstantiate EventFlow pipeline nel codice di avvio del servizio, si trova `Program.cs` file. In hello aggiunte correlati EventFlow di esempio seguenti sono contrassegnate con commenti a partire da `****`:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

il nome di Hello passato come parametro hello di hello `CreatePipeline` metodo hello `ServiceFabricDiagnosticsPipelineFactory` nome hello di hello *entità integrità* che rappresenta di pipeline di raccolta log EventFlow hello. Questo nome viene utilizzato se viene rilevato EventFlow e di errore e la segnala tramite hello del sottosistema di integrità di Service Fabric.

## <a name="verification"></a>Verifica
Avviare il servizio e osservare hello Debug la finestra di output in Visual Studio. Una volta avviato il servizio di hello, è consigliabile iniziare a visualizzare la prova che il servizio invia i record di "Telemetria di Application Insights". Aprire un web browser e passare la risorsa di Application Insights tooyour passare. Aprire la scheda "Ricerca" (nella parte superiore di hello del Pannello di hello predefinito "Overview"). Dopo un breve ritardo si dovrebbe iniziare a vedere le tracce nel portale Application Insights hello:

![Portale di Application Insights con i log da un'applicazione di Service Fabric][2]

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sulla diagnostica e il monitoraggio di un servizio di infrastruttura di servizi](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [Documentazione di EventFlow](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
