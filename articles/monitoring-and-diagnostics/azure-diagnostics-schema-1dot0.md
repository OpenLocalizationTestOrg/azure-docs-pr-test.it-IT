---
title: Schema di configurazione di Diagnostica di Azure 1.0 | Documentazione Microsoft
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
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="63cd2-103">Schema di configurazione di Diagnostica di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="63cd2-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="63cd2-104">Diagnostica di Azure è il componente usato per raccogliere i contatori delle prestazioni e altre statistiche da Macchine virtuali, set di scalabilità di macchine virtuali, Service Fabric e Servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="63cd2-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="63cd2-105">Questa pagina è utile solo se si usa uno di questi servizi.</span><span class="sxs-lookup"><span data-stu-id="63cd2-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="63cd2-106">Lo strumento Diagnostica di Azure viene usato con altri prodotti di diagnostica Microsoft, quali Monitoraggio di Azure, Application Insights e Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="63cd2-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="63cd2-107">Il file di configurazione di Diagnostica di Azure definisce i valori usati per inizializzare il monitor di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="63cd2-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="63cd2-108">Il file viene usato per inizializzare le impostazioni di diagnostica quando viene avviato il monitor di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="63cd2-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="63cd2-109">Per impostazione predefinita, il file dello schema di configurazione di Diagnostica di Azure viene installato nella directory `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas`.</span><span class="sxs-lookup"><span data-stu-id="63cd2-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="63cd2-110">Sostituire `<version>` con la versione installata di [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="63cd2-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="63cd2-111">Il file di configurazione della diagnostica viene generalmente usato con le attività di avvio che richiedono la raccolta dei dati di diagnostica in una fase precedente del processo di avvio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="63cd2-112">Per altre informazioni sull'uso di Diagnostica di Azure, vedere [Raccogliere dati di registrazione usando Diagnostica di Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="63cd2-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="63cd2-113">Esempio del file di configurazione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="63cd2-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="63cd2-114">L'esempio seguente illustra un tipico file di configurazione della diagnostica:</span><span class="sxs-lookup"><span data-stu-id="63cd2-114">The following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="63cd2-115">Spazio dei nomi DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="63cd2-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="63cd2-116">Lo spazio dei nomi XML per il file di configurazione della diagnostica è il seguente:</span><span class="sxs-lookup"><span data-stu-id="63cd2-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="63cd2-117">Elementi dello schema</span><span class="sxs-lookup"><span data-stu-id="63cd2-117">Schema Elements</span></span>  
 <span data-ttu-id="63cd2-118">Il file di configurazione della diagnostica include gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="63cd2-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="63cd2-119">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="63cd2-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="63cd2-120">Elemento di livello superiore del file di configurazione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="63cd2-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="63cd2-121">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-121">Attributes:</span></span>

|<span data-ttu-id="63cd2-122">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-122">Attribute</span></span>  |<span data-ttu-id="63cd2-123">Type</span><span class="sxs-lookup"><span data-stu-id="63cd2-123">Type</span></span>   |<span data-ttu-id="63cd2-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="63cd2-124">Required</span></span>| <span data-ttu-id="63cd2-125">Default</span><span class="sxs-lookup"><span data-stu-id="63cd2-125">Default</span></span> | <span data-ttu-id="63cd2-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="63cd2-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="63cd2-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="63cd2-128">duration</span><span class="sxs-lookup"><span data-stu-id="63cd2-128">duration</span></span>|<span data-ttu-id="63cd2-129">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="63cd2-129">Optional</span></span> | <span data-ttu-id="63cd2-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="63cd2-130">PT1M</span></span>| <span data-ttu-id="63cd2-131">Specifica l'intervallo con cui il monitor di diagnostica esegue il polling per le modifiche della configurazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="63cd2-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="63cd2-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="63cd2-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-133">unsignedInt</span></span>|<span data-ttu-id="63cd2-134">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="63cd2-134">Optional</span></span>| <span data-ttu-id="63cd2-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="63cd2-135">4000 MB.</span></span> <span data-ttu-id="63cd2-136">Se si specifica un valore, non deve superare la quantità</span><span class="sxs-lookup"><span data-stu-id="63cd2-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="63cd2-137">Spazio totale di archiviazione del file system allocato per tutti i buffer di registrazione.</span><span class="sxs-lookup"><span data-stu-id="63cd2-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="63cd2-138">Elemento DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="63cd2-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="63cd2-139">Definisce la configurazione del buffer per i log generati dall'infrastruttura di diagnostica sottostante.</span><span class="sxs-lookup"><span data-stu-id="63cd2-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="63cd2-140">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="63cd2-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="63cd2-141">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-141">Attributes:</span></span>

