---
title: dati di diagnostica di Azure nel percorso di frequente hello tramite hub di eventi aaaStreaming | Documenti Microsoft
description: Configurazione della diagnostica Azure con gli hub di eventi di fine tooend, incluse indicazioni per gli scenari comuni.
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Flusso di dati di diagnostica di Azure nel percorso critico hello tramite gli hub di eventi
Diagnostica di Azure fornisce metodi flessibili toocollect metriche e i log da cloud services le macchine virtuali (VM) e trasferire risultati tooAzure archiviazione. A partire da hello marzo 2016 (2.9 SDK) di tempo, è possibile inviare diagnostica toocustom origini dati e trasferire i dati di percorso ricorrente in secondi tramite [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/).

Tipi di dati supportati:

* Tracciamento degli eventi di Windows (ETW)
* Contatori delle prestazioni
* Registri eventi di Windows
* Log applicazioni
* Log dell'infrastruttura Diagnostica di Azure

Questo articolo illustra come tooconfigure diagnostica di Azure con gli hub di eventi da terminare tooend. Vengono inoltre fornite istruzioni relative hello scenari comuni seguenti:

* Modalità di registrazione toocustomize hello e le metriche che vengano inviate tooEvent hub
* Come le configurazioni di toochange in ogni ambiente
* Hub di eventi tooview come flusso di dati
* Come tootroubleshoot hello connessione  

## <a name="prerequisites"></a>Prerequisiti
Dati dell'evento hub receieving da diagnostica di Azure sono supportati in servizi Cloud, macchine virtuali, il set di scalabilità di macchine virtuali e Service Fabric a partire da Azure SDK 2.9 hello e hello corrispondente di strumenti di Azure per Visual Studio.

