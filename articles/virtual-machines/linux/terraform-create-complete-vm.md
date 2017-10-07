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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Creare un'infrastruttura di base in Azure usando Terraform
Questo articolo descrive i passaggi di hello tootake tooprovision una macchina virtuale, con l'infrastruttura sottostante, è necessario in Azure. Si apprenderà come toowrite Terraform script e come toovisualize hello cambia prima di renderli nell'infrastruttura cloud. È inoltre verrà illustrato come infrastruttura toocreate in Azure utilizzando Terraform.

tooget avviato, creare un file denominato \terraform_azure101.tf nell'editor di testo di scelta (Visual Studio codice/Sublime/Vim/ecc.). nome esatto di Hello del file hello non è importante perché Terraform accetta un parametro di nome di cartella hello: tutti gli script nella cartella hello venga eseguiti. Incollare hello seguente codice nel nuovo file hello:

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
In hello `provider` sezione di hello script, si indicano Terraform toouse le risorse tooprovision un provider di Azure nello script hello. i valori tooget per subscription_id, appId, password e tenant_id, vedere hello [installare e configurare Terraform](terraform-install-configure.md) Guida. Se le variabili di ambiente per i valori hello è stato creato in questo blocco, non è necessario tooinclude è. 

Hello `azurerm_resource_group` risorsa indica Terraform toocreate un nuovo gruppo di risorse. Altri tipi di risorse disponibili in Terraform sono elencati più avanti in questo articolo.

## <a name="execute-hello-script"></a>Eseguire lo script hello
Dopo aver salvato script hello, uscire dalla riga di comando o della console toohello e digitare hello riportato di seguito:
```
terraform init
```
 provider di Terraform tooinitialize hello per Azure. Quindi modificare anche le directory hello**terraformscripts**, e hello problema comando seguente:
```
terraform plan
```
È stato usato hello `plan` Terraform comando, che esamina le risorse di hello definite negli script hello. Confronta le informazioni di stato toohello salvate da Terraform e quindi output hello esecuzione pianificato _senza_ effettivamente la creazione di risorse in Azure. 

Dopo l'esecuzione di comandi precedente hello, dovrebbe essere simile al seguente hello seguente schermata:

![Piano Terraform](./media/terraform/tf_plan2.png)

Se tutto sembra corretto, eseguire il provisioning di questo nuovo gruppo di risorse in Azure eseguendo hello seguente: 
```
terraform apply
```
Nel portale di Azure hello, vedrai hello nuovo vuoto gruppo di risorse denominato `terraformtest`. Nella seguente sezione di hello, aggiungere che una macchina virtuale e tutti i hello infrastruttura di supporto per il gruppo di risorse toohello macchina virtuale.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Eseguire il provisioning di una VM Ubuntu con Terraform
È possibile estendere script Terraform hello che abbiamo creato con i dettagli hello tooprovision necessari una macchina virtuale in esecuzione Ubuntu. le risorse Hello viene effettuato il provisioning in hello le sezioni seguenti sono:

* Una rete con una singola subnet
* Una scheda di interfaccia di rete 
* Un account di archiviazione per diagnostica della macchina virtuale hello
* Un indirizzo IP pubblico
* Una macchina virtuale che utilizza tutte le risorse di precedente hello 

Per una documentazione approfondita per ciascuna delle risorse di Azure Terraform hello, vedere hello [Terraform documentazione](https://www.terraform.io/docs/providers/azurerm/index.html).

versione completa di Hello di hello [script di provisioning](#complete-terraform-script) viene inoltre fornita per comodità.

### <a name="extend-hello-terraform-script"></a>Estendere script Terraform hello
Estendere script hello che è stato creato con hello seguenti risorse: 
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
script precedente Hello crea una rete virtuale e una subnet all'interno della rete virtuale. Si noti gruppo risorse toohello riferimento hello che avere già creato tramite "${azurerm_resource_group.helloterraform.name}" nella rete virtuale hello sia la definizione di subnet hello.

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
frammenti di codice script precedente Hello creare un indirizzo IP pubblico e un'interfaccia di rete che fa uso di indirizzo IP pubblico hello creato. Si noti hello riferimenti toosubnet_id e public_ip_address_id. Terraform ha toounderstand intelligenti che hello interfaccia di rete presenta una dipendenza risorse hello toobe tale esigenza creato prima della creazione di hello hello dell'interfaccia di rete.

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
Qui viene creato un account di archiviazione. Questo account di archiviazione è in macchina virtuale hello verranno archiviati i dettagli di diagnostica.

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
Infine, frammento precedente hello crea una macchina virtuale che utilizza tutte le risorse di hello stato già eseguito il provisioning. Sono un account di archiviazione per diagnostica della macchina virtuale hello, un'interfaccia di rete con subnet specificato e un IP pubblico e il gruppo di risorse hello già stato creato. Si noti proprietà vm_size hello, in cui viene specificata una SKU di Azure Standard DS1v2 script hello.

È necessario toosupply una chiave pubblica SSH. Inserire il valore di chiave pubblica di hello sezione hello **... INSERT OPENSSH PUBLIC KEY HERE ...**, visualizzata nell'esempio di codice precedente. È possibile utilizzare un oggetto esistente ssh coppia di chiavi o seguire hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) o [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentazione toogenerate hello coppia di chiavi.

### <a name="execute-hello-script"></a>Eseguire lo script hello
Script completo hello salvato, uscire dalla riga di comando o della console toohello e digitare hello riportato di seguito:
```
terraform apply
```
In un secondo momento, le risorse di hello, tra cui una macchina virtuale, vengono visualizzate in hello `terraformtest` gruppo di risorse in hello portale di Azure.

## <a name="complete-terraform-script"></a>Completare lo script Terraform

Per praticità, di seguito è hello completo Terraform script che esegue il provisioning dell'infrastruttura di hello descritti in questo articolo.

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

## <a name="next-steps"></a>Passaggi successivi
È stata creata un'infrastruttura di base in Azure usando Terraform. Per scenari più complessi, inclusi esempi d'uso di servizi di bilanciamento del carico e set di scalabilità delle macchine virtuali, vedere i numerosi [esempi di Terraform per Azure](https://github.com/hashicorp/terraform/tree/master/examples). Per un elenco aggiornato dei provider di Azure supportati, vedere hello [Terraform documentazione](https://www.terraform.io/docs/providers/azurerm/index.html).
