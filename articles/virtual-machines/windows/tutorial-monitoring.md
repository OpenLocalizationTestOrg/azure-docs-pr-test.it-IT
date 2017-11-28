---
title: Monitoraggio di Azure e macchine virtuali Windows | Microsoft Docs
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
ms.openlocfilehash: 42a475092bdd615c23154e5f813861b0acefcf29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="ab0f6-103">Monitorare una macchina virtuale Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab0f6-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="ab0f6-104">Monitoraggio di Azure usa gli agenti per raccogliere dati di avvio e sulle prestazioni da macchine virtuali di Azure, archiviare tali dati in Archiviazione di Azure e renderli accessibili tramite il portale, il modulo Azure PowerShell e l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-104">Azure monitoring uses agents to collect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, the Azure PowerShell module, and the Azure CLI.</span></span> <span data-ttu-id="ab0f6-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="ab0f6-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab0f6-106">Abilitare la diagnostica di avvio in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="ab0f6-107">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="ab0f6-107">View boot diagnostics</span></span>
> * <span data-ttu-id="ab0f6-108">Visualizzare le metriche host della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-108">View VM host metrics</span></span>
> * <span data-ttu-id="ab0f6-109">Installare l'estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="ab0f6-109">Install the diagnostics extension</span></span>
> * <span data-ttu-id="ab0f6-110">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-110">View VM metrics</span></span>
> * <span data-ttu-id="ab0f6-111">Creare un avviso</span><span class="sxs-lookup"><span data-stu-id="ab0f6-111">Create an alert</span></span>
> * <span data-ttu-id="ab0f6-112">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="ab0f6-112">Set up advanced monitoring</span></span>

<span data-ttu-id="ab0f6-113">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ab0f6-114">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="ab0f6-115">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ab0f6-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="ab0f6-116">Per completare l'esempio contenuto in questa esercitazione è necessario disporre di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-116">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="ab0f6-117">Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="ab0f6-118">Quando si esegue l'esercitazione, sostituire il gruppo di risorse, il nome della macchina virtuale e la posizione dove necessario.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-118">When working through the tutorial, replace the resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="ab0f6-119">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="ab0f6-119">View boot diagnostics</span></span>

<span data-ttu-id="ab0f6-120">All'avvio delle macchine virtuali Windows, l'agente di diagnostica di avvio acquisisce l'output su schermo utilizzabile per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-120">As Windows virtual machines boot up, the boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="ab0f6-121">Questa funzionalità è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-121">This capability is enabled by default.</span></span> <span data-ttu-id="ab0f6-122">Le schermate acquisite vengono archiviate in un account di archiviazione di Azure, anch'esso creato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-122">The captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="ab0f6-123">È possibile ottenere i dati di diagnostica di avvio con il comando [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata).</span><span class="sxs-lookup"><span data-stu-id="ab0f6-123">You can get the boot diagnostic data with the [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="ab0f6-124">Nell'esempio seguente i dati di diagnostica di avvio vengono scaricati nella radice dell'unità *c:\*.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-124">In the following example, boot diagnostics are downloaded to the root of the *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="ab0f6-125">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="ab0f6-125">View host metrics</span></span>

<span data-ttu-id="ab0f6-126">Una macchina virtuale Windows ha una macchina virtuale host dedicata in Azure con cui interagisce.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="ab0f6-127">Le metriche per l'host vengono raccolte automaticamente e possono essere visualizzate nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-127">Metrics are automatically collected for the Host and can be viewed in the Azure portal.</span></span>

