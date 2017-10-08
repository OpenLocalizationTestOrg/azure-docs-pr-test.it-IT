---
title: infrastruttura di base di aaaCreate in Azure utilizzando Terraform | Documenti Microsoft
description: Informazioni su come toocreate Azure le risorse tramite Terraform
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="001aa-103">Creare un'infrastruttura di base in Azure usando Terraform</span><span class="sxs-lookup"><span data-stu-id="001aa-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="001aa-104">Questo articolo descrive i passaggi di hello tootake tooprovision una macchina virtuale, con l'infrastruttura sottostante, è necessario in Azure.</span><span class="sxs-lookup"><span data-stu-id="001aa-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="001aa-105">Si apprenderà come toowrite Terraform script e come toovisualize hello cambia prima di renderli nell'infrastruttura cloud.</span><span class="sxs-lookup"><span data-stu-id="001aa-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="001aa-106">È inoltre verrà illustrato come infrastruttura toocreate in Azure utilizzando Terraform.</span><span class="sxs-lookup"><span data-stu-id="001aa-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="001aa-107">tooget avviato, creare un file denominato \terraform_azure101.tf nell'editor di testo di scelta (Visual Studio codice/Sublime/Vim/ecc.).</span><span class="sxs-lookup"><span data-stu-id="001aa-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="001aa-108">nome esatto di Hello del file hello non è importante perché Terraform accetta un parametro di nome di cartella hello: tutti gli script nella cartella hello venga eseguiti.</span><span class="sxs-lookup"><span data-stu-id="001aa-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="001aa-109">Incollare hello seguente codice nel nuovo file hello:</span><span class="sxs-lookup"><span data-stu-id="001aa-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="001aa-110">In hello `provider` sezione di hello script, si indicano Terraform toouse le risorse tooprovision un provider di Azure nello script hello.</span><span class="sxs-lookup"><span data-stu-id="001aa-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="001aa-111">i valori tooget per subscription_id, appId, password e tenant_id, vedere hello [installare e configurare Terraform](terraform-install-configure.md) Guida.</span><span class="sxs-lookup"><span data-stu-id="001aa-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="001aa-112">Se le variabili di ambiente per i valori hello è stato creato in questo blocco, non è necessario tooinclude è.</span><span class="sxs-lookup"><span data-stu-id="001aa-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="001aa-113">Hello `azurerm_resource_group` risorsa indica Terraform toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="001aa-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="001aa-114">Altri tipi di risorse disponibili in Terraform sono elencati più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="001aa-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="001aa-115">Eseguire lo script hello</span><span class="sxs-lookup"><span data-stu-id="001aa-115">Execute hello script</span></span>
<span data-ttu-id="001aa-116">Dopo aver salvato script hello, uscire dalla riga di comando o della console toohello e digitare hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="001aa-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="001aa-117">provider di Terraform tooinitialize per Azure.</span><span class="sxs-lookup"><span data-stu-id="001aa-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="001aa-118">Quindi digitare hello segue:</span><span class="sxs-lookup"><span data-stu-id="001aa-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="001aa-119">Si presuppone che `terraformscripts` hello cartella in cui è stato salvato script hello.</span><span class="sxs-lookup"><span data-stu-id="001aa-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="001aa-120">È stato usato hello `plan` Terraform comando, che esamina le risorse di hello definite negli script hello.</span><span class="sxs-lookup"><span data-stu-id="001aa-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="001aa-121">Confronta le informazioni di stato toohello salvate da Terraform e quindi output hello esecuzione pianificato _senza_ effettivamente la creazione di risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="001aa-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="001aa-122">Dopo l'esecuzione di comandi precedente hello, dovrebbe essere simile al seguente hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="001aa-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Piano Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="001aa-124">Se tutto sembra corretto, eseguire il provisioning di questo nuovo gruppo di risorse in Azure eseguendo hello seguente:</span><span class="sxs-lookup"><span data-stu-id="001aa-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="001aa-125">Nel portale di Azure hello, vedrai hello nuovo vuoto gruppo di risorse denominato `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="001aa-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="001aa-126">Nella seguente sezione di hello, aggiungere che una macchina virtuale e tutti i hello infrastruttura di supporto per il gruppo di risorse toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="001aa-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="001aa-127">Eseguire il provisioning di una VM Ubuntu con Terraform</span><span class="sxs-lookup"><span data-stu-id="001aa-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="001aa-128">È possibile estendere script Terraform hello che abbiamo creato con i dettagli hello tooprovision necessari una macchina virtuale in esecuzione Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="001aa-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="001aa-129">le risorse Hello viene effettuato il provisioning in hello le sezioni seguenti sono:</span><span class="sxs-lookup"><span data-stu-id="001aa-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="001aa-130">Una rete con una singola subnet</span><span class="sxs-lookup"><span data-stu-id="001aa-130">A network with a single subnet</span></span>
* <span data-ttu-id="001aa-131">Una scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="001aa-131">A network interface card</span></span> 
* <span data-ttu-id="001aa-132">Un account di archiviazione con un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="001aa-132">A storage account with a storage container</span></span>
* <span data-ttu-id="001aa-133">Un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="001aa-133">A public IP</span></span>
* <span data-ttu-id="001aa-134">Una macchina virtuale che utilizza tutte le risorse di precedente hello</span><span class="sxs-lookup"><span data-stu-id="001aa-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="001aa-135">Per una documentazione approfondita per ciascuna delle risorse di Azure Terraform hello, vedere hello [Terraform documentazione](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="001aa-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="001aa-136">versione completa di Hello di hello [script di provisioning](#complete-terraform-script) viene inoltre fornita per comodità.</span><span class="sxs-lookup"><span data-stu-id="001aa-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="001aa-137">Estendere script Terraform hello</span><span class="sxs-lookup"><span data-stu-id="001aa-137">Extend hello Terraform script</span></span>
<span data-ttu-id="001aa-138">Estendere script hello che è stato creato con hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="001aa-138">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="001aa-139">script precedente Hello crea una rete virtuale e una subnet all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="001aa-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="001aa-140">Si noti gruppo risorse toohello riferimento hello che avere già creato tramite "${azurerm_resource_group.helloterraform.name}" nella rete virtuale hello sia la definizione di subnet hello.</span><span class="sxs-lookup"><span data-stu-id="001aa-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}
~~~~
<span data-ttu-id="001aa-141">frammenti di codice script precedente Hello creare un indirizzo IP pubblico e un'interfaccia di rete che fa uso di indirizzo IP pubblico hello creato.</span><span class="sxs-lookup"><span data-stu-id="001aa-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="001aa-142">Si noti hello riferimenti toosubnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="001aa-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="001aa-143">Terraform ha toounderstand intelligenti che hello interfaccia di rete presenta una dipendenza risorse hello toobe tale esigenza creato prima della creazione di hello hello dell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="001aa-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="001aa-144">In questo caso è stato creato un account di archiviazione e in tale account è stato definito un contenitore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="001aa-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="001aa-145">Questo account di archiviazione è in cui vengono archiviati dischi rigidi virtuali (VHD) per la macchina virtuale hello su toobe creato.</span><span class="sxs-lookup"><span data-stu-id="001aa-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="001aa-146">Infine, frammento precedente hello crea una macchina virtuale che utilizza tutte le risorse di hello stato già eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="001aa-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="001aa-147">Sono un account di archiviazione e un contenitore per un disco rigido virtuale, un'interfaccia di rete con subnet specificato e un IP pubblico e il gruppo di risorse hello già stato creato.</span><span class="sxs-lookup"><span data-stu-id="001aa-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="001aa-148">Si noti proprietà vm_size hello, in cui viene specificata una SKU A0 Azure script hello.</span><span class="sxs-lookup"><span data-stu-id="001aa-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="001aa-149">Eseguire lo script hello</span><span class="sxs-lookup"><span data-stu-id="001aa-149">Execute hello script</span></span>
<span data-ttu-id="001aa-150">Script completo hello salvato, uscire dalla riga di comando o della console toohello e digitare hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="001aa-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="001aa-151">In un secondo momento, le risorse di hello, tra cui una macchina virtuale, vengono visualizzate in hello `terraformtest` gruppo di risorse in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="001aa-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="001aa-152">Completare lo script Terraform</span><span class="sxs-lookup"><span data-stu-id="001aa-152">Complete Terraform script</span></span>

<span data-ttu-id="001aa-153">Per praticità, di seguito è hello completo Terraform script che esegue il provisioning dell'infrastruttura di hello descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="001aa-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="001aa-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="001aa-154">Next steps</span></span>
<span data-ttu-id="001aa-155">È stata creata un'infrastruttura di base in Azure usando Terraform.</span><span class="sxs-lookup"><span data-stu-id="001aa-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="001aa-156">Per scenari più complessi, inclusi esempi d'uso di servizi di bilanciamento del carico e set di scalabilità delle macchine virtuali, vedere i numerosi [esempi di Terraform per Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="001aa-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="001aa-157">Per un elenco aggiornato dei provider di Azure supportati, vedere hello [Terraform documentazione](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="001aa-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
