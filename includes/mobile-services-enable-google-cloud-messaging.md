
1. <span data-ttu-id="43cd7-101">Passare toohello [Google Cloud Console](https://console.developers.google.com/project), accedere con le credenziali dell'account Google.</span><span class="sxs-lookup"><span data-stu-id="43cd7-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="43cd7-102">Fare clic su **Crea progetto**, digitare un nome di progetto e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="43cd7-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="43cd7-103">Se richiesto, eseguire la verifica tramite SMS hello e fare clic su **crea** nuovamente.</span><span class="sxs-lookup"><span data-stu-id="43cd7-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Creare un nuovo progetto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="43cd7-105">Digitare il nuovo **nome del progetto** e fare clic su **Crea progetto**.</span><span class="sxs-lookup"><span data-stu-id="43cd7-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="43cd7-106">Fare clic su hello **utilità e altro ancora** pulsante e quindi fare clic su **informazioni sul progetto**.</span><span class="sxs-lookup"><span data-stu-id="43cd7-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="43cd7-107">Prendere nota di hello **numero progetto**.</span><span class="sxs-lookup"><span data-stu-id="43cd7-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="43cd7-108">Sarà necessario tooset questo valore come hello `SenderId` variabili nell'app client hello.</span><span class="sxs-lookup"><span data-stu-id="43cd7-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Utilità e altro ancora](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="43cd7-110">In hello progetto dashboard, in **API Mobile**, fare clic su **Google Cloud Messaging**, quindi fare clic nella pagina successiva hello **Abilita API** e accettare le condizioni di hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="43cd7-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![Abilitare GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Abilitare GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="43cd7-113">Nel dashboard del progetto hello, fare clic su **credenziali** > **Create Credential** > **chiave API**.</span><span class="sxs-lookup"><span data-stu-id="43cd7-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="43cd7-114">In **Crea una nuova chiave** fare clic su **Chiave server**, digitare un nome per la chiave e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="43cd7-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="43cd7-115">Prendere nota di hello **chiave API** valore.</span><span class="sxs-lookup"><span data-stu-id="43cd7-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="43cd7-116">Si utilizza questo tooenable valore della chiave API tooauthenticate Azure con GCM e inviare notifiche push per conto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43cd7-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

