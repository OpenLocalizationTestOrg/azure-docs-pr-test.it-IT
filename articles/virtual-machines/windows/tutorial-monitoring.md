---
title: aaaAzure monitoraggio e macchine virtuali di Windows | Documenti Microsoft
description: 'Esercitazione: monitorare una macchina virtuale Windows con Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="62430-103">Monitorare una macchina virtuale Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="62430-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="62430-104">Monitoraggio Azure utilizza avvio toocollect gli agenti e i dati sulle prestazioni da macchine virtuali di Azure, memorizzare i dati nell'archiviazione di Azure e renderlo accessibile tramite il portale, il modulo di Azure PowerShell hello e hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="62430-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="62430-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="62430-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="62430-106">Abilitare la diagnostica di avvio in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="62430-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="62430-107">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="62430-107">View boot diagnostics</span></span>
> * <span data-ttu-id="62430-108">Visualizzare le metriche host della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="62430-108">View VM host metrics</span></span>
> * <span data-ttu-id="62430-109">Installare l'estensione diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="62430-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="62430-110">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="62430-110">View VM metrics</span></span>
> * <span data-ttu-id="62430-111">Creare un avviso</span><span class="sxs-lookup"><span data-stu-id="62430-111">Create an alert</span></span>
> * <span data-ttu-id="62430-112">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="62430-112">Set up advanced monitoring</span></span>

<span data-ttu-id="62430-113">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="62430-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="62430-114">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="62430-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="62430-115">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="62430-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="62430-116">esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="62430-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="62430-117">Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente.</span><span class="sxs-lookup"><span data-stu-id="62430-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="62430-118">Quando si utilizza l'esercitazione di hello, sostituire il gruppo di risorse hello, nome della macchina virtuale e posizione dove necessario.</span><span class="sxs-lookup"><span data-stu-id="62430-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="62430-119">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="62430-119">View boot diagnostics</span></span>

<span data-ttu-id="62430-120">Come avviare macchine virtuali di Windows, agente di diagnostica di avvio di hello acquisisce l'output dello schermo che può essere utilizzato per la risoluzione dei problemi relativi a scopo.</span><span class="sxs-lookup"><span data-stu-id="62430-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="62430-121">Questa funzionalità è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="62430-121">This capability is enabled by default.</span></span> <span data-ttu-id="62430-122">Hello acquisiti schermata catture vengono archiviati in un account di archiviazione di Azure, viene anche creato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="62430-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="62430-123">È possibile ottenere dati di diagnostica di avvio hello con hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) comando.</span><span class="sxs-lookup"><span data-stu-id="62430-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="62430-124">Nel seguente esempio di hello, la diagnostica di avvio è radice toohello scaricato hello * c:\* unità.</span><span class="sxs-lookup"><span data-stu-id="62430-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="62430-125">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="62430-125">View host metrics</span></span>

<span data-ttu-id="62430-126">Una macchina virtuale Windows ha una macchina virtuale host dedicata in Azure con cui interagisce.</span><span class="sxs-lookup"><span data-stu-id="62430-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="62430-127">Le metriche vengono automaticamente raccolte per hello Host e possono essere visualizzate nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="62430-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="62430-128">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="62430-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="62430-129">Fare clic su **metriche** hello pannello VM e quindi selezionare una delle metriche Host hello in **le metriche disponibili** toosee delle prestazioni di hello Host VM.</span><span class="sxs-lookup"><span data-stu-id="62430-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Visualizzare le metriche host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="62430-131">Installare l'estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="62430-131">Install diagnostics extension</span></span>

<span data-ttu-id="62430-132">le metriche di base host Hello sono disponibili, ma toosee più granulare e metriche specifiche di macchina virtuale, si tooneed tooinstall hello Azure estensione diagnostica per hello VM.</span><span class="sxs-lookup"><span data-stu-id="62430-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="62430-133">Hello estensione diagnostica di Azure consente un monitoraggio aggiuntivo e toobe di dati di diagnostica recuperati hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62430-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="62430-134">È possibile visualizzare queste misurazioni delle prestazioni e creare avvisi basati sulle modalità di funzionamento hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62430-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="62430-135">estensione di diagnostica Hello viene installata tramite il portale di Azure hello come segue:</span><span class="sxs-lookup"><span data-stu-id="62430-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="62430-136">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="62430-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="62430-137">Fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="62430-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="62430-138">elenco di Hello mostra che *diagnostica di avvio* è già stata abilitata dalla sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="62430-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="62430-139">Fare clic sulla casella di controllo hello *metriche base*.</span><span class="sxs-lookup"><span data-stu-id="62430-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="62430-140">Fare clic su hello **abilitare il monitoraggio a livello di guest** pulsante.</span><span class="sxs-lookup"><span data-stu-id="62430-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Visualizzare le metriche di diagnostica](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="62430-142">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="62430-142">View VM metrics</span></span>

