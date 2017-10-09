<span data-ttu-id="72895-101">profilo tooenable modifica sull'applicazione, sarà necessario toocreate un modifica dei criteri del profilo.</span><span class="sxs-lookup"><span data-stu-id="72895-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="72895-102">Questo criterio viene esperienze hello consumer passerà tramite durante il contenuto di modifica e hello profilo di token che un'applicazione hello riceverà il corretto completamento.</span><span class="sxs-lookup"><span data-stu-id="72895-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="72895-103">Nella sezione criteri hello delle impostazioni selezionare **modifica i criteri del profilo** e fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72895-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Selezionare i criteri di modifica del profilo e fare clic sul pulsante Aggiungi hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="72895-105">Immettere un criterio **nome** per tooreference l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="72895-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="72895-106">Ad esempio, immettere `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="72895-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="72895-107">Selezionare **Provider di identità** e quindi selezionare**Accesso all'account locale**.</span><span class="sxs-lookup"><span data-stu-id="72895-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="72895-108">Facoltativamente, è anche possibile selezionare i provider di identità tramite social network, se già configurati.</span><span class="sxs-lookup"><span data-stu-id="72895-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="72895-109">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="72895-109">Click **OK**.</span></span>

![Selezionare Signin Account locale come provider di identità e fare clic sul pulsante OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="72895-111">Selezionare **Attributi del profilo**.</span><span class="sxs-lookup"><span data-stu-id="72895-111">Select **Profile attributes**.</span></span> <span data-ttu-id="72895-112">Scegliere di visualizzare e modificare nel loro profilo consumer hello attributi.</span><span class="sxs-lookup"><span data-stu-id="72895-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="72895-113">Selezionare ad esempio **Paese/area geografica**, **Nome visualizzato** e **Codice postale**.</span><span class="sxs-lookup"><span data-stu-id="72895-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="72895-114">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="72895-114">Click **OK**.</span></span>

![Selezionare alcuni attributi e fare clic sul pulsante OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="72895-116">Selezionare **Attestazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="72895-116">Select **Application claims**.</span></span> <span data-ttu-id="72895-117">Scegliere le attestazioni da includere nel token di autorizzazione hello inviati applicazione back-tooyour dopo un profilo di esito positivo di un'esperienza di modifica.</span><span class="sxs-lookup"><span data-stu-id="72895-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="72895-118">Selezionare ad esempio **Nome visualizzato** e **Codice postale**.</span><span class="sxs-lookup"><span data-stu-id="72895-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Selezionare alcune attestazioni dell'applicazione e fare clic sul pulsante OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="72895-120">Fare clic su **crea** criteri hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="72895-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="72895-121">criteri di Hello sono elencato come **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="72895-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="72895-122">Hello **B2C_1_** prefisso viene aggiunto toohello nome.</span><span class="sxs-lookup"><span data-stu-id="72895-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="72895-123">Aprire criteri hello selezionando **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="72895-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="72895-124">Verificare le impostazioni di hello specificate nella tabella hello, quindi fare clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="72895-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selezionare un criterio ed eseguirlo](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="72895-126">Impostazione</span><span class="sxs-lookup"><span data-stu-id="72895-126">Setting</span></span>      | <span data-ttu-id="72895-127">Valore</span><span class="sxs-lookup"><span data-stu-id="72895-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="72895-128">**Applicazioni**</span><span class="sxs-lookup"><span data-stu-id="72895-128">**Applications**</span></span> | <span data-ttu-id="72895-129">App Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="72895-129">Contoso B2C app</span></span> |
| <span data-ttu-id="72895-130">**Selezionare l'URL di risposta**</span><span class="sxs-lookup"><span data-stu-id="72895-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="72895-131">Verrà visualizzata una nuova scheda del browser e si può verificare il profilo di hello consumer esperienza di modifica, come configurato.</span><span class="sxs-lookup"><span data-stu-id="72895-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="72895-132">Occupi tooa minuto per la creazione dei criteri e aggiorna tootake effetto.</span><span class="sxs-lookup"><span data-stu-id="72895-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>