---
title: Symantec Endpoint Protection in una macchina virtuale Windows in Azure aaaInstall | Documenti Microsoft
description: Informazioni su come tooinstall e configurare l'estensione di sicurezza di hello Symantec Endpoint Protection in un nuovo o esistente macchina virtuale di Azure creata con modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="b38e6-103">Come tooinstall e configurare Symantec Endpoint Protection in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="b38e6-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b38e6-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b38e6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b38e6-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="b38e6-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b38e6-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="b38e6-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="b38e6-107">In questo articolo illustra come tooinstall e configurare i client di hello Symantec Endpoint Protection in una macchina virtuale esistente (VM) che esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b38e6-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="b38e6-108">Questo client completo include servizi come protezione da virus e spyware, firewall e prevenzione delle intrusioni.</span><span class="sxs-lookup"><span data-stu-id="b38e6-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="b38e6-109">client Hello viene installato come un'estensione di sicurezza utilizzando hello agente della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b38e6-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="b38e6-110">Se si dispone di una sottoscrizione esistente da Symantec per una soluzione locale, è possibile usarlo tooprotect macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b38e6-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="b38e6-111">Se non si è ancora clienti, è possibile iscriversi per una sottoscrizione di valutazione.</span><span class="sxs-lookup"><span data-stu-id="b38e6-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="b38e6-112">Per altre informazioni su questa soluzione, vedere la pagina relativa all'uso di [Symantec Endpoint Protection sulla piattaforma Microsoft Azure][Symantec].</span><span class="sxs-lookup"><span data-stu-id="b38e6-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="b38e6-113">Questa pagina include anche collegamenti toolicensing informazioni e istruzioni per l'installazione client hello se si è già un cliente di Symantec.</span><span class="sxs-lookup"><span data-stu-id="b38e6-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="b38e6-114">Installare Symantec Endpoint Protection in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="b38e6-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="b38e6-115">Prima di iniziare, è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="b38e6-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="b38e6-116">modulo di Azure PowerShell Hello, versione 0.8.2 o versione successiva, nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b38e6-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="b38e6-117">È possibile controllare la versione hello di Azure PowerShell che è stato installato con hello **Get-Module azure | versione formato tabella** comando.</span><span class="sxs-lookup"><span data-stu-id="b38e6-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="b38e6-118">Per istruzioni e una versione più recente toohello di collegamento, vedere [come tooInstall e configurare Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="b38e6-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="b38e6-119">Accedi con sottoscrizione di Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="b38e6-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="b38e6-120">Hello hello di agente di macchine Virtuali in esecuzione in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b38e6-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="b38e6-121">Verificare innanzitutto che hello che agente VM è già installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b38e6-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="b38e6-122">Specificare nome del servizio cloud hello e nome della macchina virtuale e quindi eseguire hello seguenti comandi in un prompt dei comandi di Azure PowerShell a livello di amministratore.</span><span class="sxs-lookup"><span data-stu-id="b38e6-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="b38e6-123">Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri.</span><span class="sxs-lookup"><span data-stu-id="b38e6-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="b38e6-124">Se non si conosce il servizio di cloud hello e nomi di macchina virtuale, eseguire **Get-AzureVM** nomi hello toolist per tutte le macchine virtuali nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="b38e6-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="b38e6-125">Se hello **write-host** comando Visualizza **True**, hello è installato l'agente di macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="b38e6-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="b38e6-126">Se viene visualizzato **False**, vedere le istruzioni di hello e toohello un collegamento Scarica nel post di blog di Azure hello [agente VM ed estensioni - parte 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="b38e6-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="b38e6-127">Se è installato l'agente VM hello, eseguire agente di Symantec Endpoint Protection questi comandi tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="b38e6-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="b38e6-128">tooverify che hello Symantec estensione di sicurezza è stato installato e aggiornato:</span><span class="sxs-lookup"><span data-stu-id="b38e6-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="b38e6-129">Accedere a macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="b38e6-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="b38e6-130">Per istruzioni, vedere [come tooLog nella macchina virtuale che esegue Windows Server tooa][Logon].</span><span class="sxs-lookup"><span data-stu-id="b38e6-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="b38e6-131">Per Windows Server 2008 R2, fare clic su **Start > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="b38e6-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="b38e6-132">Per Windows Server 2012 o Windows Server 2012 R2, dalla schermata start hello, digitare **Symantec**, quindi fare clic su **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="b38e6-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="b38e6-133">Da hello **stato** scheda di hello **stato Symantec Endpoint Protection** finestra, applicare gli aggiornamenti o riavviare se necessario.</span><span class="sxs-lookup"><span data-stu-id="b38e6-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b38e6-134">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b38e6-134">Additional resources</span></span>
<span data-ttu-id="b38e6-135">[Come tooLog su tooa macchina virtuale che esegue Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="b38e6-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="b38e6-136">[Estensioni e funzionalità delle macchine virtuali di Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="b38e6-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
