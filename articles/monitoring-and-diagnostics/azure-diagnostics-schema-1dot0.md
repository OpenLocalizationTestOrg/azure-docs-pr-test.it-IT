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
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="1391b-103">Schema di configurazione di Diagnostica di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1391b-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="1391b-104">Diagnostica di Azure è contatori delle prestazioni toocollect componente utilizzato hello e altre statistiche da macchine virtuali di Azure, il set di scalabilità di macchine virtuali, Service Fabric e servizi Cloud.</span><span class="sxs-lookup"><span data-stu-id="1391b-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="1391b-105">Questa pagina è utile solo se si usa uno di questi servizi.</span><span class="sxs-lookup"><span data-stu-id="1391b-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="1391b-106">Lo strumento Diagnostica di Azure viene usato con altri prodotti di diagnostica Microsoft, quali Monitoraggio di Azure, Application Insights e Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1391b-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="1391b-107">file di configurazione di diagnostica Azure Hello definisce i valori vengono utilizzati tooinitialize hello Monitor di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="1391b-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="1391b-108">Questo file è tooinitialize utilizzate le impostazioni di configurazione quando si avvia il monitoraggio di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="1391b-109">Per impostazione predefinita, i file dello schema di configurazione diagnostica di Azure di hello è toohello installato `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span><span class="sxs-lookup"><span data-stu-id="1391b-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="1391b-110">Sostituire `<version>` con la versione di hello installato di hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1391b-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="1391b-111">file di configurazione della diagnostica Hello viene in genere utilizzata con le attività di avvio che richiedono toobe dati di diagnostica raccolti in precedenza nel processo di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="1391b-112">Per altre informazioni sull'uso di Diagnostica di Azure, vedere [Raccogliere dati di registrazione usando Diagnostica di Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="1391b-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="1391b-113">Esempio di file di configurazione della diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="1391b-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="1391b-114">Hello di esempio seguente viene illustrato un tipico file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="1391b-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="1391b-115">Spazio dei nomi DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="1391b-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="1391b-116">spazio dei nomi XML Hello per file di configurazione di diagnostica hello è:</span><span class="sxs-lookup"><span data-stu-id="1391b-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="1391b-117">Elementi dello schema</span><span class="sxs-lookup"><span data-stu-id="1391b-117">Schema Elements</span></span>  
 <span data-ttu-id="1391b-118">file di configurazione della diagnostica Hello include hello seguenti elementi.</span><span class="sxs-lookup"><span data-stu-id="1391b-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="1391b-119">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="1391b-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="1391b-120">elemento di primo livello Hello hello diagnostica del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1391b-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="1391b-121">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-121">Attributes:</span></span>

|<span data-ttu-id="1391b-122">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-122">Attribute</span></span>  |<span data-ttu-id="1391b-123">Type</span><span class="sxs-lookup"><span data-stu-id="1391b-123">Type</span></span>   |<span data-ttu-id="1391b-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1391b-124">Required</span></span>| <span data-ttu-id="1391b-125">Default</span><span class="sxs-lookup"><span data-stu-id="1391b-125">Default</span></span> | <span data-ttu-id="1391b-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="1391b-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="1391b-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="1391b-128">duration</span><span class="sxs-lookup"><span data-stu-id="1391b-128">duration</span></span>|<span data-ttu-id="1391b-129">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="1391b-129">Optional</span></span> | <span data-ttu-id="1391b-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="1391b-130">PT1M</span></span>| <span data-ttu-id="1391b-131">Specifica l'intervallo hello in cui viene eseguito il polling monitor di diagnostica hello per le modifiche di configurazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="1391b-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="1391b-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="1391b-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-133">unsignedInt</span></span>|<span data-ttu-id="1391b-134">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="1391b-134">Optional</span></span>| <span data-ttu-id="1391b-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="1391b-135">4000 MB.</span></span> <span data-ttu-id="1391b-136">Se si specifica un valore, non deve superare la quantità</span><span class="sxs-lookup"><span data-stu-id="1391b-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="1391b-137">quantità totale di Hello di archiviazione nel file system allocato per tutti i buffer di registrazione.</span><span class="sxs-lookup"><span data-stu-id="1391b-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="1391b-138">Elemento DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="1391b-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="1391b-139">Definisce una configurazione del buffer hello per i log hello generati dall'infrastruttura diagnostica sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="1391b-140">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1391b-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="1391b-141">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-141">Attributes:</span></span>

