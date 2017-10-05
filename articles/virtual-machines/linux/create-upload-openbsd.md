---
title: Creare e caricare un'immagine di VM OpenBSD in Azure | Microsoft Docs
description: Informazioni su come creare e caricare un disco rigido virtuale (VHD) che contiene il sistema operativo OpenBSD per creare una macchina virtuale di Azure tramite l'interfaccia della riga di comando di Azure
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
ms.openlocfilehash: 716c07f6a738189d6cf2b3caafa16b753927d182
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-to-azure"></a><span data-ttu-id="a8d54-103">Creare e caricare un'immagine disco OpenBSD in Azure</span><span class="sxs-lookup"><span data-stu-id="a8d54-103">Create and Upload an OpenBSD disk image to Azure</span></span>
<span data-ttu-id="a8d54-104">Questo articolo descrive come creare e caricare un disco rigido virtuale (VHD) che contiene il sistema operativo OpenBSD.</span><span class="sxs-lookup"><span data-stu-id="a8d54-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the OpenBSD operating system.</span></span> <span data-ttu-id="a8d54-105">Dopo il caricamento, è possibile usarlo come immagine personalizzata per creare una macchina virtuale in Azure tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d54-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a8d54-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8d54-106">Prerequisites</span></span>
<span data-ttu-id="a8d54-107">In questo articolo si presuppone che l'utente disponga degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8d54-107">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="a8d54-108">**Una sottoscrizione Azure**: se non è già disponibile un account, è possibile crearne uno in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a8d54-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="a8d54-109">Se si ha un abbonamento a MSDN, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="a8d54-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="a8d54-110">Altrimenti, vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8d54-110">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="a8d54-111">**Interfaccia della riga di comando di Azure 2.0**: assicurarsi di avere installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli) e di aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a8d54-111">**Azure CLI 2.0** - Make sure you have the latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in to your Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="a8d54-112">**Sistema operativo OpenBSD installato in un file VHD**: è necessario installare un sistema operativo OpenBSD supportato (versione 6.1) in un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="a8d54-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed to a virtual hard disk.</span></span> <span data-ttu-id="a8d54-113">Sono disponibili vari strumenti per la creazione di file VHD.</span><span class="sxs-lookup"><span data-stu-id="a8d54-113">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="a8d54-114">Ad esempio, per creare il file VHD e installare il sistema operativo, è possibile usare soluzioni di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a8d54-114">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="a8d54-115">Per istruzioni, vedere su come installare e usare Hyper-V, vedere [Installare Hyper-V e creare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d54-115">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="a8d54-116">Preparare l'immagine OpenBSD per Azure</span><span class="sxs-lookup"><span data-stu-id="a8d54-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="a8d54-117">Nella macchina virtuale in cui è stato installato il sistema operativo OpenBSD 6.1 con l'aggiunta del supporto Hyper-V, completare le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8d54-117">On the VM where you installed the OpenBSD operating system 6.1, which added Hyper-V support, complete the following procedures:</span></span>

1. <span data-ttu-id="a8d54-118">Se DHCP non è stato abilitato durante l'installazione, abilitare il servizio come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-118">If DHCP is not enabled during installation, enable the service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="a8d54-119">Configurare una console seriale come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="a8d54-120">Configurare l'installazione del pacchetto come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="a8d54-121">Per impostazione predefinita, l'utente `root` è disabilitato nelle macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d54-121">By default, the `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="a8d54-122">Gli utenti possono eseguire comandi con privilegi elevati usando il comando `doas` nella VM OpenBSD.</span><span class="sxs-lookup"><span data-stu-id="a8d54-122">Users can run commands with elevated privileges by using the `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="a8d54-123">Doas è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a8d54-123">Doas is enabled by default.</span></span> <span data-ttu-id="a8d54-124">Per altre informazioni, vedere [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="a8d54-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="a8d54-125">Installare e configurare i prerequisiti per l'agente di Azure come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-125">Install and configure prerequisites for the Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="a8d54-126">La versione più recente dell'agente di Azure è sempre disponibile in [GitHub](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="a8d54-126">The latest release of the Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="a8d54-127">Installare l'agente come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-127">Install the agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="a8d54-128">Dopo aver installato l'agente di Azure, è consigliabile verificare che sia in esecuzione come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-128">After you install Azure Agent, it's a good idea to verify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="a8d54-129">Eseguire il deprovisioning del sistema per pulire il sistema e renderlo idoneo per un nuovo provisioning.</span><span class="sxs-lookup"><span data-stu-id="a8d54-129">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="a8d54-130">Il comando seguente elimina anche l'ultimo account utente di cui è stato effettuato il provisioning e i dati associati:</span><span class="sxs-lookup"><span data-stu-id="a8d54-130">The following command also deletes the last provisioned user account and the associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="a8d54-131">Ora è possibile arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a8d54-131">Now you can shut down your VM.</span></span>


