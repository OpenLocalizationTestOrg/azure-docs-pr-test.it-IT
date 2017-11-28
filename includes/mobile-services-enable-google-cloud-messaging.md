
1. <span data-ttu-id="af5ed-101">Passare a [Google Cloud Console](https://console.developers.google.com/project)ed eseguire l'accesso con le credenziali dell'account Google.</span><span class="sxs-lookup"><span data-stu-id="af5ed-101">Navigate to the [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="af5ed-102">Fare clic su **Crea progetto**, digitare un nome di progetto e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="af5ed-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="af5ed-103">Se necessario, eseguire la verifica SMS, quindi fare nuovamente clic su **Crea** .</span><span class="sxs-lookup"><span data-stu-id="af5ed-103">If requested, carry out the SMS Verification, and click **Create** again.</span></span>
   
    ![Creare un nuovo progetto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="af5ed-105">Digitare il nuovo **nome del progetto** e fare clic su **Crea progetto**.</span><span class="sxs-lookup"><span data-stu-id="af5ed-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="af5ed-106">Fare clic sul pulsante **Utilities and More** (Utilità e altro) e quindi su **Informazioni progetto**.</span><span class="sxs-lookup"><span data-stu-id="af5ed-106">Click the **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="af5ed-107">Prendere nota del valore di **Project Number**.</span><span class="sxs-lookup"><span data-stu-id="af5ed-107">Make a note of the **Project Number**.</span></span> <span data-ttu-id="af5ed-108">Sarà necessario impostare questo valore come variabile `SenderId` nell'app client.</span><span class="sxs-lookup"><span data-stu-id="af5ed-108">You will need to set this value as the `SenderId` variable in the client app.</span></span>
   
    ![Utilità e altro ancora](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="af5ed-110">Nel dashboard del progetto fare clic su **Google Cloud Messaging** in **Mobile APIs** (API per dispositivi mobili), quindi nella pagina successiva fare clic su **Enable API** (Abilita API) e accettare le condizioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="af5ed-110">In the project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on the next page click **Enable API** and accept the terms of service.</span></span> 
   
    ![Abilitare GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Abilitare GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="af5ed-113">Nel dashboard del progetto fare clic su **Credenziali** > **Crea credenziale** > **Chiave API**.</span><span class="sxs-lookup"><span data-stu-id="af5ed-113">In the project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="af5ed-114">In **Crea una nuova chiave** fare clic su **Chiave server**, digitare un nome per la chiave e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="af5ed-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="af5ed-115">Prendere nota del valore di **API KEY** .</span><span class="sxs-lookup"><span data-stu-id="af5ed-115">Make a note of the **API KEY** value.</span></span>
   
    <span data-ttu-id="af5ed-116">Questo valore della chiave dell'API verrà usato successivamente per abilitare Azure per l'autenticazione con GCM e l'invio di notifiche push per conto dell'app.</span><span class="sxs-lookup"><span data-stu-id="af5ed-116">You will use this API key value to enable Azure to authenticate with GCM and send push notifications on behalf of your app.</span></span>

