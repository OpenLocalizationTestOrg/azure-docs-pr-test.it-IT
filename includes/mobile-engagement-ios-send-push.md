### <a name="grant-access-to-your-push-certificate-to-mobile-engagement"></a><span data-ttu-id="a7d20-101">Concedere a Mobile Engagement l'accesso al certificato push</span><span class="sxs-lookup"><span data-stu-id="a7d20-101">Grant access to your Push Certificate to Mobile Engagement</span></span>
<span data-ttu-id="a7d20-102">Per consentire a Mobile Engagement di inviare notifiche push per conto dell'utente, è necessario concedere l'accesso al certificato.</span><span class="sxs-lookup"><span data-stu-id="a7d20-102">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your certificate.</span></span> <span data-ttu-id="a7d20-103">A tale scopo, è necessario configurare il certificato e immetterlo nel portale di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a7d20-103">This is done by configuring and entering your certificate into the Mobile Engagement portal.</span></span> <span data-ttu-id="a7d20-104">Assicurarsi di avere ottenuto il certificato con estensione p12 come descritto nella [documentazione di Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="a7d20-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="a7d20-105">Passare al portale di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a7d20-105">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="a7d20-106">Verificare la posizione corretta e fare clic sul pulsante **Attiva** nella parte inferiore:</span><span class="sxs-lookup"><span data-stu-id="a7d20-106">Ensure you're in the correct and then click on the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="a7d20-107">Verrà visualizzata la pagina **Impostazioni** nel portale di Engagement.</span><span class="sxs-lookup"><span data-stu-id="a7d20-107">Click on the **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="a7d20-108">Da questa posizione fare clic sulla sezione **Push nativo** per aprire il certificato p12:</span><span class="sxs-lookup"><span data-stu-id="a7d20-108">From there click on the **Native Push** section to upload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="a7d20-109">Selezionare il certificato p12, caricarlo e digitare la password:</span><span class="sxs-lookup"><span data-stu-id="a7d20-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="a7d20-110"><a id="send"></a>Inviare una notifica all'app</span><span class="sxs-lookup"><span data-stu-id="a7d20-110"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="a7d20-111">Si creerà ora una semplice campagna di notifica push per l'invio di un push all'app.</span><span class="sxs-lookup"><span data-stu-id="a7d20-111">We will now create a simple Push Notification campaign that will send a push to our app:</span></span>

1. <span data-ttu-id="a7d20-112">Passare alla scheda **Reach** nel portale di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a7d20-112">Navigate to the **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="a7d20-113">Fare clic su **Nuovo annuncio** per creare la campagna di push.</span><span class="sxs-lookup"><span data-stu-id="a7d20-113">Click **New Announcement** to create your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="a7d20-114">Configurare i primi campi della campagna:</span><span class="sxs-lookup"><span data-stu-id="a7d20-114">Setup the first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="a7d20-115">Fornire un **Nome** per la campagna</span><span class="sxs-lookup"><span data-stu-id="a7d20-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="a7d20-116">Per **Ora di consegna** selezionare **Out of app only** (Solo all'esterno dell'app): si tratta di un tipo di notifica push Apple semplice che include testo.</span><span class="sxs-lookup"><span data-stu-id="a7d20-116">Select the **Delivery time** as **Out of app only**: this is the simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="a7d20-117">Nel testo della notifica digitare innanzitutto il **titolo** che sarà la prima riga del push.</span><span class="sxs-lookup"><span data-stu-id="a7d20-117">In the notification text, type first the **Title** which will be the first line in the push.</span></span>
   * <span data-ttu-id="a7d20-118">Digitare quindi il **messaggio** che costituirà la seconda riga</span><span class="sxs-lookup"><span data-stu-id="a7d20-118">Then type your **Message** which will be the second line</span></span>
4. <span data-ttu-id="a7d20-119">Scorrere verso il basso e nella sezione contenuto selezionare **Solo notifica**</span><span class="sxs-lookup"><span data-stu-id="a7d20-119">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="a7d20-120">L'impostazione della campagna più semplice è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a7d20-120">You're done setting the most basic campaign.</span></span> <span data-ttu-id="a7d20-121">Ora scorrere verso il basso e fare clic sul pulsante **Crea** per salvare la campagna di notifica push.</span><span class="sxs-lookup"><span data-stu-id="a7d20-121">Now scroll down and click on **Create** button to save your push notification campaign.</span></span> 
6. <span data-ttu-id="a7d20-122">Infine, fare clic sul **Attiva** per inviare notifiche push.</span><span class="sxs-lookup"><span data-stu-id="a7d20-122">Finally - click on **Activate** to send push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="a7d20-123">Sarà possibile ricevere la notifica sul dispositivo iOS nel centro di notifica, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a7d20-123">You will be able receive the notification on your iOS device in the notification center like the following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="a7d20-124">Se si dispone di un controllo Apple abbinato a questo dispositivo iOS, allora verrà visualizzata la notifica nel controllo Apple:</span><span class="sxs-lookup"><span data-stu-id="a7d20-124">If you have an Apple Watch paired with this iOS device then you will see the notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