## <a name="prepare-the-vhd"></a><span data-ttu-id="a8d54-132">Preparare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="a8d54-132">Prepare the VHD</span></span>
<span data-ttu-id="a8d54-133">Il formato VHDX non è supportato in Azure, solo nei **VHD fissi**.</span><span class="sxs-lookup"><span data-stu-id="a8d54-133">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="a8d54-134">È possibile convertire il disco in formato VHD fisso tramite la console di gestione di Hyper-V o il cmdlet [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8d54-134">You can convert the disk to fixed VHD format using Hyper-V Manager or the Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="a8d54-135">Di seguito è riportato un esempio.</span><span class="sxs-lookup"><span data-stu-id="a8d54-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="a8d54-136">Creare e caricare risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a8d54-136">Create storage resources and upload</span></span>
<span data-ttu-id="a8d54-137">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a8d54-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a8d54-138">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="a8d54-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a8d54-139">Per caricare il disco rigido virtuale, creare un account di archiviazione con il comando [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="a8d54-139">To upload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="a8d54-140">Il nome dell'account di archiviazione deve essere univoco; assegnare quindi all'account il proprio nome.</span><span class="sxs-lookup"><span data-stu-id="a8d54-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="a8d54-141">L'esempio seguente crea un account di archiviazione denominato *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="a8d54-141">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="a8d54-142">Per controllare l'accesso all'account di archiviazione, ottenere la chiave di archiviazione con [az storage account keys list](/cli/azure/storage/account/keys#list) come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-142">To control access to the storage account, obtain the storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="a8d54-143">Per separare in modo logico i dischi rigidi virtuali caricati, creare un contenitore nell'account di archiviazione con [az storage container create](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="a8d54-143">To logically separate the VHDs you upload, create a container within the storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="a8d54-144">Caricare infine il disco rigido virtuale con [az storage blob upload](/cli/azure/storage/blob#upload) come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="a8d54-145">Creare una macchina virtuale dal disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="a8d54-145">Create VM from your VHD</span></span>
<span data-ttu-id="a8d54-146">È possibile creare una macchina virtuale con un [script di esempio](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) o direttamente con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a8d54-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a8d54-147">Per specificare il disco rigido virtuale OpenBSD caricato, usare il parametro `--image` come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-147">To specify the OpenBSD VHD you uploaded, use the `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="a8d54-148">Ottenere l'indirizzo IP per la VM OpenBSD con [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) come segue:</span><span class="sxs-lookup"><span data-stu-id="a8d54-148">Obtain the IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="a8d54-149">Ora è possibile connettersi alla VM OpenBSD tramite SSH nel modo usuale:</span><span class="sxs-lookup"><span data-stu-id="a8d54-149">Now you can SSH to your OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="a8d54-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8d54-150">Next steps</span></span>
<span data-ttu-id="a8d54-151">Per altre informazioni sul supporto di Hyper-V in OpenBSD 6.1, vedere [OpenBSD 6.1](https://www.openbsd.org/61.html) e [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="a8d54-151">If you want to know more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="a8d54-152">Per creare una macchina virtuale dal disco gestito, vedere [az disk](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="a8d54-152">If you want to create a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 