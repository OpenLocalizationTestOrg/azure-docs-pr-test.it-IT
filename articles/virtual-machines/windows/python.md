---
title: aaaCreate e gestire una macchina virtuale Windows in Azure usando Python | Documenti Microsoft
description: Informazioni toouse Python toocreate e gestire una macchina virtuale Windows in Azure.
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
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="11087-103">Creare e gestire macchine virtuali Windows in Azure usando Python</span><span class="sxs-lookup"><span data-stu-id="11087-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="11087-104">Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="11087-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="11087-105">Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale usando Python.</span><span class="sxs-lookup"><span data-stu-id="11087-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="11087-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="11087-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="11087-107">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11087-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="11087-108">Installare i pacchetti</span><span class="sxs-lookup"><span data-stu-id="11087-108">Install packages</span></span>
> * <span data-ttu-id="11087-109">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="11087-109">Create credentials</span></span>
> * <span data-ttu-id="11087-110">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="11087-110">Create resources</span></span>
> * <span data-ttu-id="11087-111">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="11087-111">Perform management tasks</span></span>
> * <span data-ttu-id="11087-112">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="11087-112">Delete resources</span></span>
> * <span data-ttu-id="11087-113">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="11087-113">Run hello application</span></span>

<span data-ttu-id="11087-114">Sono necessari circa 20 minuti toodo questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="11087-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="11087-115">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11087-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="11087-116">Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="11087-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="11087-117">Selezionare **sviluppo Python** hello pagina carichi di lavoro e quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="11087-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="11087-118">In hello riepilogo, è possibile vedere che **Python 3 64-bit (3.6.0)** viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="11087-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="11087-119">Se già stato installato Visual Studio, è possibile aggiungere hello Python il carico di lavoro hello utilità di avvio di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11087-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="11087-120">Dopo aver installato e avviato Visual Studio, fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="11087-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="11087-121">Fare clic su **modelli** > **Python** > **applicazione Python**, immettere *myPythonProject* per nome hello hello progetto di, selezionare il percorso di hello del progetto hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="11087-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="11087-122">Installare i pacchetti</span><span class="sxs-lookup"><span data-stu-id="11087-122">Install packages</span></span>

1. <span data-ttu-id="11087-123">In Esplora soluzioni, in *myPythonProject*, fare clic con il pulsante destro del mouse su **Ambienti Python** e quindi selezionare **Aggiungi ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="11087-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="11087-124">Nella schermata Aggiungi ambiente virtuale hello, accettare il nome predefinito hello di *env*, assicurarsi che *3.6 Python (64 bit)* è selezionata per l'interprete base hello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="11087-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="11087-125">Pulsante destro del mouse hello *env* ambiente che è stato creato, fare clic su **Installa pacchetto Python**, immettere *azure* in hello casella di ricerca e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="11087-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="11087-126">Verrà visualizzato nella finestra di output di hello che i pacchetti hello azure sono stati installati correttamente.</span><span class="sxs-lookup"><span data-stu-id="11087-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="11087-127">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="11087-127">Create credentials</span></span>

<span data-ttu-id="11087-128">Prima di iniziare questo passaggio, verificare di disporre di un'[entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11087-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="11087-129">È inoltre necessario registrare l'ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="11087-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="11087-130">Aprire *myPythonProject.py* file che è stato creato, quindi aggiungere questo codice tooenable toorun l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="11087-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="11087-131">codice hello tooimport che è necessario aggiungere questi top toohello istruzioni del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="11087-132">Nel file hello. py aggiungere variabili dopo le istruzioni import hello toospecify comuni valori utilizzati nel codice di hello:</span><span class="sxs-lookup"><span data-stu-id="11087-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="11087-133">Sostituire **subscription-id** con l'identificatore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="11087-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="11087-134">le credenziali di Active Directory hello toocreate toomake richieste, è necessario aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="11087-135">Sostituire **id applicazione**, **chiave di autenticazione**, e **id tenant** con valori hello raccolti in precedenza durante la creazione di Azure Active Directory entità servizio.</span><span class="sxs-lookup"><span data-stu-id="11087-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="11087-136">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="11087-137">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="11087-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="11087-138">Inizializzare i client di gestione</span><span class="sxs-lookup"><span data-stu-id="11087-138">Initialize management clients</span></span>

<span data-ttu-id="11087-139">Client di gestione sono necessari toocreate e gestire risorse utilizzando hello SDK Python in Azure.</span><span class="sxs-lookup"><span data-stu-id="11087-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="11087-140">client di gestione di hello toocreate, aggiungere questo codice sotto hello **se** istruzione quindi fine del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

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

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="11087-141">Creare VM hello e risorse di supporto</span><span class="sxs-lookup"><span data-stu-id="11087-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="11087-142">Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11087-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="11087-143">toocreate un gruppo di risorse, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="11087-144">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="11087-145">[Set di disponibilità](tutorial-availability-sets.md) rendono più semplice per l'utente nelle macchine virtuali di hello toomaintain utilizzate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="11087-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="11087-146">toocreate una disponibilità set, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
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

