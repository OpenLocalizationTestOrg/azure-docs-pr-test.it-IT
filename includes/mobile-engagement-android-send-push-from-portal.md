### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="ee3bb-101">Engagement Mobile concedere accesso tooyour chiave API GCM</span><span class="sxs-lookup"><span data-stu-id="ee3bb-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="ee3bb-102">tooallow Mobile Engagement toosend delle notifiche push per conto dell'utente, è necessario accedere a tooyour chiave API toogrant.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="ee3bb-103">Questa operazione viene eseguita la configurazione e inserendo la chiave nel portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="ee3bb-104">Mediante il portale di Azure classico, verificare le app hello è in uso per questo progetto e quindi fare clic su hello **attirare** pulsante nella parte inferiore di hello:</span><span class="sxs-lookup"><span data-stu-id="ee3bb-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="ee3bb-105">Quindi fare clic su hello **impostazioni** -> **Push nativo** sezione tooenter la chiave GCM:</span><span class="sxs-lookup"><span data-stu-id="ee3bb-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="ee3bb-106">Fare clic su hello **modifica** icona davanti **chiave API** in hello **impostazioni GCM** sezione come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ee3bb-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="ee3bb-107">Nel menu a comparsa hello, incollare hello chiave Server GCM ottenuto prima e quindi fare clic su **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="ee3bb-108"><a id="send"></a>Invia un'app tooyour notifica</span><span class="sxs-lookup"><span data-stu-id="ee3bb-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="ee3bb-109">Verrà ora creata una campagna di notifica push semplice che invia un'app tooour di notifica push.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="ee3bb-110">Passare toohello **raggiungere** scheda nel portale Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="ee3bb-111">Fare clic su **nuovo annuncio** toocreate la campagna di notifica push.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="ee3bb-112">Impostare i campi prima di hello della campagna tramite hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ee3bb-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="ee3bb-113">a.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-113">a.</span></span> <span data-ttu-id="ee3bb-114">Assegnare un nome alla campagna.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-114">Name your campaign.</span></span>
   
    <span data-ttu-id="ee3bb-115">b.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-115">b.</span></span> <span data-ttu-id="ee3bb-116">Seleziona hello **tipo di recapito** come *notifica di sistema -> semplice*: tipo di notifica push Android semplice hello che le funzionalità di un titolo e una riga di piccole dimensioni di testo.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="ee3bb-117">c.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-117">c.</span></span> <span data-ttu-id="ee3bb-118">Selezionare **l'ora di recapito** come *qualsiasi momento* tooallow hello app tooreceive una notifica se l'applicazione hello è stato avviato o meno.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="ee3bb-119">d.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-119">d.</span></span> <span data-ttu-id="ee3bb-120">In hello di tipo testo notifica hello **titolo** che sarà grassetto in push hello.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="ee3bb-121">e.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-121">e.</span></span> <span data-ttu-id="ee3bb-122">Digitare quindi il **messaggio**</span><span class="sxs-lookup"><span data-stu-id="ee3bb-122">Then type your **Message**</span></span>
4. <span data-ttu-id="ee3bb-123">Scorrere verso il basso e in hello **contenuto** selezionare **sola notifica**.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="ee3bb-124">Possibili campagna più elementare di impostazione hello completato.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="ee3bb-125">Ora nuovamente a scorrere verso il basso e fare clic su hello **crea** pulsante toosave la campagna.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="ee3bb-126">Ultimo passaggio: scegliere **attiva** tooactivate le notifiche di push toosend campagna.</span><span class="sxs-lookup"><span data-stu-id="ee3bb-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

