---
title: aaaGetting avviato con DSC di automazione di Azure | Documenti Microsoft
description: "Descrizione ed esempi di attività più comuni di hello in Azure Automation DSC Desired State Configuration)"
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
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="6aeee-103">Introduzione ad Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="6aeee-104">In questo argomento viene illustrato come toodo hello attività più comuni con Azure Automation DSC Desired State Configuration (), ad esempio la creazione, l'importazione e la compilazione di configurazioni, gestiscono troppo macchine, caricamento e visualizzazione di report.</span><span class="sxs-lookup"><span data-stu-id="6aeee-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="6aeee-105">Per una panoramica delle caratteristiche di Automation DSC per Azure, vedere [Panoramica della piattaforma DSC di Automazione di Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6aeee-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="6aeee-106">Per la documentazione di DSC, vedere [Panoramica di Windows PowerShell DSC (Desired State Configuration)](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="6aeee-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="6aeee-107">In questo argomento fornisce una toousing Guida dettagliata Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="6aeee-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="6aeee-108">Se si desidera un ambiente di esempio che è già impostato senza seguire passaggi hello descritti in questo argomento, è possibile utilizzare [hello seguenti modello ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="6aeee-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="6aeee-109">Tale modello configura un ambiente Automation DSC per Azure completo, che include una VM di Azure gestita da Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="6aeee-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aeee-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6aeee-110">Prerequisites</span></span>
<span data-ttu-id="6aeee-111">esempi di hello toocomplete in questo argomento, hello elementi seguenti sono necessari:</span><span class="sxs-lookup"><span data-stu-id="6aeee-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="6aeee-112">Un account di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6aeee-112">An Azure Automation account.</span></span> <span data-ttu-id="6aeee-113">Per istruzioni sulla creazione di un account RunAs di Automazione di Azure, vedere [Autenticare runbook con account RunAs di Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="6aeee-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="6aeee-114">Una VM di Azure Resource Manager (non classica) che esegue Windows Server 2008 R2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6aeee-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="6aeee-115">Per istruzioni sulla creazione di una macchina virtuale, vedere [creare la prima macchina virtuale Windows hello portale di Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="6aeee-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="6aeee-116">Creazione di una configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="6aeee-116">Creating a DSC configuration</span></span>
<span data-ttu-id="6aeee-117">Verrà creata una semplice [configurazione DSC](https://msdn.microsoft.com/powershell/dsc/configurations) che garantisce la presenza di hello o l'assenza di hello **Server Web** Windows funzionalità (IIS), a seconda della modalità di assegnazione di nodi.</span><span class="sxs-lookup"><span data-stu-id="6aeee-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="6aeee-118">Avviare Windows PowerShell ISE hello (o qualsiasi editor di testo).</span><span class="sxs-lookup"><span data-stu-id="6aeee-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="6aeee-119">Digitare hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="6aeee-119">Type hello following text:</span></span>
   
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
3. <span data-ttu-id="6aeee-120">Salvare il file hello come `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="6aeee-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="6aeee-121">Questa configurazione chiama una risorsa in ogni blocco di nodo, hello [risorsa WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), che garantisce la presenza di hello o l'assenza di hello **Server Web** funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6aeee-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="6aeee-122">Importazione di una configurazione in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="6aeee-123">Successivamente, si importerà configurazione hello in hello account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="6aeee-124">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-125">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-126">In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="6aeee-127">In hello **le configurazioni DSC** pannello, fare clic su **aggiungere una configurazione**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="6aeee-128">In hello **Importa configurazione** blade, Sfoglia toohello `TestConfig.ps1` file nel computer.</span><span class="sxs-lookup"><span data-stu-id="6aeee-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Schermata di hello * * blade Importa configurazione * *](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="6aeee-130">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="6aeee-131">Visualizzazione di una configurazione in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="6aeee-132">Dopo avere importato una configurazione, è possibile visualizzarlo nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="6aeee-133">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-134">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-135">In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**</span><span class="sxs-lookup"><span data-stu-id="6aeee-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="6aeee-136">In hello **le configurazioni DSC** pannello, fare clic su **TestConfig** (questo è il nome di hello della configurazione di hello è stato importato nella procedura precedente hello).</span><span class="sxs-lookup"><span data-stu-id="6aeee-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="6aeee-137">In hello **TestConfig configurazione** pannello, fare clic su **Visualizza origine configurazione**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Schermata del Pannello di configurazione TestConfig hello](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="6aeee-139">Oggetto **origine configurazione TestConfig** pannello visualizzata codice PowerShell hello per la configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="6aeee-140">Compilazione di una configurazione in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="6aeee-141">Prima di poter applicare un nodo tooa dello stato desiderato, una configurazione DSC che definisce lo stato deve essere compilata in uno o più configurazioni del nodo (documento MOF) e sul Server di Pull DSC di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="6aeee-142">Per una descrizione più dettagliata della compilazione di configurazioni in Automation DSC per Azure, vedere [Compilazione di configurazioni in Automation DSC per Azure](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="6aeee-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="6aeee-143">Per altre informazioni sulla compilazione di configurazioni, vedere [Configurazioni DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="6aeee-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="6aeee-144">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-145">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-146">In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**</span><span class="sxs-lookup"><span data-stu-id="6aeee-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="6aeee-147">In hello **le configurazioni DSC** pannello, fare clic su **TestConfig** (nome hello di hello precedentemente importata configurazione).</span><span class="sxs-lookup"><span data-stu-id="6aeee-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="6aeee-148">In hello **TestConfig configurazione** pannello, fare clic su **compilare**, quindi fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="6aeee-149">Verrà avviato un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-149">This starts a compilation job.</span></span>
   
    ![Schermata del Pannello di configurazione TestConfig hello evidenziazione pulsante di compilazione](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="6aeee-151">Quando si compila una configurazione in automazione di Azure, distribuisce automaticamente qualsiasi server di pull creato nodo toohello file MOF di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="6aeee-152">Visualizzazione di un processo di compilazione</span><span class="sxs-lookup"><span data-stu-id="6aeee-152">Viewing a compilation job</span></span>
<span data-ttu-id="6aeee-153">Dopo avere avviato una compilazione, è possibile visualizzare in hello **i processi di compilazione** riquadro in hello **configurazione** blade.</span><span class="sxs-lookup"><span data-stu-id="6aeee-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="6aeee-154">Hello **i processi di compilazione** riquadro Mostra attualmente in esecuzione, completato e processi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="6aeee-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="6aeee-155">Quando si apre un pannello di processo di compilazione, vengono visualizzate informazioni su tale processo, inclusi eventuali errori o avvisi durante, parametri di input di compilazione e configurazione di hello registri.</span><span class="sxs-lookup"><span data-stu-id="6aeee-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="6aeee-156">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-157">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-158">In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="6aeee-159">In hello **le configurazioni DSC** pannello, fare clic su **TestConfig** (nome hello di hello precedentemente importata configurazione).</span><span class="sxs-lookup"><span data-stu-id="6aeee-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="6aeee-160">In hello **i processi di compilazione** affiancato di hello **TestConfig configurazione** pannello, fare clic su uno dei processi di hello elencati.</span><span class="sxs-lookup"><span data-stu-id="6aeee-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="6aeee-161">Oggetto **processo di compilazione** si apre Pannello etichetta con data hello hello processo di compilazione è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="6aeee-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Schermata del Pannello di processo di compilazione hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="6aeee-163">Fare clic su qualsiasi riquadro in hello **processo di compilazione** pannello toosee ulteriormente i dettagli sul processo hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="6aeee-164">Visualizzazione delle configurazioni di nodo</span><span class="sxs-lookup"><span data-stu-id="6aeee-164">Viewing node configurations</span></span>
<span data-ttu-id="6aeee-165">Con il completamento di un processo di compilazione vengono create una o più configurazioni di nodo.</span><span class="sxs-lookup"><span data-stu-id="6aeee-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="6aeee-166">Una configurazione del nodo è un documento MOF è il server di pull toohello distribuito e pronto toobe estratti e applicato da uno o più nodi.</span><span class="sxs-lookup"><span data-stu-id="6aeee-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="6aeee-167">È possibile visualizzare le configurazioni del nodo hello nell'account di automazione in hello **configurazioni del nodo DSC** blade.</span><span class="sxs-lookup"><span data-stu-id="6aeee-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="6aeee-168">Una configurazione del nodo con un nome con il modulo hello *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="6aeee-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="6aeee-169">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-170">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-171">In hello **account di automazione** pannello, fare clic su **configurazioni del nodo DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Schermata del Pannello di configurazioni del nodo DSC hello](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="6aeee-173">Caricamento di una VM di Azure per la gestione con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="6aeee-174">È possibile utilizzare macchine virtuali di Azure toomanage DSC di automazione di Azure (classica e Gestione risorse), le macchine virtuali locali, macchine Linux, le macchine virtuali AWS e computer fisici locali.</span><span class="sxs-lookup"><span data-stu-id="6aeee-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="6aeee-175">In questo argomento viene illustrata la modalità tooonboard solo macchine virtuali di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6aeee-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="6aeee-176">Per informazioni sul caricamento di altri tipi di computer, vedere [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="6aeee-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="6aeee-177">tooonboard una VM di Azure Resource Manager per la gestione da Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="6aeee-178">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-179">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-180">In hello **account di automazione** pannello, fare clic su **i nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="6aeee-181">In hello **i nodi DSC** pannello, fare clic su **macchina virtuale di Azure aggiungere**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Schermata del pannello i nodi DSC hello evidenziazione pulsante Aggiungi macchina virtuale di Azure hello](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="6aeee-183">In hello **aggiungere macchine virtuali di Azure** pannello, fare clic su **selezionare le macchine virtuali tooonboard**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="6aeee-184">In hello **selezionare le macchine virtuali** seleziona hello VM tooonboard desiderato e fare clic su pannello **OK**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="6aeee-185">Deve trattarsi di una VM di Azure Resource Manager che esegue Windows Server 2008 R2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6aeee-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="6aeee-186">In hello **aggiungere macchine virtuali di Azure** pannello, fare clic su **configurare i dati di registrazione**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="6aeee-187">In hello **registrazione** pannello, immettere il nome di hello della configurazione nodo hello desiderato tooapply toohello VM in hello **nome configurazione nodo** casella.</span><span class="sxs-lookup"><span data-stu-id="6aeee-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="6aeee-188">Nome hello di una configurazione in hello account di automazione deve corrispondere esattamente.</span><span class="sxs-lookup"><span data-stu-id="6aeee-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="6aeee-189">Specificare un nome in questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6aeee-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="6aeee-190">È possibile modificare una configurazione del nodo hello assegnato dopo il nodo di hello onboarding.</span><span class="sxs-lookup"><span data-stu-id="6aeee-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="6aeee-191">Selezionare **Riavvia il nodo se necessario** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Schermata del pannello registrazione hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="6aeee-193">configurazione nodo Hello specificata verrà applicata toohello VM a intervalli determinati dall'hello **frequenza della modalità di configurazione**, e verifica hello VM per la configurazione di nodo toohello gli aggiornamenti a intervalli determinati dall'hello  **Frequenza di aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="6aeee-194">Per ulteriori informazioni sull'utilizzo di questi valori, vedere [hello configurazione Gestione configurazione locale](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="6aeee-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="6aeee-195">In hello **aggiungere macchine virtuali di Azure** pannello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="6aeee-196">Azure verrà avviato il processo di hello di onboarding hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6aeee-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="6aeee-197">Al termine, verrà visualizzato hello VM nella hello **i nodi DSC** pannello in hello account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="6aeee-198">Visualizzazione elenco hello dei nodi DSC</span><span class="sxs-lookup"><span data-stu-id="6aeee-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="6aeee-199">È possibile visualizzare l'elenco di hello di tutti i computer che sono state caricate per la gestione di account di automazione in hello **i nodi DSC** blade.</span><span class="sxs-lookup"><span data-stu-id="6aeee-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="6aeee-200">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-201">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-202">In hello **account di automazione** pannello, fare clic su **i nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="6aeee-203">Visualizzazione di report per i nodi DSC</span><span class="sxs-lookup"><span data-stu-id="6aeee-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="6aeee-204">Ogni volta che l'automazione di Azure DSC esegue una verifica coerenza su un nodo gestito, il nodo di hello invia un server di pull toohello back-report di stato.</span><span class="sxs-lookup"><span data-stu-id="6aeee-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="6aeee-205">È possibile visualizzare questi report nel Pannello di hello per tale nodo.</span><span class="sxs-lookup"><span data-stu-id="6aeee-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="6aeee-206">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-207">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-208">In hello **account di automazione** pannello, fare clic su **i nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="6aeee-209">In hello **report** riquadro, fare clic su uno dei report hello nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Schermata del pannello Report hello](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="6aeee-211">Nel Pannello di hello per un singolo report, è possibile visualizzare le seguenti informazioni di stato per la coerenza corrispondente hello hello controllare:</span><span class="sxs-lookup"><span data-stu-id="6aeee-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="6aeee-212">Hello segnalare lo stato, se il nodo hello è "Conformi," configurazione hello "Failed", o nodo hello è "Non conforme" (quando il nodo hello è **applyandmonitor** modalità e hello macchina non è in stato di hello desiderato).</span><span class="sxs-lookup"><span data-stu-id="6aeee-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="6aeee-213">Hello ora di inizio per il controllo di coerenza hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="6aeee-214">fase di esecuzione totale Hello per garantire l'uniformità hello controllare.</span><span class="sxs-lookup"><span data-stu-id="6aeee-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="6aeee-215">controllo di tipo Hello di verifica di coerenza.</span><span class="sxs-lookup"><span data-stu-id="6aeee-215">hello type of consistency check.</span></span>
* <span data-ttu-id="6aeee-216">Eventuali errori, inclusi i messaggio di errore e codice di errore hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="6aeee-217">Le risorse DSC utilizzate in configurazione hello e hello stato di ogni risorsa (se il nodo hello è nello stato desiderato di hello per tale risorsa), è possibile fare clic su ogni risorsa tooget ulteriori informazioni per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="6aeee-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="6aeee-218">nome Hello, indirizzo IP e la modalità di configurazione del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="6aeee-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="6aeee-219">È anche possibile fare clic su **visualizzare i report non elaborati** toosee hello dati effettivi che hello nodo invia toohello server.</span><span class="sxs-lookup"><span data-stu-id="6aeee-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="6aeee-220">Per altre informazioni sull'uso di tali dati, vedere [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver)(Uso di un server di report DSC).</span><span class="sxs-lookup"><span data-stu-id="6aeee-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="6aeee-221">Può richiedere qualche tempo dopo un nodo è caricate prima hello primo report è disponibile.</span><span class="sxs-lookup"><span data-stu-id="6aeee-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="6aeee-222">Potrebbe essere necessario toowait backup too30 minuti per primo report hello dopo avere incorporato un nodo.</span><span class="sxs-lookup"><span data-stu-id="6aeee-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="6aeee-223">Riassegnazione di una configurazione di un nodo diverso nodo tooa</span><span class="sxs-lookup"><span data-stu-id="6aeee-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="6aeee-224">È possibile assegnare una configurazione di un nodo diverso toouse un nodo di hello inizialmente assegnato un oggetto.</span><span class="sxs-lookup"><span data-stu-id="6aeee-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="6aeee-225">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-226">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-227">In hello **account di automazione** pannello, fare clic su **i nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="6aeee-228">In hello **i nodi DSC** pannello, fare clic sul nome hello del nodo hello desiderato tooreassign.</span><span class="sxs-lookup"><span data-stu-id="6aeee-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="6aeee-229">Nel Pannello di hello per tale nodo, fare clic su **nodo Assign**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Schermata del pannello nodo hello evidenziazione pulsante assegnare nodo hello](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="6aeee-231">In hello **assegnare configurazione nodo** blade, hello selezionare nodo Configurazione toowhich desidera tooassign hello nodo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Schermata del Pannello di configurazione del nodo assegnare hello](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="6aeee-233">Annullamento della registrazione di un nodo</span><span class="sxs-lookup"><span data-stu-id="6aeee-233">Unregistering a node</span></span>
<span data-ttu-id="6aeee-234">Se non si desidera più toobe un nodo gestito da Automation DSC per Azure, è possibile annullarne.</span><span class="sxs-lookup"><span data-stu-id="6aeee-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="6aeee-235">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6aeee-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6aeee-236">Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6aeee-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="6aeee-237">In hello **account di automazione** pannello, fare clic su **i nodi DSC**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="6aeee-238">In hello **i nodi DSC** pannello, fare clic sul nome hello del nodo hello desiderato toounregister.</span><span class="sxs-lookup"><span data-stu-id="6aeee-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="6aeee-239">Nel Pannello di hello per tale nodo, fare clic su **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="6aeee-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Schermata del pannello nodo hello evidenziazione pulsante di annullamento della registrazione hello](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="6aeee-241">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="6aeee-241">Related Articles</span></span>
* [<span data-ttu-id="6aeee-242">Panoramica di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="6aeee-243">Caricamento di computer per la gestione con Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="6aeee-244">Panoramica di Windows PowerShell DSC (Desired State Configuration)</span><span class="sxs-lookup"><span data-stu-id="6aeee-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="6aeee-245">Cmdlet di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="6aeee-246">Prezzi di Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="6aeee-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

