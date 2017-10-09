# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="bd542-101">Creare un cluster, Kubernetes, controller di dominio o del sistema operativo o Docker Swarm tooa connessione remota</span><span class="sxs-lookup"><span data-stu-id="bd542-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="bd542-102">Dopo aver creato un cluster il servizio contenitore di Azure, è necessario tooconnect toohello cluster toodeploy e gestire i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="bd542-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="bd542-103">In questo articolo viene descritto come tooconnect toohello master VM di hello cluster da un computer remoto.</span><span class="sxs-lookup"><span data-stu-id="bd542-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="bd542-104">i cluster di Kubernetes, controller di dominio/OS e Docker Swarm Hello includono localmente gli endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="bd542-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="bd542-105">Per Kubernetes, questo endpoint viene esposto in modo sicuro su internet hello ed è possibile accedervi tramite l'esecuzione di hello `kubectl` strumento da riga di comando da qualsiasi computer connesso a internet.</span><span class="sxs-lookup"><span data-stu-id="bd542-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="bd542-106">Per i controller di dominio/OS e Docker Swarm, è consigliabile creare un tunnel sicuro shell (SSH) dal sistema di Gestione cluster toohello computer locale.</span><span class="sxs-lookup"><span data-stu-id="bd542-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="bd542-107">Dopo aver stabilito il tunnel hello, è possibile eseguire comandi che utilizzano gli endpoint HTTP hello e web dell'interfaccia di orchestrator hello visualizzazione (se disponibile) dal sistema locale.</span><span class="sxs-lookup"><span data-stu-id="bd542-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bd542-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd542-108">Prerequisites</span></span>