|<span data-ttu-id="63cd2-142">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-142">Attribute</span></span>|<span data-ttu-id="63cd2-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-143">Type</span></span>|<span data-ttu-id="63cd2-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="63cd2-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="63cd2-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-146">unsignedInt</span></span>|<span data-ttu-id="63cd2-147">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-147">Optional.</span></span> <span data-ttu-id="63cd2-148">Specifica lo spazio massimo di archiviazione del file system disponibile per i dati specificati.</span><span class="sxs-lookup"><span data-stu-id="63cd2-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="63cd2-149">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-149">The default is 0.</span></span>|  
|<span data-ttu-id="63cd2-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="63cd2-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="63cd2-151">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-151">string</span></span>|<span data-ttu-id="63cd2-152">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-152">Optional.</span></span> <span data-ttu-id="63cd2-153">Specifica il livello di gravità minimo per le voci di log trasferite.</span><span class="sxs-lookup"><span data-stu-id="63cd2-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="63cd2-154">Il valore predefinito è **Non definito**.</span><span class="sxs-lookup"><span data-stu-id="63cd2-154">The default value is **Undefined**.</span></span> <span data-ttu-id="63cd2-155">Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="63cd2-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="63cd2-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="63cd2-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="63cd2-157">duration</span><span class="sxs-lookup"><span data-stu-id="63cd2-157">duration</span></span>|<span data-ttu-id="63cd2-158">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-158">Optional.</span></span> <span data-ttu-id="63cd2-159">Specifica l'intervallo tra trasferimenti di dati pianificati, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="63cd2-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="63cd2-160">Il valore predefinito è PT0S.</span><span class="sxs-lookup"><span data-stu-id="63cd2-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="63cd2-161">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="63cd2-161">Logs Element</span></span>  
 <span data-ttu-id="63cd2-162">Definisce la configurazione del buffer per i log di base di Azure.</span><span class="sxs-lookup"><span data-stu-id="63cd2-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="63cd2-163">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="63cd2-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="63cd2-164">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-164">Attributes:</span></span>  

|<span data-ttu-id="63cd2-165">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-165">Attribute</span></span>|<span data-ttu-id="63cd2-166">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-166">Type</span></span>|<span data-ttu-id="63cd2-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="63cd2-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-169">unsignedInt</span></span>|<span data-ttu-id="63cd2-170">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-170">Optional.</span></span> <span data-ttu-id="63cd2-171">Specifica lo spazio massimo di archiviazione del file system disponibile per i dati specificati.</span><span class="sxs-lookup"><span data-stu-id="63cd2-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="63cd2-172">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-172">The default is 0.</span></span>|  
|<span data-ttu-id="63cd2-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="63cd2-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="63cd2-174">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-174">string</span></span>|<span data-ttu-id="63cd2-175">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-175">Optional.</span></span> <span data-ttu-id="63cd2-176">Specifica il livello di gravità minimo per le voci di log trasferite.</span><span class="sxs-lookup"><span data-stu-id="63cd2-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="63cd2-177">Il valore predefinito è **Non definito**.</span><span class="sxs-lookup"><span data-stu-id="63cd2-177">The default value is **Undefined**.</span></span> <span data-ttu-id="63cd2-178">Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="63cd2-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="63cd2-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="63cd2-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="63cd2-180">duration</span><span class="sxs-lookup"><span data-stu-id="63cd2-180">duration</span></span>|<span data-ttu-id="63cd2-181">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-181">Optional.</span></span> <span data-ttu-id="63cd2-182">Specifica l'intervallo tra trasferimenti di dati pianificati, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="63cd2-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="63cd2-183">Il valore predefinito è PT0S.</span><span class="sxs-lookup"><span data-stu-id="63cd2-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="63cd2-184">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="63cd2-184">Directories Element</span></span>  
<span data-ttu-id="63cd2-185">Definisce la configurazione del buffer per i log basati su file che è possibile definire.</span><span class="sxs-lookup"><span data-stu-id="63cd2-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="63cd2-186">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="63cd2-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="63cd2-187">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-187">Attributes:</span></span>  

