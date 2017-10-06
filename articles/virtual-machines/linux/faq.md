---
title: domande frequenti per le macchine virtuali Linux in Azure aaaFrequently | Documenti Microsoft
description: Fornisce le risposte toosome di domande frequenti di hello relative macchine virtuali Linux create con il modello di gestione risorse hello.
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
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="942ca-103">Domande frequenti sulle macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="942ca-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="942ca-104">Questo articolo illustra alcune domande frequenti sulle macchine virtuali Linux create in Azure tramite il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="942ca-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="942ca-105">La versione di Windows hello di questo argomento, vedere [domande frequenti sulle macchine virtuali di Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="942ca-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="942ca-106">Cosa è possibile eseguire in una VM di Azure?</span><span class="sxs-lookup"><span data-stu-id="942ca-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="942ca-107">Tutti i sottoscrittori possono eseguire software del server in una macchina virtuale Azure.</span><span class="sxs-lookup"><span data-stu-id="942ca-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="942ca-108">Per altre informazioni, vedere [Distribuzioni di Linux supportate da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="942ca-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="942ca-109">Quanta memoria è possibile utilizzare con una macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="942ca-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="942ca-110">Ogni disco dati può essere backup too1 TB.</span><span class="sxs-lookup"><span data-stu-id="942ca-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="942ca-111">numero di Hello di dischi di dati che è possibile utilizzare dipende dalle dimensioni hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="942ca-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="942ca-112">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="942ca-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="942ca-113">Un account di archiviazione di Azure fornisce archiviazione per disco del sistema operativo hello e per eventuali dischi dati.</span><span class="sxs-lookup"><span data-stu-id="942ca-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="942ca-114">Ogni disco è un file con estensione vhd archiviato come BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="942ca-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="942ca-115">Per informazioni sui prezzi, vedere [Dettagli prezzi di archiviazione](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="942ca-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="942ca-116">Come si accede alla macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="942ca-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="942ca-117">Stabilire una connessione remota di toolog nella macchina virtuale toohello tramite Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="942ca-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="942ca-118">Vedere le istruzioni di hello sul tooconnect [da Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [da Linux e Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="942ca-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="942ca-119">Per impostazione predefinita, la SSH consente un massimo di 10 connessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="942ca-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="942ca-120">È possibile aumentare questo numero modificando il file di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="942ca-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="942ca-121">Se si verificano problemi, vedere l'argomento [Risolvere i problemi relativi alle connessioni Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="942ca-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="942ca-122">È possibile utilizzare i dati di toostore hello disco temporaneo (dev/sdb1)?</span><span class="sxs-lookup"><span data-stu-id="942ca-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="942ca-123">Non utilizzare dati di toostore hello disco temporaneo (dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="942ca-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="942ca-124">Serve solo per l'archiviazione temporanea.</span><span class="sxs-lookup"><span data-stu-id="942ca-124">It is only there for temporary storage.</span></span> <span data-ttu-id="942ca-125">I dati non ripristinabili rischiano di andare persi.</span><span class="sxs-lookup"><span data-stu-id="942ca-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="942ca-126">È possibile copiare o clonare una VM di Azure esistente?</span><span class="sxs-lookup"><span data-stu-id="942ca-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="942ca-127">Sì.</span><span class="sxs-lookup"><span data-stu-id="942ca-127">Yes.</span></span> <span data-ttu-id="942ca-128">Per istruzioni, vedere [come toocreate una copia di una macchina virtuale di Linux in hello il modello di distribuzione di gestione risorse](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="942ca-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="942ca-129">Perché non si vedono le aree del Canada centrale e del Canada orientale tramite Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="942ca-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="942ca-130">Hello due nuove aree di centrale Canada e Canada orientale non vengono registrate automaticamente per la creazione della macchina virtuale per le sottoscrizioni di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="942ca-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="942ca-131">Questa registrazione viene eseguita automaticamente quando una macchina virtuale viene distribuita tramite hello tooany portale Azure altre aree di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="942ca-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="942ca-132">Dopo una macchina virtuale è distribuita tooany altre aree di Azure, nuove aree hello devono essere disponibili per le macchine virtuali successive.</span><span class="sxs-lookup"><span data-stu-id="942ca-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="942ca-133">È possibile aggiungere un toomy NIC VM dopo averla creata?</span><span class="sxs-lookup"><span data-stu-id="942ca-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="942ca-134">Sì, ora è possibile.</span><span class="sxs-lookup"><span data-stu-id="942ca-134">Yes, this is now possible.</span></span> <span data-ttu-id="942ca-135">Hello VM prima esigenze toobe arrestate deallocate.</span><span class="sxs-lookup"><span data-stu-id="942ca-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="942ca-136">È possibile aggiungere o rimuovere una scheda di rete (a meno che non è hello ultimo NIC hello VM).</span><span class="sxs-lookup"><span data-stu-id="942ca-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="942ca-137">Esistono requisiti relativi al nome del computer?</span><span class="sxs-lookup"><span data-stu-id="942ca-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="942ca-138">Sì.</span><span class="sxs-lookup"><span data-stu-id="942ca-138">Yes.</span></span> <span data-ttu-id="942ca-139">nome del computer Hello può contenere un massimo di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="942ca-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="942ca-140">Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sulla denominazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="942ca-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="942ca-141">Vi sono requisiti relativi al nome del gruppo di risorse?</span><span class="sxs-lookup"><span data-stu-id="942ca-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="942ca-142">Sì.</span><span class="sxs-lookup"><span data-stu-id="942ca-142">Yes.</span></span> <span data-ttu-id="942ca-143">nome del gruppo di risorse Hello può contenere un massimo di 90 caratteri.</span><span class="sxs-lookup"><span data-stu-id="942ca-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="942ca-144">Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sui gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="942ca-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="942ca-145">Quali sono i requisiti di nome utente hello durante la creazione di una macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="942ca-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="942ca-146">I nomi utente devono contenere da 1 a 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="942ca-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="942ca-147">non è consentita Hello nomi utente di seguenti:</span><span class="sxs-lookup"><span data-stu-id="942ca-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-148">entità</span><span class="sxs-lookup"><span data-stu-id="942ca-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-149">admin</span><span class="sxs-lookup"><span data-stu-id="942ca-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-150">user</span><span class="sxs-lookup"><span data-stu-id="942ca-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-151">user1</span><span class="sxs-lookup"><span data-stu-id="942ca-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-152">test</span><span class="sxs-lookup"><span data-stu-id="942ca-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-153">user2</span><span class="sxs-lookup"><span data-stu-id="942ca-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-154">test1</span><span class="sxs-lookup"><span data-stu-id="942ca-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-155">user3</span><span class="sxs-lookup"><span data-stu-id="942ca-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-156">admin1</span><span class="sxs-lookup"><span data-stu-id="942ca-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-157">1</span><span class="sxs-lookup"><span data-stu-id="942ca-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-158">123</span><span class="sxs-lookup"><span data-stu-id="942ca-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-159">a</span><span class="sxs-lookup"><span data-stu-id="942ca-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-160">actuser</span><span class="sxs-lookup"><span data-stu-id="942ca-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="942ca-161">adm</span><span class="sxs-lookup"><span data-stu-id="942ca-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-162">admin2</span><span class="sxs-lookup"><span data-stu-id="942ca-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="942ca-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-164">backup</span><span class="sxs-lookup"><span data-stu-id="942ca-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-165">console</span><span class="sxs-lookup"><span data-stu-id="942ca-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-166">david</span><span class="sxs-lookup"><span data-stu-id="942ca-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-167">guest</span><span class="sxs-lookup"><span data-stu-id="942ca-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-168">john</span><span class="sxs-lookup"><span data-stu-id="942ca-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-169">proprietario</span><span class="sxs-lookup"><span data-stu-id="942ca-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-170">root</span><span class="sxs-lookup"><span data-stu-id="942ca-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-171">server</span><span class="sxs-lookup"><span data-stu-id="942ca-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-172">sql</span><span class="sxs-lookup"><span data-stu-id="942ca-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-173">support</span><span class="sxs-lookup"><span data-stu-id="942ca-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="942ca-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-175">sys</span><span class="sxs-lookup"><span data-stu-id="942ca-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="942ca-176">test2</span><span class="sxs-lookup"><span data-stu-id="942ca-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-177">test3</span><span class="sxs-lookup"><span data-stu-id="942ca-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-178">user4</span><span class="sxs-lookup"><span data-stu-id="942ca-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="942ca-179">user5</span><span class="sxs-lookup"><span data-stu-id="942ca-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="942ca-180">Quali sono i requisiti della password hello durante la creazione di una macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="942ca-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="942ca-181">Le password devono essere di 6-72 caratteri e soddisfare 3 fuori hello dopo 4 requisiti di complessità:</span><span class="sxs-lookup"><span data-stu-id="942ca-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="942ca-182">Devono contenere caratteri minuscoli</span><span class="sxs-lookup"><span data-stu-id="942ca-182">Have lower characters</span></span>
* <span data-ttu-id="942ca-183">Devono contenere caratteri maiuscoli</span><span class="sxs-lookup"><span data-stu-id="942ca-183">Have upper characters</span></span>
* <span data-ttu-id="942ca-184">Devono contenere almeno un numero</span><span class="sxs-lookup"><span data-stu-id="942ca-184">Have a digit</span></span>
* <span data-ttu-id="942ca-185">Devono contenere un carattere speciale (REGEX.CONFRONTA [\W_])</span><span class="sxs-lookup"><span data-stu-id="942ca-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="942ca-186">Hello seguendo le password non è consentito:</span><span class="sxs-lookup"><span data-stu-id="942ca-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="942ca-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="942ca-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="942ca-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="942ca-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="942ca-189">Password!</span><span class="sxs-lookup"><span data-stu-id="942ca-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="942ca-190">Password1</span><span class="sxs-lookup"><span data-stu-id="942ca-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="942ca-191">Password22</span><span class="sxs-lookup"><span data-stu-id="942ca-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="942ca-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="942ca-192">iloveyou!</span></span></td>
    </tr>
</table>
