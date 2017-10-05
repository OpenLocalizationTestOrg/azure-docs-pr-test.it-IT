---
title: Onboarding di computer per la gestione con Automation DSC per Azure | Microsoft Docs
description: Come configurare i computer per la gestione con Automation DSC per Azure
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="7880a-103">Caricamento di computer per la gestione con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="7880a-104">Perché gestire computer con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="7880a-105">Come [PowerShell DSC (Desired State Configuration)](https://technet.microsoft.com/library/dn249912.aspx), Automation DSC (Desired State Configuration) per Azure è un servizio semplice ma potente per la gestione della configurazione dei nodi DSC (macchine virtuali e computer fisici) in qualsiasi data center nel cloud o locale.</span><span class="sxs-lookup"><span data-stu-id="7880a-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="7880a-106">Consente la scalabilità tra migliaia di computer in modo rapido e facile da una posizione centrale e sicura.</span><span class="sxs-lookup"><span data-stu-id="7880a-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="7880a-107">È possibile caricare facilmente i computer, assegnare agli stessi configurazioni dichiarative e visualizzare report che mostrano la conformità di ogni computer con lo stato desiderato specificato.</span><span class="sxs-lookup"><span data-stu-id="7880a-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="7880a-108">Il livello di gestione di Automation DSC per Azure è per DSC ciò che il livello di gestione di Automazione di Azure rappresenta per gli script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7880a-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="7880a-109">In altre parole, Automazione di Azure consente di gestire gli script di PowerShell e le configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="7880a-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="7880a-110">Per altre informazioni sui vantaggi dell'uso di Automation DSC per Azure, vedere [Panoramica della piattaforma DSC di Automazione di Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7880a-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="7880a-111">È possibile usare Automation DSC per Azure in molti tipi di computer.</span><span class="sxs-lookup"><span data-stu-id="7880a-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="7880a-112">Macchine virtuali di Azure (classica)</span><span class="sxs-lookup"><span data-stu-id="7880a-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="7880a-113">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-113">Azure virtual machines</span></span>
* <span data-ttu-id="7880a-114">Macchine virtuali di Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="7880a-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="7880a-115">Computer fisici/macchine virtuali Windows locali o in un cloud diverso da Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="7880a-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="7880a-116">Computer fisici/macchine virtuali Linux locali, in Azure o in un cloud diverso da Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="7880a-117">Inoltre, se non si è pronti a gestire la configurazione delle macchina virtuali dal cloud, Automation DSC per Azure può anche essere usato come endpoint solo per i report.</span><span class="sxs-lookup"><span data-stu-id="7880a-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="7880a-118">In questo modo è possibile impostare (push) la configurazione desiderata tramite DSC locale e visualizzare i dettagli dei report sulla conformità dei nodi con lo stato scelto in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="7880a-119">Le sezioni seguenti illustrano come caricare ogni tipo di computer in Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="7880a-120">Macchine virtuali di Azure (classica)</span><span class="sxs-lookup"><span data-stu-id="7880a-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="7880a-121">Con Automation DSC per Azure è possibile caricare facilmente macchine virtuali di Azure (classica) per la gestione della configurazione tramite il portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7880a-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="7880a-122">Dietro le quinte, e senza che l'amministratore debba connettersi in remoto alla VM, l'estensione DSC (Desired State Configuration) per le VM di Azure regista la VM con Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="7880a-123">Poiché l'estensione DSC per le VM di Azure viene eseguita in modalità asincrona, nella sezione seguente [**Risoluzione dei problemi di caricamento di macchine virtuali di Azure**](#troubleshooting-azure-virtual-machine-onboarding) è disponibile la procedura per tenere traccia dell'avanzamento o risolverne i problemi.</span><span class="sxs-lookup"><span data-stu-id="7880a-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="7880a-124">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-124">Azure portal</span></span>

<span data-ttu-id="7880a-125">Nel [portale di Azure](http://portal.azure.com/) fare clic su **Esplora** -> **Macchine virtuali (classico)**.</span><span class="sxs-lookup"><span data-stu-id="7880a-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="7880a-126">Selezionare la macchina virtuale Windows da caricare.</span><span class="sxs-lookup"><span data-stu-id="7880a-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="7880a-127">Nel pannello del dashboard della macchina virtuale fare clic su **Tutte le impostazioni** -> **Estensioni** -> **Aggiungi** -> **Automation DSC per Azure** -> **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7880a-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="7880a-128">Immettere i [valori di Gestione configurazione locale per PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessari per il proprio caso d'uso, la chiave e l'URL di registrazione dell'account di automazione e facoltativamente una configurazione del nodo da assegnare alla VM.</span><span class="sxs-lookup"><span data-stu-id="7880a-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="7880a-129">Per trovare l'URL e la chiave di registrazione dell'account di automazione in cui caricare la macchina virtuale, vedere la sezione [**Registrazione sicura**](#secure-registration) è disponibile la procedura per tenere traccia dell'avanzamento o risolverne i problemi.</span><span class="sxs-lookup"><span data-stu-id="7880a-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="7880a-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7880a-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="7880a-131">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-131">Azure virtual machines</span></span>

<span data-ttu-id="7880a-132">Automation DSC per Azure consente di caricare facilmente macchine virtuali di Azure per la gestione della configurazione tramite il portale di Azure, i modelli di Gestione risorse di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7880a-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="7880a-133">Dietro le quinte, e senza che l'amministratore debba connettersi in remoto alla VM, l'estensione DSC (Desired State Configuration) per le VM di Azure regista la VM con Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="7880a-134">Poiché l'estensione DSC per le VM di Azure viene eseguita in modalità asincrona, nella sezione seguente [**Risoluzione dei problemi di caricamento di macchine virtuali di Azure**](#troubleshooting-azure-virtual-machine-onboarding) è disponibile la procedura per tenere traccia dell'avanzamento o risolverne i problemi.</span><span class="sxs-lookup"><span data-stu-id="7880a-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="7880a-135">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-135">Azure portal</span></span>

<span data-ttu-id="7880a-136">Nel [portale di Azure](https://portal.azure.com/)passare all'account di Automazione di Azure in cui caricare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7880a-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="7880a-137">Nel dashboard dell'account di automazione fare clic su **Nodi DSC** -> **Aggiungi macchina virtuale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="7880a-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="7880a-138">In **Seleziona macchine virtuali da caricare**selezionare una o più macchine virtuali di Azure da caricare.</span><span class="sxs-lookup"><span data-stu-id="7880a-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="7880a-139">In **Configura dati di registrazione**immettere i [valori di Gestione configurazione locale per PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessari per il proprio caso d'uso e facoltativamente una configurazione del nodo da assegnare alla VM.</span><span class="sxs-lookup"><span data-stu-id="7880a-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="7880a-140">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="7880a-141">Le macchine virtuali di Azure possono essere distribuite e caricate in Automation DSC di Azure usando i modelli di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="7880a-142">Per un modello di esempio che carica una VM esistente in Automation DSC per Azure, vedere [Configurare una VM tramite l'estensione DSC e Automation DSC per Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) .</span><span class="sxs-lookup"><span data-stu-id="7880a-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="7880a-143">Per trovare la chiave e l'URL di registrazione accettati come input in questo modello, vedere la sezione [**Registrazione sicura**](#secure-registration) è disponibile la procedura per tenere traccia dell'avanzamento o risolverne i problemi.</span><span class="sxs-lookup"><span data-stu-id="7880a-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="7880a-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7880a-144">PowerShell</span></span>

<span data-ttu-id="7880a-145">Il cmdlet [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) può essere usato per caricare macchine virtuali nel portale di Azure tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7880a-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="7880a-146">Macchine virtuali di Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="7880a-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="7880a-147">È possibile caricare con facilità le macchine virtuali Amazon Web Services per la gestione della configurazione da Automation DSC per Azure mediante il toolkit DSC AWS.</span><span class="sxs-lookup"><span data-stu-id="7880a-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="7880a-148">Altre informazioni sul toolkit sono disponibili [qui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="7880a-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="7880a-149">Computer fisici/macchine virtuali Windows locali o in un cloud diverso da Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="7880a-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="7880a-150">I computer Windows locali e le macchine virtuali Windows in cloud non di Azure, ad esempio Amazon Web Services, possono essere caricati in Automation DSC per Azure con pochi e semplici passaggi, a condizione che abbiano l'accesso in uscita a Internet:</span><span class="sxs-lookup"><span data-stu-id="7880a-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="7880a-151">Assicurarsi che nei computer da caricare in Automation DSC per Azure sia installata la versione più recente di [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="7880a-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="7880a-152">Seguire le istruzioni riportate nella sezione [**Generazione di metaconfigurazioni DSC**](#generating-dsc-metaconfigurations) di seguito per generare una cartella contenente le metaconfigurazioni DSC necessarie.</span><span class="sxs-lookup"><span data-stu-id="7880a-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="7880a-153">Applicare in remoto la metaconfigurazione di PowerShell DSC ai computer da caricare.</span><span class="sxs-lookup"><span data-stu-id="7880a-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="7880a-154">**Nel computer dal quale viene eseguito questo comando deve essere installata la versione più recente di [WMF 5](http://aka.ms/wmf5latest)**:</span><span class="sxs-lookup"><span data-stu-id="7880a-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="7880a-155">Se non è possibile applicare le metaconfigurazioni di PowerShell DSC in remoto, copiare la cartella delle metaconfigurazioni dal passaggio 2 in ogni computer da caricare.</span><span class="sxs-lookup"><span data-stu-id="7880a-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="7880a-156">Chiamare quindi **Set-DscLocalConfigurationManager** localmente in ogni computer da caricare.</span><span class="sxs-lookup"><span data-stu-id="7880a-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="7880a-157">Tramite il portale di Azure o i cmdlet verificare che ora i computer da caricare siano visualizzati come nodi DSC registrati nell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="7880a-158">Computer fisici/macchine virtuali Linux locali, in Azure o in un cloud diverso da Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="7880a-159">I computer Linux locali, i computer Linux in Azure, e le macchine virtuali Linux in cloud non di Azure possono essere caricati in Automation DSC per Azure con pochi e semplici passaggi, a condizione che abbiano l'accesso in uscita a Internet:</span><span class="sxs-lookup"><span data-stu-id="7880a-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="7880a-160">Assicurarsi che la versione più recente di [PowerShell DSC (Desidered State Configuration) per Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) sia installata nei computer in cui caricare Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="7880a-161">Se i [valori predefiniti di Gestione configurazione locale per PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) corrispondono al caso d'uso corrente e si vogliono caricare i computer in modo che **entrambi** eseguano il pull e inviino informazioni ad Automation DSC per Azure:</span><span class="sxs-lookup"><span data-stu-id="7880a-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="7880a-162">In tutti i computer Linux da caricare in Automation DSC per Azure usare Register.py per caricarli con i valori predefiniti di Gestione configurazione locale per PowerShell DSC:</span><span class="sxs-lookup"><span data-stu-id="7880a-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="7880a-163">Per trovare la chiave e l'URL di registrazione per l'account di automazione, vedere la sezione [**Registrazione sicura**](#secure-registration) è disponibile la procedura per tenere traccia dell'avanzamento o risolverne i problemi.</span><span class="sxs-lookup"><span data-stu-id="7880a-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="7880a-164">Se i valori predefiniti di Gestione configurazione locale per PowerShell DSC **no****n** corrispondono al caso d'uso corrente o si vogliono caricare i computer in modo che inviino informazioni solo ad Automation DSC per Azure, ma non eseguano il pull della configurazione o dei moduli di PowerShell, seguire i passaggi da 3 a 6.</span><span class="sxs-lookup"><span data-stu-id="7880a-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="7880a-165">In caso contrario, andare direttamente al passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="7880a-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="7880a-166">Seguire le istruzioni riportate di seguito nella sezione [**Generazione di metaconfigurazioni DSC**](#generating-dsc-metaconfigurations) per generare una cartella contenente le metaconfigurazioni DSC necessarie.</span><span class="sxs-lookup"><span data-stu-id="7880a-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="7880a-167">Applicare in remoto la metaconfigurazione di PowerShell DSC ai computer da caricare:</span><span class="sxs-lookup"><span data-stu-id="7880a-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="7880a-168">Nel computer dal quale viene eseguito questo comando deve essere installata la versione più recente di [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="7880a-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="7880a-169">Se non è possibile caricare le metaconfigurazioni di PowerShell DSC in remoto, per ogni computer Linux da caricare copiare la metaconfigurazione corrispondente a quel computer dalla cartella nel passaggio 5 nel computer Linux.</span><span class="sxs-lookup"><span data-stu-id="7880a-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="7880a-170">Chiamare quindi `SetDscLocalConfigurationManager.py` localmente in ogni computer Linux da caricare in Automation DSC per Azure:</span><span class="sxs-lookup"><span data-stu-id="7880a-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="7880a-171">Tramite il portale di Azure o i cmdlet verificare che ora i computer da caricare siano visualizzati come nodi DSC registrati nell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="7880a-172">Generazione di metaconfigurazioni DSC</span><span class="sxs-lookup"><span data-stu-id="7880a-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="7880a-173">Per caricare in modo generico qualsiasi computer in Automation DSC per Azure, può essere generata una [metaconfigurazione DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) che, quando applicata, indichi all'agente DSC nel computer di eseguire il pull e/o inviare informazioni ad Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="7880a-174">Le metaconfigurazioni DSC per Automation DSC per Azure possono essere generate tramite una configurazione DSC di PowerShell o tramite i cmdlet PowerShell di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="7880a-175">Le metaconfigurazioni DSC contengono i segreti necessari per caricare un computer in un account di automazione per la relativa gestione.</span><span class="sxs-lookup"><span data-stu-id="7880a-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="7880a-176">Assicurarsi di proteggere adeguatamente le metaconfigurazioni DSC create oppure eliminarle dopo l'uso.</span><span class="sxs-lookup"><span data-stu-id="7880a-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="7880a-177">Uso di una configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="7880a-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="7880a-178">Aprire PowerShell ISE come amministratore in un computer nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="7880a-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="7880a-179">Nel computer deve essere installata la versione più recente di [WMF 5](http://aka.ms/wmf5latest) .</span><span class="sxs-lookup"><span data-stu-id="7880a-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="7880a-180">Copiare localmente lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="7880a-180">Copy the following script locally.</span></span> <span data-ttu-id="7880a-181">Questo script contiene una configurazione DSC di PowerShell per la creazione delle metaconfigurazioni e un comando per avviare la creazione delle metaconfigurazioni.</span><span class="sxs-lookup"><span data-stu-id="7880a-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="7880a-182">Specificare il codice di registrazione e l'URL per l'account di automazione, nonché i nomi dei computer da caricare.</span><span class="sxs-lookup"><span data-stu-id="7880a-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="7880a-183">Tutti gli altri parametri sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="7880a-183">All other parameters are optional.</span></span> <span data-ttu-id="7880a-184">Per trovare la chiave e l'URL di registrazione per l'account di automazione, vedere la sezione [**Registrazione sicura**](#secure-registration) è disponibile la procedura per tenere traccia dell'avanzamento o risolverne i problemi.</span><span class="sxs-lookup"><span data-stu-id="7880a-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="7880a-185">Se si vuole che i computer inviino informazioni sullo stato DSC ad Automation DSC per Azure ma non eseguano il pull della configurazione o dei moduli di PowerShell, impostare il parametro **ReportOnly** su true.</span><span class="sxs-lookup"><span data-stu-id="7880a-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="7880a-186">Eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="7880a-186">Run the script.</span></span> <span data-ttu-id="7880a-187">A questo punto è disponibile una cartella denominata **DscMetaConfigs** nella directory di lavoro, contenente le metaconfigurazioni di PowerShell DSC per i computer da caricare (come amministratore):</span><span class="sxs-lookup"><span data-stu-id="7880a-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="7880a-188">Uso dei cmdlet di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="7880a-189">Se i valori predefiniti di Gestione configurazione locale per PowerShell DSC corrispondono al caso d'uso corrente e si vuole caricare i computer in modo che entrambi eseguano il pull e inviino informazioni ad Automation DSC per Azure, i cmdlet di Automazione di Azure offrono un metodo semplificato per generare le metaconfigurazioni DSC necessarie:</span><span class="sxs-lookup"><span data-stu-id="7880a-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="7880a-190">Aprire la console di PowerShell o PowerShell ISE come amministratore in un computer nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="7880a-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="7880a-191">Connettersi ad Azure Resource Manager con **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="7880a-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="7880a-192">Dall'account di automazione in cui si caricheranno i nodi, scaricare le metaconfigurazioni di PowerShell DSC per i computer da caricare:</span><span class="sxs-lookup"><span data-stu-id="7880a-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="7880a-193">A questo punto è disponibile una cartella denominata ***DscMetaConfigs***, contenente le metaconfigurazioni di PowerShell DSC per i computer da caricare (come amministratore):</span><span class="sxs-lookup"><span data-stu-id="7880a-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="7880a-194">Registrazione sicura</span><span class="sxs-lookup"><span data-stu-id="7880a-194">Secure registration</span></span>

<span data-ttu-id="7880a-195">I computer possono essere caricati in modo sicuro in un account di Automazione di Azure tramite il protocollo di registrazione DSC WMF 5, che consente a un nodo DSC di autenticarsi con un server di pull o di report di PowerShell DSC V2, incluso Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="7880a-196">Il nodo si registra al server con un **URL di registrazione**, autenticandosi con una **Chiave di registrazione**.</span><span class="sxs-lookup"><span data-stu-id="7880a-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="7880a-197">Durante la registrazione, il nodo DSC e il server di pull/report DSC negoziano un certificato univoco per questo nodo da usare per l'autenticazione con il server successivamente alla registrazione.</span><span class="sxs-lookup"><span data-stu-id="7880a-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="7880a-198">Questo processo impedisce ai nodi caricati di rappresentarsi reciprocamente, ad esempio nel caso di un nodo compromesso e che presenta un comportamento dannoso.</span><span class="sxs-lookup"><span data-stu-id="7880a-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="7880a-199">Dopo la registrazione, la chiave di registrazione non viene usata di nuovo per l'autenticazione e viene eliminata dal nodo.</span><span class="sxs-lookup"><span data-stu-id="7880a-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="7880a-200">È possibile ottenere le informazioni richieste per il protocollo di registrazione DSC nel pannello **Gestisci chiavi** del portale di anteprima di Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="7880a-201">Aprire questo pannello facendo clic sull'icona della chiave nel pannello **Informazioni di base** dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="7880a-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="7880a-202">L'URL di registrazione si trova nel campo URL del pannello Gestisci chiavi.</span><span class="sxs-lookup"><span data-stu-id="7880a-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="7880a-203">La chiave di registrazione si trova nel campo Chiave di accesso primaria o Chiave di accesso secondaria del pannello Gestisci chiavi.</span><span class="sxs-lookup"><span data-stu-id="7880a-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="7880a-204">È possibile usare una delle due chiavi.</span><span class="sxs-lookup"><span data-stu-id="7880a-204">Either key can be used.</span></span>

<span data-ttu-id="7880a-205">Per maggiore sicurezza, le chiavi di accesso primaria e secondaria di un account di automazione possono essere rigenerate in qualsiasi momento, tramite il pannello **Gestisci chiavi** , per evitare l'esecuzione di registrazioni di nodi future con chiavi precedenti.</span><span class="sxs-lookup"><span data-stu-id="7880a-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="7880a-206">Risoluzione dei problemi di caricamento di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="7880a-207">Automation DSC di Azure consente di caricare macchine virtuali Windows di Azure per la gestione della configurazione.</span><span class="sxs-lookup"><span data-stu-id="7880a-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="7880a-208">Dietro le quinte, viene usata l'estensione DSC (Desired State Configuration) per le VM di Azure per registrare la VM con Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="7880a-209">Poiché l'estensione DSC (Desired State Configuration) per le VM di Azure viene eseguita in modalità asincrona, può essere importante tenere traccia dell'avanzamento e risolvere i problemi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7880a-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="7880a-210">Qualsiasi metodo di caricamento di una VM Windows di Azure in Automation DSC per Azure che usa l'estensione DSC (Desired State Configuration) per le VM di Azure può richiedere fino a un'ora prima che il modo appaia come registrato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="7880a-211">Questo comportamento è causato dall'installazione di Windows Management Framework 5.0 nella macchina virtuale da parte dell'estensione DSC per le VM di Azure, necessario per caricare la VM in Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="7880a-212">Per risolvere i problemi o visualizzare lo stato dell'estensione DSC per le macchine virtuali di Azure, nel portale di Azure passare alla macchina virtuali da caricare, quindi fare clic su -> **Tutte le impostazioni** -> **Estensioni** -> **DSC**.</span><span class="sxs-lookup"><span data-stu-id="7880a-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="7880a-213">Per altri dettagli, è possibile fare clic su **Visualizza stato dettagliato**.</span><span class="sxs-lookup"><span data-stu-id="7880a-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="7880a-214">Scadenza del certificato e nuova registrazione</span><span class="sxs-lookup"><span data-stu-id="7880a-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="7880a-215">Dopo la registrazione di un computer come nodo DSC in Automation DSC per Azure, esistono diversi motivi, che rendono necessario ripetere la registrazione del nodo in futuro:</span><span class="sxs-lookup"><span data-stu-id="7880a-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="7880a-216">Dopo la registrazione, ogni nodo negozia automaticamente un certificato univoco per l'autenticazione che scade dopo un anno.</span><span class="sxs-lookup"><span data-stu-id="7880a-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="7880a-217">Attualmente il protocollo di registrazione di PowerShell DSC non può rinnovare automaticamente i certificati quando si avvicina la scadenza, quindi è necessario registrare di nuovo i nodi dopo un anno.</span><span class="sxs-lookup"><span data-stu-id="7880a-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="7880a-218">Prima di registrare di nuovo, verificare che ogni nodo esegua Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="7880a-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="7880a-219">Se il certificato di autenticazione di un nodo scade e se il nodo non è registrato, il nodo non sarà in grado di comunicare con Automazione di Azure e sarà indicato che "Non risponde".</span><span class="sxs-lookup"><span data-stu-id="7880a-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="7880a-220">Una registrazione eseguita 90 giorni o meno dall'ora di scadenza del certificato, o in qualsiasi momento dopo l'ora di scadenza del certificato. comporterà un nuovo certificato che viene generato e utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7880a-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="7880a-221">Per modificare qualsiasi [valore di Gestione configurazione locale per PowerShell DS](https://msdn.microsoft.com/powershell/dsc/metaconfig4) impostato durante la registrazione iniziale del nodo, ad esempio ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="7880a-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="7880a-222">Attualmente, i valori dell'agente DSC possono essere modificati solo tramite la registrazione.</span><span class="sxs-lookup"><span data-stu-id="7880a-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="7880a-223">L'unica eccezione è il valore di Configurazione del nodo assegnato al nodo che può essere modificato direttamente in Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="7880a-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="7880a-224">La ripetizione della registrazione può essere eseguita così' come è stato registrato il nodo inizialmente, usando uno dei metodi di caricamento descritti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="7880a-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="7880a-225">Non è necessario annullare la registrazione di un nodo da Automation DSC per Azure prima di registrarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="7880a-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="7880a-226">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="7880a-226">Related Articles</span></span>

* [<span data-ttu-id="7880a-227">Panoramica di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="7880a-228">Cmdlet di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="7880a-229">Prezzi di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="7880a-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
