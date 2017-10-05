---
title: Schema di configurazione dell'estensione di Diagnostica di Azure 1.3 e versioni successive | Microsoft Docs
description: Schema di Diagnostica di Azure 1.3 e versioni successive fornito con Microsoft Azure SDK 2.4 e versioni successive.
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
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="fe434-103">Schema di configurazione di Diagnostica di Azure 1.3 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="fe434-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="fe434-104">Il componente estensione di Diagnostica di Azure viene usato per raccogliere i contatori delle prestazioni e altre statistiche da:</span><span class="sxs-lookup"><span data-stu-id="fe434-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="fe434-105">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="fe434-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="fe434-106">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fe434-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="fe434-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fe434-107">Service Fabric</span></span> 
> - <span data-ttu-id="fe434-108">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="fe434-108">Cloud Services</span></span> 
> - <span data-ttu-id="fe434-109">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="fe434-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="fe434-110">Questa pagina è utile solo se si usa uno di questi servizi.</span><span class="sxs-lookup"><span data-stu-id="fe434-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="fe434-111">Questa pagina è valida per le versioni 1.3 e più recenti (Azure SDK 2.4 e versioni più recenti).</span><span class="sxs-lookup"><span data-stu-id="fe434-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="fe434-112">Le sezioni di configurazione più recenti hanno commenti per indicare in quale versione sono state aggiunte.</span><span class="sxs-lookup"><span data-stu-id="fe434-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="fe434-113">Il file di configurazione descritto qui viene usato per definire le impostazioni di configurazione della diagnostica all'avvio del monitor di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="fe434-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="fe434-114">L'estensione viene usata in combinazione con altri prodotti di diagnostica Microsoft, come Monitoraggio di Azure, Application Insights e Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fe434-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="fe434-115">Scaricare la definizione dello schema del file di configurazione pubblico eseguendo il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="fe434-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="fe434-116">Per altre informazioni su Diagnostica di Azure, vedere [Estensione di Diagnostica di Azure](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="fe434-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="fe434-117">Esempio del file di configurazione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="fe434-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="fe434-118">L'esempio seguente illustra un tipico file di configurazione della diagnostica:</span><span class="sxs-lookup"><span data-stu-id="fe434-118">The following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="fe434-119">Equivalente JSON del file di configurazione XML precedente.</span><span class="sxs-lookup"><span data-stu-id="fe434-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="fe434-120">PublicConfig e PrivateConfig sono separati perché vengono passati come variabili differenti nella maggior parte dei casi in cui viene usato il formato JSON.</span><span class="sxs-lookup"><span data-stu-id="fe434-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="fe434-121">Alcuni esempi sono i modelli di Resource Manager, i set di scalabilità di macchine virtuali PowerShell e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe434-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="fe434-122">Come leggere questa pagina</span><span class="sxs-lookup"><span data-stu-id="fe434-122">Reading this page</span></span>  
 <span data-ttu-id="fe434-123">I tag seguenti sono più o meno nell'ordine indicato nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="fe434-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="fe434-124">Se non si trova rapidamente la descrizione completa, cercare l'elemento o l'attributo nella pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="fe434-125">Tipi di attributi comuni</span><span class="sxs-lookup"><span data-stu-id="fe434-125">Common Attribute Types</span></span>  
 <span data-ttu-id="fe434-126">L'attributo **scheduledTransferPeriod** è presente in diversi elementi.</span><span class="sxs-lookup"><span data-stu-id="fe434-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="fe434-127">Si tratta dell'intervallo tra trasferimenti pianificati per l'archivio, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="fe434-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="fe434-128">Il valore è un ["Tipo di dati di durata" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="fe434-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="fe434-129">Elemento DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="fe434-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="fe434-130">*Albero: radice - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="fe434-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="fe434-131">Aggiunto nella versione 1.3.</span><span class="sxs-lookup"><span data-stu-id="fe434-131">Added in version 1.3.</span></span>  

