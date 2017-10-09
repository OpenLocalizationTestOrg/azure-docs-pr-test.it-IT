---
title: Panoramica dell'agente di macchine virtuali aaaAzure | Documenti Microsoft
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
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="37fef-103">Panoramica dell'agente di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="37fef-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="37fef-104">Hello agente della macchina virtuale Microsoft Azure (agente AM) è un processo leggero protetto che gestisce l'interazione di VM con hello Controller di infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-104">hello Microsoft Azure Virtual Machine Agent (AM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="37fef-105">Hello agente VM svolge un ruolo primario di attivazione e l'esecuzione di estensioni di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="37fef-106">Le estensioni VM rendono possibile la configurazione post-distribuzione delle macchine virtuali, ad esempio l'installazione e configurazione di software.</span><span class="sxs-lookup"><span data-stu-id="37fef-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="37fef-107">Estensioni di macchine virtuali abilitano anche le funzionalità di ripristino, ad esempio la reimpostazione delle password amministrativa di hello di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="37fef-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="37fef-108">Senza hello agente VM di Azure, è Impossibile eseguire le estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="37fef-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="37fef-109">Questo documento illustra in dettaglio installazione, il rilevamento e rimozione di hello agente della macchina virtuale Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="37fef-110">Installare l'agente VM hello</span><span class="sxs-lookup"><span data-stu-id="37fef-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="37fef-111">Immagine della raccolta di Azure</span><span class="sxs-lookup"><span data-stu-id="37fef-111">Azure gallery image</span></span>

<span data-ttu-id="37fef-112">Hello agente VM di Azure viene installato per impostazione predefinita in qualsiasi macchina virtuale Windows distribuito da un'immagine della raccolta di Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="37fef-113">Quando si distribuisce un'immagine della raccolta di Azure dal portale hello, PowerShell, interfaccia della riga di comando o un modello di gestione risorse di Azure, installare hello che è anche l'agente VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="37fef-114">Installazione manuale</span><span class="sxs-lookup"><span data-stu-id="37fef-114">Manual installation</span></span>

<span data-ttu-id="37fef-115">agente di macchine Virtuali di Windows Hello può essere installato manualmente utilizzando il pacchetto Windows installer.</span><span class="sxs-lookup"><span data-stu-id="37fef-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="37fef-116">L'installazione manuale potrebbe essere necessaria quando si crea un'immagine di macchina virtuale personalizzata che verrà distribuita in Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="37fef-117">toomanually installazione hello agente VM di Windows, scaricare installazione guidata agente di macchine Virtuali di hello da questo percorso [scaricare l'agente di Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="37fef-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="37fef-118">Hello agente della macchina virtuale può essere installato facendo doppio clic sul file di programma di installazione di windows hello.</span><span class="sxs-lookup"><span data-stu-id="37fef-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="37fef-119">Per un'installazione automatica o automatica dell'agente di macchine Virtuali hello, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="37fef-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="37fef-120">Rilevare hello agente della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="37fef-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="37fef-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37fef-121">PowerShell</span></span>

<span data-ttu-id="37fef-122">modulo di gestione risorse di Azure PowerShell Hello può essere utilizzato tooretrieve informazioni sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="37fef-123">Esecuzione `Get-AzureRmVM` restituisce gran parte delle informazioni tra cui hello provisioning stato hello agente VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="37fef-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="37fef-124">di seguito Hello è solo un subset di hello `Get-AzureRmVM` output.</span><span class="sxs-lookup"><span data-stu-id="37fef-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="37fef-125">Hello preavviso `ProvisionVMAgent` annidata proprietà `OSProfile`, questa proprietà può essere utilizzato toodetermine se l'agente VM hello è stato macchina virtuale distribuita toohello.</span><span class="sxs-lookup"><span data-stu-id="37fef-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="37fef-126">Hello lo script seguente può essere utilizzato tooreturn un breve elenco di nomi di macchina virtuale e lo stato di hello di hello agente della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="37fef-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="37fef-127">Rilevamento manuale</span><span class="sxs-lookup"><span data-stu-id="37fef-127">Manual Detection</span></span>

<span data-ttu-id="37fef-128">Quando connesso tooa macchina virtuale Windows Azure, Gestione attività può essere utilizzato tooexamine processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="37fef-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="37fef-129">toocheck per hello agente VM di Azure, aprire Gestione attività > fare clic sulla scheda Dettagli hello e cercare un nome di processo `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="37fef-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="37fef-130">presenza di Hello di questo processo indica che l'agente VM hello è installato.</span><span class="sxs-lookup"><span data-stu-id="37fef-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="37fef-131">Aggiornare l'agente VM hello</span><span class="sxs-lookup"><span data-stu-id="37fef-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="37fef-132">Hello Azure VM agente per Windows viene aggiornato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="37fef-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="37fef-133">Nuove macchine virtuali sono distribuite tooAzure, ricevono più recenti dell'agente VM hello.</span><span class="sxs-lookup"><span data-stu-id="37fef-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="37fef-134">Immagini di macchina virtuale personalizzate devono essere aggiornato manualmente tooinclude hello nuovo VM agente.</span><span class="sxs-lookup"><span data-stu-id="37fef-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
