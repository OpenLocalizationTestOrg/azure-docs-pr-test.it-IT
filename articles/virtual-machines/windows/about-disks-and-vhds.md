---
title: aaaAbout dischi e i dischi rigidi virtuali per macchine virtuali di Windows di Microsoft Azure | Documenti Microsoft
description: Informazioni sui concetti di base di hello di dischi e i dischi rigidi virtuali per Windows macchine virtuali in Azure.
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
ms.openlocfilehash: 1b0d6bf05237bb3d1497b2c60f79a0159b730108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="87810-103">Informazioni sui dischi e sui dischi rigidi virtuali per le VM Windows di Azure</span><span class="sxs-lookup"><span data-stu-id="87810-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="87810-104">Analogamente a qualsiasi altro computer, le macchine virtuali in Azure usare dischi come un toostore sul posto del sistema operativo, applicazioni e dati.</span><span class="sxs-lookup"><span data-stu-id="87810-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="87810-105">Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="87810-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="87810-106">disco del sistema operativo Hello è creato da un'immagine disco del sistema operativo hello sia immagine hello sono dischi rigidi virtuali (VHD) archiviati in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="87810-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="87810-107">Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="87810-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="87810-108">In questo articolo, si parla hello diversi usi dischi hello e quindi illustrano hello diversi tipi di dischi è possibile creare e utilizzare.</span><span class="sxs-lookup"><span data-stu-id="87810-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="87810-109">Questo articolo è disponibile anche per le [macchine virtuali Linux](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="87810-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="87810-110">Dischi usati dalle VM</span><span class="sxs-lookup"><span data-stu-id="87810-110">Disks used by VMs</span></span>

<span data-ttu-id="87810-111">Esaminiamo un utilizzo dischi hello in hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="87810-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="87810-112">Disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="87810-112">Operating system disk</span></span>
<span data-ttu-id="87810-113">Tutte le macchine virtuali dispongono di un disco del sistema operativo collegato.</span><span class="sxs-lookup"><span data-stu-id="87810-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="87810-114">Ha registrato come unità SATA ed etichettato come unità c: hello per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="87810-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="87810-115">Questo disco ha una capacità massima di 2048 GB.</span><span class="sxs-lookup"><span data-stu-id="87810-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="87810-116">Disco temporaneo</span><span class="sxs-lookup"><span data-stu-id="87810-116">Temporary disk</span></span>
<span data-ttu-id="87810-117">Ogni VM contiene un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="87810-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="87810-118">disco temporaneo Hello fornisce l'archiviazione a breve termine per i processi e le applicazioni e dati di archivio tooonly desiderato, ad esempio i file di paging o di scambio.</span><span class="sxs-lookup"><span data-stu-id="87810-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="87810-119">Dati su disco temporaneo hello potrebbero andare persi durante un [evento di manutenzione](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o quando si [ridistribuire una macchina virtuale](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87810-119">Data on hello temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="87810-120">Durante un riavvio standard di hello VM, dati hello nell'unità temporanea hello devono essere rese persistenti.</span><span class="sxs-lookup"><span data-stu-id="87810-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="87810-121">disco temporaneo Hello viene etichettato come unità d: hello, per impostazione predefinita e viene utilizzato per l'archiviazione pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="87810-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="87810-122">tooremap questa lettera di unità diversa tooa disco, vedere [lettera di unità di modifica hello del disco temporaneo di Windows hello](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="87810-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="87810-123">dimensioni Hello del disco temporaneo hello variano in base alle dimensioni di hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="87810-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="87810-124">Per maggiori informazioni, vedere [Dimensioni delle macchine virtuali di Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="87810-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="87810-125">Per ulteriori informazioni sulle modalità di utilizzo disco temporaneo hello Azure, vedere [informazioni sulle unità temporanea hello in macchine virtuali di Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="87810-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="87810-126">Disco dati</span><span class="sxs-lookup"><span data-stu-id="87810-126">Data disk</span></span>
<span data-ttu-id="87810-127">Un disco dati è un disco rigido virtuale collegato tooa macchina virtuale toostore dati dell'applicazione o altri dati necessari tookeep.</span><span class="sxs-lookup"><span data-stu-id="87810-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="87810-128">I dischi dati vengono registrati come unità SCSI ed etichettati con una lettera di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="87810-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="87810-129">Ogni disco dati ha una capacità massima di 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="87810-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="87810-130">dimensione della macchina virtuale hello Hello determina il numero di dischi dati è possibile collegare tooit e hello il tipo di archiviazione è possibile usare dischi hello toohost.</span><span class="sxs-lookup"><span data-stu-id="87810-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="87810-131">Per altre informazioni sulle capacità delle macchine virtuali, vedere [Dimensioni delle macchine virtuali di Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="87810-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="87810-132">Quando viene creata una macchina virtuale da un'immagine, Azure crea un disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="87810-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="87810-133">Se si utilizza un'immagine che include dischi dati, Azure crea anche hello dischi dati durante la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="87810-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="87810-134">In caso contrario, aggiungere dischi dati dopo aver creato una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="87810-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="87810-135">È possibile aggiungere da macchina virtuale tooa dischi di dati in qualsiasi momento, **collegamento** hello macchina virtuale di toohello disco.</span><span class="sxs-lookup"><span data-stu-id="87810-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="87810-136">È possibile utilizzare un disco rigido virtuale che è stato caricato o copiato tooyour account di archiviazione o uno che Azure crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="87810-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="87810-137">Collegando un disco dati associa file di disco rigido virtuale hello hello VM inserendo un 'lease' sul disco rigido virtuale hello pertanto non può essere eliminato dall'archiviazione mentre è ancora collegato.</span><span class="sxs-lookup"><span data-stu-id="87810-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="87810-138">Un ultimo suggerimento: usare TRIM con i dischi standard non gestiti</span><span class="sxs-lookup"><span data-stu-id="87810-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="87810-139">Se si usano dischi standard non gestiti, è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="87810-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="87810-140">TRIM rimuove i blocchi inutilizzati nel disco hello in modo verrà addebitato solo per l'archiviazione che stiano effettivamente usando.</span><span class="sxs-lookup"><span data-stu-id="87810-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="87810-141">In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="87810-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="87810-142">È possibile eseguire questo comando toocheck hello TRIM impostare.</span><span class="sxs-lookup"><span data-stu-id="87810-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="87810-143">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="87810-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="87810-144">Se il comando hello restituisce 0, l'ottimizzazione TRIM è abilitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="87810-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="87810-145">Se viene restituito 1, eseguire hello tooenable comando TRIM seguenti:</span><span class="sxs-lookup"><span data-stu-id="87810-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="87810-146">Nota: Il supporto dell'ottimizzazione inizia con Windows Server 2012 o Windows 8 e versioni successive, vedere vedere [nuova API consente alle App media toostorage di hint "TRIM e annullare il mapping di" toosend](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="87810-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="87810-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87810-147">Next steps</span></span>
* <span data-ttu-id="87810-148">[Collegare un disco](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd ulteriore spazio di archiviazione per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="87810-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="87810-149">[Lettera di unità di modifica hello del disco temporaneo di Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) affinché l'applicazione può utilizzare l'unità d: hello per i dati.</span><span class="sxs-lookup"><span data-stu-id="87810-149">[Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