<span data-ttu-id="fe434-132">Elemento di livello superiore del file di configurazione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="fe434-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="fe434-133">**Attributo** xmlns: lo spazio dei nomi XML per il file di configurazione della diagnostica è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fe434-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="fe434-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="fe434-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="fe434-135">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-135">Child Elements</span></span>|<span data-ttu-id="fe434-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="fe434-137">**PublicConfig**</span></span>|<span data-ttu-id="fe434-138">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="fe434-138">Required.</span></span> <span data-ttu-id="fe434-139">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="fe434-140">**PrivateConfig**</span></span>|<span data-ttu-id="fe434-141">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-141">Optional.</span></span> <span data-ttu-id="fe434-142">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="fe434-143">**IsEnabled**</span></span>|<span data-ttu-id="fe434-144">Booleano.</span><span class="sxs-lookup"><span data-stu-id="fe434-144">Boolean.</span></span> <span data-ttu-id="fe434-145">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="fe434-146">Elemento PublicConfig</span><span class="sxs-lookup"><span data-stu-id="fe434-146">PublicConfig Element</span></span>  
 <span data-ttu-id="fe434-147">*Albero: radice - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="fe434-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="fe434-148">Descrive la configurazione della diagnostica pubblica.</span><span class="sxs-lookup"><span data-stu-id="fe434-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="fe434-149">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-149">Child Elements</span></span>|<span data-ttu-id="fe434-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="fe434-151">**WadCfg**</span></span>|<span data-ttu-id="fe434-152">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="fe434-152">Required.</span></span> <span data-ttu-id="fe434-153">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="fe434-154">**StorageAccount**</span></span>|<span data-ttu-id="fe434-155">Nome dell'account di archiviazione di Azure in cui archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="fe434-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="fe434-156">Può anche essere specificato come parametro quando si esegue il cmdlet Set-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="fe434-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="fe434-157">**Tipo di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="fe434-157">**StorageType**</span></span>|<span data-ttu-id="fe434-158">Può essere *Table*, *Blob* o *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="fe434-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="fe434-159">Table è il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="fe434-159">Table is default.</span></span> <span data-ttu-id="fe434-160">Quando si sceglie TableAndBlob, i dati di diagnostica vengono scritti due volte, una volta per ogni tipo.</span><span class="sxs-lookup"><span data-stu-id="fe434-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="fe434-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="fe434-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="fe434-162">Directory nella macchina virtuale in cui l'agente di monitoraggio archivia i dati degli eventi.</span><span class="sxs-lookup"><span data-stu-id="fe434-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="fe434-163">Se non impostata, verrà usata la directory predefinita:</span><span class="sxs-lookup"><span data-stu-id="fe434-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="fe434-164">Per un ruolo di lavoro/Web: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="fe434-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="fe434-165">Per una macchina virtuale: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="fe434-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="fe434-166">Gli attributi obbligatori sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe434-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="fe434-167">- **path**: directory nel sistema che dovrà essere usata da Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe434-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="fe434-168">- **expandEnvironment**: definisce se le variabili di ambiente vengono espanse nel nome del percorso.</span><span class="sxs-lookup"><span data-stu-id="fe434-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="fe434-169">Elemento WadCFG</span><span class="sxs-lookup"><span data-stu-id="fe434-169">WadCFG Element</span></span>  
 <span data-ttu-id="fe434-170">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="fe434-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="fe434-171">Identifica e configura i dati di telemetria da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="fe434-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="fe434-172">Elemento DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="fe434-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="fe434-173">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="fe434-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="fe434-174">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fe434-174">Required</span></span> 

