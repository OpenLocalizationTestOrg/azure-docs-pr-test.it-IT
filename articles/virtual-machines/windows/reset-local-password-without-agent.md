---
title: aaaReset una password locale di Windows senza agente di Azure | Documenti Microsoft
description: "Come tooreset hello password dell'account utente locale di Windows quando l'agente guest Azure hello non è installato o funzionante in una macchina virtuale"
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
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="8258c-103">Come tooreset password di Windows locale per la macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="8258c-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="8258c-104">È possibile reimpostare la password di Windows locale di hello di una macchina virtuale in Azure utilizzando hello [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fornito è installato l'agente guest Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="8258c-105">Questo metodo è hello tooreset di mezzo principale con una password per una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8258c-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="8258c-106">Se si verificano problemi con l'agente guest Azure hello non risponde o non superati tooinstall dopo il caricamento di un'immagine personalizzata, è possibile reimpostare manualmente una password di Windows.</span><span class="sxs-lookup"><span data-stu-id="8258c-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="8258c-107">In questo articolo illustra in dettaglio come tooreset una password di account locale mediante l'aggiunta di hello tooanother disco virtuale di origine del sistema operativo VM.</span><span class="sxs-lookup"><span data-stu-id="8258c-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="8258c-108">Questo processo viene usato solo come ultima risorsa.</span><span class="sxs-lookup"><span data-stu-id="8258c-108">Only use this process as a last resort.</span></span> <span data-ttu-id="8258c-109">Provare sempre una password utilizzando hello tooreset [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima.</span><span class="sxs-lookup"><span data-stu-id="8258c-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="8258c-110">Panoramica del processo di hello</span><span class="sxs-lookup"><span data-stu-id="8258c-110">Overview of hello process</span></span>
<span data-ttu-id="8258c-111">passaggi di base Hello per l'esecuzione di una password locale reimpostata per una macchina virtuale Windows in Azure quando nessun agente guest Azure toohello di accesso è il seguente:</span><span class="sxs-lookup"><span data-stu-id="8258c-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="8258c-112">Eliminare una macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-112">Delete hello source VM.</span></span> <span data-ttu-id="8258c-113">i dischi virtuali Hello vengono mantenuti.</span><span class="sxs-lookup"><span data-stu-id="8258c-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="8258c-114">Collegare tooanother disco della macchina virtuale di hello origine del sistema operativo VM su hello stessa posizione all'interno di sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8258c-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="8258c-115">Questa macchina virtuale è hello di cui viene fatto riferimento tooas risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8258c-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="8258c-116">Utilizzando hello risoluzione dei problemi di macchina virtuale, creare i file di configurazione dal disco del sistema operativo della macchina virtuale di hello origine.</span><span class="sxs-lookup"><span data-stu-id="8258c-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="8258c-117">Scollegare il disco del sistema operativo della macchina virtuale di hello da hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8258c-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="8258c-118">Utilizzare un toocreate di gestione risorse modello una macchina virtuale con disco virtuale originale hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="8258c-119">Quando viene avviato a nuova macchina virtuale, hello hello i file di configurazione è creare hello aggiornamento della password dell'utente hello necessario.</span><span class="sxs-lookup"><span data-stu-id="8258c-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="8258c-120">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="8258c-120">Detailed steps</span></span>
<span data-ttu-id="8258c-121">Provare sempre una password utilizzando hello tooreset [portale di Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di tentare di hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="8258c-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="8258c-122">Assicurarsi di disporre di un backup della VM prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="8258c-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="8258c-123">Eliminare hello interessate VM nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8258c-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="8258c-124">L'eliminazione hello VM Elimina solo i metadati hello, riferimento hello di hello VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="8258c-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="8258c-125">i dischi virtuali Hello vengono mantenuti quando viene eliminato hello VM:</span><span class="sxs-lookup"><span data-stu-id="8258c-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="8258c-126">Fare clic su hello seleziona macchina virtuale nel portale di Azure hello *eliminare*:</span><span class="sxs-lookup"><span data-stu-id="8258c-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Eliminare la VM esistente](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="8258c-128">Collegare toohello di disco del sistema operativo della macchina virtuale di hello origine risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8258c-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="8258c-129">Hello risoluzione dei problemi di macchina virtuale deve essere in hello stessa area come disco del sistema operativo della macchina virtuale di hello origine (ad esempio `West US`):</span><span class="sxs-lookup"><span data-stu-id="8258c-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="8258c-130">Selezionare la risoluzione dei problemi di macchina virtuale nel portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="8258c-131">Fare clic su *Dischi* | *Collega esistente*:</span><span class="sxs-lookup"><span data-stu-id="8258c-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Collegare un disco esistente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="8258c-133">Selezionare *File VHD* e quindi selezionare l'account di archiviazione hello che contiene la macchina virtuale di origine:</span><span class="sxs-lookup"><span data-stu-id="8258c-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Selezionare l'account di archiviazione](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="8258c-135">Selezionare il contenitore di origine hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-135">Select hello source container.</span></span> <span data-ttu-id="8258c-136">contenitore di origine Hello è in genere *dischi rigidi virtuali*:</span><span class="sxs-lookup"><span data-stu-id="8258c-136">hello source container is typically *vhds*:</span></span>
     
     ![Selezionare il contenitore di archiviazione](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="8258c-138">Selezionare hello tooattach di disco rigido virtuale del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8258c-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="8258c-139">Fare clic su *selezionare* processo hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8258c-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Selezionare il disco virtuale di origine](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="8258c-141">Toohello macchina virtuale tramite Desktop remoto di risoluzione dei problemi di connessione e assicurarsi che è visibile disco del sistema operativo della macchina virtuale di hello origine:</span><span class="sxs-lookup"><span data-stu-id="8258c-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="8258c-142">Selezionare la risoluzione dei problemi di macchina virtuale nel portale di Azure hello hello e fare clic su *Connetti*.</span><span class="sxs-lookup"><span data-stu-id="8258c-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="8258c-143">Aprire il file RDP hello che scarica.</span><span class="sxs-lookup"><span data-stu-id="8258c-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="8258c-144">Immettere nome utente di hello e la password di hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8258c-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="8258c-145">In Esplora File, cercare il disco di dati hello che è collegato.</span><span class="sxs-lookup"><span data-stu-id="8258c-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="8258c-146">Se hello origine che disco rigido virtuale della macchina virtuale è hello toohello disco collegato dati solo la risoluzione dei problemi di macchina virtuale, questa deve essere unità f: hello:</span><span class="sxs-lookup"><span data-stu-id="8258c-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Visualizzare il disco dati collegato](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="8258c-148">Creare `gpt.ini` in `\Windows\System32\GroupPolicy` sul disco della macchina virtuale di hello origine (se esiste gpt.ini, rinominare toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="8258c-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="8258c-149">Assicurarsi che non accidentalmente creare hello i seguenti file in C:\Windows, hello unità del sistema operativo per la risoluzione dei problemi di VM hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="8258c-150">Creare i seguenti file nell'unità di hello del sistema operativo per la macchina virtuale che viene collegato un disco dati di origine hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="8258c-151">Aggiungere hello dopo le righe in hello `gpt.ini` file creato:</span><span class="sxs-lookup"><span data-stu-id="8258c-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Creare gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="8258c-153">Creare `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="8258c-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="8258c-154">Accertarsi che vengano visualizzate le cartelle nascoste.</span><span class="sxs-lookup"><span data-stu-id="8258c-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="8258c-155">Se necessario, creare hello `Machine` o `Scripts` cartelle.</span><span class="sxs-lookup"><span data-stu-id="8258c-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="8258c-156">Aggiungere hello seguente hello righe `scripts.ini` file creato:</span><span class="sxs-lookup"><span data-stu-id="8258c-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Creare scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="8258c-158">Creare `FixAzureVM.cmd` in `\Windows\System32` con hello contenuto seguente, sostituendo `<username>` e `<newpassword>` con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="8258c-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Creare FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="8258c-160">Quando si definisce una nuova password hello, è necessario soddisfare i requisiti di complessità password hello configurato per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8258c-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="8258c-161">Nel portale di Azure, scollegare il disco di hello dalla risoluzione dei problemi di VM hello:</span><span class="sxs-lookup"><span data-stu-id="8258c-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="8258c-162">Selezionare la risoluzione dei problemi di macchina virtuale nel portale di Azure hello hello, fare clic su *dischi*.</span><span class="sxs-lookup"><span data-stu-id="8258c-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="8258c-163">I dischi di dati selezionare hello collegati nel passaggio 2, fare clic su *scollegamento*:</span><span class="sxs-lookup"><span data-stu-id="8258c-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Scollegare il disco](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="8258c-165">Prima di creare una macchina virtuale, è possibile ottenere il disco del sistema operativo di hello URI tooyour origine:</span><span class="sxs-lookup"><span data-stu-id="8258c-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="8258c-166">Fare clic su account di archiviazione hello selezionare nel portale di Azure hello *BLOB*.</span><span class="sxs-lookup"><span data-stu-id="8258c-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="8258c-167">Selezionare il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="8258c-167">Select hello container.</span></span> <span data-ttu-id="8258c-168">contenitore di origine Hello è in genere *dischi rigidi virtuali*:</span><span class="sxs-lookup"><span data-stu-id="8258c-168">hello source container is typically *vhds*:</span></span>
     
     ![Selezionare il BLOB dell'account di archiviazione](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="8258c-170">Selezionare il disco rigido virtuale del sistema operativo VM di origine e fare clic su hello *copia* pulsante Avanti toohello *URL* nome:</span><span class="sxs-lookup"><span data-stu-id="8258c-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Copiare l'URI del disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="8258c-172">Creare una macchina virtuale dal disco del sistema operativo della macchina virtuale di hello origine:</span><span class="sxs-lookup"><span data-stu-id="8258c-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="8258c-173">Utilizzare [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate una macchina virtuale da un disco rigido virtuale specializzata.</span><span class="sxs-lookup"><span data-stu-id="8258c-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="8258c-174">Fare clic su hello `Deploy tooAzure` hello tooopen pulsante portale di Azure con i dettagli di hello basati su modelli popolato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8258c-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="8258c-175">Se si desiderano tooretain tutte le impostazioni precedenti hello per hello macchina virtuale, selezionare *modifica modelli* tooprovide la rete virtuale esistente, subnet, scheda di rete o indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="8258c-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="8258c-176">In hello `OSDISKVHDURI` la casella di testo di parametro, hello Incolla ottenere l'URI dell'origine del disco rigido virtuale nel precedente passaggio hello:</span><span class="sxs-lookup"><span data-stu-id="8258c-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Creare una VM dal modello](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="8258c-178">Dopo aver hello nuova macchina virtuale è in esecuzione, connettersi toohello macchina virtuale tramite Desktop remoto con password hello specificata in hello `FixAzureVM.cmd` script.</span><span class="sxs-lookup"><span data-stu-id="8258c-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="8258c-179">Da toohello la sessione remota nuova macchina virtuale, rimuovere hello seguente file tooclean ambiente hello:</span><span class="sxs-lookup"><span data-stu-id="8258c-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="8258c-180">Da %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="8258c-180">From %windir%\System32</span></span>
      * <span data-ttu-id="8258c-181">rimuovere FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="8258c-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="8258c-182">Da %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="8258c-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="8258c-183">rimuovere scripts.ini</span><span class="sxs-lookup"><span data-stu-id="8258c-183">remove scripts.ini</span></span>
    * <span data-ttu-id="8258c-184">Da %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="8258c-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="8258c-185">rimuovere gpt.ini (gpt.ini esistenti prima, se è stata rinominata toogpt.ini.bak, ridenominazione hello bak file indietro toogpt.ini)</span><span class="sxs-lookup"><span data-stu-id="8258c-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8258c-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8258c-186">Next steps</span></span>
<span data-ttu-id="8258c-187">Se non è possibile connettersi tramite Desktop remoto, vedere hello [Guida alla risoluzione dei problemi di RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8258c-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8258c-188">Hello [RDP risoluzione dei problemi di Guida dettagliate](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) esamina la risoluzione dei problemi relativi a metodi anziché i passaggi specifici.</span><span class="sxs-lookup"><span data-stu-id="8258c-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="8258c-189">È anche possibile [aprire una richiesta di supporto tecnico di Azure](https://azure.microsoft.com/support/options/) per ricevere un supporto pratico.</span><span class="sxs-lookup"><span data-stu-id="8258c-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