|<span data-ttu-id="1391b-142">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-142">Attribute</span></span>|<span data-ttu-id="1391b-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-143">Type</span></span>|<span data-ttu-id="1391b-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="1391b-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1391b-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-146">unsignedInt</span></span>|<span data-ttu-id="1391b-147">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-147">Optional.</span></span> <span data-ttu-id="1391b-148">Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.</span><span class="sxs-lookup"><span data-stu-id="1391b-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1391b-149">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-149">hello default is 0.</span></span>|  
|<span data-ttu-id="1391b-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="1391b-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="1391b-151">string</span><span class="sxs-lookup"><span data-stu-id="1391b-151">string</span></span>|<span data-ttu-id="1391b-152">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-152">Optional.</span></span> <span data-ttu-id="1391b-153">Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1391b-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="1391b-154">valore predefinito di Hello è **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="1391b-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="1391b-155">Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="1391b-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="1391b-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1391b-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1391b-157">duration</span><span class="sxs-lookup"><span data-stu-id="1391b-157">duration</span></span>|<span data-ttu-id="1391b-158">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-158">Optional.</span></span> <span data-ttu-id="1391b-159">Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="1391b-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1391b-160">valore predefinito di Hello è PT0S.</span><span class="sxs-lookup"><span data-stu-id="1391b-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="1391b-161">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="1391b-161">Logs Element</span></span>  
 <span data-ttu-id="1391b-162">Definisce una configurazione del buffer hello per i log di Azure di base.</span><span class="sxs-lookup"><span data-stu-id="1391b-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="1391b-163">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1391b-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="1391b-164">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-164">Attributes:</span></span>  

|<span data-ttu-id="1391b-165">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-165">Attribute</span></span>|<span data-ttu-id="1391b-166">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-166">Type</span></span>|<span data-ttu-id="1391b-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1391b-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-169">unsignedInt</span></span>|<span data-ttu-id="1391b-170">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-170">Optional.</span></span> <span data-ttu-id="1391b-171">Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.</span><span class="sxs-lookup"><span data-stu-id="1391b-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1391b-172">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-172">hello default is 0.</span></span>|  
|<span data-ttu-id="1391b-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="1391b-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="1391b-174">string</span><span class="sxs-lookup"><span data-stu-id="1391b-174">string</span></span>|<span data-ttu-id="1391b-175">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-175">Optional.</span></span> <span data-ttu-id="1391b-176">Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1391b-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="1391b-177">valore predefinito di Hello è **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="1391b-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="1391b-178">Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="1391b-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="1391b-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1391b-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1391b-180">duration</span><span class="sxs-lookup"><span data-stu-id="1391b-180">duration</span></span>|<span data-ttu-id="1391b-181">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-181">Optional.</span></span> <span data-ttu-id="1391b-182">Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="1391b-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1391b-183">valore predefinito di Hello è PT0S.</span><span class="sxs-lookup"><span data-stu-id="1391b-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="1391b-184">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="1391b-184">Directories Element</span></span>  
<span data-ttu-id="1391b-185">Definisce la configurazione di hello buffer per i log basati su file che è possibile definire.</span><span class="sxs-lookup"><span data-stu-id="1391b-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="1391b-186">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1391b-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="1391b-187">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-187">Attributes:</span></span>  

|<span data-ttu-id="1391b-188">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-188">Attribute</span></span>|<span data-ttu-id="1391b-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-189">Type</span></span>|<span data-ttu-id="1391b-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1391b-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-192">unsignedInt</span></span>|<span data-ttu-id="1391b-193">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-193">Optional.</span></span> <span data-ttu-id="1391b-194">Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.</span><span class="sxs-lookup"><span data-stu-id="1391b-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1391b-195">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-195">hello default is 0.</span></span>|  
|<span data-ttu-id="1391b-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1391b-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1391b-197">duration</span><span class="sxs-lookup"><span data-stu-id="1391b-197">duration</span></span>|<span data-ttu-id="1391b-198">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-198">Optional.</span></span> <span data-ttu-id="1391b-199">Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="1391b-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1391b-200">valore predefinito di Hello è PT0S.</span><span class="sxs-lookup"><span data-stu-id="1391b-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="1391b-201">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="1391b-201">CrashDumps Element</span></span>  
 <span data-ttu-id="1391b-202">Definisce hello directory dei dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="1391b-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="1391b-203">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1391b-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="1391b-204">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-204">Attributes:</span></span>  

