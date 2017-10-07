---
title: aaaConfigure diagnostica Azure toosend dati tooApplication Insights | Documenti Microsoft
description: Aggiornare hello diagnostica Azure configurazione pubblica toosend dati tooApplication Insights.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Inviare i dati di diagnostica del servizio Cloud, macchine virtuali o Service Fabric tooApplication Insights
Servizi cloud, macchine virtuali, il set di scalabilità di macchine virtuali e Service Fabric utilizzano dati toocollect dell'estensione diagnostica di Azure hello.  Diagnostica di Azure invia dati tooAzure tabelle di archiviazione.  Tuttavia, è anche possibile tutti pipe o un subset di posizioni di tooother hello dati utilizzando l'estensione diagnostica Azure 1.5 o versioni successiva.

In questo articolo viene descritto come dati toosend hello tooApplication estensione diagnostica di Azure Insights.

## <a name="diagnostics-configuration-explained"></a>Descrizione della configurazione di Diagnostica
sink di estensione 1.5 introdotto diagnostica Windows Azure Hello, che sono percorsi aggiuntivi in cui è possibile inviare i dati di diagnostica.

Esempio di configurazione di un sink per Application Insights:

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- Hello **Sink** *nome* attributo è un valore stringa che identifica in modo univoco il sink hello.

- Hello **ApplicationInsights** elemento specifica la chiave di strumentazione di hello in cui verrà inviato i dati di diagnostica Azure hello risorsa di Application insights.
    - Se non si dispone di una risorsa di Application Insights esistente, vedere [creare una nuova risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md) per ulteriori informazioni sulla creazione di una risorsa e ottenere la chiave di strumentazione hello.
    - Se si sviluppa un servizio Cloud con Azure SDK 2.8 e versioni successive, questa chiave di strumentazione viene compilata automaticamente. il valore di Hello è basato su hello **APPINSIGHTS_INSTRUMENTATIONKEY** impostazione di configurazione del servizio al progetto di servizio Cloud hello. Vedere [problemi di servizio Cloud di utilizzare Application Insights con diagnostica Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Hello **canali** elemento contiene uno o più **canale** elementi.
    - Hello *nome* attributo fa riferimento in modo univoco il canale toothat.
    - Hello *loglevel* consente di specificare a livello di registrazione hello che hello canale consente di attributo. livelli di log disponibili Hello nell'ordine della maggior parte delle informazioni tooleast sono:
        - Dettagliato
        - Informazioni
        - Avviso
        - Errore
        - Critico

Un canale consente tooselect log specifici livelli toosend toohello destinazione sink e funziona come un filtro. Ad esempio, si potrebbe raccogliere log dettagliati e inviarli toostorage, ma solo sink toohello di errori di trasmissione.

Hello nella figura seguente viene illustrata questa relazione.

![Configurazione pubblica di Diagnostica](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Hello elemento grafico seguente sono riepilogati i valori di configurazione hello e sul relativo funzionamento. È possibile includere più sink nella configurazione di hello a diversi livelli nella gerarchia di hello. sink di Hello al primo livello hello funge da un'impostazione globale e hello uno specificata nella hello singoli elemento funziona come un'impostazione globale toothat di sostituzione.

![Configurazione dei sink di diagnostica con Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Esempio di configurazione del sink completo
Ecco un esempio completo della configurazione pubblica hello file
1. Invia tutti gli errori Insights tooApplication (specificato hello **DiagnosticMonitorConfiguration** nodo)
2. Invia anche i log dettagliati di livello per i registri applicazione hello (specificato hello **registri** nodo).

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
Nella configurazione precedente hello, hello seguendo le linee è hello seguenti significati:

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Invia tutti i dati di hello raccolti dalla diagnostica di Azure

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Invia solo i registri toohello Application Insights il sink di errore

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Trasmissione dettagliata applicazione registra tooApplication Insights

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Limitazioni

- **Unico tipo di log Channels e non per i contatori delle prestazioni.** Se si specifica un canale con un elemento contatore delle prestazioni, verrà ignorato.
- **livello di log Hello di un canale non può superare il livello di log hello di ciò che sono stati raccolti dalla diagnostica di Azure.** Ad esempio, non è possibile raccogliere gli errori di registro dell'applicazione nell'elemento registri hello si cerca toosend log dettagliati toohello Application Insights sink. Hello *scheduledTransferLogLevelFilter* attributo necessario raccogliere sempre uguale o più log di hello registra si sta tentando di toosend tooa sink.
- **Non è possibile inviare dati blob raccolti da tooApplication estensione diagnostica di Azure Insights.** Ad esempio, un valore specificato in hello *directory* nodo. Per i dump di arresto anomalo dump di arresto anomalo del sistema effettivo hello viene inviato archiviazione tooblob e solo una notifica che hello dump di arresto anomalo del sistema è stata generata viene inviato tooApplication Insights.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[visualizzare le informazioni di diagnostica di Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.
* Utilizzare [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello estensione diagnostica di Azure per l'applicazione.
* Utilizzare [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello estensione diagnostica di Azure per l'applicazione
