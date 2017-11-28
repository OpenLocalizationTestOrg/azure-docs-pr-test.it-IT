---
title: aaaCapture toouse una macchina virtuale Linux di Azure come modello | Documenti Microsoft
description: Informazioni su come toocapture e generalizzare un'immagine di una basata su Linux Azure macchina virtuale (VM) creata con modello di distribuzione Azure Resource Manager hello.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="a1367-103">Acquisire una VM Linux in esecuzione su Azure</span><span class="sxs-lookup"><span data-stu-id="a1367-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="a1367-104">Seguire i passaggi hello in toogeneralize questo articolo e acquisire una macchina virtuale Linux di Azure (VM) in modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="a1367-105">Quando si generalizza hello macchina virtuale, si rimuovere informazioni sull'account personale e si prepara hello VM toobe utilizzato come immagine.</span><span class="sxs-lookup"><span data-stu-id="a1367-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="a1367-106">È quindi l'acquisizione dell'immagine di un disco rigido virtuale generalizzato (VHD) per hello del sistema operativo, i dischi rigidi virtuali per i dischi dati collegati, e un [modello di gestione risorse](../../azure-resource-manager/resource-group-overview.md) per nuove distribuzioni di macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="a1367-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="a1367-107">In questo articolo illustra in dettaglio come immagine toocapture una macchina virtuale con hello Azure CLI 1.0 per una macchina virtuale tramite dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="a1367-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="a1367-108">È anche possibile [acquisire una macchina virtuale con dischi di Azure gestiti hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1367-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a1367-109">Dischi gestiti vengono gestiti dal hello piattaforma Azure e non richiedono alcun toostore preparazione o percorso li.</span><span class="sxs-lookup"><span data-stu-id="a1367-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="a1367-110">Per altre informazioni, vedere [Azure Managed Disks Overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="a1367-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="a1367-111">toocreate macchine virtuali con immagine di hello, configurare le risorse di rete per ogni nuova macchina virtuale e utilizzare toodeploy modello (un file JavaScript Object Notation o JSON) hello dalla hello acquisita immagini VHD.</span><span class="sxs-lookup"><span data-stu-id="a1367-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="a1367-112">In questo modo, è possibile replicare una macchina virtuale con la configurazione corrente di software, analogamente toohello usare immagini in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a1367-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="a1367-113">Se si desidera toocreate una copia della VM Linux esistente con il relativo stato specializzato per il backup o il debug, vedere [creare una copia di una macchina virtuale di Linux in esecuzione in Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1367-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a1367-114">Se si desidera tooupload un VHD Linux da una macchina virtuale locale, vedere [caricare e creare una VM Linux dall'immagine del disco personalizzato](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1367-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a1367-115">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="a1367-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a1367-116">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="a1367-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a1367-117">[Azure CLI 1.0](#before-you-begin) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="a1367-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a1367-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="a1367-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1367-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a1367-119">Before you begin</span></span>
<span data-ttu-id="a1367-120">Verificare che siano soddisfatti hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="a1367-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="a1367-121">**Macchina virtuale di Azure creata nel modello di distribuzione di gestione risorse di hello** -se è stata creata una VM Linux, è possibile utilizzare hello [portale](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [CLI di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), o [Gestione risorse modelli](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="a1367-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="a1367-122">Configurare hello macchina virtuale in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="a1367-122">Configure hello VM as needed.</span></span> <span data-ttu-id="a1367-123">Ad esempio, [aggiungere dischi dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), applicare aggiornamenti e installare applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a1367-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="a1367-124">**CLI di Azure** -Install hello [CLI di Azure](../../cli-install-nodejs.md) in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="a1367-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="a1367-125">Passaggio 1: Rimuovere l'agente Linux di Azure hello</span><span class="sxs-lookup"><span data-stu-id="a1367-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="a1367-126">Eseguire innanzitutto hello **waagent** con hello **deprovisioning** parametro hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="a1367-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="a1367-127">Questo comando Elimina i file e dati toomake hello VM pronto per la generalizzazione.</span><span class="sxs-lookup"><span data-stu-id="a1367-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="a1367-128">Per informazioni dettagliate, vedere hello [Guida dell'utente dell'agente Linux di Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1367-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="a1367-129">Connettersi tooyour VM Linux utilizzando un client SSH.</span><span class="sxs-lookup"><span data-stu-id="a1367-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="a1367-130">Nella finestra di hello SSH, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a1367-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="a1367-131">Solo il seguente comando in una macchina virtuale che si desidera toocapture come immagine.</span><span class="sxs-lookup"><span data-stu-id="a1367-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="a1367-132">Non garantisce che l'immagine hello viene cancellato di tutte le informazioni riservate o adatto per la ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="a1367-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="a1367-133">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a1367-133">Type **y** toocontinue.</span></span> <span data-ttu-id="a1367-134">È possibile aggiungere hello **-force** tooavoid parametro questo passaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="a1367-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="a1367-135">Al termine del comando di hello, digitare **uscire**.</span><span class="sxs-lookup"><span data-stu-id="a1367-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="a1367-136">Questo passaggio consente di chiudere client SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="a1367-137">Passaggio 2: Acquisizione hello VM</span><span class="sxs-lookup"><span data-stu-id="a1367-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="a1367-138">Utilizzare toogeneralize CLI di Azure hello e acquisire hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="a1367-139">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="a1367-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a1367-140">I nomi dei parametri di esempio includono **myResourceGroup**, **myVnet** e **myVM**.</span><span class="sxs-lookup"><span data-stu-id="a1367-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="a1367-141">Dal computer locale, aprire hello Azure CLI e [tooyour accesso sottoscrizione di Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a1367-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="a1367-142">Verificare di essere in modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a1367-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="a1367-143">Arrestare hello macchina virtuale che già deprovisioning utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a1367-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="a1367-144">Generalizzare hello VM con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a1367-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="a1367-145">A questo punto eseguire hello **acquisizione macchina virtuale di azure** comando, che acquisisce hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="a1367-146">Nell'esempio seguente di hello, immagine hello vengono acquisiti i dischi rigidi virtuali con nomi che iniziano con **MyVHDNamePrefix**, hello e **-t** opzione specifica un modello di percorso toohello **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="a1367-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="a1367-147">i file VHD di Hello immagine vengono creati per impostazione predefinita in hello stesso account di archiviazione che hello VM originale utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a1367-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="a1367-148">Hello utilizzare *stesso account di archiviazione* toostore hello dischi rigidi virtuali per nuove macchine virtuali create da immagini hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="a1367-149">percorso di hello toofind di un'immagine acquisita, il modello JSON hello aperto in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="a1367-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="a1367-150">In hello **storageProfile**, trovare hello **uri** di hello **immagine** si trova in hello **sistema** contenitore.</span><span class="sxs-lookup"><span data-stu-id="a1367-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="a1367-151">Ad esempio, hello URI dell'immagine del disco del sistema operativo hello è simile troppo`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="a1367-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="a1367-152">Passaggio 3: Creare una macchina virtuale dall'immagine acquisita hello</span><span class="sxs-lookup"><span data-stu-id="a1367-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="a1367-153">Ora è possibile utilizzare immagini hello con un toocreate modello una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="a1367-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="a1367-154">Questi passaggi mostrano come toouse hello Azure CLI e hello modello file JSON acquisita toocreate hello VM in una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="a1367-155">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="a1367-155">Create network resources</span></span>
<span data-ttu-id="a1367-156">modello di hello toouse, è necessario innanzitutto tooset di una rete virtuale e una scheda di rete per la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="a1367-157">È consigliabile che creare un gruppo di risorse per tali risorse in posizione hello in cui memorizzare l'immagine di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="a1367-158">Eseguire i comandi simile toohello seguente, sostituendo i nomi per le risorse e un percorso appropriato di Azure ("centralus" in questi comandi):</span><span class="sxs-lookup"><span data-stu-id="a1367-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="a1367-159">Ottenere l'Id di hello NIC hello</span><span class="sxs-lookup"><span data-stu-id="a1367-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="a1367-160">toodeploy una macchina virtuale dall'immagine hello utilizzando hello JSON è stato salvato durante l'acquisizione, è necessario hello Id di hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="a1367-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="a1367-161">Ottenerlo eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a1367-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="a1367-162">Hello **Id** hello output è analogo troppo`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="a1367-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="a1367-163">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a1367-163">Create a VM</span></span>
<span data-ttu-id="a1367-164">Dopo il comando che segue hello esecuzione toocreate la macchina virtuale da hello acquisito l'immagine di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="a1367-165">Hello utilizzare **-f** parametro toospecify hello percorso toohello modello JSON file salvato.</span><span class="sxs-lookup"><span data-stu-id="a1367-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="a1367-166">Nell'output del comando hello, sono richieste toosupply un nuovo nome della macchina virtuale, nome utente amministratore di hello e una password e Id della scheda di rete creato in precedenza hello hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="a1367-167">Hello seguente esempio viene illustrato ciò che viene visualizzato per una corretta distribuzione:</span><span class="sxs-lookup"><span data-stu-id="a1367-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="a1367-168">Verificare la distribuzione di hello</span><span class="sxs-lookup"><span data-stu-id="a1367-168">Verify hello deployment</span></span>
<span data-ttu-id="a1367-169">Ora SSH toohello macchina virtuale è stato creato distribuzione hello tooverify e iniziare a usare hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="a1367-170">tooconnect tramite SSH, trovare l'indirizzo IP di hello di hello macchina virtuale creata tramite l'esecuzione di hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a1367-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="a1367-171">indirizzo IP pubblico Hello è elencato nella finestra di output del comando hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="a1367-172">Per impostazione predefinita si connetterà toohello VM Linux da SSH sulla porta 22.</span><span class="sxs-lookup"><span data-stu-id="a1367-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="a1367-173">Creare altre macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a1367-173">Create additional VMs</span></span>
<span data-ttu-id="a1367-174">Hello utilizzare acquisiti toodeploy immagine e il modello di altre macchine virtuali utilizzando i passaggi di hello hello precedente sezione.</span><span class="sxs-lookup"><span data-stu-id="a1367-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="a1367-175">Altre opzioni toocreate macchine virtuali, dall'immagine hello includono utilizzando un modello di avvio rapido o l'esecuzione di hello **macchina virtuale di azure creare** comando.</span><span class="sxs-lookup"><span data-stu-id="a1367-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="a1367-176">Modello di hello acquisita</span><span class="sxs-lookup"><span data-stu-id="a1367-176">Use hello captured template</span></span>
<span data-ttu-id="a1367-177">hello toouse acquisiti immagine e il modello, seguire questi passaggi (descritta in dettaglio nella precedente sezione hello):</span><span class="sxs-lookup"><span data-stu-id="a1367-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="a1367-178">Verificare che l'immagine di macchina virtuale sia in hello stesso account di archiviazione che ospita VHD virtuale della macchina.</span><span class="sxs-lookup"><span data-stu-id="a1367-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="a1367-179">Copiare i file JSON del modello di hello e specificare un nome univoco per il disco del sistema operativo hello del hello nuova macchina virtuale disco rigido virtuale (o i dischi rigidi virtuali).</span><span class="sxs-lookup"><span data-stu-id="a1367-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="a1367-180">Ad esempio, in hello **storageProfile**, in **vhd**nella **uri**, specificare un nome univoco per hello **osDisk** disco rigido virtuale, simile troppo`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="a1367-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="a1367-181">Creare una scheda di rete in uno hello stesso o in un'altra rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="a1367-182">Utilizza file JSON di hello modificato del modello, creare una distribuzione nel gruppo di risorse hello in cui impostare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="a1367-183">Uso di un modello di Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="a1367-183">Use a quickstart template</span></span>
<span data-ttu-id="a1367-184">Se si desidera configurare automaticamente quando si crea una macchina virtuale dall'immagine hello rete di hello, è possibile specificare tali risorse in un modello.</span><span class="sxs-lookup"><span data-stu-id="a1367-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="a1367-185">Ad esempio, vedere hello [101 vm da utente immagine modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) da GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1367-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="a1367-186">Questo modello consente di creare una macchina virtuale dall'immagine personalizzata e rete virtuale necessaria hello, indirizzo IP pubblico e le risorse di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a1367-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="a1367-187">Per una procedura dettagliata dell'utilizzo di modello hello in hello portale di Azure, vedere [come una macchina virtuale da un'immagine personalizzata utilizzando un modello di gestione risorse toocreate](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="a1367-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="a1367-188">Utilizzare hello azure vm creare un comando</span><span class="sxs-lookup"><span data-stu-id="a1367-188">Use hello azure vm create command</span></span>
<span data-ttu-id="a1367-189">In genere è più semplice toouse toocreate di modello una macchina virtuale dall'immagine hello un gestore delle risorse.</span><span class="sxs-lookup"><span data-stu-id="a1367-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="a1367-190">Tuttavia, è possibile creare VM hello *in modo imperativo* utilizzando hello **macchina virtuale di azure creare** con hello **-Q** (**-immagine urn**) parametro .</span><span class="sxs-lookup"><span data-stu-id="a1367-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="a1367-191">Se si utilizza questo metodo, è anche passare hello **-d** (**- os-disco-disco rigido virtuale**) percorso hello toospecify di parametro del file con estensione vhd hello del sistema operativo per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="a1367-192">Questo file deve essere nel contenitore di dischi rigidi virtuali hello hello dell'account di archiviazione in cui è archiviato i file VHD dell'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="a1367-193">comando copie hello VHD per hello Hello nuova macchina virtuale automaticamente toohello **dischi rigidi virtuali** contenitore.</span><span class="sxs-lookup"><span data-stu-id="a1367-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="a1367-194">Prima di eseguire **macchina virtuale di azure creare** con immagine di hello, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a1367-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="a1367-195">Creare un gruppo di risorse, o identificare un gruppo di risorse esistente per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="a1367-196">Creare un pubblico risorsa indirizzo IP e una risorsa NIC per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a1367-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="a1367-197">Per passaggi toocreate rete virtuale, un indirizzo IP di pubblico e NIC mediante hello CLI, vedere più indietro in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a1367-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="a1367-198">(**macchina virtuale di azure creare** inoltre possibile creare una scheda di rete, ma è necessario toopass di parametri aggiuntivi per una rete virtuale e una subnet.)</span><span class="sxs-lookup"><span data-stu-id="a1367-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="a1367-199">Quindi eseguire un comando che passa gli URI tooboth hello nuovo disco rigido virtuale del sistema operativo file e hello immagine esistente.</span><span class="sxs-lookup"><span data-stu-id="a1367-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="a1367-200">In questo esempio viene creata una dimensione VM Standard_A1 nell'area Stati Uniti orientali hello.</span><span class="sxs-lookup"><span data-stu-id="a1367-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="a1367-201">Per altre opzioni del comando, eseguire `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="a1367-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1367-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1367-202">Next steps</span></span>
<span data-ttu-id="a1367-203">toomanage le macchine virtuali con hello CLI, vedere attività hello [distribuire e gestire macchine virtuali utilizzando modelli di gestione risorse di Azure e hello Azure CLI](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="a1367-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

