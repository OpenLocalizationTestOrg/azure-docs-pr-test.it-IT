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
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Creare e gestire macchine virtuali Windows in Azure usando Python

Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure. Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale usando Python. Si apprenderà come:

> [!div class="checklist"]
> * Creare un progetto di Visual Studio
> * Installare i pacchetti
> * Creare le credenziali
> * Creare le risorse
> * Eseguire le attività di gestione
> * Eliminare le risorse
> * Eseguire un'applicazione hello

Sono necessari circa 20 minuti toodo questi passaggi.

## <a name="create-a-visual-studio-project"></a>Creare un progetto di Visual Studio

1. Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selezionare **sviluppo Python** hello pagina carichi di lavoro e quindi fare clic su **installare**. In hello riepilogo, è possibile vedere che **Python 3 64-bit (3.6.0)** viene selezionato automaticamente. Se già stato installato Visual Studio, è possibile aggiungere hello Python il carico di lavoro hello utilità di avvio di Visual Studio.
2. Dopo aver installato e avviato Visual Studio, fare clic su **File** > **Nuovo** > **Progetto**.
3. Fare clic su **modelli** > **Python** > **applicazione Python**, immettere *myPythonProject* per nome hello hello progetto di, selezionare il percorso di hello del progetto hello e quindi fare clic su **OK**.

## <a name="install-packages"></a>Installare i pacchetti

1. In Esplora soluzioni, in *myPythonProject*, fare clic con il pulsante destro del mouse su **Ambienti Python** e quindi selezionare **Aggiungi ambiente virtuale**.
2. Nella schermata Aggiungi ambiente virtuale hello, accettare il nome predefinito hello di *env*, assicurarsi che *3.6 Python (64 bit)* è selezionata per l'interprete base hello e quindi fare clic su **crea**.
3. Pulsante destro del mouse hello *env* ambiente che è stato creato, fare clic su **Installa pacchetto Python**, immettere *azure* in hello casella di ricerca e quindi premere INVIO.

Verrà visualizzato nella finestra di output di hello che i pacchetti hello azure sono stati installati correttamente. 

## <a name="create-credentials"></a>Creare le credenziali

Prima di iniziare questo passaggio, verificare di disporre di un'[entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). È inoltre necessario registrare l'ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario in un passaggio successivo.

1. Aprire *myPythonProject.py* file che è stato creato, quindi aggiungere questo codice tooenable toorun l'applicazione:

    ```python
    if __name__ == "__main__":
    ```

2. codice hello tooimport che è necessario aggiungere questi top toohello istruzioni del file. py hello:

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. Nel file hello. py aggiungere variabili dopo le istruzioni import hello toospecify comuni valori utilizzati nel codice di hello:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Sostituire **subscription-id** con l'identificatore della sottoscrizione.

4. le credenziali di Active Directory hello toocreate toomake richieste, è necessario aggiungere questa funzione dopo le variabili di hello in file di py hello:

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Sostituire **id applicazione**, **chiave di autenticazione**, e **id tenant** con valori hello raccolti in precedenza durante la creazione di Azure Active Directory entità servizio.

5. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Creare le risorse
 
### <a name="initialize-management-clients"></a>Inizializzare i client di gestione

Client di gestione sono necessari toocreate e gestire risorse utilizzando hello SDK Python in Azure. client di gestione di hello toocreate, aggiungere questo codice sotto hello **se** istruzione quindi fine del file. py hello:

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

### <a name="create-hello-vm-and-supporting-resources"></a>Creare VM hello e risorse di supporto

Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).

1. toocreate un gruppo di risorse, aggiungere questa funzione dopo le variabili di hello in file di py hello:

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Set di disponibilità](tutorial-availability-sets.md) rendono più semplice per l'utente nelle macchine virtuali di hello toomaintain utilizzate dall'applicazione.

1. toocreate una disponibilità set, aggiungere questa funzione dopo le variabili di hello in file di py hello:
   
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

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

Oggetto [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario toocommunicate con la macchina virtuale hello.

1. toocreate un indirizzo IP pubblico per la macchina virtuale hello, aggiungere questa funzione dopo le variabili di hello in file di py hello:

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

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).

