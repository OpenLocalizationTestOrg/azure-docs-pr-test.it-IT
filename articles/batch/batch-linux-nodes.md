---
title: Batch di Azure - i nodi di calcolo aaaRun Linux nella macchina virtuale | Documenti Microsoft
description: Informazioni su come tooprocess il parallelo calcolare carichi di lavoro nel pool di macchine virtuali Linux in Azure Batch.
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Eseguire il provisioning di nodi di calcolo Linux nei pool di Batch

È possibile utilizzare i carichi di lavoro di Azure Batch toorun calcolo parallelo nelle macchine virtuali Linux e Windows. In questo articolo illustra in dettaglio come pool toocreate di Linux nodi di calcolo nel servizio Batch hello utilizzando entrambi hello [Python Batch] [ py_batch_package] e [.NET per Batch] [ api_net] librerie client.

> [!NOTE]
> I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017. Sono supportate nei pool di Batch creato tra 10 marzo 2016 e 5 luglio 2017 solo se il pool di hello è stato creato utilizzando una configurazione del servizio Cloud. Pool di batch creati too10 precedente marzo 2016 non supportano pacchetti di applicazioni. Per ulteriori informazioni sull'utilizzo dell'applicazione pacchetti toodeploy i nodi di Batch tooyour applicazioni, vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Configurazione della macchina virtuale
Quando si crea un pool di nodi di calcolo in Batch, sono disponibili due opzioni da cui tooselect dimensione del nodo hello e sistema operativo: configurazione della macchina virtuale e la configurazione di servizi Cloud.

