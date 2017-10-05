---
title: Creare e gestire una macchina virtuale Windows in Azure usando Python | Microsoft Docs
description: Informazioni sull'uso di Python per creare e gestire una macchina virtuale Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: bb777d41570d7b1dc97402d532519488912948e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="a14fc-103">Creare e gestire macchine virtuali Windows in Azure usando Python</span><span class="sxs-lookup"><span data-stu-id="a14fc-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="a14fc-104">Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="a14fc-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="a14fc-105">Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale usando Python.</span><span class="sxs-lookup"><span data-stu-id="a14fc-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="a14fc-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="a14fc-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a14fc-107">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a14fc-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="a14fc-108">Installare i pacchetti</span><span class="sxs-lookup"><span data-stu-id="a14fc-108">Install packages</span></span>
> * <span data-ttu-id="a14fc-109">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="a14fc-109">Create credentials</span></span>
> * <span data-ttu-id="a14fc-110">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="a14fc-110">Create resources</span></span>
> * <span data-ttu-id="a14fc-111">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="a14fc-111">Perform management tasks</span></span>
> * <span data-ttu-id="a14fc-112">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="a14fc-112">Delete resources</span></span>
> * <span data-ttu-id="a14fc-113">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="a14fc-113">Run the application</span></span>

<span data-ttu-id="a14fc-114">L'esecuzione di questi passaggi richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="a14fc-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="a14fc-115">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a14fc-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="a14fc-116">Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="a14fc-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="a14fc-117">Selezionare **Sviluppo Python** nella pagina Carichi di lavoro e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="a14fc-117">Select **Python development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="a14fc-118">Nel riepilogo si noti che **Python 3 a 64 bit (3.6.0)** viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a14fc-118">In the summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="a14fc-119">Se Visual Studio è già stato installato, è possibile aggiungere il carico di lavoro Python usando l'utilità di avvio di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a14fc-119">If you have already installed Visual Studio, you can add the Python workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="a14fc-120">Dopo aver installato e avviato Visual Studio, fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="a14fc-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="a14fc-121">Fare clic su **Modelli** > **Python** > **Applicazione Python**, immettere *myPythonProject* come nome del progetto, selezionare il percorso del progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a14fc-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="a14fc-122">Installare i pacchetti</span><span class="sxs-lookup"><span data-stu-id="a14fc-122">Install packages</span></span>

1. <span data-ttu-id="a14fc-123">In Esplora soluzioni, in *myPythonProject*, fare clic con il pulsante destro del mouse su **Ambienti Python** e quindi selezionare **Aggiungi ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="a14fc-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="a14fc-124">Nella schermata Aggiungi ambiente virtuale accettare il nome predefinito *env*, verificare che *Python 3.6 (64 bit)* sia selezionato per l'interprete di base e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a14fc-124">On the Add Virtual Environment screen, accept the default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for the base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="a14fc-125">Fare clic con il pulsante destro del mouse sull'ambiente *env* appena creato, fare clic su **Installa pacchetto Python**, immettere *azure* nella casella di ricerca e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="a14fc-125">Right-click the *env* environment that you created, click **Install Python Package**, enter *azure* in the search box, and then press Enter.</span></span>

<span data-ttu-id="a14fc-126">La corretta installazione dei pacchetti di Azure verrà indicata nelle finestre di output.</span><span class="sxs-lookup"><span data-stu-id="a14fc-126">You should see in the output windows that the azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="a14fc-127">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="a14fc-127">Create credentials</span></span>

<span data-ttu-id="a14fc-128">Prima di iniziare questo passaggio, verificare di disporre di un'[entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a14fc-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a14fc-129">È inoltre necessario registrare l'ID dell'applicazione, la chiave di autenticazione e l'ID del tenant che saranno necessari in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="a14fc-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="a14fc-130">Aprire il file *myPythonProject.py* che è stato creato e quindi aggiungere questo codice per consentire l'esecuzione dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="a14fc-130">Open *myPythonProject.py* file that was created, and then add this code to enable your application to run:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="a14fc-131">Per importare il codice necessario, aggiungere queste istruzioni all'inizio del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-131">To import the code that is needed, add these statements to the top of the .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="a14fc-132">Nel file con estensione py aggiungere quindi le variabili dopo le istruzioni di importazione per specificare i valori comuni usati nel codice:</span><span class="sxs-lookup"><span data-stu-id="a14fc-132">Next in the .py file, add variables after the import statements to specify common values used in the code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="a14fc-133">Sostituire **subscription-id** con l'identificatore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a14fc-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="a14fc-134">Per creare le credenziali di Active Directory necessarie per inoltrare le richieste, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-134">To create the Active Directory credentials that you need to make requests, add this function after the variables in the .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="a14fc-135">Sostituire **application-id**, **authentication-key** e **tenant-id** con i valori raccolti durante la creazione dell'entità servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a14fc-135">Replace **application-id**, **authentication-key**, and **tenant-id** with the values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="a14fc-136">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-136">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="a14fc-137">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="a14fc-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="a14fc-138">Inizializzare i client di gestione</span><span class="sxs-lookup"><span data-stu-id="a14fc-138">Initialize management clients</span></span>

