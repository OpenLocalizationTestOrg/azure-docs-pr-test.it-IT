---
title: Installare Trend Micro Deep Security in una macchina virtuale | Microsoft Docs
description: In questo articolo viene descritto come installare e configurare la sicurezza Trend Micro su una macchina virtuale creata con il modello di distribuzione classica in Azure.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: 911b8f12472dcbda3e6bfeb8c97bf1d04a63e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="c5083-103">Come installare e configurare Trend Micro Deep Security come servizio in una macchina virtuale di Windows</span><span class="sxs-lookup"><span data-stu-id="c5083-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c5083-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c5083-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c5083-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="c5083-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c5083-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="c5083-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="c5083-107">Questo articolo illustra come installare e configurare Trend Micro Deep Security as a Service in una macchina virtuale (VM) nuova o esistente che esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c5083-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="c5083-108">Deep Security as a Service offre protezione antimalware, un firewall, un sistema di prevenzione delle intrusioni e il monitoraggio dell'integrità.</span><span class="sxs-lookup"><span data-stu-id="c5083-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="c5083-109">Il client viene installato come estensione di sicurezza usando l'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c5083-109">The client is installed as a security extension via the VM Agent.</span></span> <span data-ttu-id="c5083-110">In una nuova macchina virtuale è necessario installare Deep Security Agent, in quanto l'agente di macchine virtuali viene creato automaticamente tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5083-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span></span>

<span data-ttu-id="c5083-111">Una macchina virtuale esistente creata tramite il portale classico, l'interfaccia della riga di comando di Azure o PowerShell potrebbe non disporre di un agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c5083-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="c5083-112">In una macchina virtuale esistente priva dell'agente di macchine virtuali, è necessario prima di tutto scaricare l'agente e installarlo.</span><span class="sxs-lookup"><span data-stu-id="c5083-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span></span> <span data-ttu-id="c5083-113">In questo articolo vengono descritte entrambe le situazioni.</span><span class="sxs-lookup"><span data-stu-id="c5083-113">This article covers both situations.</span></span>

<span data-ttu-id="c5083-114">Se si dispone di una sottoscrizione Trend Micro per una soluzione locale, è possibile usarla per proteggere le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5083-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span></span> <span data-ttu-id="c5083-115">Se non si è ancora clienti, è possibile iscriversi per una sottoscrizione di valutazione.</span><span class="sxs-lookup"><span data-stu-id="c5083-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="c5083-116">Per altre informazioni su questa soluzione, vedere il post di blog Trend Micro relativo all' [estensione dell'agente di macchine virtuali di Microsoft Azure per Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="c5083-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-the-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="c5083-117">Installare Deep Security Agent in una nuova VM</span><span class="sxs-lookup"><span data-stu-id="c5083-117">Install the Deep Security Agent on a new VM</span></span>

