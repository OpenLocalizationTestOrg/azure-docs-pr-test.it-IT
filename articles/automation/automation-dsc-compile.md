---
title: configurazioni aaaCompiling in Automation DSC per Azure | Documenti Microsoft
description: Questo articolo viene descritto come le configurazioni di configurazione DSC (Desired State) toocompile per l'automazione di Azure.
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="4e5e6-103">Compilazione di configurazioni in Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="4e5e6-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="4e5e6-104">È possibile compilare le configurazioni di configurazione DSC (Desired State) in due modi con automazione di Azure: nel portale di Azure hello e con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="4e5e6-105">Hello nella tabella seguente consentono di determinare quando il metodo in base alle caratteristiche di hello di ogni toouse:</span><span class="sxs-lookup"><span data-stu-id="4e5e6-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4e5e6-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4e5e6-106">Azure portal</span></span>

* <span data-ttu-id="4e5e6-107">Metodo più semplice con interfaccia utente interattiva</span><span class="sxs-lookup"><span data-stu-id="4e5e6-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="4e5e6-108">Valori dei parametri semplice tooprovide modulo</span><span class="sxs-lookup"><span data-stu-id="4e5e6-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="4e5e6-109">Facilità di controllo dello stato dei processi</span><span class="sxs-lookup"><span data-stu-id="4e5e6-109">Easily track job state</span></span>
* <span data-ttu-id="4e5e6-110">Accesso autenticato con l'accesso di Azure</span><span class="sxs-lookup"><span data-stu-id="4e5e6-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="4e5e6-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e5e6-111">Windows PowerShell</span></span>

