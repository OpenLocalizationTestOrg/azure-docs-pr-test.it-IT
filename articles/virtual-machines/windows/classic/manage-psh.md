---
title: aaaManage le macchine virtuali tramite Azure PowerShell | Documenti Microsoft
description: "Informazioni sui comandi che è possibile utilizzare attività tooautomate nella gestione delle macchine virtuali."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="607b3-103">Gestire le macchine virtuali con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="607b3-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="607b3-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="607b3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="607b3-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="607b3-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="607b3-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="607b3-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="607b3-107">Per i comandi PowerShell utilizzando il modello di gestione risorse hello comuni, vedere [qui](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="607b3-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="607b3-108">Molte attività si toomanage ogni giorno le macchine virtuali possono essere automatizzate tramite i cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="607b3-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="607b3-109">In questo articolo fornisce comandi di esempio per attività più semplice e tooarticles di collegamenti che mostra i comandi di hello per attività più complesse.</span><span class="sxs-lookup"><span data-stu-id="607b3-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="607b3-110">Se non è ancora stato installato e configurato Azure PowerShell, è possibile ottenere le istruzioni nell'articolo hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="607b3-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="607b3-111">Come toouse hello comandi di esempio</span><span class="sxs-lookup"><span data-stu-id="607b3-111">How toouse hello example commands</span></span>
<span data-ttu-id="607b3-112">È necessario tooreplace parte del testo hello in hello comandi con il testo che è appropriato per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="607b3-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="607b3-113">Hello < e > simboli indicano il testo è necessario tooreplace.</span><span class="sxs-lookup"><span data-stu-id="607b3-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="607b3-114">Quando si sostituisce il testo hello, rimuovere i simboli di hello ma lasciare virgolette hello sul posto.</span><span class="sxs-lookup"><span data-stu-id="607b3-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="607b3-115">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607b3-115">Get a VM</span></span>
<span data-ttu-id="607b3-116">Si tratta di un'attività di base che si utilizzerà spesso.</span><span class="sxs-lookup"><span data-stu-id="607b3-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="607b3-117">Utilizzarlo tooget informazioni su una macchina virtuale, eseguire le attività in una macchina virtuale o ottenere output toostore in una variabile.</span><span class="sxs-lookup"><span data-stu-id="607b3-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="607b3-118">tooget informazioni hello macchina virtuale, eseguire questo comando, sostituendo tutti gli elementi di offerta di hello, che includono caratteri hello < e >:</span><span class="sxs-lookup"><span data-stu-id="607b3-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="607b3-119">hello toostore output in una variabile $vm, eseguire:</span><span class="sxs-lookup"><span data-stu-id="607b3-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="607b3-120">Accedere tooa VM basate su Windows</span><span class="sxs-lookup"><span data-stu-id="607b3-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="607b3-121">Eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="607b3-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="607b3-122">È possibile ottenere macchine virtuali hello e nome del servizio cloud dalla visualizzazione hello di hello **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="607b3-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="607b3-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unità e la cartella toostore hello download RDP file del percorso, ad esempio: c:\temp >" $localFile = $localPath + "\" $vmname +"RDP"Get-AzureRemoteDesktopFile - ServiceName $svcName-nome $vmName - LocalPath $localFile-avvio</span><span class="sxs-lookup"><span data-stu-id="607b3-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="607b3-124">Arrestare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607b3-124">Stop a VM</span></span>
<span data-ttu-id="607b3-125">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="607b3-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="607b3-126">Utilizzare questo hello tookeep parametro IP virtuale (VIP) del cloud hello del servizio nel caso in cui è hello ultima VM nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="607b3-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="607b3-127">Se si usa il parametro StayProvisioned hello, ancora verrà addebitato per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607b3-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="607b3-128">Avviare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607b3-128">Start a VM</span></span>
<span data-ttu-id="607b3-129">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="607b3-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="607b3-130">Collegamento di un disco dati</span><span class="sxs-lookup"><span data-stu-id="607b3-130">Attach a data disk</span></span>
<span data-ttu-id="607b3-131">Questa operazione richiede alcuni passaggi.</span><span class="sxs-lookup"><span data-stu-id="607b3-131">This task requires a few steps.</span></span> <span data-ttu-id="607b3-132">Innanzitutto, utilizzare hello * * * Add-AzureDataDisk * * * cmdlet tooadd hello toohello $vm oggetto disco.</span><span class="sxs-lookup"><span data-stu-id="607b3-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="607b3-133">Utilizzare quindi **Update-AzureVM** configurazione hello tooupdate di cmdlet di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607b3-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="607b3-134">È anche necessario toodecide se tooattach un nuovo disco o uno che contiene dati.</span><span class="sxs-lookup"><span data-stu-id="607b3-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="607b3-135">Per un nuovo disco, il comando di hello crea file con estensione vhd hello e lo collega.</span><span class="sxs-lookup"><span data-stu-id="607b3-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="607b3-136">tooattach un nuovo disco, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="607b3-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="607b3-137">tooattach un disco dati esistente, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="607b3-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="607b3-138">tooattach dischi di dati da un file con estensione vhd esistente nell'archiviazione blob, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="607b3-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="607b3-139">Creare una macchina virtuale basata su Windows</span><span class="sxs-lookup"><span data-stu-id="607b3-139">Create a Windows-based VM</span></span>
<span data-ttu-id="607b3-140">una nuova macchina virtuale basato su Windows in Azure, hello seguire le istruzioni riportate in toocreate [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="607b3-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="607b3-141">Questo argomento descrive i passaggi di creazione di hello di un set di comandi di Azure PowerShell crea una macchina virtuale basata su Windows che può essere preconfigurata:</span><span class="sxs-lookup"><span data-stu-id="607b3-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="607b3-142">Con l’appartenenza al dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="607b3-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="607b3-143">Con Dischi aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="607b3-143">With additional disks.</span></span>
* <span data-ttu-id="607b3-144">Come membro di un set esistente con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="607b3-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="607b3-145">Con un indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="607b3-145">With a static IP address.</span></span>

