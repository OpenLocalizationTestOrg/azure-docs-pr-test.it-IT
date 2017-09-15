## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="d4505-101">Configurare l'interfaccia della riga di comando di Azure per DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="d4505-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="d4505-102">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d4505-102">Before you begin</span></span>

<span data-ttu-id="d4505-103">Prima di iniziare la configurazione, verificare di essere in possesso degli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d4505-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="d4505-104">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4505-104">An Azure subscription.</span></span> <span data-ttu-id="d4505-105">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4505-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d4505-106">Installare la versione più recente dell'interfaccia della riga di comando di Azure, disponibile per Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="d4505-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="d4505-107">Per altre informazioni, vedere [Installare l'interfaccia della riga di comando di Azure](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d4505-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="d4505-108">Accedere con l'account Azure</span><span class="sxs-lookup"><span data-stu-id="d4505-108">Sign in to your Azure account</span></span>

<span data-ttu-id="d4505-109">Aprire una finestra della console ed eseguire l'autenticazione con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="d4505-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="d4505-110">Per altre informazioni, vedere [Accedere ad Azure dall'interfaccia della riga di comando di Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d4505-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="d4505-111">Passare alla modalità interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="d4505-111">Switch CLI mode</span></span>

<span data-ttu-id="d4505-112">DNS di Azure usa Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4505-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="d4505-113">Assicurarsi di passare alla modalità interfaccia della riga di comando per usare i comandi di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4505-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-the-subscription"></a><span data-ttu-id="d4505-114">Selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d4505-114">Select the subscription</span></span>

<span data-ttu-id="d4505-115">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="d4505-115">Check the subscriptions for the account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="d4505-116">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="d4505-116">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d4505-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d4505-117">Create a resource group</span></span>

<span data-ttu-id="d4505-118">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="d4505-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d4505-119">che viene usato come percorso predefinito per le risorse presenti in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d4505-119">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="d4505-120">Tuttavia, dato che tutte le risorse DNS sono globali, non regionali, la scelta del percorso del gruppo di risorse non ha alcun impatto sul servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4505-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="d4505-121">Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="d4505-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="d4505-122">Registrare il provider di risorse</span><span class="sxs-lookup"><span data-stu-id="d4505-122">Register resource provider</span></span>

<span data-ttu-id="d4505-123">Il servizio DNS di Azure viene gestito dal provider di risorse Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="d4505-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="d4505-124">Per poter usare il servizio DNS di Azure, la sottoscrizione di Azure deve essere registrata per l'uso di questo provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="d4505-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="d4505-125">Questa operazione viene eseguita una sola volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d4505-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