1. toocreate una rete virtuale, aggiungere questa funzione dopo le variabili di hello in file di py hello:

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

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd una rete virtuale toohello subnet, aggiungere questa funzione dopo le variabili di hello in file di py hello:
    
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
        
4. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Una macchina virtuale richiede un toocommunicate di interfaccia di rete nella rete virtuale hello.

1. toocreate un'interfaccia di rete, aggiungere questa funzione dopo le variabili di hello in file di py hello:

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

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Dopo aver creato hello tutte le risorse di supporto, è possibile creare una macchina virtuale.

1. toocreate hello macchina virtuale, aggiungere questa funzione dopo le variabili di hello nel file. py hello:
   
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
    > Questa esercitazione consente di creare una macchina virtuale in esecuzione una versione del sistema operativo di Windows Server hello. toolearn più sulla selezione di altre immagini, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con Windows PowerShell e hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Eseguire le attività di gestione

Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale. Inoltre, è consigliabile toocreate codice tooautomate attività ripetitive o complesse.

### <a name="get-information-about-hello-vm"></a>Ottenere informazioni su hello VM

1. tooget informazioni hello macchina virtuale, aggiungere questa funzione dopo le variabili di hello in file di py hello:

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
2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Arrestare VM hello

È possibile arrestare una macchina virtuale e mantenere tutte le relative impostazioni, ma continuare toobe addebitato oppure è possibile arrestare una macchina virtuale e deallocarlo. Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.

1. macchina virtuale di hello toostop senza deallocarlo, aggiungere questa funzione dopo le variabili di hello in file di py hello:

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Se si desidera una macchina virtuale di hello toodeallocate, modificare il codice di toothis hello power_off chiamata:

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Avviare hello VM

1. toostart hello macchina virtuale, aggiungere questa funzione dopo le variabili di hello nel file. py hello:

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Ridimensionare hello VM

Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione. Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).

1. dimensioni hello toochange della macchina virtuale hello, aggiungere questa funzione dopo le variabili di hello in file di py hello:

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

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Aggiungere un toohello disco dati VM

Le macchine virtuali possono disporre di uno o più [dischi dati](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) archiviati in dischi rigidi virtuali.

1. tooadd una macchina virtuale toohello disco dati, aggiungere questa funzione dopo le variabili di hello in file di py hello: 

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

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Eliminare le risorse

Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre un risorse toodelete buona norma che non sono più necessari. Se si desidera toodelete hello le macchine virtuali e hello tutte le risorse di supporto, si dispone di toodo è gruppo di risorse hello di eliminazione.

1. gruppo di risorse toodelete hello e tutte le risorse, è possibile aggiungere questa funzione dopo le variabili di hello in file di py hello:
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. funzione hello toocall aggiunto in precedenza, aggiungere questo codice sotto hello **se** istruzione alla fine di hello del file. py hello:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Salvare *myPythonProject.py*.

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

1. un'applicazione console hello toorun, fare clic su **avviare** in Visual Studio.

2. Premere **invio** dopo che viene restituito lo stato di hello di ogni risorsa. In informazioni sullo stato di hello, vedrai un **Succeeded** lo stato di provisioning. Dopo la creazione di macchine virtuali hello, si dispone di hello opportunità toodelete tutte le risorse di hello creati. Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti tooverify relativa creazione in hello portale di Azure. Se si hanno hello Apri portale di Azure, potrebbe essere toorefresh hello pannello toosee nuove risorse.  

    Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish. Potrebbe richiedere alcuni minuti dopo l'applicazione hello è terminata prima di tutte le risorse di hello e gruppo di risorse hello vengono eliminati.


## <a name="next-steps"></a>Passaggi successivi

- Se si sono verificati problemi con la distribuzione di hello, un passaggio successivo consisterebbe toolook in [risoluzione dei problemi delle distribuzioni del gruppo di risorse con il portale di Azure](../../resource-manager-troubleshoot-deployments-portal.md)
- Altre informazioni su hello [libreria Python di Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

