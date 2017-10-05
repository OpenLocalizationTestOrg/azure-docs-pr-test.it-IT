---
title: Creare un'infrastruttura di base in Azure usando Terraform | Microsoft Docs
description: Informazioni su come creare risorse di Azure usando Terraform
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
ms.openlocfilehash: aa0926de32dd85f4460bbfa84b7a6007e2199d51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="c4975-103">Creare un'infrastruttura di base in Azure usando Terraform</span><span class="sxs-lookup"><span data-stu-id="c4975-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="c4975-104">Questo articolo illustra i passaggi necessari per eseguire il provisioning di una macchina virtuale in Azure e descrive l'infrastruttura sottostante.</span><span class="sxs-lookup"><span data-stu-id="c4975-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="c4975-105">Spiega come creare script Terraform e come visualizzare le modifiche prima di implementarle nell'infrastruttura cloud.</span><span class="sxs-lookup"><span data-stu-id="c4975-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="c4975-106">Spiega anche come creare l'infrastruttura in Azure usando Terraform.</span><span class="sxs-lookup"><span data-stu-id="c4975-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="c4975-107">Per iniziare, nell'editor di testo desiderato (Visual Studio Code/Sublime/Vim/e così via) creare il file \terraform_azure101.tf.</span><span class="sxs-lookup"><span data-stu-id="c4975-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="c4975-108">Il nome esatto del file non è importante, perché Terraform accetta come parametro il nome della cartella e vengono eseguiti tutti gli script presenti nella cartella.</span><span class="sxs-lookup"><span data-stu-id="c4975-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="c4975-109">Incollare il codice seguente nel nuovo file:</span><span class="sxs-lookup"><span data-stu-id="c4975-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
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
<span data-ttu-id="c4975-110">Nella sezione `provider` dello script si indica a Terraform di usare un provider di Azure per eseguire il provisioning delle risorse nello script.</span><span class="sxs-lookup"><span data-stu-id="c4975-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="c4975-111">Per ottenere i valori per subscription_id, appId, password e tenant_id, vedere [Installare e configurare Terraform per eseguire il provisioning di macchine virtuali e altra infrastruttura in Azure](terraform-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c4975-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="c4975-112">Se sono state create variabili di ambiente per i valori in questo blocco, non è necessario includere il blocco.</span><span class="sxs-lookup"><span data-stu-id="c4975-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="c4975-113">La risorsa `azurerm_resource_group` indica a Terraform di creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c4975-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="c4975-114">Altri tipi di risorse disponibili in Terraform sono elencati più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c4975-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="c4975-115">Eseguire lo script</span><span class="sxs-lookup"><span data-stu-id="c4975-115">Execute the script</span></span>
<span data-ttu-id="c4975-116">Dopo avere salvato lo script passare alla console o alla riga di comando e digitare:</span><span class="sxs-lookup"><span data-stu-id="c4975-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
 <span data-ttu-id="c4975-117">per inizializzare il provider di Terraform per Azure.</span><span class="sxs-lookup"><span data-stu-id="c4975-117">to initialize the Terraform provider for Azure.</span></span> <span data-ttu-id="c4975-118">Quindi passare alla directory **terraformscripts**e digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c4975-118">Then change the directory to **terraformscripts**, and issue the following command:</span></span>
```
terraform plan
```
<span data-ttu-id="c4975-119">È stato usato il comando Terraform `plan`, che esamina le risorse definite negli script.</span><span class="sxs-lookup"><span data-stu-id="c4975-119">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="c4975-120">Il comando confronta le risorse con le informazioni sullo stato salvate da Terraform e restituisce l'esecuzione pianificata _senza_ creare di fatto risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4975-120">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="c4975-121">Dopo l'esecuzione del comando viene visualizzata una schermata simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="c4975-121">After you execute the previous command, you should see something like the following screen:</span></span>

