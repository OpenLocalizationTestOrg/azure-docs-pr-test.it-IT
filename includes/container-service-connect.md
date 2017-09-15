# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="49889-101">Stabilire una connessione remota a un cluster Kubernetes, DC/OS o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="49889-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="49889-102">Dopo aver creato un cluster del servizio contenitore di Azure è necessario connettersi al cluster per distribuire e gestire i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="49889-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="49889-103">Questo articolo descrive come connettersi alla VM master del cluster da un computer remoto.</span><span class="sxs-lookup"><span data-stu-id="49889-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="49889-104">I cluster Kubernetes, DC/OS e Docker Swarm forniscono localmente endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="49889-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="49889-105">Per Kubernetes, questo endpoint viene esposto in modo sicuro in Internet ed è possibile accedervi eseguendo lo strumento da riga di comando `kubectl` da qualsiasi computer connesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="49889-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="49889-106">Per DC/OS e Docker Swarm, è consigliabile creare un tunnel Secure Shell (SSH) dal computer locale al sistema di gestione cluster.</span><span class="sxs-lookup"><span data-stu-id="49889-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="49889-107">Dopo la creazione del tunnel, è possibile eseguire comandi che usano gli endpoint HTTP e visualizzare l'interfaccia Web dell'agente di orchestrazione (se disponibile) dal sistema locale.</span><span class="sxs-lookup"><span data-stu-id="49889-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="49889-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="49889-108">Prerequisites</span></span>

