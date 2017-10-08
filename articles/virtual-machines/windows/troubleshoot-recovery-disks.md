---
title: aaaUse una macchina virtuale con Azure PowerShell di risoluzione dei problemi di Windows | Documenti Microsoft
description: Informazioni su come problemi tootroubleshoot macchina virtuale Windows in Azure tramite la connessione di ripristino di tooa dischi hello del sistema operativo VM con Azure PowerShell
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="5fd58-103">Risolvere i problemi relativi a una macchina virtuale di Windows tramite il collegamento di ripristino di tooa dischi hello del sistema operativo VM con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fd58-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="5fd58-104">Se la macchina di virtuale (VM) di Windows in Azure rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso.</span><span class="sxs-lookup"><span data-stu-id="5fd58-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="5fd58-105">Un esempio comune sarebbe un aggiornamento di applicazione non riuscita che impedisce hello macchina virtuale in grado di tooboot correttamente.</span><span class="sxs-lookup"><span data-stu-id="5fd58-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="5fd58-106">Questo articolo come dettagli toouse Azure PowerShell tooconnect toofix di macchina virtuale Windows tooanother il disco rigido virtuale eventuali errori, quindi ricreare la macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="5fd58-107">Panoramica del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="5fd58-107">Recovery process overview</span></span>
<span data-ttu-id="5fd58-108">processo di risoluzione dei problemi di Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5fd58-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="5fd58-109">Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="5fd58-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="5fd58-110">Collegare e montare hello tooanother di disco rigido virtuale a macchina virtuale di Windows per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="5fd58-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="5fd58-111">Connettersi toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="5fd58-112">Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="5fd58-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="5fd58-113">Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="5fd58-114">Creare una macchina virtuale con disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="5fd58-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="5fd58-115">Assicurarsi di aver [hello più recente di Azure PowerShell](/powershell/azure/overview) installato e registrato nella sottoscrizione tooyour:</span><span class="sxs-lookup"><span data-stu-id="5fd58-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="5fd58-116">In hello negli esempi seguenti, sostituire i nomi dei parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="5fd58-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="5fd58-117">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="5fd58-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="5fd58-118">Individuare i problemi di avvio</span><span class="sxs-lookup"><span data-stu-id="5fd58-118">Determine boot issues</span></span>
<span data-ttu-id="5fd58-119">È possibile visualizzare una schermata della macchina virtuale in Azure toohelp di risolvere i problemi di avvio.</span><span class="sxs-lookup"><span data-stu-id="5fd58-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="5fd58-120">Questa schermata consente di identificare il motivo di una macchina virtuale ha esito negativo tooboot.</span><span class="sxs-lookup"><span data-stu-id="5fd58-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="5fd58-121">Hello seguente esempio mostra come ottenere schermata hello dalla macchina virtuale di Windows denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5fd58-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="5fd58-122">Esaminare toodetermine schermata hello hello VM motivi tooboot.</span><span class="sxs-lookup"><span data-stu-id="5fd58-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="5fd58-123">Esaminare i messaggi di errore o i codici di errore specifici visualizzati.</span><span class="sxs-lookup"><span data-stu-id="5fd58-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="5fd58-124">Visualizzare i dettagli del disco rigido virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="5fd58-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="5fd58-125">Prima di poter allegare i tooanother di disco rigido virtuale a macchina virtuale, è necessario il nome hello tooidentify di hello disco rigido virtuale (VHD).</span><span class="sxs-lookup"><span data-stu-id="5fd58-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="5fd58-126">Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5fd58-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="5fd58-127">Cercare `Vhd URI` all'interno di hello `StorageProfile` sezione dall'output di hello di hello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="5fd58-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="5fd58-128">output di esempio troncato seguente Hello Mostra hello `Vhd URI` verso la fine hello del blocco di codice hello:</span><span class="sxs-lookup"><span data-stu-id="5fd58-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="5fd58-129">Eliminare la VM esistente</span><span class="sxs-lookup"><span data-stu-id="5fd58-129">Delete existing VM</span></span>
<span data-ttu-id="5fd58-130">In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte.</span><span class="sxs-lookup"><span data-stu-id="5fd58-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="5fd58-131">Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="5fd58-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="5fd58-132">Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="5fd58-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="5fd58-133">Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="5fd58-134">Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="5fd58-135">lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.</span><span class="sxs-lookup"><span data-stu-id="5fd58-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="5fd58-136">primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso.</span><span class="sxs-lookup"><span data-stu-id="5fd58-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="5fd58-137">L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5fd58-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="5fd58-138">Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.</span><span class="sxs-lookup"><span data-stu-id="5fd58-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="5fd58-139">Hello seguente esempio vengono eliminate hello macchina virtuale denominata `myVM` dal gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5fd58-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="5fd58-140">Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="5fd58-141">lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="5fd58-142">Collegare tooanother disco rigido virtuale esistente VM</span><span class="sxs-lookup"><span data-stu-id="5fd58-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="5fd58-143">Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="5fd58-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="5fd58-144">Per collegare hello toothis di disco rigido virtuale esistente toobrowse VM di risoluzione dei problemi e modificare il contenuto del disco hello.</span><span class="sxs-lookup"><span data-stu-id="5fd58-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="5fd58-145">Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system.</span><span class="sxs-lookup"><span data-stu-id="5fd58-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="5fd58-146">Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="5fd58-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="5fd58-147">Quando si collega hello disco rigido virtuale esistente, specificare disco toohello di URL hello ottenuto in precedenza hello `Get-AzureRmVM` comando.</span><span class="sxs-lookup"><span data-stu-id="5fd58-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="5fd58-148">esempio Hello collega un toohello disco rigido virtuale esistente, risoluzione dei problemi di macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5fd58-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="5fd58-149">Aggiunta di un disco, è necessario dimensioni hello toospecify del disco hello.</span><span class="sxs-lookup"><span data-stu-id="5fd58-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="5fd58-150">Come si collega un disco esistente, hello `-DiskSizeInGB` è specificato come `$null`.</span><span class="sxs-lookup"><span data-stu-id="5fd58-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="5fd58-151">Questo valore garantisce disco dati hello è correttamente associato e senza hello necessario toodetermine hello dimensione effettiva del disco dati.</span><span class="sxs-lookup"><span data-stu-id="5fd58-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="5fd58-152">Montare il disco di dati collegato hello</span><span class="sxs-lookup"><span data-stu-id="5fd58-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="5fd58-153">Risoluzione dei problemi di macchina virtuale utilizzando le credenziali appropriate hello tooyour RDP.</span><span class="sxs-lookup"><span data-stu-id="5fd58-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="5fd58-154">esempio Hello Scarica file di connessione RDP hello per la macchina virtuale denominata hello `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`e lo scarica troppo`C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="5fd58-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="5fd58-155">disco dati Hello viene automaticamente rilevato e collegato.</span><span class="sxs-lookup"><span data-stu-id="5fd58-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="5fd58-156">Elenco hello volumi collegati toodetermine hello di lettera di unità come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5fd58-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="5fd58-157">Hello output di esempio seguente viene illustrato il disco rigido virtuale di hello connesso un disco **2**.</span><span class="sxs-lookup"><span data-stu-id="5fd58-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="5fd58-158">(È anche possibile usare `Get-Volume` lettera di unità hello tooview):</span><span class="sxs-lookup"><span data-stu-id="5fd58-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="5fd58-159">Risolvere i problemi del disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="5fd58-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="5fd58-160">Con hello esistente disco rigido virtuale montato, è ora possibile eseguire operazioni di manutenzione e risoluzione dei problemi in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5fd58-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="5fd58-161">Dopo avere risolto i problemi di hello, continuare con hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="5fd58-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="5fd58-162">Smontare e scollegare il disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="5fd58-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="5fd58-163">Una volta risolti gli errori, si smontare e Scollega hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="5fd58-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="5fd58-164">È possibile utilizzare il disco rigido virtuale con qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello collegamento hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="5fd58-165">Dalla sessione RDP, smontare disco dati hello nella macchina virtuale di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5fd58-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="5fd58-166">È necessario il numero di disco hello da hello precedente `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5fd58-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="5fd58-167">Utilizzare quindi `Set-Disk` disco come non in linea di tooset hello:</span><span class="sxs-lookup"><span data-stu-id="5fd58-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="5fd58-168">Verificare il disco di hello è impostato come non in linea utilizzando `Get-Disk` nuovamente.</span><span class="sxs-lookup"><span data-stu-id="5fd58-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="5fd58-169">Hello output di esempio seguente viene illustrato il disco di hello è ora impostato come offline:</span><span class="sxs-lookup"><span data-stu-id="5fd58-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="5fd58-170">Uscire dalla sessione RDP.</span><span class="sxs-lookup"><span data-stu-id="5fd58-170">Exit your RDP session.</span></span> <span data-ttu-id="5fd58-171">Dalla sessione di PowerShell di Azure, rimuovere il disco rigido virtuale di hello hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="5fd58-172">Creare una macchina virtuale dal disco rigido originale</span><span class="sxs-lookup"><span data-stu-id="5fd58-172">Create VM from original hard disk</span></span>
<span data-ttu-id="5fd58-173">utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="5fd58-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="5fd58-174">modello JSON effettivi Hello è hello link riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5fd58-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="5fd58-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="5fd58-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="5fd58-176">modello Hello distribuisce una macchina virtuale in una rete virtuale esistente, utilizzando il messaggio hello URL VHD from hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="5fd58-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="5fd58-177">esempio Hello distribuisce hello modello toohello gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5fd58-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="5fd58-178">Hello risposta richiesto per il modello di hello come nome della macchina virtuale, il tipo del sistema operativo e dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="5fd58-179">Hello `osDiskVhdUri` è hello stesso utilizzato in precedenza durante l'associazione toohello disco rigido virtuale esistente hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fd58-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="5fd58-180">Riabilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="5fd58-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="5fd58-181">Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5fd58-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="5fd58-182">esempio Hello consente hello un'estensione di diagnostica nella macchina virtuale denominata hello `myVMDeployed` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5fd58-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="5fd58-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5fd58-183">Next steps</span></span>
<span data-ttu-id="5fd58-184">Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni RDP risolvere macchina virtuale di Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fd58-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5fd58-185">Per problemi relativi all'accesso alle applicazioni in esecuzione nella VM, vedere [Risolvere i problemi di connettività a un'applicazione in una macchina virtuale Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fd58-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5fd58-186">Per altre informazioni sull'uso di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fd58-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