<span data-ttu-id="a14fc-139">I client di gestione sono necessari per creare e gestire le risorse tramite Python SDK in Azure.</span><span class="sxs-lookup"><span data-stu-id="a14fc-139">Management clients are needed to create and manage resources using the Python SDK in Azure.</span></span> <span data-ttu-id="a14fc-140">Per creare i client di gestione, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-140">To create the management clients, add this code under the **if** statement at then end of the .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-the-vm-and-supporting-resources"></a><span data-ttu-id="a14fc-141">Creare la macchina virtuale e le risorse di supporto</span><span class="sxs-lookup"><span data-stu-id="a14fc-141">Create the VM and supporting resources</span></span>

<span data-ttu-id="a14fc-142">Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a14fc-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="a14fc-143">Per creare un gruppo di risorse, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-143">To create a resource group, add this function after the variables in the .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="a14fc-144">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-144">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter to continue...')
    ```

<span data-ttu-id="a14fc-145">I [set di disponibilità](tutorial-availability-sets.md) semplificano la manutenzione delle macchine virtuali usate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a14fc-145">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

1. <span data-ttu-id="a14fc-146">Per creare un set di disponibilità, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-146">To create an availability set, add this function after the variables in the .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="a14fc-147">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-147">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter to continue...')
    ```

<span data-ttu-id="a14fc-148">Un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario per comunicare con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a14fc-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

1. <span data-ttu-id="a14fc-149">Per creare un indirizzo IP pubblico per la macchina virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-149">To create a public IP address for the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="a14fc-150">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-150">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="a14fc-151">Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a14fc-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a14fc-152">Per creare una rete virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-152">To create a virtual network, add this function after the variables in the .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="a14fc-153">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-153">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

3. <span data-ttu-id="a14fc-154">Per aggiungere una subnet alla rete virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-154">To add a subnet to the virtual network, add this function after the variables in the .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="a14fc-155">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-155">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="a14fc-156">Una macchina virtuale richiede un'interfaccia di rete per comunicare nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a14fc-156">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

1. <span data-ttu-id="a14fc-157">Per creare un'interfaccia di rete, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-157">To create a network interface, add this function after the variables in the .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="a14fc-158">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-158">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="a14fc-159">Dopo avere creato tutte le risorse di supporto, è possibile creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a14fc-159">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="a14fc-160">Per creare una macchina virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-160">To create the virtual machine, add this function after the variables in the .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="a14fc-161">Questa esercitazione illustra come creare una macchina virtuale in cui è in esecuzione una versione del sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a14fc-161">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="a14fc-162">Per altre informazioni sulla selezione di altre immagini, vedere [Esplorare e selezionare immagini delle macchine virtuali di Azure con Windows PowerShell e l'interfaccia della riga di comando di Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a14fc-162">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="a14fc-163">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-163">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="a14fc-164">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="a14fc-164">Perform management tasks</span></span>

<span data-ttu-id="a14fc-165">Durante il ciclo di vita di una macchina virtuale si eseguono attività di gestione come l'avvio, l'arresto o l'eliminazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a14fc-165">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="a14fc-166">È inoltre possibile creare codice per automatizzare le attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="a14fc-166">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

### <a name="get-information-about-the-vm"></a><span data-ttu-id="a14fc-167">Ottenere informazioni sulla VM</span><span class="sxs-lookup"><span data-stu-id="a14fc-167">Get information about the VM</span></span>

1. <span data-ttu-id="a14fc-168">Per ottenere informazioni sulla macchina virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-168">To get information about the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="a14fc-169">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-169">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter to continue...')
    ```

### <a name="stop-the-vm"></a><span data-ttu-id="a14fc-170">Arrestare la VM</span><span class="sxs-lookup"><span data-stu-id="a14fc-170">Stop the VM</span></span>

<span data-ttu-id="a14fc-171">È possibile arrestare una macchina virtuale e mantenere tutte le sue impostazioni, pur continuando a vedersela addebitata oppure è possibile arrestare una macchina virtuale e deallocarla.</span><span class="sxs-lookup"><span data-stu-id="a14fc-171">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="a14fc-172">Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.</span><span class="sxs-lookup"><span data-stu-id="a14fc-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="a14fc-173">Per arrestare la macchina virtuale senza deallocarla, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-173">To stop the virtual machine without deallocating it, add this function after the variables in the .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="a14fc-174">Per deallocare la macchina virtuale, sostituire la chiamata power_off con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a14fc-174">If you want to deallocate the virtual machine, change the power_off call to this code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="a14fc-175">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-175">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="start-the-vm"></a><span data-ttu-id="a14fc-176">Avviare la VM</span><span class="sxs-lookup"><span data-stu-id="a14fc-176">Start the VM</span></span>

1. <span data-ttu-id="a14fc-177">Per avviare la macchina virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-177">To start the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="a14fc-178">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-178">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="resize-the-vm"></a><span data-ttu-id="a14fc-179">Ridimensionare la VM</span><span class="sxs-lookup"><span data-stu-id="a14fc-179">Resize the VM</span></span>

<span data-ttu-id="a14fc-180">Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a14fc-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="a14fc-181">Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="a14fc-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="a14fc-182">Per modificare le dimensioni della macchina virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-182">To change the size of the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="a14fc-183">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-183">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter to continue...')
    ```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="a14fc-184">Aggiungere un disco dati alla VM</span><span class="sxs-lookup"><span data-stu-id="a14fc-184">Add a data disk to the VM</span></span>

