---
title: Compilazione di configurazioni in Azure Automation DSC | Documentazione Microsoft
description: Questo articolo descrive come compilare configurazioni Desired State Configuration (DSC) per l'automazione di Azure.
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
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="28395-103">Compilazione di configurazioni in Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="28395-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="28395-104">È possibile compilare configurazioni dello stato desiderato (DSC, Desired State Configuration) in due modi con Automazione di Azure: nel portale di Azure e con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28395-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="28395-105">La tabella seguente consente di determinare quando usare ciascun metodo in base alle caratteristiche specifiche:</span><span class="sxs-lookup"><span data-stu-id="28395-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="28395-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="28395-106">Azure portal</span></span>

* <span data-ttu-id="28395-107">Metodo più semplice con interfaccia utente interattiva</span><span class="sxs-lookup"><span data-stu-id="28395-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="28395-108">Modulo per specificare valori di parametri semplici</span><span class="sxs-lookup"><span data-stu-id="28395-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="28395-109">Facilità di controllo dello stato dei processi</span><span class="sxs-lookup"><span data-stu-id="28395-109">Easily track job state</span></span>
* <span data-ttu-id="28395-110">Accesso autenticato con l'accesso di Azure</span><span class="sxs-lookup"><span data-stu-id="28395-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="28395-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="28395-111">Windows PowerShell</span></span>

