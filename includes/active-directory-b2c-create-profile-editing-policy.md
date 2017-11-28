<span data-ttu-id="9b36b-101">Per abilitare la modifica del profilo nell'applicazione, è necessario creare i criteri di modifica del profilo.</span><span class="sxs-lookup"><span data-stu-id="9b36b-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="9b36b-102">Questi criteri descrivono l'esperienza utente durante la procedura di modifica del profilo e il contenuto dei token che l'applicazione riceverà al completamento della procedura.</span><span class="sxs-lookup"><span data-stu-id="9b36b-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="9b36b-103">Nella sezione delle impostazioni relativa ai criteri selezionare **Criteri di modifica del profilo** e fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Selezionare Criteri di modifica del profilo e fare clic sul pulsante Aggiungi](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="9b36b-105">Immettere un **Nome** di criterio a cui l'applicazione può fare riferimento.</span><span class="sxs-lookup"><span data-stu-id="9b36b-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="9b36b-106">Ad esempio, immettere `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="9b36b-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="9b36b-107">Selezionare **Provider di identità** e quindi selezionare**Accesso all'account locale**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="9b36b-108">Facoltativamente, è anche possibile selezionare i provider di identità tramite social network, se già configurati.</span><span class="sxs-lookup"><span data-stu-id="9b36b-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="9b36b-109">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-109">Click **OK**.</span></span>

![Selezionare Accesso all'account locale come provider di identità e quindi fare clic sul pulsante OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="9b36b-111">Selezionare **Attributi del profilo**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-111">Select **Profile attributes**.</span></span> <span data-ttu-id="9b36b-112">Scegliere gli attributi che l'utente può visualizzare e modificare nel profilo.</span><span class="sxs-lookup"><span data-stu-id="9b36b-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="9b36b-113">Selezionare ad esempio **Paese/area geografica**, **Nome visualizzato** e **Codice postale**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="9b36b-114">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-114">Click **OK**.</span></span>

![Selezionare alcuni attributi e fare clic sul pulsante OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="9b36b-116">Selezionare **Attestazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-116">Select **Application claims**.</span></span> <span data-ttu-id="9b36b-117">Scegliere le attestazioni che devono essere restituite nei token di autorizzazione inviati all'applicazione dopo un'esperienza di modifica del profilo riuscita.</span><span class="sxs-lookup"><span data-stu-id="9b36b-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="9b36b-118">Selezionare ad esempio **Nome visualizzato** e **Codice postale**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Selezionare alcune attestazioni dell'applicazione e fare clic sul pulsante OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="9b36b-120">Fare clic su **Crea** per aggiungere il criterio.</span><span class="sxs-lookup"><span data-stu-id="9b36b-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="9b36b-121">Il criterio viene elencato come **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="9b36b-122">Il prefisso **B2C_1_** viene aggiunto al nome.</span><span class="sxs-lookup"><span data-stu-id="9b36b-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="9b36b-123">Aprire i criteri selezionando **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="9b36b-124">Verificare le impostazioni specificate nella tabella e quindi fare clic su **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="9b36b-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Selezionare un criterio ed eseguirlo](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="9b36b-126">Impostazione</span><span class="sxs-lookup"><span data-stu-id="9b36b-126">Setting</span></span>      | <span data-ttu-id="9b36b-127">Valore</span><span class="sxs-lookup"><span data-stu-id="9b36b-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="9b36b-128">**Applicazioni**</span><span class="sxs-lookup"><span data-stu-id="9b36b-128">**Applications**</span></span> | <span data-ttu-id="9b36b-129">App Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="9b36b-129">Contoso B2C app</span></span> |
| <span data-ttu-id="9b36b-130">**Selezionare l'URL di risposta**</span><span class="sxs-lookup"><span data-stu-id="9b36b-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="9b36b-131">Viene visualizzata una nuova scheda del browser ed è possibile verificare l'esperienza di modifica del profilo dell'utente in base alla configurazione specificata.</span><span class="sxs-lookup"><span data-stu-id="9b36b-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="9b36b-132">La creazione e gli aggiornamenti dei criteri avranno effetto dopo circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="9b36b-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>