|<span data-ttu-id="63cd2-188">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-188">Attribute</span></span>|<span data-ttu-id="63cd2-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-189">Type</span></span>|<span data-ttu-id="63cd2-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="63cd2-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-192">unsignedInt</span></span>|<span data-ttu-id="63cd2-193">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-193">Optional.</span></span> <span data-ttu-id="63cd2-194">Specifica lo spazio massimo di archiviazione del file system disponibile per i dati specificati.</span><span class="sxs-lookup"><span data-stu-id="63cd2-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="63cd2-195">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-195">The default is 0.</span></span>|  
|<span data-ttu-id="63cd2-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="63cd2-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="63cd2-197">duration</span><span class="sxs-lookup"><span data-stu-id="63cd2-197">duration</span></span>|<span data-ttu-id="63cd2-198">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-198">Optional.</span></span> <span data-ttu-id="63cd2-199">Specifica l'intervallo tra trasferimenti di dati pianificati, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="63cd2-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="63cd2-200">Il valore predefinito è PT0S.</span><span class="sxs-lookup"><span data-stu-id="63cd2-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="63cd2-201">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="63cd2-201">CrashDumps Element</span></span>  
 <span data-ttu-id="63cd2-202">Definisce la directory dei dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="63cd2-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="63cd2-203">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="63cd2-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="63cd2-204">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-204">Attributes:</span></span>  

|<span data-ttu-id="63cd2-205">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-205">Attribute</span></span>|<span data-ttu-id="63cd2-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-206">Type</span></span>|<span data-ttu-id="63cd2-207">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-208">**container**</span><span class="sxs-lookup"><span data-stu-id="63cd2-208">**container**</span></span>|<span data-ttu-id="63cd2-209">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-209">string</span></span>|<span data-ttu-id="63cd2-210">Nome del contenitore in cui dovrà essere trasferito il contenuto della directory.</span><span class="sxs-lookup"><span data-stu-id="63cd2-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="63cd2-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="63cd2-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-212">unsignedInt</span></span>|<span data-ttu-id="63cd2-213">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-213">Optional.</span></span> <span data-ttu-id="63cd2-214">Specifica le dimensioni massime della directory in MB.</span><span class="sxs-lookup"><span data-stu-id="63cd2-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="63cd2-215">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="63cd2-216">Elemento FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="63cd2-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="63cd2-217">Definisce la directory dei log di richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="63cd2-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="63cd2-218">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="63cd2-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="63cd2-219">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-219">Attributes:</span></span>  

