---
title: Installare Symantec Endpoint Protection in una macchina virtuale Windows in Azure | Documentazione Microsoft
description: Informazioni su come installare e configurare l'estensione di sicurezza Symantec Endpoint Protection in una macchina virtuale di Azure nuova o esistente creata con il modello di distribuzione classica.
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
ms.openlocfilehash: 1603ebc7ee3c29277f30fbb802bdd8205b92d648
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="b45e6-103">Come installare e configurare Symantec Endpoint Protection in una macchina virtuale di Windows</span><span class="sxs-lookup"><span data-stu-id="b45e6-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b45e6-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b45e6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b45e6-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="b45e6-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b45e6-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="b45e6-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="b45e6-107">Questo articolo illustra come installare e configurare il client di Symantec Endpoint Protection in una macchina virtuale (VM) esistente in cui si esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b45e6-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="b45e6-108">Questo client completo include servizi come protezione da virus e spyware, firewall e prevenzione delle intrusioni.</span><span class="sxs-lookup"><span data-stu-id="b45e6-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="b45e6-109">Il client viene installato come estensione di sicurezza usando l'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b45e6-109">The client is installed as a security extension by using the VM Agent.</span></span>

<span data-ttu-id="b45e6-110">Se si dispone di una sottoscrizione Symantec per una soluzione locale, è possibile usarla per proteggere le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b45e6-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span></span> <span data-ttu-id="b45e6-111">Se non si è ancora clienti, è possibile iscriversi per una sottoscrizione di valutazione.</span><span class="sxs-lookup"><span data-stu-id="b45e6-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="b45e6-112">Per altre informazioni su questa soluzione, vedere la pagina relativa all'uso di [Symantec Endpoint Protection sulla piattaforma Microsoft Azure][Symantec].</span><span class="sxs-lookup"><span data-stu-id="b45e6-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="b45e6-113">Questa pagina include anche collegamenti a informazioni sulle licenze e a istruzioni per installare il client se si è già clienti Symantec.</span><span class="sxs-lookup"><span data-stu-id="b45e6-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="b45e6-114">Installare Symantec Endpoint Protection in una VM esistente</span><span class="sxs-lookup"><span data-stu-id="b45e6-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="b45e6-115">Prima di iniziare, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b45e6-115">Before you begin, you need the following:</span></span>

* <span data-ttu-id="b45e6-116">Il modulo Azure PowerShell 0.8.2 o versione successiva sul computer di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b45e6-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="b45e6-117">È possibile controllare la versione di Azure PowerShell installata con il comando **Get-Module azure | format-table version** .</span><span class="sxs-lookup"><span data-stu-id="b45e6-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="b45e6-118">Per istruzioni e un collegamento alla versione più recente, vedere [come installare e configurare Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="b45e6-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="b45e6-119">Effettuare l'accesso alla sottoscrizione di Azure usando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="b45e6-119">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="b45e6-120">L'agente di macchine virtuali in esecuzione sulla macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b45e6-120">The VM Agent running on the Azure Virtual Machine.</span></span>

<span data-ttu-id="b45e6-121">Verificare innanzitutto che l'agente di macchine virtuali sia già installato sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b45e6-121">First, verify that the VM Agent is already installed on the virtual machine.</span></span> <span data-ttu-id="b45e6-122">Specificare il nome del servizio cloud e il nome della macchina virtuale, quindi eseguire i comandi seguenti a un prompt dei comandi di Azure PowerShell di livello amministratore.</span><span class="sxs-lookup"><span data-stu-id="b45e6-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="b45e6-123">Sostituire tutti gli elementi all'interno delle virgolette, inclusi i caratteri < e >.</span><span class="sxs-lookup"><span data-stu-id="b45e6-123">Replace everything within the quotes, including the < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="b45e6-124">Se non si conosce il nome del servizio cloud e della macchina virtuale, eseguire **Get-AzureVM** per visualizzare l'elenco dei nomi di tutte le macchine virtuali nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="b45e6-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="b45e6-125">Se il comando **write-host** restituisce **True**, l'agente di macchine virtuali è installato.</span><span class="sxs-lookup"><span data-stu-id="b45e6-125">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="b45e6-126">Se restituisce **False**, nel post di blog di Azure relativo all'[agente di macchine virtuali ed estensioni, parte 2][Agent] sono disponibili istruzioni e un collegamento per il download.</span><span class="sxs-lookup"><span data-stu-id="b45e6-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="b45e6-127">Se l'agente di macchine virtuali è installato, eseguire questi comandi per installare l'agente Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="b45e6-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="b45e6-128">Per verificare che l'estensione di sicurezza Symantec sia stata installata e sia aggiornata:</span><span class="sxs-lookup"><span data-stu-id="b45e6-128">To verify that the Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="b45e6-129">Accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b45e6-129">Log on to the virtual machine.</span></span> <span data-ttu-id="b45e6-130">Per istruzioni, vedere [Come accedere a una macchina virtuale che esegue Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="b45e6-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="b45e6-131">Per Windows Server 2008 R2, fare clic su **Start > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="b45e6-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="b45e6-132">Per Windows Server 2012 o Windows Server 2012 R2, nella schermata Start digitare **Symantec**, quindi fare clic su **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="b45e6-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="b45e6-133">Nella scheda **Stato** della finestra **Stato - Symantec Endpoint Protection** applicare gli aggiornamenti o, se necessario, riavviare.</span><span class="sxs-lookup"><span data-stu-id="b45e6-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b45e6-134">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b45e6-134">Additional resources</span></span>
<span data-ttu-id="b45e6-135">[Come accedere a una macchina virtuale che esegue Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="b45e6-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="b45e6-136">[Estensioni e funzionalità delle macchine virtuali di Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="b45e6-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
