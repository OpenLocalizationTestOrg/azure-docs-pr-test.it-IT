---
title: Schema di configurazione di diagnostica 1.2 aaaAzure | Documenti Microsoft
description: "Utile SOLO se si usa Azure SDK 2.5 con le macchine virtuali di Azure, il set di scalabilità di macchine virtuali, Service Fabric o servizi Cloud."
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Schema di configurazione di Diagnostica Azure 1.2
> [!NOTE]
> Diagnostica di Azure è contatori delle prestazioni toocollect componente utilizzato hello e altre statistiche da macchine virtuali di Azure, il set di scalabilità di macchine virtuali, Service Fabric e servizi Cloud.  Questa pagina è utile solo se si usa uno di questi servizi.
>

Lo strumento Diagnostica di Azure viene usato con altri prodotti di diagnostica Microsoft, quali Monitoraggio di Azure, Application Insights e Log Analytics.

Questo schema definisce i valori possibili hello è possibile utilizzare le impostazioni di configurazione di diagnostica tooinitialize all'avvio di monitor di diagnostica hello.  


 Scarica definizione dello schema file di configurazione pubblica hello eseguendo hello comando PowerShell seguente:  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Per altre informazioni sulla diagnostica di Azure, vedere [Abilitazione di Diagnostica di Azure in Servizi cloud di Azure](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Esempio di file di configurazione della diagnostica hello  
 Hello di esempio seguente viene illustrato un tipico file di configurazione:  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
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
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
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
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Spazio dei nomi di configurazione della diagnostica  
 spazio dei nomi XML Hello per file di configurazione di diagnostica hello è:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>Elemento PublicConfig  
 Elemento di livello principale del file di configurazione di diagnostica hello. Hello nella tabella seguente descrive gli elementi di hello hello del file di configurazione.  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**WadCfg**|Obbligatorio. Impostazioni di configurazione per toobe dati di telemetria hello raccolti.|  
|**StorageAccount**|nome Hello hello Azure account toostore hello dei dati di archiviazione in. Questo può anche essere specificato come un parametro quando si esegue il cmdlet Set-AzureServiceDiagnosticsExtension hello.|  
|**LocalResourceDirectory**|directory di Hello in hello toobe di macchina virtuale utilizzata da hello dati dell'evento toostore Monitoring Agent. Se non viene usato set, directory predefinita hello:<br /><br /> Per un ruolo di lavoro/Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Per una macchina virtuale: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Gli attributi obbligatori sono i seguenti:<br /><br /> -                      **percorso** : hello directory hello sistema toobe utilizzato dagli strumenti di diagnostica di Azure.<br /><br /> -                      **expandEnvironment** -controlla se le variabili di ambiente vengono espanse nel nome di percorso hello.|  

## <a name="wadcfg-element"></a>Elemento WadCFG  
Definisce le impostazioni di configurazione per hello toobe di dati di telemetria raccolti. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Obbligatorio. Gli attributi facoltativi sono i seguenti:<br /><br /> -                     **overallQuotaInMB** -quantità massima di hello di spazio su disco locale che può essere utilizzata da hello vari tipi di dati di diagnostica raccolti da diagnostica di Azure. Hello predefinito è 5120MB.<br /><br /> -                     **useProxyServer** -configurare diagnostica Azure toouse hello impostazioni del server proxy come set di impostazioni di Internet Explorer.|  
|**CrashDumps**|Abilitare la raccolta di dump di arresto anomalo del sistema. Gli attributi facoltativi sono i seguenti:<br /><br /> -                     **containerName** -nome hello del contenitore blob hello in toobe di account del servizio di archiviazione Azure utilizzato toostore arresto anomalo del sistema.<br /><br /> -                     **crashDumpType** -consente di configurare diagnostica Azure toocollect Mini o Full arresto anomalo del dump.<br /><br /> -                     **directoryQuotaPercentage**-consente di configurare la percentuale hello di **overallQuotaInMB** toobe riservato per il dump di arresto anomalo in hello macchina virtuale.|  
|**DiagnosticInfrastructureLogs**|Abilita la raccolta dei log generati da Diagnostica di Azure. log dell'infrastruttura diagnostica Hello sono utili per la risoluzione dei problemi hello stesso sistema di diagnostica. Gli attributi facoltativi sono i seguenti:<br /><br /> -                     **scheduledTransferLogLevelFilter** -consente di configurare il livello minimo di gravità hello di hello log raccolti.<br /><br /> -                     **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Directories**|Abilita hello hello contenuto di una directory della raccolta, i log delle richieste di accesso e/o di log di IIS non riuscite di IIS. Attributo facoltativo:<br /><br /> **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|Configura la raccolta di eventi ETW da EventSource e/o da provider basati su manifesti ETW.|  
|**Metriche**|Questo elemento consente toogenerate una tabella del contatore delle prestazioni che è ottimizzata per le query veloce. Ogni contatore delle prestazioni che è definito in hello **PerformanceCounters** elemento viene archiviato nella tabella di metriche hello nella tabella di addizione toohello contatore delle prestazioni. Attributo obbligatorio:<br /><br /> **resourceId** -hello ID di risorsa di macchina virtuale si distribuisce la diagnostica di Azure per hello. Ottenere hello **resourceID** da hello [portale di Azure](https://portal.azure.com). Selezionare **Esplora** -> **Gruppi di risorse** -> **<Nome\>**. Fare clic su hello **proprietà** riquadro e copiare il valore di hello hello **ID** campo.|  
|**PerformanceCounters**|Abilita la raccolta di hello dei contatori delle prestazioni. Attributo facoltativo:<br /><br /> **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. Il valore è un ["Tipo di dati di durata" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**WindowsEventLog**|Abilita la raccolta di hello nei registri eventi di Windows. Attributo facoltativo:<br /><br /> **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. Il valore è un ["Tipo di dati di durata" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="crashdumps-element"></a>Elemento CrashDumps  
 Abilita la raccolta di dump di arresto anomalo del sistema. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|Obbligatorio. Attributo obbligatorio:<br /><br /> **processName** : hello nome del processo di hello da diagnostica di Azure toocollect un dump di arresto anomalo del sistema per.|  
|**crashDumpType**|Consente di configurare diagnostica Azure toocollect completo o breve anomalo.|  
|**directoryQuotaPercentage**|Consente di configurare la percentuale hello di **overallQuotaInMB** toobe riservato per il dump di arresto anomalo in hello macchina virtuale.|  

## <a name="directories-element"></a>Elemento Directories  
 Abilita hello hello contenuto di una directory della raccolta, i log delle richieste di accesso e/o di log di IIS non riuscite di IIS. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**DataSources**|Un elenco di directory toomonitor.|  
|**FailedRequestLogs**|Tra cui questo elemento di configurazione hello abilita la raccolta dei registri sul sito IIS tooan richieste non riuscite o l'applicazione. È anche necessario abilitare le opzioni di traccia sotto **system.WebServer** in **Web.config**.|  
|**IISLogs**|Tra cui questo elemento di configurazione hello abilita la raccolta di hello di log di IIS:<br /><br /> **containerName** -nome hello del contenitore blob hello in toobe di account del servizio di archiviazione Azure utilizzato toostore hello log di IIS.|  

## <a name="datasources-element"></a>Elemento DataSources  
 Un elenco di directory toomonitor. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**DirectoryConfiguration**|Obbligatorio. Attributo obbligatorio:<br /><br /> **containerName** -nome hello del contenitore blob hello nell'archiviazione Azure account toostore toobe utilizzato i file di log hello.|  

## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 **DirectoryConfiguration** può includere entrambi hello **assoluto** o **LocalResource** elemento ma non entrambi. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**Absolute**|Hello toomonitor directory toohello di percorso assoluto. Hello gli attributi seguenti è necessario:<br /><br /> -                     **Percorso** -hello toomonitor directory toohello di percorso assoluto.<br /><br /> -                      **expandEnvironment**: definisce se le variabili di ambiente vengono espanse in Path.|  
|**LocalResource**|Hello toomonitor di percorso relativo tooa risorsa locale. Gli attributi obbligatori sono i seguenti:<br /><br /> -                     **Nome** -hello risorsa locale contenente hello directory toomonitor<br /><br /> -                     **relativePath** -hello tooName relativo percorso contenente hello directory toomonitor|  

## <a name="etwproviders-element"></a>Elemento EtwProviders  
 Configura la raccolta di eventi ETW da EventSource e/o da provider basati su manifesti ETW. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Attributo obbligatorio:<br /><br /> **provider** -nome della classe di evento EventSource hello hello.<br /><br /> Gli attributi facoltativi sono i seguenti:<br /><br /> -                     **scheduledTransferLogLevelFilter** -hello account di archiviazione tooyour tootransfer livello minimo di gravità.<br /><br /> -                     **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. Il valore è un [Tipo di dati di durata XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Attributo obbligatorio:<br /><br /> **provider** -GUID del provider di eventi hello hello<br /><br /> Gli attributi facoltativi sono i seguenti:<br /><br /> - **scheduledTransferLogLevelFilter** -hello account di archiviazione tooyour tootransfer livello minimo di gravità.<br /><br /> -                     **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. Il valore è un [Tipo di dati di durata XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>Elemento EtwEventSourceProviderConfiguration  
 Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**DefaultEvents**|Attributo facoltativo:<br /><br /> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  
|**Event**|Attributo obbligatorio:<br /><br /> **ID** -id hello dell'evento di hello.<br /><br /> Attributo facoltativo:<br /><br /> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  

## <a name="etwmanifestproviderconfiguration-element"></a>Elemento EtwManifestProviderConfiguration  
 Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**DefaultEvents**|Attributo facoltativo:<br /><br /> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  
|**Event**|Attributo obbligatorio:<br /><br /> **ID** -id hello dell'evento di hello.<br /><br /> Attributo facoltativo:<br /><br /> **eventDestination** : hello nome di eventi di hello tabella toostore hello in|  

## <a name="metrics-element"></a>Elemento Metrics  
 Consente di toogenerate una tabella del contatore delle prestazioni che è ottimizzata per le query veloce. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**MetricAggregation**|Attributo obbligatorio:<br /><br /> **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto. Il valore è un [Tipo di dati di durata XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 Abilita la raccolta di hello dei contatori delle prestazioni. Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hello gli attributi seguenti è necessario:<br /><br /> -                     **counterSpecifier** : hello Nome hello contatore delle prestazioni. ad esempio `\Processor(_Total)\% Processor Time`. un elenco di contatori delle prestazioni nell'host di cui eseguire il comando hello tooget `typeperf`.<br /><br /> -                     **sampleRate** -frequenza hello del contatore.<br /><br /> Attributo facoltativo:<br /><br /> **unità** -unità di misura del contatore hello di hello.|  

## <a name="performancecounterconfiguration-element"></a>Elemento PerformanceCounterConfiguration  
 Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**annotation**|Attributo obbligatorio:<br /><br /> **displayName** -nome visualizzato hello contatore hello<br /><br /> Attributo facoltativo:<br /><br /> **impostazioni locali** -hello toouse internazionali quando si visualizza il nome di contatore hello|  

## <a name="windowseventlog-element"></a>Elemento WindowsEventLog  
 Hello nella tabella seguente vengono descritti gli elementi figlio:  

|Nome dell'elemento|Descrizione|  
|------------------|-----------------|  
|**DataSource**|toocollect i registri eventi di Windows Hello. Attributo obbligatorio:<br /><br /> **nome** -query XPath hello che descrive toobe gli eventi di windows hello raccolti. ad esempio:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> specificare tutti gli eventi, toocollect "*".|