1. <span data-ttu-id="ab0f6-128">Nel portale di Azure fare clic su **Gruppi di risorse**, selezionare **myResourceGroup** e quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-128">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="ab0f6-129">Fare clic su **Metriche** nel pannello della macchina virtuale e quindi selezionare una metrica host in **Metriche disponibili** per visualizzare le prestazioni della macchina virtuale host.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-129">Click **Metrics** on the VM blade, and then select any of the Host metrics under **Available metrics** to see how the Host VM is performing.</span></span>

    ![Visualizzare le metriche host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="ab0f6-131">Installare l'estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="ab0f6-131">Install diagnostics extension</span></span>

<span data-ttu-id="ab0f6-132">Sono disponibili le metriche di base host, ma per visualizzare metriche specifiche per la macchina virtuale e più granulari è necessario installare l'estensione Diagnostica di Azure nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-132">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="ab0f6-133">L'estensione Diagnostica di Azure consente un monitoraggio aggiuntivo e il recupero dei dati di diagnostica dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-133">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="ab0f6-134">È possibile visualizzare queste metriche delle prestazioni e creare avvisi in base al funzionamento della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-134">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="ab0f6-135">L'estensione Diagnostica viene installata tramite il portale di Azure come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ab0f6-135">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="ab0f6-136">Nel portale di Azure fare clic su **Gruppi di risorse**, selezionare **myResourceGroup** e quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-136">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="ab0f6-137">Fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="ab0f6-138">L'elenco mostra che *Diagnostica di avvio* è già stata abilitata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-138">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="ab0f6-139">Selezionare la casella di controllo per *Metriche di base*.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-139">Click the check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="ab0f6-140">Fare clic sul pulsante **Abilita monitoraggio a livello di guest**.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-140">Click the **Enable guest-level monitoring** button.</span></span>

    ![Visualizzare le metriche di diagnostica](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="ab0f6-142">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-142">View VM metrics</span></span>

<span data-ttu-id="ab0f6-143">È possibile visualizzare le metriche della macchina virtuale nello stesso modo in cui sono state visualizzate le metriche della macchina virtuale host:</span><span class="sxs-lookup"><span data-stu-id="ab0f6-143">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="ab0f6-144">Nel portale di Azure fare clic su **Gruppi di risorse**, selezionare **myResourceGroup** e quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-144">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="ab0f6-145">Per visualizzare le prestazioni della macchina virtuale, fare clic su **Metriche** nel pannello della macchina virtuale, quindi selezionare una metrica di diagnostica in **Metriche disponibili**.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-145">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![Visualizzare le metriche della macchina virtuale](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="ab0f6-147">Creare avvisi</span><span class="sxs-lookup"><span data-stu-id="ab0f6-147">Create alerts</span></span>

<span data-ttu-id="ab0f6-148">È possibile creare avvisi basati sulle metriche di prestazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="ab0f6-149">Gli avvisi possono essere usati, ad esempio, per inviare una notifica quando l'uso medio della CPU supera una determinata soglia o lo spazio su disco disponibile è inferiore a una determinata quantità.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-149">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="ab0f6-150">Gli avvisi vengono visualizzati nel portale di Azure o possono essere inviati tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-150">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="ab0f6-151">In risposta agli avvisi generati, è anche possibile attivare i runbook di Automazione di Azure o App per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="ab0f6-152">L'esempio seguente crea un avviso per l'uso medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-152">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="ab0f6-153">Nel portale di Azure fare clic su **Gruppi di risorse**, selezionare **myResourceGroup** e quindi selezionare **myVM** nell'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-153">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="ab0f6-154">Nel pannello della macchina virtuale fare clic su **Regole di avviso**, quindi fare clic su **Aggiungi avviso per la metrica** nella parte superiore del pannello degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-154">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="ab0f6-155">Inserire un **Nome** per l'avviso, ad esempio *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="ab0f6-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="ab0f6-156">Per attivare un avviso quando la percentuale di CPU supera 1.0 per cinque minuti, lasciare tutte le altre impostazioni predefinite selezionate.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-156">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="ab0f6-157">Facoltativamente, è possibile selezionare la casella per *Invia messaggio di posta elettronica a proprietari, collaboratori e lettori* per inviare una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-157">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="ab0f6-158">L'azione predefinita è di presentare una notifica nel portale.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-158">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="ab0f6-159">Fare clic sul pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-159">Click the **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="ab0f6-160">Monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="ab0f6-160">Advanced monitoring</span></span> 

<span data-ttu-id="ab0f6-161">È possibile eseguire un monitoraggio più approfondito della macchina virtuale tramite [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="ab0f6-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="ab0f6-162">Se non è già stato fatto, è possibile iscriversi per avere una [versione di prova gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="ab0f6-163">Quando si ha accesso al portale di OMS, è possibile trovare la chiave e l'identificatore dell'area di lavoro nel pannello Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-163">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="ab0f6-164">Usare il comando [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) per aggiungere l'estensione OMS alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-164">Use the [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand to to add the OMS extension to the VM.</span></span> <span data-ttu-id="ab0f6-165">Aggiornare i valori delle variabili nell'esempio seguente in base alla chiave e all'identificatore dell'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-165">Update the variable values in the below sample to reflect you OMS workspace key and workspace Id.</span></span>  

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

<span data-ttu-id="ab0f6-166">Dopo alcuni minuti, la nuova macchina virtuale verrà visualizzata nell'area di lavoro di OMS.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-166">After a few minutes, you should see the new VM in the OMS workspace.</span></span> 

![Pannello OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="ab0f6-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab0f6-168">Next steps</span></span>
<span data-ttu-id="ab0f6-169">In questa esercitazione le macchine virtuali sono state configurate ed esaminate con il Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="ab0f6-170">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="ab0f6-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab0f6-171">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-171">Create a virtual network</span></span>
> * <span data-ttu-id="ab0f6-172">Creare un gruppo di risorse e una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="ab0f6-173">Abilitare la diagnostica di avvio in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-173">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="ab0f6-174">Visualizzare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="ab0f6-174">View boot diagnostics</span></span>
> * <span data-ttu-id="ab0f6-175">Visualizzare le metriche host</span><span class="sxs-lookup"><span data-stu-id="ab0f6-175">View host metrics</span></span>
> * <span data-ttu-id="ab0f6-176">Installare l'estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="ab0f6-176">Install the diagnostics extension</span></span>
> * <span data-ttu-id="ab0f6-177">Visualizzare le metriche della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab0f6-177">View VM metrics</span></span>
> * <span data-ttu-id="ab0f6-178">Creare un avviso</span><span class="sxs-lookup"><span data-stu-id="ab0f6-178">Create an alert</span></span>
> * <span data-ttu-id="ab0f6-179">Configurare il monitoraggio avanzato</span><span class="sxs-lookup"><span data-stu-id="ab0f6-179">Set up advanced monitoring</span></span>

<span data-ttu-id="ab0f6-180">Passare all'esercitazione successiva per informazioni sul Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0f6-180">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab0f6-181">Gestire la sicurezza delle VM</span><span class="sxs-lookup"><span data-stu-id="ab0f6-181">Manage VM security</span></span>](./tutorial-azure-security.md)