![Piano Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="c4975-123">Se tutti i dati sono corretti effettuare il provisioning di questo nuovo gruppo di risorse in Azure eseguendo quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c4975-123">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply
```
<span data-ttu-id="c4975-124">Nel portale di Azure viene visualizzato un nuovo gruppo di risorse vuoto con nome `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="c4975-124">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="c4975-125">Nella sezione seguente si aggiunge una VM e l'infrastruttura di supporto al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c4975-125">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="c4975-126">Eseguire il provisioning di una VM Ubuntu con Terraform</span><span class="sxs-lookup"><span data-stu-id="c4975-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="c4975-127">È possibile estendere lo script di Terraform creato in precedenza con i dettagli necessari per il provisioning di una macchina virtuale che esegue Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c4975-127">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="c4975-128">Le risorse di cui viene effettuato il provisioning nelle sezioni seguenti sono:</span><span class="sxs-lookup"><span data-stu-id="c4975-128">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="c4975-129">Una rete con una singola subnet</span><span class="sxs-lookup"><span data-stu-id="c4975-129">A network with a single subnet</span></span>
* <span data-ttu-id="c4975-130">Una scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="c4975-130">A network interface card</span></span> 
* <span data-ttu-id="c4975-131">Un account di archiviazione per la diagnostica della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c4975-131">A storage account for the virtual machine diagnostics</span></span>
* <span data-ttu-id="c4975-132">Un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="c4975-132">A public IP</span></span>
* <span data-ttu-id="c4975-133">Una macchina virtuale che usa tutte le risorse precedenti</span><span class="sxs-lookup"><span data-stu-id="c4975-133">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="c4975-134">Per informazioni approfondite sulle singole risorse di Azure Terraform, vedere la [documentazione di Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c4975-134">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="c4975-135">Per comodità viene fornita anche la versione completa dello [script di provisioning](#complete-terraform-script).</span><span class="sxs-lookup"><span data-stu-id="c4975-135">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="c4975-136">Estendere lo script Terraform</span><span class="sxs-lookup"><span data-stu-id="c4975-136">Extend the Terraform script</span></span>
<span data-ttu-id="c4975-137">Estendere lo script creato in precedenza con le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4975-137">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="c4975-138">Lo script precedente crea una rete virtuale e una subnet al suo interno.</span><span class="sxs-lookup"><span data-stu-id="c4975-138">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="c4975-139">Si noti il riferimento al gruppo di risorse già creato tramite "${azurerm_resource_group.helloterraform.name}" sia nella definizione della rete virtuale che nella definizione della subnet.</span><span class="sxs-lookup"><span data-stu-id="c4975-139">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="c4975-140">I frammenti di script precedenti creano un indirizzo IP pubblico e un'interfaccia di rete che usa l'indirizzo IP pubblico creato.</span><span class="sxs-lookup"><span data-stu-id="c4975-140">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="c4975-141">Tenere presenti i riferimenti a subnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="c4975-141">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="c4975-142">L'intelligence integrata di Terraform rileva che l'interfaccia di rete presenta una dipendenza dalle risorse che vanno create prima della creazione dell'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c4975-142">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="c4975-143">Qui viene creato un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c4975-143">Here, you created a storage account.</span></span> <span data-ttu-id="c4975-144">L'account di archiviazione è il punto in cui la macchina virtuale archivia i propri dettagli di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c4975-144">This storage account is where the virtual machine will store its diagnostics details.</span></span>

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
<span data-ttu-id="c4975-145">Infine il frammento precedente crea una macchina virtuale che usa tutte le risorse già specificate.</span><span class="sxs-lookup"><span data-stu-id="c4975-145">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="c4975-146">Si tratta di un account di archiviazione per la diagnostica della macchina virtuale, un'interfaccia di rete con subnet e indirizzo IP pubblico specificati e il gruppo di risorse già creato.</span><span class="sxs-lookup"><span data-stu-id="c4975-146">They are a storage account for the virtual machine diagnostics, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="c4975-147">Si noti la proprietà vm_size, in cui lo script specifica uno SKU DS1v2 Standard di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4975-147">Note the vm_size property, where the script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="c4975-148">È necessario fornire una chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="c4975-148">You are required to supply an SSH public key.</span></span> <span data-ttu-id="c4975-149">Inserire il valore di chiave pubblica nella sezione **... INSERT OPENSSH PUBLIC KEY HERE ...**, visualizzata nell'esempio di codice precedente.</span><span class="sxs-lookup"><span data-stu-id="c4975-149">Place the public key value into the section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="c4975-150">È possibile usare una coppia di chiavi SSH esistente o seguire la documentazione per [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) o [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) per generare la coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="c4975-150">You can use an existing ssh key pair or follow the [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation to generate the key pair.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="c4975-151">Eseguire lo script</span><span class="sxs-lookup"><span data-stu-id="c4975-151">Execute the script</span></span>
<span data-ttu-id="c4975-152">Dopo aver salvato l'intero script chiudere la riga di comando o la console e digitare:</span><span class="sxs-lookup"><span data-stu-id="c4975-152">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply
```
<span data-ttu-id="c4975-153">Dopo qualche istante le risorse, compresa la VM, appaiono nel gruppo di risorse `terraformtest` nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4975-153">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="c4975-154">Completare lo script Terraform</span><span class="sxs-lookup"><span data-stu-id="c4975-154">Complete Terraform script</span></span>

<span data-ttu-id="c4975-155">Per praticità, di seguito è riportato lo script Terraform completo che esegue il provisioning dell'intera infrastruttura descritta in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c4975-155">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
# Configure the Microsoft Azure Provider
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

## <a name="next-steps"></a><span data-ttu-id="c4975-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4975-156">Next steps</span></span>
<span data-ttu-id="c4975-157">È stata creata un'infrastruttura di base in Azure usando Terraform.</span><span class="sxs-lookup"><span data-stu-id="c4975-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="c4975-158">Per scenari più complessi, inclusi esempi d'uso di servizi di bilanciamento del carico e set di scalabilità delle macchine virtuali, vedere i numerosi [esempi di Terraform per Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="c4975-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="c4975-159">La [documentazione di Terraform](https://www.terraform.io/docs/providers/azurerm/index.html) include un elenco completo e aggiornato dei provider di Azure supportati.</span><span class="sxs-lookup"><span data-stu-id="c4975-159">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
