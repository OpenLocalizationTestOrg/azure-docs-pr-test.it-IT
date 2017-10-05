---
title: Gestire le macchine virtuali tramite Azure PowerShell | Microsoft Docs
description: "Informazioni su comandi che è possibile utilizzare per automatizzare le attività di gestione delle macchine virtuali."
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
ms.openlocfilehash: fd2df7e1029ced11974d0b832258bed2cf3bbb27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="4aa4c-103">Gestire le macchine virtuali con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4aa4c-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4aa4c-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4aa4c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4aa4c-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4aa4c-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4aa4c-107">Per i comandi comuni di PowerShell con il modello di Resource Manager, vedere [qui](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4aa4c-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4aa4c-108">Molte attività che è possibile eseguire ogni giorno per gestire le macchine virtuali possono essere automatizzate utilizzando i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4aa4c-109">In questo articolo offre esempi di comandi per le attività più semplici e collegamenti ad articoli in cui visualizzare i comandi per attività più complesse.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="4aa4c-110">Se non è ancora stato installato e configurato Azure PowerShell, è possibile ottenere le istruzioni nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4aa4c-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-to-use-the-example-commands"></a><span data-ttu-id="4aa4c-111">Come utilizzare i comandi di esempio</span><span class="sxs-lookup"><span data-stu-id="4aa4c-111">How to use the example commands</span></span>
<span data-ttu-id="4aa4c-112">È necessario sostituire una parte del testo nei comandi con il testo appropriato per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="4aa4c-113">I simboli < e > indicano il testo da sostituire.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-113">The < and > symbols indicate text you need to replace.</span></span> <span data-ttu-id="4aa4c-114">Quando si sostituisce il testo, rimuovere i simboli ma mantenere le virgolette.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-114">When you replace the text, remove the symbols but leave the quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="4aa4c-115">Ottenere una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4aa4c-115">Get a VM</span></span>
<span data-ttu-id="4aa4c-116">Si tratta di un'attività di base che si utilizzerà spesso.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="4aa4c-117">È possibile utilizzarla per ottenere informazioni su una macchina virtuale, eseguire le attività in una macchina virtuale o recuperare l'output da archiviare in una variabile.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span></span>

<span data-ttu-id="4aa4c-118">Per ottenere informazioni sulla macchina virtuale, eseguire questo comando sostituendo tutto ciò che è racchiuso tra virgolette, inclusi i caratteri < e >:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="4aa4c-119">Per archiviare l'output in una variabile $vm, eseguire:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-119">To store the output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a><span data-ttu-id="4aa4c-120">Accedere a una macchina virtuale basata su Windows</span><span class="sxs-lookup"><span data-stu-id="4aa4c-120">Log on to a Windows-based VM</span></span>
<span data-ttu-id="4aa4c-121">Eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="4aa4c-122">È possibile ottenere il nome del servizio delle macchine virtuali e cloud dalla visualizzazione della **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="4aa4c-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<posizione dell'unità e della cartella in cui archiviare il file con estensione RDP scaricato, ad esempio: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span><span class="sxs-lookup"><span data-stu-id="4aa4c-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="4aa4c-124">Arrestare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4aa4c-124">Stop a VM</span></span>
<span data-ttu-id="4aa4c-125">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="4aa4c-126">Utilizzare questo parametro per mantenere l'IP virtuale (VIP) del servizio cloud, qualora fosse l'ultima macchina virtuale inclusa nel servizio cloud specifico.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="4aa4c-127">Se si utilizza il parametro StayProvisioned, sarà ancora configurato per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="4aa4c-128">Avviare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4aa4c-128">Start a VM</span></span>
<span data-ttu-id="4aa4c-129">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="4aa4c-130">Collegamento di un disco dati</span><span class="sxs-lookup"><span data-stu-id="4aa4c-130">Attach a data disk</span></span>
<span data-ttu-id="4aa4c-131">Questa operazione richiede alcuni passaggi.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-131">This task requires a few steps.</span></span> <span data-ttu-id="4aa4c-132">Utilizzare innanzitutto la cmdlet****Aggiungi-DiscoDatiAzure**** per aggiungere il disco per l'oggetto $vm.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-132">First, you use the ****Add-AzureDataDisk**** cmdlet to add the disk to the $vm object.</span></span> <span data-ttu-id="4aa4c-133">Quindi è possibile utilizzare il cmdlet **Aggiorna-MacchinaVirtualeAzure** per aggiornare la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span></span>

<span data-ttu-id="4aa4c-134">È inoltre necessario decidere se collegare un nuovo disco o uno che contiene già dati.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-134">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="4aa4c-135">Per un nuovo disco, il comando permette di creare il file con estensione VHD e contemporaneamente di collegarlo.</span><span class="sxs-lookup"><span data-stu-id="4aa4c-135">For a new disk, the command creates the .vhd file and attaches it.</span></span>

<span data-ttu-id="4aa4c-136">Per collegare un nuovo disco, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-136">To attach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="4aa4c-137">Per collegare un disco dati esistente, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-137">To attach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="4aa4c-138">Per collegare dischi dati da un file con estensione vhd esistente nell'archiviazione blob, è necessario eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="4aa4c-139">Creare una macchina virtuale basata su Windows</span><span class="sxs-lookup"><span data-stu-id="4aa4c-139">Create a Windows-based VM</span></span>
<span data-ttu-id="4aa4c-140">Per creare una nuova macchina virtuale basata su Windows in Azure, usare le istruzioni nell'argomento relativo all'[uso di Azure PowerShell per creare e preconfigurare le macchine virtuali basate su Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4aa4c-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="4aa4c-141">Questo argomento illustra la creazione di un set di comandi di PowerShell che consente di creare una macchina virtuale di Windows che può essere preconfigurata con:</span><span class="sxs-lookup"><span data-stu-id="4aa4c-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="4aa4c-142">Con l’appartenenza al dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="4aa4c-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="4aa4c-143">Con Dischi aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="4aa4c-143">With additional disks.</span></span>
* <span data-ttu-id="4aa4c-144">Come membro di un set esistente con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="4aa4c-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="4aa4c-145">Con un indirizzo IP statico</span><span class="sxs-lookup"><span data-stu-id="4aa4c-145">With a static IP address.</span></span>