* <span data-ttu-id="49889-109">Un cluster Kubernetes, DC/OS o Docker Swarm [distribuito nel servizio contenitore di Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="49889-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="49889-110">File di chiave privata SSH RSA, corrispondente alla chiave pubblica aggiunta al cluster durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="49889-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="49889-111">Questi comandi presuppongono che la chiave privata SSH si trovi in `$HOME/.ssh/id_rsa` nel computer.</span><span class="sxs-lookup"><span data-stu-id="49889-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="49889-112">Per altre informazioni, vedere le istruzioni per [macOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o per [Windows](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="49889-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="49889-113">Se la connessione SSH non funziona, potrebbe essere necessario [reimpostare le chiavi SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="49889-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="49889-114">Connettersi a un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="49889-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="49889-115">Seguire questi passaggi per installare e configurare `kubectl` nel computer.</span><span class="sxs-lookup"><span data-stu-id="49889-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="49889-116">In Linux o macOS potrebbe essere necessario eseguire i comandi in questa sezione usando `sudo`.</span><span class="sxs-lookup"><span data-stu-id="49889-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="49889-117">Installare kubectl</span><span class="sxs-lookup"><span data-stu-id="49889-117">Install kubectl</span></span>
<span data-ttu-id="49889-118">Un modo per installare questo strumento è usare il comando `az acs kubernetes install-cli` dell'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="49889-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="49889-119">Per eseguire questo comando, assicurarsi di avere [installato](/cli/azure/install-az-cli2) la versione più recente dell'interfaccia della riga di comando di Azure 2.0 e di avere effettuato l'accesso a un account Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="49889-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="49889-120">In alternativa, è possibile scaricare il client `kubectl` più recente direttamente dalla [pagina delle versioni di Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="49889-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="49889-121">Per altre informazioni, vedere [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Installazione e configurazione di kubectl).</span><span class="sxs-lookup"><span data-stu-id="49889-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="49889-122">Scaricare le credenziali del cluster</span><span class="sxs-lookup"><span data-stu-id="49889-122">Download cluster credentials</span></span>
<span data-ttu-id="49889-123">Dopo aver installato `kubectl`, è necessario copiare le credenziali del cluster nel computer.</span><span class="sxs-lookup"><span data-stu-id="49889-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="49889-124">Un modo per ottenere le credenziali è con il comando `az acs kubernetes get-credentials`.</span><span class="sxs-lookup"><span data-stu-id="49889-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="49889-125">Passare il nome del gruppo di risorse e il nome della risorsa del servizio contenitore:</span><span class="sxs-lookup"><span data-stu-id="49889-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="49889-126">Questo comando scarica le credenziali del cluster in `$HOME/.kube/config` dove si prevede che sia disponibile `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="49889-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="49889-127">In alternativa è possibile usare `scp` per copiare in modo sicuro i file da `$HOME/.kube/config` nella VM master al computer locale.</span><span class="sxs-lookup"><span data-stu-id="49889-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="49889-128">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="49889-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="49889-129">Se si esegue questa operazione in Windows, è possibile usare Bash su Ubuntu in Windows, il client di copia file sicura PuTTY o uno strumento simile.</span><span class="sxs-lookup"><span data-stu-id="49889-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="49889-130">Usare kubectl</span><span class="sxs-lookup"><span data-stu-id="49889-130">Use kubectl</span></span>

<span data-ttu-id="49889-131">Dopo aver configurato `kubectl`, testare la connessione elencando i nodi nel cluster:</span><span class="sxs-lookup"><span data-stu-id="49889-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="49889-132">È possibile provare altri comandi `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="49889-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="49889-133">È ad esempio possibile visualizzare il dashboard Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="49889-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="49889-134">Eseguire prima un proxy per il server API Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="49889-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="49889-135">L'interfaccia utente di Kubernetes è ora disponibile all'indirizzo: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="49889-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="49889-136">Per altre informazioni, vedere la [Guida rapida di Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="49889-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="49889-137">Connettersi a un cluster DC/OS o Swarm</span><span class="sxs-lookup"><span data-stu-id="49889-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="49889-138">Per usare i cluster DC/OS e Docker Swarm distribuiti dal servizio contenitore di Azure, seguire queste istruzioni per creare un tunnel SSH dal sistema Linux, macOS o Windows locale.</span><span class="sxs-lookup"><span data-stu-id="49889-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="49889-139">Queste istruzioni sono incentrate sul tunneling del traffico TCP su SSH.</span><span class="sxs-lookup"><span data-stu-id="49889-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="49889-140">È anche possibile avviare una sessione SSH interattiva con uno dei sistemi interni di gestione dei cluster, ma questa opzione non è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="49889-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="49889-141">L'intervento diretto su un sistema interno comporta il rischio di modifiche accidentali alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="49889-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="49889-142">Creare un tunnel SSH in Linux o macOS</span><span class="sxs-lookup"><span data-stu-id="49889-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="49889-143">Quando si crea un tunnel SSH in Linux o macOS, prima di tutto è necessario individuare il nome DNS pubblico dei master con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="49889-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="49889-144">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="49889-144">Follow these steps:</span></span>


1. <span data-ttu-id="49889-145">Nel [portale di Azure](https://portal.azure.com) passare al gruppo di risorse che contiene il cluster del servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="49889-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="49889-146">Espandere il gruppo di risorse in modo che vengano visualizzate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="49889-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="49889-147">Fare clic sulla risorsa del **servizio contenitore** e quindi su **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="49889-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="49889-148">Viene visualizzato il **Nome di dominio completo master** del cluster in **Informazioni di base**.</span><span class="sxs-lookup"><span data-stu-id="49889-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="49889-149">Salvare questo nome per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="49889-149">Save this name for later use.</span></span> 

    ![Nome DNS pubblico](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="49889-151">In alternativa, eseguire il comando `az acs show` nel servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="49889-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="49889-152">Cercare la proprietà **Master Profile:fqdn** nell'output del comando.</span><span class="sxs-lookup"><span data-stu-id="49889-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="49889-153">Aprire ora una shell ed eseguire il comando `ssh` specificando i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="49889-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="49889-154">**LOCAL_PORT** è la porta TCP sul lato server del tunnel a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="49889-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="49889-155">Per Swarm, impostare questo valore su 2375.</span><span class="sxs-lookup"><span data-stu-id="49889-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="49889-156">Per DC/OS, impostare questo valore su 80.</span><span class="sxs-lookup"><span data-stu-id="49889-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="49889-157">**REMOTE_PORT** è la porta dell'endpoint da esporre.</span><span class="sxs-lookup"><span data-stu-id="49889-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="49889-158">Per Swarm, usare la porta 2375.</span><span class="sxs-lookup"><span data-stu-id="49889-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="49889-159">Per DC/OS usare la porta 80.</span><span class="sxs-lookup"><span data-stu-id="49889-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="49889-160">**USERNAME** è il nome utente specificato al momento della distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="49889-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="49889-161">**DNSPREFIX** è il prefisso DNS specificato al momento della distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="49889-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="49889-162">**REGION** è l'area in cui si trova il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="49889-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="49889-163">**PATH_TO_PRIVATE_KEY** [FACOLTATIVO] è il percorso della chiave privata che corrisponde alla chiave pubblica specificata durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="49889-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="49889-164">Usare questa opzione con il flag `-i`.</span><span class="sxs-lookup"><span data-stu-id="49889-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="49889-165">La porta di connessione SSH è la 2200, non la porta 22 standard.</span><span class="sxs-lookup"><span data-stu-id="49889-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="49889-166">In un cluster con più di una VM master, si tratta della porta di connessione per la prima VM master.</span><span class="sxs-lookup"><span data-stu-id="49889-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="49889-167">Il comando viene completato senza output.</span><span class="sxs-lookup"><span data-stu-id="49889-167">The command returns without output.</span></span>

<span data-ttu-id="49889-168">Vedere gli esempi per DC/OS e Swarm nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="49889-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="49889-169">Tunnel DC/OS</span><span class="sxs-lookup"><span data-stu-id="49889-169">DC/OS tunnel</span></span>
<span data-ttu-id="49889-170">Per aprire un tunnel per endpoint DC/OS, eseguire un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="49889-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="49889-171">Verificare che non sia presente un altro processo locale che associa la porta 80.</span><span class="sxs-lookup"><span data-stu-id="49889-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="49889-172">Se necessario, è possibile specificare una porta locale diversa dalla porta 80, ad esempio la porta 8080.</span><span class="sxs-lookup"><span data-stu-id="49889-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="49889-173">È tuttavia possibile che alcuni collegamenti dell'interfaccia utente Web non funzionino quando si usa questa porta.</span><span class="sxs-lookup"><span data-stu-id="49889-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="49889-174">È ora possibile accedere agli endpoint DC/OS dal sistema locale tramite gli URL (presupponendo che la porta locale sia 80):</span><span class="sxs-lookup"><span data-stu-id="49889-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="49889-175">Controller di dominio/sistema operativo: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="49889-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="49889-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="49889-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="49889-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="49889-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="49889-178">In modo analogo, è possibile raggiungere le API REST per ogni applicazione attraverso questo tunnel.</span><span class="sxs-lookup"><span data-stu-id="49889-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="49889-179">Tunnel Swarm</span><span class="sxs-lookup"><span data-stu-id="49889-179">Swarm tunnel</span></span>
<span data-ttu-id="49889-180">Per aprire un tunnel per gli endpoint Swarm, eseguire un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="49889-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="49889-181">Verificare che non sia presente un altro processo locale che associa la porta 2375.</span><span class="sxs-lookup"><span data-stu-id="49889-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="49889-182">Se il daemon Docker viene eseguito in locale, ad esempio, per impostazione predefinita usa la porta 2375.</span><span class="sxs-lookup"><span data-stu-id="49889-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="49889-183">Se necessario, è possibile specificare una porta locale diversa dalla porta 2375.</span><span class="sxs-lookup"><span data-stu-id="49889-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="49889-184">È ora possibile accedere al cluster Docker Swarm usando l'interfaccia della riga di comando di Docker nel sistema locale.</span><span class="sxs-lookup"><span data-stu-id="49889-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="49889-185">Per istruzioni sull'installazione, vedere [Install Docker](https://docs.docker.com/engine/installation/) (Installare Docker).</span><span class="sxs-lookup"><span data-stu-id="49889-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="49889-186">Impostare la variabile di ambiente DOCKER_HOST sulla porta locale configurata per il tunnel.</span><span class="sxs-lookup"><span data-stu-id="49889-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="49889-187">Eseguire i comandi di Docker che effettuano il tunneling al cluster Docker Swarm,</span><span class="sxs-lookup"><span data-stu-id="49889-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="49889-188">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="49889-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="49889-189">Creare un tunnel SSH in Windows</span><span class="sxs-lookup"><span data-stu-id="49889-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="49889-190">Esistono più opzioni per creare i tunnel SSH in Windows.</span><span class="sxs-lookup"><span data-stu-id="49889-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="49889-191">Se si esegue Bash su Ubuntu in Windows o uno strumento simile, è possibile seguire le istruzioni relative al tunneling SSH riportate più indietro in questo articolo per macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="49889-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="49889-192">Come alternativa in Windows, questa sezione descrive come usare PuTTY per creare il tunnel.</span><span class="sxs-lookup"><span data-stu-id="49889-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="49889-193">[Scaricare PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) nel sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="49889-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="49889-194">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="49889-194">Run the application.</span></span>

3. <span data-ttu-id="49889-195">Immettere un nome host che include il nome utente dell'amministratore cluster e il nome DNS pubblico del primo master nel cluster.</span><span class="sxs-lookup"><span data-stu-id="49889-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="49889-196">Il **nome host** è simile a `azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="49889-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="49889-197">Immettere 2200 nel campo **Port**.</span><span class="sxs-lookup"><span data-stu-id="49889-197">Enter 2200 for the **Port**.</span></span>

    ![Configurazione PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="49889-199">Selezionare **SSH > Auth**.</span><span class="sxs-lookup"><span data-stu-id="49889-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="49889-200">Aggiungere un percorso al file di chiave privata (formato ppk) per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="49889-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="49889-201">È possibile usare uno strumento come [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) per generare questo file dalla chiave SSH usata per creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="49889-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![Configurazione PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="49889-203">Selezionare **SSH > Tunnels** (Tunnel) e configurare le porte inoltrate seguenti:</span><span class="sxs-lookup"><span data-stu-id="49889-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="49889-204">**Source Port** (Porta di origine): usare 80 per DC/OS o 2375 per Swarm.</span><span class="sxs-lookup"><span data-stu-id="49889-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="49889-205">**Destination:** usare localhost:80 per il controller di dominio/sistema operativo o localhost:2375 per Swarm.</span><span class="sxs-lookup"><span data-stu-id="49889-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="49889-206">L'esempio seguente è configurato per DC/OS, ma avrà un aspetto simile anche per Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="49889-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="49889-207">La porta 80 non deve essere usata quando si crea il tunnel.</span><span class="sxs-lookup"><span data-stu-id="49889-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configurazione PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="49889-209">Al termine, fare clic su **Session > Save** (Sessione > Salva) per salvare la configurazione di connessione.</span><span class="sxs-lookup"><span data-stu-id="49889-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="49889-210">Fare clic su **Open** (Apri) per connettersi alla sessione PuTTY.</span><span class="sxs-lookup"><span data-stu-id="49889-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="49889-211">Dopo la connessione, è possibile visualizzare la configurazione della porta nel registro eventi di PuTTY.</span><span class="sxs-lookup"><span data-stu-id="49889-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![Log eventi di PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="49889-213">Dopo aver configurato il tunnel per DC/OS, è possibile accedere agli endpoint correlati all'indirizzo:</span><span class="sxs-lookup"><span data-stu-id="49889-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="49889-214">Controller di dominio/sistema operativo: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="49889-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="49889-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="49889-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="49889-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="49889-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="49889-217">Dopo aver configurato il tunnel per Docker Swarm, aprire le impostazioni di Windows per configurare una variabile di ambiente di sistema denominata `DOCKER_HOST` con un valore di `:2375`.</span><span class="sxs-lookup"><span data-stu-id="49889-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="49889-218">Sarà quindi possibile accedere al cluster Swarm dall'interfaccia della riga di comando di Docker.</span><span class="sxs-lookup"><span data-stu-id="49889-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49889-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49889-219">Next steps</span></span>
<span data-ttu-id="49889-220">Distribuire e gestire contenitori nel cluster:</span><span class="sxs-lookup"><span data-stu-id="49889-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="49889-221">Uso del servizio contenitore di Azure e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="49889-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="49889-222">Gestione di contenitori tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="49889-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="49889-223">Gestione dei contenitori con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="49889-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