* <span data-ttu-id="28395-112">Chiamata mediante cmdlet di Windows PowerShell nella riga di comando</span><span class="sxs-lookup"><span data-stu-id="28395-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="28395-113">Possibilità di inclusione in una soluzione automatizzata con più passaggi</span><span class="sxs-lookup"><span data-stu-id="28395-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="28395-114">Possibilità di specificare valori di parametri semplici e complessi</span><span class="sxs-lookup"><span data-stu-id="28395-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="28395-115">Possibilità di controllare lo stato dei processi</span><span class="sxs-lookup"><span data-stu-id="28395-115">Track job state</span></span>
* <span data-ttu-id="28395-116">Obbligo per il client di supporto dei cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="28395-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="28395-117">Passaggio di ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="28395-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="28395-118">Compilazione di configurazioni che usano credenziali</span><span class="sxs-lookup"><span data-stu-id="28395-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="28395-119">Una volta scelto il metodo di compilazione, è possibile seguire le rispettive procedure indicate sotto per iniziare la compilazione.</span><span class="sxs-lookup"><span data-stu-id="28395-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="28395-120">Compilazione di una configurazione DSC con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="28395-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="28395-121">Nell'account di Automazione fare clic su **Configurazioni DSC**.</span><span class="sxs-lookup"><span data-stu-id="28395-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="28395-122">Fare clic su una configurazione per aprirne il pannello.</span><span class="sxs-lookup"><span data-stu-id="28395-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="28395-123">Fare clic su **Compila**.</span><span class="sxs-lookup"><span data-stu-id="28395-123">Click **Compile**.</span></span>
4. <span data-ttu-id="28395-124">Se la configurazione non ha alcun parametro, verrà richiesto di confermare se compilarla.</span><span class="sxs-lookup"><span data-stu-id="28395-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="28395-125">Se la configurazione contiene parametri, verrà aperto il pannello **Compila configurazione** in cui sarà possibile specificare i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="28395-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="28395-126">Per altri dettagli sui parametri, vedere la sezione [**Parametri di base**](#basic-parameters) più avanti.</span><span class="sxs-lookup"><span data-stu-id="28395-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="28395-127">Viene aperto il pannello **Processo di compilazione** in cui è possibile tenere traccia dello stato del processo di compilazione e delle configurazioni dei nodi (documenti di configurazione MOF) che sono state inserite nel server di pull di Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="28395-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="28395-128">Compilazione di una configurazione DSC con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="28395-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="28395-129">È possibile usare [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) per avviare la compilazione con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28395-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="28395-130">Il codice di esempio seguente avvia la compilazione di una configurazione DSC denominata **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="28395-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="28395-131">`Start-AzureRmAutomationDscCompilationJob` restituisce un oggetto processo di compilazione che è possibile usare per tenere traccia dello stato.</span><span class="sxs-lookup"><span data-stu-id="28395-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="28395-132">È quindi possibile usare questo oggetto processo di compilazione con [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) per determinare lo stato del processo di compilazione e con [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) per visualizzarne i flussi (output).</span><span class="sxs-lookup"><span data-stu-id="28395-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="28395-133">Il codice di esempio seguente avvia la compilazione della configurazione **SampleConfig** , attende che venga completata e quindi ne visualizza i flussi.</span><span class="sxs-lookup"><span data-stu-id="28395-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="28395-134">Parametri di base</span><span class="sxs-lookup"><span data-stu-id="28395-134">Basic Parameters</span></span>
<span data-ttu-id="28395-135">La dichiarazione dei parametri nelle configurazioni DSC, inclusi i tipi e le proprietà dei parametri, funziona esattamente come nei runbook di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="28395-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="28395-136">Per altre informazioni sui parametri dei runbook, vedere [Avvio di un Runbook in Automazione di Azure](automation-starting-a-runbook.md) .</span><span class="sxs-lookup"><span data-stu-id="28395-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="28395-137">L'esempio seguente usa due parametri denominati **FeatureName** e **IsPresent**, per determinare i valori delle proprietà nella configurazione del nodo **ParametersExample.sample**, generati durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="28395-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="28395-138">È possibile compilare configurazioni DSC che usano parametri di base nel portale di Automation DSC per Azure o con Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="28395-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="28395-139">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="28395-139">Portal</span></span>

<span data-ttu-id="28395-140">Nel portale è possibile immettere i valori dei parametri dopo avere fatto clic su **Compila**.</span><span class="sxs-lookup"><span data-stu-id="28395-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![testo alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="28395-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="28395-142">PowerShell</span></span>

<span data-ttu-id="28395-143">PowerShell richiede i parametri in un elemento [hashtable](http://technet.microsoft.com/library/hh847780.aspx) dove la chiave corrisponde al nome del parametro e il valore è uguale al valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="28395-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="28395-144">Per informazioni sul passaggio di PSCredentials come parametri, vedere <a href="#credential-assets">**Asset credenziali**</a> più avanti.</span><span class="sxs-lookup"><span data-stu-id="28395-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="28395-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="28395-145">ConfigurationData</span></span>
<span data-ttu-id="28395-146">**ConfigurationData** consente di separare la configurazione strutturale dalla configurazione specifica di qualsiasi ambiente mentre si usa PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="28395-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="28395-147">Vedere il blog relativo alla [distinzione tra "cosa" e "dove" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) per altre informazioni su **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="28395-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="28395-148">È possibile usare **ConfigurationData** quando si compila in Azure Automation DSC con Azure PowerShell, ma non nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28395-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="28395-149">La configurazione DSC di esempio seguente usa **ConfigurationData** con le parole chiave **$ConfigurationData** e **$AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="28395-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="28395-150">Per questo esempio sarà necessario anche il [modulo **xWebAdministration**](https://www.powershellgallery.com/packages/xWebAdministration/):</span><span class="sxs-lookup"><span data-stu-id="28395-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="28395-151">È possibile compilare la configurazione DSC precedente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28395-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="28395-152">Il cmdlet di PowerShell seguente aggiunge due configurazioni di nodo al server di pull di Automation DSC per Azure, **ConfigurationDataSample.MyVM1** e **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="28395-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="28395-153">asset</span><span class="sxs-lookup"><span data-stu-id="28395-153">Assets</span></span>

<span data-ttu-id="28395-154">I riferimenti agli asset sono gli stessi nelle configurazioni di Azure Automation DSC e nei runbook.</span><span class="sxs-lookup"><span data-stu-id="28395-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="28395-155">Per altre informazioni, vedere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="28395-155">See the following for more information:</span></span>

* [<span data-ttu-id="28395-156">Certificati</span><span class="sxs-lookup"><span data-stu-id="28395-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="28395-157">Connessioni</span><span class="sxs-lookup"><span data-stu-id="28395-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="28395-158">Credenziali</span><span class="sxs-lookup"><span data-stu-id="28395-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="28395-159">Variabili</span><span class="sxs-lookup"><span data-stu-id="28395-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="28395-160">Asset credenziali</span><span class="sxs-lookup"><span data-stu-id="28395-160">Credential Assets</span></span>

<span data-ttu-id="28395-161">Anche se le configurazioni DSC in Automazione di Azure possono fare riferimento ad asset di credenziali con **Get-AzureRmAutomationCredential**, gli asset di credenziali possono essere passati anche con i parametri, se necessario.</span><span class="sxs-lookup"><span data-stu-id="28395-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="28395-162">Se una configurazione accetta un parametro di tipo **PSCredential** , è necessario passare il nome stringa di un asset di credenziali di Automazione di Azure come valore di tale parametro, invece di un oggetto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="28395-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="28395-163">In background, l'asset credenziali di Automazione di Azure con tale nome verrà recuperato e passato alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="28395-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="28395-164">Per garantire la sicurezza delle credenziali nelle configurazioni dei nodi (documenti di configurazione MOF), è necessario crittografare le credenziali nel file MOF delle configurazioni dei nodi.</span><span class="sxs-lookup"><span data-stu-id="28395-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="28395-165">Automazione di Azure va oltre e crittografa l'intero file MOF.</span><span class="sxs-lookup"><span data-stu-id="28395-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="28395-166">Attualmente è però necessario comunicare a PowerShell DSC che l'output delle credenziali in testo normale durante la generazione dei file MOF delle configurazioni dei nodi è corretto, perché PowerShell DSC non sa che dopo la generazione Automazione di Azure crittograferà l'intero file MOF tramite un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="28395-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="28395-167">Per comunicare a PowerShell DSC che l'output delle credenziali in testo normale nei file MOF delle configurazioni dei nodi generati è corretto, è possibile usare [**ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="28395-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="28395-168">È consigliabile passare `PSDscAllowPlainTextPassword = $true` tramite **ConfigurationData** per il nome di ogni blocco di nodi visualizzato nella configurazione DSC che usa le credenziali.</span><span class="sxs-lookup"><span data-stu-id="28395-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="28395-169">L'esempio seguente mostra una configurazione DSC che usa un asset credenziali di Automazione.</span><span class="sxs-lookup"><span data-stu-id="28395-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="28395-170">È possibile compilare la configurazione DSC precedente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28395-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="28395-171">Il cmdlet di PowerShell seguente aggiunge due configurazioni del nodo al server di pull di Automation DSC per Azure, **CredentialSample.MyVM1** e **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="28395-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="28395-172">Importazione delle configurazioni di nodo</span><span class="sxs-lookup"><span data-stu-id="28395-172">Importing node configurations</span></span>

<span data-ttu-id="28395-173">È anche possibile importare configurazioni di nodo (MOF) compilate all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="28395-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="28395-174">Uno dei vantaggi di questa operazione consiste nel fatto che le configurazioni di nodo possono essere firmate.</span><span class="sxs-lookup"><span data-stu-id="28395-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="28395-175">Una configurazione del nodo firmata viene verificata in locale in un nodo gestito dall'agente DSC, garantendo che la configurazione applicata al nodo provenga da una fonte autorizzata.</span><span class="sxs-lookup"><span data-stu-id="28395-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="28395-176">È possibile importare configurazioni firmate nell'account di Automazione di Azure, che tuttavia attualmente non supporta la compilazione di configurazioni firmate.</span><span class="sxs-lookup"><span data-stu-id="28395-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="28395-177">Il file di configurazione del nodo deve essere superiore a 1 MB per consentire l'importazione in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="28395-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="28395-178">Altre informazioni su come firmare le configurazioni del nodo firmate sono reperibili all'indirizzo: https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="28395-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="28395-179">Importazione di una configurazione del nodo nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="28395-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="28395-180">Nell'account di Automazione fare clic su **Configurazioni del nodo DSC**.</span><span class="sxs-lookup"><span data-stu-id="28395-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Configurazioni del nodo DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="28395-182">Nel pannello **Configurazioni del nodo DSC** fare clic su **Add a NodeConfiguration** (Aggiungi una configurazione nodo).</span><span class="sxs-lookup"><span data-stu-id="28395-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="28395-183">Nel pannello **Importa** fare clic sull'icona della cartella accanto alla casella di testo **Node Configuration File** (File di configurazione nodo) per cercare un file di configurazione del nodo (MOF) nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="28395-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![Cercare il file locale](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="28395-185">Immettere un nome nella casella di testo **Nome configurazione**.</span><span class="sxs-lookup"><span data-stu-id="28395-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="28395-186">Il nome deve corrispondere al nome della configurazione da cui è stata compilata la configurazione del nodo.</span><span class="sxs-lookup"><span data-stu-id="28395-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="28395-187">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="28395-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="28395-188">Importazione di una configurazione del nodo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="28395-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="28395-189">È possibile usare il cmdlet [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) per importare una configurazione del nodo nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="28395-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



