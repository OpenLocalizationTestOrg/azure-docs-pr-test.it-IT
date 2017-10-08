---
title: aaaCreate e caricamento di una VM OpenBSD immagine tooAzure | Documenti Microsoft
description: Informazioni su come toocreate e caricare un disco rigido virtuale (VHD) che contiene hello OpenBSD del sistema operativo toocreate una macchina virtuale di Azure mediante Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="7f8d4-103">Creare e caricare un tooAzure di immagine disco OpenBSD</span><span class="sxs-lookup"><span data-stu-id="7f8d4-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="7f8d4-104">Questo articolo illustra come toocreate e caricare un disco rigido virtuale (VHD) che contiene hello OpenBSD del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="7f8d4-105">Dopo aver caricato il, è possibile utilizzare, come la propria toocreate immagine una macchina virtuale (VM) in Azure mediante Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7f8d4-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7f8d4-106">Prerequisites</span></span>
<span data-ttu-id="7f8d4-107">Questo articolo si presuppone di aver hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="7f8d4-108">**Una sottoscrizione Azure**: se non è già disponibile un account, è possibile crearne uno in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="7f8d4-109">Se si ha un abbonamento a MSDN, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="7f8d4-110">In caso contrario, informazioni su come troppo[creare un account di prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="7f8d4-111">**Azure CLI 2.0** -assicurarsi di disporre di più recente hello [CLI di Azure 2.0](/cli/azure/install-azure-cli) installato e registrato nel tooyour account Azure con [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="7f8d4-112">**Sistema operativo OpenBSD installato in un file con estensione vhd** -un sistema operativo OpenBSD (6.1 versione) deve essere il disco rigido virtuale di tooa installato.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="7f8d4-113">Più strumenti esistono toocreate file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="7f8d4-114">Ad esempio, è possibile usare una soluzione di virtualizzazione, ad esempio file con estensione vhd di Hyper-V toocreate hello e installare hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="7f8d4-115">Per istruzioni su come tooinstall e utilizzare Hyper-V, vedere [installare Hyper-V e creare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="7f8d4-116">Preparare l'immagine OpenBSD per Azure</span><span class="sxs-lookup"><span data-stu-id="7f8d4-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="7f8d4-117">Nella macchina virtuale in cui è installato hello OpenBSD sistema operativo 6.1, aggiunto il supporto di Hyper-V, hello completare hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="7f8d4-118">Se DHCP non è abilitato durante l'installazione, abilitare il servizio hello come segue:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="7f8d4-119">Configurare una console seriale come segue:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="7f8d4-120">Configurare l'installazione del pacchetto come segue:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="7f8d4-121">Per impostazione predefinita, hello `root` utente è disabilitato nelle macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="7f8d4-122">Gli utenti possono eseguire i comandi con privilegi elevati tramite hello `doas` comando OpenBSD VM.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="7f8d4-123">Doas è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-123">Doas is enabled by default.</span></span> <span data-ttu-id="7f8d4-124">Per altre informazioni, vedere [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="7f8d4-125">Installare e configurare i prerequisiti per l'agente di Azure hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="7f8d4-126">versione più recente di Hello di hello agente di Azure è sempre disponibile nel [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="7f8d4-127">Installare l'agente hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7f8d4-128">Dopo aver installato l'agente di Azure, è un tooverify buona norma che è in esecuzione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="7f8d4-129">Deprovisioning hello tooclean di sistema e verificare che è adatto per la riconfigurazione.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="7f8d4-130">Hello seguente comando Elimina inoltre ultimo account di provisioning utente hello e dati hello associata:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="7f8d4-131">Ora è possibile arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="7f8d4-132">Preparare hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="7f8d4-132">Prepare hello VHD</span></span>
<span data-ttu-id="7f8d4-133">formato VHDX Hello non è supportato solo in Azure, **disco rigido virtuale fisso**.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="7f8d4-134">È possibile convertire formato VHD, hello disco toofixed tramite Hyper-V Manager oppure Powershell hello [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="7f8d4-135">Di seguito è riportato un esempio.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="7f8d4-136">Creare e caricare risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7f8d4-136">Create storage resources and upload</span></span>
<span data-ttu-id="7f8d4-137">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7f8d4-138">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7f8d4-139">tooupload il disco rigido virtuale, creare un account di archiviazione con [creare account di archiviazione az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="7f8d4-140">Il nome dell'account di archiviazione deve essere univoco; assegnare quindi all'account il proprio nome.</span><span class="sxs-lookup"><span data-stu-id="7f8d4-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="7f8d4-141">esempio Hello crea un account di archiviazione denominato *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="7f8d4-142">toocontrol accedere toohello account di archiviazione, ottenere la chiave di archiviazione hello con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="7f8d4-143">hello separato toologically i dischi rigidi virtuali, caricare, creare un contenitore nell'account di archiviazione hello con [creare il contenitore di archiviazione az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="7f8d4-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="7f8d4-144">Caricare infine il disco rigido virtuale con [az storage blob upload](/cli/azure/storage/blob#upload) come segue:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="7f8d4-145">Creare una macchina virtuale dal disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="7f8d4-145">Create VM from your VHD</span></span>
<span data-ttu-id="7f8d4-146">È possibile creare una macchina virtuale con un [script di esempio](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) o direttamente con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7f8d4-147">toospecify hello OpenBSD VHD caricato, utilizzare hello `--image` parametro come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="7f8d4-148">Ottenere l'indirizzo IP hello per le VM OpenBSD con [az vm gli indirizzi ip elenco](/cli/azure/vm#list-ip-addresses) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="7f8d4-149">È ora possibile SSH tooyour OpenBSD VM come di consueto:</span><span class="sxs-lookup"><span data-stu-id="7f8d4-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="7f8d4-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f8d4-150">Next steps</span></span>
<span data-ttu-id="7f8d4-151">Se si desidera ulteriori informazioni su Hyper-V supporta in OpenBSD6.1 tooknow, leggere [OpenBSD 6.1](https://www.openbsd.org/61.html) e [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="7f8d4-152">Se si desidera toocreate una macchina virtuale dal disco gestito, leggere [disco az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="7f8d4-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
