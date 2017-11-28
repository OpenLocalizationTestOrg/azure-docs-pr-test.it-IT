## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="d48cd-101">Configurazione di PowerShell per i modelli di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d48cd-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="d48cd-102">Prima di poter usare Azure PowerShell con Gestione risorse, è necessario verificare di disporre delle versioni corrette di Windows PowerShell e Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d48cd-102">Before you can use Azure PowerShell with Resource Manager, you will need to have the right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="d48cd-103">Verificare le versioni di PowerShell</span><span class="sxs-lookup"><span data-stu-id="d48cd-103">Verify PowerShell versions</span></span>
<span data-ttu-id="d48cd-104">Verificare che la versione di Windows PowerShell in uso sia 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="d48cd-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="d48cd-105">Per individuare la versione di Windows PowerShell, digitare il comando seguente al prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d48cd-105">To find the version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="d48cd-106">Verrà visualizzato il tipo di informazioni seguente:</span><span class="sxs-lookup"><span data-stu-id="d48cd-106">You will receive the following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="d48cd-107">Verificare che il valore di **PSVersion** sia 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="d48cd-107">Verify that the value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="d48cd-108">In caso contrario, vedere [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="d48cd-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="d48cd-109">Impostare l'account e la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="d48cd-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="d48cd-110">Se non si ha già una sottoscrizione di Azure, è possibile attivare i [benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d48cd-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="d48cd-111">Aprire un prompt dei comandi di Azure PowerShell e usare il comando seguente per accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="d48cd-111">Open an Azure PowerShell command prompt and log on to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="d48cd-112">Se si dispone di più sottoscrizioni di Azure, è possibile usare il comando seguente per visualizzarne l'elenco.</span><span class="sxs-lookup"><span data-stu-id="d48cd-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="d48cd-113">Verrà visualizzato il tipo di informazioni seguente:</span><span class="sxs-lookup"><span data-stu-id="d48cd-113">You will receive the following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="d48cd-114">Per impostare la sottoscrizione di Azure corrente, eseguire i comandi seguenti al prompt dei comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d48cd-114">You can set the current Azure subscription by running these commands at the Azure PowerShell command prompt.</span></span> <span data-ttu-id="d48cd-115">Sostituire tutti gli elementi all'interno delle virgolette, inclusi i caratteri < e >, con il nome corretto.</span><span class="sxs-lookup"><span data-stu-id="d48cd-115">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<SubscriptionName from the display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="d48cd-116">Per altre informazioni su sottoscrizioni e account di Azure, vedere [Procedura: Connettersi alla sottoscrizione](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="d48cd-116">For more information about Azure subscriptions and accounts, see [How to: Connect to your subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

