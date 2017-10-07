---
title: schema di configurazione 1.3 e versioni successive di estensione di diagnostica aaaAzure | Documenti Microsoft
description: Versione dello schema 1.3 e versioni successive diagnostica Windows Azure fornito come parte di hello Microsoft Azure SDK 2.4 e versioni successive.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Schema di configurazione di Diagnostica di Azure 1.3 e versioni successive
> [!NOTE]
> Hello estensione diagnostica di Azure è il componente di hello utilizzato toocollect contatori delle prestazioni e altre statistiche da:
> - Macchine virtuali di Azure 
> - Set di scalabilità di macchine virtuali
> - Service Fabric 
> - Servizi cloud 
> - Gruppi di sicurezza di rete
> 
> Questa pagina è utile solo se si usa uno di questi servizi.

Questa pagina è valida per le versioni 1.3 e più recenti (Azure SDK 2.4 e versioni più recenti). Le sezioni di configurazione più recenti sono tooshow commentata nella versione sono stati aggiunti.  

file di configurazione di Hello descritti di seguito è tooset utilizzate le impostazioni di configurazione quando si avvia il monitoraggio di diagnostica hello.  

estensione Hello viene utilizzato in combinazione con altri prodotti Microsoft, diagnostica quali monitoraggio di Azure, Application Insights e Analitica di Log.