|<span data-ttu-id="63cd2-220">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-220">Attribute</span></span>|<span data-ttu-id="63cd2-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-221">Type</span></span>|<span data-ttu-id="63cd2-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-223">**container**</span><span class="sxs-lookup"><span data-stu-id="63cd2-223">**container**</span></span>|<span data-ttu-id="63cd2-224">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-224">string</span></span>|<span data-ttu-id="63cd2-225">Nome del contenitore in cui dovrà essere trasferito il contenuto della directory.</span><span class="sxs-lookup"><span data-stu-id="63cd2-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="63cd2-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="63cd2-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-227">unsignedInt</span></span>|<span data-ttu-id="63cd2-228">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-228">Optional.</span></span> <span data-ttu-id="63cd2-229">Specifica le dimensioni massime della directory in MB.</span><span class="sxs-lookup"><span data-stu-id="63cd2-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="63cd2-230">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="63cd2-231">Elemento IISLogs</span><span class="sxs-lookup"><span data-stu-id="63cd2-231">IISLogs Element</span></span>  
 <span data-ttu-id="63cd2-232">Definisce la directory di log IIS.</span><span class="sxs-lookup"><span data-stu-id="63cd2-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="63cd2-233">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="63cd2-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="63cd2-234">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-234">Attributes:</span></span>  