**Cloud Services Configuration** (Configurazione servizi cloud) fornisce *solo*nodi di calcolo Windows. Dimensioni di nodo di calcolo disponibili sono elencate [dimensioni per i servizi Cloud](../cloud-services/cloud-services-sizes-specs.md), e i sistemi operativi disponibili sono elencati in hello [versioni del sistema operativo Guest Azure e matrice di compatibilità SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Quando si crea un pool che contiene i nodi di servizi Cloud di Azure, è possibile specificare dimensioni di nodo hello e hello famiglia del sistema operativo, che sono descritte nel hello indicato in precedenza gli articoli. Quando si creano pool di nodi di calcolo Windows, viene in genere usata l'opzione Servizi cloud.

La **configurazione della macchina virtuale** fornisce immagini Linux e Windows per i nodi di calcolo. Le dimensioni disponibili per i nodi di calcolo sono elencate in [Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) e [Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows). Quando si crea un pool che contiene i nodi di configurazione della macchina virtuale, è necessario specificare dimensioni di hello di nodi di hello, riferimento all'immagine di macchina virtuale hello e toobe SKU hello Batch nodo agente installato nei nodi hello.

### <a name="virtual-machine-image-reference"></a>Riferimento all'immagine della macchina virtuale
Hello servizio Batch Usa [set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux nodi di calcolo. È possibile specificare un'immagine da hello [Azure Marketplace][vm_marketplace], o fornire un'immagine personalizzata che è stato preparato. Per informazioni dettagliate sulle immagini personalizzate, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md#pool).

Quando si configura un riferimento all'immagine di macchina virtuale, specificare le proprietà di hello dell'immagine di macchina virtuale hello. Hello le proprietà seguenti è necessario quando si crea un riferimento all'immagine di macchina virtuale:

| **Proprietà del riferimento all'immagine** | **Esempio** |
| --- | --- |
| Autore |Canonical |
| Offerta |UbuntuServer |
| SKU |14.04.4-LTS |
| Versione |più recenti |

> [!TIP]
> Maggiori informazioni su queste proprietà e come toolist Marketplace immagini in [Naviga e selezionare le immagini di macchina virtuale di Linux in Azure con CLI o PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Si noti che non tutte le immagini del Marketplace sono attualmente compatibili con Batch. Per altre informazioni, vedere [SKU dell'agente del nodo](#node-agent-sku).
>
>

### <a name="node-agent-sku"></a>SKU dell'agente del nodo
agente di Hello Batch nodo è un programma che viene eseguito in ogni nodo nel pool di hello e fornisce l'interfaccia di comando e controllo hello tra nodo hello e il servizio Batch hello. Esistono diverse implementazioni dell'agente del nodo hello, noto come SKU, per sistemi operativi diversi. In pratica, quando si crea una configurazione della macchina virtuale, è innanzitutto necessario specificare riferimento all'immagine di macchina virtuale hello e quindi si specificare hello nodo agente tooinstall sull'immagine di hello. Ogni SKU dell'agente del nodo è in genere compatibile con più immagini di macchina virtuale. Ecco alcuni esempi di SKU dell'agente del nodo:

* batch.node.ubuntu 14.04
* batch.node.centos 7
* batch.node.windows amd64

> [!IMPORTANT]
> Non tutte le immagini di macchina virtuale sono disponibili in Marketplace hello sono compatibili con gli agenti nodo Batch attualmente disponibili hello. Usare l'agente di nodo disponibile hello toolist Batch SDK hello SKU e hello immagini di macchina virtuale a cui sono compatibili. Vedere hello [immagini di elenco di macchine virtuali](#list-of-virtual-machine-images) più avanti in questo articolo per ulteriori informazioni ed esempi di come tooretrieve un elenco di immagini valide in fase di esecuzione.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Creare un pool Linux: Batch Python
Hello frammento di codice seguente viene illustrato un esempio di hello toouse [libreria Client di Microsoft Azure Batch per Python] [ py_batch_package] toocreate un pool di Ubuntu Server nodi di calcolo. Fare riferimento alla documentazione per il modulo di Python Batch è reperibile in hello [azure.batch pacchetto] [ py_batch_docs] in lettura hello documenti.

Questo frammento di codice crea in modo esplicito un metodo [ImageReference][py_imagereference], specificando tutte le rispettive proprietà, ovvero editore, offerta, SKU, versione. Nel codice di produzione, tuttavia, è consigliabile utilizzare hello [list_node_agent_skus] [ py_list_skus] toodetermine (metodo) e scegliere tra hello immagine e il nodo agente SKU combinazioni disponibili in fase di esecuzione.

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

Come accennato in precedenza, si consiglia invece di creare hello [ImageReference] [ py_imagereference] in modo esplicito, utilizzare hello [list_node_agent_skus] [ py_list_skus] metodo toodynamically scegliere hello è attualmente supportato combinazioni immagine agente/Marketplace di nodo. Hello seguente mostra Python come toouse questo metodo.

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a>Creare un pool Linux: Batch .NET
Hello frammento di codice seguente viene illustrato un esempio di hello toouse [.NET per Batch] [ nuget_batch_net] toocreate libreria client un pool di Ubuntu Server nodi di calcolo. È possibile trovare hello [la documentazione di riferimento di .NET per Batch] [ api_net] su MSDN.

frammento di codice seguente Hello utilizza hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect metodo dall'elenco di hello di attualmente Marketplace immagine e il nodo agente SKU combinazioni supportate. Questa tecnica è utile perché elenco hello di combinazioni supportate potrebbe cambiare da tootime ora. in genere a causa dell'aggiunta di altre combinazioni supportate.

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

Sebbene frammento precedente hello utilizza hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] metodo toodynamically elenco e selezionare da supportata immagine e il nodo combinazioni di SKU dell'agente (scelta consigliate), è inoltre possibile configurare un [ImageReference] [ net_imagereference] in modo esplicito:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>Elenco di immagini di macchine virtuali
Hello nella tabella seguente elenca le immagini di macchina virtuale Marketplace hello che sono compatibili con gli agenti nodo Batch disponibili hello dell'ultimo aggiornamento di questo articolo. È importante toonote che questo elenco non è definitivo poiché le immagini e gli agenti di nodo è possibile aggiungere o rimuovere in qualsiasi momento. È consigliabile che le applicazioni di Batch e i servizi utilizzino sempre [list_node_agent_skus] [ py_list_skus] (Python) e [ListNodeAgentSkus] [ net_list_skus] Toodetermine (batch .NET) e scegliere tra hello SKU attualmente disponibili.

> [!WARNING]
> Hello segue l'elenco può cambiare in qualsiasi momento. Utilizzare sempre hello **agente nodo elenco SKU** metodi disponibili in toolist API Batch hello hello compatibile macchina virtuale e l'agente di nodo SKU quando si eseguono i processi Batch.
>
>

| **Autore** | **Offerta** | **SKU dell'immagine** | **Versione** | **ID dello SKU dell'agente del nodo** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | più recenti | batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | più recenti | batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | più recenti | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | più recenti | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | più recenti | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1 | più recenti | batch.node.centos 7 |
| OpenLogic | CentOS | 7,2 | più recenti | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.0 | più recenti | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7,2 | più recenti | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | più recenti | batch.node.opensuse 13.2 |
| SUSE | openSUSE-Leap | 42.1 | più recenti | batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | più recenti | batch.node.opensuse 42.1 |
| SUSE | SLES-HPC | 12-SP1 | più recenti | batch.node.opensuse 42.1 |
| microsoft-ads | linux-data-science-vm | linuxdsvm | più recenti | batch.node.centos 7 |
| microsoft-ads | standard-data-science-vm | standard-data-science-vm | più recenti | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008 R2-SP1 | più recenti | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | più recenti | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | più recenti | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter | più recenti | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter-with-Containers | più recenti | batch.node.windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>La connessione dei nodi tooLinux tramite SSH
Durante lo sviluppo o durante la risoluzione dei problemi, potrebbe essere necessario toosign nei nodi toohello del pool. A differenza dei nodi di calcolo di Windows, è possibile utilizzare i nodi tooLinux tooconnect Remote Desktop Protocol (RDP). In alternativa, hello servizio Batch consente l'accesso SSH in ogni nodo per la connessione remota.

Hello seguente frammento di codice Python crea un utente in ogni nodo in un pool, che è necessario per la connessione remota. Stampa quindi le informazioni sulla connessione per ogni nodo hello sicura shell (SSH).

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

Di seguito è riportato un output per il codice precedente hello per un pool che contiene quattro nodi di Linux:

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

Invece di una password, è possibile specificare una chiave pubblica SSH durante la creazione di un utente in un nodo. In hello Python SDK, usare hello **ssh_public_key** parametro [ComputeNodeUser][py_computenodeuser]. In .NET, usare hello [ComputeNodeUser][net_computenodeuser].[ Parametri SshPublicKey] [ net_ssh_key] proprietà.

## <a name="pricing"></a>Prezzi
Azure Batch è basato sulla tecnologia di Servizi cloud di Azure e di Macchine virtuali di Azure. il servizio Batch stesso Hello è offerto gratuitamente, vengono addebitati solo i hello indica le risorse che utilizzano le soluzioni di Batch di calcolo. Quando si sceglie **configurazione di servizi Cloud**, vengono addebitati in base a hello [prezzi servizi Cloud] [ cloud_services_pricing] struttura. Quando si sceglie **configurazione della macchina virtuale**, vengono addebitati in base a hello [prezzi-macchine virtuali] [ vm_pricing] struttura. 

Se si distribuiscono applicazioni tooyour Batch nodi [pacchetti di applicazioni](batch-application-packages.md), verranno inoltre addebitati il costo per le risorse di archiviazione di Azure hello che utilizzano i pacchetti di applicazioni. In generale, i costi di archiviazione di Azure hello sono minimi. 

## <a name="next-steps"></a>Passaggi successivi
### <a name="batch-python-tutorial"></a>Esercitazione su Python per Batch
Per un'esercitazione più dettagliata su come toowork con Batch usando Python, estrazione [introduzione client Python di Azure Batch hello](batch-python-tutorial.md). Esso correlato [nell'esempio di codice] [ github_samples_pyclient] include una funzione di supporto, `get_vm_config_for_distro`, un'altra tecnica tooobtain che mostra una configurazione della macchina virtuale.

### <a name="batch-python-code-samples"></a>Esempi di codice Batch Python
Hello [esempi di codice Python] [ github_samples_py] in hello [esempi di azure batch] [ github_samples] il repository in GitHub contiene script che mostrano come tooperform operazioni di Batch comuni, ad esempio pool di processi e creazione di attività. Hello [Leggimi] [ github_py_readme] che vengono forniti esempi di Python hello contiene informazioni dettagliate su come tooinstall hello necessari pacchetti.

### <a name="batch-forum"></a>Forum di Batch
Hello [Forum di Azure Batch] [ forum] su MSDN è un ottimo posizionare toodiscuss Batch e porre domande sul servizio hello. Leggere i post aggiunti e inviare domande durante le procedure di compilazione di soluzioni Batch.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
