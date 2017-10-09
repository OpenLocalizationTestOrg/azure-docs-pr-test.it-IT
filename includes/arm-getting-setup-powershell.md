## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="5adc0-101">Configurazione di PowerShell per i modelli di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="5adc0-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="5adc0-102">Prima di poter utilizzare Azure PowerShell con Gestione risorse, sarà necessario toohave hello Windows PowerShell e Azure PowerShell versioni corrette.</span><span class="sxs-lookup"><span data-stu-id="5adc0-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="5adc0-103">Verificare le versioni di PowerShell</span><span class="sxs-lookup"><span data-stu-id="5adc0-103">Verify PowerShell versions</span></span>
<span data-ttu-id="5adc0-104">Verificare che la versione di Windows PowerShell in uso sia 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="5adc0-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="5adc0-105">versione di hello toofind di Windows PowerShell, digitare il comando seguente al prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5adc0-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="5adc0-106">Verrà visualizzato hello dopo il tipo di informazioni:</span><span class="sxs-lookup"><span data-stu-id="5adc0-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="5adc0-107">Verificare che il valore di hello **PSVersion** è 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="5adc0-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="5adc0-108">In caso contrario, vedere [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="5adc0-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="5adc0-109">Impostare l'account e la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="5adc0-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="5adc0-110">Se non si ha già una sottoscrizione di Azure, è possibile attivare i [benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5adc0-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="5adc0-111">Aprire un prompt dei comandi di Azure PowerShell e accedere tooAzure con questo comando.</span><span class="sxs-lookup"><span data-stu-id="5adc0-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="5adc0-112">Se si dispone di più sottoscrizioni di Azure, è possibile usare il comando seguente per visualizzarne l'elenco.</span><span class="sxs-lookup"><span data-stu-id="5adc0-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="5adc0-113">Verrà visualizzato hello dopo il tipo di informazioni:</span><span class="sxs-lookup"><span data-stu-id="5adc0-113">You will receive hello following type of information:</span></span>

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

<span data-ttu-id="5adc0-114">È possibile impostare la sottoscrizione di Azure corrente di hello mediante l'esecuzione di questi comandi al prompt dei comandi di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5adc0-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="5adc0-115">Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri, con il nome corretto hello.</span><span class="sxs-lookup"><span data-stu-id="5adc0-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="5adc0-116">Per ulteriori informazioni sull'account e le sottoscrizioni di Azure, vedere [procedura: connettere sottoscrizione tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="5adc0-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

