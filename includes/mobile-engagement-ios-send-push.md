### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="06c44-101">Concedere accesso tooyour certificato Push tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="06c44-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="06c44-102">Engagement Mobile tooallow toosend le notifiche Push per conto dell'utente, è necessario accedere a certificato tooyour toogrant.</span><span class="sxs-lookup"><span data-stu-id="06c44-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="06c44-103">Questa operazione viene eseguita la configurazione e immettendo il certificato al portale Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="06c44-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="06c44-104">Assicurarsi di avere ottenuto il certificato con estensione p12 come descritto nella [documentazione di Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="06c44-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="06c44-105">Passare portale Mobile Engagement tooyour.</span><span class="sxs-lookup"><span data-stu-id="06c44-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="06c44-106">Verificare la corretta hello sono quindi fare clic su hello **attirare** pulsante nella parte inferiore di hello:</span><span class="sxs-lookup"><span data-stu-id="06c44-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="06c44-107">Fare clic su hello **impostazioni** pagina del portale del progetto.</span><span class="sxs-lookup"><span data-stu-id="06c44-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="06c44-108">Da scegliere è hello **Push nativo** sezione tooupload il certificato p12:</span><span class="sxs-lookup"><span data-stu-id="06c44-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="06c44-109">Selezionare il certificato p12, caricarlo e digitare la password:</span><span class="sxs-lookup"><span data-stu-id="06c44-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="06c44-110"><a id="send"></a>Invia un'app tooyour notifica</span><span class="sxs-lookup"><span data-stu-id="06c44-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="06c44-111">Verrà ora creata una semplice campagna di notifica Push che invierà un'app tooour push:</span><span class="sxs-lookup"><span data-stu-id="06c44-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="06c44-112">Passare toohello **raggiungere** scheda nel portale Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="06c44-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="06c44-113">Fare clic su **nuovo annuncio** toocreate la campagna push</span><span class="sxs-lookup"><span data-stu-id="06c44-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="06c44-114">I campi prima di hello della campagna del programma di installazione:</span><span class="sxs-lookup"><span data-stu-id="06c44-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="06c44-115">Fornire un **Nome** per la campagna</span><span class="sxs-lookup"><span data-stu-id="06c44-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="06c44-116">Seleziona hello **l'ora di recapito** come **all'esterno dell'app solo**: si tratta di hello Apple push notification tipo semplice che le funzionalità del testo.</span><span class="sxs-lookup"><span data-stu-id="06c44-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="06c44-117">Nel testo della notifica hello, digitare hello prima **titolo** che sarà hello nella prima riga push hello.</span><span class="sxs-lookup"><span data-stu-id="06c44-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="06c44-118">Digitare quindi il **messaggio** che sarà della seconda riga hello</span><span class="sxs-lookup"><span data-stu-id="06c44-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="06c44-119">Scorrere verso il basso e in hello sezione di contenuto selezionare **sola notifica**</span><span class="sxs-lookup"><span data-stu-id="06c44-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="06c44-120">Campagna più elementare di hello impostazione completata.</span><span class="sxs-lookup"><span data-stu-id="06c44-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="06c44-121">A questo punto, scorrere verso il basso e fare clic su **crea** pulsante toosave la campagna di notifica push.</span><span class="sxs-lookup"><span data-stu-id="06c44-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="06c44-122">Infine, fare clic su **attiva** notifica push toosend.</span><span class="sxs-lookup"><span data-stu-id="06c44-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="06c44-123">Sarà possibile ricevere una notifica di hello sul dispositivo iOS nell'area di notifica hello hello seguente:</span><span class="sxs-lookup"><span data-stu-id="06c44-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="06c44-124">Se si dispone di un Apple Watch associati a questo dispositivo iOS si vedrà notifica hello nel Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="06c44-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