Scarica definizione dello schema file di configurazione pubblica hello eseguendo hello comando PowerShell seguente:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Per altre informazioni su Diagnostica di Azure, vedere [Estensione di Diagnostica di Azure](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Esempio di file di configurazione della diagnostica hello  
 Hello di esempio seguente viene illustrato un tipico file di configurazione:  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

Equivalente in JSON del file di configurazione XML precedente hello. 

Hello PublicConfig e PrivateConfig sono separate, poiché nella maggior parte dei casi di utilizzo di json, vengono passati come variabili diverse. Alcuni esempi sono i modelli di Resource Manager, i set di scalabilità di macchine virtuali PowerShell e Visual Studio. 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
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
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>Come leggere questa pagina  
 Hello i tag seguenti sono approssimativamente nell'ordine illustrato nell'esempio sopra riportato hello.  Se non viene visualizzata una descrizione completa in cui si prevede, pagina di ricerca hello per hello elemento o attributo.  

## <a name="common-attribute-types"></a>Tipi di attributi comuni  
 L'attributo **scheduledTransferPeriod** è presente in diversi elementi. È l'intervallo di hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>Elemento DiagnosticsConfiguration  
 *Albero: radice - DiagnosticsConfiguration*

Aggiunto nella versione 1.3.  

elemento di primo livello Hello hello diagnostica del file di configurazione.  

**Attributo** xmlns - hello spazio dei nomi XML per il file di configurazione della diagnostica hello è:  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**PublicConfig**|Obbligatorio. Vedere la descrizione altrove in questa pagina.|  
|**PrivateConfig**|Facoltativa. Vedere la descrizione altrove in questa pagina.|  
|**IsEnabled**|Booleano. Vedere la descrizione altrove in questa pagina.|  

## <a name="publicconfig-element"></a>Elemento PublicConfig  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig*

 Descrive una configurazione della diagnostica pubblica hello.  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**WadCfg**|Obbligatorio. Vedere la descrizione altrove in questa pagina.|  
|**StorageAccount**|nome Hello hello Azure account toostore hello dei dati di archiviazione in. Può anche essere specificato come parametro quando si esegue il cmdlet Set-AzureServiceDiagnosticsExtension hello.|  
|**Tipo di archiviazione**|Può essere *Table*, *Blob* o *TableAndBlob*. Table è il valore predefinito. Quando viene scelto TableAndBlob, dati di diagnostica vengono scritti due volte, una volta tooeach tipo.|  
|**LocalResourceDirectory**|directory di Hello nella macchina virtuale hello in hello Monitoring Agent memorizza dati dell'evento. Se non impostato, viene utilizzato directory predefinita hello:<br /><br /> Per un ruolo di lavoro/Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Per una macchina virtuale: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Gli attributi obbligatori sono i seguenti:<br /><br /> - **percorso** : hello directory hello sistema toobe utilizzato dagli strumenti di diagnostica di Azure.<br /><br /> - **expandEnvironment** -controlla se le variabili di ambiente vengono espanse nel nome di percorso hello.|  

## <a name="wadcfg-element"></a>Elemento WadCFG  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG*
 
 Identifica e configura hello toobe di dati di telemetria raccolti.  


## <a name="diagnosticmonitorconfiguration-element"></a>Elemento DiagnosticMonitorConfiguration 
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*

 Obbligatorio 

|Attributi|Descrizione|  
|----------------|-----------------|  
| **overallQuotaInMB** | quantità massima di Hello di spazio su disco locale che può essere utilizzata da hello vari tipi di dati di diagnostica raccolti tramite diagnostica Azure. Hello predefinito è 5120 MB.<br />
|**useProxyServer** | Configurare impostazioni del server proxy hello toouse diagnostica di Azure come set di impostazioni di Internet Explorer.|  

<br /> <br />

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**CrashDumps**|Vedere la descrizione altrove in questa pagina.|  
|**DiagnosticInfrastructureLogs**|Abilita la raccolta dei log generati da Diagnostica di Azure. log dell'infrastruttura diagnostica Hello sono utili per la risoluzione dei problemi hello stesso sistema di diagnostica. Gli attributi facoltativi sono i seguenti:<br /><br /> - **scheduledTransferLogLevelFilter** -consente di configurare il livello minimo di gravità hello di hello log raccolti.<br /><br /> - **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Directories**|Vedere la descrizione altrove in questa pagina.|  
|**EtwProviders**|Vedere la descrizione altrove in questa pagina.|  
|**Metriche**|Vedere la descrizione altrove in questa pagina.|  
|**PerformanceCounters**|Vedere la descrizione altrove in questa pagina.|  
|**WindowsEventLog**|Vedere la descrizione altrove in questa pagina.| 
|**DockerSources**|Vedere la descrizione altrove in questa pagina. | 



## <a name="crashdumps-element"></a>Elemento CrashDumps  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*
 
 Abilitare la raccolta di hello dei dump di arresto anomalo del sistema.  

|Attributi|Descrizione|  
|----------------|-----------------|  
|**containerName**|Facoltativo. nome di Hello del contenitore blob hello in toobe di account del servizio di archiviazione Azure utilizzato toostore arresto anomalo del sistema.|  
|**crashDumpType**|Facoltativo.  Consente di configurare diagnostica Azure toocollect completo o breve anomalo.|  
|**directoryQuotaPercentage**|Facoltativo.  Consente di configurare la percentuale hello di **overallQuotaInMB** toobe riservato per il dump di arresto anomalo in hello macchina virtuale.|  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Obbligatorio. Definisce i valori di configurazione di ogni processo.<br /><br /> è necessario anche Hello seguente attributo:<br /><br /> **processName** : hello nome del processo di hello da diagnostica di Azure toocollect un dump di arresto anomalo del sistema per.|  

## <a name="directories-element"></a>Elemento Directories 
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories*

 Abilita hello hello contenuto di una directory della raccolta, i log delle richieste di accesso e/o di log di IIS non riuscite di IIS.  

 Attributo **scheduledTransferPeriod** facoltativo. Vedere la spiegazione indicata in precedenza.  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**IISLogs**|Tra cui questo elemento di configurazione hello abilita la raccolta di hello di log di IIS:<br /><br /> **containerName** -nome hello del contenitore blob hello in toobe di account del servizio di archiviazione Azure utilizzato toostore hello log di IIS.|   
|**FailedRequestLogs**|Tra cui questo elemento di configurazione hello abilita la raccolta dei registri sul sito IIS tooan richieste non riuscite o l'applicazione. È anche necessario abilitare le opzioni di traccia sotto **system.WebServer** in **Web.config**.|  
|**DataSources**|Un elenco di directory toomonitor.| 




## <a name="datasources-element"></a>Elemento DataSources  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*

 Un elenco di directory toomonitor.  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Obbligatorio. Attributo obbligatorio:<br /><br /> **containerName** : hello nome del contenitore blob hello nell'account di archiviazione di Azure che toobe utilizzato i file di log toostore hello.|  





## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*

 Può includere entrambi hello **assoluto** o **LocalResource** elemento ma non entrambi.  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**Absolute**|Hello toomonitor directory toohello di percorso assoluto. Hello gli attributi seguenti è necessario:<br /><br /> - **Percorso** -hello toomonitor directory toohello di percorso assoluto.<br /><br /> - **expandEnvironment**: definisce se le variabili di ambiente vengono espanse in Path.|  
|**LocalResource**|Hello toomonitor di percorso relativo tooa risorsa locale. Gli attributi obbligatori sono i seguenti:<br /><br /> - **Nome** -hello risorsa locale contenente hello directory toomonitor<br /><br /> - **relativePath** -hello tooName relativo percorso contenente hello directory toomonitor|  



## <a name="etwproviders-element"></a>Elemento EtwProviders  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*

 Configura la raccolta di eventi ETW da EventSource e/o da provider basati su manifesti ETW.  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Attributo obbligatorio:<br /><br /> **provider** -nome della classe di evento EventSource hello hello.<br /><br /> Gli attributi facoltativi sono i seguenti:<br /><br /> - **scheduledTransferLogLevelFilter** -hello account di archiviazione tooyour tootransfer livello minimo di gravità.<br /><br /> - **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Attributo obbligatorio:<br /><br /> **provider** -GUID del provider di eventi hello hello<br /><br /> Gli attributi facoltativi sono i seguenti:<br /><br /> - **scheduledTransferLogLevelFilter** -hello account di archiviazione tooyour tootransfer livello minimo di gravità.<br /><br /> - **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>Elemento EtwEventSourceProviderConfiguration  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*

 Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**DefaultEvents**|Attributo facoltativo:<br/><br/> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  
|**Event**|Attributo obbligatorio:<br /><br /> **ID** -id hello dell'evento di hello.<br /><br /> Attributo facoltativo:<br /><br /> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  



## <a name="etwmanifestproviderconfiguration-element"></a>Elemento EtwManifestProviderConfiguration  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**DefaultEvents**|Attributo facoltativo:<br /><br /> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  
|**Event**|Attributo obbligatorio:<br /><br /> **ID** -id hello dell'evento di hello.<br /><br /> Attributo facoltativo:<br /><br /> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  



## <a name="metrics-element"></a>Elemento Metrics  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*

 Consente di toogenerate una tabella del contatore delle prestazioni che è ottimizzata per le query veloce. Ogni contatore delle prestazioni che è definito in hello **PerformanceCounters** elemento viene archiviato nella tabella di metriche hello nella tabella di addizione toohello contatore delle prestazioni.  

 Hello **resourceId** attributo è obbligatorio.  ID di risorsa Hello della macchina virtuale si distribuisce la diagnostica di Azure per hello. Ottenere hello **resourceID** da hello [portale di Azure](https://portal.azure.com). Selezionare **Esplora** -> **Gruppi di risorse** -> **<Nome\>**. Fare clic su hello **proprietà** riquadro e copiare il valore di hello hello **ID** campo.  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**MetricAggregation**|Attributo obbligatorio:<br /><br /> **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*

 Abilita la raccolta di hello dei contatori delle prestazioni.  

 Attributo facoltativo:  

 Attributo **scheduledTransferPeriod** facoltativo. Vedere la spiegazione indicata in precedenza.

|Elemento figlio|Descrizione|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hello gli attributi seguenti è necessario:<br /><br /> - **counterSpecifier** : hello Nome hello contatore delle prestazioni. ad esempio `\Processor(_Total)\% Processor Time`. tooget un elenco di prestazioni contatori sull'host, eseguire il comando di hello `typeperf`.<br /><br /> - **sampleRate** -frequenza hello del contatore.<br /><br /> Attributo facoltativo:<br /><br /> **unità** -unità di misura del contatore hello di hello.|  




## <a name="windowseventlog-element"></a>Elemento WindowsEventLog
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*
 
 Abilita la raccolta di hello nei registri eventi di Windows.  

 Attributo **scheduledTransferPeriod** facoltativo. Vedere la spiegazione indicata in precedenza.  

|Elemento figlio|Descrizione|  
|-------------------|-----------------|  
|**DataSource**|toocollect i registri eventi di Windows Hello. Attributo obbligatorio:<br /><br /> **nome** -query XPath hello che descrive toobe gli eventi di windows hello raccolti. ad esempio:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> specificare tutti gli eventi, toocollect "*"|  




## <a name="logs-element"></a>Elemento Logs  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*

 Presente nella versione 1.0 e 1.1. Assente nella versione 1.2. Aggiunto nuovamente nella versione 1.3.  

 Definisce una configurazione del buffer hello per i log di Azure di base.  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|Facoltativo. Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.<br /><br /> valore predefinito di Hello è 0.|  
|**scheduledTransferLogLevelFilterr**|**string**|Facoltativo. Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti. valore predefinito di Hello è **Undefined**, che trasferisce tutti i log. Altri valori possibili (nell'ordine della maggior parte delle informazioni tooleast) sono **Verbose**, **informazioni**, **avviso**, **errore**e **Critico**.|  
|**scheduledTransferPeriod**|**duration**|Facoltativo. Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.<br /><br /> valore predefinito di Hello è PT0S.|  
|**sinks** aggiunto nella versione 1.5|**string**|Facoltativo. Punti tooa sink percorso tooalso inviare dati di diagnostica. ad esempio Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*

 Elementi aggiunti nella versione 1.9.

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**Stats**|Indica il sistema di hello toocollect statistiche per i contenitori di Docker|  

## <a name="sinksconfig-element"></a>Elemento SinksConfig  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*

 Un elenco di percorsi toosend dati tooand hello configurazione di diagnostica associati a tali percorsi.  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**Sink**|Vedere la descrizione altrove in questa pagina.|  

## <a name="sink-element"></a>Elemento Sink
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*

 Aggiunto nella versione 1.5.  

 Definisce i percorsi toosend dati di diagnostica. Salve, ad esempio, il servizio di Application Insights.  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**nome**|string|Stringa identificazione sinkname hello.|  

|Elemento|Type|Descrizione|  
|-------------|----------|-----------------|  
|**Application Insights**|string|Utilizzato solo quando l'invio di dati tooApplication Insights. Contenere hello chiave di strumentazione per un account di Application Insights attivo che è possibile accedere.|  
|**Channels**|string|Uno per ogni filtro aggiuntivo per i flussi|  

## <a name="channels-element"></a>Elemento Channels  
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*

 Aggiunto nella versione 1.5.  

 Definisce i filtri per i flussi di dati di log che attraversano un sink.  

|Elemento|Type|Descrizione|  
|-------------|----------|-----------------|  
|**Channel**|string|Vedere la descrizione altrove in questa pagina.|  

## <a name="channel-element"></a>Elemento Channel
 *Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*

 Aggiunto nella versione 1.5.  

 Definisce i percorsi toosend dati di diagnostica. Salve, ad esempio, il servizio di Application Insights.  

|Attributi|Type|Descrizione|  
|----------------|----------|-----------------|  
|**logLevel**|**string**|Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti. valore predefinito di Hello è **Undefined**, che trasferisce tutti i log. Altri valori possibili (nell'ordine della maggior parte delle informazioni tooleast) sono **Verbose**, **informazioni**, **avviso**, **errore**e **Critico**.|  
|**nome**|**string**|Un nome univoco di hello canale toorefer per|  


## <a name="privateconfig-element"></a>Elemento PrivateConfig 
 *Albero: radice - DiagnosticsConfiguration - PrivateConfig*

 Aggiunto nella versione 1.3.  

 Facoltativo  

 Archivia i dettagli di privata hello hello dell'account di archiviazione (nome, chiave ed endpoint). Queste informazioni viene inviate una macchina virtuale toohello, ma non possono essere recuperate da esso.  

|Elementi figlio|Descrizione|  
|--------------------|-----------------|  
|**StorageAccount**|toouse di account di archiviazione Hello. Hello gli attributi seguenti è obbligatorio<br /><br /> - **nome** : hello nome dell'account di archiviazione hello.<br /><br /> - **chiave** : hello toohello account di archiviazione della chiave.<br /><br /> - **endpoint** -hello endpoint tooaccess hello account di archiviazione. <br /><br /> -**sasToken** (è possibile specificare un token di firma di accesso condiviso anziché una chiave di account di archiviazione nel file di configurazione privata hello 1.8.1)-aggiunto. Se fornito, chiave di account di archiviazione hello viene ignorato. <br />Requisiti per il Token SAS hello: <br />- Supporta solo il token di firma di accesso condiviso dell'account <br />Sono obbligatori i tipi di servizio - *b* e *t*. <br /> Sono obbligatorie le autorizzazioni - *a*, *c*, *u*, *w*. <br /> Sono obbligatori i tipi di risorse - *c*, *o*. <br /> -Supporta solo il protocollo HTTPS hello <br /> -I valori dell'ora di inizio e di scadenza devono essere validi.|  


## <a name="isenabled-element"></a>Elemento IsEnabled  
 *Albero: radice - DiagnosticsConfiguration - IsEnabled*

 Booleano. Utilizzare `true` diagnostica hello tooenable o `false` diagnostica hello toodisable.