<span data-ttu-id="a14fc-185">Le macchine virtuali possono disporre di uno o più [dischi dati](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) archiviati in dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="a14fc-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="a14fc-186">Per aggiungere un disco dati alla macchina virtuale, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-186">To add a data disk to the virtual machine, add this function after the variables in the .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="a14fc-187">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-187">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter to continue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="a14fc-188">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="a14fc-188">Delete resources</span></span>

<span data-ttu-id="a14fc-189">Dal momento che le risorse usate in Azure vengono addebitate, è sempre consigliabile eliminare le risorse non più necessarie.</span><span class="sxs-lookup"><span data-stu-id="a14fc-189">Because you are charged for resources used in Azure, it's always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="a14fc-190">Per eliminare le macchine virtuali e tutte le risorse di supporto, è sufficiente eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a14fc-190">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="a14fc-191">Per eliminare il gruppo di risorse e tutte le risorse, aggiungere questa funzione dopo le variabili nel file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-191">To delete the resource group and all resources, add this function after the variables in the .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="a14fc-192">Per chiamare la funzione aggiunta in precedenza, aggiungere questo codice sotto l'istruzione **if** alla fine del file con estensione py:</span><span class="sxs-lookup"><span data-stu-id="a14fc-192">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="a14fc-193">Salvare *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="a14fc-193">Save *myPythonProject.py*.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="a14fc-194">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="a14fc-194">Run the application</span></span>

1. <span data-ttu-id="a14fc-195">Per eseguire l'applicazione console, fare clic su **Avvia** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a14fc-195">To run the console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="a14fc-196">Premere **INVIO** dopo che è stato restituito lo stato di ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="a14fc-196">Press **Enter** after the status of each resource is returned.</span></span> <span data-ttu-id="a14fc-197">Nelle informazioni sullo stato dovrebbe essere visualizzato lo stato di provisioning **Completato**.</span><span class="sxs-lookup"><span data-stu-id="a14fc-197">In the status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="a14fc-198">Dopo che la macchina virtuale è stata creata, si avrà l'opportunità di eliminare tutte le risorse create.</span><span class="sxs-lookup"><span data-stu-id="a14fc-198">After the virtual machine is created, you have the opportunity to delete all the resources that you create.</span></span> <span data-ttu-id="a14fc-199">Prima di premere **INVIO** per iniziare a eliminare le risorse, è consigliabile dedicare qualche minuto alla verifica della loro creazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a14fc-199">Before you press **Enter** to start deleting resources, you could take a few minutes to verify their creation in the Azure portal.</span></span> <span data-ttu-id="a14fc-200">Se il portale di Azure è aperto, potrebbe essere necessario aggiornare il pannello per visualizzare le nuove risorse.</span><span class="sxs-lookup"><span data-stu-id="a14fc-200">If you have the Azure portal open, you might have to refresh the blade to see new resources.</span></span>  

    <span data-ttu-id="a14fc-201">L'esecuzione completa dell'applicazione console dall'inizio alla fine richiederà circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="a14fc-201">It should take about five minutes for this console application to run completely from start to finish.</span></span> <span data-ttu-id="a14fc-202">L'eliminazione di tutte le risorse e del gruppo di risorse potrebbe richiedere alcuni minuti dopo l'esecuzione completa dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a14fc-202">It may take several minutes after the application has finished before all the resources and the resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a14fc-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a14fc-203">Next steps</span></span>

- <span data-ttu-id="a14fc-204">Se si sono verificati problemi con la distribuzione, è consigliabile vedere come [risolvere i problemi della distribuzione di gruppi di risorse con il portale di Azure](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a14fc-204">If there were issues with the deployment, a next step would be to look at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="a14fc-205">Altre informazioni sulla [libreria Python di Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="a14fc-205">Learn more about the [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

