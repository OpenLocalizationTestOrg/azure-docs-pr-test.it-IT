---
title: Informazioni sui dischi e sui dischi rigidi virtuali per le VM Windows di Microsoft Azure | Documentazione Microsoft
description: Informazioni di base sui dischi e sui dischi rigidi virtuali per le macchine virtuali in Azure.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: c194ca0f31d077ffa998764b9d63b12dd596ac32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="b0344-103">Informazioni sui dischi e sui dischi rigidi virtuali per le VM Windows di Azure</span><span class="sxs-lookup"><span data-stu-id="b0344-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="b0344-104">Analogamente a qualsiasi altro computer, le macchine virtuali in Azure utilizzano i dischi come posizioni per archiviare un sistema operativo, le applicazioni e i dati.</span><span class="sxs-lookup"><span data-stu-id="b0344-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="b0344-105">Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="b0344-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="b0344-106">Il disco del sistema operativo viene creato da un'immagine e sia il disco del sistema operativo sia l'immagine sono dischi rigidi virtuali archiviati in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0344-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="b0344-107">Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="b0344-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="b0344-108">Questo articolo illustra i diversi usi dei dischi e descrive i diversi tipi di dischi che è possibile creare e usare.</span><span class="sxs-lookup"><span data-stu-id="b0344-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="b0344-109">Questo articolo è disponibile anche per le [macchine virtuali Linux](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="b0344-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="b0344-110">Dischi usati dalle VM</span><span class="sxs-lookup"><span data-stu-id="b0344-110">Disks used by VMs</span></span>

<span data-ttu-id="b0344-111">Esaminiamo come i dischi vengono usati dalle VM.</span><span class="sxs-lookup"><span data-stu-id="b0344-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="b0344-112">Disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="b0344-112">Operating system disk</span></span>
<span data-ttu-id="b0344-113">Tutte le macchine virtuali dispongono di un disco del sistema operativo collegato.</span><span class="sxs-lookup"><span data-stu-id="b0344-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="b0344-114">Per impostazione predefinita, è registrato come unità SATA ed etichettato come unità C:.</span><span class="sxs-lookup"><span data-stu-id="b0344-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="b0344-115">Questo disco ha una capacità massima di 2048 GB.</span><span class="sxs-lookup"><span data-stu-id="b0344-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="b0344-116">Disco temporaneo</span><span class="sxs-lookup"><span data-stu-id="b0344-116">Temporary disk</span></span>
<span data-ttu-id="b0344-117">Ogni VM contiene un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="b0344-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="b0344-118">Il disco temporaneo offre archiviazione a breve termine per applicazioni e processi ed è destinato solo all'archiviazione di dati come file di paging o di scambio.</span><span class="sxs-lookup"><span data-stu-id="b0344-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="b0344-119">I dati presenti nel disco temporaneo potrebbero andare persi durante un [evento di manutenzione](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o la [ridistribuzione di una VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0344-119">Data on the temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b0344-120">Durante un riavvio standard della macchina virtuale, i dati nell'unità temporanea vengono mantenuti.</span><span class="sxs-lookup"><span data-stu-id="b0344-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="b0344-121">Per impostazione predefinita il disco temporaneo viene etichettato come unità D: e usato per l'archiviazione di pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="b0344-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="b0344-122">Per eseguire un nuovo mapping di questo disco su un'altra lettera di unità, vedere [Modifica della lettera di unità del disco temporaneo di Windows](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="b0344-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="b0344-123">Le dimensioni del disco temporaneo variano in base alle dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0344-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="b0344-124">Per maggiori informazioni, vedere [Dimensioni delle macchine virtuali di Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="b0344-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="b0344-125">Per altre informazioni sull'uso del disco temporaneo in Azure, vedere l'articolo relativo alle [unità temporanee nelle macchine virtuali di Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="b0344-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="b0344-126">Disco dati</span><span class="sxs-lookup"><span data-stu-id="b0344-126">Data disk</span></span>
<span data-ttu-id="b0344-127">Un disco dati è un disco rigido virtuale collegato a una macchina virtuale per archiviare i dati delle applicazioni o altri dati che è necessario conservare.</span><span class="sxs-lookup"><span data-stu-id="b0344-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="b0344-128">I dischi dati vengono registrati come unità SCSI ed etichettati con una lettera di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="b0344-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="b0344-129">Ogni disco dati ha una capacità massima di 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="b0344-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="b0344-130">Le dimensioni della macchina virtuale determinano il numero di dischi dati è possibile collegare e il tipo di archiviazione che è possibile utilizzare per ospitare i dischi.</span><span class="sxs-lookup"><span data-stu-id="b0344-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="b0344-131">Per altre informazioni sulle capacità delle macchine virtuali, vedere [Dimensioni delle macchine virtuali di Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="b0344-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="b0344-132">Quando viene creata una macchina virtuale da un'immagine, Azure crea un disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b0344-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="b0344-133">Se si utilizza un'immagine che include dischi dati, anche Azure crea dischi dati quando viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0344-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="b0344-134">In caso contrario, aggiungere dischi dati dopo aver creato la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0344-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="b0344-135">È possibile aggiungere dischi dati a una macchina virtuale in qualsiasi momento, **collegando** il disco alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0344-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="b0344-136">È possibile usare un disco rigido virtuale caricato o copiato nell'account di archiviazione o uno creato da Azure.</span><span class="sxs-lookup"><span data-stu-id="b0344-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="b0344-137">Il collegamento di un disco dati associa il file del disco rigido virtuale alla macchina virtuale, inserendo un "lease" nel disco rigido virtuale in modo che non possa essere eliminato dalla memoria se ancora collegato.</span><span class="sxs-lookup"><span data-stu-id="b0344-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="b0344-138">Un ultimo suggerimento: usare TRIM con i dischi standard non gestiti</span><span class="sxs-lookup"><span data-stu-id="b0344-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="b0344-139">Se si usano dischi standard non gestiti, è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="b0344-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="b0344-140">TRIM ignora i blocchi inutilizzati nel disco facendo in modo che venga addebitato solo lo spazio di archiviazione usato effettivamente.</span><span class="sxs-lookup"><span data-stu-id="b0344-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="b0344-141">In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="b0344-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="b0344-142">Per verificare l'impostazione TRIM, è possibile eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="b0344-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="b0344-143">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="b0344-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="b0344-144">Se il comando restituisce 0, l'impostazione TRIM è abilitata correttamente.</span><span class="sxs-lookup"><span data-stu-id="b0344-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="b0344-145">Se restituisce 1, eseguire questo comando per abilitare TRIM:</span><span class="sxs-lookup"><span data-stu-id="b0344-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="b0344-146">Nota: il supporto per Trim è disponibile con Windows Server 2012/Windows 8 e versioni successive. Vedere [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints) (La nuova API consente alle app di inviare hint TRIM e Unmap ai supporti di memorizzazione).</span><span class="sxs-lookup"><span data-stu-id="b0344-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="b0344-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0344-147">Next steps</span></span>
* <span data-ttu-id="b0344-148">[Collegare un disco](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) per aggiungere altro spazio di archiviazione per la VM.</span><span class="sxs-lookup"><span data-stu-id="b0344-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="b0344-149">[Modificare la lettera di unità del disco temporaneo di Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) in modo che l'applicazione possa usare l'unità D: per i dati.</span><span class="sxs-lookup"><span data-stu-id="b0344-149">[Change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