<span data-ttu-id="c5083-118">Il [portale di Azure classico](http://portal.azure.com) consente di installare l'estensione per la sicurezza di Trend Micro quando si usa un'immagine da **Marketplace** per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5083-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span></span> <span data-ttu-id="c5083-119">Quando si crea un'unica macchina virtuale, l'uso del portale è un metodo semplice per aggiungere la protezione di Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="c5083-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span></span>

<span data-ttu-id="c5083-120">L'uso di una voce di **Marketplace** determina l'avvio di una procedura guidata che consente di configurare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5083-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span></span> <span data-ttu-id="c5083-121">Usare il terzo pannello della procedura guidata, **Impostazioni**, per installare l'estensione per la sicurezza di Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="c5083-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span></span>  <span data-ttu-id="c5083-122">Per istruzioni generali, vedere [Creare una macchina virtuale con Windows nel portale di Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c5083-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>

<span data-ttu-id="c5083-123">Quando si raggiunge il pannello **Impostazioni** della procedura guidata, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c5083-123">When you get to the **Settings** blade of the wizard, do the following steps:</span></span>

1. <span data-ttu-id="c5083-124">Fare clic su **Estensioni**, quindi fare clic su **Aggiungi estensione** nel riquadro successivo.</span><span class="sxs-lookup"><span data-stu-id="c5083-124">Click **Extensions**, then click **Add extension** in the next pane.</span></span>

   ![Iniziare ad aggiungere l'estensione][1]

2. <span data-ttu-id="c5083-126">Selezionare **Deep Security Agent** nel riquadro **Nuova risorsa**.</span><span class="sxs-lookup"><span data-stu-id="c5083-126">Select **Deep Security Agent** in the **New resource** pane.</span></span> <span data-ttu-id="c5083-127">Nel riquadro Deep Security Agent fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c5083-127">In the Deep Security Agent pane, click **Create**.</span></span>

   ![Identificare Deep Security Agent][2]

3. <span data-ttu-id="c5083-129">Immettere l'**identificatore del tenant** e la **password di attivazione del tenant** per l'estensione.</span><span class="sxs-lookup"><span data-stu-id="c5083-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span></span> <span data-ttu-id="c5083-130">Se lo si desidera, è possibile immettere un **identificatore dei criteri di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="c5083-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="c5083-131">Fare quindi clic su **OK** per aggiungere il client.</span><span class="sxs-lookup"><span data-stu-id="c5083-131">Then, click **OK** to add the client.</span></span>

   ![Immettere i dettagli relativi all'estensione][3]

## <a name="install-the-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="c5083-133">Installare Deep Security Agent in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="c5083-133">Install the Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="c5083-134">Per installare l'agente in una VM esistente, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c5083-134">To install the agent on an existing VM, you need the following items:</span></span>

* <span data-ttu-id="c5083-135">Il modulo Azure PowerShell 0.8.2 o versioni successive installato nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="c5083-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="c5083-136">È possibile controllare la versione di Azure PowerShell installata con il comando **Get-Module azure | format-table version** .</span><span class="sxs-lookup"><span data-stu-id="c5083-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="c5083-137">Per istruzioni e un collegamento alla versione più recente, vedere l'argomento relativo alla [modalità di installazione e configurazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5083-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="c5083-138">Effettuare l'accesso alla sottoscrizione di Azure usando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="c5083-138">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="c5083-139">L'agente di macchine virtuali installato nella macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c5083-139">The VM Agent installed on the target virtual machine.</span></span>

<span data-ttu-id="c5083-140">Verificare innanzitutto che l'agente di macchine virtuali sia già installato.</span><span class="sxs-lookup"><span data-stu-id="c5083-140">First, verify that the VM Agent is already installed.</span></span> <span data-ttu-id="c5083-141">Specificare il nome del servizio cloud e il nome della macchina virtuale, quindi eseguire i comandi seguenti a un prompt dei comandi di Azure PowerShell di livello amministratore.</span><span class="sxs-lookup"><span data-stu-id="c5083-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="c5083-142">Sostituire tutti gli elementi all'interno delle virgolette, inclusi i caratteri < e >.</span><span class="sxs-lookup"><span data-stu-id="c5083-142">Replace everything within the quotes, including the < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="c5083-143">Se non si conosce il nome del servizio cloud e della macchina virtuale, eseguire **Get-AzureVM** per visualizzare tali informazioni per tutte le macchine virtuali nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="c5083-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span></span>

<span data-ttu-id="c5083-144">Se il comando **write-host** restituisce **True**, l'agente di macchine virtuali è installato.</span><span class="sxs-lookup"><span data-stu-id="c5083-144">If the **write-host** command returns **True**, the VM Agent is installed.</span></span> <span data-ttu-id="c5083-145">Se restituisce **False**, nel post di blog di Azure relativo all' [agente di macchine virtuali ed estensioni, parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947)sono disponibili istruzioni e un collegamento per il download.</span><span class="sxs-lookup"><span data-stu-id="c5083-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="c5083-146">Se l'agente di macchine virtuali è installato, eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="c5083-146">If the VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="c5083-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5083-147">Next steps</span></span>
<span data-ttu-id="c5083-148">Per l'avvio dell'agente sono necessari alcuni minuti dopo l'installazione.</span><span class="sxs-lookup"><span data-stu-id="c5083-148">It takes a few minutes for the agent to start running when it is installed.</span></span> <span data-ttu-id="c5083-149">In seguito è necessario attivare Deep Security sulla macchina virtuale in modo che venga gestita da un Deep Security Manager.</span><span class="sxs-lookup"><span data-stu-id="c5083-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="c5083-150">Per altre istruzioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5083-150">See the following articles for additional instructions:</span></span>

* <span data-ttu-id="c5083-151">Articolo di Trend Micro sulla [sicurezza cloud immediata per Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="c5083-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="c5083-152">Uno [Script di Windows PowerShell di esempio](http://go.microsoft.com/fwlink/?LinkId=404100) per configurare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5083-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span></span>
* <span data-ttu-id="c5083-153">[Istruzioni](http://go.microsoft.com/fwlink/?LinkId=404099) per l'esempio</span><span class="sxs-lookup"><span data-stu-id="c5083-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5083-154">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c5083-154">Additional resources</span></span>
<span data-ttu-id="c5083-155">[Come accedere a una macchina virtuale che esegue Windows Server]</span><span class="sxs-lookup"><span data-stu-id="c5083-155">[How to log on to a virtual machine running Windows Server]</span></span>

<span data-ttu-id="c5083-156">[Estensioni VM e funzionalità di Azure]</span><span class="sxs-lookup"><span data-stu-id="c5083-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
<span data-ttu-id="c5083-157">[Come accedere a una macchina virtuale che esegue Windows Server]:connect-logon.md</span><span class="sxs-lookup"><span data-stu-id="c5083-157">[How to log on to a virtual machine running Windows Server]:connect-logon.md</span></span>
<span data-ttu-id="c5083-158">[Estensioni VM e funzionalità di Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="c5083-158">[Azure VM Extensions and features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span></span>