2. <span data-ttu-id="11087-147">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="11087-148">Oggetto [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario toocommunicate con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="11087-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="11087-149">toocreate un indirizzo IP pubblico per la macchina virtuale hello, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="11087-150">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="11087-151">Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11087-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="11087-152">toocreate una rete virtuale, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="11087-153">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="11087-154">tooadd una rete virtuale toohello subnet, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
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
        
4. <span data-ttu-id="11087-155">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="11087-156">Una macchina virtuale richiede un toocommunicate di interfaccia di rete nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="11087-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="11087-157">toocreate un'interfaccia di rete, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="11087-158">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="11087-159">Dopo aver creato hello tutte le risorse di supporto, è possibile creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11087-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="11087-160">toocreate hello macchina virtuale, aggiungere questa funzione dopo le variabili di hello nel file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
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
    > <span data-ttu-id="11087-161">Questa esercitazione consente di creare una macchina virtuale in esecuzione una versione del sistema operativo di Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="11087-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="11087-162">toolearn più sulla selezione di altre immagini, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con Windows PowerShell e hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11087-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="11087-163">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="11087-164">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="11087-164">Perform management tasks</span></span>

<span data-ttu-id="11087-165">Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11087-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="11087-166">Inoltre, è consigliabile toocreate codice tooautomate attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="11087-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="11087-167">Ottenere informazioni su hello VM</span><span class="sxs-lookup"><span data-stu-id="11087-167">Get information about hello VM</span></span>

1. <span data-ttu-id="11087-168">tooget informazioni hello macchina virtuale, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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
2. <span data-ttu-id="11087-169">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="11087-170">Arrestare VM hello</span><span class="sxs-lookup"><span data-stu-id="11087-170">Stop hello VM</span></span>

<span data-ttu-id="11087-171">È possibile arrestare una macchina virtuale e mantenere tutte le relative impostazioni, ma continuare toobe addebitato oppure è possibile arrestare una macchina virtuale e deallocarlo.</span><span class="sxs-lookup"><span data-stu-id="11087-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="11087-172">Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.</span><span class="sxs-lookup"><span data-stu-id="11087-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="11087-173">macchina virtuale di hello toostop senza deallocarlo, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="11087-174">Se si desidera una macchina virtuale di hello toodeallocate, modificare il codice di toothis hello power_off chiamata:</span><span class="sxs-lookup"><span data-stu-id="11087-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="11087-175">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="11087-176">Avviare hello VM</span><span class="sxs-lookup"><span data-stu-id="11087-176">Start hello VM</span></span>

1. <span data-ttu-id="11087-177">toostart hello macchina virtuale, aggiungere questa funzione dopo le variabili di hello nel file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="11087-178">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="11087-179">Ridimensionare hello VM</span><span class="sxs-lookup"><span data-stu-id="11087-179">Resize hello VM</span></span>

<span data-ttu-id="11087-180">Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="11087-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="11087-181">Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="11087-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="11087-182">dimensioni hello toochange della macchina virtuale hello, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="11087-183">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="11087-184">Aggiungere un toohello disco dati VM</span><span class="sxs-lookup"><span data-stu-id="11087-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="11087-185">Le macchine virtuali possono disporre di uno o più [dischi dati](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) archiviati in dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="11087-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="11087-186">tooadd una macchina virtuale toohello disco dati, aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

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

2. <span data-ttu-id="11087-187">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="11087-188">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="11087-188">Delete resources</span></span>

<span data-ttu-id="11087-189">Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre un risorse toodelete buona norma che non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="11087-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="11087-190">Se si desidera toodelete hello le macchine virtuali e hello tutte le risorse di supporto, si dispone di toodo è gruppo di risorse hello di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="11087-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="11087-191">gruppo di risorse toodelete hello e tutte le risorse, è possibile aggiungere questa funzione dopo le variabili di hello in file di py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="11087-192">funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:</span><span class="sxs-lookup"><span data-stu-id="11087-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="11087-193">Salvare *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="11087-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="11087-194">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="11087-194">Run hello application</span></span>

1. <span data-ttu-id="11087-195">un'applicazione console hello toorun, fare clic su **avviare** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11087-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="11087-196">Premere **invio** dopo che viene restituito lo stato di hello di ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="11087-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="11087-197">In informazioni sullo stato di hello, vedrai un **Succeeded** lo stato di provisioning.</span><span class="sxs-lookup"><span data-stu-id="11087-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="11087-198">Dopo la creazione di macchine virtuali hello, si dispone di hello opportunità toodelete tutte le risorse di hello creati.</span><span class="sxs-lookup"><span data-stu-id="11087-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="11087-199">Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti tooverify relativa creazione in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="11087-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="11087-200">Se si hanno hello Apri portale di Azure, potrebbe essere toorefresh hello pannello toosee nuove risorse.</span><span class="sxs-lookup"><span data-stu-id="11087-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="11087-201">Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish.</span><span class="sxs-lookup"><span data-stu-id="11087-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="11087-202">Potrebbe richiedere alcuni minuti dopo l'applicazione hello è terminata prima di tutte le risorse di hello e gruppo di risorse hello vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="11087-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="11087-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11087-203">Next steps</span></span>

- <span data-ttu-id="11087-204">Se si sono verificati problemi con la distribuzione di hello, un passaggio successivo consisterebbe toolook in [risoluzione dei problemi delle distribuzioni del gruppo di risorse con il portale di Azure](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="11087-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="11087-205">Altre informazioni su hello [libreria Python di Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="11087-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

