## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="08c41-101">Configurare Azure PowerShell per DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="08c41-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="08c41-102">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="08c41-102">Before you begin</span></span>

<span data-ttu-id="08c41-103">Prima di iniziare la configurazione, verificare di essere in possesso degli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="08c41-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="08c41-104">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="08c41-104">An Azure subscription.</span></span> <span data-ttu-id="08c41-105">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08c41-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="08c41-106">È necessario installare la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08c41-106">You need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="08c41-107">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="08c41-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="08c41-108">Accedere con l'account Azure</span><span class="sxs-lookup"><span data-stu-id="08c41-108">Sign in to your Azure account</span></span>

<span data-ttu-id="08c41-109">Aprire la console di PowerShell e connettersi al proprio account.</span><span class="sxs-lookup"><span data-stu-id="08c41-109">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="08c41-110">Per altre informazioni, vedere [Uso di PowerShell con Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="08c41-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-the-subscription"></a><span data-ttu-id="08c41-111">Selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="08c41-111">Select the subscription</span></span>
 
<span data-ttu-id="08c41-112">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="08c41-112">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="08c41-113">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="08c41-113">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="08c41-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="08c41-114">Create a resource group</span></span>

<span data-ttu-id="08c41-115">Azure Resource Manager richiede che tutti i gruppi di risorse specifichino una località.</span><span class="sxs-lookup"><span data-stu-id="08c41-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="08c41-116">che viene usato come percorso predefinito per le risorse presenti in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="08c41-116">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="08c41-117">Tuttavia, dato che tutte le risorse DNS sono globali, non regionali, la scelta del percorso del gruppo di risorse non ha alcun impatto sul servizio DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="08c41-117">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="08c41-118">Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="08c41-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="08c41-119">Registrare il provider di risorse</span><span class="sxs-lookup"><span data-stu-id="08c41-119">Register resource provider</span></span>

<span data-ttu-id="08c41-120">Il servizio DNS di Azure viene gestito dal provider di risorse Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="08c41-120">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="08c41-121">Per poter usare il servizio DNS di Azure, la sottoscrizione di Azure deve essere registrata per l'uso di questo provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="08c41-121">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="08c41-122">Questa operazione viene eseguita una sola volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="08c41-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```