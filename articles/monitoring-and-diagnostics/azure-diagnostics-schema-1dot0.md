---
title: Schema di configurazione di diagnostica 1.0 aaaAzure | Documenti Microsoft
description: "Utile SOLO se si usa Azure SDK 2.4 e versioni precedenti con le macchine virtuali di Azure, il set di scalabilità di macchine virtuali, Service Fabric o servizi Cloud."
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Schema di configurazione di Diagnostica di Azure 1.0
> [!NOTE]
> Diagnostica di Azure è contatori delle prestazioni toocollect componente utilizzato hello e altre statistiche da macchine virtuali di Azure, il set di scalabilità di macchine virtuali, Service Fabric e servizi Cloud.  Questa pagina è utile solo se si usa uno di questi servizi.
>

Lo strumento Diagnostica di Azure viene usato con altri prodotti di diagnostica Microsoft, quali Monitoraggio di Azure, Application Insights e Log Analytics.

file di configurazione di diagnostica Azure Hello definisce i valori vengono utilizzati tooinitialize hello Monitor di diagnostica. Questo file è tooinitialize utilizzate le impostazioni di configurazione quando si avvia il monitoraggio di diagnostica hello.  

 Per impostazione predefinita, i file dello schema di configurazione diagnostica di Azure di hello è toohello installato `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory. Sostituire `<version>` con la versione di hello installato di hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  file di configurazione della diagnostica Hello viene in genere utilizzata con le attività di avvio che richiedono toobe dati di diagnostica raccolti in precedenza nel processo di avvio hello. Per altre informazioni sull'uso di Diagnostica di Azure, vedere [Raccogliere dati di registrazione usando Diagnostica di Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Esempio di file di configurazione della diagnostica hello  
 Hello di esempio seguente viene illustrato un tipico file di configurazione:  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>Spazio dei nomi DiagnosticsConfiguration  
 spazio dei nomi XML Hello per file di configurazione di diagnostica hello è:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Elementi dello schema  
 file di configurazione della diagnostica Hello include hello seguenti elementi.


## <a name="diagnosticmonitorconfiguration-element"></a>Elemento DiagnosticMonitorConfiguration  
elemento di primo livello Hello hello diagnostica del file di configurazione.  

Attributi:

|Attributo  |Type   |Obbligatorio| Default | Descrizione|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|duration|Facoltativo | PT1M| Specifica l'intervallo hello in cui viene eseguito il polling monitor di diagnostica hello per le modifiche di configurazione di diagnostica.|  
|**overallQuotaInMB**|unsignedInt|Facoltativo| 4000 MB. Se si specifica un valore, non deve superare la quantità |quantità totale di Hello di archiviazione nel file system allocato per tutti i buffer di registrazione.|  

## <a name="diagnosticinfrastructurelogs-element"></a>Elemento DiagnosticInfrastructureLogs  
Definisce una configurazione del buffer hello per i log hello generati dall'infrastruttura diagnostica sottostante hello.

Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Attributi:

|Attributo|Tipo|Descrizione|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Facoltativo. Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.<br /><br /> valore predefinito di Hello è 0.|  
|**scheduledTransferLogLevelFilter**|string|Facoltativo. Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti. valore predefinito di Hello è **Undefined**. Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.|  
|**scheduledTransferPeriod**|duration|Facoltativo. Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.<br /><br /> valore predefinito di Hello è PT0S.|  

## <a name="logs-element"></a>Elemento Logs  
 Definisce una configurazione del buffer hello per i log di Azure di base.

 Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Facoltativo. Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.<br /><br /> valore predefinito di Hello è 0.|  
|**scheduledTransferLogLevelFilter**|string|Facoltativo. Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti. valore predefinito di Hello è **Undefined**. Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.|  
|**scheduledTransferPeriod**|duration|Facoltativo. Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.<br /><br /> valore predefinito di Hello è PT0S.|  

## <a name="directories-element"></a>Elemento Directories  
Definisce la configurazione di hello buffer per i log basati su file che è possibile definire.

Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  


Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Facoltativo. Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.<br /><br /> valore predefinito di Hello è 0.|  
|**scheduledTransferPeriod**|duration|Facoltativo. Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.<br /><br /> valore predefinito di Hello è PT0S.|  

## <a name="crashdumps-element"></a>Elemento CrashDumps  
 Definisce hello directory dei dump di arresto anomalo del sistema.

 Elemento padre: [elemento Directories](#Directories).  

Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**container**|string|nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.|  
|**directoryQuotaInMB**|unsignedInt|Facoltativo. Specifica dimensioni massime di hello della directory hello in megabyte.<br /><br /> valore predefinito di Hello è 0.|  

## <a name="failedrequestlogs-element"></a>Elemento FailedRequestLogs  
 Definisce hello directory dei log richieste non riuscite.

 Elemento padre: [elemento Directories](#Directories).  

Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**container**|string|nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.|  
|**directoryQuotaInMB**|unsignedInt|Facoltativo. Specifica dimensioni massime di hello della directory hello in megabyte.<br /><br /> valore predefinito di Hello è 0.|  

##  <a name="iislogs-element"></a>Elemento IISLogs  
 Definisce hello directory dei log IIS.

 Elemento padre: [elemento Directories](#Directories).  

Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**container**|string|nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.|  
|**directoryQuotaInMB**|unsignedInt|Facoltativo. Specifica dimensioni massime di hello della directory hello in megabyte.<br /><br /> valore predefinito di Hello è 0.|  

## <a name="datasources-element"></a>Elemento DataSources  
 Definisce zero o più directory di log aggiuntivi.

 Elemento padre: [elemento Directories](#Directories).

## <a name="directoryconfiguration-element"></a>Elemento DirectoryConfiguration  
 Definisce la directory hello di toomonitor i file di log.

 Elemento padre: [elemento DataSources](#DataSources).

Attributi:

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**container**|string|nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.|  
|**directoryQuotaInMB**|unsignedInt|Facoltativo. Specifica dimensioni massime di hello della directory hello in megabyte.<br /><br /> valore predefinito di Hello è 0.|  

## <a name="absolute-element"></a>Elemento Absolute  
 Definisce un percorso assoluto di hello directory toomonitor con espansione dell'ambiente facoltativo.

 Elemento padre: [elemento DirectoryConfiguration](#DirectoryConfiguration).  

Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**path**|string|Obbligatorio. Hello toomonitor directory toohello di percorso assoluto.|  
|**expandEnvironment**|boolean|Obbligatorio. Se impostato troppo**true**, le variabili di ambiente nel percorso hello vengono espanse.|  

## <a name="localresource-element"></a>Elemento LocalResource  
 Definisce una risorsa locale tooa relativo percorso definita nella definizione del servizio hello.

 Elemento padre: [elemento DirectoryConfiguration](#DirectoryConfiguration).  

Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**nome**|string|Obbligatorio. nome Hello della risorsa locale hello contenente toomonitor directory hello.|  
|**relativePath**|string|Obbligatorio. Hello toomonitor di percorso relativo toohello risorsa locale.|  

## <a name="performancecounters-element"></a>Elemento PerformanceCounters  
 Definisce il toocollect contatore delle prestazioni di hello percorso toohello.

 Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).


 Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Facoltativo. Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.<br /><br /> valore predefinito di Hello è 0.|  
|**scheduledTransferPeriod**|duration|Facoltativo. Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.<br /><br /> valore predefinito di Hello è PT0S.|  

## <a name="performancecounterconfiguration-element"></a>Elemento PerformanceCounterConfiguration  
 Definisce toocollect contatore delle prestazioni di hello.

 Elemento principale: [PerformanceCounters Element](#PerformanceCounters).  

 Attributi:  

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**counterSpecifier**|string|Obbligatorio. Hello toocollect contatore delle prestazioni toohello di percorso.|  
|**sampleRate**|duration|Obbligatorio. frequenza di Hello in cui hello deve essere raccolti contatore delle prestazioni.|  

## <a name="windowseventlog-element"></a>Elemento WindowsEventLog  
 Definisce hello toomonitor di registri eventi.

 Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).

  Attributi:

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|Facoltativo. Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.<br /><br /> valore predefinito di Hello è 0.|  
|**scheduledTransferLogLevelFilter**|string|Facoltativo. Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti. valore predefinito di Hello è **Undefined**. Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.|  
|**scheduledTransferPeriod**|duration|Facoltativo. Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.<br /><br /> valore predefinito di Hello è PT0S.|  

## <a name="datasource-element"></a>Elemento DataSource  
 Definisce toomonitor registro eventi di hello.

 Elemento principale: [elemento WindowsEventLog](#windowsEventLog).  

 Attributi:

|Attributo|Tipo|Descrizione|  
|---------------|----------|-----------------|  
|**nome**|string|Obbligatorio. Un'espressione XPath specifica toocollect log hello.|  
