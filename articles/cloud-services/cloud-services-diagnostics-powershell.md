---
title: Abilitare la diagnostica nei servizi cloud di Azure con PowerShell | Documentazione Microsoft
description: Informazioni su come abilitare la diagnostica per i servizi cloud tramite PowerShell
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="39cad-103">Abilitare la diagnostica nei servizi cloud di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="39cad-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="39cad-104">È possibile raccogliere dati di diagnostica come log applicazioni, contatori delle prestazioni e così via da un servizio cloud mediante l'estensione Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="39cad-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="39cad-105">Questo articolo descrive come abilitare l'estensione Diagnostica di Azure per un servizio Cloud tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39cad-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="39cad-106">Per i prerequisiti necessari per questo articolo, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="39cad-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="39cad-107">Abilitare l'estensione delle funzionalità di diagnostica come parte della distribuzione di un servizio Cloud</span><span class="sxs-lookup"><span data-stu-id="39cad-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="39cad-108">Questo approccio è applicabile al tipo di scenari di integrazione continua, in cui l'estensione Diagnostica può essere abilitata come parte della distribuzione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="39cad-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="39cad-109">Quando si crea una nuova distribuzione del servizio cloud, è possibile abilitare l'estensione Diagnostica passando il parametro *ExtensionConfiguration* al cmdlet [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="39cad-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="39cad-110">Il parametro *ExtensionConfiguration* accetta una matrice di configurazioni di diagnostica che può essere creata utilizzando il cmdlet [New AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="39cad-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="39cad-111">L'esempio seguente mostra come abilitare la diagnostica per un servizio cloud con un WebRole e un WorkerRole, ognuno dei quali ha una configurazione di diagnostica diversa.</span><span class="sxs-lookup"><span data-stu-id="39cad-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="39cad-112">Se il file di configurazione della diagnostica specifica un elemento `StorageAccount` con il nome di un account di archiviazione, il cmdlet `New-AzureServiceDiagnosticsExtensionConfig` userà automaticamente tale account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="39cad-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="39cad-113">A questo scopo, l'account di archiviazione deve trovarsi nella stessa sottoscrizione del servizio cloud da distribuire.</span><span class="sxs-lookup"><span data-stu-id="39cad-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="39cad-114">Da Azure SDK 2.6 in poi, i file di configurazione dell'estensione generati dall'output della destinazione di pubblicazione di MSBuild includeranno il nome dell'account di archiviazione basato sulla stringa di configurazione della diagnostica specificata nel file di configurazione del servizio (cscfg).</span><span class="sxs-lookup"><span data-stu-id="39cad-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="39cad-115">Lo script seguente mostra come analizzare i file di configurazione dell'estensione dall'output della destinazione di pubblicazione e configurare l'estensione Diagnostica per ogni ruolo quando si distribuisce il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="39cad-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="39cad-116">Visual Studio Online usa un approccio simile per le distribuzioni automatiche di Servizi cloud con l'estensione Diagnostica.</span><span class="sxs-lookup"><span data-stu-id="39cad-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="39cad-117">Per un esempio completo, vedere [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) .</span><span class="sxs-lookup"><span data-stu-id="39cad-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="39cad-118">Se nella configurazione di diagnostica non è specificato alcun elemento `StorageAccount`, è necessario passare il parametro *StorageAccountName* al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="39cad-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="39cad-119">Se il parametro *StorageAccountName* è specificato, il cmdlet userà sempre l'account di archiviazione specificato nel parametro e non quello specificato nel file di configurazione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="39cad-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="39cad-120">Se l'account di archiviazione di diagnostica si trova in una sottoscrizione diversa da quella del servizio cloud, è necessario passare al cmdlet i parametri *StorageAccountName* e *StorageAccountKey* in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="39cad-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="39cad-121">Il parametro *StorageAccountKey* non è necessario quando l'account di archiviazione di diagnostica si trova nella stessa sottoscrizione perché il cmdlet può automaticamente eseguire una query e impostare il valore della chiave durante l'abilitazione dell'estensione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="39cad-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="39cad-122">Tuttavia, se l'account di archiviazione di diagnostica si trova in una sottoscrizione diversa, il cmdlet potrebbe non essere in grado di ottenere automaticamente la chiave, quindi si deve specificare la chiave in modo esplicito tramite il parametro *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="39cad-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="39cad-123">Abilitare l'estensione della diagnostica in un servizio Cloud esistente</span><span class="sxs-lookup"><span data-stu-id="39cad-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="39cad-124">È possibile usare il cmdlet [Set AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) per abilitare o aggiornare la configurazione della diagnostica in un servizio cloud già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="39cad-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="39cad-125">Ottenere la configurazione di estensione della diagnostica corrente</span><span class="sxs-lookup"><span data-stu-id="39cad-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="39cad-126">Utilizzare il cmdlet [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) per ottenere la configurazione di diagnostica corrente per un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="39cad-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="39cad-127">Rimuovere l'estensione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="39cad-127">Remove diagnostics extension</span></span>
<span data-ttu-id="39cad-128">Per disattivare la diagnostica in un servizio cloud, è possibile utilizzare il cmdlet [Remove AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="39cad-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="39cad-129">Se è stata abilitata l'estensione di diagnostica con *Set-AzureServiceDiagnosticsExtension* o *New AzureServiceDiagnosticsExtensionConfig* senza il parametro *Role*, è possibile rimuovere l'estensione usando *Remove AzureServiceDiagnosticsExtension* senza il parametro *Role*.</span><span class="sxs-lookup"><span data-stu-id="39cad-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="39cad-130">Se il parametro *Ruolo* è stato utilizzato al momento di abilitare l'estensione, allora deve essere utilizzato anche quando si rimuove l'estensione.</span><span class="sxs-lookup"><span data-stu-id="39cad-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="39cad-131">Per rimuovere l'estensione della diagnostica da ogni singolo ruolo:</span><span class="sxs-lookup"><span data-stu-id="39cad-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="39cad-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39cad-132">Next Steps</span></span>
* <span data-ttu-id="39cad-133">Per altre istruzioni sull'uso della diagnostica di Azure e di altre tecniche per la risoluzione dei problemi, vedere [Abilitazione di Diagnostica in servizi cloud e macchine virtuali di Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="39cad-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="39cad-134">Lo [Schema di configurazione della diagnostica](https://msdn.microsoft.com/library/azure/dn782207.aspx) illustra le varie opzioni di configurazione xml per l'estensione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="39cad-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="39cad-135">Per informazioni su come abilitare l'estensione della diagnostica per le macchine virtuali, vedere [Creare una macchina virtuale Windows con monitoraggio e diagnostica mediante i modelli di Gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="39cad-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
