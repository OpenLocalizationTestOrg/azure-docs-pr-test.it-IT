<span data-ttu-id="87b57-101">tooenable accurato la reimpostazione della password nell'applicazione, sarà necessario toocreate un criterio di reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="87b57-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="87b57-102">Si noti che la password a livello di tenant hello Reimposta l'opzione specificata [qui](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="87b57-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="87b57-103">Questo criterio viene esperienze hello consumer hello passa attraverso durante la reimpostazione della password e verrà visualizzato il contenuto di hello di token che hello applicazione al termine dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="87b57-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="87b57-104">Nella sezione criteri hello delle impostazioni selezionare **criteri di reimpostazione della Password** e fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="87b57-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Selezionare i criteri di iscrizione o accesso e fare clic sul pulsante Aggiungi hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="87b57-106">Immettere un criterio **nome** per tooreference l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="87b57-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="87b57-107">Ad esempio, immettere `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="87b57-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="87b57-108">Selezionare **Provider di identità** e quindi selezionare **Reimposta la password usando l'indirizzo di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="87b57-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="87b57-109">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="87b57-109">Click **OK**.</span></span>

![Selezionare la reimpostazione della password utilizzando l'indirizzo di posta elettronica come provider di identità e fare clic sul pulsante OK hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="87b57-111">Selezionare **Attestazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="87b57-111">Select **Application claims**.</span></span> <span data-ttu-id="87b57-112">Scegliere le attestazioni da includere nel token di autorizzazione hello inviati tooyour indietro applicazione dopo la reimpostazione della password riuscita esperienza.</span><span class="sxs-lookup"><span data-stu-id="87b57-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="87b57-113">Selezionare ad esempio **ID oggetto dell'utente**.</span><span class="sxs-lookup"><span data-stu-id="87b57-113">For example, select **User's Object ID**.</span></span>

![Selezionare alcune attestazioni dell'applicazione e fare clic sul pulsante OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="87b57-115">Fare clic su **crea** criteri hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="87b57-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="87b57-116">criteri di Hello sono elencato come **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="87b57-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="87b57-117">Hello **B2C_1_** prefisso viene aggiunto toohello nome.</span><span class="sxs-lookup"><span data-stu-id="87b57-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="87b57-118">Aprire criteri hello selezionando **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="87b57-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="87b57-119">Verificare le impostazioni di hello specificate nella tabella hello, quindi fare clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="87b57-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selezionare un criterio ed eseguirlo](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="87b57-121">Impostazione</span><span class="sxs-lookup"><span data-stu-id="87b57-121">Setting</span></span>      | <span data-ttu-id="87b57-122">Valore</span><span class="sxs-lookup"><span data-stu-id="87b57-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="87b57-123">**Applicazioni**</span><span class="sxs-lookup"><span data-stu-id="87b57-123">**Applications**</span></span> | <span data-ttu-id="87b57-124">App Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="87b57-124">Contoso B2C app</span></span> |
| <span data-ttu-id="87b57-125">**Selezionare l'URL di risposta**</span><span class="sxs-lookup"><span data-stu-id="87b57-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="87b57-126">Verrà visualizzata una nuova scheda del browser e per verificare l'esperienza utente dell'applicazione di reimpostazione della password hello.</span><span class="sxs-lookup"><span data-stu-id="87b57-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="87b57-127">Occupi tooa minuto per la creazione dei criteri e aggiorna tootake effetto.</span><span class="sxs-lookup"><span data-stu-id="87b57-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