<span data-ttu-id="62430-143">È possibile visualizzare le metriche VM hello in hello allo stesso modo visualizzato metriche di hello host macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="62430-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="62430-144">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="62430-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="62430-145">toosee come hello macchina virtuale viene eseguita, fare clic su **metriche** hello pannello VM e quindi selezionare una delle metriche di diagnostica hello in **le metriche disponibili**.</span><span class="sxs-lookup"><span data-stu-id="62430-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Visualizzare le metriche della macchina virtuale](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="62430-147">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="62430-147">Create alerts</span></span>

<span data-ttu-id="62430-148">È possibile creare avvisi basati sulle metriche di prestazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="62430-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="62430-149">Gli avvisi possono essere ad esempio toonotify utilizzato per l'utilizzo medio della CPU supera una determinata soglia o spazio su disco disponibile scende di sotto di una certa quantità.</span><span class="sxs-lookup"><span data-stu-id="62430-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="62430-150">Gli avvisi vengono visualizzati nel portale di Azure hello o possono essere inviati tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="62430-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="62430-151">È inoltre possibile attivare i runbook di automazione di Azure o Azure logica App in tooalerts risposta in corso la generazione.</span><span class="sxs-lookup"><span data-stu-id="62430-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="62430-152">Hello seguente viene creato un avviso per l'utilizzo medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="62430-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="62430-153">Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="62430-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="62430-154">Fare clic su **regole di avviso** nel pannello VM hello, quindi fare clic su **Aggiungi avviso metrica** in alto di hello del pannello avvisi hello.</span><span class="sxs-lookup"><span data-stu-id="62430-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="62430-155">Inserire un **Nome** per l'avviso, ad esempio *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="62430-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="62430-156">tootrigger un avviso quando la percentuale della CPU supera 1.0 per cinque minuti, lasciare hello tutti gli altri valori predefiniti selezionati.</span><span class="sxs-lookup"><span data-stu-id="62430-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="62430-157">Facoltativamente, selezionare la casella di hello per *i proprietari, collaboratori e lettori di posta elettronica* toosend notifica di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="62430-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="62430-158">azione predefinita Hello è toopresent una notifica nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="62430-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="62430-159">Fare clic su hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="62430-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="62430-160">Monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="62430-160">Advanced monitoring</span></span> 

<span data-ttu-id="62430-161">È possibile eseguire un monitoraggio più approfondito della macchina virtuale tramite [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="62430-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="62430-162">Se non è già stato fatto, è possibile iscriversi per avere una [versione di prova gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="62430-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="62430-163">Quando si dispone di accesso toohello OMS portale, è possibile trovare l'identificatore di chiave e dell'area di lavoro dell'area di lavoro hello nel pannello impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="62430-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="62430-164">Hello utilizzare [Set AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) specifica tootooadd hello OMS estensione toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="62430-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="62430-165">Aggiornamento hello valori delle variabili in hello seguito esempio tooreflect è chiave dell'area di lavoro OMS e area di lavoro ID.</span><span class="sxs-lookup"><span data-stu-id="62430-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="62430-166">Dopo alcuni minuti, dovrebbe essere hello nuova macchina virtuale nell'area di lavoro OMS hello.</span><span class="sxs-lookup"><span data-stu-id="62430-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![Pannello OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="62430-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62430-168">Next steps</span></span>
<span data-ttu-id="62430-169">In questa esercitazione le macchine virtuali sono state configurate ed esaminate con il Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="62430-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="62430-170">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="62430-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="62430-171">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="62430-171">Create a virtual network</span></span>
> * <span data-ttu-id="62430-172">Creare un gruppo di risorse e una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="62430-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="62430-173">Abilitare la diagnostica di avvio su hello VM</span><span class="sxs-lookup"><span data-stu-id="62430-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="62430-174">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="62430-174">View boot diagnostics</span></span>
> * <span data-ttu-id="62430-175">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="62430-175">View host metrics</span></span>
> * <span data-ttu-id="62430-176">Installare l'estensione diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="62430-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="62430-177">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="62430-177">View VM metrics</span></span>
> * <span data-ttu-id="62430-178">Creare un avviso</span><span class="sxs-lookup"><span data-stu-id="62430-178">Create an alert</span></span>
> * <span data-ttu-id="62430-179">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="62430-179">Set up advanced monitoring</span></span>

<span data-ttu-id="62430-180">Spostare toohello toolearn esercitazione successiva sul Centro protezione di Azure.</span><span class="sxs-lookup"><span data-stu-id="62430-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62430-181">Gestire la sicurezza delle VM</span><span class="sxs-lookup"><span data-stu-id="62430-181">Manage VM security</span></span>](./tutorial-azure-security.md)