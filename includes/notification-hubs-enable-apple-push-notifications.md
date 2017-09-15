

## <a name="generate-the-certificate-signing-request-file"></a><span data-ttu-id="f89fc-101">Generare il file di richiesta di firma del certificato</span><span class="sxs-lookup"><span data-stu-id="f89fc-101">Generate the Certificate Signing Request file</span></span>
<span data-ttu-id="f89fc-102">Il servizio Apple Push Notification Service (APNS) usa i certificati per autenticare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="f89fc-102">The Apple Push Notification Service (APNS) uses certificates to authenticate your push notifications.</span></span> <span data-ttu-id="f89fc-103">Seguire queste istruzioni per creare il certificato push necessario per inviare e ricevere notifiche.</span><span class="sxs-lookup"><span data-stu-id="f89fc-103">Follow these instructions to create the necessary push certificate to send and receive notifications.</span></span> <span data-ttu-id="f89fc-104">Per altre informazioni su questi concetti, vedere la documentazione ufficiale relativa al servizio [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) .</span><span class="sxs-lookup"><span data-stu-id="f89fc-104">For more information on these concepts see the official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="f89fc-105">Generare il file della richiesta di firma del certificato usato da Apple per la generazione di un certificato push firmato.</span><span class="sxs-lookup"><span data-stu-id="f89fc-105">Generate the Certificate Signing Request (CSR) file, which is used by Apple to generate a signed push certificate.</span></span>

1. <span data-ttu-id="f89fc-106">Sul Mac eseguire lo strumento Accesso Portachiavi.</span><span class="sxs-lookup"><span data-stu-id="f89fc-106">On your Mac, run the Keychain Access tool.</span></span> <span data-ttu-id="f89fc-107">Può essere aperto dalla cartella **Utilities** (Utility) o **Other** (Altro) nella finestra di avvio.</span><span class="sxs-lookup"><span data-stu-id="f89fc-107">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span></span>
2. <span data-ttu-id="f89fc-108">Fare clic su **Keychain Access** (Accesso Portachiavi), espandere **Certificate Assistant** (Assistente Certificato), quindi fare clic su **Request a Certificate from a Certificate Authority...** (Richiedi un certificato da una Autorità di Certificazione...).</span><span class="sxs-lookup"><span data-stu-id="f89fc-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="f89fc-109">Selezionare **User Email Address** (Indirizzo e-mail utente) e **Common Name** (Nome comune), assicurarsi che l'opzione **Saved to disk** (Salvata sul disco) sia selezionata, quindi fare clic su **Continue** (Continua).</span><span class="sxs-lookup"><span data-stu-id="f89fc-109">Select your **User Email Address** and **Common Name** , make sure that **Saved to disk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="f89fc-110">Lasciare vuoto il campo **Indirizzo e-mail CA** , in quanto non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f89fc-110">Leave the **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="f89fc-111">Digitare un nome per il file della richiesta di firma del certificato (CSR) in **Save As**, (Salva col nome), selezionare il percorso in **Where** (Posizione), quindi fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="f89fc-111">Type a name for the Certificate Signing Request (CSR) file in **Save As**, select the location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="f89fc-112">Il file CSR viene salvato nel percorso selezionato. Il percorso predefinito è Scrivania.</span><span class="sxs-lookup"><span data-stu-id="f89fc-112">This saves the CSR file in the selected location; the default location is in the Desktop.</span></span> <span data-ttu-id="f89fc-113">Tenere a mente il percorso scelto per il file.</span><span class="sxs-lookup"><span data-stu-id="f89fc-113">Remember the location chosen for this file.</span></span>

