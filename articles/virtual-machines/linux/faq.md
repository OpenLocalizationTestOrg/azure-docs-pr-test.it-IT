---
title: Domande frequenti sulle macchine virtuali Linux in Azure | Microsoft Docs
description: Fornisce le risposte ad alcune delle domande comuni sulle macchine virtuali Linux create con un modello di Resource Manager.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0e06d21bd0b6ef807f38e41dcd50c9cd715607a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="49595-103">Domande frequenti sulle macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="49595-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="49595-104">Questo articolo analizza alcune delle domande più comuni sulle macchine virtuali Linux create in Azure mediante il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49595-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="49595-105">Per la versione di Windows di questo argomento, vedere [Domande frequenti sulle macchine virtuali Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="49595-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="49595-106">Cosa è possibile eseguire in una VM di Azure?</span><span class="sxs-lookup"><span data-stu-id="49595-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="49595-107">Tutti i sottoscrittori possono eseguire software del server in una macchina virtuale Azure.</span><span class="sxs-lookup"><span data-stu-id="49595-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="49595-108">Per altre informazioni, vedere [Distribuzioni di Linux supportate da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="49595-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="49595-109">Quanta memoria è possibile utilizzare con una macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="49595-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="49595-110">Ogni disco dati può essere fino a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="49595-110">Each data disk can be up to 1 TB.</span></span> <span data-ttu-id="49595-111">Il numero di dischi dati che è possibile utilizzare dipende dalla dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="49595-111">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="49595-112">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49595-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="49595-113">Un account di archiviazione Azure fornisce memoria per il disco del sistema operativo e per qualsiasi disco dati.</span><span class="sxs-lookup"><span data-stu-id="49595-113">An Azure storage account provides storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="49595-114">Ogni disco è un file con estensione vhd archiviato come BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="49595-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="49595-115">Per informazioni sui prezzi, vedere [Dettagli prezzi di archiviazione](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="49595-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="49595-116">Come si accede alla macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="49595-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="49595-117">Stabilire una connessione remota per accedere alla macchina virtuale tramite Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="49595-117">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="49595-118">Vedere le istruzioni su come connettersi [da Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [da Linux e Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49595-118">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="49595-119">Per impostazione predefinita, la SSH consente un massimo di 10 connessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="49595-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="49595-120">È possibile aumentare questo numero modificando il file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="49595-120">You can increase this number by editing the configuration file.</span></span>

<span data-ttu-id="49595-121">Se si verificano problemi, vedere l'argomento [Risolvere i problemi relativi alle connessioni Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49595-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-the-temporary-disk-devsdb1-to-store-data"></a><span data-ttu-id="49595-122">È possibile usare il disco temporaneo (/dev/sdb1) per archiviare i dati?</span><span class="sxs-lookup"><span data-stu-id="49595-122">Can I use the temporary disk (/dev/sdb1) to store data?</span></span>
<span data-ttu-id="49595-123">Non usare il disco temporaneo (/dev/sdb1) per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="49595-123">Don't use the temporary disk (/dev/sdb1) to store data.</span></span> <span data-ttu-id="49595-124">Serve solo per l'archiviazione temporanea.</span><span class="sxs-lookup"><span data-stu-id="49595-124">It is only there for temporary storage.</span></span> <span data-ttu-id="49595-125">I dati non ripristinabili rischiano di andare persi.</span><span class="sxs-lookup"><span data-stu-id="49595-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="49595-126">È possibile copiare o clonare una VM di Azure esistente?</span><span class="sxs-lookup"><span data-stu-id="49595-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="49595-127">Sì.</span><span class="sxs-lookup"><span data-stu-id="49595-127">Yes.</span></span> <span data-ttu-id="49595-128">Per le istruzioni, vedere [Creare una copia di una macchina virtuale Linux nel modello di distribuzione di Resource Manager](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49595-128">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="49595-129">Perché non si vedono le aree del Canada centrale e del Canada orientale tramite Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="49595-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="49595-130">Le due nuove aree del Canada centrale e del Canada orientale non vengono registrate automaticamente per la creazione della macchina virtuale per le sottoscrizioni di Azure esistenti.</span><span class="sxs-lookup"><span data-stu-id="49595-130">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="49595-131">La registrazione viene eseguita automaticamente quando si distribuisce una macchina virtuale tramite il portale di Azure in qualsiasi altra area di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49595-131">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="49595-132">Dopo aver distribuito una macchina virtuale in qualsiasi altra area di Azure le nuove aree dovrebbero essere disponibili per le macchine virtuali successive.</span><span class="sxs-lookup"><span data-stu-id="49595-132">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="49595-133">È possibile aggiungere un NIC alla VM dopo la sua creazione?</span><span class="sxs-lookup"><span data-stu-id="49595-133">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="49595-134">Sì, ora è possibile.</span><span class="sxs-lookup"><span data-stu-id="49595-134">Yes, this is now possible.</span></span> <span data-ttu-id="49595-135">La macchina virtuale deve prima essere arrestata e deallocata.</span><span class="sxs-lookup"><span data-stu-id="49595-135">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="49595-136">È possibile a questo punto aggiungere o rimuovere una scheda di interfaccia di rete (a meno che non sia l'ultima nella macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="49595-136">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="49595-137">Esistono requisiti relativi al nome del computer?</span><span class="sxs-lookup"><span data-stu-id="49595-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="49595-138">Sì.</span><span class="sxs-lookup"><span data-stu-id="49595-138">Yes.</span></span> <span data-ttu-id="49595-139">Il nome del computer non può contenere più di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="49595-139">The computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="49595-140">Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sulla denominazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="49595-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="49595-141">Vi sono requisiti relativi al nome del gruppo di risorse?</span><span class="sxs-lookup"><span data-stu-id="49595-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="49595-142">Sì.</span><span class="sxs-lookup"><span data-stu-id="49595-142">Yes.</span></span> <span data-ttu-id="49595-143">Il nome del gruppo di risorse non può contenere più di 90 caratteri.</span><span class="sxs-lookup"><span data-stu-id="49595-143">The resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="49595-144">Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sui gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="49595-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="49595-145">Quali requisiti devono avere i nomi utente durante la creazione di una VM?</span><span class="sxs-lookup"><span data-stu-id="49595-145">What are the username requirements when creating a VM?</span></span>
<span data-ttu-id="49595-146">I nomi utente devono contenere da 1 a 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="49595-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="49595-147">I nomi utente seguenti non sono consentiti:</span><span class="sxs-lookup"><span data-stu-id="49595-147">The following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-148">administrator</span><span class="sxs-lookup"><span data-stu-id="49595-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-149">admin</span><span class="sxs-lookup"><span data-stu-id="49595-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-150">user</span><span class="sxs-lookup"><span data-stu-id="49595-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-151">user1</span><span class="sxs-lookup"><span data-stu-id="49595-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-152">test</span><span class="sxs-lookup"><span data-stu-id="49595-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-153">user2</span><span class="sxs-lookup"><span data-stu-id="49595-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-154">test1</span><span class="sxs-lookup"><span data-stu-id="49595-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-155">user3</span><span class="sxs-lookup"><span data-stu-id="49595-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-156">admin1</span><span class="sxs-lookup"><span data-stu-id="49595-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-157">1</span><span class="sxs-lookup"><span data-stu-id="49595-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-158">123</span><span class="sxs-lookup"><span data-stu-id="49595-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-159">a</span><span class="sxs-lookup"><span data-stu-id="49595-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-160">actuser</span><span class="sxs-lookup"><span data-stu-id="49595-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="49595-161">adm</span><span class="sxs-lookup"><span data-stu-id="49595-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-162">admin2</span><span class="sxs-lookup"><span data-stu-id="49595-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="49595-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-164">backup</span><span class="sxs-lookup"><span data-stu-id="49595-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-165">console</span><span class="sxs-lookup"><span data-stu-id="49595-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-166">david</span><span class="sxs-lookup"><span data-stu-id="49595-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-167">guest</span><span class="sxs-lookup"><span data-stu-id="49595-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-168">john</span><span class="sxs-lookup"><span data-stu-id="49595-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-169">proprietario</span><span class="sxs-lookup"><span data-stu-id="49595-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-170">root</span><span class="sxs-lookup"><span data-stu-id="49595-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-171">server</span><span class="sxs-lookup"><span data-stu-id="49595-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-172">sql</span><span class="sxs-lookup"><span data-stu-id="49595-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-173">support</span><span class="sxs-lookup"><span data-stu-id="49595-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="49595-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-175">sys</span><span class="sxs-lookup"><span data-stu-id="49595-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="49595-176">test2</span><span class="sxs-lookup"><span data-stu-id="49595-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-177">test3</span><span class="sxs-lookup"><span data-stu-id="49595-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-178">user4</span><span class="sxs-lookup"><span data-stu-id="49595-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="49595-179">user5</span><span class="sxs-lookup"><span data-stu-id="49595-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="49595-180">Quali requisiti devono avere le password durante la creazione di una VM?</span><span class="sxs-lookup"><span data-stu-id="49595-180">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="49595-181">Le password devono contenere da 6 a 72 caratteri e soddisfare 3 dei seguenti 4 requisiti di complessità:</span><span class="sxs-lookup"><span data-stu-id="49595-181">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="49595-182">Devono contenere caratteri minuscoli</span><span class="sxs-lookup"><span data-stu-id="49595-182">Have lower characters</span></span>
* <span data-ttu-id="49595-183">Devono contenere caratteri maiuscoli</span><span class="sxs-lookup"><span data-stu-id="49595-183">Have upper characters</span></span>
* <span data-ttu-id="49595-184">Devono contenere almeno un numero</span><span class="sxs-lookup"><span data-stu-id="49595-184">Have a digit</span></span>
* <span data-ttu-id="49595-185">Devono contenere un carattere speciale (REGEX.CONFRONTA [\W_])</span><span class="sxs-lookup"><span data-stu-id="49595-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="49595-186">Le password seguenti non sono consentite:</span><span class="sxs-lookup"><span data-stu-id="49595-186">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="49595-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="49595-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="49595-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="49595-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="49595-189">Password!</span><span class="sxs-lookup"><span data-stu-id="49595-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="49595-190">Password1</span><span class="sxs-lookup"><span data-stu-id="49595-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="49595-191">Password22</span><span class="sxs-lookup"><span data-stu-id="49595-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="49595-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="49595-192">iloveyou!</span></span></td>
    </tr>
</table>
