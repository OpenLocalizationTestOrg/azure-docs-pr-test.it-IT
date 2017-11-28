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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="e096a-103">Creare un'infrastruttura di base in Azure usando Terraform</span><span class="sxs-lookup"><span data-stu-id="e096a-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="e096a-104">Questo articolo descrive i passaggi di hello tootake tooprovision una macchina virtuale, con l'infrastruttura sottostante, è necessario in Azure.</span><span class="sxs-lookup"><span data-stu-id="e096a-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="e096a-105">Si apprenderà come toowrite Terraform script e come toovisualize hello cambia prima di renderli nell'infrastruttura cloud.</span><span class="sxs-lookup"><span data-stu-id="e096a-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="e096a-106">È inoltre verrà illustrato come infrastruttura toocreate in Azure utilizzando Terraform.</span><span class="sxs-lookup"><span data-stu-id="e096a-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="e096a-107">tooget avviato, creare un file denominato \terraform_azure101.tf nell'editor di testo di scelta (Visual Studio codice/Sublime/Vim/ecc.).</span><span class="sxs-lookup"><span data-stu-id="e096a-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="e096a-108">nome esatto di Hello del file hello non è importante perché Terraform accetta un parametro di nome di cartella hello: tutti gli script nella cartella hello venga eseguiti.</span><span class="sxs-lookup"><span data-stu-id="e096a-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="e096a-109">Incollare hello seguente codice nel nuovo file hello:</span><span class="sxs-lookup"><span data-stu-id="e096a-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="e096a-110">In hello `provider` sezione di hello script, si indicano Terraform toouse le risorse tooprovision un provider di Azure nello script hello.</span><span class="sxs-lookup"><span data-stu-id="e096a-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="e096a-111">i valori tooget per subscription_id, appId, password e tenant_id, vedere hello [installare e configurare Terraform](terraform-install-configure.md) Guida.</span><span class="sxs-lookup"><span data-stu-id="e096a-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="e096a-112">Se le variabili di ambiente per i valori hello è stato creato in questo blocco, non è necessario tooinclude è.</span><span class="sxs-lookup"><span data-stu-id="e096a-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="e096a-113">Hello `azurerm_resource_group` risorsa indica Terraform toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e096a-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="e096a-114">Altri tipi di risorse disponibili in Terraform sono elencati più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e096a-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="e096a-115">Eseguire lo script hello</span><span class="sxs-lookup"><span data-stu-id="e096a-115">Execute hello script</span></span>
<span data-ttu-id="e096a-116">Dopo aver salvato script hello, uscire dalla riga di comando o della console toohello e digitare hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e096a-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="e096a-117">provider di Terraform tooinitialize hello per Azure.</span><span class="sxs-lookup"><span data-stu-id="e096a-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="e096a-118">Quindi modificare anche le directory hello**terraformscripts**, e hello problema comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e096a-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="e096a-119">È stato usato hello `plan` Terraform comando, che esamina le risorse di hello definite negli script hello.</span><span class="sxs-lookup"><span data-stu-id="e096a-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="e096a-120">Confronta le informazioni di stato toohello salvate da Terraform e quindi output hello esecuzione pianificato _senza_ effettivamente la creazione di risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="e096a-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="e096a-121">Dopo l'esecuzione di comandi precedente hello, dovrebbe essere simile al seguente hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="e096a-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Piano Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="e096a-123">Se tutto sembra corretto, eseguire il provisioning di questo nuovo gruppo di risorse in Azure eseguendo hello seguente:</span><span class="sxs-lookup"><span data-stu-id="e096a-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="e096a-124">Nel portale di Azure hello, vedrai hello nuovo vuoto gruppo di risorse denominato `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="e096a-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="e096a-125">Nella seguente sezione di hello, aggiungere che una macchina virtuale e tutti i hello infrastruttura di supporto per il gruppo di risorse toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e096a-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="e096a-126">Eseguire il provisioning di una VM Ubuntu con Terraform</span><span class="sxs-lookup"><span data-stu-id="e096a-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="e096a-127">È possibile estendere script Terraform hello che abbiamo creato con i dettagli hello tooprovision necessari una macchina virtuale in esecuzione Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e096a-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="e096a-128">le risorse Hello viene effettuato il provisioning in hello le sezioni seguenti sono:</span><span class="sxs-lookup"><span data-stu-id="e096a-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="e096a-129">Una rete con una singola subnet</span><span class="sxs-lookup"><span data-stu-id="e096a-129">A network with a single subnet</span></span>
* <span data-ttu-id="e096a-130">Una scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="e096a-130">A network interface card</span></span> 
* <span data-ttu-id="e096a-131">Un account di archiviazione per diagnostica della macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="e096a-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="e096a-132">Un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="e096a-132">A public IP</span></span>
* <span data-ttu-id="e096a-133">Una macchina virtuale che utilizza tutte le risorse di precedente hello</span><span class="sxs-lookup"><span data-stu-id="e096a-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="e096a-134">Per una documentazione approfondita per ciascuna delle risorse di Azure Terraform hello, vedere hello [Terraform documentazione](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="e096a-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="e096a-135">versione completa di Hello di hello [script di provisioning](#complete-terraform-script) viene inoltre fornita per comodità.</span><span class="sxs-lookup"><span data-stu-id="e096a-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="e096a-136">Estendere script Terraform hello</span><span class="sxs-lookup"><span data-stu-id="e096a-136">Extend hello Terraform script</span></span>
<span data-ttu-id="e096a-137">Estendere script hello che è stato creato con hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="e096a-137">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="e096a-138">script precedente Hello crea una rete virtuale e una subnet all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e096a-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="e096a-139">Si noti gruppo risorse toohello riferimento hello che avere già creato tramite "${azurerm_resource_group.helloterraform.name}" nella rete virtuale hello sia la definizione di subnet hello.</span><span class="sxs-lookup"><span data-stu-id="e096a-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="e096a-140">frammenti di codice script precedente Hello creare un indirizzo IP pubblico e un'interfaccia di rete che fa uso di indirizzo IP pubblico hello creato.</span><span class="sxs-lookup"><span data-stu-id="e096a-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="e096a-141">Si noti hello riferimenti toosubnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="e096a-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="e096a-142">Terraform ha toounderstand intelligenti che hello interfaccia di rete presenta una dipendenza risorse hello toobe tale esigenza creato prima della creazione di hello hello dell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="e096a-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="e096a-143">Qui viene creato un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e096a-143">Here, you created a storage account.</span></span> <span data-ttu-id="e096a-144">Questo account di archiviazione è in macchina virtuale hello verranno archiviati i dettagli di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="e096a-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="e096a-145">Infine, frammento precedente hello crea una macchina virtuale che utilizza tutte le risorse di hello stato già eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="e096a-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="e096a-146">Sono un account di archiviazione per diagnostica della macchina virtuale hello, un'interfaccia di rete con subnet specificato e un IP pubblico e il gruppo di risorse hello già stato creato.</span><span class="sxs-lookup"><span data-stu-id="e096a-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="e096a-147">Si noti proprietà vm_size hello, in cui viene specificata una SKU di Azure Standard DS1v2 script hello.</span><span class="sxs-lookup"><span data-stu-id="e096a-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="e096a-148">È necessario toosupply una chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="e096a-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="e096a-149">Inserire il valore di chiave pubblica di hello sezione hello **... INSERT OPENSSH PUBLIC KEY HERE ...**, visualizzata nell'esempio di codice precedente.</span><span class="sxs-lookup"><span data-stu-id="e096a-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="e096a-150">È possibile utilizzare un oggetto esistente ssh coppia di chiavi o seguire hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) o [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentazione toogenerate hello coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="e096a-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="e096a-151">Eseguire lo script hello</span><span class="sxs-lookup"><span data-stu-id="e096a-151">Execute hello script</span></span>
<span data-ttu-id="e096a-152">Script completo hello salvato, uscire dalla riga di comando o della console toohello e digitare hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e096a-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="e096a-153">In un secondo momento, le risorse di hello, tra cui una macchina virtuale, vengono visualizzate in hello `terraformtest` gruppo di risorse in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e096a-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="e096a-154">Completare lo script Terraform</span><span class="sxs-lookup"><span data-stu-id="e096a-154">Complete Terraform script</span></span>

<span data-ttu-id="e096a-155">Per praticità, di seguito è hello completo Terraform script che esegue il provisioning dell'infrastruttura di hello descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e096a-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
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

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="e096a-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e096a-156">Next steps</span></span>
<span data-ttu-id="e096a-157">È stata creata un'infrastruttura di base in Azure usando Terraform.</span><span class="sxs-lookup"><span data-stu-id="e096a-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="e096a-158">Per scenari più complessi, inclusi esempi d'uso di servizi di bilanciamento del carico e set di scalabilità delle macchine virtuali, vedere i numerosi [esempi di Terraform per Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="e096a-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="e096a-159">Per un elenco aggiornato dei provider di Azure supportati, vedere hello [Terraform documentazione](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="e096a-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