|<span data-ttu-id="1391b-205">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-205">Attribute</span></span>|<span data-ttu-id="1391b-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-206">Type</span></span>|<span data-ttu-id="1391b-207">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-208">**container**</span><span class="sxs-lookup"><span data-stu-id="1391b-208">**container**</span></span>|<span data-ttu-id="1391b-209">string</span><span class="sxs-lookup"><span data-stu-id="1391b-209">string</span></span>|<span data-ttu-id="1391b-210">nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1391b-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1391b-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1391b-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-212">unsignedInt</span></span>|<span data-ttu-id="1391b-213">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-213">Optional.</span></span> <span data-ttu-id="1391b-214">Specifica dimensioni massime di hello della directory hello in megabyte.</span><span class="sxs-lookup"><span data-stu-id="1391b-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1391b-215">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="1391b-216">Elemento FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="1391b-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="1391b-217">Definisce hello directory dei log richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="1391b-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="1391b-218">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1391b-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="1391b-219">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-219">Attributes:</span></span>  

|<span data-ttu-id="1391b-220">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-220">Attribute</span></span>|<span data-ttu-id="1391b-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-221">Type</span></span>|<span data-ttu-id="1391b-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-223">**container**</span><span class="sxs-lookup"><span data-stu-id="1391b-223">**container**</span></span>|<span data-ttu-id="1391b-224">string</span><span class="sxs-lookup"><span data-stu-id="1391b-224">string</span></span>|<span data-ttu-id="1391b-225">nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1391b-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1391b-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1391b-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-227">unsignedInt</span></span>|<span data-ttu-id="1391b-228">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-228">Optional.</span></span> <span data-ttu-id="1391b-229">Specifica dimensioni massime di hello della directory hello in megabyte.</span><span class="sxs-lookup"><span data-stu-id="1391b-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1391b-230">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="1391b-231">Elemento IISLogs</span><span class="sxs-lookup"><span data-stu-id="1391b-231">IISLogs Element</span></span>  
 <span data-ttu-id="1391b-232">Definisce hello directory dei log IIS.</span><span class="sxs-lookup"><span data-stu-id="1391b-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="1391b-233">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1391b-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="1391b-234">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-234">Attributes:</span></span>  

