## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="d8ef4-101">Prepararsi all'autenticazione delle richieste di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8ef4-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="d8ef4-102">Si devono autenticare tutte le attività da eseguire sulle risorse mediante [Gestione risorse di Azure][lnk-authenticate-arm] con Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="d8ef4-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="d8ef4-103">Il modo più semplice per configurare questa impostazione è usare PowerShell o l’interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="d8ef4-104">Installare i [cmdlet di Azure PowerShell][lnk-powershell-install] prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-104">Install the [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="d8ef4-105">La procedura seguente illustra come configurare l'autenticazione della password per un'applicazione di AD mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="d8ef4-106">È possibile eseguire questi comandi in una sessione standard di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="d8ef4-107">Accedere alla sottoscrizione di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8ef4-107">Log in to your Azure subscription using the following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="d8ef4-108">Se si usano più sottoscrizioni Azure e si esegue l'accesso ad Azure, è possibile accedere a tutte le sottoscrizioni di Azure associate alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-108">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="d8ef4-109">Usare il comando seguente per elencare gli account Azure che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="d8ef4-109">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="d8ef4-110">Usare il comando seguente per selezionare la sottoscrizione che si vuole usare per eseguire i comandi per gestire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-110">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="d8ef4-111">È possibile usare il nome o l'ID della sottoscrizione dall'output del comando precedente:</span><span class="sxs-lookup"><span data-stu-id="d8ef4-111">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="d8ef4-112">Prendere nota dei valori di **TenantId** e **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="d8ef4-113">Saranno necessari più avanti.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-113">You need them later.</span></span>
3. <span data-ttu-id="d8ef4-114">Creare una nuova applicazione Azure Active Directory mediante il comando seguente, sostituendo i segnaposto:</span><span class="sxs-lookup"><span data-stu-id="d8ef4-114">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="d8ef4-115">**{Display name}:** un nome visualizzato per l'applicazione, ad esempio **MySampleApp**.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="d8ef4-116">**{Home page URL}:** l'URL della home page dell'app, ad esempio **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-116">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="d8ef4-117">Non è necessario che questo URL punti a un'applicazione reale.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-117">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="d8ef4-118">**{Application identifier}:** un identificatore univoco, ad esempio **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="d8ef4-119">Non è necessario che questo URL punti a un'applicazione reale.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-119">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="d8ef4-120">**{Password}:** password da usare per l'autenticazione con l'app.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-120">**{Password}:** A password that you use to authenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="d8ef4-121">Annotare l’ **ApplicationId** dell'applicazione creata.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-121">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="d8ef4-122">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-122">You need this later.</span></span>
5. <span data-ttu-id="d8ef4-123">Creare una nuova entità servizio usando il comando seguente, sostituendo **{MyApplicationId}** con il valore di **ApplicationId** del passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="d8ef4-123">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="d8ef4-124">Configurare un'assegnazione di ruolo usando il comando seguente, sostituendo **{MyApplicationId}** con il valore di **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-124">Set up a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="d8ef4-125">A questo punto è terminata la creazione dell'applicazione Azure AD che consentirà di eseguire l'autenticazione dall'applicazione C# personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d8ef4-125">You have now finished creating the Azure AD application that enables you to authenticate from your custom C# application.</span></span> <span data-ttu-id="d8ef4-126">Più avanti in questa esercitazione saranno necessari i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8ef4-126">You need the following values later in this tutorial:</span></span>

* <span data-ttu-id="d8ef4-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="d8ef4-127">TenantId</span></span>
* <span data-ttu-id="d8ef4-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="d8ef4-128">SubscriptionId</span></span>
* <span data-ttu-id="d8ef4-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="d8ef4-129">ApplicationId</span></span>
* <span data-ttu-id="d8ef4-130">Password</span><span class="sxs-lookup"><span data-stu-id="d8ef4-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
