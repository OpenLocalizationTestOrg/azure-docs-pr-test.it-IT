---
title: Panoramica dell'agente di macchine virtuali di Azure | Documentazione Microsoft
description: Panoramica dell'agente di macchine virtuali di Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="23b74-103">Panoramica dell'agente di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="23b74-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="23b74-104">L'agente di macchine virtuali di Microsoft Azure è un processo protetto e leggero che gestisce l'interazione delle macchine virtuali con il controller di infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="23b74-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="23b74-105">L'agente di macchine virtuali svolge un ruolo primario per l'abilitazione e l'esecuzione delle estensioni macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="23b74-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="23b74-106">Le estensioni VM rendono possibile la configurazione post-distribuzione delle macchine virtuali, ad esempio l'installazione e configurazione di software.</span><span class="sxs-lookup"><span data-stu-id="23b74-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="23b74-107">Le estensioni macchina virtuale abilitano anche funzionalità di ripristino, ad esempio la reimpostazione della password amministrativa di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="23b74-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="23b74-108">Senza l'agente di macchine virtuali di Azure, le estensioni macchina virtuale non possono essere eseguite.</span><span class="sxs-lookup"><span data-stu-id="23b74-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="23b74-109">Questo documento descrive in dettaglio l'installazione, il rilevamento e la rimozione dell'agente di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="23b74-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="23b74-110">Installare l'agente di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="23b74-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="23b74-111">Immagine della raccolta di Azure</span><span class="sxs-lookup"><span data-stu-id="23b74-111">Azure gallery image</span></span>

<span data-ttu-id="23b74-112">L'agente di macchine virtuali di Azure viene installato per impostazione predefinita in qualsiasi macchina virtuale di Windows distribuita da un'immagine della raccolta di Azure.</span><span class="sxs-lookup"><span data-stu-id="23b74-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="23b74-113">Quando si distribuisce un'immagine della raccolta di Azure dal portale, da PowerShell, dall'interfaccia della riga di comando o con un modello di Azure Resource Manager, viene installato anche l'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="23b74-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="23b74-114">Installazione manuale</span><span class="sxs-lookup"><span data-stu-id="23b74-114">Manual installation</span></span>

<span data-ttu-id="23b74-115">L'agente di macchine virtuali di Windows può essere installato manualmente usando un pacchetto di Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="23b74-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="23b74-116">L'installazione manuale potrebbe essere necessaria quando si crea un'immagine di macchina virtuale personalizzata che verrà distribuita in Azure.</span><span class="sxs-lookup"><span data-stu-id="23b74-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="23b74-117">Per installare manualmente l'agente di macchine virtuali di Windows, scaricare il programma di installazione dell'agente di macchine virtuali da questo percorso: [Download dell'agente di macchine virtuali di Windows Azure](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="23b74-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="23b74-118">L'agente di macchine virtuali può essere installato facendo doppio clic sul file di Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="23b74-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="23b74-119">Per eseguire un'installazione automatica dell'agente di macchine virtuali, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="23b74-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="23b74-120">Rilevare l'agente di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="23b74-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="23b74-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="23b74-121">PowerShell</span></span>

<span data-ttu-id="23b74-122">Il modulo PowerShell di Azure Resource Manager può essere usato per recuperare informazioni sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="23b74-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="23b74-123">Con l'esecuzione di `Get-AzureRmVM` vengono restituite varie informazioni, incluso lo stato di provisioning per l'agente di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="23b74-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="23b74-124">Quello che segue è solo un subset dell'output di `Get-AzureRmVM`.</span><span class="sxs-lookup"><span data-stu-id="23b74-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="23b74-125">Notare la proprietà `ProvisionVMAgent` annidata all'interno di `OSProfile`. Questa proprietà può essere usata per determinare se l'agente di macchine virtuali è stato distribuito nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="23b74-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="23b74-126">È possibile usare lo script seguente per restituire un breve elenco di nomi di macchine virtuali e lo stato dell'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="23b74-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="23b74-127">Rilevamento manuale</span><span class="sxs-lookup"><span data-stu-id="23b74-127">Manual Detection</span></span>

<span data-ttu-id="23b74-128">Quando è connesso a una VM di Windows Azure, è possibile usare Gestione attività per esaminare i processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="23b74-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="23b74-129">Per controllare il processo dell'agente di macchine virtuali di Azure, aprire Gestione attività > fare clic sulla scheda Dettagli e cercare il nome di processo `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="23b74-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="23b74-130">La presenza di questo processo indica che l'agente di macchine virtuali è installato.</span><span class="sxs-lookup"><span data-stu-id="23b74-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="23b74-131">Aggiornare l'agente di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="23b74-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="23b74-132">L'agente di macchine virtuali di Azure per Windows viene aggiornato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="23b74-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="23b74-133">Le nuove macchine virtuali distribuite in Azure ricevono la versione più recente dell'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="23b74-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="23b74-134">Immagini di VM personalizzate devono essere aggiornate manualmente per includere il nuovo agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="23b74-134">Custom VM images should be manually updated to include the new VM agent.</span></span>