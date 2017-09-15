# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="dbd23-101">Ridimensionare i nodi agente in un cluster del servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="dbd23-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="dbd23-102">Dopo aver [distribuito un cluster del servizio contenitore di Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), potrebbe essere necessario modificare il numero di nodi agente.</span><span class="sxs-lookup"><span data-stu-id="dbd23-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="dbd23-103">Ad esempio, potrebbero essere necessari più agenti in modo da eseguire più applicazioni o istanze contenitore.</span><span class="sxs-lookup"><span data-stu-id="dbd23-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="dbd23-104">È possibile modificare il numero di nodi agente in un cluster DC/OS, Docker Swarm o Kubernetes tramite il portale di Azure o l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="dbd23-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="dbd23-105">Ridimensionare con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dbd23-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="dbd23-106">Nel [portale di Azure](https://portal.azure.com), passare a **Servizi contenitore** e fare clic sul servizio contenitore da modificare.</span><span class="sxs-lookup"><span data-stu-id="dbd23-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="dbd23-107">Nel pannello **Servizio contenitore** fare clic su **Agenti**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="dbd23-108">In **Conteggio macchine virtuali** immettere il numero desiderato di nodi di agenti.</span><span class="sxs-lookup"><span data-stu-id="dbd23-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![Ridimensionare un pool nel portale](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="dbd23-110">Per salvare la configurazione, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="dbd23-111">Ridimensionare con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dbd23-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="dbd23-112">Assicurarsi di avere [installato](/cli/azure/install-az-cli2) la versione più recente dell'interfaccia della riga di comando di Azure 2.0 e di avere eseguito l'accesso a un account Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="dbd23-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="dbd23-113">Visualizzare il numero di agenti corrente</span><span class="sxs-lookup"><span data-stu-id="dbd23-113">See the current agent count</span></span>
<span data-ttu-id="dbd23-114">Per visualizzare il numero di agenti attualmente presenti nel cluster, eseguire il comando `az acs show`.</span><span class="sxs-lookup"><span data-stu-id="dbd23-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="dbd23-115">Così facendo viene mostrata la configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-115">This shows the cluster configuration.</span></span> <span data-ttu-id="dbd23-116">Ad esempio, il comando seguente mostra la configurazione del servizio contenitore denominato `containerservice-myACSName` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dbd23-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="dbd23-117">Il comando restituisce il numero di agenti nel valore `Count` in `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="dbd23-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="dbd23-118">Usare il comando az acs scale</span><span class="sxs-lookup"><span data-stu-id="dbd23-118">Use the az acs scale command</span></span>
<span data-ttu-id="dbd23-119">Per modificare il numero di nodi dell'agente, eseguire il comando `az acs scale` e indicare il **gruppo di risorse**, il **nome del servizio contenitore** e il **numero di nuovi agenti desiderato**.</span><span class="sxs-lookup"><span data-stu-id="dbd23-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="dbd23-120">Se si specifica un numero più piccolo è possibile ridurre le prestazioni, mentre se si specifica un numero più grande è possibile aumentarle.</span><span class="sxs-lookup"><span data-stu-id="dbd23-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="dbd23-121">Ad esempio, per modificare il numero di agenti nel cluster precedente a 10, digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dbd23-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="dbd23-122">L'interfaccia della riga di comando di Azure 2.0 restituisce una stringa JSON che rappresenta la nuova configurazione del servizio contenitore, incluso il nuovo numero di agenti.</span><span class="sxs-lookup"><span data-stu-id="dbd23-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="dbd23-123">Per ulteriori opzioni di comandi, eseguire `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="dbd23-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="dbd23-124">Considerazioni sulla scalabilità</span><span class="sxs-lookup"><span data-stu-id="dbd23-124">Scaling considerations</span></span>

* <span data-ttu-id="dbd23-125">Il numero di nodi agente deve essere compreso tra 1 e 100 inclusi.</span><span class="sxs-lookup"><span data-stu-id="dbd23-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="dbd23-126">La quota di core può limitare il numero di nodi agente in un cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="dbd23-127">Le operazioni di scalabilità del nodo agente vengono applicate a un set di scalabilità di macchine virtuali di Azure che contiene il pool dell'agente.</span><span class="sxs-lookup"><span data-stu-id="dbd23-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="dbd23-128">In un cluster DC/OS, le operazioni illustrate in questo articolo consentono di ridimensionare solo i nodi di agenti nel pool privato.</span><span class="sxs-lookup"><span data-stu-id="dbd23-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="dbd23-129">A seconda dell'agente di orchestrazione distribuito nel cluster, è possibile ridimensionare separatamente il numero di istanze di un contenitore in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd23-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="dbd23-130">Ad esempio, in un cluster DC/OS, usare l'[interfaccia utente di Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) per modificare il numero di istanze di un'applicazione contenitore.</span><span class="sxs-lookup"><span data-stu-id="dbd23-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="dbd23-131">Attualmente, non è supportata la scalabilità automatica dei nodi di agenti in un cluster del servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="dbd23-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbd23-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbd23-132">Next steps</span></span>
* <span data-ttu-id="dbd23-133">Vedere [altri esempi](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) dell'uso di comandi dell'interfaccia della riga di comando di Azure 2.0 con il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd23-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="dbd23-134">Ulteriori informazioni sui [pool di agenti DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd23-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

