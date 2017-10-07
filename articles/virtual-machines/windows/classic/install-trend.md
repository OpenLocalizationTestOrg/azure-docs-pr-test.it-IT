---
title: Trend Micro Deep Security in una macchina virtuale aaaInstall | Documenti Microsoft
description: Questo articolo viene descritto come tooinstall e configurare Trend Micro security in una macchina virtuale creata con modello di distribuzione classica hello in Azure.
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
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="245d5-103">Come tooinstall e configurare Trend Micro Deep Security come servizio in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="245d5-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="245d5-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="245d5-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="245d5-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="245d5-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="245d5-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="245d5-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="245d5-107">In questo articolo illustra come tooinstall e configurare Trend Micro Deep Security come servizio in una nuova o esistente macchina virtuale (VM) che esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="245d5-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="245d5-108">Deep Security as a Service offre protezione antimalware, un firewall, un sistema di prevenzione delle intrusioni e il monitoraggio dell'integrità.</span><span class="sxs-lookup"><span data-stu-id="245d5-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="245d5-109">Hello client viene installato come un'estensione di sicurezza tramite hello agente della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="245d5-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="245d5-110">In una nuova macchina virtuale, installare hello Deep Security Agent, come hello che agente della macchina virtuale viene creato automaticamente da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="245d5-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="245d5-111">Una macchina virtuale esistente creata tramite portale classico hello, hello CLI di Azure o PowerShell potrebbe non disporre di un agente di macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="245d5-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="245d5-112">Per una macchina virtuale esistente che non dispone di hello agente della macchina virtuale, è necessario toodownload ed è necessario prima installarlo.</span><span class="sxs-lookup"><span data-stu-id="245d5-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="245d5-113">In questo articolo vengono descritte entrambe le situazioni.</span><span class="sxs-lookup"><span data-stu-id="245d5-113">This article covers both situations.</span></span>