* Estensione di Diagnostica Azure 1.6 ([SDK di Azure per .NET 2.9 o versione successiva](https://azure.microsoft.com/downloads/) ha questa destinazione per impostazione predefinita)
* [Visual Studio 2013 o versione successiva](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Le configurazioni esistenti di diagnostica di Azure in un'applicazione utilizzando un *wadcfgx* file e uno dei seguenti metodi hello:
  * Visual Studio: [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell: [Abilitare la diagnostica nei servizi Cloud di Azure tramite PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)
* Spazio dei nomi degli hub di eventi il provisioning per ogni articolo hello [Introduzione agli hub di eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>La connessione di diagnostica Azure tooEvent hub sink
Per impostazione predefinita, diagnostica Azure invia sempre i log e le metriche tooan account di archiviazione di Azure. Un'applicazione può inoltre inviare dati tooEvent hub aggiungendo un nuovo **sink** sezione hello **PublicConfig** / **WadCfg** elemento di hello *wadcfgx* file. In Visual Studio, hello *wadcfgx* file viene archiviato nel seguente percorso hello: **progetto servizio Cloud** > **ruoli** > **( RoleName)** > **wadcfgx** file.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

In questo esempio, hub eventi hello è impostato l'URL toohello completamente qualificato dello spazio dei nomi dell'hub eventi hello: spazio dei nomi di hub eventi + "/" + nome hub eventi.  

hub di eventi Hello URL viene visualizzato in hello [portale di Azure](http://go.microsoft.com/fwlink/?LinkID=213885) nel dashboard di hello hub eventi.  

Hello **Sink** nome può essere impostato tooany di stringa valida, purché hello stesso valore viene utilizzato in modo coerente in tutto il file di configurazione di hello.

> [!NOTE]
> In questa sezione potrebbero esserci altri sink configurati, come ad esempio *applicationInsights* . Diagnostica di Azure consente di specificare uno o più sink toobe definite se ogni sink viene dichiarato in hello **PrivateConfig** sezione.  
>
>

Hello hub eventi sink deve inoltre essere dichiarati e definiti in hello **PrivateConfig** sezione di hello *wadcfgx* file di configurazione.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

Hello `SharedAccessKeyName` valore deve corrispondere a una chiave di firma di accesso condiviso (SAS) e i criteri che sono stato definito in hello **hub eventi** dello spazio dei nomi. Esplorare il dashboard di hub eventi toohello in hello [portale di Azure](https://manage.windowsazure.com), fare clic su hello **configura** scheda e impostare un criterio denominato (ad esempio, "SendRule") che ha *inviare* autorizzazioni. Hello **StorageAccount** viene dichiarato **PrivateConfig**. Non è necessario toochange valori qui se sono coinvolti. In questo esempio, si lascia valori hello vuoto, ovvero un segno che un asset downstream verrà impostati valori hello. Ad esempio, hello *ServiceConfiguration* file di configurazione Ambiente Imposta nomi appropriati ambiente hello e le chiavi.  

> [!WARNING]
> chiave di firma di accesso condiviso hub eventi Hello viene archiviata in testo normale nel hello *wadcfgx* file. Spesso, questa chiave viene archiviata nel controllo del codice toosource o è disponibile come una risorsa nel server di compilazione, pertanto deve essere protetto come appropriato. È consigliabile usare una chiave SAS con *solo invio* autorizzazioni in modo che un utente malintenzionato può scrivere toohello hub eventi, ma non ascolto tooit o gestirlo.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Configurare diagnostica Azure toosend metriche e log tooEvent hub
Come descritto in precedenza, tutti i dati di diagnostica personalizzata e le impostazione predefinita, vale a dire, metriche e i log, viene inviato automaticamente tooAzure archiviazione intervalli hello configurato. Con gli hub di eventi e qualsiasi sink aggiuntive, è possibile specificare qualsiasi nodo radice o foglia in toobe gerarchia hello inviati toohello hub di eventi. Questi includono gli eventi ETW, i contatori delle prestazioni, i registri eventi di Windows e i registri dell'applicazione.   

È importante tooconsider quanti punti dati devono effettivamente essere trasferiti tooEvent hub. Di solito gli sviluppatori trasferiscono i dati del percorso critico a bassa latenza che devono essere utilizzati e interpretati rapidamente. I sistemi che monitorano gli avvisi o le regole di scalabilità automatica sono degli esempi. Uno sviluppatore può anche configurare un archivio di analisi o di ricerca alternativo; ad esempio, Analisi di flusso di Azure, ElasticSearch, un sistema di monitoraggio personalizzato o un sistema di monitoraggio preferito di terze parti.

Hello seguito sono riportate alcune configurazioni di esempio.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

In hello sopra riportato, sink hello è applicato toohello padre **PerformanceCounters** nodo nella gerarchia di hello, ovvero tutti elementi figlio **PerformanceCounters** verrà inviato tooEvent hub.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

Nell'esempio precedente hello sink hello è applicato tooonly tre contatori: **richieste in coda**, **richieste rifiutate**, e **% tempo processore**.  

Hello esempio seguente viene illustrato come uno sviluppatore può limitare quantità hello di dati inviato toobe hello metriche più importanti utilizzati per l'integrità del servizio.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

In questo esempio, il sink hello è toologs applicato ed è tooerror filtrato solo livello traccia.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Distribuire e aggiornare un'applicazione dei servizi cloud e della configurazione della diagnostica
Visual Studio fornisce più semplice percorso toodeploy hello un'applicazione hello e configurazione di hub eventi sink. file di hello tooview e modifica, aprirlo hello *wadcfgx* file in Visual Studio, modificarlo e salvarlo. percorso Hello è **progetto servizio Cloud** > **ruoli** > **(RoleName)** > **wadcfgx**.  

A questo punto, tutti distribuzione e aggiornamento delle azioni in Visual Studio, Visual Studio Team System e tutti i comandi o script che si basano su MSBuild e utilizzano hello **/t: pubblicare** destinazione include hello *wadcfgx*  nel processo di creazione di pacchetti hello. Inoltre, le distribuzioni e aggiornamenti è possibile distribuire tooAzure file hello usando hello appropriato agente l'estensione diagnostica Azure in macchine virtuali.

Dopo aver distribuito l'applicazione hello e configurazione di diagnostica di Azure, verrà visualizzata immediatamente l'attività nel dashboard di hello dell'hub eventi hello. Ciò indica che si è pronti toomove sui dati di percorso a caldo hello tooviewing hello listener client o l'analisi dello strumento di propria scelta.  

Nella seguente illustrazione di hello, il dashboard di hub eventi hello Mostra integro l'invio di diagnostica dati toohello evento hub avvio un po' dopo 11 PM. Ovvero quando è stata distribuita un'applicazione hello con una versione aggiornata *wadcfgx* file e hello sink è stato configurato correttamente.

![][0]  

> [!NOTE]
> Quando si apporta file di configurazione degli aggiornamenti toohello diagnostica Azure (con estensione wadcfgx), è consigliabile push hello aggiornamenti toohello intera applicazione, nonché configurazione hello tramite la pubblicazione in Visual Studio, o uno script di Windows PowerShell.  
>
>

## <a name="view-hot-path-data"></a>Visualizzare i dati del percorso critico
Come descritto in precedenza, sono disponibili molti casi di utilizzo per l'ascolto tooand l'elaborazione dei dati di hub eventi.

Un approccio semplice è un hub eventi del test di piccole dimensioni console applicazione toolisten toohello toocreate e flusso di output di stampa hello. È possibile inserire hello seguente di codice, è illustrato più dettagliatamente nella [Introduzione agli hub di eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in un'applicazione console.  

Si noti che un'applicazione console hello deve includere hello [pacchetto NuGet Host processore di eventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Tenere presente i valori hello tooreplace tra parentesi quadre in hello **Main** funzione con valori per le risorse.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Risoluzione dei problemi relativi ai sink dell'Hub eventi
* hub di eventi Hello non mostra l'attività dell'evento in ingresso o in uscita come previsto.

    Verificare che l'Hub eventi esegua correttamente il provisioning. Tutte le informazioni di connessione in hello **PrivateConfig** sezione *wadcfgx* devono corrispondere ai valori hello della risorsa come illustrato nel portale di hello. Assicurarsi di disporre di un criterio definito ("SendRule" nell'esempio hello) nel portale di hello e che *inviare* viene concessa l'autorizzazione.  
* Dopo un aggiornamento, hub eventi hello non mostra più EventActivity in ingresso o in uscita.

    Innanzitutto, assicurarsi che tale hub eventi hello e le informazioni di configurazione siano corretta, come illustrato in precedenza. In alcuni casi hello **PrivateConfig** viene reimpostato in un aggiornamento della distribuzione. Hello consiglia di correggere tutte le modifiche troppo toomake*wadcfgx* in hello progetto e quindi inviare un aggiornamento completo dell'applicazione. In caso contrario, assicurarsi che gli aggiornamenti di diagnostica hello inserisce completa **PrivateConfig** che include una chiave SAS hello.  
* Si è tentato di suggerimenti hello e hub eventi hello ancora non funziona.

    Provare a cercare nella tabella di archiviazione di Azure hello che contiene gli errori e log di diagnostica di Azure stesso: **WADDiagnosticInfrastructureLogsTable**. Un'opzione è toouse uno strumento, ad esempio [Azure Storage Explorer](http://www.storageexplorer.com) account di archiviazione toothis tooconnect, visualizzare in questa tabella e aggiungere una query per i TimeStamp in hello ultime 24 ore. È possibile utilizzare lo strumento di hello tooexport un file CSV e aprirlo in un'applicazione, ad esempio Microsoft Excel. Excel rende facile toosearch per le stringhe di carta telefonica, ad esempio **EventHubs**, toosee indica l'errore viene segnalato.  

## <a name="next-steps"></a>Passaggi successivi
• [Altre informazioni su Hub eventi](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Appendice: completare l'esempio di file (.wadcfgx) della configurazione di Diagnostica di Azure
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

Hello complementare *ServiceConfiguration* per questo esempio è simile a hello seguenti.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

Le impostazioni basate su Json equivalenti per le macchine virtuali sono le seguenti:
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Creare un hub eventi](../event-hubs/event-hubs-create.md)
* [Domande frequenti su Hub eventi](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