* <span data-ttu-id="4e5e6-112">Chiamata mediante cmdlet di Windows PowerShell nella riga di comando</span><span class="sxs-lookup"><span data-stu-id="4e5e6-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="4e5e6-113">Possibilità di inclusione in una soluzione automatizzata con più passaggi</span><span class="sxs-lookup"><span data-stu-id="4e5e6-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="4e5e6-114">Possibilità di specificare valori di parametri semplici e complessi</span><span class="sxs-lookup"><span data-stu-id="4e5e6-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="4e5e6-115">Possibilità di controllare lo stato dei processi</span><span class="sxs-lookup"><span data-stu-id="4e5e6-115">Track job state</span></span>
* <span data-ttu-id="4e5e6-116">Toosupport client necessari i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e5e6-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="4e5e6-117">Passaggio di ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="4e5e6-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="4e5e6-118">Compilazione di configurazioni che usano credenziali</span><span class="sxs-lookup"><span data-stu-id="4e5e6-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="4e5e6-119">Dopo aver scelto un metodo di compilazione, è possibile seguire procedure rispettivi di hello sotto toostart la compilazione.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="4e5e6-120">La compilazione di una configurazione DSC con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4e5e6-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="4e5e6-121">Nell'account di Automazione fare clic su **Configurazioni DSC**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="4e5e6-122">Fare clic su una configurazione tooopen il pannello.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="4e5e6-123">Fare clic su **Compila**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-123">Click **Compile**.</span></span>
4. <span data-ttu-id="4e5e6-124">Se la configurazione hello non ha alcun parametro, si tooconfirm richiesta se si desidera toocompile è.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="4e5e6-125">Se la configurazione hello include parametri, hello **configurazione compilazione** pannello verrà aperta, pertanto è possibile fornire i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="4e5e6-126">Vedere hello [ **parametri di base** ](#basic-parameters) sezione riportata di seguito per ulteriori informazioni sui parametri.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="4e5e6-127">Hello **processo di compilazione** pannello viene aperto in modo che è possibile tenere traccia dello stato del processo di compilazione hello e hello configurazioni del nodo (documenti di configurazione MOF) ha causato toobe sul Server di Pull DSC di Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="4e5e6-128">Compilazione di una configurazione DSC con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e5e6-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="4e5e6-129">È possibile utilizzare [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart la compilazione con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="4e5e6-130">Hello codice di esempio seguente viene avviata la compilazione di una configurazione DSC denominata **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="4e5e6-131">`Start-AzureRmAutomationDscCompilationJob`oggetto che è possibile utilizzare tootrack lo stato del processo restituisce una compilazione.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="4e5e6-132">È quindi possibile utilizzare questo oggetto processo di compilazione con [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) stato hello toodetermine del processo di compilazione, hello e [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview dei flussi (output).</span><span class="sxs-lookup"><span data-stu-id="4e5e6-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="4e5e6-133">Hello codice di esempio seguente viene avviata la compilazione di hello **SampleConfig** configurazione, è in attesa fino a quando non è stata completata e quindi Visualizza dei flussi.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="4e5e6-134">Parametri di base</span><span class="sxs-lookup"><span data-stu-id="4e5e6-134">Basic Parameters</span></span>
<span data-ttu-id="4e5e6-135">Dichiarazione di parametro nelle configurazioni DSC, inclusi i tipi di parametro e le proprietà, works hello stesso come runbook di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="4e5e6-136">Vedere [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md) toolearn ulteriori informazioni sui parametri di runbook.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="4e5e6-137">esempio Hello utilizza due parametri denominati **FeatureName** e **IsPresent**, i valori hello toodetermine delle proprietà in hello **ParametersExample.sample** nodo configurazione, generata durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="4e5e6-138">È possibile compilare le configurazioni DSC che utilizzano parametri di base nel portale di Azure Automation DSC hello o con Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4e5e6-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="4e5e6-139">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4e5e6-139">Portal</span></span>

<span data-ttu-id="4e5e6-140">Nel portale di hello, è possibile immettere i valori dei parametri dopo aver fatto clic **compilare**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![testo alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="4e5e6-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e5e6-142">PowerShell</span></span>

<span data-ttu-id="4e5e6-143">PowerShell richiede i parametri in un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) dove hello chiave corrisponde a nome del parametro hello e valore hello è uguale a valore del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="4e5e6-144">Per informazioni sul passaggio di PSCredentials come parametri, vedere <a href="#credential-assets">**Asset credenziali**</a> più avanti.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="4e5e6-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="4e5e6-145">ConfigurationData</span></span>
<span data-ttu-id="4e5e6-146">**ConfigurationData** consente la configurazione strutturale di tooseparate da qualsiasi configurazione dell'ambiente specifico durante l'utilizzo di PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="4e5e6-147">Vedere [separazione "Novità" da "Dove" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn ulteriori informazioni sulla **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="4e5e6-148">È possibile utilizzare **ConfigurationData** durante la compilazione in Automation DSC per Azure con Azure PowerShell, ma non nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="4e5e6-149">Hello configurazione DSC di esempio seguente viene utilizzato **ConfigurationData** tramite hello **$ConfigurationData** e **$AllNodes** parole chiave.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="4e5e6-150">È anche necessario hello [ **xWebAdministration** modulo](https://www.powershellgallery.com/packages/xWebAdministration/) per questo esempio:</span><span class="sxs-lookup"><span data-stu-id="4e5e6-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="4e5e6-151">È possibile compilare una configurazione di DSC hello sopra con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="4e5e6-152">Hello sotto PowerShell aggiunge due nodo configurazioni toohello Server di Pull DSC di Azure Automation: **ConfigurationDataSample.MyVM1** e **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="4e5e6-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="4e5e6-153">Asset</span><span class="sxs-lookup"><span data-stu-id="4e5e6-153">Assets</span></span>

<span data-ttu-id="4e5e6-154">I riferimenti di asset vengono hello stesso nei runbook e le configurazioni DSC di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="4e5e6-155">Vedere hello seguenti per ulteriori informazioni:</span><span class="sxs-lookup"><span data-stu-id="4e5e6-155">See hello following for more information:</span></span>

* [<span data-ttu-id="4e5e6-156">Certificati</span><span class="sxs-lookup"><span data-stu-id="4e5e6-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="4e5e6-157">Connessioni</span><span class="sxs-lookup"><span data-stu-id="4e5e6-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="4e5e6-158">Credenziali</span><span class="sxs-lookup"><span data-stu-id="4e5e6-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="4e5e6-159">Variabili</span><span class="sxs-lookup"><span data-stu-id="4e5e6-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="4e5e6-160">Asset credenziali</span><span class="sxs-lookup"><span data-stu-id="4e5e6-160">Credential Assets</span></span>

<span data-ttu-id="4e5e6-161">Anche se le configurazioni DSC in Automazione di Azure possono fare riferimento ad asset di credenziali con **Get-AzureRmAutomationCredential**, gli asset di credenziali possono essere passati anche con i parametri, se necessario.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="4e5e6-162">Se una configurazione accetta un parametro di **PSCredential** digitare, quindi è necessario nome di stringa hello toopass di un asset delle credenziali di automazione di Azure come valore del parametro che, anziché un oggetto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="4e5e6-163">Background hello, asset delle credenziali di automazione di Azure hello con tale nome verrà recuperato e passato toohello configurazione.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="4e5e6-164">Mantenendo le credenziali protette in configurazioni del nodo (documenti di configurazione MOF) richiede la crittografia delle credenziali hello nel file MOF di configurazione nodo hello.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="4e5e6-165">Automazione di Azure accetta ulteriormente questo passaggio e crittografa tutto il file MOF hello.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="4e5e6-166">Tuttavia, attualmente è necessario indicare PowerShell DSC è accettabile per le credenziali toobe output in formato testo normale durante la generazione del file MOF di configurazione nodo, perché DSC PowerShell non riconosce che è possibile che automazione di Azure verrà crittografia intero file MOF hello dopo il generazione tramite un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="4e5e6-167">È possibile indicare che è per le credenziali toobe restituiti in testo normale nella configurazione del nodo hello generato i file MOF DSC PowerShell utilizzando [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="4e5e6-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="4e5e6-168">È necessario passare `PSDscAllowPlainTextPassword = $true` tramite **ConfigurationData** per nome di ogni nodo del blocco che viene visualizzato nella configurazione DSC hello e utilizza le credenziali.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="4e5e6-169">Hello seguente viene illustrata una configurazione DSC che utilizza un asset delle credenziali di automazione.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="4e5e6-170">È possibile compilare una configurazione di DSC hello sopra con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="4e5e6-171">Hello sotto PowerShell aggiunge due nodo configurazioni toohello Server di Pull DSC di Azure Automation: **CredentialSample.MyVM1** e **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="4e5e6-172">Importazione delle configurazioni di nodo</span><span class="sxs-lookup"><span data-stu-id="4e5e6-172">Importing node configurations</span></span>

<span data-ttu-id="4e5e6-173">È anche possibile importare configurazioni di nodo (MOF) compilate all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="4e5e6-174">Uno dei vantaggi di questa operazione consiste nel fatto che le configurazioni di nodo possono essere firmate.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="4e5e6-175">Una configurazione di un nodo con segno viene verificata in locale in un nodo gestito da agente hello DSC, garantendo che la configurazione di hello viene applicato toohello nodo proviene da un'origine autorizzata.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="4e5e6-176">È possibile importare configurazioni firmate nell'account di Automazione di Azure, che tuttavia attualmente non supporta la compilazione di configurazioni firmate.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="4e5e6-177">Un file di configurazione del nodo deve essere non maggiore di 1 MB tooallow è toobe importati in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="4e5e6-178">È possibile ottenere informazioni come configurazioni del nodo toosign in https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="4e5e6-179">Importare una configurazione del nodo in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4e5e6-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="4e5e6-180">Nell'account di Automazione fare clic su **Configurazioni del nodo DSC**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Configurazioni del nodo DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="4e5e6-182">In hello **configurazioni del nodo DSC** pannello, fare clic su **aggiungere un NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="4e5e6-183">In hello **importazione** pannello, fare clic su hello cartella icona Avanti toohello **File di configurazione nodo** toobrowse casella di testo per un file di configurazione del nodo (MOF) nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Cercare il file locale](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="4e5e6-185">Immettere un nome in hello **nome configurazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="4e5e6-186">Questo nome deve corrispondere il nome di hello della configurazione di hello da cui è stata compilata la configurazione di un nodo hello.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="4e5e6-187">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="4e5e6-188">Importazione di una configurazione del nodo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e5e6-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="4e5e6-189">È possibile utilizzare hello [importazione AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport cmdlet una configurazione del nodo nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="4e5e6-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



