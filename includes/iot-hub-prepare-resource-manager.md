## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="af183-101">Preparare Gestione risorse di Azure richiede tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="af183-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="af183-102">È necessario autenticare tutte le operazioni eseguite sulle risorse con hello hello [Azure Resource Manager] [ lnk-authenticate-arm] con Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="af183-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="af183-103">Hello tooconfigure modo più semplice è toouse PowerShell o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="af183-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="af183-104">Installare hello [cmdlet di Azure PowerShell] [ lnk-powershell-install] prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="af183-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="af183-105">Hello seguente procedura mostra come tooset autenticazione tramite password per un'applicazione di Active Directory tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af183-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="af183-106">È possibile eseguire questi comandi in una sessione standard di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af183-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="af183-107">Accedi tooyour sottoscrizione di Azure utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af183-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="af183-108">Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello le sottoscrizioni di Azure associate con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="af183-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="af183-109">Utilizzare hello toolist hello Azure sottoscrizioni disponibili per l'utente toouse comando seguente:</span><span class="sxs-lookup"><span data-stu-id="af183-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="af183-110">Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toomanage l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="af183-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="af183-111">È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="af183-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="af183-112">Prendere nota dei valori di **TenantId** e **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="af183-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="af183-113">Saranno necessari più avanti.</span><span class="sxs-lookup"><span data-stu-id="af183-113">You need them later.</span></span>
3. <span data-ttu-id="af183-114">Creare una nuova applicazione di Azure Active Directory utilizzando hello comando seguente, sostituendo i segnaposto hello:</span><span class="sxs-lookup"><span data-stu-id="af183-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="af183-115">**{Display name}:** un nome visualizzato per l'applicazione, ad esempio **MySampleApp**.</span><span class="sxs-lookup"><span data-stu-id="af183-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="af183-116">**{URL della Home page}:** hello URL della home page di hello dell'app, ad esempio **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="af183-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="af183-117">Questo URL non è necessario toopoint tooa reali dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="af183-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="af183-118">**{Application identifier}:** un identificatore univoco, ad esempio **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="af183-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="af183-119">Questo URL non è necessario toopoint tooa reali dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="af183-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="af183-120">**{Password}:** una password usata tooauthenticate con l'app.</span><span class="sxs-lookup"><span data-stu-id="af183-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="af183-121">Prendere nota di hello **ApplicationId** dell'applicazione hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="af183-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="af183-122">Sarà necessario più avanti.</span><span class="sxs-lookup"><span data-stu-id="af183-122">You need this later.</span></span>
5. <span data-ttu-id="af183-123">Creare una nuova entità servizio utilizzando hello comando seguente, sostituendo **{MyApplicationId}** con hello **ApplicationId** dal passaggio precedente hello:</span><span class="sxs-lookup"><span data-stu-id="af183-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="af183-124">Impostare un'assegnazione di ruolo utilizzando hello comando seguente, sostituendo **{MyApplicationId}** con il **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="af183-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="af183-125">Completata Creazione hello Azure AD è un'applicazione tooauthenticate dall'applicazione c# personalizzata.</span><span class="sxs-lookup"><span data-stu-id="af183-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="af183-126">È necessario hello seguente i valori più avanti in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="af183-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="af183-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="af183-127">TenantId</span></span>
* <span data-ttu-id="af183-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="af183-128">SubscriptionId</span></span>
* <span data-ttu-id="af183-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="af183-129">ApplicationId</span></span>
* <span data-ttu-id="af183-130">Password</span><span class="sxs-lookup"><span data-stu-id="af183-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
