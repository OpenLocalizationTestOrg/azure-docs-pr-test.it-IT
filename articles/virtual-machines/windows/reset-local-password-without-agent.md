---
title: Reimpostare una password di Windows locale senza l'agente di Azure | Documentazione Microsoft
description: "Come reimpostare la password di un account utente di Windows locale quando l'agente guest di Azure non è installato o funzionante in una VM"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: 880f5e5967298401fc2522124af3746d9906ffa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-local-windows-password-for-azure-vm"></a><span data-ttu-id="935df-103">Come reimpostare una password di Windows locale per una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="935df-103">How to reset local Windows password for Azure VM</span></span>
<span data-ttu-id="935df-104">È possibile reimpostare la password di Windows locale di una VM in Azure tramite il [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a condizione che l'agente guest di Azure sia installato.</span><span class="sxs-lookup"><span data-stu-id="935df-104">You can reset the local Windows password of a VM in Azure using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided the Azure guest agent is installed.</span></span> <span data-ttu-id="935df-105">Questo è il metodo principale per reimpostare una password per una VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="935df-105">This method is the primary way to reset a password for an Azure VM.</span></span> <span data-ttu-id="935df-106">In mancanza di risposta da parte dell'agente guest di Azure, o in caso di errore di installazione dopo il caricamento di un'immagine personalizzata, è possibile reimpostare la password di Windows manualmente.</span><span class="sxs-lookup"><span data-stu-id="935df-106">If you encounter issues with the Azure guest agent not responding, or failing to install after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="935df-107">Questo articolo illustra come reimpostare la password di un account locale collegando il disco virtuale del sistema operativo di origine a un'altra VM.</span><span class="sxs-lookup"><span data-stu-id="935df-107">This article details how to reset a local account password by attaching the source OS virtual disk to another VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="935df-108">Questo processo viene usato solo come ultima risorsa.</span><span class="sxs-lookup"><span data-stu-id="935df-108">Only use this process as a last resort.</span></span> <span data-ttu-id="935df-109">Provare sempre a reimpostare la password usando prima il [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="935df-109">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-the-process"></a><span data-ttu-id="935df-110">Panoramica della procedura</span><span class="sxs-lookup"><span data-stu-id="935df-110">Overview of the process</span></span>
<span data-ttu-id="935df-111">Di seguito sono elencati i passaggi fondamentali della reimpostazione di una password locale per una VM Windows in Azure quando non è possibile accedere all'agente guest di Azure:</span><span class="sxs-lookup"><span data-stu-id="935df-111">The core steps for performing a local password reset for a Windows VM in Azure when there is no access to the Azure guest agent is as follows:</span></span>

* <span data-ttu-id="935df-112">Eliminare la VM di origine.</span><span class="sxs-lookup"><span data-stu-id="935df-112">Delete the source VM.</span></span> <span data-ttu-id="935df-113">I dischi virtuali vengono mantenuti.</span><span class="sxs-lookup"><span data-stu-id="935df-113">The virtual disks are retained.</span></span>
* <span data-ttu-id="935df-114">Collegare il disco del sistema operativo della VM di origine a un'altra VM nella stessa posizione nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="935df-114">Attach the source VM's OS disk to another VM on the same location within your Azure subscription.</span></span> <span data-ttu-id="935df-115">Questa VM viene considerata come la VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="935df-115">This VM is referred to as the troubleshooting VM.</span></span>
* <span data-ttu-id="935df-116">Con l'ausilio di questa VM, creare dei file di configurazione sul disco del sistema operativo della VM di origine.</span><span class="sxs-lookup"><span data-stu-id="935df-116">Using the troubleshooting VM, create some config files on the source VM's OS disk.</span></span>
* <span data-ttu-id="935df-117">Scollegare il disco del sistema operativo della VM dalla VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="935df-117">Detach the VM's OS disk from the troubleshooting VM.</span></span>
* <span data-ttu-id="935df-118">Usare un modello di Resource Manager per creare una VM tramite il disco virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="935df-118">Use a Resource Manager template to create a VM, using the original virtual disk.</span></span>
* <span data-ttu-id="935df-119">All'avvio della nuova VM, i file di configurazione creati aggiornano la password dell'utente richiesto.</span><span class="sxs-lookup"><span data-stu-id="935df-119">When the new VM boots, the config files you create update the password of the required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="935df-120">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="935df-120">Detailed steps</span></span>
<span data-ttu-id="935df-121">Provare sempre a reimpostare la password usando il [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di procedere ai passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="935df-121">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying the following steps.</span></span> <span data-ttu-id="935df-122">Assicurarsi di disporre di un backup della VM prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="935df-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="935df-123">Eliminare la VM interessata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="935df-123">Delete the affected VM in Azure portal.</span></span> <span data-ttu-id="935df-124">Questa operazione determina l'eliminazione solo dei metadati, il riferimento della VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="935df-124">Deleting the VM only deletes the metadata, the reference of the VM within Azure.</span></span> <span data-ttu-id="935df-125">Quando la VM viene eliminata, i dischi virtuali vengono mantenuti:</span><span class="sxs-lookup"><span data-stu-id="935df-125">The virtual disks are retained when the VM is deleted:</span></span>
   
   * <span data-ttu-id="935df-126">Selezionare la VM nel portale di Azure, fare clic su *Elimina*:</span><span class="sxs-lookup"><span data-stu-id="935df-126">Select the VM in the Azure portal, click *Delete*:</span></span>
     
     ![Eliminare una VM esistente](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="935df-128">Collegare il disco del sistema operativo della VM di origine alla VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="935df-128">Attach the source VM’s OS disk to the troubleshooting VM.</span></span> <span data-ttu-id="935df-129">La VM per la risoluzione dei problemi deve essere nella stessa area del disco del sistema operativo della VM di origine (ad esempio `West US`):</span><span class="sxs-lookup"><span data-stu-id="935df-129">The troubleshooting VM must be in the same region as the source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="935df-130">Selezionare la VM per la risoluzione dei problemi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="935df-130">Select the troubleshooting VM in the Azure portal.</span></span> <span data-ttu-id="935df-131">Fare clic su *Dischi* | *Collega esistente*:</span><span class="sxs-lookup"><span data-stu-id="935df-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Collegare un disco esistente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="935df-133">Selezionare *File VHD*, quindi scegliere l'account di archiviazione contenente la VM di origine:</span><span class="sxs-lookup"><span data-stu-id="935df-133">Select *VHD File* and then select the storage account that contains your source VM:</span></span>
     
     ![Selezionare l'account di archiviazione](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="935df-135">Selezionare il contenitore di origine.</span><span class="sxs-lookup"><span data-stu-id="935df-135">Select the source container.</span></span> <span data-ttu-id="935df-136">Il contenitore di origine è in genere *vhd*:</span><span class="sxs-lookup"><span data-stu-id="935df-136">The source container is typically *vhds*:</span></span>
     
     ![Selezionare il contenitore di archiviazione](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="935df-138">Selezionare il disco rigido virtuale del sistema operativo da collegare.</span><span class="sxs-lookup"><span data-stu-id="935df-138">Select the OS vhd to attach.</span></span> <span data-ttu-id="935df-139">Fare clic su *Seleziona* per completare il processo:</span><span class="sxs-lookup"><span data-stu-id="935df-139">Click *Select* to complete the process:</span></span>
     
     ![Selezionare il disco virtuale di origine](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="935df-141">Connettersi alla VM per la risoluzione dei problemi tramite Desktop remoto e assicurarsi che il disco del sistema operativo della VM di origine sia visibile:</span><span class="sxs-lookup"><span data-stu-id="935df-141">Connect to the troubleshooting VM using Remote Desktop and ensure the source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="935df-142">Selezionare la VM per la risoluzione dei problemi nel portale di Azure e fare clic su *Connetti*.</span><span class="sxs-lookup"><span data-stu-id="935df-142">Select the troubleshooting VM in the Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="935df-143">Aprire il file RDP scaricato.</span><span class="sxs-lookup"><span data-stu-id="935df-143">Open the RDP file that downloads.</span></span> <span data-ttu-id="935df-144">Immettere il nome utente e la password della VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="935df-144">Enter the username and password of the troubleshooting VM.</span></span>
   * <span data-ttu-id="935df-145">In Esplora file cercare il disco dati collegato.</span><span class="sxs-lookup"><span data-stu-id="935df-145">In File Explorer, look for the data disk you attached.</span></span> <span data-ttu-id="935df-146">Se il disco rigido virtuale della VM di origine è l'unico disco dati collegato alla VM per la risoluzione dei problemi, questo deve corrispondere all'unità F:</span><span class="sxs-lookup"><span data-stu-id="935df-146">If the source VM’s VHD is the only data disk attached to the troubleshooting VM, it should be the F: drive:</span></span>
     
     ![Visualizzare il disco dati collegato](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="935df-148">Creare `gpt.ini` in `\Windows\System32\GroupPolicy` sull'unità della VM di origine (in presenza del file gpt.ini, rinominarlo in gpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="935df-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on the source VM’s drive (if gpt.ini exists, rename to gpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="935df-149">Assicurarsi di non creare accidentalmente i seguenti file in C:\Windows, l'unità del sistema operativo per la VM per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="935df-149">Make sure that you do not accidentally create the following files in C:\Windows, the OS drive for the troubleshooting VM.</span></span> <span data-ttu-id="935df-150">Creare i seguenti file nell'unità del sistema operativo per la VM di origine collegata come disco dati.</span><span class="sxs-lookup"><span data-stu-id="935df-150">Create the following files in the OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="935df-151">Aggiungere le righe seguenti al file `gpt.ini` creato:</span><span class="sxs-lookup"><span data-stu-id="935df-151">Add the following lines into the `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Creare gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="935df-153">Creare `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="935df-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="935df-154">Accertarsi che vengano visualizzate le cartelle nascoste.</span><span class="sxs-lookup"><span data-stu-id="935df-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="935df-155">Se necessario, creare le cartelle `Machine` o `Scripts`.</span><span class="sxs-lookup"><span data-stu-id="935df-155">If needed, create the `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="935df-156">Aggiungere le righe seguenti al file `scripts.ini` creato:</span><span class="sxs-lookup"><span data-stu-id="935df-156">Add the following lines the `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Creare scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="935df-158">Creare `FixAzureVM.cmd` in `\Windows\System32` con i contenuti seguenti, sostituendo `<username>` e `<newpassword>` con i propri valori:</span><span class="sxs-lookup"><span data-stu-id="935df-158">Create `FixAzureVM.cmd` in `\Windows\System32` with the following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Creare FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="935df-160">Quando si definisce la nuova password, è necessario soddisfare i requisiti di complessità delle password configurate per la VM.</span><span class="sxs-lookup"><span data-stu-id="935df-160">You must meet the configured password complexity requirements for your VM when defining the new password.</span></span>
7. <span data-ttu-id="935df-161">Nel portale di Azure scollegare il disco dalla VM per la risoluzione dei problemi:</span><span class="sxs-lookup"><span data-stu-id="935df-161">In Azure portal, detach the disk from the troubleshooting VM:</span></span>
   
   * <span data-ttu-id="935df-162">Selezionare la VM per la risoluzione dei problemi nel portale di Azure, fare clic su *Dischi*.</span><span class="sxs-lookup"><span data-stu-id="935df-162">Select the troubleshooting VM in the Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="935df-163">Selezionare il disco dati collegato nel passaggio 2, fare clic su *Scollega*:</span><span class="sxs-lookup"><span data-stu-id="935df-163">Select the data disk attached in step 2, click *Detach*:</span></span>
     
     ![Scollegare il disco](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="935df-165">Prima di creare una VM, è necessario ottenere l'URI per il disco del sistema operativo di origine:</span><span class="sxs-lookup"><span data-stu-id="935df-165">Before you create a VM, obtain the URI to your source OS disk:</span></span>
   
   * <span data-ttu-id="935df-166">Selezionare l'account di archiviazione nel portale di Azure, fare clic su *BLOB*.</span><span class="sxs-lookup"><span data-stu-id="935df-166">Select the storage account in the Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="935df-167">Selezionare il contenitore.</span><span class="sxs-lookup"><span data-stu-id="935df-167">Select the container.</span></span> <span data-ttu-id="935df-168">Il contenitore di origine è in genere *vhd*:</span><span class="sxs-lookup"><span data-stu-id="935df-168">The source container is typically *vhds*:</span></span>
     
     ![Selezionare il BLOB dell'account di archiviazione](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="935df-170">Selezionare il disco rigido virtuale del sistema operativo della VM di origine e fare clic sul pulsante *Copia* accanto al nome *URL*:</span><span class="sxs-lookup"><span data-stu-id="935df-170">Select your source VM OS VHD and click the *Copy* button next to the *URL* name:</span></span>
     
     ![Copiare l'URI del disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="935df-172">Creare una VM dal disco del sistema operativo della VM di origine:</span><span class="sxs-lookup"><span data-stu-id="935df-172">Create a VM from the source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="935df-173">Usare [questo modello di Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) per creare una VM da un disco rigido virtuale specializzato.</span><span class="sxs-lookup"><span data-stu-id="935df-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) to create a VM from a specialized VHD.</span></span> <span data-ttu-id="935df-174">Fare clic sul pulsante `Deploy to Azure` per aprire il portale di Azure con i dettagli basati su modelli compilati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="935df-174">Click the `Deploy to Azure` button to open the Azure portal with the templated details populated for you.</span></span>
   * <span data-ttu-id="935df-175">Per mantenere tutte le impostazioni precedenti per la VM, selezionare *Modifica modello* per fornire rete virtuale, subnet, scheda di rete o IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="935df-175">If you want to retain all the previous settings for the VM, select *Edit template* to provide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="935df-176">Nella casella di testo del parametro `OSDISKVHDURI` incollare l'URI del disco rigido virtuale di origine ottenuto nel passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="935df-176">In the `OSDISKVHDURI` parameter text box, paste the URI of your source VHD obtain in the preceding step:</span></span>
     
     ![Creare una VM dal modello](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="935df-178">Quando è in esecuzione, connettersi alla nuova VM tramite Desktop remoto con la nuova password specificata nello script `FixAzureVM.cmd`.</span><span class="sxs-lookup"><span data-stu-id="935df-178">After the new VM is running, connect to the VM using Remote Desktop with the new password you specified in the `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="935df-179">Dalla sessione remota per la nuova VM, rimuovere i file seguenti per pulire l'ambiente:</span><span class="sxs-lookup"><span data-stu-id="935df-179">From your remote session to the new VM, remove the following files to clean up the environment:</span></span>
    
    * <span data-ttu-id="935df-180">Da %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="935df-180">From %windir%\System32</span></span>
      * <span data-ttu-id="935df-181">rimuovere FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="935df-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="935df-182">Da %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="935df-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="935df-183">rimuovere scripts.ini</span><span class="sxs-lookup"><span data-stu-id="935df-183">remove scripts.ini</span></span>
    * <span data-ttu-id="935df-184">Da %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="935df-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="935df-185">rimuovere il file gpt.ini (se gpt.ini era presente in precedenza, ed era stato rinominato in gpt.ini.bak, modificare il nome del file con estensione bak nuovamente in gpt.ini)</span><span class="sxs-lookup"><span data-stu-id="935df-185">remove gpt.ini (if gpt.ini existed before, and you renamed it to gpt.ini.bak, rename the .bak file back to gpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="935df-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="935df-186">Next steps</span></span>
<span data-ttu-id="935df-187">Se non è ancora possibile connettersi tramite Desktop remoto, vedere la [guida alla risoluzione dei problemi di RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="935df-187">If you still cannot connect using Remote Desktop, see the [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="935df-188">La [guida alla risoluzione dei problemi di RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) esamina i metodi di risoluzione dei problemi anziché i passaggi specifici.</span><span class="sxs-lookup"><span data-stu-id="935df-188">The [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="935df-189">È anche possibile [aprire una richiesta di supporto tecnico di Azure](https://azure.microsoft.com/support/options/) per ricevere un supporto pratico.</span><span class="sxs-lookup"><span data-stu-id="935df-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

