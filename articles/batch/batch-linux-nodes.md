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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="c8a8e-103">Eseguire il provisioning di nodi di calcolo Linux nei pool di Batch</span><span class="sxs-lookup"><span data-stu-id="c8a8e-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="c8a8e-104">È possibile utilizzare i carichi di lavoro di Azure Batch toorun calcolo parallelo nelle macchine virtuali Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="c8a8e-105">In questo articolo illustra in dettaglio come pool toocreate di Linux nodi di calcolo nel servizio Batch hello utilizzando entrambi hello [Python Batch] [ py_batch_package] e [.NET per Batch] [ api_net] librerie client.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="c8a8e-106">I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="c8a8e-107">Sono supportate nei pool di Batch creato tra 10 marzo 2016 e 5 luglio 2017 solo se il pool di hello è stato creato utilizzando una configurazione del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="c8a8e-108">Pool di batch creati too10 precedente marzo 2016 non supportano pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="c8a8e-109">Per ulteriori informazioni sull'utilizzo dell'applicazione pacchetti toodeploy i nodi di Batch tooyour applicazioni, vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="c8a8e-110">Configurazione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c8a8e-110">Virtual machine configuration</span></span>
<span data-ttu-id="c8a8e-111">Quando si crea un pool di nodi di calcolo in Batch, sono disponibili due opzioni da cui tooselect dimensione del nodo hello e sistema operativo: configurazione della macchina virtuale e la configurazione di servizi Cloud.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="c8a8e-112">**Cloud Services Configuration** (Configurazione servizi cloud) fornisce *solo*nodi di calcolo Windows.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="c8a8e-113">Dimensioni di nodo di calcolo disponibili sono elencate [dimensioni per i servizi Cloud](../cloud-services/cloud-services-sizes-specs.md), e i sistemi operativi disponibili sono elencati in hello [versioni del sistema operativo Guest Azure e matrice di compatibilità SDK](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="c8a8e-114">Quando si crea un pool che contiene i nodi di servizi Cloud di Azure, è possibile specificare dimensioni di nodo hello e hello famiglia del sistema operativo, che sono descritte nel hello indicato in precedenza gli articoli.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="c8a8e-115">Quando si creano pool di nodi di calcolo Windows, viene in genere usata l'opzione Servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="c8a8e-116">La **configurazione della macchina virtuale** fornisce immagini Linux e Windows per i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="c8a8e-117">Le dimensioni disponibili per i nodi di calcolo sono elencate in [Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) e [Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="c8a8e-118">Quando si crea un pool che contiene i nodi di configurazione della macchina virtuale, è necessario specificare dimensioni di hello di nodi di hello, riferimento all'immagine di macchina virtuale hello e toobe SKU hello Batch nodo agente installato nei nodi hello.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="c8a8e-119">Riferimento all'immagine della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c8a8e-119">Virtual machine image reference</span></span>
<span data-ttu-id="c8a8e-120">Hello servizio Batch Usa [set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="c8a8e-121">È possibile specificare un'immagine da hello [Azure Marketplace][vm_marketplace], o fornire un'immagine personalizzata che è stato preparato.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="c8a8e-122">Per informazioni dettagliate sulle immagini personalizzate, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="c8a8e-123">Quando si configura un riferimento all'immagine di macchina virtuale, specificare le proprietà di hello dell'immagine di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="c8a8e-124">Hello le proprietà seguenti è necessario quando si crea un riferimento all'immagine di macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="c8a8e-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="c8a8e-125">**Proprietà del riferimento all'immagine**</span><span class="sxs-lookup"><span data-stu-id="c8a8e-125">**Image reference properties**</span></span> | <span data-ttu-id="c8a8e-126">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="c8a8e-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="c8a8e-127">Autore</span><span class="sxs-lookup"><span data-stu-id="c8a8e-127">Publisher</span></span> |<span data-ttu-id="c8a8e-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="c8a8e-128">Canonical</span></span> |
| <span data-ttu-id="c8a8e-129">Offerta</span><span class="sxs-lookup"><span data-stu-id="c8a8e-129">Offer</span></span> |<span data-ttu-id="c8a8e-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-130">UbuntuServer</span></span> |
| <span data-ttu-id="c8a8e-131">SKU</span><span class="sxs-lookup"><span data-stu-id="c8a8e-131">SKU</span></span> |<span data-ttu-id="c8a8e-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="c8a8e-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="c8a8e-133">Versione</span><span class="sxs-lookup"><span data-stu-id="c8a8e-133">Version</span></span> |<span data-ttu-id="c8a8e-134">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="c8a8e-135">Maggiori informazioni su queste proprietà e come toolist Marketplace immagini in [Naviga e selezionare le immagini di macchina virtuale di Linux in Azure con CLI o PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c8a8e-136">Si noti che non tutte le immagini del Marketplace sono attualmente compatibili con Batch.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="c8a8e-137">Per altre informazioni, vedere [SKU dell'agente del nodo](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="c8a8e-138">SKU dell'agente del nodo</span><span class="sxs-lookup"><span data-stu-id="c8a8e-138">Node agent SKU</span></span>
<span data-ttu-id="c8a8e-139">agente di Hello Batch nodo è un programma che viene eseguito in ogni nodo nel pool di hello e fornisce l'interfaccia di comando e controllo hello tra nodo hello e il servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="c8a8e-140">Esistono diverse implementazioni dell'agente del nodo hello, noto come SKU, per sistemi operativi diversi.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="c8a8e-141">In pratica, quando si crea una configurazione della macchina virtuale, è innanzitutto necessario specificare riferimento all'immagine di macchina virtuale hello e quindi si specificare hello nodo agente tooinstall sull'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="c8a8e-142">Ogni SKU dell'agente del nodo è in genere compatibile con più immagini di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="c8a8e-143">Ecco alcuni esempi di SKU dell'agente del nodo:</span><span class="sxs-lookup"><span data-stu-id="c8a8e-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="c8a8e-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c8a8e-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="c8a8e-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-145">batch.node.centos 7</span></span>
* <span data-ttu-id="c8a8e-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="c8a8e-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8a8e-147">Non tutte le immagini di macchina virtuale sono disponibili in Marketplace hello sono compatibili con gli agenti nodo Batch attualmente disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="c8a8e-148">Usare l'agente di nodo disponibile hello toolist Batch SDK hello SKU e hello immagini di macchina virtuale a cui sono compatibili.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="c8a8e-149">Vedere hello [immagini di elenco di macchine virtuali](#list-of-virtual-machine-images) più avanti in questo articolo per ulteriori informazioni ed esempi di come tooretrieve un elenco di immagini valide in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="c8a8e-150">Creare un pool Linux: Batch Python</span><span class="sxs-lookup"><span data-stu-id="c8a8e-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="c8a8e-151">Hello frammento di codice seguente viene illustrato un esempio di hello toouse [libreria Client di Microsoft Azure Batch per Python] [ py_batch_package] toocreate un pool di Ubuntu Server nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="c8a8e-152">Fare riferimento alla documentazione per il modulo di Python Batch è reperibile in hello [azure.batch pacchetto] [ py_batch_docs] in lettura hello documenti.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="c8a8e-153">Questo frammento di codice crea in modo esplicito un metodo [ImageReference][py_imagereference], specificando tutte le rispettive proprietà, ovvero editore, offerta, SKU, versione.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="c8a8e-154">Nel codice di produzione, tuttavia, è consigliabile utilizzare hello [list_node_agent_skus] [ py_list_skus] toodetermine (metodo) e scegliere tra hello immagine e il nodo agente SKU combinazioni disponibili in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

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

<span data-ttu-id="c8a8e-155">Come accennato in precedenza, si consiglia invece di creare hello [ImageReference] [ py_imagereference] in modo esplicito, utilizzare hello [list_node_agent_skus] [ py_list_skus] metodo toodynamically scegliere hello è attualmente supportato combinazioni immagine agente/Marketplace di nodo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="c8a8e-156">Hello seguente mostra Python come toouse questo metodo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-156">hello following Python snippet shows how toouse this method.</span></span>

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

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="c8a8e-157">Creare un pool Linux: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="c8a8e-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="c8a8e-158">Hello frammento di codice seguente viene illustrato un esempio di hello toouse [.NET per Batch] [ nuget_batch_net] toocreate libreria client un pool di Ubuntu Server nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="c8a8e-159">È possibile trovare hello [la documentazione di riferimento di .NET per Batch] [ api_net] su MSDN.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="c8a8e-160">frammento di codice seguente Hello utilizza hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect metodo dall'elenco di hello di attualmente Marketplace immagine e il nodo agente SKU combinazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="c8a8e-161">Questa tecnica è utile perché elenco hello di combinazioni supportate potrebbe cambiare da tootime ora.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="c8a8e-162">in genere a causa dell'aggiunta di altre combinazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-162">Most commonly, supported combinations are added.</span></span>

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

<span data-ttu-id="c8a8e-163">Sebbene frammento precedente hello utilizza hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] metodo toodynamically elenco e selezionare da supportata immagine e il nodo combinazioni di SKU dell'agente (scelta consigliate), è inoltre possibile configurare un [ImageReference] [ net_imagereference] in modo esplicito:</span><span class="sxs-lookup"><span data-stu-id="c8a8e-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="c8a8e-164">Elenco di immagini di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c8a8e-164">List of virtual machine images</span></span>
<span data-ttu-id="c8a8e-165">Hello nella tabella seguente elenca le immagini di macchina virtuale Marketplace hello che sono compatibili con gli agenti nodo Batch disponibili hello dell'ultimo aggiornamento di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="c8a8e-166">È importante toonote che questo elenco non è definitivo poiché le immagini e gli agenti di nodo è possibile aggiungere o rimuovere in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="c8a8e-167">È consigliabile che le applicazioni di Batch e i servizi utilizzino sempre [list_node_agent_skus] [ py_list_skus] (Python) e [ListNodeAgentSkus] [ net_list_skus] Toodetermine (batch .NET) e scegliere tra hello SKU attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="c8a8e-168">Hello segue l'elenco può cambiare in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-168">hello following list may change at any time.</span></span> <span data-ttu-id="c8a8e-169">Utilizzare sempre hello **agente nodo elenco SKU** metodi disponibili in toolist API Batch hello hello compatibile macchina virtuale e l'agente di nodo SKU quando si eseguono i processi Batch.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="c8a8e-170">**Autore**</span><span class="sxs-lookup"><span data-stu-id="c8a8e-170">**Publisher**</span></span> | <span data-ttu-id="c8a8e-171">**Offerta**</span><span class="sxs-lookup"><span data-stu-id="c8a8e-171">**Offer**</span></span> | <span data-ttu-id="c8a8e-172">**SKU dell'immagine**</span><span class="sxs-lookup"><span data-stu-id="c8a8e-172">**Image SKU**</span></span> | <span data-ttu-id="c8a8e-173">**Versione**</span><span class="sxs-lookup"><span data-stu-id="c8a8e-173">**Version**</span></span> | <span data-ttu-id="c8a8e-174">**ID dello SKU dell'agente del nodo**</span><span class="sxs-lookup"><span data-stu-id="c8a8e-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="c8a8e-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="c8a8e-175">Canonical</span></span> | <span data-ttu-id="c8a8e-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-176">UbuntuServer</span></span> | <span data-ttu-id="c8a8e-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="c8a8e-177">14.04.5-LTS</span></span> | <span data-ttu-id="c8a8e-178">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-178">latest</span></span> | <span data-ttu-id="c8a8e-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c8a8e-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="c8a8e-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="c8a8e-180">Canonical</span></span> | <span data-ttu-id="c8a8e-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-181">UbuntuServer</span></span> | <span data-ttu-id="c8a8e-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="c8a8e-182">16.04.0-LTS</span></span> | <span data-ttu-id="c8a8e-183">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-183">latest</span></span> | <span data-ttu-id="c8a8e-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c8a8e-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="c8a8e-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="c8a8e-185">Credativ</span></span> | <span data-ttu-id="c8a8e-186">Debian</span><span class="sxs-lookup"><span data-stu-id="c8a8e-186">Debian</span></span> | <span data-ttu-id="c8a8e-187">8</span><span class="sxs-lookup"><span data-stu-id="c8a8e-187">8</span></span> | <span data-ttu-id="c8a8e-188">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-188">latest</span></span> | <span data-ttu-id="c8a8e-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="c8a8e-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="c8a8e-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c8a8e-190">OpenLogic</span></span> | <span data-ttu-id="c8a8e-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="c8a8e-191">CentOS</span></span> | <span data-ttu-id="c8a8e-192">7.0</span><span class="sxs-lookup"><span data-stu-id="c8a8e-192">7.0</span></span> | <span data-ttu-id="c8a8e-193">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-193">latest</span></span> | <span data-ttu-id="c8a8e-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="c8a8e-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c8a8e-195">OpenLogic</span></span> | <span data-ttu-id="c8a8e-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="c8a8e-196">CentOS</span></span> | <span data-ttu-id="c8a8e-197">7.1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-197">7.1</span></span> | <span data-ttu-id="c8a8e-198">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-198">latest</span></span> | <span data-ttu-id="c8a8e-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="c8a8e-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c8a8e-200">OpenLogic</span></span> | <span data-ttu-id="c8a8e-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="c8a8e-201">CentOS-HPC</span></span> | <span data-ttu-id="c8a8e-202">7.1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-202">7.1</span></span> | <span data-ttu-id="c8a8e-203">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-203">latest</span></span> | <span data-ttu-id="c8a8e-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="c8a8e-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c8a8e-205">OpenLogic</span></span> | <span data-ttu-id="c8a8e-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="c8a8e-206">CentOS</span></span> | <span data-ttu-id="c8a8e-207">7,2</span><span class="sxs-lookup"><span data-stu-id="c8a8e-207">7.2</span></span> | <span data-ttu-id="c8a8e-208">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-208">latest</span></span> | <span data-ttu-id="c8a8e-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="c8a8e-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="c8a8e-210">Oracle</span></span> | <span data-ttu-id="c8a8e-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="c8a8e-211">Oracle-Linux</span></span> | <span data-ttu-id="c8a8e-212">7.0</span><span class="sxs-lookup"><span data-stu-id="c8a8e-212">7.0</span></span> | <span data-ttu-id="c8a8e-213">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-213">latest</span></span> | <span data-ttu-id="c8a8e-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="c8a8e-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="c8a8e-215">Oracle</span></span> | <span data-ttu-id="c8a8e-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="c8a8e-216">Oracle-Linux</span></span> | <span data-ttu-id="c8a8e-217">7,2</span><span class="sxs-lookup"><span data-stu-id="c8a8e-217">7.2</span></span> | <span data-ttu-id="c8a8e-218">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-218">latest</span></span> | <span data-ttu-id="c8a8e-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="c8a8e-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="c8a8e-220">SUSE</span></span> | <span data-ttu-id="c8a8e-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c8a8e-221">openSUSE</span></span> | <span data-ttu-id="c8a8e-222">13.2</span><span class="sxs-lookup"><span data-stu-id="c8a8e-222">13.2</span></span> | <span data-ttu-id="c8a8e-223">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-223">latest</span></span> | <span data-ttu-id="c8a8e-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="c8a8e-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="c8a8e-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="c8a8e-225">SUSE</span></span> | <span data-ttu-id="c8a8e-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="c8a8e-226">openSUSE-Leap</span></span> | <span data-ttu-id="c8a8e-227">42.1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-227">42.1</span></span> | <span data-ttu-id="c8a8e-228">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-228">latest</span></span> | <span data-ttu-id="c8a8e-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="c8a8e-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="c8a8e-230">SUSE</span></span> | <span data-ttu-id="c8a8e-231">SLES</span><span class="sxs-lookup"><span data-stu-id="c8a8e-231">SLES</span></span> | <span data-ttu-id="c8a8e-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-232">12-SP1</span></span> | <span data-ttu-id="c8a8e-233">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-233">latest</span></span> | <span data-ttu-id="c8a8e-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="c8a8e-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="c8a8e-235">SUSE</span></span> | <span data-ttu-id="c8a8e-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="c8a8e-236">SLES-HPC</span></span> | <span data-ttu-id="c8a8e-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-237">12-SP1</span></span> | <span data-ttu-id="c8a8e-238">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-238">latest</span></span> | <span data-ttu-id="c8a8e-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="c8a8e-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="c8a8e-240">microsoft-ads</span></span> | <span data-ttu-id="c8a8e-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="c8a8e-241">linux-data-science-vm</span></span> | <span data-ttu-id="c8a8e-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="c8a8e-242">linuxdsvm</span></span> | <span data-ttu-id="c8a8e-243">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-243">latest</span></span> | <span data-ttu-id="c8a8e-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c8a8e-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="c8a8e-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="c8a8e-245">microsoft-ads</span></span> | <span data-ttu-id="c8a8e-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="c8a8e-246">standard-data-science-vm</span></span> | <span data-ttu-id="c8a8e-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="c8a8e-247">standard-data-science-vm</span></span> | <span data-ttu-id="c8a8e-248">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-248">latest</span></span> | <span data-ttu-id="c8a8e-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="c8a8e-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c8a8e-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c8a8e-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-251">WindowsServer</span></span> | <span data-ttu-id="c8a8e-252">2008 R2-SP1</span><span class="sxs-lookup"><span data-stu-id="c8a8e-252">2008-R2-SP1</span></span> | <span data-ttu-id="c8a8e-253">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-253">latest</span></span> | <span data-ttu-id="c8a8e-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="c8a8e-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c8a8e-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c8a8e-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-256">WindowsServer</span></span> | <span data-ttu-id="c8a8e-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c8a8e-257">2012-Datacenter</span></span> | <span data-ttu-id="c8a8e-258">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-258">latest</span></span> | <span data-ttu-id="c8a8e-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="c8a8e-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c8a8e-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c8a8e-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-261">WindowsServer</span></span> | <span data-ttu-id="c8a8e-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c8a8e-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="c8a8e-263">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-263">latest</span></span> | <span data-ttu-id="c8a8e-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="c8a8e-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c8a8e-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c8a8e-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-266">WindowsServer</span></span> | <span data-ttu-id="c8a8e-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c8a8e-267">2016-Datacenter</span></span> | <span data-ttu-id="c8a8e-268">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-268">latest</span></span> | <span data-ttu-id="c8a8e-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="c8a8e-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c8a8e-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c8a8e-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8a8e-271">WindowsServer</span></span> | <span data-ttu-id="c8a8e-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="c8a8e-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="c8a8e-273">più recenti</span><span class="sxs-lookup"><span data-stu-id="c8a8e-273">latest</span></span> | <span data-ttu-id="c8a8e-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="c8a8e-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="c8a8e-275">La connessione dei nodi tooLinux tramite SSH</span><span class="sxs-lookup"><span data-stu-id="c8a8e-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="c8a8e-276">Durante lo sviluppo o durante la risoluzione dei problemi, potrebbe essere necessario toosign nei nodi toohello del pool.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="c8a8e-277">A differenza dei nodi di calcolo di Windows, è possibile utilizzare i nodi tooLinux tooconnect Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="c8a8e-278">In alternativa, hello servizio Batch consente l'accesso SSH in ogni nodo per la connessione remota.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="c8a8e-279">Hello seguente frammento di codice Python crea un utente in ogni nodo in un pool, che è necessario per la connessione remota.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="c8a8e-280">Stampa quindi le informazioni sulla connessione per ogni nodo hello sicura shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

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

<span data-ttu-id="c8a8e-281">Di seguito è riportato un output per il codice precedente hello per un pool che contiene quattro nodi di Linux:</span><span class="sxs-lookup"><span data-stu-id="c8a8e-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="c8a8e-282">Invece di una password, è possibile specificare una chiave pubblica SSH durante la creazione di un utente in un nodo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="c8a8e-283">In hello Python SDK, usare hello **ssh_public_key** parametro [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="c8a8e-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="c8a8e-284">In .NET, usare hello [ComputeNodeUser][net_computenodeuser].[ Parametri SshPublicKey] [ net_ssh_key] proprietà.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="c8a8e-285">Prezzi</span><span class="sxs-lookup"><span data-stu-id="c8a8e-285">Pricing</span></span>
<span data-ttu-id="c8a8e-286">Azure Batch è basato sulla tecnologia di Servizi cloud di Azure e di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="c8a8e-287">il servizio Batch stesso Hello è offerto gratuitamente, vengono addebitati solo i hello indica le risorse che utilizzano le soluzioni di Batch di calcolo.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="c8a8e-288">Quando si sceglie **configurazione di servizi Cloud**, vengono addebitati in base a hello [prezzi servizi Cloud] [ cloud_services_pricing] struttura.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="c8a8e-289">Quando si sceglie **configurazione della macchina virtuale**, vengono addebitati in base a hello [prezzi-macchine virtuali] [ vm_pricing] struttura.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="c8a8e-290">Se si distribuiscono applicazioni tooyour Batch nodi [pacchetti di applicazioni](batch-application-packages.md), verranno inoltre addebitati il costo per le risorse di archiviazione di Azure hello che utilizzano i pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="c8a8e-291">In generale, i costi di archiviazione di Azure hello sono minimi.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c8a8e-292">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8a8e-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="c8a8e-293">Esercitazione su Python per Batch</span><span class="sxs-lookup"><span data-stu-id="c8a8e-293">Batch Python tutorial</span></span>
<span data-ttu-id="c8a8e-294">Per un'esercitazione più dettagliata su come toowork con Batch usando Python, estrazione [introduzione client Python di Azure Batch hello](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c8a8e-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="c8a8e-295">Esso correlato [nell'esempio di codice] [ github_samples_pyclient] include una funzione di supporto, `get_vm_config_for_distro`, un'altra tecnica tooobtain che mostra una configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="c8a8e-296">Esempi di codice Batch Python</span><span class="sxs-lookup"><span data-stu-id="c8a8e-296">Batch Python code samples</span></span>
<span data-ttu-id="c8a8e-297">Hello [esempi di codice Python] [ github_samples_py] in hello [esempi di azure batch] [ github_samples] il repository in GitHub contiene script che mostrano come tooperform operazioni di Batch comuni, ad esempio pool di processi e creazione di attività.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="c8a8e-298">Hello [Leggimi] [ github_py_readme] che vengono forniti esempi di Python hello contiene informazioni dettagliate su come tooinstall hello necessari pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="c8a8e-299">Forum di Batch</span><span class="sxs-lookup"><span data-stu-id="c8a8e-299">Batch forum</span></span>
<span data-ttu-id="c8a8e-300">Hello [Forum di Azure Batch] [ forum] su MSDN è un ottimo posizionare toodiscuss Batch e porre domande sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="c8a8e-301">Leggere i post aggiunti e inviare domande durante le procedure di compilazione di soluzioni Batch.</span><span class="sxs-lookup"><span data-stu-id="c8a8e-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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
