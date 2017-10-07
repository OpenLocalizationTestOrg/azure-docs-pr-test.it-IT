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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="ff023-103">Schema di configurazione di Diagnostica di Azure 1.3 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="ff023-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="ff023-104">Hello estensione diagnostica di Azure è il componente di hello utilizzato toocollect contatori delle prestazioni e altre statistiche da:</span><span class="sxs-lookup"><span data-stu-id="ff023-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="ff023-105">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="ff023-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="ff023-106">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ff023-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="ff023-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff023-107">Service Fabric</span></span> 
> - <span data-ttu-id="ff023-108">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="ff023-108">Cloud Services</span></span> 
> - <span data-ttu-id="ff023-109">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="ff023-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="ff023-110">Questa pagina è utile solo se si usa uno di questi servizi.</span><span class="sxs-lookup"><span data-stu-id="ff023-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="ff023-111">Questa pagina è valida per le versioni 1.3 e più recenti (Azure SDK 2.4 e versioni più recenti).</span><span class="sxs-lookup"><span data-stu-id="ff023-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="ff023-112">Le sezioni di configurazione più recenti sono tooshow commentata nella versione sono stati aggiunti.</span><span class="sxs-lookup"><span data-stu-id="ff023-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="ff023-113">file di configurazione di Hello descritti di seguito è tooset utilizzate le impostazioni di configurazione quando si avvia il monitoraggio di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="ff023-114">estensione Hello viene utilizzato in combinazione con altri prodotti Microsoft, diagnostica quali monitoraggio di Azure, Application Insights e Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="ff023-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="ff023-115">Scarica definizione dello schema file di configurazione pubblica hello eseguendo hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="ff023-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="ff023-116">Per altre informazioni su Diagnostica di Azure, vedere [Estensione di Diagnostica di Azure](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ff023-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="ff023-117">Esempio di file di configurazione della diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="ff023-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="ff023-118">Hello di esempio seguente viene illustrato un tipico file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="ff023-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="ff023-119">Equivalente in JSON del file di configurazione XML precedente hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="ff023-120">Hello PublicConfig e PrivateConfig sono separate, poiché nella maggior parte dei casi di utilizzo di json, vengono passati come variabili diverse.</span><span class="sxs-lookup"><span data-stu-id="ff023-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="ff023-121">Alcuni esempi sono i modelli di Resource Manager, i set di scalabilità di macchine virtuali PowerShell e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff023-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="ff023-122">Come leggere questa pagina</span><span class="sxs-lookup"><span data-stu-id="ff023-122">Reading this page</span></span>  
 <span data-ttu-id="ff023-123">Hello i tag seguenti sono approssimativamente nell'ordine illustrato nell'esempio sopra riportato hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="ff023-124">Se non viene visualizzata una descrizione completa in cui si prevede, pagina di ricerca hello per hello elemento o attributo.</span><span class="sxs-lookup"><span data-stu-id="ff023-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="ff023-125">Tipi di attributi comuni</span><span class="sxs-lookup"><span data-stu-id="ff023-125">Common Attribute Types</span></span>  
 <span data-ttu-id="ff023-126">L'attributo **scheduledTransferPeriod** è presente in diversi elementi.</span><span class="sxs-lookup"><span data-stu-id="ff023-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="ff023-127">È l'intervallo di hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="ff023-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="ff023-128">il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ff023-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="ff023-129">Elemento DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff023-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="ff023-130">*Albero: radice - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ff023-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="ff023-131">Aggiunto nella versione 1.3.</span><span class="sxs-lookup"><span data-stu-id="ff023-131">Added in version 1.3.</span></span>  

<span data-ttu-id="ff023-132">elemento di primo livello Hello hello diagnostica del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ff023-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="ff023-133">**Attributo** xmlns - hello spazio dei nomi XML per il file di configurazione della diagnostica hello è:</span><span class="sxs-lookup"><span data-stu-id="ff023-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="ff023-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff023-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="ff023-135">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-135">Child Elements</span></span>|<span data-ttu-id="ff023-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="ff023-137">**PublicConfig**</span></span>|<span data-ttu-id="ff023-138">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ff023-138">Required.</span></span> <span data-ttu-id="ff023-139">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="ff023-140">**PrivateConfig**</span></span>|<span data-ttu-id="ff023-141">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="ff023-141">Optional.</span></span> <span data-ttu-id="ff023-142">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="ff023-143">**IsEnabled**</span></span>|<span data-ttu-id="ff023-144">Booleano.</span><span class="sxs-lookup"><span data-stu-id="ff023-144">Boolean.</span></span> <span data-ttu-id="ff023-145">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="ff023-146">Elemento PublicConfig</span><span class="sxs-lookup"><span data-stu-id="ff023-146">PublicConfig Element</span></span>  
 <span data-ttu-id="ff023-147">*Albero: radice - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="ff023-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="ff023-148">Descrive una configurazione della diagnostica pubblica hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="ff023-149">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-149">Child Elements</span></span>|<span data-ttu-id="ff023-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="ff023-151">**WadCfg**</span></span>|<span data-ttu-id="ff023-152">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ff023-152">Required.</span></span> <span data-ttu-id="ff023-153">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="ff023-154">**StorageAccount**</span></span>|<span data-ttu-id="ff023-155">nome Hello hello Azure account toostore hello dei dati di archiviazione in.</span><span class="sxs-lookup"><span data-stu-id="ff023-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="ff023-156">Può anche essere specificato come parametro quando si esegue il cmdlet Set-AzureServiceDiagnosticsExtension hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="ff023-157">**Tipo di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="ff023-157">**StorageType**</span></span>|<span data-ttu-id="ff023-158">Può essere *Table*, *Blob* o *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="ff023-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="ff023-159">Table è il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="ff023-159">Table is default.</span></span> <span data-ttu-id="ff023-160">Quando viene scelto TableAndBlob, dati di diagnostica vengono scritti due volte, una volta tooeach tipo.</span><span class="sxs-lookup"><span data-stu-id="ff023-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="ff023-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="ff023-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="ff023-162">directory di Hello nella macchina virtuale hello in hello Monitoring Agent memorizza dati dell'evento.</span><span class="sxs-lookup"><span data-stu-id="ff023-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="ff023-163">Se non impostato, viene utilizzato directory predefinita hello:</span><span class="sxs-lookup"><span data-stu-id="ff023-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="ff023-164">Per un ruolo di lavoro/Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="ff023-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="ff023-165">Per una macchina virtuale: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="ff023-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="ff023-166">Gli attributi obbligatori sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff023-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="ff023-167">- **percorso** : hello directory hello sistema toobe utilizzato dagli strumenti di diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff023-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="ff023-168">- **expandEnvironment** -controlla se le variabili di ambiente vengono espanse nel nome di percorso hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="ff023-169">Elemento WadCFG</span><span class="sxs-lookup"><span data-stu-id="ff023-169">WadCFG Element</span></span>  
 <span data-ttu-id="ff023-170">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="ff023-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="ff023-171">Identifica e configura hello toobe di dati di telemetria raccolti.</span><span class="sxs-lookup"><span data-stu-id="ff023-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="ff023-172">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff023-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="ff023-173">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ff023-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="ff023-174">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ff023-174">Required</span></span> 

|<span data-ttu-id="ff023-175">Attributi</span><span class="sxs-lookup"><span data-stu-id="ff023-175">Attributes</span></span>|<span data-ttu-id="ff023-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="ff023-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="ff023-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="ff023-178">quantità massima di Hello di spazio su disco locale che può essere utilizzata da hello vari tipi di dati di diagnostica raccolti tramite diagnostica Azure.</span><span class="sxs-lookup"><span data-stu-id="ff023-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="ff023-179">Hello predefinito è 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="ff023-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="ff023-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="ff023-180">**useProxyServer**</span></span> | <span data-ttu-id="ff023-181">Configurare impostazioni del server proxy hello toouse diagnostica di Azure come set di impostazioni di Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ff023-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="ff023-182">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-182">Child Elements</span></span>|<span data-ttu-id="ff023-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="ff023-184">**CrashDumps**</span></span>|<span data-ttu-id="ff023-185">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="ff023-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="ff023-187">Abilita la raccolta dei log generati da Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff023-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="ff023-188">log dell'infrastruttura diagnostica Hello sono utili per la risoluzione dei problemi hello stesso sistema di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ff023-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="ff023-189">Gli attributi facoltativi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff023-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ff023-190">- **scheduledTransferLogLevelFilter** -consente di configurare il livello minimo di gravità hello di hello log raccolti.</span><span class="sxs-lookup"><span data-stu-id="ff023-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="ff023-191">- **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="ff023-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="ff023-192">il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ff023-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="ff023-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="ff023-193">**Directories**</span></span>|<span data-ttu-id="ff023-194">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="ff023-195">**EtwProviders**</span></span>|<span data-ttu-id="ff023-196">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-197">**Metriche**</span><span class="sxs-lookup"><span data-stu-id="ff023-197">**Metrics**</span></span>|<span data-ttu-id="ff023-198">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="ff023-199">**PerformanceCounters**</span></span>|<span data-ttu-id="ff023-200">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="ff023-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="ff023-201">**WindowsEventLog**</span></span>|<span data-ttu-id="ff023-202">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="ff023-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="ff023-203">**DockerSources**</span></span>|<span data-ttu-id="ff023-204">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="ff023-205">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="ff023-205">CrashDumps Element</span></span>  
 <span data-ttu-id="ff023-206">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="ff023-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="ff023-207">Abilitare la raccolta di hello dei dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="ff023-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="ff023-208">Attributi</span><span class="sxs-lookup"><span data-stu-id="ff023-208">Attributes</span></span>|<span data-ttu-id="ff023-209">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="ff023-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="ff023-210">**containerName**</span></span>|<span data-ttu-id="ff023-211">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-211">Optional.</span></span> <span data-ttu-id="ff023-212">nome di Hello del contenitore blob hello in toobe di account del servizio di archiviazione Azure utilizzato toostore arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="ff023-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="ff023-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="ff023-213">**crashDumpType**</span></span>|<span data-ttu-id="ff023-214">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-214">Optional.</span></span>  <span data-ttu-id="ff023-215">Consente di configurare diagnostica Azure toocollect completo o breve anomalo.</span><span class="sxs-lookup"><span data-stu-id="ff023-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="ff023-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="ff023-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="ff023-217">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-217">Optional.</span></span>  <span data-ttu-id="ff023-218">Consente di configurare la percentuale hello di **overallQuotaInMB** toobe riservato per il dump di arresto anomalo in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ff023-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="ff023-219">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-219">Child Elements</span></span>|<span data-ttu-id="ff023-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ff023-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="ff023-222">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ff023-222">Required.</span></span> <span data-ttu-id="ff023-223">Definisce i valori di configurazione di ogni processo.</span><span class="sxs-lookup"><span data-stu-id="ff023-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="ff023-224">è necessario anche Hello seguente attributo:</span><span class="sxs-lookup"><span data-stu-id="ff023-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="ff023-225">**processName** : hello nome del processo di hello da diagnostica di Azure toocollect un dump di arresto anomalo del sistema per.</span><span class="sxs-lookup"><span data-stu-id="ff023-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="ff023-226">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="ff023-226">Directories Element</span></span> 
 <span data-ttu-id="ff023-227">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories*</span><span class="sxs-lookup"><span data-stu-id="ff023-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="ff023-228">Abilita hello hello contenuto di una directory della raccolta, i log delle richieste di accesso e/o di log di IIS non riuscite di IIS.</span><span class="sxs-lookup"><span data-stu-id="ff023-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="ff023-229">Attributo **scheduledTransferPeriod** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ff023-230">Vedere la spiegazione indicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff023-230">See explanation earlier.</span></span>  

|<span data-ttu-id="ff023-231">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-231">Child Elements</span></span>|<span data-ttu-id="ff023-232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="ff023-233">**IISLogs**</span></span>|<span data-ttu-id="ff023-234">Tra cui questo elemento di configurazione hello abilita la raccolta di hello di log di IIS:</span><span class="sxs-lookup"><span data-stu-id="ff023-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="ff023-235">**containerName** -nome hello del contenitore blob hello in toobe di account del servizio di archiviazione Azure utilizzato toostore hello log di IIS.</span><span class="sxs-lookup"><span data-stu-id="ff023-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="ff023-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="ff023-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="ff023-237">Tra cui questo elemento di configurazione hello abilita la raccolta dei registri sul sito IIS tooan richieste non riuscite o l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ff023-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="ff023-238">È anche necessario abilitare le opzioni di traccia sotto **system.WebServer** in **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="ff023-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="ff023-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="ff023-239">**DataSources**</span></span>|<span data-ttu-id="ff023-240">Un elenco di directory toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ff023-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="ff023-241">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="ff023-241">DataSources Element</span></span>  
 <span data-ttu-id="ff023-242">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="ff023-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="ff023-243">Un elenco di directory toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ff023-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="ff023-244">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-244">Child Elements</span></span>|<span data-ttu-id="ff023-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ff023-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="ff023-247">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ff023-247">Required.</span></span> <span data-ttu-id="ff023-248">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="ff023-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="ff023-249">**containerName** : hello nome del contenitore blob hello nell'account di archiviazione di Azure che toobe utilizzato i file di log toostore hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="ff023-250">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff023-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="ff023-251">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ff023-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="ff023-252">Può includere entrambi hello **assoluto** o **LocalResource** elemento ma non entrambi.</span><span class="sxs-lookup"><span data-stu-id="ff023-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="ff023-253">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-253">Child Elements</span></span>|<span data-ttu-id="ff023-254">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="ff023-255">**Absolute**</span></span>|<span data-ttu-id="ff023-256">Hello toomonitor directory toohello di percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="ff023-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="ff023-257">Hello gli attributi seguenti è necessario:</span><span class="sxs-lookup"><span data-stu-id="ff023-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="ff023-258">- **Percorso** -hello toomonitor directory toohello di percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="ff023-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="ff023-259">- **expandEnvironment**: definisce se le variabili di ambiente vengono espanse in Path.</span><span class="sxs-lookup"><span data-stu-id="ff023-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="ff023-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="ff023-260">**LocalResource**</span></span>|<span data-ttu-id="ff023-261">Hello toomonitor di percorso relativo tooa risorsa locale.</span><span class="sxs-lookup"><span data-stu-id="ff023-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="ff023-262">Gli attributi obbligatori sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff023-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="ff023-263">- **Nome** -hello risorsa locale contenente hello directory toomonitor</span><span class="sxs-lookup"><span data-stu-id="ff023-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="ff023-264">- **relativePath** -hello tooName relativo percorso contenente hello directory toomonitor</span><span class="sxs-lookup"><span data-stu-id="ff023-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="ff023-265">Elemento EtwProviders</span><span class="sxs-lookup"><span data-stu-id="ff023-265">EtwProviders Element</span></span>  
 <span data-ttu-id="ff023-266">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="ff023-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="ff023-267">Configura la raccolta di eventi ETW da EventSource e/o da provider basati su manifesti ETW.</span><span class="sxs-lookup"><span data-stu-id="ff023-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="ff023-268">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-268">Child Elements</span></span>|<span data-ttu-id="ff023-269">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ff023-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="ff023-271">Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ff023-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="ff023-272">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="ff023-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="ff023-273">**provider** -nome della classe di evento EventSource hello hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="ff023-274">Gli attributi facoltativi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff023-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ff023-275">- **scheduledTransferLogLevelFilter** -hello account di archiviazione tooyour tootransfer livello minimo di gravità.</span><span class="sxs-lookup"><span data-stu-id="ff023-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="ff023-276">- **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="ff023-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="ff023-277">il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ff023-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="ff023-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ff023-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="ff023-279">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="ff023-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="ff023-280">**provider** -GUID del provider di eventi hello hello</span><span class="sxs-lookup"><span data-stu-id="ff023-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="ff023-281">Gli attributi facoltativi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff023-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="ff023-282">- **scheduledTransferLogLevelFilter** -hello account di archiviazione tooyour tootransfer livello minimo di gravità.</span><span class="sxs-lookup"><span data-stu-id="ff023-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="ff023-283">- **scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="ff023-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="ff023-284">il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ff023-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="ff023-285">Elemento EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff023-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="ff023-286">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ff023-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="ff023-287">Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ff023-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="ff023-288">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-288">Child Elements</span></span>|<span data-ttu-id="ff023-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="ff023-290">**DefaultEvents**</span></span>|<span data-ttu-id="ff023-291">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="ff023-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="ff023-292">**eventDestination** : hello nome di eventi di hello tabella toostore hello in</span><span class="sxs-lookup"><span data-stu-id="ff023-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="ff023-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="ff023-293">**Event**</span></span>|<span data-ttu-id="ff023-294">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="ff023-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="ff023-295">**ID** -id hello dell'evento di hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="ff023-296">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="ff023-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ff023-297">**eventDestination** : hello nome di eventi di hello tabella toostore hello in</span><span class="sxs-lookup"><span data-stu-id="ff023-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="ff023-298">Elemento EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff023-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="ff023-299">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="ff023-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="ff023-300">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-300">Child Elements</span></span>|<span data-ttu-id="ff023-301">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="ff023-302">**DefaultEvents**</span></span>|<span data-ttu-id="ff023-303">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="ff023-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ff023-304">**eventDestination** : hello nome di eventi di hello tabella toostore hello in</span><span class="sxs-lookup"><span data-stu-id="ff023-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="ff023-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="ff023-305">**Event**</span></span>|<span data-ttu-id="ff023-306">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="ff023-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="ff023-307">**ID** -id hello dell'evento di hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="ff023-308">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="ff023-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ff023-309">**eventDestination** : hello nome di eventi di hello tabella toostore hello in</span><span class="sxs-lookup"><span data-stu-id="ff023-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="ff023-310">Elemento Metrics</span><span class="sxs-lookup"><span data-stu-id="ff023-310">Metrics Element</span></span>  
 <span data-ttu-id="ff023-311">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="ff023-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="ff023-312">Consente di toogenerate una tabella del contatore delle prestazioni che è ottimizzata per le query veloce.</span><span class="sxs-lookup"><span data-stu-id="ff023-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="ff023-313">Ogni contatore delle prestazioni che è definito in hello **PerformanceCounters** elemento viene archiviato nella tabella di metriche hello nella tabella di addizione toohello contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ff023-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="ff023-314">Hello **resourceId** attributo è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ff023-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="ff023-315">ID di risorsa Hello della macchina virtuale si distribuisce la diagnostica di Azure per hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="ff023-316">Ottenere hello **resourceID** da hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff023-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ff023-317">Selezionare **Esplora** -> **Gruppi di risorse** -> **<Nome\>**.</span><span class="sxs-lookup"><span data-stu-id="ff023-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="ff023-318">Fare clic su hello **proprietà** riquadro e copiare il valore di hello hello **ID** campo.</span><span class="sxs-lookup"><span data-stu-id="ff023-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="ff023-319">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-319">Child Elements</span></span>|<span data-ttu-id="ff023-320">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="ff023-321">**MetricAggregation**</span></span>|<span data-ttu-id="ff023-322">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="ff023-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="ff023-323">**scheduledTransferPeriod** -intervallo hello tra i trasferimenti pianificati toostorage arrotondato per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="ff023-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="ff023-324">il valore di Hello è un [XML "Tipo di dati di durata".](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="ff023-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="ff023-325">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="ff023-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="ff023-326">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="ff023-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="ff023-327">Abilita la raccolta di hello dei contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ff023-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="ff023-328">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="ff023-328">Optional attribute:</span></span>  

 <span data-ttu-id="ff023-329">Attributo **scheduledTransferPeriod** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ff023-330">Vedere la spiegazione indicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff023-330">See explanation earlier.</span></span>

|<span data-ttu-id="ff023-331">Elemento figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-331">Child Element</span></span>|<span data-ttu-id="ff023-332">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="ff023-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ff023-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="ff023-334">Hello gli attributi seguenti è necessario:</span><span class="sxs-lookup"><span data-stu-id="ff023-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="ff023-335">- **counterSpecifier** : hello Nome hello contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ff023-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="ff023-336">ad esempio `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="ff023-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="ff023-337">tooget un elenco di prestazioni contatori sull'host, eseguire il comando di hello `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="ff023-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="ff023-338">- **sampleRate** -frequenza hello del contatore.</span><span class="sxs-lookup"><span data-stu-id="ff023-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="ff023-339">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="ff023-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="ff023-340">**unità** -unità di misura del contatore hello di hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="ff023-341">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="ff023-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="ff023-342">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="ff023-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="ff023-343">Abilita la raccolta di hello nei registri eventi di Windows.</span><span class="sxs-lookup"><span data-stu-id="ff023-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="ff023-344">Attributo **scheduledTransferPeriod** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="ff023-345">Vedere la spiegazione indicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff023-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="ff023-346">Elemento figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-346">Child Element</span></span>|<span data-ttu-id="ff023-347">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="ff023-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="ff023-348">**DataSource**</span></span>|<span data-ttu-id="ff023-349">toocollect i registri eventi di Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="ff023-350">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="ff023-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="ff023-351">**nome** -query XPath hello che descrive toobe gli eventi di windows hello raccolti.</span><span class="sxs-lookup"><span data-stu-id="ff023-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="ff023-352">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ff023-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="ff023-353">specificare tutti gli eventi, toocollect "*"</span><span class="sxs-lookup"><span data-stu-id="ff023-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="ff023-354">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="ff023-354">Logs Element</span></span>  
 <span data-ttu-id="ff023-355">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="ff023-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="ff023-356">Presente nella versione 1.0 e 1.1.</span><span class="sxs-lookup"><span data-stu-id="ff023-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="ff023-357">Assente nella versione 1.2.</span><span class="sxs-lookup"><span data-stu-id="ff023-357">Missing in 1.2.</span></span> <span data-ttu-id="ff023-358">Aggiunto nuovamente nella versione 1.3.</span><span class="sxs-lookup"><span data-stu-id="ff023-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="ff023-359">Definisce una configurazione del buffer hello per i log di Azure di base.</span><span class="sxs-lookup"><span data-stu-id="ff023-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="ff023-360">Attributo</span><span class="sxs-lookup"><span data-stu-id="ff023-360">Attribute</span></span>|<span data-ttu-id="ff023-361">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff023-361">Type</span></span>|<span data-ttu-id="ff023-362">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="ff023-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="ff023-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="ff023-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="ff023-364">**unsignedInt**</span></span>|<span data-ttu-id="ff023-365">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-365">Optional.</span></span> <span data-ttu-id="ff023-366">Specifica hello quantità massima di archiviazione nel file system disponibile per hello specificato dati.</span><span class="sxs-lookup"><span data-stu-id="ff023-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="ff023-367">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="ff023-367">hello default is 0.</span></span>|  
|<span data-ttu-id="ff023-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="ff023-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="ff023-369">**string**</span><span class="sxs-lookup"><span data-stu-id="ff023-369">**string**</span></span>|<span data-ttu-id="ff023-370">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-370">Optional.</span></span> <span data-ttu-id="ff023-371">Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti.</span><span class="sxs-lookup"><span data-stu-id="ff023-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="ff023-372">valore predefinito di Hello è **Undefined**, che trasferisce tutti i log.</span><span class="sxs-lookup"><span data-stu-id="ff023-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="ff023-373">Altri valori possibili (nell'ordine della maggior parte delle informazioni tooleast) sono **Verbose**, **informazioni**, **avviso**, **errore**e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="ff023-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="ff023-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="ff023-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="ff023-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="ff023-375">**duration**</span></span>|<span data-ttu-id="ff023-376">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-376">Optional.</span></span> <span data-ttu-id="ff023-377">Specifica l'intervallo di hello tra i trasferimenti pianificati dei dati, arrotondati per eccesso toohello più vicino al minuto.</span><span class="sxs-lookup"><span data-stu-id="ff023-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="ff023-378">valore predefinito di Hello è PT0S.</span><span class="sxs-lookup"><span data-stu-id="ff023-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="ff023-379">**sinks** aggiunto nella versione 1.5</span><span class="sxs-lookup"><span data-stu-id="ff023-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="ff023-380">**string**</span><span class="sxs-lookup"><span data-stu-id="ff023-380">**string**</span></span>|<span data-ttu-id="ff023-381">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ff023-381">Optional.</span></span> <span data-ttu-id="ff023-382">Punti tooa sink percorso tooalso inviare dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ff023-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="ff023-383">ad esempio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ff023-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="ff023-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="ff023-384">DockerSources</span></span>
 <span data-ttu-id="ff023-385">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="ff023-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="ff023-386">Elementi aggiunti nella versione 1.9.</span><span class="sxs-lookup"><span data-stu-id="ff023-386">Added in 1.9.</span></span>

|<span data-ttu-id="ff023-387">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="ff023-387">Element Name</span></span>|<span data-ttu-id="ff023-388">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="ff023-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="ff023-389">**Stats**</span></span>|<span data-ttu-id="ff023-390">Indica il sistema di hello toocollect statistiche per i contenitori di Docker</span><span class="sxs-lookup"><span data-stu-id="ff023-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="ff023-391">Elemento SinksConfig</span><span class="sxs-lookup"><span data-stu-id="ff023-391">SinksConfig Element</span></span>  
 <span data-ttu-id="ff023-392">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="ff023-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="ff023-393">Un elenco di percorsi toosend dati tooand hello configurazione di diagnostica associati a tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="ff023-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="ff023-394">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="ff023-394">Element Name</span></span>|<span data-ttu-id="ff023-395">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="ff023-396">**Sink**</span><span class="sxs-lookup"><span data-stu-id="ff023-396">**Sink**</span></span>|<span data-ttu-id="ff023-397">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="ff023-398">Elemento Sink</span><span class="sxs-lookup"><span data-stu-id="ff023-398">Sink Element</span></span>
 <span data-ttu-id="ff023-399">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="ff023-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="ff023-400">Aggiunto nella versione 1.5.</span><span class="sxs-lookup"><span data-stu-id="ff023-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="ff023-401">Definisce i percorsi toosend dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ff023-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="ff023-402">Salve, ad esempio, il servizio di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ff023-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="ff023-403">Attributo</span><span class="sxs-lookup"><span data-stu-id="ff023-403">Attribute</span></span>|<span data-ttu-id="ff023-404">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff023-404">Type</span></span>|<span data-ttu-id="ff023-405">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="ff023-406">**nome**</span><span class="sxs-lookup"><span data-stu-id="ff023-406">**name**</span></span>|<span data-ttu-id="ff023-407">string</span><span class="sxs-lookup"><span data-stu-id="ff023-407">string</span></span>|<span data-ttu-id="ff023-408">Stringa identificazione sinkname hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="ff023-409">Elemento</span><span class="sxs-lookup"><span data-stu-id="ff023-409">Element</span></span>|<span data-ttu-id="ff023-410">Type</span><span class="sxs-lookup"><span data-stu-id="ff023-410">Type</span></span>|<span data-ttu-id="ff023-411">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="ff023-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="ff023-412">**Application Insights**</span></span>|<span data-ttu-id="ff023-413">string</span><span class="sxs-lookup"><span data-stu-id="ff023-413">string</span></span>|<span data-ttu-id="ff023-414">Utilizzato solo quando l'invio di dati tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="ff023-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="ff023-415">Contenere hello chiave di strumentazione per un account di Application Insights attivo che è possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="ff023-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="ff023-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="ff023-416">**Channels**</span></span>|<span data-ttu-id="ff023-417">string</span><span class="sxs-lookup"><span data-stu-id="ff023-417">string</span></span>|<span data-ttu-id="ff023-418">Uno per ogni filtro aggiuntivo per i flussi</span><span class="sxs-lookup"><span data-stu-id="ff023-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="ff023-419">Elemento Channels</span><span class="sxs-lookup"><span data-stu-id="ff023-419">Channels Element</span></span>  
 <span data-ttu-id="ff023-420">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="ff023-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="ff023-421">Aggiunto nella versione 1.5.</span><span class="sxs-lookup"><span data-stu-id="ff023-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="ff023-422">Definisce i filtri per i flussi di dati di log che attraversano un sink.</span><span class="sxs-lookup"><span data-stu-id="ff023-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="ff023-423">Elemento</span><span class="sxs-lookup"><span data-stu-id="ff023-423">Element</span></span>|<span data-ttu-id="ff023-424">Type</span><span class="sxs-lookup"><span data-stu-id="ff023-424">Type</span></span>|<span data-ttu-id="ff023-425">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="ff023-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="ff023-426">**Channel**</span></span>|<span data-ttu-id="ff023-427">string</span><span class="sxs-lookup"><span data-stu-id="ff023-427">string</span></span>|<span data-ttu-id="ff023-428">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="ff023-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="ff023-429">Elemento Channel</span><span class="sxs-lookup"><span data-stu-id="ff023-429">Channel Element</span></span>
 <span data-ttu-id="ff023-430">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="ff023-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="ff023-431">Aggiunto nella versione 1.5.</span><span class="sxs-lookup"><span data-stu-id="ff023-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="ff023-432">Definisce i percorsi toosend dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ff023-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="ff023-433">Salve, ad esempio, il servizio di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ff023-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="ff023-434">Attributi</span><span class="sxs-lookup"><span data-stu-id="ff023-434">Attributes</span></span>|<span data-ttu-id="ff023-435">Type</span><span class="sxs-lookup"><span data-stu-id="ff023-435">Type</span></span>|<span data-ttu-id="ff023-436">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="ff023-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="ff023-437">**logLevel**</span></span>|<span data-ttu-id="ff023-438">**string**</span><span class="sxs-lookup"><span data-stu-id="ff023-438">**string**</span></span>|<span data-ttu-id="ff023-439">Specifica il livello minimo di gravità hello per le voci di log che vengono trasferiti.</span><span class="sxs-lookup"><span data-stu-id="ff023-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="ff023-440">valore predefinito di Hello è **Undefined**, che trasferisce tutti i log.</span><span class="sxs-lookup"><span data-stu-id="ff023-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="ff023-441">Altri valori possibili (nell'ordine della maggior parte delle informazioni tooleast) sono **Verbose**, **informazioni**, **avviso**, **errore**e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="ff023-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="ff023-442">**nome**</span><span class="sxs-lookup"><span data-stu-id="ff023-442">**name**</span></span>|<span data-ttu-id="ff023-443">**string**</span><span class="sxs-lookup"><span data-stu-id="ff023-443">**string**</span></span>|<span data-ttu-id="ff023-444">Un nome univoco di hello canale toorefer per</span><span class="sxs-lookup"><span data-stu-id="ff023-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="ff023-445">Elemento PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="ff023-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="ff023-446">*Albero: radice - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="ff023-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="ff023-447">Aggiunto nella versione 1.3.</span><span class="sxs-lookup"><span data-stu-id="ff023-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="ff023-448">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="ff023-448">Optional</span></span>  

 <span data-ttu-id="ff023-449">Archivia i dettagli di privata hello hello dell'account di archiviazione (nome, chiave ed endpoint).</span><span class="sxs-lookup"><span data-stu-id="ff023-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="ff023-450">Queste informazioni viene inviate una macchina virtuale toohello, ma non possono essere recuperate da esso.</span><span class="sxs-lookup"><span data-stu-id="ff023-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="ff023-451">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="ff023-451">Child Elements</span></span>|<span data-ttu-id="ff023-452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff023-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="ff023-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="ff023-453">**StorageAccount**</span></span>|<span data-ttu-id="ff023-454">toouse di account di archiviazione Hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-454">hello storage account toouse.</span></span> <span data-ttu-id="ff023-455">Hello gli attributi seguenti è obbligatorio</span><span class="sxs-lookup"><span data-stu-id="ff023-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="ff023-456">- **nome** : hello nome dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="ff023-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="ff023-457">- **chiave** : hello toohello account di archiviazione della chiave.</span><span class="sxs-lookup"><span data-stu-id="ff023-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="ff023-458">- **endpoint** -hello endpoint tooaccess hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ff023-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="ff023-459">-**sasToken** (è possibile specificare un token di firma di accesso condiviso anziché una chiave di account di archiviazione nel file di configurazione privata hello 1.8.1)-aggiunto. Se fornito, chiave di account di archiviazione hello viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="ff023-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="ff023-460">Requisiti per il Token SAS hello:</span><span class="sxs-lookup"><span data-stu-id="ff023-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="ff023-461">- Supporta solo il token di firma di accesso condiviso dell'account</span><span class="sxs-lookup"><span data-stu-id="ff023-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="ff023-462">Sono obbligatori i tipi di servizio - *b* e *t*.</span><span class="sxs-lookup"><span data-stu-id="ff023-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="ff023-463">Sono obbligatorie le autorizzazioni - *a*, *c*, *u*, *w*.</span><span class="sxs-lookup"><span data-stu-id="ff023-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="ff023-464">Sono obbligatori i tipi di risorse - *c*, *o*.</span><span class="sxs-lookup"><span data-stu-id="ff023-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="ff023-465">-Supporta solo il protocollo HTTPS hello</span><span class="sxs-lookup"><span data-stu-id="ff023-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="ff023-466">-I valori dell'ora di inizio e di scadenza devono essere validi.</span><span class="sxs-lookup"><span data-stu-id="ff023-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="ff023-467">Elemento IsEnabled</span><span class="sxs-lookup"><span data-stu-id="ff023-467">IsEnabled Element</span></span>  
 <span data-ttu-id="ff023-468">*Albero: radice - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="ff023-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="ff023-469">Booleano.</span><span class="sxs-lookup"><span data-stu-id="ff023-469">Boolean.</span></span> <span data-ttu-id="ff023-470">Utilizzare `true` diagnostica hello tooenable o `false` diagnostica hello toodisable.</span><span class="sxs-lookup"><span data-stu-id="ff023-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
