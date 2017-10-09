---
title: aaaOnboarding macchine per la gestione da DSC di automazione di Azure | Documenti Microsoft
description: Come toosetup macchine per la gestione con DSC di automazione di Azure
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
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="1b51f-103">Caricamento di computer per la gestione con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="1b51f-104">Perché gestire computer con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="1b51f-105">Come [PowerShell DSC (Desired State Configuration)](https://technet.microsoft.com/library/dn249912.aspx), Automation DSC (Desired State Configuration) per Azure è un servizio semplice ma potente per la gestione della configurazione dei nodi DSC (macchine virtuali e computer fisici) in qualsiasi data center nel cloud o locale.</span><span class="sxs-lookup"><span data-stu-id="1b51f-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="1b51f-106">Consente la scalabilità tra migliaia di computer in modo rapido e facile da una posizione centrale e sicura.</span><span class="sxs-lookup"><span data-stu-id="1b51f-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="1b51f-107">È possibile caricare facilmente le macchine, assegnare loro configurazioni dichiarative e visualizzare i report che mostra ogni computer di stato di conformità toohello desiderato specificato.</span><span class="sxs-lookup"><span data-stu-id="1b51f-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="1b51f-108">livello di gestione di automazione di Azure DSC Hello è tooDSC il livello di gestione di automazione di Azure hello tooPowerShell di script.</span><span class="sxs-lookup"><span data-stu-id="1b51f-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="1b51f-109">In altre parole, in hello stesso modo in cui l'automazione di Azure consente di gestire gli script di PowerShell, consente inoltre di gestire le configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="1b51f-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="1b51f-110">toolearn ulteriori informazioni sui vantaggi di hello dell'utilizzo di Automation DSC per Azure, vedere [Cenni preliminari su automazione di Azure DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b51f-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="1b51f-111">DSC di automazione di Azure può essere utilizzato toomanage diverse macchine:</span><span class="sxs-lookup"><span data-stu-id="1b51f-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="1b51f-112">Macchine virtuali di Azure (classica)</span><span class="sxs-lookup"><span data-stu-id="1b51f-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="1b51f-113">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-113">Azure virtual machines</span></span>
* <span data-ttu-id="1b51f-114">Macchine virtuali di Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="1b51f-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="1b51f-115">Computer fisici/macchine virtuali Windows locali o in un cloud diverso da Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="1b51f-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="1b51f-116">Computer fisici/macchine virtuali Linux locali, in Azure o in un cloud diverso da Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="1b51f-117">Inoltre, se non si dispone di una configurazione della macchina toomanage pronto dal cloud hello, DSC di automazione di Azure anche utilizzabile come un endpoint solo report.</span><span class="sxs-lookup"><span data-stu-id="1b51f-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="1b51f-118">In questo modo è tooset (push) la configurazione desiderata tramite DSC locale e Visualizza dettagli report avanzati sulla conformità di nodo con hello desiderato lo stato in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b51f-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="1b51f-119">Hello le sezioni seguenti viene descritto come è possibile iniziare ogni tipo di computer tooAzure DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="1b51f-120">Macchine virtuali di Azure (classica)</span><span class="sxs-lookup"><span data-stu-id="1b51f-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="1b51f-121">Con Automation DSC per Azure, è possibile caricare facilmente le macchine virtuali Azure (versione classica) per la gestione della configurazione con hello portale di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b51f-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="1b51f-122">Quinte hello e senza un amministratore con tooremote in hello VM, hello estensione Azure VM Desired State Configuration registra hello VM con automazione di Azure DSC.</span><span class="sxs-lookup"><span data-stu-id="1b51f-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="1b51f-123">Poiché hello estensione configurazione dello stato desiderato di macchina virtuale di Azure viene eseguito in modo asincrono, i passaggi tootrack lo stato di avanzamento o risolvere i problemi sono disponibili in hello [ **onboarding di macchina virtuale di Azure di risoluzione dei problemi** ](#troubleshooting-azure-virtual-machine-onboarding)sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b51f-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="1b51f-124">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-124">Azure portal</span></span>

<span data-ttu-id="1b51f-125">In hello [portale di Azure](http://portal.azure.com/), fare clic su **Sfoglia** -> **macchine virtuali (classico)**.</span><span class="sxs-lookup"><span data-stu-id="1b51f-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="1b51f-126">Selezionare hello desiderato tooonboard macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="1b51f-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="1b51f-127">Nel Pannello di dashboard della macchina virtuale hello, fare clic su **tutte le impostazioni** -> **estensioni** -> **Aggiungi**  ->   **Automazione di Azure DSC** -> **creare**.</span><span class="sxs-lookup"><span data-stu-id="1b51f-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="1b51f-128">Immettere hello [i valori di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessarie per il caso d'uso, la chiave di registrazione dell'account di automazione e registrazione URL e facoltativamente un toohello tooassign di nodo configurazione macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1b51f-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="1b51f-129">URL di registrazione toofind hello e la chiave per la macchina hello automazione account tooonboard hello, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b51f-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="1b51f-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b51f-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
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

## <a name="azure-virtual-machines"></a><span data-ttu-id="1b51f-131">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-131">Azure virtual machines</span></span>

<span data-ttu-id="1b51f-132">DSC di automazione di Azure consente di caricare facilmente macchine virtuali di Azure per la gestione della configurazione, utilizzando hello portale di Azure, modelli di gestione risorse di Azure o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b51f-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="1b51f-133">Quinte hello e senza un amministratore con tooremote in hello VM, hello estensione Azure VM Desired State Configuration registra hello VM con automazione di Azure DSC.</span><span class="sxs-lookup"><span data-stu-id="1b51f-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="1b51f-134">Poiché hello estensione configurazione dello stato desiderato di macchina virtuale di Azure viene eseguito in modo asincrono, i passaggi tootrack lo stato di avanzamento o risolvere i problemi sono disponibili in hello [ **onboarding di macchina virtuale di Azure di risoluzione dei problemi** ](#troubleshooting-azure-virtual-machine-onboarding)sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b51f-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="1b51f-135">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-135">Azure portal</span></span>

<span data-ttu-id="1b51f-136">In hello [portale di Azure](https://portal.azure.com/), passare toohello account di automazione di Azure in cui si desidera tooonboard le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1b51f-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="1b51f-137">Nel dashboard dell'account di automazione hello, fare clic su **i nodi DSC** -> **macchina virtuale di Azure aggiungere**.</span><span class="sxs-lookup"><span data-stu-id="1b51f-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="1b51f-138">In **selezionare le macchine virtuali tooonboard**, selezionare uno o tooonboard di macchine virtuali di Azure più.</span><span class="sxs-lookup"><span data-stu-id="1b51f-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="1b51f-139">In **configurare i dati di registrazione**, immettere hello [i valori di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessari per il caso d'uso e, facoltativamente, un toohello tooassign di nodo configurazione macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1b51f-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="1b51f-140">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="1b51f-141">Macchine virtuali di Azure può essere distribuite e caricate tooAzure DSC di automazione tramite modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b51f-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="1b51f-142">Vedere [configurare una macchina virtuale tramite l'estensione DSC e automazione di Azure DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) per un modello di esempio che onboards un tooAzure VM DSC di automazione esistente.</span><span class="sxs-lookup"><span data-stu-id="1b51f-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="1b51f-143">toofind hello chiave e registrazione URL di registrazione eseguito come input in questo modello, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b51f-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="1b51f-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b51f-144">PowerShell</span></span>

<span data-ttu-id="1b51f-145">Hello [registro AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet può essere utilizzato tooonboard di macchine virtuali nel portale di Azure tramite PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="1b51f-146">Macchine virtuali di Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="1b51f-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="1b51f-147">È possibile caricare facilmente le macchine virtuali Amazon Web Services per la gestione della configurazione da Automation DSC per Azure utilizzando hello AWS DSC Toolkit.</span><span class="sxs-lookup"><span data-stu-id="1b51f-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="1b51f-148">Altre informazioni sul toolkit di hello [qui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span><span class="sxs-lookup"><span data-stu-id="1b51f-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="1b51f-149">Computer fisici/macchine virtuali Windows locali o in un cloud diverso da Azure/AWS</span><span class="sxs-lookup"><span data-stu-id="1b51f-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="1b51f-150">Il computer di Windows locale e i computer di Windows in aree diverse da Azure (ad esempio, Amazon Web Services) possono rivelarsi caricate tooAzure DSC di automazione, purché dispongano dell'accesso in uscita toohello internet, con pochi semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="1b51f-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="1b51f-151">Verificare che hello di versione più recente del [WMF 5](http://aka.ms/wmf5latest) viene installato nei computer hello desiderato tooonboard tooAzure DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="1b51f-152">Seguire le direzioni di hello nella sezione [ **generazione DSC metaconfigurazioni** ](#generating-dsc-metaconfigurations) seguito toogenerate una cartella contenente hello necessari metaconfigurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="1b51f-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="1b51f-153">Si applica in modalità remota hello DSC PowerShell metaconfigurazione toohello le macchine da tooonboard.</span><span class="sxs-lookup"><span data-stu-id="1b51f-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="1b51f-154">**Questo comando viene eseguito dalla macchina di Hello deve avere più recente di hello [WMF 5](http://aka.ms/wmf5latest) installato**:</span><span class="sxs-lookup"><span data-stu-id="1b51f-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="1b51f-155">Se non è possibile applicare metaconfigurazioni di PowerShell DSC hello in modalità remota, è possibile copiare cartella metaconfigurazioni hello dal passaggio 2 in tooonboard ogni computer.</span><span class="sxs-lookup"><span data-stu-id="1b51f-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="1b51f-156">Chiamare quindi **Set-DscLocalConfigurationManager** in ogni tooonboard macchina locale.</span><span class="sxs-lookup"><span data-stu-id="1b51f-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="1b51f-157">Utilizzo di hello portale di Azure o i cmdlet, verificare che hello macchine tooonboard ora visualizzati come nodi DSC registrato nell'account di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b51f-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="1b51f-158">Computer fisici/macchine virtuali Linux locali, in Azure o in un cloud diverso da Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="1b51f-159">Computer Linux locale, i computer Linux in Azure, oltre a macchine Linux in cloud di Azure non caricate tooAzure DSC di automazione, purché dispongano dell'accesso in uscita toohello internet, con pochi semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="1b51f-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="1b51f-160">Verificare che hello di versione più recente del [PowerShell DSC per Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) viene installato nei computer hello desiderato tooonboard tooAzure DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="1b51f-161">Se hello [valori predefiniti di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) corrisponde il caso d'uso e si desidera tooonboard computer ad che essi **entrambi** pull da e report tooAzure DSC di automazione:</span><span class="sxs-lookup"><span data-stu-id="1b51f-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="1b51f-162">TooAzure DSC di automazione del tooonboard di computer ogni Linux, utilizzare tooonboard Register.py hello impostazioni predefinite di Gestione configurazione locale DSC di PowerShell utilizzando:</span><span class="sxs-lookup"><span data-stu-id="1b51f-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="1b51f-163">toofind hello chiave e registrazione URL di registrazione per l'account di automazione, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b51f-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="1b51f-164">Se hello Configuration Manager locale DSC PowerShell predefinito **si** **non** corrisponde il caso d'uso o se si desidera tooonboard macchine in modo che solo report tooAzure DSC di automazione, ma non effettuare il pull configurazione o i moduli di PowerShell, seguire i passaggi da 3 a 6.</span><span class="sxs-lookup"><span data-stu-id="1b51f-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="1b51f-165">In caso contrario, procedere direttamente toostep 6.</span><span class="sxs-lookup"><span data-stu-id="1b51f-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="1b51f-166">Seguire le direzioni di hello in hello [ **generazione DSC metaconfigurazioni** ](#generating-dsc-metaconfigurations) sezione toogenerate una cartella contenente metaconfigurazioni DSC hello necessita.</span><span class="sxs-lookup"><span data-stu-id="1b51f-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="1b51f-167">Applica in modalità remota hello DSC PowerShell metaconfigurazione toohello le macchine da tooonboard:</span><span class="sxs-lookup"><span data-stu-id="1b51f-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="1b51f-168">Questo comando viene eseguito dalla macchina di Hello deve avere più recente di hello [WMF 5](http://aka.ms/wmf5latest) installato.</span><span class="sxs-lookup"><span data-stu-id="1b51f-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="1b51f-169">Se non è possibile applicare metaconfigurazioni di PowerShell DSC hello in modalità remota, per ogni tooonboard computer Linux, è possibile copiare la macchina hello metaconfigurazione corrispondente toothat dalla cartella hello nel passaggio 5 in computer Linux hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="1b51f-170">Chiamare quindi `SetDscLocalConfigurationManager.py` in locale in ogni computer Linux desiderato tooonboard tooAzure DSC di automazione:</span><span class="sxs-lookup"><span data-stu-id="1b51f-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="1b51f-171">Utilizzo di hello portale di Azure o i cmdlet, verificare che hello macchine tooonboard ora visualizzati come nodi DSC registrato nell'account di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b51f-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="1b51f-172">Generazione di metaconfigurazioni DSC</span><span class="sxs-lookup"><span data-stu-id="1b51f-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="1b51f-173">toogenerically caricare qualsiasi computer tooAzure DSC di automazione, un [metaconfigurazione DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) può essere generato che, quando applicata, indica ad Agente hello DSC in hello macchina toopull da e/o report tooAzure DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="1b51f-174">Metaconfigurazioni di DSC per Azure Automation DSC possono essere generato utilizzando una configurazione DSC PowerShell o i cmdlet di PowerShell di automazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="1b51f-175">Metaconfigurazioni di DSC contengono hello segreti necessiti tooonboard un account di automazione per la gestione di tooan macchina.</span><span class="sxs-lookup"><span data-stu-id="1b51f-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="1b51f-176">Verificare che tooproperly proteggere qualsiasi metaconfigurazioni DSC che crei o eliminarli dopo l'uso.</span><span class="sxs-lookup"><span data-stu-id="1b51f-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="1b51f-177">Uso di una configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="1b51f-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="1b51f-178">Aprire PowerShell ISE come amministratore hello in un computer nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="1b51f-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="1b51f-179">macchina Hello deve avere una versione più recente di hello di [WMF 5](http://aka.ms/wmf5latest) installato.</span><span class="sxs-lookup"><span data-stu-id="1b51f-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="1b51f-180">Hello Copia localmente lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="1b51f-180">Copy hello following script locally.</span></span> <span data-ttu-id="1b51f-181">Questo script contiene una configurazione DSC PowerShell per la creazione di metaconfigurazioni e tookick un comando esterno creazione metaconfigurazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
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

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="1b51f-182">Compilare il codice di registrazione hello e l'URL per l'account di automazione, nonché i nomi di hello di hello macchine tooonboard.</span><span class="sxs-lookup"><span data-stu-id="1b51f-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="1b51f-183">Tutti gli altri parametri sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="1b51f-183">All other parameters are optional.</span></span> <span data-ttu-id="1b51f-184">toofind hello chiave e registrazione URL di registrazione per l'account di automazione, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b51f-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="1b51f-185">Se si desidera hello macchine tooreport DSC stato informazioni tooAzure DSC di automazione, ma non effettuare il pull configurazione o i moduli di PowerShell, impostare hello **ReportOnly** tootrue di parametro.</span><span class="sxs-lookup"><span data-stu-id="1b51f-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="1b51f-186">Eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-186">Run hello script.</span></span> <span data-ttu-id="1b51f-187">È ora una cartella denominata **DscMetaConfigs** nella directory di lavoro, contenente hello metaconfigurazioni di PowerShell DSC per hello macchine tooonboard (come amministratore):</span><span class="sxs-lookup"><span data-stu-id="1b51f-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="1b51f-188">Utilizzo dei cmdlet di automazione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="1b51f-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="1b51f-189">Se le impostazioni predefinite di Configuration Manager locale DSC PowerShell hello corrispondano il caso d'uso, e si desidera tooonboard macchine quale effettuare il pull da e tooAzure DSC di automazione del report, i cmdlet di automazione di Azure hello offrono un metodo semplificato di generazione hello DSC metaconfigurazioni necessita:</span><span class="sxs-lookup"><span data-stu-id="1b51f-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="1b51f-190">Aprire la console di PowerShell hello o PowerShell ISE come amministratore in un computer nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="1b51f-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="1b51f-191">Connettersi usando Gestione risorse tooAzure **Aggiungi AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="1b51f-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="1b51f-192">Scaricare metaconfigurazioni di PowerShell DSC hello per le macchine hello da tooonboard da hello automazione account toowhich desiderato tooonboard nodi:</span><span class="sxs-lookup"><span data-stu-id="1b51f-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="1b51f-193">È ora una cartella denominata ***DscMetaConfigs***, contenente hello metaconfigurazioni di PowerShell DSC per hello macchine tooonboard (come amministratore):</span><span class="sxs-lookup"><span data-stu-id="1b51f-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="1b51f-194">Registrazione sicura</span><span class="sxs-lookup"><span data-stu-id="1b51f-194">Secure registration</span></span>

<span data-ttu-id="1b51f-195">Macchine è possibile caricare in modo sicuro tooan account di automazione di Azure tramite protocollo di registrazione WMF 5 DSC hello, che consente un DSC nodo tooauthenticate tooa PowerShell DSC V2 Pull o Reporting server (inclusi DSC di automazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="1b51f-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="1b51f-196">nodo Hello Registra server toohello un **registrazione URL**, che esegue l'autenticazione utilizzando un **chiave di registrazione**.</span><span class="sxs-lookup"><span data-stu-id="1b51f-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="1b51f-197">Durante la registrazione, nodo hello DSC e i server di Pull DSC/report negoziare un certificato univoco per questo toouse nodo per la post-registrazione di autenticazione toohello server.</span><span class="sxs-lookup"><span data-stu-id="1b51f-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="1b51f-198">Questo processo impedisce ai nodi caricati di rappresentarsi reciprocamente, ad esempio nel caso di un nodo compromesso e che presenta un comportamento dannoso.</span><span class="sxs-lookup"><span data-stu-id="1b51f-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="1b51f-199">Dopo la registrazione, la chiave di registrazione hello non viene utilizzata per l'autenticazione nuovamente e viene eliminata dal nodo hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="1b51f-200">È possibile ottenere informazioni hello necessarie per il protocollo di registrazione hello DSC da hello **Gestisci chiavi** pannello nel portale di anteprima di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="1b51f-201">Aprire il pannello facendo clic sull'icona chiave hello in hello **Essentials** pannello per hello account di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="1b51f-202">URL di registrazione è il campo URL hello nel Pannello di gestione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="1b51f-203">Chiave di registrazione è hello chiave di accesso primaria o la chiave di accesso secondaria nel Pannello di gestione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="1b51f-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="1b51f-204">È possibile usare una delle due chiavi.</span><span class="sxs-lookup"><span data-stu-id="1b51f-204">Either key can be used.</span></span>

<span data-ttu-id="1b51f-205">Per maggiore sicurezza, è possono rigenerare le chiavi di accesso primarie e secondarie hello di un account di automazione in qualsiasi momento (in hello **Gestisci chiavi** blade) tooprevent nodo future registrazioni chiavi precedente.</span><span class="sxs-lookup"><span data-stu-id="1b51f-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="1b51f-206">Risoluzione dei problemi di caricamento di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="1b51f-207">Automation DSC di Azure consente di caricare macchine virtuali Windows di Azure per la gestione della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="1b51f-208">Quinte hello, hello estensione Azure VM Desired State Configuration è usato tooregister hello VM con automazione di Azure DSC.</span><span class="sxs-lookup"><span data-stu-id="1b51f-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="1b51f-209">Poiché hello estensione Azure VM DSC viene eseguito in modo asincrono, lo stato di avanzamento di rilevamento e risoluzione dei problemi relativa esecuzione potrebbe essere importante.</span><span class="sxs-lookup"><span data-stu-id="1b51f-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="1b51f-210">Qualsiasi metodo di caricamento di un tooAzure macchina virtuale Windows Azure DSC di automazione che utilizza l'estensione di configurazione dello stato desiderato di Azure VM hello potrebbe richiedere ora tooan per hello nodo tooshow backup registrato in automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b51f-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="1b51f-211">Ciò è dovuto toohello installazione di Windows Management Framework 5.0 in hello VM con l'estensione di macchina virtuale di Azure DSC hello, che è necessario tooonboard hello VM tooAzure DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="1b51f-212">tootroubleshoot o una vista stato hello dell'estensione di configurazione dello stato desiderato di macchina virtuale di Azure, nel portale di Azure hello hello passare toohello macchina virtuale viene caricato, quindi fare clic su -> **tutte le impostazioni** -> **estensioni**   ->  **DSC**.</span><span class="sxs-lookup"><span data-stu-id="1b51f-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="1b51f-213">Per altri dettagli, è possibile fare clic su **Visualizza stato dettagliato**.</span><span class="sxs-lookup"><span data-stu-id="1b51f-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="1b51f-214">Scadenza del certificato e nuova registrazione</span><span class="sxs-lookup"><span data-stu-id="1b51f-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="1b51f-215">Dopo la registrazione di un computer come un nodo DSC in Automation DSC per Azure, esistono una serie di motivi per cui potrebbe essere necessario tooreregister tale nodo nel hello futura:</span><span class="sxs-lookup"><span data-stu-id="1b51f-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="1b51f-216">Dopo la registrazione, ogni nodo negozia automaticamente un certificato univoco per l'autenticazione che scade dopo un anno.</span><span class="sxs-lookup"><span data-stu-id="1b51f-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="1b51f-217">Attualmente, hello protocollo di registrazione di PowerShell DSC automaticamente non è possibile rinnovare i certificati quando essi sono prossime alla scadenza, pertanto è necessario nodi hello tooreregister dopo un anno.</span><span class="sxs-lookup"><span data-stu-id="1b51f-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="1b51f-218">Prima di registrare di nuovo, verificare che ogni nodo esegua Windows Management Framework 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="1b51f-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="1b51f-219">Scadenza del certificato di autenticazione di un nodo, se il nodo hello non è registrato, nodo hello sarà Impossibile toocommunicate con automazione di Azure e verrà contrassegnato come 'Inattiva'.</span><span class="sxs-lookup"><span data-stu-id="1b51f-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="1b51f-220">La registrazione eseguita 90 giorni o minore dall'ora di scadenza certificato hello o in qualsiasi momento dopo l'ora di scadenza del certificato hello, verrà generato un nuovo certificato viene generato e utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1b51f-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="1b51f-221">toochange qualsiasi [i valori di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) che sono state impostate durante la registrazione iniziale del nodo di hello, ad esempio ConfigurationMode.</span><span class="sxs-lookup"><span data-stu-id="1b51f-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="1b51f-222">Attualmente, i valori dell'agente DSC possono essere modificati solo tramite la registrazione.</span><span class="sxs-lookup"><span data-stu-id="1b51f-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="1b51f-223">un'eccezione di Hello è hello configurazione nodo assegnata nodo toohello - può essere modificato direttamente in automazione di Azure DSC.</span><span class="sxs-lookup"><span data-stu-id="1b51f-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="1b51f-224">La registrazione può essere eseguita in hello allo stesso modo è stato registrato il nodo hello inizialmente, utilizzando uno dei metodi di caricamento hello descritte in questo documento.</span><span class="sxs-lookup"><span data-stu-id="1b51f-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="1b51f-225">Prima di registrare di nuovo, non è necessario toounregister un nodo da Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="1b51f-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="1b51f-226">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="1b51f-226">Related Articles</span></span>

* [<span data-ttu-id="1b51f-227">Panoramica di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="1b51f-228">Cmdlet di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="1b51f-229">Prezzi di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="1b51f-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
