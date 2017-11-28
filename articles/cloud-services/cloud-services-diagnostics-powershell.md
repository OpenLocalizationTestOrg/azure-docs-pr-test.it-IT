---
title: aaaEnable diagnostica nei servizi Cloud di Azure tramite PowerShell | Documenti Microsoft
description: Informazioni su come diagnostica tooenable per cloud services utilizzando PowerShell
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
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="a53ce-103">Abilitare la diagnostica nei servizi cloud di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a53ce-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="a53ce-104">È possibile raccogliere dati di diagnostica come i log applicazioni, i contatori delle prestazioni e così via. da un servizio Cloud tramite hello estensione diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="a53ce-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="a53ce-105">In questo articolo viene descritto come tooenable hello estensione diagnostica di Azure per un servizio Cloud tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a53ce-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="a53ce-106">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per prerequisiti hello necessari per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a53ce-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="a53ce-107">Abilitare l'estensione delle funzionalità di diagnostica come parte della distribuzione di un servizio Cloud</span><span class="sxs-lookup"><span data-stu-id="a53ce-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="a53ce-108">Questo approccio è il tipo di integrazione toocontinuous applicabile di scenari, in cui diagnostica hello estensione può essere attivata come parte della distribuzione di hello servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a53ce-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="a53ce-109">Quando si crea una nuova distribuzione di servizio Cloud, è possibile abilitare l'estensione diagnostica hello passando hello *ExtensionConfiguration* parametro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a53ce-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="a53ce-110">Hello *ExtensionConfiguration* parametro accetta una matrice di configurazioni di diagnostica che possono essere creati utilizzando hello [New AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a53ce-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="a53ce-111">Hello esempio seguente viene illustrato come è possibile abilitare la diagnostica per un servizio cloud con un WebRole e WorkerRole, ognuno dei quali con una configurazione di diagnostica diversi.</span><span class="sxs-lookup"><span data-stu-id="a53ce-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="a53ce-112">Se il file di configurazione diagnostica hello specifica un `StorageAccount` elemento con un nome di account di archiviazione, quindi hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet utilizzeranno automaticamente l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a53ce-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="a53ce-113">Per questo toowork, account di archiviazione di hello deve toobe in hello stessa sottoscrizione come hello servizio Cloud distribuito.</span><span class="sxs-lookup"><span data-stu-id="a53ce-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="a53ce-114">Da pubblicano file di configurazione di estensione hello successivo generati da MSBuild hello Azure SDK 2.6 output di destinazione includono il nome account di archiviazione hello in base alla stringa di configurazione di diagnostica hello specificato nel file di configurazione del servizio hello (. cscfg).</span><span class="sxs-lookup"><span data-stu-id="a53ce-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="a53ce-115">script Hello riportato di seguito viene illustrato come file di configurazione delle estensioni di tooparse hello da hello l'output di destinazione di pubblicazione e configurare l'estensione diagnostica per ogni ruolo durante la distribuzione di servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a53ce-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="a53ce-116">Visual Studio Online viene utilizzato un approccio simile per le distribuzioni automatiche dei servizi Cloud con l'estensione diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="a53ce-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="a53ce-117">Per un esempio completo, vedere [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) .</span><span class="sxs-lookup"><span data-stu-id="a53ce-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="a53ce-118">Se non `StorageAccount` è stato specificato nella configurazione di diagnostica hello, è necessario toopass in hello *StorageAccountName* parametro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a53ce-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="a53ce-119">Se hello *StorageAccountName* viene specificato, quindi hello cmdlet sarà sempre utilizzare account di archiviazione hello specificato nel parametro hello e hello non è specificato nel file di configurazione di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="a53ce-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="a53ce-120">Se la diagnostica hello account di archiviazione è in una sottoscrizione diversa da hello servizio Cloud, è necessario tooexplicitly passato hello *StorageAccountName* e *StorageAccountKey* parametri cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="a53ce-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="a53ce-121">Hello *StorageAccountKey* parametro non è necessaria quando diagnostica hello account di archiviazione è in hello stessa sottoscrizione, come i cmdlet di hello automaticamente può eseguire query e impostare il valore chiave di hello quando si abilita l'estensione diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="a53ce-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="a53ce-122">Tuttavia, se hello account di archiviazione di diagnostica è in una sottoscrizione diversa, quindi hello cmdlet potrebbe non essere in grado di tooget chiave di hello automaticamente e tooexplicitly necessario specificare la chiave hello tramite hello *StorageAccountKey* parametro.</span><span class="sxs-lookup"><span data-stu-id="a53ce-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="a53ce-123">Abilitare l'estensione della diagnostica in un servizio Cloud esistente</span><span class="sxs-lookup"><span data-stu-id="a53ce-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="a53ce-124">È possibile utilizzare hello [Set AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable o aggiornamento configurazione della diagnostica in un servizio Cloud che è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a53ce-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="a53ce-125">Ottenere la configurazione di estensione della diagnostica corrente</span><span class="sxs-lookup"><span data-stu-id="a53ce-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="a53ce-126">Hello utilizzare [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello configurazione di diagnostica corrente per un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a53ce-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="a53ce-127">Rimuovere l'estensione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="a53ce-127">Remove diagnostics extension</span></span>
<span data-ttu-id="a53ce-128">tooturn disattivata diagnostica in un cloud service è possibile utilizzare hello [Remove AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a53ce-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="a53ce-129">Se è abilitata l'estensione di diagnostica hello utilizzando *Set AzureServiceDiagnosticsExtension* o hello *New AzureServiceDiagnosticsExtensionConfig* senza hello *ruolo* parametro, è possibile rimuovere l'estensione hello usando *Remove AzureServiceDiagnosticsExtension* senza hello *ruolo* parametro.</span><span class="sxs-lookup"><span data-stu-id="a53ce-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="a53ce-130">Se hello *ruolo* parametro utilizzato durante l'abilitazione di estensione hello, quindi deve essere utilizzato anche quando si rimuove l'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a53ce-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="a53ce-131">estensione di diagnostica hello tooremove da ogni singolo ruolo:</span><span class="sxs-lookup"><span data-stu-id="a53ce-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="a53ce-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a53ce-132">Next Steps</span></span>
* <span data-ttu-id="a53ce-133">Per ulteriori informazioni sull'uso di diagnostica di Azure e altri problemi di tootroubleshoot tecniche, vedere [abilitazione di diagnostica in servizi Cloud di Azure e macchine virtuali](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a53ce-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="a53ce-134">Hello [dello Schema di configurazione di diagnostica](https://msdn.microsoft.com/library/azure/dn782207.aspx) illustra diverse configurazioni xml opzioni per l'estensione diagnostica hello hello.</span><span class="sxs-lookup"><span data-stu-id="a53ce-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="a53ce-135">estensione di diagnostica tooenable hello per le macchine virtuali, vedere toolearn [creare una macchina virtuale Windows con monitoraggio e diagnostica usando il modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="a53ce-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
