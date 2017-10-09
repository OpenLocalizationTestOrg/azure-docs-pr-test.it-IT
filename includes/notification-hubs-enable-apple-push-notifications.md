

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="53602-101">Generare file di richiesta di firma certificato hello</span><span class="sxs-lookup"><span data-stu-id="53602-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="53602-102">Hello Apple Push Notification Service (APNS) utilizza certificati tooauthenticate le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="53602-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="53602-103">Seguire questi toosend certificato push necessarie di istruzioni toocreate hello e ricevere le notifiche.</span><span class="sxs-lookup"><span data-stu-id="53602-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="53602-104">Per ulteriori informazioni su questi concetti, vedere ufficiale hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentazione.</span><span class="sxs-lookup"><span data-stu-id="53602-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="53602-105">Creare file di firma richiesta certificato (CSR) hello, che viene utilizzato da toogenerate Apple un certificato firmato push.</span><span class="sxs-lookup"><span data-stu-id="53602-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="53602-106">Nel Mac, eseguire lo strumento di accesso portachiavi hello.</span><span class="sxs-lookup"><span data-stu-id="53602-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="53602-107">Può essere aperta da hello **utilità** cartella o hello **altri** cartella nel punto di partenza hello.</span><span class="sxs-lookup"><span data-stu-id="53602-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="53602-108">Fare clic su **Keychain Access** (Accesso Portachiavi), espandere **Certificate Assistant** (Assistente Certificato), quindi fare clic su **Request a Certificate from a Certificate Authority...** (Richiedi un certificato da una Autorità di Certificazione...).</span><span class="sxs-lookup"><span data-stu-id="53602-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="53602-109">Selezionare il **indirizzo di posta elettronica utente** e **nome comune** , assicurarsi che **salvato toodisk** sia selezionata e quindi fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="53602-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="53602-110">Lasciare hello **indirizzo di posta elettronica CA** campo vuoto perché non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="53602-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="53602-111">Digitare un nome per il file di firma richiesta certificato (CSR) hello in **Salva con nome**, selezionare il percorso di hello in **in**, quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="53602-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="53602-112">Questo file CSR di hello Salva nel percorso di hello selezionato. percorso predefinito di Hello è hello Desktop.</span><span class="sxs-lookup"><span data-stu-id="53602-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="53602-113">Tenere presente che il percorso di hello scelto per il file.</span><span class="sxs-lookup"><span data-stu-id="53602-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="53602-114">Successivamente, si verrà registrare l'app di Apple, abilitare le notifiche push e caricare questo toocreate CSR esportato un certificato per il push.</span><span class="sxs-lookup"><span data-stu-id="53602-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="53602-115">Registrare l'app per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="53602-115">Register your app for push notifications</span></span>
<span data-ttu-id="53602-116">toobe toosend in grado di push notifiche tooan app iOS, è necessario registrare l'applicazione con Apple e registrate per le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="53602-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="53602-117">Se non è già stato registrato l'app, passare toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">portale di Provisioning iOS</a> in hello Centro per sviluppatori di Apple, eseguire l'accesso con il proprio ID Apple, fare clic su **identificatori**, quindi fare clic su **ID App** e infine fare clic su hello  **+**  tooregister una nuova app di accedere.</span><span class="sxs-lookup"><span data-stu-id="53602-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="53602-118">Aggiornare i seguenti tre campi per la nuova app hello e quindi fare clic su **continua**:</span><span class="sxs-lookup"><span data-stu-id="53602-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="53602-119">**Nome**: digitare un nome descrittivo per l'app in hello **nome** campo hello **descrizione dell'ID App** sezione.</span><span class="sxs-lookup"><span data-stu-id="53602-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="53602-120">**Identificatore di aggregazione**: in hello **ID App esplicito** sezione, immettere un **identificatore Bundle** nel modulo hello `<Organization Identifier>.<Product Name>` come indicato in hello [distribuzione di App Guida](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="53602-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="53602-121">Hello *identificatore organizzazione* e *nome prodotto* uso deve corrispondere identificatore organizzazione hello e il nome di prodotto che verrà utilizzato quando si crea il progetto XCode.</span><span class="sxs-lookup"><span data-stu-id="53602-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="53602-122">In seguito screeshot di hello *degli hub di notifica* viene utilizzato come l'identificatore di un'organizzazione e *GetStarted* viene utilizzato come nome del prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="53602-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="53602-123">Assicurandosi che corrisponde valori hello che verranno utilizzati nel progetto XCode consentirà è toouse hello corretto profilo di pubblicazione con XCode.</span><span class="sxs-lookup"><span data-stu-id="53602-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="53602-124">**Le notifiche push**: hello controllo **le notifiche Push** opzione hello **servizi App** sezione.</span><span class="sxs-lookup"><span data-stu-id="53602-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="53602-125">Questo genera l'ID di App e si richiede informazioni hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="53602-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="53602-126">Fare clic su **registrare** tooconfirm hello nuovo ID di App.</span><span class="sxs-lookup"><span data-stu-id="53602-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="53602-127">Quando si fa clic su **registrare**, verrà visualizzato hello **registrazione completare** schermata, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="53602-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="53602-128">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="53602-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="53602-129">Nel centro per sviluppatori, con l'ID dell'App, hello individuare hello app ID appena creato, quindi fare clic sulla riga corrispondente.</span><span class="sxs-lookup"><span data-stu-id="53602-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="53602-130">Facendo clic sull'ID di app hello verranno visualizzati i dettagli dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="53602-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="53602-131">Fare clic su hello **modifica** pulsante nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="53602-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="53602-132">Scorrere toohello parte inferiore della schermata di hello e fare clic su hello **Create Certificate...**  pulsante nella sezione hello **certificato SSL di Push di sviluppo**.</span><span class="sxs-lookup"><span data-stu-id="53602-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="53602-133">Consente di visualizzare Assistente "Aggiungi certificato iOS" hello.</span><span class="sxs-lookup"><span data-stu-id="53602-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="53602-134">Questa esercitazione usa un certificato di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="53602-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="53602-135">Hello stesso processo viene utilizzato durante la registrazione di un certificato di produzione.</span><span class="sxs-lookup"><span data-stu-id="53602-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="53602-136">Assicurarsi di utilizzare hello stesso quando si inviano notifiche di tipo di certificato.</span><span class="sxs-lookup"><span data-stu-id="53602-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="53602-137">Fare clic su **Scegli File**, toohello percorso di salvataggio file CSR hello creato nella prima attività hello Sfoglia, quindi fare clic su **genera**.</span><span class="sxs-lookup"><span data-stu-id="53602-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="53602-138">Dopo aver creato il certificato di hello dal portale di hello, fare clic su hello **scaricare** pulsante e fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="53602-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="53602-139">Questo download certificato hello e lo salva tooyour computer nella cartella di download.</span><span class="sxs-lookup"><span data-stu-id="53602-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="53602-140">Per impostazione predefinita, hello scaricati file un certificato di sviluppo è denominato **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="53602-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="53602-141">Fare doppio clic sul certificato scaricato push hello **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="53602-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="53602-142">Questo modo vengono installati nuovo certificato hello hello Keychain, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="53602-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="53602-143">nome Hello nel certificato potrebbe essere diverso, ma verrà preceduto **sviluppo Apple iOS servizi Push:**.</span><span class="sxs-lookup"><span data-stu-id="53602-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="53602-144">In accesso portachiavi, fare clic sul certificato push nuova hello creati in hello **certificati** categoria.</span><span class="sxs-lookup"><span data-stu-id="53602-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="53602-145">Fare clic su **esportare**, assegnare un nome file hello, selezionare hello **. p12** formattare e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="53602-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="53602-146">Prendere nota del nome file hello e percorso del certificato esportato. p12 hello.</span><span class="sxs-lookup"><span data-stu-id="53602-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="53602-147">Sarà tooenable utilizzata l'autenticazione con il servizio APN.</span><span class="sxs-lookup"><span data-stu-id="53602-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="53602-148">In questa esercitazione viene creato un file QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="53602-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="53602-149">Il nome e il percorso del file potrebbero essere diversi.</span><span class="sxs-lookup"><span data-stu-id="53602-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="53602-150">Creare un profilo di provisioning per l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="53602-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="53602-151">In hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">portale di Provisioning iOS</a>selezionare **i profili di Provisioning**selezionare **tutti**e quindi fare clic su hello  **+**  pulsante toocreate un nuovo profilo.</span><span class="sxs-lookup"><span data-stu-id="53602-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="53602-152">Verrà avviata hello **aggiungere Provisiong profilo iOS** guidata</span><span class="sxs-lookup"><span data-stu-id="53602-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="53602-153">Selezionare **lo sviluppo di App iOS** in **sviluppo** come tipo di profilo provisiong hello, fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="53602-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="53602-154">Selezionare quindi l'ID app hello appena creata dal hello **ID App** elenco a discesa e fare clic su **continua**</span><span class="sxs-lookup"><span data-stu-id="53602-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="53602-155">In hello **selezionare certificati** schermata, selezionare il certificato di sviluppo consuete utilizzato per la firma del codice e fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="53602-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="53602-156">Non si tratta del certificato per push hello che appena creato.</span><span class="sxs-lookup"><span data-stu-id="53602-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="53602-157">Selezionare quindi hello **dispositivi** toouse per i test e fare clic su **continua**</span><span class="sxs-lookup"><span data-stu-id="53602-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="53602-158">Infine, scegliere un nome per il profilo di hello in **nome profilo**, fare clic su **genera**.</span><span class="sxs-lookup"><span data-stu-id="53602-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="53602-159">Quando viene creato nuovo profilo di provisioning hello fare clic su toodownload e installazione sul computer di sviluppo Xcode.</span><span class="sxs-lookup"><span data-stu-id="53602-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="53602-160">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="53602-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