|<span data-ttu-id="63cd2-235">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-235">Attribute</span></span>|<span data-ttu-id="63cd2-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-236">Type</span></span>|<span data-ttu-id="63cd2-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-238">**container**</span><span class="sxs-lookup"><span data-stu-id="63cd2-238">**container**</span></span>|<span data-ttu-id="63cd2-239">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-239">string</span></span>|<span data-ttu-id="63cd2-240">Nome del contenitore in cui dovrà essere trasferito il contenuto della directory.</span><span class="sxs-lookup"><span data-stu-id="63cd2-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="63cd2-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="63cd2-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-242">unsignedInt</span></span>|<span data-ttu-id="63cd2-243">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-243">Optional.</span></span> <span data-ttu-id="63cd2-244">Specifica le dimensioni massime della directory in MB.</span><span class="sxs-lookup"><span data-stu-id="63cd2-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="63cd2-245">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="63cd2-246">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="63cd2-246">DataSources Element</span></span>  
 <span data-ttu-id="63cd2-247">Definisce zero o più directory di log aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="63cd2-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="63cd2-248">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="63cd2-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="63cd2-249">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="63cd2-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="63cd2-250">Definisce la directory di file di log da monitorare.</span><span class="sxs-lookup"><span data-stu-id="63cd2-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="63cd2-251">Elemento padre: [elemento DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="63cd2-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="63cd2-252">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-252">Attributes:</span></span>

|<span data-ttu-id="63cd2-253">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-253">Attribute</span></span>|<span data-ttu-id="63cd2-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-254">Type</span></span>|<span data-ttu-id="63cd2-255">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-256">**container**</span><span class="sxs-lookup"><span data-stu-id="63cd2-256">**container**</span></span>|<span data-ttu-id="63cd2-257">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-257">string</span></span>|<span data-ttu-id="63cd2-258">Nome del contenitore in cui dovrà essere trasferito il contenuto della directory.</span><span class="sxs-lookup"><span data-stu-id="63cd2-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="63cd2-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="63cd2-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-260">unsignedInt</span></span>|<span data-ttu-id="63cd2-261">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-261">Optional.</span></span> <span data-ttu-id="63cd2-262">Specifica le dimensioni massime della directory in MB.</span><span class="sxs-lookup"><span data-stu-id="63cd2-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="63cd2-263">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="63cd2-264">Elemento Absolute</span><span class="sxs-lookup"><span data-stu-id="63cd2-264">Absolute Element</span></span>  
 <span data-ttu-id="63cd2-265">Definisce un percorso assoluto della directory da monitorare con espansione dell'ambiente facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="63cd2-266">Elemento padre: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="63cd2-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="63cd2-267">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-267">Attributes:</span></span>  

|<span data-ttu-id="63cd2-268">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-268">Attribute</span></span>|<span data-ttu-id="63cd2-269">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-269">Type</span></span>|<span data-ttu-id="63cd2-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-271">**path**</span><span class="sxs-lookup"><span data-stu-id="63cd2-271">**path**</span></span>|<span data-ttu-id="63cd2-272">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-272">string</span></span>|<span data-ttu-id="63cd2-273">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-273">Required.</span></span> <span data-ttu-id="63cd2-274">Percorso assoluto della directory da monitorare.</span><span class="sxs-lookup"><span data-stu-id="63cd2-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="63cd2-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="63cd2-275">**expandEnvironment**</span></span>|<span data-ttu-id="63cd2-276">boolean</span><span class="sxs-lookup"><span data-stu-id="63cd2-276">boolean</span></span>|<span data-ttu-id="63cd2-277">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-277">Required.</span></span> <span data-ttu-id="63cd2-278">Se impostato su **true**, le variabili di ambiente nel percorso verranno espanse.</span><span class="sxs-lookup"><span data-stu-id="63cd2-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="63cd2-279">Elemento LocalResource</span><span class="sxs-lookup"><span data-stu-id="63cd2-279">LocalResource Element</span></span>  
 <span data-ttu-id="63cd2-280">Definisce un percorso relativo a una risorsa locale nella definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="63cd2-281">Elemento padre: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="63cd2-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="63cd2-282">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-282">Attributes:</span></span>  

|<span data-ttu-id="63cd2-283">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-283">Attribute</span></span>|<span data-ttu-id="63cd2-284">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-284">Type</span></span>|<span data-ttu-id="63cd2-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-286">**nome**</span><span class="sxs-lookup"><span data-stu-id="63cd2-286">**name**</span></span>|<span data-ttu-id="63cd2-287">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-287">string</span></span>|<span data-ttu-id="63cd2-288">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-288">Required.</span></span> <span data-ttu-id="63cd2-289">Nome della risorsa locale che contiene la directory da monitorare.</span><span class="sxs-lookup"><span data-stu-id="63cd2-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="63cd2-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="63cd2-290">**relativePath**</span></span>|<span data-ttu-id="63cd2-291">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-291">string</span></span>|<span data-ttu-id="63cd2-292">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-292">Required.</span></span> <span data-ttu-id="63cd2-293">Percorso relativo della risorsa locale da monitorare.</span><span class="sxs-lookup"><span data-stu-id="63cd2-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="63cd2-294">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="63cd2-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="63cd2-295">Definisce il percorso del contatore delle prestazioni da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="63cd2-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="63cd2-296">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="63cd2-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="63cd2-297">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-297">Attributes:</span></span>  

|<span data-ttu-id="63cd2-298">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-298">Attribute</span></span>|<span data-ttu-id="63cd2-299">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-299">Type</span></span>|<span data-ttu-id="63cd2-300">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="63cd2-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-302">unsignedInt</span></span>|<span data-ttu-id="63cd2-303">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-303">Optional.</span></span> <span data-ttu-id="63cd2-304">Specifica lo spazio massimo di archiviazione del file system disponibile per i dati specificati.</span><span class="sxs-lookup"><span data-stu-id="63cd2-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="63cd2-305">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-305">The default is 0.</span></span>|  
|<span data-ttu-id="63cd2-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="63cd2-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="63cd2-307">duration</span><span class="sxs-lookup"><span data-stu-id="63cd2-307">duration</span></span>|<span data-ttu-id="63cd2-308">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-308">Optional.</span></span> <span data-ttu-id="63cd2-309">Specifica l'intervallo tra trasferimenti di dati pianificati, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="63cd2-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="63cd2-310">Il valore predefinito è PT0S.</span><span class="sxs-lookup"><span data-stu-id="63cd2-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="63cd2-311">Elemento PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="63cd2-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="63cd2-312">Definisce il contatore delle prestazioni da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="63cd2-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="63cd2-313">Elemento principale: [PerformanceCounters Element](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="63cd2-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="63cd2-314">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-314">Attributes:</span></span>  

|<span data-ttu-id="63cd2-315">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-315">Attribute</span></span>|<span data-ttu-id="63cd2-316">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-316">Type</span></span>|<span data-ttu-id="63cd2-317">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="63cd2-318">**counterSpecifier**</span></span>|<span data-ttu-id="63cd2-319">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-319">string</span></span>|<span data-ttu-id="63cd2-320">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-320">Required.</span></span> <span data-ttu-id="63cd2-321">Percorso del contatore delle prestazioni da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="63cd2-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="63cd2-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="63cd2-322">**sampleRate**</span></span>|<span data-ttu-id="63cd2-323">duration</span><span class="sxs-lookup"><span data-stu-id="63cd2-323">duration</span></span>|<span data-ttu-id="63cd2-324">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-324">Required.</span></span> <span data-ttu-id="63cd2-325">Frequenza con la quale raccogliere il contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="63cd2-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="63cd2-326">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="63cd2-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="63cd2-327">Definisce i registri eventi da monitorare.</span><span class="sxs-lookup"><span data-stu-id="63cd2-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="63cd2-328">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="63cd2-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="63cd2-329">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-329">Attributes:</span></span>

|<span data-ttu-id="63cd2-330">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-330">Attribute</span></span>|<span data-ttu-id="63cd2-331">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-331">Type</span></span>|<span data-ttu-id="63cd2-332">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="63cd2-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="63cd2-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="63cd2-334">unsignedInt</span></span>|<span data-ttu-id="63cd2-335">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-335">Optional.</span></span> <span data-ttu-id="63cd2-336">Specifica lo spazio massimo di archiviazione del file system disponibile per i dati specificati.</span><span class="sxs-lookup"><span data-stu-id="63cd2-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="63cd2-337">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="63cd2-337">The default is 0.</span></span>|  
|<span data-ttu-id="63cd2-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="63cd2-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="63cd2-339">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-339">string</span></span>|<span data-ttu-id="63cd2-340">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-340">Optional.</span></span> <span data-ttu-id="63cd2-341">Specifica il livello di gravità minimo per le voci di log trasferite.</span><span class="sxs-lookup"><span data-stu-id="63cd2-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="63cd2-342">Il valore predefinito è **Non definito**.</span><span class="sxs-lookup"><span data-stu-id="63cd2-342">The default value is **Undefined**.</span></span> <span data-ttu-id="63cd2-343">Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="63cd2-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="63cd2-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="63cd2-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="63cd2-345">duration</span><span class="sxs-lookup"><span data-stu-id="63cd2-345">duration</span></span>|<span data-ttu-id="63cd2-346">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="63cd2-346">Optional.</span></span> <span data-ttu-id="63cd2-347">Specifica l'intervallo tra trasferimenti di dati pianificati, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="63cd2-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="63cd2-348">Il valore predefinito è PT0S.</span><span class="sxs-lookup"><span data-stu-id="63cd2-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="63cd2-349">Elemento DataSource</span><span class="sxs-lookup"><span data-stu-id="63cd2-349">DataSource Element</span></span>  
 <span data-ttu-id="63cd2-350">Definisce il registro eventi da monitorare.</span><span class="sxs-lookup"><span data-stu-id="63cd2-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="63cd2-351">Elemento principale: [elemento WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="63cd2-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="63cd2-352">Attributi:</span><span class="sxs-lookup"><span data-stu-id="63cd2-352">Attributes:</span></span>

|<span data-ttu-id="63cd2-353">Attributo</span><span class="sxs-lookup"><span data-stu-id="63cd2-353">Attribute</span></span>|<span data-ttu-id="63cd2-354">Tipo</span><span class="sxs-lookup"><span data-stu-id="63cd2-354">Type</span></span>|<span data-ttu-id="63cd2-355">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cd2-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="63cd2-356">**nome**</span><span class="sxs-lookup"><span data-stu-id="63cd2-356">**name**</span></span>|<span data-ttu-id="63cd2-357">string</span><span class="sxs-lookup"><span data-stu-id="63cd2-357">string</span></span>|<span data-ttu-id="63cd2-358">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="63cd2-358">Required.</span></span> <span data-ttu-id="63cd2-359">Espressione XPath che specifica il log da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="63cd2-359">An XPath expression specifying the log to collect.</span></span>|  
