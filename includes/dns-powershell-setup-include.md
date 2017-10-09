## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="2a85c-101">Configurare Azure PowerShell per DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="2a85c-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="2a85c-102">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2a85c-102">Before you begin</span></span>

<span data-ttu-id="2a85c-103">Verificare di aver hello seguenti prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2a85c-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="2a85c-104">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85c-104">An Azure subscription.</span></span> <span data-ttu-id="2a85c-105">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a85c-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2a85c-106">È necessario tooinstall hello più recente di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85c-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="2a85c-107">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2a85c-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="2a85c-108">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="2a85c-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="2a85c-109">Aprire la console di PowerShell e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="2a85c-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="2a85c-110">Per altre informazioni, vedere [Uso di PowerShell con Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2a85c-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="2a85c-111">Selezionare la sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="2a85c-111">Select hello subscription</span></span>
 
<span data-ttu-id="2a85c-112">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="2a85c-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="2a85c-113">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85c-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="2a85c-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="2a85c-114">Create a resource group</span></span>

<span data-ttu-id="2a85c-115">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="2a85c-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="2a85c-116">Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2a85c-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="2a85c-117">Tuttavia, poiché tutte le risorse DNS sono globali, non è regionale, scelta hello del percorso del gruppo di risorse ha alcun impatto su DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85c-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="2a85c-118">Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="2a85c-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="2a85c-119">Registrare il provider di risorse</span><span class="sxs-lookup"><span data-stu-id="2a85c-119">Register resource provider</span></span>

<span data-ttu-id="2a85c-120">Hello servizio DNS di Azure viene gestita dal provider di risorse Microsoft. Network hello.</span><span class="sxs-lookup"><span data-stu-id="2a85c-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="2a85c-121">La sottoscrizione di Azure deve essere registrato toouse questo provider di risorse prima di poter usare DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a85c-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="2a85c-122">Questa operazione viene eseguita una sola volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2a85c-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```