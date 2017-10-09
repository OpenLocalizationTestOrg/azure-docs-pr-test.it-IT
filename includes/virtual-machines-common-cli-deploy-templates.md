
* [<span data-ttu-id="7cbab-101">Creazione rapida di una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="7cbab-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="7cbab-102">Distribuire una macchina virtuale in Azure da un modello</span><span class="sxs-lookup"><span data-stu-id="7cbab-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="7cbab-103">Creare una macchina virtuale da un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="7cbab-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="7cbab-104">Distribuire una macchina virtuale che usa una rete virtuale e un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="7cbab-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="7cbab-105">Rimuovere un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7cbab-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="7cbab-106">Mostra log hello per la distribuzione di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7cbab-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="7cbab-107">Visualizzare informazioni relative a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7cbab-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="7cbab-108">Connettere tooa di macchina virtuale basata su Linux</span><span class="sxs-lookup"><span data-stu-id="7cbab-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="7cbab-109">Arrestare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7cbab-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="7cbab-110">Avviare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7cbab-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="7cbab-111">Collegare un disco dati</span><span class="sxs-lookup"><span data-stu-id="7cbab-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="7cbab-112">Preparazione</span><span class="sxs-lookup"><span data-stu-id="7cbab-112">Getting ready</span></span>
<span data-ttu-id="7cbab-113">Prima di poter utilizzare hello CLI di Azure con i gruppi di risorse di Azure, è necessario la versione toohave hello corretta CLI di Azure e un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbab-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="7cbab-114">Se non si dispone di hello CLI di Azure, [installarlo](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7cbab-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="7cbab-115">Aggiornare il too0.9.0 versione CLI di Azure o versione successiva</span><span class="sxs-lookup"><span data-stu-id="7cbab-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="7cbab-116">Tipo `azure --version` toosee se si dispone già installata una versione 0.9.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="7cbab-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="7cbab-117">Se la versione non è di tipo 0.9.0 o versioni successive, è necessario tooupdate usando uno dei programmi di installazione native di hello o tramite **npm** digitando `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="7cbab-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="7cbab-118">È inoltre possibile eseguire come un contenitore Docker CLI di Azure tramite hello seguenti [immagine Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="7cbab-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="7cbab-119">Da un host Docker, eseguire il comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7cbab-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="7cbab-120">Impostare l'account e la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="7cbab-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="7cbab-121">Se non si dispone già di una sottoscrizione di Azure, ma si dispone di una sottoscrizione MSDN, è possibile attivare i [vantaggi per i titolari di sottoscrizioni MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)</span><span class="sxs-lookup"><span data-stu-id="7cbab-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="7cbab-122">oppure iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7cbab-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="7cbab-123">Ora [Accedi tooyour account Azure in modo interattivo](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) digitando `azure login` e seguendo hello richiede un tooyour esperienza di accesso interattivo account Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbab-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="7cbab-124">Se si dispone di un o dell'istituto di istruzione ID e si è certi di non è abilitata l'autenticazione a due fattori, è possibile **anche** utilizzare `azure login -u` insieme ai hello di lavoro o dell'istituto di istruzione toolog ID in *senza* una sessione interattiva.</span><span class="sxs-lookup"><span data-stu-id="7cbab-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="7cbab-125">Se si non dispone di un o dell'istituto di istruzione ID, è possibile [creare un id aziendale o dell'istituto di istruzione dal tuo account Microsoft personale](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="7cbab-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="7cbab-126">L'account può includere più di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7cbab-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="7cbab-127">È possibile elencare le sottoscrizioni digitando `azure account list`, comando che potrebbe essere visualizzato in modo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7cbab-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="7cbab-128">È possibile impostare una sottoscrizione Azure corrente hello digitando hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7cbab-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="7cbab-129">Utilizzare hello ID sottoscrizione di nome o hello ha risorse hello è toomanage.</span><span class="sxs-lookup"><span data-stu-id="7cbab-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="7cbab-130">Passare in modalità gruppo di risorse di toohello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="7cbab-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="7cbab-131">Per impostazione predefinita, hello CLI di Azure viene avviato in modalità di Gestione servizio hello (**asm** modalità).</span><span class="sxs-lookup"><span data-stu-id="7cbab-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="7cbab-132">Digitare hello seguenti modalità di tooswitch tooresource gruppo.</span><span class="sxs-lookup"><span data-stu-id="7cbab-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="7cbab-133">Informazioni su modelli di risorse e gruppi di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7cbab-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="7cbab-134">La maggior parte delle applicazioni è costituita da una combinazione di tipi di risorse diversi, ad esempio una o più macchine virtuali e account di archiviazione, un database SQL, una rete virtuale o una rete per la distribuzione di contenuti.</span><span class="sxs-lookup"><span data-stu-id="7cbab-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="7cbab-135">Hello API di gestione predefinito servizio di Azure e hello portale di Azure classico rappresentato questi elementi utilizzando un approccio di servizio dal servizio.</span><span class="sxs-lookup"><span data-stu-id="7cbab-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="7cbab-136">Questo approccio richiede toodeploy e gestire singolarmente i singoli servizi hello (o altri strumenti che farlo) e non come una singola unità logica di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7cbab-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="7cbab-137">*Modelli di Azure Resource Manager*, tuttavia, consentono di toodeploy e gestire queste risorse diverse come un'unità logica di distribuzione in modo dichiarativo.</span><span class="sxs-lookup"><span data-stu-id="7cbab-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="7cbab-138">Anziché in modo imperativo tramite Azure quali toodeploy un comando dopo l'altro, descrivere l'intera distribuzione di un file JSON - tutte le risorse di hello e configurazione associata e parametri di distribuzione - e indicare toodeploy Azure tali risorse come uno gruppo.</span><span class="sxs-lookup"><span data-stu-id="7cbab-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="7cbab-139">È quindi possibile gestire hello ciclo di vita globale delle risorse del gruppo di hello utilizzando i comandi di gestione risorse di CLI di Azure per:</span><span class="sxs-lookup"><span data-stu-id="7cbab-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="7cbab-140">Arrestare, avviare o eliminare tutte le risorse di hello in gruppo hello in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="7cbab-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="7cbab-141">Applicare toolock regole di controllo di accesso basato sui ruoli (RBAC) verso il basso le autorizzazioni di sicurezza su di essi.</span><span class="sxs-lookup"><span data-stu-id="7cbab-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="7cbab-142">Controllare le operazioni.</span><span class="sxs-lookup"><span data-stu-id="7cbab-142">Audit operations.</span></span>
* <span data-ttu-id="7cbab-143">Contrassegnare le risorse con metadati aggiuntivi per una gestione più efficiente.</span><span class="sxs-lookup"><span data-stu-id="7cbab-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="7cbab-144">È possibile ottenere informazioni molto altro ancora sui gruppi di risorse di Azure e le operazioni consentite per l'utente in hello [Panoramica di gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cbab-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="7cbab-145">Se si è interessati alla creazione di modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7cbab-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="7cbab-146"><a id="quick-create-a-vm-in-azure"></a>Attività: Creare rapidamente una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="7cbab-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="7cbab-147">A volte si sa quale immagine è necessario, è necessario ora una macchina virtuale da quell'immagine e non si è interessati troppo infrastruttura hello - forse è disponibile tootest un elemento in una nuova VM.</span><span class="sxs-lookup"><span data-stu-id="7cbab-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="7cbab-148">Ovvero quando si desidera toouse hello `azure vm quick-create` comandi e passare hello argomenti necessari toocreate una macchina virtuale e l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="7cbab-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="7cbab-149">Innanzitutto, creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7cbab-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="7cbab-150">In secondo luogo, è necessaria un'immagine.</span><span class="sxs-lookup"><span data-stu-id="7cbab-150">Second, you'll need an image.</span></span> <span data-ttu-id="7cbab-151">toofind un'immagine con hello CLI di Azure, vedere [Navigating e selezione di immagini di macchina virtuale di Azure con PowerShell e hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cbab-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7cbab-152">In questo articolo è riportato un breve elenco delle immagini più diffuse.</span><span class="sxs-lookup"><span data-stu-id="7cbab-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="7cbab-153">Verrà creata un'immagine stabile di CoreOS per questa creazione rapida.</span><span class="sxs-lookup"><span data-stu-id="7cbab-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="7cbab-154">Per ComputeImageVersion, è possibile anche semplicemente fornire 'più recente' come parametro nel linguaggio del modello sia hello in hello Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="7cbab-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="7cbab-155">In questo modo che è tooalways utilizzare la versione più recente e con patch di hello dell'immagine di hello senza toomodify script o modelli.</span><span class="sxs-lookup"><span data-stu-id="7cbab-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="7cbab-156">come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7cbab-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="7cbab-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="7cbab-157">PublisherName</span></span> | <span data-ttu-id="7cbab-158">Offerta</span><span class="sxs-lookup"><span data-stu-id="7cbab-158">Offer</span></span> | <span data-ttu-id="7cbab-159">Sku</span><span class="sxs-lookup"><span data-stu-id="7cbab-159">Sku</span></span> | <span data-ttu-id="7cbab-160">Versione</span><span class="sxs-lookup"><span data-stu-id="7cbab-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7cbab-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="7cbab-161">OpenLogic</span></span> |<span data-ttu-id="7cbab-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="7cbab-162">CentOS</span></span> |<span data-ttu-id="7cbab-163">7</span><span class="sxs-lookup"><span data-stu-id="7cbab-163">7</span></span> |<span data-ttu-id="7cbab-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="7cbab-164">7.0.201503</span></span> |
| <span data-ttu-id="7cbab-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="7cbab-165">OpenLogic</span></span> |<span data-ttu-id="7cbab-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="7cbab-166">CentOS</span></span> |<span data-ttu-id="7cbab-167">7.1</span><span class="sxs-lookup"><span data-stu-id="7cbab-167">7.1</span></span> |<span data-ttu-id="7cbab-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="7cbab-168">7.1.201504</span></span> |
| <span data-ttu-id="7cbab-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7cbab-169">CoreOS</span></span> |<span data-ttu-id="7cbab-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7cbab-170">CoreOS</span></span> |<span data-ttu-id="7cbab-171">Beta</span><span class="sxs-lookup"><span data-stu-id="7cbab-171">Beta</span></span> |<span data-ttu-id="7cbab-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="7cbab-172">647.0.0</span></span> |
| <span data-ttu-id="7cbab-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7cbab-173">CoreOS</span></span> |<span data-ttu-id="7cbab-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7cbab-174">CoreOS</span></span> |<span data-ttu-id="7cbab-175">Stabile</span><span class="sxs-lookup"><span data-stu-id="7cbab-175">Stable</span></span> |<span data-ttu-id="7cbab-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="7cbab-176">633.1.0</span></span> |
| <span data-ttu-id="7cbab-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="7cbab-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="7cbab-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="7cbab-178">DynamicsNAV</span></span> |<span data-ttu-id="7cbab-179">2015</span><span class="sxs-lookup"><span data-stu-id="7cbab-179">2015</span></span> |<span data-ttu-id="7cbab-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="7cbab-180">8.0.40459</span></span> |
| <span data-ttu-id="7cbab-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="7cbab-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="7cbab-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="7cbab-183">2013</span><span class="sxs-lookup"><span data-stu-id="7cbab-183">2013</span></span> |<span data-ttu-id="7cbab-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="7cbab-184">1.0.0</span></span> |
| <span data-ttu-id="7cbab-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="7cbab-185">msopentech</span></span> |<span data-ttu-id="7cbab-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="7cbab-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="7cbab-187">Standard</span><span class="sxs-lookup"><span data-stu-id="7cbab-187">Standard</span></span> |<span data-ttu-id="7cbab-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="7cbab-188">1.0.0</span></span> |
| <span data-ttu-id="7cbab-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="7cbab-189">msopentech</span></span> |<span data-ttu-id="7cbab-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="7cbab-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="7cbab-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="7cbab-191">Enterprise</span></span> |<span data-ttu-id="7cbab-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="7cbab-192">1.0.0</span></span> |
| <span data-ttu-id="7cbab-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="7cbab-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="7cbab-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="7cbab-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="7cbab-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="7cbab-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="7cbab-196">12.0.2430</span></span> |
| <span data-ttu-id="7cbab-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="7cbab-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="7cbab-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="7cbab-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="7cbab-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="7cbab-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="7cbab-200">12.0.2430</span></span> |
| <span data-ttu-id="7cbab-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="7cbab-201">Canonical</span></span> |<span data-ttu-id="7cbab-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-202">UbuntuServer</span></span> |<span data-ttu-id="7cbab-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="7cbab-203">12.04.5-LTS</span></span> |<span data-ttu-id="7cbab-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="7cbab-204">12.04.201504230</span></span> |
| <span data-ttu-id="7cbab-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="7cbab-205">Canonical</span></span> |<span data-ttu-id="7cbab-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-206">UbuntuServer</span></span> |<span data-ttu-id="7cbab-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="7cbab-207">14.04.2-LTS</span></span> |<span data-ttu-id="7cbab-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="7cbab-208">14.04.201503090</span></span> |
| <span data-ttu-id="7cbab-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="7cbab-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-210">WindowsServer</span></span> |<span data-ttu-id="7cbab-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="7cbab-211">2012-Datacenter</span></span> |<span data-ttu-id="7cbab-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="7cbab-212">3.0.201503</span></span> |
| <span data-ttu-id="7cbab-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="7cbab-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-214">WindowsServer</span></span> |<span data-ttu-id="7cbab-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="7cbab-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="7cbab-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="7cbab-216">4.0.201503</span></span> |
| <span data-ttu-id="7cbab-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="7cbab-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="7cbab-218">WindowsServer</span></span> |<span data-ttu-id="7cbab-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="7cbab-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="7cbab-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="7cbab-220">5.0.201504</span></span> |
| <span data-ttu-id="7cbab-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="7cbab-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="7cbab-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="7cbab-222">WindowsServerEssentials</span></span> |<span data-ttu-id="7cbab-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="7cbab-223">WindowsServerEssentials</span></span> |<span data-ttu-id="7cbab-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="7cbab-224">1.0.141204</span></span> |
| <span data-ttu-id="7cbab-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="7cbab-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="7cbab-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="7cbab-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="7cbab-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="7cbab-227">2012R2</span></span> |<span data-ttu-id="7cbab-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="7cbab-228">4.3.4665</span></span> |

<span data-ttu-id="7cbab-229">Creare la macchina virtuale tramite l'immissione di hello `azure vm quick-create` comando ed è pronto per hello richieste.</span><span class="sxs-lookup"><span data-stu-id="7cbab-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="7cbab-230">Dovrebbe essere visualizzata una schermata analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="7cbab-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="7cbab-231">La nuova macchina virtuale è stata completata.</span><span class="sxs-lookup"><span data-stu-id="7cbab-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="7cbab-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Attività: Distribuire una macchina virtuale in Azure da un modello</span><span class="sxs-lookup"><span data-stu-id="7cbab-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="7cbab-233">Utilizzare istruzioni hello in questi toodeploy sezioni, una nuova macchina virtuale di Azure tramite un modello con hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbab-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="7cbab-234">Questo modello consente di creare una singola macchina virtuale in una nuova rete virtuale con una singola subnet e, a differenza `azure vm quick-create`, consente di toodescribe esattamente come si desidera e ripeterlo senza errori.</span><span class="sxs-lookup"><span data-stu-id="7cbab-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="7cbab-235">Di seguito ciò che viene creato da questo modello:</span><span class="sxs-lookup"><span data-stu-id="7cbab-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="7cbab-236">Passaggio 1: Esaminare il file JSON hello per parametri modello hello</span><span class="sxs-lookup"><span data-stu-id="7cbab-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="7cbab-237">Di seguito sono contenuti hello del file JSON hello per modello hello.</span><span class="sxs-lookup"><span data-stu-id="7cbab-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="7cbab-238">(modello hello è disponibile anche in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="7cbab-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="7cbab-239">I modelli sono flessibili, in modo che progettazione hello potrebbe avere scelto toogive è un numero elevato di parametri o scelto toooffer solo poche creando un modello più corretti.</span><span class="sxs-lookup"><span data-stu-id="7cbab-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="7cbab-240">Nelle informazioni di hello toocollect ordine è necessario un modello di hello toopass come parametri, aprire il file di modello hello (in questo argomento è un modello inline, sotto) ed esaminare hello **parametri** valori.</span><span class="sxs-lookup"><span data-stu-id="7cbab-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="7cbab-241">In questo caso, verrà chiesta modello hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7cbab-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="7cbab-242">Un nome dell'account di archiviazione univoco.</span><span class="sxs-lookup"><span data-stu-id="7cbab-242">A unique storage account name.</span></span>
* <span data-ttu-id="7cbab-243">Un nome utente amministratore hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7cbab-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="7cbab-244">Una password.</span><span class="sxs-lookup"><span data-stu-id="7cbab-244">A password.</span></span>
* <span data-ttu-id="7cbab-245">Un nome di dominio per hello world toouse di fuori.</span><span class="sxs-lookup"><span data-stu-id="7cbab-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="7cbab-246">Un numero di versione di Ubuntu Server (verrà accettato un solo numero dall'interno di un elenco).</span><span class="sxs-lookup"><span data-stu-id="7cbab-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="7cbab-247">Sono disponibili altre informazioni sui [requisiti relativi a nome utente e password](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="7cbab-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="7cbab-248">Dopo aver deciso su questi valori, è possibile toocreate un gruppo per e distribuire questo modello nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbab-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="7cbab-249">Passaggio 2: Creare una macchina virtuale hello utilizzando il modello di hello</span><span class="sxs-lookup"><span data-stu-id="7cbab-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="7cbab-250">Dopo aver creato i valori di parametro pronti, è necessario creare un gruppo di risorse per la distribuzione del modello e quindi distribuire il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7cbab-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="7cbab-251">gruppo di risorse hello toocreate, tipo `azure group create <group name> <location>` con nome hello del gruppo di hello desiderato e ubicazione del Data Center hello in cui si desidera toodeploy.</span><span class="sxs-lookup"><span data-stu-id="7cbab-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="7cbab-252">Ciò si verifica rapidamente:</span><span class="sxs-lookup"><span data-stu-id="7cbab-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="7cbab-253">Distribuzione di hello toocreate ora, chiamare `azure group deployment create` e passare:</span><span class="sxs-lookup"><span data-stu-id="7cbab-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="7cbab-254">file di modello Hello (se è stato salvato hello sopra file locale tooa di modello JSON).</span><span class="sxs-lookup"><span data-stu-id="7cbab-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="7cbab-255">Un modello di URI (se si desidera toopoint file hello in GitHub o un altro indirizzo web).</span><span class="sxs-lookup"><span data-stu-id="7cbab-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="7cbab-256">gruppo di risorse Hello in cui si desidera toodeploy.</span><span class="sxs-lookup"><span data-stu-id="7cbab-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="7cbab-257">Un nome di distribuzione facoltativo.</span><span class="sxs-lookup"><span data-stu-id="7cbab-257">An optional deployment name.</span></span>

<span data-ttu-id="7cbab-258">Sarà richiesto toosupply hello valori dei parametri nella sezione "parametri" hello del file JSON hello.</span><span class="sxs-lookup"><span data-stu-id="7cbab-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="7cbab-259">Dopo aver specificato tutti i valori di parametro hello, verrà avviata la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7cbab-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="7cbab-260">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="7cbab-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="7cbab-261">Verrà visualizzato hello dopo il tipo di informazioni:</span><span class="sxs-lookup"><span data-stu-id="7cbab-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="7cbab-262"><a id="create-a-custom-vm-image"></a>Attività: Creare un'immagine di macchina virtuale personalizzata</span><span class="sxs-lookup"><span data-stu-id="7cbab-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="7cbab-263">È stato illustrato l'utilizzo di base hello dei modelli precedenti, pertanto ora è possibile usare toocreate istruzioni simili una macchina virtuale personalizzata da un file VHD in Azure utilizzando un modello tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbab-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="7cbab-264">Hello differenza è che in questo modello consente di creare una singola macchina virtuale da un disco rigido virtuale specificato (VHD).</span><span class="sxs-lookup"><span data-stu-id="7cbab-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="7cbab-265">Passaggio 1: Esaminare il file JSON hello per modello hello</span><span class="sxs-lookup"><span data-stu-id="7cbab-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="7cbab-266">Di seguito sono contenuti hello del file JSON hello per modello di hello in questa sezione viene utilizzato come esempio.</span><span class="sxs-lookup"><span data-stu-id="7cbab-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="7cbab-267">(modello hello è disponibile anche in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="7cbab-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="7cbab-268">Nuovamente, è necessario che i valori di hello toofind da tooenter per i parametri di hello che non contengono valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="7cbab-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="7cbab-269">Quando si esegue hello `azure group deployment create` comando hello Azure CLI richiederà si tooenter tali valori.</span><span class="sxs-lookup"><span data-stu-id="7cbab-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="7cbab-270">Passaggio 2: Ottenere hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="7cbab-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="7cbab-271">Ovviamente, è necessario un file VHD per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="7cbab-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="7cbab-272">È possibile usarne uno già presente in Azure o caricarne uno.</span><span class="sxs-lookup"><span data-stu-id="7cbab-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="7cbab-273">Per una macchina virtuale basato su Windows, vedere [creazione e caricamento di un disco rigido virtuale di Windows Server di tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cbab-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="7cbab-274">Per una macchina virtuale basata su Linux, vedere [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cbab-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="7cbab-275">Passaggio 3: Creare una macchina virtuale hello utilizzando il modello di hello</span><span class="sxs-lookup"><span data-stu-id="7cbab-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="7cbab-276">Ora si è pronti toocreate una nuova macchina virtuale basata su file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="7cbab-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="7cbab-277">Creare un gruppo toodeploy in, utilizzando `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="7cbab-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="7cbab-278">Quindi creare la distribuzione di hello utilizzando hello `--template-uri` toocall opzione direttamente modello hello (o è possibile utilizzare hello `--template-file` opzione toouse un file salvato in locale).</span><span class="sxs-lookup"><span data-stu-id="7cbab-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="7cbab-279">Si noti che poiché il modello di hello ha valori predefiniti specificati, viene richiesto solo alcuni aspetti.</span><span class="sxs-lookup"><span data-stu-id="7cbab-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="7cbab-280">Se si distribuisce il modello di hello in posizioni diverse, è possibile che alcuni conflitti di denominazione si verificano con i valori predefiniti di hello (in particolare hello nome DNS crei).</span><span class="sxs-lookup"><span data-stu-id="7cbab-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="7cbab-281">Output sarà simile alla seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7cbab-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="7cbab-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Attività: Distribuire un'applicazione per più macchine virtuali che usa una rete virtuale e un servizio di bilanciamento del carico esterno</span><span class="sxs-lookup"><span data-stu-id="7cbab-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="7cbab-283">Questo modello consente toocreate due macchine virtuali in un bilanciamento del carico e configurare una regola di bilanciamento del carico sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="7cbab-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="7cbab-284">Questo modello distribuisce anche un account di archiviazione, una rete virtuale, l'indirizzo IP pubblico, il set di disponibilità e le interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="7cbab-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="7cbab-285">Seguire questi toodeploy passaggi un'applicazione multi-VM che utilizza una rete virtuale e un servizio di bilanciamento del carico con un modello di gestione delle risorse nel repository di modello GitHub hello tramite i comandi di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbab-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="7cbab-286">Passaggio 1: Esaminare il file JSON hello per modello hello</span><span class="sxs-lookup"><span data-stu-id="7cbab-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="7cbab-287">Di seguito sono contenuti hello del file JSON hello per modello hello.</span><span class="sxs-lookup"><span data-stu-id="7cbab-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="7cbab-288">Se si desidera una versione più recente di hello, ha individuato [al repository GitHub hello per i modelli di](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7cbab-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="7cbab-289">In questo argomento utilizza hello `--template-uri` toocall commutatore nel modello di hello, ma è anche possibile usare hello `--template-file` passare toopass una versione locale.</span><span class="sxs-lookup"><span data-stu-id="7cbab-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="7cbab-290">Passaggio 2: Creare una distribuzione hello utilizzando il modello di hello</span><span class="sxs-lookup"><span data-stu-id="7cbab-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="7cbab-291">Creare un gruppo di risorse per il modello di hello utilizzando `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="7cbab-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="7cbab-292">Quindi, creare una distribuzione in tale gruppo di risorse utilizzando `azure group deployment create` e passando il gruppo di risorse hello, passando un nome di distribuzione e rispondere alle richieste di hello per i parametri di modello hello che non disponevano di valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="7cbab-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="7cbab-293">A questo punto utilizzare hello `azure group deployment create` comando e hello `--template-uri` modello hello toodeploy di opzioni.</span><span class="sxs-lookup"><span data-stu-id="7cbab-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="7cbab-294">Quando richiesto, specificare i valori dei parametri, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7cbab-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="7cbab-295">Si noti che questo modello distribuisce un'immagine di Windows Server. Questa immagine potrebbe essere tuttavia sostituita con qualsiasi immagine Linux.</span><span class="sxs-lookup"><span data-stu-id="7cbab-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="7cbab-296">Vuole toocreate un cluster di Docker con più gestioni sciame?</span><span class="sxs-lookup"><span data-stu-id="7cbab-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="7cbab-297">Per eseguire questa operazione, consultare [questa pagina](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="7cbab-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="7cbab-298"><a id="remove-a-resource-group"></a>Attività: Rimuovere un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7cbab-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="7cbab-299">Ricordare che è possibile ridistribuire il gruppo di risorse tooa, ma con un termine, è possibile eliminarlo utilizzando `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="7cbab-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="7cbab-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Attività: Visualizzazione del log hello per la distribuzione di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="7cbab-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="7cbab-301">Questa operazione è piuttosto comune durante la creazione o l'utilizzo di modelli.</span><span class="sxs-lookup"><span data-stu-id="7cbab-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="7cbab-302">distribuzione di hello toodisplay chiamata Hello i log per un gruppo è `azure group log show <groupname>`, che consente di visualizzare diverse informazioni utili per comprendere perché si è verificato, o non.</span><span class="sxs-lookup"><span data-stu-id="7cbab-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="7cbab-303">Per altre informazioni sulla risoluzione dei problemi relativi alle distribuzioni o ad altri errori, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="7cbab-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="7cbab-304">tootarget errori specifici, ad esempio, è possibile utilizzare strumenti come **jq** operazioni tooquery un po' più precisamente, ad esempio gli errori che singoli occorre toocorrect.</span><span class="sxs-lookup"><span data-stu-id="7cbab-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="7cbab-305">Hello seguente utilizza **jq** tooparse di log per una distribuzione **lbgroup**ricercano gli errori.</span><span class="sxs-lookup"><span data-stu-id="7cbab-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="7cbab-306">È possibile individuare molto rapidamente la causa dell'errore, correggerlo e riprovare.</span><span class="sxs-lookup"><span data-stu-id="7cbab-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="7cbab-307">In hello successive a case, il modello di hello era stato creazione due macchine virtuali in hello stesso tempo, che ha creato un blocco su hello VHD.</span><span class="sxs-lookup"><span data-stu-id="7cbab-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="7cbab-308">(Dopo aver modificato il modello di hello, hello distribuzione completata rapidamente).</span><span class="sxs-lookup"><span data-stu-id="7cbab-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="7cbab-309"><a id="display-information-about-a-virtual-machine"></a>Attività: Visualizzare informazioni relative a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7cbab-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="7cbab-310">È possibile visualizzare informazioni sulle specifiche macchine virtuali nel gruppo di risorse utilizzando hello `azure vm show <groupname> <vmname>` comando.</span><span class="sxs-lookup"><span data-stu-id="7cbab-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="7cbab-311">Se si dispone più di una macchina virtuale del gruppo, potrebbe essere necessario innanzitutto hello toolist macchine virtuali in un gruppo tramite `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="7cbab-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="7cbab-312">Selezionare quindi myVM1:</span><span class="sxs-lookup"><span data-stu-id="7cbab-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="7cbab-313">Se si desidera tooprogrammatically archivio e manipolare l'output di hello i di comandi della console, è opportuno toouse strumento di analisi di JSON ad esempio  **[jq](https://github.com/stedolan/jq)**  o  **[jsawk](https://github.com/micha/jsawk)** , o raccolte di linguaggio che sono ideali per l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="7cbab-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="7cbab-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Attività: Accesso tooa di macchina virtuale basata su Linux</span><span class="sxs-lookup"><span data-stu-id="7cbab-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="7cbab-315">In genere macchine Linux sono connessi toothrough SSH.</span><span class="sxs-lookup"><span data-stu-id="7cbab-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="7cbab-316">Per ulteriori informazioni, vedere [come toouse SSH con Linux in Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cbab-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="7cbab-317"><a id="stop-a-virtual-machine"></a>Attività: Arrestare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7cbab-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="7cbab-318">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="7cbab-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="7cbab-319">Utilizzare questo parametro tookeep hello IP virtuale (VIP) di rete virtuale hello nel caso in cui è hello ultima macchina virtuale in tale rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7cbab-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="7cbab-320">Se si utilizza hello `StayProvisioned` parametro, è comunque addebitato per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7cbab-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="7cbab-321"><a id="start-a-virtual-machine"></a>Attività: Avviare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7cbab-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="7cbab-322">Eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="7cbab-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="7cbab-323"><a id="attach-a-data-disk"></a>Attività: Collegare un disco dati</span><span class="sxs-lookup"><span data-stu-id="7cbab-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="7cbab-324">È anche necessario toodecide se tooattach un nuovo disco o uno che contiene dati.</span><span class="sxs-lookup"><span data-stu-id="7cbab-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="7cbab-325">Per un nuovo disco, il comando hello crea file con estensione vhd hello e lo collega in hello stesso comando.</span><span class="sxs-lookup"><span data-stu-id="7cbab-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="7cbab-326">tooattach un nuovo disco, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="7cbab-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="7cbab-327">tooattach un disco dati esistente, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="7cbab-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="7cbab-328">Quindi è necessario toomount hello disco, in modo analogo in Linux.</span><span class="sxs-lookup"><span data-stu-id="7cbab-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cbab-329">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cbab-329">Next steps</span></span>
<span data-ttu-id="7cbab-330">Per ulteriori esempi di utilizzo dell'interfaccia CLI di Azure con hello **arm** modalità, vedere [Using hello CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7cbab-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="7cbab-331">toolearn informazioni sulle risorse di Azure e i concetti, vedere [Panoramica di gestione risorse di Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cbab-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="7cbab-332">Per altri modelli disponibili, vedere [Modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) e [Framework applicazioni usando i modelli](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cbab-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