* <span data-ttu-id="bd542-109">Un cluster Kubernetes, DC/OS o Docker Swarm [distribuito nel servizio contenitore di Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="bd542-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="bd542-110">SSH RSA file di chiave privata, corrispondente toohello pubblica toohello aggiunto chiave cluster durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bd542-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="bd542-111">Questi comandi presuppongono la chiave SSH privata hello in `$HOME/.ssh/id_rsa` nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bd542-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="bd542-112">Per altre informazioni, vedere le istruzioni per [macOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o per [Windows](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="bd542-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="bd542-113">Se la connessione SSH hello non funziona, potrebbe essere troppo [reimpostare le chiavi SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="bd542-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="bd542-114">Connettere il cluster di Kubernetes tooa</span><span class="sxs-lookup"><span data-stu-id="bd542-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="bd542-115">Seguire questi passaggi tooinstall e configurare `kubectl` nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bd542-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="bd542-116">In Linux o Mac OS, potrebbe essere necessario comandi hello toorun in questa sezione utilizzando `sudo`.</span><span class="sxs-lookup"><span data-stu-id="bd542-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="bd542-117">Installare kubectl</span><span class="sxs-lookup"><span data-stu-id="bd542-117">Install kubectl</span></span>
<span data-ttu-id="bd542-118">Un modo tooinstall questo strumento è hello toouse `az acs kubernetes install-cli` comando CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="bd542-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="bd542-119">toorun questo comando, assicurarsi che si [installato](/cli/azure/install-az-cli2) hello 2.0 CLI di Azure più recenti e registrato nell'account Azure tooan (`az login`).</span><span class="sxs-lookup"><span data-stu-id="bd542-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="bd542-120">In alternativa, è possibile scaricare hello più recente `kubectl` client direttamente dal hello [Kubernetes rilascia pagina](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="bd542-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="bd542-121">Per altre informazioni, vedere [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Installazione e configurazione di kubectl).</span><span class="sxs-lookup"><span data-stu-id="bd542-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="bd542-122">Scaricare le credenziali del cluster</span><span class="sxs-lookup"><span data-stu-id="bd542-122">Download cluster credentials</span></span>
<span data-ttu-id="bd542-123">Dopo aver `kubectl` installato, è necessario il computer tooyour le credenziali di toocopy hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="bd542-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="bd542-124">Le credenziali di un modo toodo get hello è con hello `az acs kubernetes get-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="bd542-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="bd542-125">Passare il nome di hello hello del gruppo di risorse e il nome di hello della risorsa del servizio contenitore hello:</span><span class="sxs-lookup"><span data-stu-id="bd542-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="bd542-126">Questo comando Scarica le credenziali del cluster hello troppo`$HOME/.kube/config`, dove `kubectl` si aspetta che lo trova toobe.</span><span class="sxs-lookup"><span data-stu-id="bd542-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="bd542-127">In alternativa, è possibile utilizzare `scp` toosecurely copia del file hello da `$HOME/.kube/config` computer hello master VM tooyour locale.</span><span class="sxs-lookup"><span data-stu-id="bd542-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="bd542-128">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="bd542-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="bd542-129">Se si utilizza Windows, è possibile utilizzare Bash in Ubuntu in Windows, i client per copie di file sicuri PuTTy hello o uno strumento simile.</span><span class="sxs-lookup"><span data-stu-id="bd542-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="bd542-130">Usare kubectl</span><span class="sxs-lookup"><span data-stu-id="bd542-130">Use kubectl</span></span>

<span data-ttu-id="bd542-131">Dopo aver `kubectl` configurato, testare la connessione hello elencare hello i nodi del cluster:</span><span class="sxs-lookup"><span data-stu-id="bd542-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="bd542-132">È possibile provare altri comandi `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="bd542-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="bd542-133">Ad esempio, è possibile visualizzare Kubernetes Dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="bd542-134">Eseguire prima di tutto un proxy server dell'API Kubernetes toohello:</span><span class="sxs-lookup"><span data-stu-id="bd542-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="bd542-135">Hello UI Kubernetes è ora disponibile all'indirizzo: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="bd542-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="bd542-136">Per ulteriori informazioni, vedere hello [Kubernetes introduttiva](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="bd542-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="bd542-137">Connettere il cluster di controller di dominio o del sistema operativo o sciame tooa</span><span class="sxs-lookup"><span data-stu-id="bd542-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="bd542-138">hello toouse DC/OS e cluster Docker Swarm distribuiti dal servizio di contenitore di Azure, seguire questi toocreate istruzioni un tunnel SSH dal sistema di Windows, Linux o macOS locale.</span><span class="sxs-lookup"><span data-stu-id="bd542-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="bd542-139">Queste istruzioni sono incentrate sul tunneling del traffico TCP su SSH.</span><span class="sxs-lookup"><span data-stu-id="bd542-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="bd542-140">È anche possibile avviare una sessione interattiva di SSH con uno dei sistemi di gestione di hello interne al cluster, ma non ti consigliamo di questa.</span><span class="sxs-lookup"><span data-stu-id="bd542-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="bd542-141">L'intervento diretto su un sistema interno comporta il rischio di modifiche accidentali alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="bd542-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="bd542-142">Creare un tunnel SSH in Linux o macOS</span><span class="sxs-lookup"><span data-stu-id="bd542-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="bd542-143">Hello prima cosa è quando si crea un tunnel SSH in Linux o macOS è toolocate hello nome DNS pubblico di schemi con bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="bd542-144">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bd542-144">Follow these steps:</span></span>


1. <span data-ttu-id="bd542-145">In hello [portale di Azure](https://portal.azure.com), selezionare il gruppo di risorse toohello che contiene il cluster del servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="bd542-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="bd542-146">Espandere il gruppo di risorse hello in modo che ogni risorsa è visualizzata.</span><span class="sxs-lookup"><span data-stu-id="bd542-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="bd542-147">Fare clic su hello **servizio contenitore** risorse e fare clic su **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="bd542-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="bd542-148">Hello **FQDN Master** di hello cluster viene visualizzato sotto **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="bd542-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="bd542-149">Salvare questo nome per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="bd542-149">Save this name for later use.</span></span> 

    ![Nome DNS pubblico](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="bd542-151">In alternativa, eseguire hello `az acs show` comando sul servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="bd542-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="bd542-152">Cercare hello **profilo Master: fqdn** proprietà nell'output del comando hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="bd542-153">Aprire una shell ed eseguire hello `ssh` comando specificando hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="bd542-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="bd542-154">**LOCAL_PORT** è sul lato servizio hello di hello tunnel tooconnect per la porta TCP hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="bd542-155">Per sciame, impostare questo too2375.</span><span class="sxs-lookup"><span data-stu-id="bd542-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="bd542-156">Per i controller di dominio o del sistema operativo, impostare questo too80.</span><span class="sxs-lookup"><span data-stu-id="bd542-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="bd542-157">**REMOTE_PORT** hello porta dell'endpoint hello che si desidera tooexpose.</span><span class="sxs-lookup"><span data-stu-id="bd542-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="bd542-158">Per Swarm, usare la porta 2375.</span><span class="sxs-lookup"><span data-stu-id="bd542-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="bd542-159">Per DC/OS usare la porta 80.</span><span class="sxs-lookup"><span data-stu-id="bd542-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="bd542-160">**Nome utente** hello utente nome fornito al momento della distribuzione cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="bd542-161">**DNSPREFIX** è un prefisso DNS hello fornito al momento della distribuzione cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="bd542-162">**AREA** hello area in cui si trova il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bd542-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="bd542-163">**PATH_TO_PRIVATE_KEY** [facoltativo] è hello percorso toohello chiave privata corrispondente toohello chiave pubblica fornita al momento della creazione del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="bd542-164">Utilizzare questa opzione con hello `-i` flag.</span><span class="sxs-lookup"><span data-stu-id="bd542-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="bd542-165">la porta di connessione SSH Hello è 2200 e non hello porta standard 22.</span><span class="sxs-lookup"><span data-stu-id="bd542-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="bd542-166">In un cluster con più di una macchina virtuale master, si tratta di hello connessione porta toohello prima master macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bd542-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="bd542-167">comando Hello restituisce senza output.</span><span class="sxs-lookup"><span data-stu-id="bd542-167">hello command returns without output.</span></span>

<span data-ttu-id="bd542-168">Vedere esempi hello per controller di dominio/OS e sciame in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="bd542-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="bd542-169">Tunnel DC/OS</span><span class="sxs-lookup"><span data-stu-id="bd542-169">DC/OS tunnel</span></span>
<span data-ttu-id="bd542-170">tooopen un tunnel per gli endpoint di controller di dominio o del sistema operativo, eseguire un comando simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="bd542-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="bd542-171">Verificare che non sia presente un altro processo locale che associa la porta 80.</span><span class="sxs-lookup"><span data-stu-id="bd542-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="bd542-172">Se necessario, è possibile specificare una porta locale diversa dalla porta 80, ad esempio la porta 8080.</span><span class="sxs-lookup"><span data-stu-id="bd542-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="bd542-173">È tuttavia possibile che alcuni collegamenti dell'interfaccia utente Web non funzionino quando si usa questa porta.</span><span class="sxs-lookup"><span data-stu-id="bd542-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="bd542-174">È ora possibile accedere a endpoint di controller di dominio/OS hello dal sistema locale tramite hello URL (presupponendo che la porta locale 80) seguenti:</span><span class="sxs-lookup"><span data-stu-id="bd542-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="bd542-175">Controller di dominio/sistema operativo: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="bd542-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="bd542-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="bd542-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="bd542-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="bd542-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="bd542-178">Analogamente, è possibile raggiungere le API rest hello per ogni applicazione attraverso questo tunnel.</span><span class="sxs-lookup"><span data-stu-id="bd542-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="bd542-179">Tunnel Swarm</span><span class="sxs-lookup"><span data-stu-id="bd542-179">Swarm tunnel</span></span>
<span data-ttu-id="bd542-180">tooopen un endpoint sciame toohello tunnel, eseguire un comando simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="bd542-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="bd542-181">Verificare che non sia presente un altro processo locale che associa la porta 2375.</span><span class="sxs-lookup"><span data-stu-id="bd542-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="bd542-182">Ad esempio, se si esegue il daemon di Docker hello in locale, viene impostato dalla porta toouse predefinito 2375.</span><span class="sxs-lookup"><span data-stu-id="bd542-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="bd542-183">Se necessario, è possibile specificare una porta locale diversa dalla porta 2375.</span><span class="sxs-lookup"><span data-stu-id="bd542-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="bd542-184">Ora è possibile accedere tramite l'interfaccia della riga di comando di Docker hello (Docker CLI) nel sistema locale cluster Docker Swarm hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="bd542-185">Per istruzioni sull'installazione, vedere [Install Docker](https://docs.docker.com/engine/installation/) (Installare Docker).</span><span class="sxs-lookup"><span data-stu-id="bd542-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="bd542-186">Impostare il toohello variabile di ambiente DOCKER_HOST porta locale che è configurato per il tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="bd542-187">Eseguire i comandi di Docker cluster Docker Swarm toohello tunnel.</span><span class="sxs-lookup"><span data-stu-id="bd542-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="bd542-188">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="bd542-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="bd542-189">Creare un tunnel SSH in Windows</span><span class="sxs-lookup"><span data-stu-id="bd542-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="bd542-190">Esistono più opzioni per creare i tunnel SSH in Windows.</span><span class="sxs-lookup"><span data-stu-id="bd542-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="bd542-191">Se si eseguono Bash Ubuntu in Windows o uno strumento simile, è possibile seguire istruzioni tunneling SSH hello illustrate in precedenza in questo articolo per macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="bd542-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="bd542-192">In alternativa, in Windows, questa sezione viene descritto come tunnel di hello toouse toocreate PuTTY.</span><span class="sxs-lookup"><span data-stu-id="bd542-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="bd542-193">[Scaricare PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="bd542-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="bd542-194">Eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-194">Run hello application.</span></span>

3. <span data-ttu-id="bd542-195">Immettere un nome host è costituito da nome utente amministratore di cluster hello e nome DNS pubblico hello del database master prima di hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="bd542-196">Hello **nome Host** simile troppo`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="bd542-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="bd542-197">Immettere 2200 per hello **porta**.</span><span class="sxs-lookup"><span data-stu-id="bd542-197">Enter 2200 for hello **Port**.</span></span>

    ![Configurazione PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="bd542-199">Selezionare **SSH > Auth**. Aggiungere un percorso tooyour file di chiave privata (formato *.ppk) per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="bd542-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="bd542-200">È possibile utilizzare uno strumento come [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate questo file hello del cluster di hello toocreate utilizzati chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="bd542-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![Configurazione PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="bd542-202">Selezionare **SSH > tunnel** e configurare segue hello inoltrati porte:</span><span class="sxs-lookup"><span data-stu-id="bd542-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="bd542-203">**Source Port** (Porta di origine): usare 80 per DC/OS o 2375 per Swarm.</span><span class="sxs-lookup"><span data-stu-id="bd542-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="bd542-204">**Destination:** usare localhost:80 per il controller di dominio/sistema operativo o localhost:2375 per Swarm.</span><span class="sxs-lookup"><span data-stu-id="bd542-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="bd542-205">Hello di esempio seguente è configurato per il controller di dominio o sistema operativo, ma sarà simile per Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="bd542-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd542-206">La porta 80 non deve essere usata quando si crea il tunnel.</span><span class="sxs-lookup"><span data-stu-id="bd542-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configurazione PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="bd542-208">Al termine, fare clic su **sessione > salvare** configurazione della connessione toosave hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="bd542-209">tooconnect toohello PuTTY sessione, fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="bd542-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="bd542-210">Quando ci si connette, è possibile visualizzare la configurazione della porta hello nel registro eventi PuTTY hello.</span><span class="sxs-lookup"><span data-stu-id="bd542-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![Log eventi di PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="bd542-212">Dopo aver configurato i tunnel hello per controller di dominio o del sistema operativo, è possibile accedere hello relativi endpoint:</span><span class="sxs-lookup"><span data-stu-id="bd542-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="bd542-213">Controller di dominio/sistema operativo: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="bd542-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="bd542-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="bd542-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="bd542-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="bd542-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="bd542-216">Dopo aver configurato i tunnel hello per Docker Swarm, aprire il tooconfigure le impostazioni di Windows una variabile di ambiente system denominata `DOCKER_HOST` con un valore di `:2375`.</span><span class="sxs-lookup"><span data-stu-id="bd542-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="bd542-217">Quindi, è possibile accedere cluster sciame hello tramite hello CLI di Docker.</span><span class="sxs-lookup"><span data-stu-id="bd542-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd542-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd542-218">Next steps</span></span>
<span data-ttu-id="bd542-219">Distribuire e gestire contenitori nel cluster:</span><span class="sxs-lookup"><span data-stu-id="bd542-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="bd542-220">Uso del servizio contenitore di Azure e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bd542-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="bd542-221">Gestione di contenitori tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="bd542-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="bd542-222">Utilizzo di hello Azure il servizio di contenitore e Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="bd542-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

