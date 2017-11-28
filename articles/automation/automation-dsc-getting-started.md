---
title: Introduzione a DSC di Automazione di Azure | Microsoft Docs
description: "Spiegazione ed esempi delle attività più comuni in Automation DSC (Desired State Configuration) per Azure"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="a5d12-103">Introduzione ad Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="a5d12-104">Questo argomento illustra come eseguire le attività più comuni in Automation DSC (Desired State Configuration) per Azure, come la creazione, l'importazione e la compilazione di configurazioni, il caricamento di computer per la gestione e la visualizzazione di report.</span><span class="sxs-lookup"><span data-stu-id="a5d12-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="a5d12-105">Per una panoramica delle caratteristiche di Automation DSC per Azure, vedere [Panoramica della piattaforma DSC di Automazione di Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5d12-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="a5d12-106">Per la documentazione di DSC, vedere [Panoramica di Windows PowerShell DSC (Desired State Configuration)](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="a5d12-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="a5d12-107">Questo argomento offre una guida dettagliata all'uso di Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="a5d12-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="a5d12-108">Se si preferisce un ambiente di esempio già configurato senza seguire le procedure descritte in questo argomento, è possibile usare il [modello di Azure Resource Manager](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="a5d12-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="a5d12-109">Tale modello configura un ambiente Automation DSC per Azure completo, che include una VM di Azure gestita da Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="a5d12-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5d12-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5d12-110">Prerequisites</span></span>
<span data-ttu-id="a5d12-111">Per completare gli esempi di questo argomento, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a5d12-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="a5d12-112">Un account di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5d12-112">An Azure Automation account.</span></span> <span data-ttu-id="a5d12-113">Per istruzioni sulla creazione di un account RunAs di Automazione di Azure, vedere [Autenticare runbook con account RunAs di Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="a5d12-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="a5d12-114">Una VM di Azure Resource Manager (non classica) che esegue Windows Server 2008 R2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a5d12-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="a5d12-115">Per istruzioni sulla creazione di una VM, vedere [Creare la prima macchina virtuale Windows nel portale di Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="a5d12-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="a5d12-116">Creazione di una configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="a5d12-116">Creating a DSC configuration</span></span>
<span data-ttu-id="a5d12-117">Verrà creata una [configurazione DSC](https://msdn.microsoft.com/powershell/dsc/configurations) semplice che assicura la presenza o l'assenza della funzionalità di Windows (IIS) **Web-Server** , a seconda di come vengono assegnati i nodi.</span><span class="sxs-lookup"><span data-stu-id="a5d12-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="a5d12-118">Avviare Windows PowerShell ISE (o qualsiasi editor di testo).</span><span class="sxs-lookup"><span data-stu-id="a5d12-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="a5d12-119">Digitare il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a5d12-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="a5d12-120">Salvare il file con il nome `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="a5d12-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="a5d12-121">Questa configurazione chiama in ogni blocco di nodi una [risorsa WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource)che assicura la presenza o l'assenza della funzionalità **Web-Server** .</span><span class="sxs-lookup"><span data-stu-id="a5d12-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="a5d12-122">Importazione di una configurazione in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="a5d12-123">Successivamente, la configurazione verrà importata nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="a5d12-124">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-125">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-126">Nel pannello **Account di Automazione** fare clic su **Configurazioni DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="a5d12-127">Nel pannello **Configurazioni DSC** fare clic su **Aggiungi una configurazione**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="a5d12-128">Nel pannello **Importa configurazione** selezionare il file `TestConfig.ps1` nel computer.</span><span class="sxs-lookup"><span data-stu-id="a5d12-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Screenshot del pannello **Importa configurazione**](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="a5d12-130">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="a5d12-131">Visualizzazione di una configurazione in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="a5d12-132">Dopo aver importato una configurazione, è possibile visualizzarla nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5d12-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="a5d12-133">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-134">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-135">Nel pannello **Account di automazione** fare clic su **Configurazioni DSC**</span><span class="sxs-lookup"><span data-stu-id="a5d12-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="a5d12-136">Nel pannello **Configurazioni DSC** fare clic su **TestConfig**, ovvero il nome della configurazione importata nella procedura precedente.</span><span class="sxs-lookup"><span data-stu-id="a5d12-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="a5d12-137">Nel pannello **Configurazione TestConfig** fare clic su **Visualizza origine configurazione**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Screenshot del pannello Configurazione TestConfig](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="a5d12-139">Verrà visualizzato un pannello **Origine configurazione TestConfig** contenente il codice PowerShell per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="a5d12-140">Compilazione di una configurazione in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="a5d12-141">Per poter applicare uno stato desiderato a un nodo, è prima necessario compilare una configurazione DSC che definisce tale stato in una o più configurazioni di nodo (documenti MOF) e inserire tale configurazione DSC nel server di pull di Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="a5d12-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="a5d12-142">Per una descrizione più dettagliata della compilazione di configurazioni in Automation DSC per Azure, vedere [Compilazione di configurazioni in Automation DSC per Azure](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="a5d12-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="a5d12-143">Per altre informazioni sulla compilazione di configurazioni, vedere [Configurazioni DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="a5d12-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="a5d12-144">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-145">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-146">Nel pannello **Account di automazione** fare clic su **Configurazioni DSC**</span><span class="sxs-lookup"><span data-stu-id="a5d12-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="a5d12-147">Nel pannello **Configurazioni DSC** fare clic su **TestConfig**, ovvero il nome della configurazione importata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a5d12-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="a5d12-148">Nel pannello **Configurazione TestConfig** fare clic su **Compila**, quindi su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="a5d12-149">Verrà avviato un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-149">This starts a compilation job.</span></span>
   
    ![Screenshot del pannello Configurazione TestConfig con pulsante Compila evidenziato](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="a5d12-151">Quando si compila una configurazione in Automazione di Azure, tutti i documenti MOF delle configurazioni di nodo creati vengono distribuiti automaticamente nel server di pull.</span><span class="sxs-lookup"><span data-stu-id="a5d12-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="a5d12-152">Visualizzazione di un processo di compilazione</span><span class="sxs-lookup"><span data-stu-id="a5d12-152">Viewing a compilation job</span></span>
<span data-ttu-id="a5d12-153">Dopo aver avviato una compilazione, è possibile visualizzarla nel riquadro **Processi di compilazione** del pannello **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="a5d12-154">Nel riquadro **Processi di compilazione** vengono visualizzati i processi attualmente in esecuzione, completati e non riusciti.</span><span class="sxs-lookup"><span data-stu-id="a5d12-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="a5d12-155">Aprendo il pannello di un processo di compilazione vengono visualizzate informazioni sul processo, inclusi gli eventuali errori o avvisi rilevati, i parametri di input usati nella configurazione e i log di compilazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="a5d12-156">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-157">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-158">Nel pannello **Account di Automazione** fare clic su **Configurazioni DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="a5d12-159">Nel pannello **Configurazioni DSC** fare clic su **TestConfig**, ovvero il nome della configurazione importata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a5d12-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="a5d12-160">Nel riquadro **Processi di compilazione** del pannello **Configurazione TestConfig** fare clic su qualsiasi processo incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="a5d12-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="a5d12-161">Verrà visualizzato un pannello **Processo di compilazione** con la data in cui è stato avviato il processo di compilazione come etichetta.</span><span class="sxs-lookup"><span data-stu-id="a5d12-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Screenshot del pannello Processo di compilazione](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="a5d12-163">Fare clic su qualsiasi riquadro nel pannello **Processo di compilazione** per visualizzare altri dettagli sul processo.</span><span class="sxs-lookup"><span data-stu-id="a5d12-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="a5d12-164">Visualizzazione delle configurazioni di nodo</span><span class="sxs-lookup"><span data-stu-id="a5d12-164">Viewing node configurations</span></span>
<span data-ttu-id="a5d12-165">Con il completamento di un processo di compilazione vengono create una o più configurazioni di nodo.</span><span class="sxs-lookup"><span data-stu-id="a5d12-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="a5d12-166">Una configurazione di nodo è un documento MOF che viene distribuito nel server di pull ed è disponibile per il pull e l'applicazione da parte di uno o più nodi.</span><span class="sxs-lookup"><span data-stu-id="a5d12-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="a5d12-167">È possibile visualizzare le configurazioni dei nodi dell'account di Automazione nel pannello **Configurazioni del nodo DSC** .</span><span class="sxs-lookup"><span data-stu-id="a5d12-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="a5d12-168">Il nome di una configurazione del nodo presenta il formato *ConfigurationName*.*NodeName*.</span><span class="sxs-lookup"><span data-stu-id="a5d12-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="a5d12-169">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-170">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-171">Nel pannello **Account di automazione** fare clic su **Configurazioni del nodo DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Screenshot del pannello Configurazioni del nodo DSC](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="a5d12-173">Caricamento di una VM di Azure per la gestione con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="a5d12-174">È possibile usare Automation DSC per Azure per gestire VM di Azure (sia classiche che di Resource Manager), VM locali, computer Linux, VM di AWS e computer fisici locali.</span><span class="sxs-lookup"><span data-stu-id="a5d12-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="a5d12-175">In questo argomento viene descritto soltanto il caricamento di VM di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a5d12-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="a5d12-176">Per informazioni sul caricamento di altri tipi di computer, vedere [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="a5d12-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="a5d12-177">Per caricare una VM di Azure Resource Manager per la gestione con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="a5d12-178">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-179">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-180">Nel pannello **Account di automazione** fare clic su **Nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5d12-181">Nel pannello **Nodi DSC** fare clic su **Aggiungi macchina virtuale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Screenshot del pannello Nodi DSC con pulsante Aggiungi macchina virtuale di Azure evidenziato](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="a5d12-183">Nel pannello **Aggiungi macchine virtuali di Azure** fare clic su **Seleziona macchine virtuali da caricare**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="a5d12-184">Nel pannello **Seleziona macchine virtuali** selezionare la VM da caricare e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a5d12-185">Deve trattarsi di una VM di Azure Resource Manager che esegue Windows Server 2008 R2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a5d12-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="a5d12-186">Nel pannello **Aggiungi macchine virtuali di Azure** fare clic su **Configura i dati di registrazione**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="a5d12-187">Nel pannello **Registrazione** immettere il nome della configurazione del nodo che si vuole applicare alla VM nella casella **Nome della configurazione del nodo**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="a5d12-188">Deve corrispondere esattamente al nome di una configurazione di nodo nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="a5d12-189">Specificare un nome in questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="a5d12-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="a5d12-190">È possibile modificare la configurazione di nodo assegnata dopo il caricamento del nodo.</span><span class="sxs-lookup"><span data-stu-id="a5d12-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="a5d12-191">Selezionare **Riavvia il nodo se necessario** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Screenshot del pannello Registrazione](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="a5d12-193">La configurazione del nodo specificata verrà applicata alla VM agli intervalli specificati in **Frequenza modalità di configurazione** e la VM verificherà la disponibilità di aggiornamenti agli intervalli specificati in **Frequenza di aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="a5d12-194">Per altre informazioni sul modo in cui vengono usati questi valori, vedere [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig)(Configurazione di Gestione configurazione locale).</span><span class="sxs-lookup"><span data-stu-id="a5d12-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="a5d12-195">Nel pannello **Aggiungi macchine virtuali di Azure** fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="a5d12-196">Azure avvierà il processo di caricamento della VM.</span><span class="sxs-lookup"><span data-stu-id="a5d12-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="a5d12-197">Al termine, la VM verrà visualizzata nel pannello **Nodi DSC** dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="a5d12-198">Visualizzazione dell'elenco dei nodi DSC</span><span class="sxs-lookup"><span data-stu-id="a5d12-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="a5d12-199">L'elenco di tutti i computer caricati per la gestione nell'account di Automazione può essere visualizzato nel pannello **Nodi DSC** .</span><span class="sxs-lookup"><span data-stu-id="a5d12-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="a5d12-200">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-201">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-202">Nel pannello **Account di automazione** fare clic su **Nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="a5d12-203">Visualizzazione di report per i nodi DSC</span><span class="sxs-lookup"><span data-stu-id="a5d12-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="a5d12-204">Ogni volta che Automation DSC per Azure esegue una verifica di coerenza su un nodo gestito, il nodo restituisce un report di stato al server di pull.</span><span class="sxs-lookup"><span data-stu-id="a5d12-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="a5d12-205">È possibile visualizzare tali report nel pannello per il nodo.</span><span class="sxs-lookup"><span data-stu-id="a5d12-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="a5d12-206">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-207">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-208">Nel pannello **Account di automazione** fare clic su **Nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5d12-209">Nel riquadro **Report** fare clic su qualsiasi report nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="a5d12-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Screenshot del pannello Report](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="a5d12-211">Nel pannello per un singolo report è possibile visualizzare per la verifica di coerenza corrispondente le informazioni di stato seguenti.</span><span class="sxs-lookup"><span data-stu-id="a5d12-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="a5d12-212">Stato del report: il nodo può essere "Conforme" o "Non conforme", quando il nodo è in modalità **ApplyAndMonitor** e il computer non è nello stato previsto, oppure la configurazione può essere "Non riuscita".</span><span class="sxs-lookup"><span data-stu-id="a5d12-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="a5d12-213">Ora di inizio della verifica di coerenza.</span><span class="sxs-lookup"><span data-stu-id="a5d12-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="a5d12-214">Runtime totale della verifica di coerenza.</span><span class="sxs-lookup"><span data-stu-id="a5d12-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="a5d12-215">Tipo di verifica di coerenza.</span><span class="sxs-lookup"><span data-stu-id="a5d12-215">The type of consistency check.</span></span>
* <span data-ttu-id="a5d12-216">Eventuali errori, con codice e messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="a5d12-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="a5d12-217">Risorse DSC usate nella configurazione e lo stato di ogni risorsa, ovvero se il nodo è nello stato previsto per la risorsa. È possibile fare clic su ogni risorsa per ottenere informazioni più dettagliate su di essa.</span><span class="sxs-lookup"><span data-stu-id="a5d12-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="a5d12-218">Nome, indirizzo IP e modalità di configurazione del nodo.</span><span class="sxs-lookup"><span data-stu-id="a5d12-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="a5d12-219">È anche possibile fare clic su **Visualizza report non elaborato** per visualizzare i dati effettivi inviati dal nodo al server.</span><span class="sxs-lookup"><span data-stu-id="a5d12-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="a5d12-220">Per altre informazioni sull'uso di tali dati, vedere [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver)(Uso di un server di report DSC).</span><span class="sxs-lookup"><span data-stu-id="a5d12-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="a5d12-221">Dopo il caricamento di un nodo, può trascorrere tempo prima che sia disponibile il primo report</span><span class="sxs-lookup"><span data-stu-id="a5d12-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="a5d12-222">e potrebbe essere necessario attendere fino a 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="a5d12-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="a5d12-223">Riassegnazione di un nodo a una diversa configurazione di nodo</span><span class="sxs-lookup"><span data-stu-id="a5d12-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="a5d12-224">È possibile assegnare un nodo in modo che usi una configurazione di nodo diversa rispetto a quella inizialmente assegnata.</span><span class="sxs-lookup"><span data-stu-id="a5d12-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="a5d12-225">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-226">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-227">Nel pannello **Account di automazione** fare clic su **Nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5d12-228">Nel pannello **Nodi DSC** fare clic sul nome del nodo da riassegnare.</span><span class="sxs-lookup"><span data-stu-id="a5d12-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="a5d12-229">Nel pannello per tale nodo fare clic u **Assegna configurazione nodo**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Screenshot del pannello del nodo con pulsante Assegna configurazione nodo evidenziato](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="a5d12-231">Nel pannello **Assegna configurazione nodo** selezionare la configurazione che si vuole assegnare al nodo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Screenshot del pannello Assegna configurazione nodo](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="a5d12-233">Annullamento della registrazione di un nodo</span><span class="sxs-lookup"><span data-stu-id="a5d12-233">Unregistering a node</span></span>
<span data-ttu-id="a5d12-234">Se non si vuole più che un nodo venga gestito da Automation DSC per Azure, è possibile annullarne la registrazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="a5d12-235">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5d12-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5d12-236">Scegliere **Tutte le risorse** dal menu Hub e quindi fare clic sul nome dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="a5d12-237">Nel pannello **Account di automazione** fare clic su **Nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5d12-238">Nel pannello **Nodi DSC** fare clic sul nome del nodo per il quale annullare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="a5d12-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="a5d12-239">Nel pannello per tale nodo fare clic su **Annulla registrazione**.</span><span class="sxs-lookup"><span data-stu-id="a5d12-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Screenshot del pannello del nodo con pulsante Annulla registrazione evidenziato](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="a5d12-241">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="a5d12-241">Related Articles</span></span>
* [<span data-ttu-id="a5d12-242">Panoramica di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="a5d12-243">Caricamento di computer per la gestione con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="a5d12-244">Panoramica di Windows PowerShell DSC (Desired State Configuration)</span><span class="sxs-lookup"><span data-stu-id="a5d12-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="a5d12-245">Cmdlet di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="a5d12-246">Prezzi di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="a5d12-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