|<span data-ttu-id="1391b-235">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-235">Attribute</span></span>|<span data-ttu-id="1391b-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-236">Type</span></span>|<span data-ttu-id="1391b-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-238">**container**</span><span class="sxs-lookup"><span data-stu-id="1391b-238">**container**</span></span>|<span data-ttu-id="1391b-239">string</span><span class="sxs-lookup"><span data-stu-id="1391b-239">string</span></span>|<span data-ttu-id="1391b-240">nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1391b-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1391b-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1391b-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-242">unsignedInt</span></span>|<span data-ttu-id="1391b-243">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-243">Optional.</span></span> <span data-ttu-id="1391b-244">Specifica dimensioni massime di hello della directory hello in megabyte.</span><span class="sxs-lookup"><span data-stu-id="1391b-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1391b-245">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="1391b-246">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="1391b-246">DataSources Element</span></span>  
 <span data-ttu-id="1391b-247">Definisce zero o più directory di log aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="1391b-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="1391b-248">Elemento padre: [elemento Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="1391b-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="1391b-249">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="1391b-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="1391b-250">Definisce la directory hello di toomonitor i file di log.</span><span class="sxs-lookup"><span data-stu-id="1391b-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="1391b-251">Elemento padre: [elemento DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="1391b-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="1391b-252">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-252">Attributes:</span></span>

|<span data-ttu-id="1391b-253">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-253">Attribute</span></span>|<span data-ttu-id="1391b-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-254">Type</span></span>|<span data-ttu-id="1391b-255">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-256">**container**</span><span class="sxs-lookup"><span data-stu-id="1391b-256">**container**</span></span>|<span data-ttu-id="1391b-257">string</span><span class="sxs-lookup"><span data-stu-id="1391b-257">string</span></span>|<span data-ttu-id="1391b-258">nome Hello del contenitore di hello in cui il contenuto di hello della directory hello è toobe trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1391b-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="1391b-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="1391b-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-260">unsignedInt</span></span>|<span data-ttu-id="1391b-261">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-261">Optional.</span></span> <span data-ttu-id="1391b-262">Specifica dimensioni massime di hello della directory hello in megabyte.</span><span class="sxs-lookup"><span data-stu-id="1391b-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="1391b-263">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="1391b-264">Elemento Absolute</span><span class="sxs-lookup"><span data-stu-id="1391b-264">Absolute Element</span></span>  
 <span data-ttu-id="1391b-265">Definisce un percorso assoluto di hello directory toomonitor con espansione dell'ambiente facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="1391b-266">Elemento padre: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1391b-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="1391b-267">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-267">Attributes:</span></span>  

|<span data-ttu-id="1391b-268">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-268">Attribute</span></span>|<span data-ttu-id="1391b-269">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-269">Type</span></span>|<span data-ttu-id="1391b-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-271">**path**</span><span class="sxs-lookup"><span data-stu-id="1391b-271">**path**</span></span>|<span data-ttu-id="1391b-272">string</span><span class="sxs-lookup"><span data-stu-id="1391b-272">string</span></span>|<span data-ttu-id="1391b-273">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1391b-273">Required.</span></span> <span data-ttu-id="1391b-274">Hello toomonitor directory toohello di percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="1391b-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="1391b-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="1391b-275">**expandEnvironment**</span></span>|<span data-ttu-id="1391b-276">boolean</span><span class="sxs-lookup"><span data-stu-id="1391b-276">boolean</span></span>|<span data-ttu-id="1391b-277">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1391b-277">Required.</span></span> <span data-ttu-id="1391b-278">Se impostato troppo**true**, le variabili di ambiente nel percorso hello vengono espanse.</span><span class="sxs-lookup"><span data-stu-id="1391b-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="1391b-279">Elemento LocalResource</span><span class="sxs-lookup"><span data-stu-id="1391b-279">LocalResource Element</span></span>  
 <span data-ttu-id="1391b-280">Definisce una risorsa locale tooa relativo percorso definita nella definizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="1391b-281">Elemento padre: [elemento DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1391b-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="1391b-282">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-282">Attributes:</span></span>  

|<span data-ttu-id="1391b-283">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-283">Attribute</span></span>|<span data-ttu-id="1391b-284">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-284">Type</span></span>|<span data-ttu-id="1391b-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-286">**nome**</span><span class="sxs-lookup"><span data-stu-id="1391b-286">**name**</span></span>|<span data-ttu-id="1391b-287">string</span><span class="sxs-lookup"><span data-stu-id="1391b-287">string</span></span>|<span data-ttu-id="1391b-288">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1391b-288">Required.</span></span> <span data-ttu-id="1391b-289">nome Hello della risorsa locale hello contenente toomonitor directory hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="1391b-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="1391b-290">**relativePath**</span></span>|<span data-ttu-id="1391b-291">string</span><span class="sxs-lookup"><span data-stu-id="1391b-291">string</span></span>|<span data-ttu-id="1391b-292">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1391b-292">Required.</span></span> <span data-ttu-id="1391b-293">Hello toomonitor di percorso relativo toohello risorsa locale.</span><span class="sxs-lookup"><span data-stu-id="1391b-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="1391b-294">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="1391b-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="1391b-295">Definisce il toocollect contatore delle prestazioni di hello percorso toohello.</span><span class="sxs-lookup"><span data-stu-id="1391b-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="1391b-296">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1391b-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="1391b-297">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-297">Attributes:</span></span>  

|<span data-ttu-id="1391b-298">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-298">Attribute</span></span>|<span data-ttu-id="1391b-299">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-299">Type</span></span>|<span data-ttu-id="1391b-300">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1391b-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-302">unsignedInt</span></span>|<span data-ttu-id="1391b-303">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-303">Optional.</span></span> <span data-ttu-id="1391b-304">Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.</span><span class="sxs-lookup"><span data-stu-id="1391b-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1391b-305">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-305">hello default is 0.</span></span>|  
|<span data-ttu-id="1391b-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1391b-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1391b-307">duration</span><span class="sxs-lookup"><span data-stu-id="1391b-307">duration</span></span>|<span data-ttu-id="1391b-308">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-308">Optional.</span></span> <span data-ttu-id="1391b-309">Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="1391b-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1391b-310">valore predefinito di Hello è PT0S.</span><span class="sxs-lookup"><span data-stu-id="1391b-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="1391b-311">Elemento PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="1391b-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="1391b-312">Definisce toocollect contatore delle prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="1391b-313">Elemento principale: [PerformanceCounters Element](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="1391b-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="1391b-314">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-314">Attributes:</span></span>  

|<span data-ttu-id="1391b-315">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-315">Attribute</span></span>|<span data-ttu-id="1391b-316">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-316">Type</span></span>|<span data-ttu-id="1391b-317">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="1391b-318">**counterSpecifier**</span></span>|<span data-ttu-id="1391b-319">string</span><span class="sxs-lookup"><span data-stu-id="1391b-319">string</span></span>|<span data-ttu-id="1391b-320">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1391b-320">Required.</span></span> <span data-ttu-id="1391b-321">Hello toocollect contatore delle prestazioni toohello di percorso.</span><span class="sxs-lookup"><span data-stu-id="1391b-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="1391b-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="1391b-322">**sampleRate**</span></span>|<span data-ttu-id="1391b-323">duration</span><span class="sxs-lookup"><span data-stu-id="1391b-323">duration</span></span>|<span data-ttu-id="1391b-324">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1391b-324">Required.</span></span> <span data-ttu-id="1391b-325">frequenza di Hello in cui hello deve essere raccolti contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1391b-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="1391b-326">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="1391b-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="1391b-327">Definisce hello toomonitor di registri eventi.</span><span class="sxs-lookup"><span data-stu-id="1391b-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="1391b-328">Elemento padre: [elemento DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1391b-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="1391b-329">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-329">Attributes:</span></span>

|<span data-ttu-id="1391b-330">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-330">Attribute</span></span>|<span data-ttu-id="1391b-331">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-331">Type</span></span>|<span data-ttu-id="1391b-332">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="1391b-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="1391b-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="1391b-334">unsignedInt</span></span>|<span data-ttu-id="1391b-335">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-335">Optional.</span></span> <span data-ttu-id="1391b-336">Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.</span><span class="sxs-lookup"><span data-stu-id="1391b-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="1391b-337">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="1391b-337">hello default is 0.</span></span>|  
|<span data-ttu-id="1391b-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="1391b-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="1391b-339">string</span><span class="sxs-lookup"><span data-stu-id="1391b-339">string</span></span>|<span data-ttu-id="1391b-340">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-340">Optional.</span></span> <span data-ttu-id="1391b-341">Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1391b-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="1391b-342">valore predefinito di Hello è **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="1391b-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="1391b-343">Altri valori possibili sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="1391b-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="1391b-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="1391b-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="1391b-345">duration</span><span class="sxs-lookup"><span data-stu-id="1391b-345">duration</span></span>|<span data-ttu-id="1391b-346">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1391b-346">Optional.</span></span> <span data-ttu-id="1391b-347">Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="1391b-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="1391b-348">valore predefinito di Hello è PT0S.</span><span class="sxs-lookup"><span data-stu-id="1391b-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="1391b-349">Elemento DataSource</span><span class="sxs-lookup"><span data-stu-id="1391b-349">DataSource Element</span></span>  
 <span data-ttu-id="1391b-350">Definisce toomonitor registro eventi di hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="1391b-351">Elemento principale: [elemento WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="1391b-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="1391b-352">Attributi:</span><span class="sxs-lookup"><span data-stu-id="1391b-352">Attributes:</span></span>

|<span data-ttu-id="1391b-353">Attributo</span><span class="sxs-lookup"><span data-stu-id="1391b-353">Attribute</span></span>|<span data-ttu-id="1391b-354">Tipo</span><span class="sxs-lookup"><span data-stu-id="1391b-354">Type</span></span>|<span data-ttu-id="1391b-355">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1391b-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="1391b-356">**nome**</span><span class="sxs-lookup"><span data-stu-id="1391b-356">**name**</span></span>|<span data-ttu-id="1391b-357">string</span><span class="sxs-lookup"><span data-stu-id="1391b-357">string</span></span>|<span data-ttu-id="1391b-358">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1391b-358">Required.</span></span> <span data-ttu-id="1391b-359">Un'espressione XPath specifica toocollect log hello.</span><span class="sxs-lookup"><span data-stu-id="1391b-359">An XPath expression specifying hello log toocollect.</span></span>|  