<span data-ttu-id="f89fc-114">A questo punto registrare l'app con Apple, abilitare le notifiche push e caricare il file CSR esportato per creare un certificato push.</span><span class="sxs-lookup"><span data-stu-id="f89fc-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR to create a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="f89fc-115">Registrare l'app per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="f89fc-115">Register your app for push notifications</span></span>
<span data-ttu-id="f89fc-116">Per poter inviare notifiche push a un'app per iOS, è necessario registrare l'applicazione con Apple ed eseguire un'altra registrazione per abilitare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="f89fc-116">To be able to send push notifications to an iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="f89fc-117">Se l'app non è ancora stata registrata, accedere al <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">portale di provisioning iOS</a> su Apple Developer Center, eseguire l'accesso con il proprio ID Apple, fare clic su **Identifiers**, quindi su **App IDs** e infine fare clic sul segno **+** per registrare una nuova app.</span><span class="sxs-lookup"><span data-stu-id="f89fc-117">If you have not already registered your app, navigate to the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at the Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on the **+** sign to register a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="f89fc-118">Aggiornare i tre campi seguenti per la nuova app e quindi fare clic su **Continue**:</span><span class="sxs-lookup"><span data-stu-id="f89fc-118">Update the following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="f89fc-119">**Name**: digitare un nome descrittivo per l'app nel campo **Name** della sezione **App ID Description**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-119">**Name**: Type a descriptive name for your app in the **Name** field in the **App ID Description** section.</span></span>
   * <span data-ttu-id="f89fc-120">**Bundle Identifier**: nella sezione **Explicit App ID** immettere un valore in **Bundle Identifier** nel formato `<Organization Identifier>.<Product Name>`, come indicato nel documento [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="f89fc-120">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>` as mentioned in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="f89fc-121">*Organization Identifier* e *Product Name* devono corrispondere all'identificatore dell'organizzazione e al nome del prodotto che verranno usati quando si crea il progetto XCode.</span><span class="sxs-lookup"><span data-stu-id="f89fc-121">The *Organization Identifier* and *Product Name* you use must match the organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="f89fc-122">Nella schermata seguente *NotificationHubs* viene usato come identificatore di organizzazione e *GetStarted* viene usato come nome del prodotto.</span><span class="sxs-lookup"><span data-stu-id="f89fc-122">In the screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as the product name.</span></span> <span data-ttu-id="f89fc-123">Verificare che corrispondano ai valori che si useranno nel progetto XCode, in modo da usare il profilo di pubblicazione corretto con XCode.</span><span class="sxs-lookup"><span data-stu-id="f89fc-123">Making sure this matches the values you will use in your XCode project will allow you to use the correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="f89fc-124">**Notifiche Push**: selezionare l'opzione **Notifiche Push** nella sezione **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-124">**Push Notifications**: Check the **Push Notifications** option in the **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="f89fc-125">Verrà generato l'ID app e all'utente verrà chiesto di confermare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="f89fc-125">This generates your App ID and requests you to confirm the information.</span></span> <span data-ttu-id="f89fc-126">Fare clic su **Registra** per confermare il nuovo ID app.</span><span class="sxs-lookup"><span data-stu-id="f89fc-126">Click **Register** to confirm the new App ID.</span></span>
     
      <span data-ttu-id="f89fc-127">Dopo aver fatto clic su **Register** (Registrazione) verrà visualizzata la schermata **Registrazione completa**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f89fc-127">Once you click **Register**, you will see the **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="f89fc-128">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="f89fc-129">In Developer Center, sotto App IDs trovare l'ID app appena creato e fare clic sulla relativa riga.</span><span class="sxs-lookup"><span data-stu-id="f89fc-129">In the Developer Center, under App IDs, locate the app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="f89fc-130">Facendo clic sull'ID app verranno visualizzati i dettagli relativi all'app.</span><span class="sxs-lookup"><span data-stu-id="f89fc-130">Clicking on the app ID will display the app details.</span></span> <span data-ttu-id="f89fc-131">Fare clic sul pulsante **Edit** nella parte inferiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="f89fc-131">Click the **Edit** button at the bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="f89fc-132">Scorrere fino alla fine della schermata e fare clic su **Crea Certificato...** nella sezione **Development Push SSL Certificate**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-132">Scroll to the bottom of the screen, and click the **Create Certificate...** button under the section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="f89fc-133">Verrà visualizzato l'assistente "Add iOS Certificate".</span><span class="sxs-lookup"><span data-stu-id="f89fc-133">This displays the "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f89fc-134">Questa esercitazione usa un certificato di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="f89fc-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="f89fc-135">La stessa procedura viene usata per registrare un certificato di produzione.</span><span class="sxs-lookup"><span data-stu-id="f89fc-135">The same process is used when registering a production certificate.</span></span> <span data-ttu-id="f89fc-136">Per l'invio delle notifiche, assicurarsi di usare lo stesso tipo di certificato.</span><span class="sxs-lookup"><span data-stu-id="f89fc-136">Just make sure that you use the same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="f89fc-137">Fare clic su **Choose File**, passare al percorso in cui è stato salvato il file CSR creato durante la prima attività, quindi fare clic su **Generate**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-137">Click **Choose File**, browse to the location where you saved the CSR file that you created in the first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="f89fc-138">Al termine della creazione del certificato nel portale, fare clic su **Download** e quindi su **Done**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-138">After the certificate is created by the portal, click the **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="f89fc-139">Il certificato di firma verrà scaricato e salvato nel computer nella cartella Download.</span><span class="sxs-lookup"><span data-stu-id="f89fc-139">This downloads the certificate and saves it to your computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="f89fc-140">Per impostazione predefinita, il file scaricato di un certificato di sviluppo è denominato **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-140">By default, the downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="f89fc-141">Fare doppio clic sul certificato push scaricato **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-141">Double-click the downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="f89fc-142">Il nuovo certificato verrà installato nel Portachiavi, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f89fc-142">This installs the new certificate in the Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="f89fc-143">Il nome del certificato potrebbe essere diverso, ma verrà preceduto da **Apple Development iOS Push Services:**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-143">The name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="f89fc-144">In Accesso portachiavi fare clic con il pulsante destro del mouse sul nuovo certificato push creato nella categoria **Certificati** .</span><span class="sxs-lookup"><span data-stu-id="f89fc-144">In Keychain Access, right-click the new push certificate that you created in the **Certificates** category.</span></span> <span data-ttu-id="f89fc-145">Fare clic su **Esporta**, assegnare un nome al file, selezionare il formato **.p12** e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-145">Click **Export**, name the file, select the **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="f89fc-146">Prendere nota del nome del file e del percorso del certificato con estensione p12 esportato.</span><span class="sxs-lookup"><span data-stu-id="f89fc-146">Make a note of the file name and location of the exported .p12 certificate.</span></span> <span data-ttu-id="f89fc-147">Verrà usato per abilitare l'autenticazione con il servizio APN.</span><span class="sxs-lookup"><span data-stu-id="f89fc-147">It will be used to enable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f89fc-148">In questa esercitazione viene creato un file QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="f89fc-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="f89fc-149">Il nome e il percorso del file potrebbero essere diversi.</span><span class="sxs-lookup"><span data-stu-id="f89fc-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-the-app"></a><span data-ttu-id="f89fc-150">Creare un profilo di provisioning per l'app</span><span class="sxs-lookup"><span data-stu-id="f89fc-150">Create a provisioning profile for the app</span></span>
1. <span data-ttu-id="f89fc-151">Nel <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">portale di provisioning iOS</a> selezionare **Provisioning Profiles**, quindi **All** e infine fare clic sul pulsante **+** per creare un nuovo profilo.</span><span class="sxs-lookup"><span data-stu-id="f89fc-151">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click the **+** button to create a new profile.</span></span> <span data-ttu-id="f89fc-152">Verrà avviata la procedura guidata **Add iOS Provisiong Profile**</span><span class="sxs-lookup"><span data-stu-id="f89fc-152">This launches the **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="f89fc-153">Selezionare **iOS App Development** in **Development** come tipo di profilo di provisioning e fare clic su **Continue**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-153">Select **iOS App Development** under **Development** as the provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="f89fc-154">Selezionare quindi l'ID app appena creato nell'elenco a discesa **App ID**e fare clic su **Continue**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-154">Next, select the app ID you just created from the **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="f89fc-155">Nella schermata **Select certificates** selezionare il solito certificato di sviluppo usato per la firma del codice e fare clic su **Continue**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-155">In the **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="f89fc-156">Questo non è il certificato push appena creato.</span><span class="sxs-lookup"><span data-stu-id="f89fc-156">This is not the push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="f89fc-157">In **Devices** selezionare i dispositivi da usare per il test e fare clic su **Continue**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-157">Next, select the **Devices** to use for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="f89fc-158">Scegliere infine un nome per il profilo in **Profile Name** e fare clic su **Generate**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-158">Finally, pick a name for the profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="f89fc-159">Una volta creato il nuovo profilo di provisioning, fare clic per scaricarlo e installarlo nel computer di sviluppo Xcode.</span><span class="sxs-lookup"><span data-stu-id="f89fc-159">When the new provisioning profile is created click to download it and install it on your Xcode development machine.</span></span> <span data-ttu-id="f89fc-160">Fare quindi clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="f89fc-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