|<span data-ttu-id="fe434-175">Attributi</span><span class="sxs-lookup"><span data-stu-id="fe434-175">Attributes</span></span>|<span data-ttu-id="fe434-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="fe434-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="fe434-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="fe434-178">Spazio massimo sul disco locale che può essere usato dai vari tipi di dati di diagnostica raccolti da Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe434-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="fe434-179">L'impostazione predefinita è 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="fe434-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="fe434-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="fe434-180">**useProxyServer**</span></span> | <span data-ttu-id="fe434-181">Configurare Diagnostica di Azure per l'uso delle impostazioni del server proxy definite nelle impostazioni di Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="fe434-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="fe434-182">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-182">Child Elements</span></span>|<span data-ttu-id="fe434-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="fe434-184">**CrashDumps**</span></span>|<span data-ttu-id="fe434-185">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="fe434-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="fe434-187">Abilita la raccolta dei log generati da Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe434-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="fe434-188">I log dell'infrastruttura di diagnostica sono utili per la risoluzione dei problemi del sistema di diagnostica stesso.</span><span class="sxs-lookup"><span data-stu-id="fe434-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="fe434-189">Gli attributi facoltativi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe434-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="fe434-190">- **scheduledTransferLogLevelFilter**: consente di configurare il livello di gravità minimo dei log raccolti.</span><span class="sxs-lookup"><span data-stu-id="fe434-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="fe434-191">- **scheduledTransferPeriod**: intervallo tra trasferimenti pianificati per l'archivio, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="fe434-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="fe434-192">Il valore è un ["Tipo di dati di durata" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="fe434-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="fe434-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="fe434-193">**Directories**</span></span>|<span data-ttu-id="fe434-194">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="fe434-195">**EtwProviders**</span></span>|<span data-ttu-id="fe434-196">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-197">**Metriche**</span><span class="sxs-lookup"><span data-stu-id="fe434-197">**Metrics**</span></span>|<span data-ttu-id="fe434-198">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="fe434-199">**PerformanceCounters**</span></span>|<span data-ttu-id="fe434-200">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="fe434-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="fe434-201">**WindowsEventLog**</span></span>|<span data-ttu-id="fe434-202">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="fe434-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="fe434-203">**DockerSources**</span></span>|<span data-ttu-id="fe434-204">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="fe434-205">Elemento CrashDumps</span><span class="sxs-lookup"><span data-stu-id="fe434-205">CrashDumps Element</span></span>  
 <span data-ttu-id="fe434-206">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="fe434-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="fe434-207">Abilitare la raccolta di dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fe434-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="fe434-208">Attributi</span><span class="sxs-lookup"><span data-stu-id="fe434-208">Attributes</span></span>|<span data-ttu-id="fe434-209">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="fe434-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="fe434-210">**containerName**</span></span>|<span data-ttu-id="fe434-211">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-211">Optional.</span></span> <span data-ttu-id="fe434-212">Nome del contenitore BLOB dell'account di archiviazione di Azure da usare per archiviare i dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fe434-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="fe434-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="fe434-213">**crashDumpType**</span></span>|<span data-ttu-id="fe434-214">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-214">Optional.</span></span>  <span data-ttu-id="fe434-215">Configura Diagnostica di Azure per la raccolta di dump di arresto anomalo del sistema completi o mini.</span><span class="sxs-lookup"><span data-stu-id="fe434-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="fe434-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="fe434-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="fe434-217">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-217">Optional.</span></span>  <span data-ttu-id="fe434-218">Configura la percentuale di **overallQuotaInMB** da riservare per i dump di arresto anomalo del sistema nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fe434-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="fe434-219">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-219">Child Elements</span></span>|<span data-ttu-id="fe434-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="fe434-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="fe434-222">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="fe434-222">Required.</span></span> <span data-ttu-id="fe434-223">Definisce i valori di configurazione di ogni processo.</span><span class="sxs-lookup"><span data-stu-id="fe434-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="fe434-224">Anche l'attributo seguente è obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="fe434-225">**processName**: nome del processo per il quale Diagnostica di Azure dovrà raccogliere un dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fe434-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="fe434-226">Elemento Directories</span><span class="sxs-lookup"><span data-stu-id="fe434-226">Directories Element</span></span> 
 <span data-ttu-id="fe434-227">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories*</span><span class="sxs-lookup"><span data-stu-id="fe434-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="fe434-228">Abilita la raccolta del contenuto di una directory, dei log delle richieste di accesso IIS non riuscite e/o dei log IIS.</span><span class="sxs-lookup"><span data-stu-id="fe434-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="fe434-229">Attributo **scheduledTransferPeriod** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="fe434-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="fe434-230">Vedere la spiegazione indicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fe434-230">See explanation earlier.</span></span>  

|<span data-ttu-id="fe434-231">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-231">Child Elements</span></span>|<span data-ttu-id="fe434-232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="fe434-233">**IISLogs**</span></span>|<span data-ttu-id="fe434-234">Includendo questo elemento nella configurazione viene abilitata la raccolta di log IIS:</span><span class="sxs-lookup"><span data-stu-id="fe434-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="fe434-235">**containerName**: nome del contenitore BLOB dell'account di archiviazione di Azure da usare per archiviare i log IIS.</span><span class="sxs-lookup"><span data-stu-id="fe434-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="fe434-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="fe434-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="fe434-237">Con questo elemento nella configurazione è possibile raccogliere i log relativi alle richieste non riuscite per un'applicazione o un sito IIS.</span><span class="sxs-lookup"><span data-stu-id="fe434-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="fe434-238">È anche necessario abilitare le opzioni di traccia sotto **system.WebServer** in **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="fe434-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="fe434-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="fe434-239">**DataSources**</span></span>|<span data-ttu-id="fe434-240">Elenco di directory da monitorare.</span><span class="sxs-lookup"><span data-stu-id="fe434-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="fe434-241">Elemento DataSources</span><span class="sxs-lookup"><span data-stu-id="fe434-241">DataSources Element</span></span>  
 <span data-ttu-id="fe434-242">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="fe434-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="fe434-243">Elenco di directory da monitorare.</span><span class="sxs-lookup"><span data-stu-id="fe434-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="fe434-244">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-244">Child Elements</span></span>|<span data-ttu-id="fe434-245">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="fe434-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="fe434-247">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="fe434-247">Required.</span></span> <span data-ttu-id="fe434-248">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="fe434-249">**containerName**: nome del contenitore BLOB dell'account di archiviazione di Azure da usare per archiviare i file log.</span><span class="sxs-lookup"><span data-stu-id="fe434-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="fe434-250">Elemento DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="fe434-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="fe434-251">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="fe434-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="fe434-252">Può includere l'elemento **Absolute** o **LocalResource**, ma non entrambi.</span><span class="sxs-lookup"><span data-stu-id="fe434-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="fe434-253">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-253">Child Elements</span></span>|<span data-ttu-id="fe434-254">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="fe434-255">**Absolute**</span></span>|<span data-ttu-id="fe434-256">Percorso assoluto della directory da monitorare.</span><span class="sxs-lookup"><span data-stu-id="fe434-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="fe434-257">Gli attributi seguenti sono obbligatori:</span><span class="sxs-lookup"><span data-stu-id="fe434-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="fe434-258">- **Path**: percorso assoluto della directory da monitorare.</span><span class="sxs-lookup"><span data-stu-id="fe434-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="fe434-259">- **expandEnvironment**: definisce se le variabili di ambiente vengono espanse in Path.</span><span class="sxs-lookup"><span data-stu-id="fe434-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="fe434-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="fe434-260">**LocalResource**</span></span>|<span data-ttu-id="fe434-261">Percorso relativo di una risorsa locale da monitorare.</span><span class="sxs-lookup"><span data-stu-id="fe434-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="fe434-262">Gli attributi obbligatori sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe434-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="fe434-263">- **Name**: nome della risorsa locale che contiene la directory da monitorare</span><span class="sxs-lookup"><span data-stu-id="fe434-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="fe434-264">- **relativePath**: percorso relativo del nome che contiene la directory da monitorare</span><span class="sxs-lookup"><span data-stu-id="fe434-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="fe434-265">Elemento EtwProviders</span><span class="sxs-lookup"><span data-stu-id="fe434-265">EtwProviders Element</span></span>  
 <span data-ttu-id="fe434-266">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="fe434-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="fe434-267">Configura la raccolta di eventi ETW da EventSource e/o da provider basati su manifesti ETW.</span><span class="sxs-lookup"><span data-stu-id="fe434-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="fe434-268">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-268">Child Elements</span></span>|<span data-ttu-id="fe434-269">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="fe434-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="fe434-271">Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="fe434-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="fe434-272">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="fe434-273">**provider**: nome della classe dell'evento EventSource.</span><span class="sxs-lookup"><span data-stu-id="fe434-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="fe434-274">Gli attributi facoltativi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe434-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="fe434-275">- **scheduledTransferLogLevelFilter**: livello di gravità minimo per il trasferimento nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fe434-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="fe434-276">- **scheduledTransferPeriod**: intervallo tra trasferimenti pianificati per l'archivio, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="fe434-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="fe434-277">Il valore è un ["Tipo di dati di durata" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="fe434-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="fe434-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="fe434-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="fe434-279">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="fe434-280">**provider**: GUID del provider di eventi</span><span class="sxs-lookup"><span data-stu-id="fe434-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="fe434-281">Gli attributi facoltativi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe434-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="fe434-282">- **scheduledTransferLogLevelFilter**: livello di gravità minimo per il trasferimento nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fe434-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="fe434-283">- **scheduledTransferPeriod**: intervallo tra trasferimenti pianificati per l'archivio, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="fe434-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="fe434-284">Il valore è un ["Tipo di dati di durata" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="fe434-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="fe434-285">Elemento EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="fe434-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="fe434-286">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="fe434-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="fe434-287">Configura la raccolta di eventi generati dalla [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="fe434-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="fe434-288">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-288">Child Elements</span></span>|<span data-ttu-id="fe434-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="fe434-290">**DefaultEvents**</span></span>|<span data-ttu-id="fe434-291">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="fe434-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="fe434-292">**eventDestination**: nome della tabella nella quale archiviare gli eventi</span><span class="sxs-lookup"><span data-stu-id="fe434-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="fe434-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="fe434-293">**Event**</span></span>|<span data-ttu-id="fe434-294">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="fe434-295">**id**: ID dell'evento.</span><span class="sxs-lookup"><span data-stu-id="fe434-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="fe434-296">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="fe434-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="fe434-297">**eventDestination**: nome della tabella nella quale archiviare gli eventi</span><span class="sxs-lookup"><span data-stu-id="fe434-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="fe434-298">Elemento EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="fe434-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="fe434-299">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="fe434-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="fe434-300">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-300">Child Elements</span></span>|<span data-ttu-id="fe434-301">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="fe434-302">**DefaultEvents**</span></span>|<span data-ttu-id="fe434-303">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="fe434-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="fe434-304">**eventDestination**: nome della tabella nella quale archiviare gli eventi</span><span class="sxs-lookup"><span data-stu-id="fe434-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="fe434-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="fe434-305">**Event**</span></span>|<span data-ttu-id="fe434-306">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="fe434-307">**id**: ID dell'evento.</span><span class="sxs-lookup"><span data-stu-id="fe434-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="fe434-308">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="fe434-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="fe434-309">**eventDestination**: nome della tabella nella quale archiviare gli eventi</span><span class="sxs-lookup"><span data-stu-id="fe434-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="fe434-310">Elemento Metrics</span><span class="sxs-lookup"><span data-stu-id="fe434-310">Metrics Element</span></span>  
 <span data-ttu-id="fe434-311">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="fe434-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="fe434-312">Consente di generare una tabella di contatori delle prestazioni ottimizzata per le query veloci.</span><span class="sxs-lookup"><span data-stu-id="fe434-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="fe434-313">Ogni contatore delle prestazioni definito nell'elemento **PerformanceCounters** viene archiviato nella tabella delle metriche oltre che nella tabella dei contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="fe434-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="fe434-314">L'attributo **resourceId** è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="fe434-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="fe434-315">L'ID risorsa della macchina virtuale nella quale si distribuisce Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe434-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="fe434-316">Ottenere l'attributo **resourceID** dal [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe434-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fe434-317">Selezionare **Esplora** -> **Gruppi di risorse** -> **<Nome\>**.</span><span class="sxs-lookup"><span data-stu-id="fe434-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="fe434-318">Fare clic sul riquadro **Proprietà** e copiare il valore del campo **ID**.</span><span class="sxs-lookup"><span data-stu-id="fe434-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="fe434-319">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-319">Child Elements</span></span>|<span data-ttu-id="fe434-320">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="fe434-321">**MetricAggregation**</span></span>|<span data-ttu-id="fe434-322">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="fe434-323">**scheduledTransferPeriod**: intervallo tra trasferimenti pianificati per l'archivio, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="fe434-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="fe434-324">Il valore è un ["Tipo di dati di durata" XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="fe434-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="fe434-325">Elemento PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="fe434-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="fe434-326">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="fe434-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="fe434-327">Abilita la raccolta dei contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="fe434-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="fe434-328">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="fe434-328">Optional attribute:</span></span>  

 <span data-ttu-id="fe434-329">Attributo **scheduledTransferPeriod** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="fe434-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="fe434-330">Vedere la spiegazione indicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fe434-330">See explanation earlier.</span></span>

|<span data-ttu-id="fe434-331">Elemento figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-331">Child Element</span></span>|<span data-ttu-id="fe434-332">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="fe434-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="fe434-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="fe434-334">Gli attributi seguenti sono obbligatori:</span><span class="sxs-lookup"><span data-stu-id="fe434-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="fe434-335">- **counterSpecifier**: nome del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="fe434-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="fe434-336">Ad esempio, `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="fe434-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="fe434-337">Per ottenere un elenco di contatori delle prestazioni nell'host eseguire il comando `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="fe434-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="fe434-338">- **sampleRate**: frequenza di campionamento del contatore.</span><span class="sxs-lookup"><span data-stu-id="fe434-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="fe434-339">Attributo facoltativo:</span><span class="sxs-lookup"><span data-stu-id="fe434-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="fe434-340">**unit**: unità di misura del contatore.</span><span class="sxs-lookup"><span data-stu-id="fe434-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="fe434-341">Elemento WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="fe434-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="fe434-342">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="fe434-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="fe434-343">Abilita la raccolta dei registri eventi di Windows.</span><span class="sxs-lookup"><span data-stu-id="fe434-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="fe434-344">Attributo **scheduledTransferPeriod** facoltativo.</span><span class="sxs-lookup"><span data-stu-id="fe434-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="fe434-345">Vedere la spiegazione indicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fe434-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="fe434-346">Elemento figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-346">Child Element</span></span>|<span data-ttu-id="fe434-347">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="fe434-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="fe434-348">**DataSource**</span></span>|<span data-ttu-id="fe434-349">Registri eventi di Windows da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="fe434-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="fe434-350">Attributo obbligatorio:</span><span class="sxs-lookup"><span data-stu-id="fe434-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="fe434-351">**name**: query XPath che descrive gli eventi di Windows da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="fe434-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="fe434-352">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fe434-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="fe434-353">Per raccogliere tutti gli eventi, specificare "*"</span><span class="sxs-lookup"><span data-stu-id="fe434-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="fe434-354">Elemento Logs</span><span class="sxs-lookup"><span data-stu-id="fe434-354">Logs Element</span></span>  
 <span data-ttu-id="fe434-355">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="fe434-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="fe434-356">Presente nella versione 1.0 e 1.1.</span><span class="sxs-lookup"><span data-stu-id="fe434-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="fe434-357">Assente nella versione 1.2.</span><span class="sxs-lookup"><span data-stu-id="fe434-357">Missing in 1.2.</span></span> <span data-ttu-id="fe434-358">Aggiunto nuovamente nella versione 1.3.</span><span class="sxs-lookup"><span data-stu-id="fe434-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="fe434-359">Definisce la configurazione del buffer per i log di base di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe434-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="fe434-360">Attributo</span><span class="sxs-lookup"><span data-stu-id="fe434-360">Attribute</span></span>|<span data-ttu-id="fe434-361">Tipo</span><span class="sxs-lookup"><span data-stu-id="fe434-361">Type</span></span>|<span data-ttu-id="fe434-362">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="fe434-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="fe434-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="fe434-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="fe434-364">**unsignedInt**</span></span>|<span data-ttu-id="fe434-365">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-365">Optional.</span></span> <span data-ttu-id="fe434-366">Specifica lo spazio massimo di archiviazione del file system disponibile per i dati specificati.</span><span class="sxs-lookup"><span data-stu-id="fe434-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="fe434-367">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="fe434-367">The default is 0.</span></span>|  
|<span data-ttu-id="fe434-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="fe434-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="fe434-369">**string**</span><span class="sxs-lookup"><span data-stu-id="fe434-369">**string**</span></span>|<span data-ttu-id="fe434-370">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-370">Optional.</span></span> <span data-ttu-id="fe434-371">Specifica il livello di gravità minimo per le voci di log trasferite.</span><span class="sxs-lookup"><span data-stu-id="fe434-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="fe434-372">Il valore predefinito è **Non definito**, con il quale verranno trasferiti tutti i log.</span><span class="sxs-lookup"><span data-stu-id="fe434-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="fe434-373">Altri valori possibili (dal più dettagliato al meno dettagliato) sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="fe434-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="fe434-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="fe434-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="fe434-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="fe434-375">**duration**</span></span>|<span data-ttu-id="fe434-376">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-376">Optional.</span></span> <span data-ttu-id="fe434-377">Specifica l'intervallo tra trasferimenti di dati pianificati, arrotondato per eccesso al minuto più vicino.</span><span class="sxs-lookup"><span data-stu-id="fe434-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="fe434-378">Il valore predefinito è PT0S.</span><span class="sxs-lookup"><span data-stu-id="fe434-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="fe434-379">**sinks** aggiunto nella versione 1.5</span><span class="sxs-lookup"><span data-stu-id="fe434-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="fe434-380">**string**</span><span class="sxs-lookup"><span data-stu-id="fe434-380">**string**</span></span>|<span data-ttu-id="fe434-381">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fe434-381">Optional.</span></span> <span data-ttu-id="fe434-382">Punta a una posizione di sink per l'invio di dati di diagnostica,</span><span class="sxs-lookup"><span data-stu-id="fe434-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="fe434-383">ad esempio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fe434-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="fe434-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="fe434-384">DockerSources</span></span>
 <span data-ttu-id="fe434-385">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="fe434-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="fe434-386">Elementi aggiunti nella versione 1.9.</span><span class="sxs-lookup"><span data-stu-id="fe434-386">Added in 1.9.</span></span>

|<span data-ttu-id="fe434-387">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="fe434-387">Element Name</span></span>|<span data-ttu-id="fe434-388">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="fe434-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="fe434-389">**Stats**</span></span>|<span data-ttu-id="fe434-390">Indica al sistema di raccogliere statistiche per i contenitori Docker</span><span class="sxs-lookup"><span data-stu-id="fe434-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="fe434-391">Elemento SinksConfig</span><span class="sxs-lookup"><span data-stu-id="fe434-391">SinksConfig Element</span></span>  
 <span data-ttu-id="fe434-392">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="fe434-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="fe434-393">Elenco di posizioni a cui inviare i dati di diagnostica e la configurazione associata a tali posizioni.</span><span class="sxs-lookup"><span data-stu-id="fe434-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="fe434-394">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="fe434-394">Element Name</span></span>|<span data-ttu-id="fe434-395">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="fe434-396">**Sink**</span><span class="sxs-lookup"><span data-stu-id="fe434-396">**Sink**</span></span>|<span data-ttu-id="fe434-397">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="fe434-398">Elemento Sink</span><span class="sxs-lookup"><span data-stu-id="fe434-398">Sink Element</span></span>
 <span data-ttu-id="fe434-399">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="fe434-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="fe434-400">Aggiunto nella versione 1.5.</span><span class="sxs-lookup"><span data-stu-id="fe434-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="fe434-401">Definisce le posizioni a cui inviare i dati di diagnostica,</span><span class="sxs-lookup"><span data-stu-id="fe434-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="fe434-402">ad esempio il servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fe434-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="fe434-403">Attributo</span><span class="sxs-lookup"><span data-stu-id="fe434-403">Attribute</span></span>|<span data-ttu-id="fe434-404">Tipo</span><span class="sxs-lookup"><span data-stu-id="fe434-404">Type</span></span>|<span data-ttu-id="fe434-405">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="fe434-406">**nome**</span><span class="sxs-lookup"><span data-stu-id="fe434-406">**name**</span></span>|<span data-ttu-id="fe434-407">string</span><span class="sxs-lookup"><span data-stu-id="fe434-407">string</span></span>|<span data-ttu-id="fe434-408">Stringa che identifica il nome del sink.</span><span class="sxs-lookup"><span data-stu-id="fe434-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="fe434-409">Elemento</span><span class="sxs-lookup"><span data-stu-id="fe434-409">Element</span></span>|<span data-ttu-id="fe434-410">Type</span><span class="sxs-lookup"><span data-stu-id="fe434-410">Type</span></span>|<span data-ttu-id="fe434-411">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="fe434-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="fe434-412">**Application Insights**</span></span>|<span data-ttu-id="fe434-413">string</span><span class="sxs-lookup"><span data-stu-id="fe434-413">string</span></span>|<span data-ttu-id="fe434-414">Usato solo per inviare dati ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fe434-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="fe434-415">Contiene la chiave di strumentazione per un account di Application Insights attivo a cui è possibile accedere.</span><span class="sxs-lookup"><span data-stu-id="fe434-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="fe434-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="fe434-416">**Channels**</span></span>|<span data-ttu-id="fe434-417">string</span><span class="sxs-lookup"><span data-stu-id="fe434-417">string</span></span>|<span data-ttu-id="fe434-418">Uno per ogni filtro aggiuntivo per i flussi</span><span class="sxs-lookup"><span data-stu-id="fe434-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="fe434-419">Elemento Channels</span><span class="sxs-lookup"><span data-stu-id="fe434-419">Channels Element</span></span>  
 <span data-ttu-id="fe434-420">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="fe434-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="fe434-421">Aggiunto nella versione 1.5.</span><span class="sxs-lookup"><span data-stu-id="fe434-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="fe434-422">Definisce i filtri per i flussi di dati di log che attraversano un sink.</span><span class="sxs-lookup"><span data-stu-id="fe434-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="fe434-423">Elemento</span><span class="sxs-lookup"><span data-stu-id="fe434-423">Element</span></span>|<span data-ttu-id="fe434-424">Type</span><span class="sxs-lookup"><span data-stu-id="fe434-424">Type</span></span>|<span data-ttu-id="fe434-425">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="fe434-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="fe434-426">**Channel**</span></span>|<span data-ttu-id="fe434-427">string</span><span class="sxs-lookup"><span data-stu-id="fe434-427">string</span></span>|<span data-ttu-id="fe434-428">Vedere la descrizione altrove in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="fe434-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="fe434-429">Elemento Channel</span><span class="sxs-lookup"><span data-stu-id="fe434-429">Channel Element</span></span>
 <span data-ttu-id="fe434-430">*Albero: radice - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="fe434-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="fe434-431">Aggiunto nella versione 1.5.</span><span class="sxs-lookup"><span data-stu-id="fe434-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="fe434-432">Definisce le posizioni a cui inviare i dati di diagnostica,</span><span class="sxs-lookup"><span data-stu-id="fe434-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="fe434-433">ad esempio il servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fe434-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="fe434-434">Attributi</span><span class="sxs-lookup"><span data-stu-id="fe434-434">Attributes</span></span>|<span data-ttu-id="fe434-435">Type</span><span class="sxs-lookup"><span data-stu-id="fe434-435">Type</span></span>|<span data-ttu-id="fe434-436">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="fe434-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="fe434-437">**logLevel**</span></span>|<span data-ttu-id="fe434-438">**string**</span><span class="sxs-lookup"><span data-stu-id="fe434-438">**string**</span></span>|<span data-ttu-id="fe434-439">Specifica il livello di gravità minimo per le voci di log trasferite.</span><span class="sxs-lookup"><span data-stu-id="fe434-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="fe434-440">Il valore predefinito è **Non definito**, con il quale verranno trasferiti tutti i log.</span><span class="sxs-lookup"><span data-stu-id="fe434-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="fe434-441">Altri valori possibili (dal più dettagliato al meno dettagliato) sono **Dettagli**, **Informazioni**, **Avviso**, **Errore** e **Critico**.</span><span class="sxs-lookup"><span data-stu-id="fe434-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="fe434-442">**nome**</span><span class="sxs-lookup"><span data-stu-id="fe434-442">**name**</span></span>|<span data-ttu-id="fe434-443">**string**</span><span class="sxs-lookup"><span data-stu-id="fe434-443">**string**</span></span>|<span data-ttu-id="fe434-444">Nome univoco per fare riferimento al canale</span><span class="sxs-lookup"><span data-stu-id="fe434-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="fe434-445">Elemento PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="fe434-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="fe434-446">*Albero: radice - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="fe434-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="fe434-447">Aggiunto nella versione 1.3.</span><span class="sxs-lookup"><span data-stu-id="fe434-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="fe434-448">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="fe434-448">Optional</span></span>  

 <span data-ttu-id="fe434-449">Archivia le informazioni private dell'account di archiviazione, ovvero nome, chiave ed endpoint.</span><span class="sxs-lookup"><span data-stu-id="fe434-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="fe434-450">Queste informazioni vengono inviate alla macchina virtuale, ma non possono essere recuperate dalla macchina virtuale stessa.</span><span class="sxs-lookup"><span data-stu-id="fe434-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="fe434-451">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe434-451">Child Elements</span></span>|<span data-ttu-id="fe434-452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe434-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="fe434-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="fe434-453">**StorageAccount**</span></span>|<span data-ttu-id="fe434-454">Account di archiviazione da usare.</span><span class="sxs-lookup"><span data-stu-id="fe434-454">The storage account to use.</span></span> <span data-ttu-id="fe434-455">Gli attributi seguenti sono obbligatori:</span><span class="sxs-lookup"><span data-stu-id="fe434-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="fe434-456">- **name**: nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fe434-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="fe434-457">- **key**: chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fe434-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="fe434-458">- **endpoint**: endpoint per accedere all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fe434-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="fe434-459">-**sasToken** (elemento aggiunto alla versione 1.8.1): è possibile specificare un token di firma di accesso condiviso anziché una chiave dell'account di archiviazione in PrivateConfig.</span><span class="sxs-lookup"><span data-stu-id="fe434-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="fe434-460">Se viene fornito, la chiave dell'account di archiviazione viene ignorata.</span><span class="sxs-lookup"><span data-stu-id="fe434-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="fe434-461">Requisiti per il token di firma di accesso condiviso:</span><span class="sxs-lookup"><span data-stu-id="fe434-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="fe434-462">- Supporta solo il token di firma di accesso condiviso dell'account</span><span class="sxs-lookup"><span data-stu-id="fe434-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="fe434-463">Sono obbligatori i tipi di servizio - *b* e *t*.</span><span class="sxs-lookup"><span data-stu-id="fe434-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="fe434-464">Sono obbligatorie le autorizzazioni - *a*, *c*, *u*, *w*.</span><span class="sxs-lookup"><span data-stu-id="fe434-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="fe434-465">Sono obbligatori i tipi di risorse - *c*, *o*.</span><span class="sxs-lookup"><span data-stu-id="fe434-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="fe434-466">- Supporta solo il protocollo HTTPS</span><span class="sxs-lookup"><span data-stu-id="fe434-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="fe434-467">-I valori dell'ora di inizio e di scadenza devono essere validi.</span><span class="sxs-lookup"><span data-stu-id="fe434-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="fe434-468">Elemento IsEnabled</span><span class="sxs-lookup"><span data-stu-id="fe434-468">IsEnabled Element</span></span>  
 <span data-ttu-id="fe434-469">*Albero: radice - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="fe434-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="fe434-470">Booleano.</span><span class="sxs-lookup"><span data-stu-id="fe434-470">Boolean.</span></span> <span data-ttu-id="fe434-471">Usare `true` per abilitare la diagnostica o `false` per disabilitarla.</span><span class="sxs-lookup"><span data-stu-id="fe434-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
