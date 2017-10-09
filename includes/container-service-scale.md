# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="ae6d6-101">Ridimensionare i nodi agente in un cluster del servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="ae6d6-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="ae6d6-102">Dopo aver [distribuzione di un cluster il servizio contenitore di Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), potrebbe essere necessario numero hello toochange dei nodi dell'agente.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="ae6d6-103">Ad esempio, potrebbero essere necessari più agenti in modo da eseguire più applicazioni o istanze contenitore.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="ae6d6-104">È possibile modificare il numero di hello di nodi dell'agente in un cluster di controller di dominio o del sistema operativo, Docker Swarm o Kubernetes utilizzando hello portale di Azure o hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="ae6d6-105">Scalabilità con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ae6d6-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="ae6d6-106">In hello [portale di Azure](https://portal.azure.com), cercare **servizi contenitore**, quindi fare clic su servizio di contenitore hello che si desidera toomodify.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="ae6d6-107">In hello **servizio contenitore** pannello, fare clic su **agenti**.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="ae6d6-108">In **conteggio VM**, immettere il numero desiderato di hello dei nodi di agenti.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Ridimensionare un pool nel portale di hello](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="ae6d6-110">configurazione di hello toosave, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="ae6d6-111">Scalabilità con hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ae6d6-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="ae6d6-112">Assicurarsi che si [installato](/cli/azure/install-az-cli2) hello 2.0 CLI di Azure più recenti e registrato nel tooan account azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="ae6d6-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="ae6d6-113">Vedere il numero di agenti corrente di hello</span><span class="sxs-lookup"><span data-stu-id="ae6d6-113">See hello current agent count</span></span>
<span data-ttu-id="ae6d6-114">numero di hello toosee di agenti attualmente cluster hello, esegue hello `az acs show` comando.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="ae6d6-115">Verrà visualizzata configurazione cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="ae6d6-116">Ad esempio, hello comando Mostra hello configurazione del servizio di contenitore hello denominato seguente `containerservice-myACSName` nel gruppo di risorse hello `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ae6d6-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="ae6d6-117">comando Hello restituisce il numero di hello degli agenti in hello `Count` valore `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="ae6d6-118">Utilizzare hello az comando scala acs</span><span class="sxs-lookup"><span data-stu-id="ae6d6-118">Use hello az acs scale command</span></span>
<span data-ttu-id="ae6d6-119">numero di hello toochange dei nodi di agente, eseguire hello `az acs scale` hello comando e specificare **gruppo di risorse**, **nome del servizio contenitore**, hello desiderato e **nuovo numero di agenti**.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="ae6d6-120">Se si specifica un numero più piccolo è possibile ridurre le prestazioni, mentre se si specifica un numero più grande è possibile aumentarle.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="ae6d6-121">Ad esempio, toochange hello numero di agenti in hello too10 cluster precedente, hello tipo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ae6d6-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="ae6d6-122">Hello Azure CLI 2.0 restituisce una stringa JSON che rappresenta la nuova hello-configurazione del servizio di contenitore hello, incluso il numero di hello nuovo agente.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="ae6d6-123">Per ulteriori opzioni di comandi, eseguire `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="ae6d6-124">Considerazioni sulla scalabilità</span><span class="sxs-lookup"><span data-stu-id="ae6d6-124">Scaling considerations</span></span>

* <span data-ttu-id="ae6d6-125">numero di Hello dei nodi dell'agente deve essere compreso tra 1 e 100 inclusi.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="ae6d6-126">La quota di core è possibile limitare il numero di hello dei nodi dell'agente in un cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="ae6d6-127">Le operazioni di ridimensionamento nodo agente vengono applicati tooan set di scalabilità della macchina virtuale di Azure che contiene il pool di agenti hello.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="ae6d6-128">In un cluster di controller di dominio o del sistema operativo, vengono ridimensionati solo i nodi dell'agente nel pool privata hello dalle operazioni hello illustrate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="ae6d6-129">A seconda di orchestrator hello che la distribuzione del cluster, è possibile ridimensionare separatamente numero hello di istanze di un contenitore in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="ae6d6-130">Ad esempio, in un cluster di controller di dominio o del sistema operativo, utilizzare hello [dell'interfaccia utente maratona](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) numero hello toochange di istanze di un'applicazione contenitore.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="ae6d6-131">Attualmente, non è supportata la scalabilità automatica dei nodi di agenti in un cluster del servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae6d6-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ae6d6-132">Next steps</span></span>
* <span data-ttu-id="ae6d6-133">Vedere [altri esempi](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) dell'uso di comandi dell'interfaccia della riga di comando di Azure 2.0 con il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="ae6d6-134">Ulteriori informazioni sui [pool di agenti DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae6d6-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

