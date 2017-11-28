<span data-ttu-id="c1015-101">Per abilitare una reimpostazione dettagliata delle password nell'applicazione, è necessario creare criteri di reimpostazione delle password.</span><span class="sxs-lookup"><span data-stu-id="c1015-101">To enable fine-grained password reset on your application, you will need to create a password reset policy.</span></span> <span data-ttu-id="c1015-102">Annotare l'opzione di reimpostazione delle password a livello di tenant specificata [qui](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="c1015-102">Note that the tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="c1015-103">Questi criteri descrivono l'esperienza utente durante la procedura di reimpostazione delle password e il contenuto dei token che l'applicazione riceverà al completamento della procedura.</span><span class="sxs-lookup"><span data-stu-id="c1015-103">This policy describes the experiences that the consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="c1015-104">Nella sezione delle impostazioni relativa ai criteri selezionare **Criteri di reimpostazione password** e fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c1015-104">In the policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Selezionare i criteri di iscrizione o di accesso e fare clic sul pulsante Aggiungi](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="c1015-106">Immettere un **Nome** di criterio a cui l'applicazione può fare riferimento.</span><span class="sxs-lookup"><span data-stu-id="c1015-106">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="c1015-107">Ad esempio, immettere `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="c1015-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="c1015-108">Selezionare **Provider di identità** e quindi selezionare **Reimposta la password usando l'indirizzo di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="c1015-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="c1015-109">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c1015-109">Click **OK**.</span></span>

![Selezionare Reimposta la password usando l'indirizzo di posta elettronica come provider di identità e fare clic sul pulsante OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="c1015-111">Selezionare **Attestazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="c1015-111">Select **Application claims**.</span></span> <span data-ttu-id="c1015-112">Scegliere le attestazioni che devono essere restituite nei token di autorizzazione inviati all'applicazione dopo un'esperienza di reimpostazione della password riuscita.</span><span class="sxs-lookup"><span data-stu-id="c1015-112">Choose claims you want returned in the authorization tokens sent back to your application after a successful password reset experience.</span></span> <span data-ttu-id="c1015-113">Selezionare ad esempio **ID oggetto dell'utente**.</span><span class="sxs-lookup"><span data-stu-id="c1015-113">For example, select **User's Object ID**.</span></span>

![Selezionare alcune attestazioni dell'applicazione e fare clic sul pulsante OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="c1015-115">Fare clic su **Crea** per aggiungere il criterio.</span><span class="sxs-lookup"><span data-stu-id="c1015-115">Click **Create** to add the policy.</span></span> <span data-ttu-id="c1015-116">Il criterio viene elencato come **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="c1015-116">The policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="c1015-117">Il prefisso **B2C_1_** viene aggiunto al nome.</span><span class="sxs-lookup"><span data-stu-id="c1015-117">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="c1015-118">Aprire i criteri selezionando **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="c1015-118">Open the policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="c1015-119">Verificare le impostazioni specificate nella tabella e quindi fare clic su **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="c1015-119">Verify the settings specified in the table then click **Run now**.</span></span>

![Selezionare un criterio ed eseguirlo](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="c1015-121">Impostazione</span><span class="sxs-lookup"><span data-stu-id="c1015-121">Setting</span></span>      | <span data-ttu-id="c1015-122">Valore</span><span class="sxs-lookup"><span data-stu-id="c1015-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="c1015-123">**Applicazioni**</span><span class="sxs-lookup"><span data-stu-id="c1015-123">**Applications**</span></span> | <span data-ttu-id="c1015-124">App Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="c1015-124">Contoso B2C app</span></span> |
| <span data-ttu-id="c1015-125">**Selezionare l'URL di risposta**</span><span class="sxs-lookup"><span data-stu-id="c1015-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="c1015-126">Viene visualizzata una nuova scheda del browser ed è possibile verificare l'esperienza di reimpostazione della password dell'utente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c1015-126">A new browser tab opens, and you can verify the password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="c1015-127">La creazione e gli aggiornamenti dei criteri avranno effetto dopo circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="c1015-127">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