<span data-ttu-id="245d5-114">Se si dispone di una sottoscrizione corrente da Trend Micro per una soluzione locale, è possibile utilizzare toohelp proteggere macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="245d5-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="245d5-115">Se non si è ancora clienti, è possibile iscriversi per una sottoscrizione di valutazione.</span><span class="sxs-lookup"><span data-stu-id="245d5-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="245d5-116">Per ulteriori informazioni su questa soluzione, vedere hello Trend Micro post di blog [Microsoft Azure VM agente di estensione per Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="245d5-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="245d5-117">Installare hello Deep Security Agent in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="245d5-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="245d5-118">Hello [portale di Azure](http://portal.azure.com) consente di installare l'estensione di sicurezza Trend Micro hello quando si utilizza un'immagine da hello **Marketplace** macchina virtuale di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="245d5-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="245d5-119">Se si sta creando una singola macchina virtuale, l'uso del portale di hello è una protezione tooadd facilmente da Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="245d5-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="245d5-120">Con una voce da hello **Marketplace** apre una procedura guidata che consente di imposta la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="245d5-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="245d5-121">Utilizzare hello **impostazioni** blade, pannello di terzo hello della procedura guidata hello, hello tooinstall estensione di sicurezza Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="245d5-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="245d5-122">Per istruzioni generali, vedere [creare una macchina virtuale Windows in esecuzione in Azure portal hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="245d5-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="245d5-123">Quando si ottengono toohello **impostazioni** pannello della procedura guidata hello hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="245d5-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="245d5-124">Fare clic su **estensioni**, quindi fare clic su **aggiungere estensione** nel riquadro successivo di hello.</span><span class="sxs-lookup"><span data-stu-id="245d5-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Iniziare ad aggiungere l'estensione hello][1]

2. <span data-ttu-id="245d5-126">Selezionare **Deep Security Agent** in hello **nuova risorsa** riquadro.</span><span class="sxs-lookup"><span data-stu-id="245d5-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="245d5-127">Nel riquadro di hello Deep Security Agent, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="245d5-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Identificare Deep Security Agent][2]

3. <span data-ttu-id="245d5-129">Immettere hello **identificatore del Tenant** e **Password di attivazione Tenant** per estensione hello.</span><span class="sxs-lookup"><span data-stu-id="245d5-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="245d5-130">Se lo si desidera, è possibile immettere un **identificatore dei criteri di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="245d5-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="245d5-131">Quindi, fare clic su **OK** client hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="245d5-131">Then, click **OK** tooadd hello client.</span></span>

   ![Immettere i dettagli relativi all'estensione][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="245d5-133">Installare hello Deep Security Agent in una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="245d5-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="245d5-134">agente di hello tooinstall in una macchina virtuale esistente, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="245d5-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="245d5-135">modulo di Azure PowerShell Hello, versione 0.8.2 o successive, installato nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="245d5-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="245d5-136">È possibile controllare la versione hello di Azure PowerShell che è stato installato tramite hello **Get-Module azure | versione formato tabella** comando.</span><span class="sxs-lookup"><span data-stu-id="245d5-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="245d5-137">Per istruzioni e una versione più recente toohello di collegamento, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="245d5-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="245d5-138">Accedi con sottoscrizione di Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="245d5-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="245d5-139">Agente VM installato nella macchina virtuale di destinazione hello Hello.</span><span class="sxs-lookup"><span data-stu-id="245d5-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="245d5-140">Verificare innanzitutto che hello che agente VM è già installato.</span><span class="sxs-lookup"><span data-stu-id="245d5-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="245d5-141">Specificare nome del servizio cloud hello e nome della macchina virtuale e quindi eseguire hello seguenti comandi in un prompt dei comandi di Azure PowerShell a livello di amministratore.</span><span class="sxs-lookup"><span data-stu-id="245d5-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="245d5-142">Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri.</span><span class="sxs-lookup"><span data-stu-id="245d5-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="245d5-143">Se non si conosce il nome di macchina virtuale e servizio cloud hello, eseguire **Get-AzureVM** toodisplay che le informazioni su tutti hello macchine virtuali nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="245d5-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="245d5-144">Se hello **write-host** comando restituisce **True**, hello è installato l'agente di macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="245d5-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="245d5-145">Se restituisce **False**, vedere le istruzioni di hello e toohello un collegamento Scarica nel post di blog di Azure hello [agente VM ed estensioni - parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="245d5-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="245d5-146">Se è installato l'agente VM hello, eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="245d5-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="245d5-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="245d5-147">Next steps</span></span>
<span data-ttu-id="245d5-148">Sono necessari alcuni minuti per toostart agente hello in esecuzione quando viene installato.</span><span class="sxs-lookup"><span data-stu-id="245d5-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="245d5-149">Successivamente, è necessario tooactivate Deep Security nella macchina virtuale hello in modo da poter essere gestito da un gestore protezione completa.</span><span class="sxs-lookup"><span data-stu-id="245d5-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="245d5-150">Vedere i seguenti articoli per le istruzioni aggiuntive hello:</span><span class="sxs-lookup"><span data-stu-id="245d5-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="245d5-151">Articolo di Trend Micro sulla [sicurezza cloud immediata per Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="245d5-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="245d5-152">Oggetto [script Windows PowerShell di esempio](http://go.microsoft.com/fwlink/?LinkId=404100) macchina virtuale di hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="245d5-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="245d5-153">[Istruzioni](http://go.microsoft.com/fwlink/?LinkId=404099) per esempio hello</span><span class="sxs-lookup"><span data-stu-id="245d5-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="245d5-154">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="245d5-154">Additional resources</span></span>
<span data-ttu-id="245d5-155">[Come toolog nella macchina virtuale tooa che esegue Windows Server]</span><span class="sxs-lookup"><span data-stu-id="245d5-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="245d5-156">[Estensioni VM e funzionalità di Azure]</span><span class="sxs-lookup"><span data-stu-id="245d5-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Come toolog nella macchina virtuale tooa che esegue Windows Server]:connect-logon.md
[Estensioni VM e funzionalità di Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
