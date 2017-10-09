## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="15417-101">Configurare l'interfaccia della riga di comando di Azure per DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="15417-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="15417-102">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="15417-102">Before you begin</span></span>

<span data-ttu-id="15417-103">Verificare di aver hello seguenti prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="15417-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="15417-104">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="15417-104">An Azure subscription.</span></span> <span data-ttu-id="15417-105">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15417-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="15417-106">Installare hello l'ultima versione di hello CLI di Azure, disponibile per Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="15417-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="15417-107">Altre informazioni sono disponibile all'indirizzo [installazione hello Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="15417-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="15417-108">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="15417-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="15417-109">Aprire una finestra della console ed eseguire l'autenticazione con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="15417-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="15417-110">Per ulteriori informazioni, vedere [Accedi tooAzure da hello CLI di Azure](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="15417-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="15417-111">Passare alla modalità interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="15417-111">Switch CLI mode</span></span>

<span data-ttu-id="15417-112">DNS di Azure usa Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="15417-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="15417-113">Accertarsi di passare i comandi CLI modalità toouse Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="15417-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="15417-114">Selezionare la sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="15417-114">Select hello subscription</span></span>

<span data-ttu-id="15417-115">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="15417-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="15417-116">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="15417-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="15417-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="15417-117">Create a resource group</span></span>

<span data-ttu-id="15417-118">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="15417-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="15417-119">Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="15417-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="15417-120">Tuttavia, poiché tutte le risorse DNS sono globali, non è regionale, scelta hello del percorso del gruppo di risorse ha alcun impatto su DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="15417-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="15417-121">Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="15417-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="15417-122">Registrare il provider di risorse</span><span class="sxs-lookup"><span data-stu-id="15417-122">Register resource provider</span></span>

<span data-ttu-id="15417-123">Hello servizio DNS di Azure viene gestita dal provider di risorse Microsoft. Network hello.</span><span class="sxs-lookup"><span data-stu-id="15417-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="15417-124">La sottoscrizione di Azure deve essere registrato toouse questo provider di risorse prima di poter usare DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="15417-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="15417-125">Questa operazione viene eseguita una sola volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="15417-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

