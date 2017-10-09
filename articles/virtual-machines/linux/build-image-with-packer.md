---
title: aaaHow toocreate immagini di macchina virtuale Linux Azure con chi | Documenti Microsoft
description: Informazioni su come le immagini di toocreate chi toouse delle macchine virtuali Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="d1958-103">Come le immagini di macchina virtuale Linux di toouse chi toocreate in Azure</span><span class="sxs-lookup"><span data-stu-id="d1958-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="d1958-104">Ogni macchina virtuale (VM) in Azure viene creato da un'immagine che definisce hello di Linux e versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d1958-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="d1958-105">Le immagini possono includere applicazioni e configurazioni preinstallate.</span><span class="sxs-lookup"><span data-stu-id="d1958-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="d1958-106">Hello Azure Marketplace fornisce molte immagini prima e di terze parti per le distribuzioni più comuni e di ambienti applicazione oppure è possibile creare le proprie esigenze tooyour immagini personalizzate personalizzate.</span><span class="sxs-lookup"><span data-stu-id="d1958-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="d1958-107">In questo articolo illustra in dettaglio come hello toouse aprire lo strumento di origine [chi](https://www.packer.io/) toodefine e compilazione immagini personalizzate in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1958-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="d1958-108">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="d1958-108">Create Azure resource group</span></span>
<span data-ttu-id="d1958-109">Durante il processo di compilazione hello, chi crea risorse di Azure temporanee durante la compilazione di macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="d1958-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="d1958-110">toocapture che VM di origine per l'utilizzo come un'immagine, è necessario definire un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d1958-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="d1958-111">l'output dal processo di compilazione chi hello Hello viene archiviato in questo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d1958-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="d1958-112">Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d1958-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d1958-113">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="d1958-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="d1958-114">Creare credenziali di Azure</span><span class="sxs-lookup"><span data-stu-id="d1958-114">Create Azure credentials</span></span>
<span data-ttu-id="d1958-115">Per eseguire l'autenticazione con Azure, Packer usa un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d1958-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="d1958-116">Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Packer.</span><span class="sxs-lookup"><span data-stu-id="d1958-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="d1958-117">È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1958-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="d1958-118">Creare un servizio principale con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac) e le credenziali di hello output che chi deve:</span><span class="sxs-lookup"><span data-stu-id="d1958-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="d1958-119">Un esempio di output di hello da hello precedenti comandi è la seguente:</span><span class="sxs-lookup"><span data-stu-id="d1958-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="d1958-120">tooAzure tooauthenticate, è necessario anche con l'ID sottoscrizione Azure tooobtain [mostra account az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="d1958-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="d1958-121">Utilizzare l'output di hello di questi due comandi nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="d1958-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="d1958-122">Definire un modello di Packer</span><span class="sxs-lookup"><span data-stu-id="d1958-122">Define Packer template</span></span>
<span data-ttu-id="d1958-123">immagini toobuild, si crea un modello come un file JSON.</span><span class="sxs-lookup"><span data-stu-id="d1958-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="d1958-124">Nel modello hello definisce generatori e provisioners per l'esecuzione di hello effettivo processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="d1958-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="d1958-125">Chi ha un [strumento di provisioning per Azure](https://www.packer.io/docs/builders/azure.html) che consentono di toodefine Azure risorse, ad esempio credenziali dell'entità servizio hello create nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d1958-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="d1958-126">Creare un file denominato *ubuntu.json* e Incolla hello seguendo il contenuto.</span><span class="sxs-lookup"><span data-stu-id="d1958-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="d1958-127">Immettere i valori per i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d1958-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="d1958-128">.</span><span class="sxs-lookup"><span data-stu-id="d1958-128">Parameter</span></span>                           | <span data-ttu-id="d1958-129">Dove tooobtain</span><span class="sxs-lookup"><span data-stu-id="d1958-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="d1958-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="d1958-130">*client_id*</span></span>                         | <span data-ttu-id="d1958-131">Prima riga di output da `az ad sp` create command - *appId*</span><span class="sxs-lookup"><span data-stu-id="d1958-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="d1958-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="d1958-132">*client_secret*</span></span>                     | <span data-ttu-id="d1958-133">Seconda riga di output da `az ad sp` create command - *password*</span><span class="sxs-lookup"><span data-stu-id="d1958-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="d1958-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="d1958-134">*tenant_id*</span></span>                         | <span data-ttu-id="d1958-135">Terza riga di output da `az ad sp` create command - *tenant*</span><span class="sxs-lookup"><span data-stu-id="d1958-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="d1958-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="d1958-136">*subscription_id*</span></span>                   | <span data-ttu-id="d1958-137">Output del comando `az account show`</span><span class="sxs-lookup"><span data-stu-id="d1958-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="d1958-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="d1958-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="d1958-139">Nome del gruppo di risorse creato nel primo passaggio hello</span><span class="sxs-lookup"><span data-stu-id="d1958-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="d1958-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="d1958-140">*managed_image_name*</span></span>                | <span data-ttu-id="d1958-141">Nome dell'immagine di disco gestito hello creato</span><span class="sxs-lookup"><span data-stu-id="d1958-141">Name for hello managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="d1958-142">Questo modello crea un'immagine Ubuntu 16.04 LTS, installa NGINX e annullamento del provisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1958-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="d1958-143">Se si espande credenziali dell'utente tooprovision questo modello, modificare il comando di provisioning hello che l'annullamento del provisioning hello Azure agente tooread `-deprovision` anziché `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="d1958-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="d1958-144">Hello `+user` flag rimuove tutti gli account utente dalla macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="d1958-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="d1958-145">Compilare l'immagine in Packer</span><span class="sxs-lookup"><span data-stu-id="d1958-145">Build Packer image</span></span>
<span data-ttu-id="d1958-146">Se non si dispone già installati nel computer locale, chi [seguire le istruzioni di installazione di hello chi](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="d1958-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="d1958-147">Creare immagini hello specificando il chi file modello nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="d1958-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="d1958-148">Un esempio di output di hello da hello precedenti comandi è la seguente:</span><span class="sxs-lookup"><span data-stu-id="d1958-148">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="d1958-149">Creare una macchina virtuale da un'immagine di Azure</span><span class="sxs-lookup"><span data-stu-id="d1958-149">Create VM from Azure Image</span></span>
<span data-ttu-id="d1958-150">È ora possibile creare una macchina virtuale dall'immagine con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d1958-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d1958-151">Specificare l'immagine è stato creato con hello hello `--image` parametro.</span><span class="sxs-lookup"><span data-stu-id="d1958-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="d1958-152">esempio Hello crea una macchina virtuale denominata *myVM* da *myPackerImage* e genera le chiavi SSH se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="d1958-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="d1958-153">Sono necessari alcuni minuti toocreate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1958-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="d1958-154">Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1958-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="d1958-155">Questo indirizzo è sito NGINX di hello tooaccess usato tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="d1958-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="d1958-156">tooallow web tooreach traffico la macchina virtuale, aprire la porta 80 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="d1958-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="d1958-157">Testare la macchina virtuale e NGINX</span><span class="sxs-lookup"><span data-stu-id="d1958-157">Test VM and NGINX</span></span>
<span data-ttu-id="d1958-158">È ora possibile aprire un web browser e immettere `http://publicIpAddress` nella barra degli indirizzi hello.</span><span class="sxs-lookup"><span data-stu-id="d1958-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="d1958-159">Fornire la propria pubblico indirizzo IP da hello VM creare il processo.</span><span class="sxs-lookup"><span data-stu-id="d1958-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="d1958-160">verrà visualizzata la pagina NGINX di Hello predefinito come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d1958-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Sito NGINX predefinito](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="d1958-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1958-162">Next steps</span></span>
<span data-ttu-id="d1958-163">In questo esempio, chi toocreate un'immagine di macchina virtuale è usato con NGINX già installato.</span><span class="sxs-lookup"><span data-stu-id="d1958-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="d1958-164">È possibile utilizzare questa immagine di macchina virtuale insieme a distribuzione flussi di lavoro esistenti, ad esempio toodeploy tooVMs l'app creata da hello immagine con Ansible, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="d1958-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="d1958-165">Per altri modelli di Packer di esempio per distribuzioni di Linux di altro tipo, vedere [questo repository di GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="d1958-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>