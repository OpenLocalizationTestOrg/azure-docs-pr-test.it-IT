
1. <span data-ttu-id="82683-101">Nel [Portale di Azure](https://portal.azure.com/) fare clic su **Browse All** (Esplora tutto)  > **Servizi app** e quindi scegliere il back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="82683-101">In the [Azure portal](https://portal.azure.com/), click **Browse All** > **App Services**, and then click your Mobile Apps back end.</span></span> <span data-ttu-id="82683-102">In **Impostazioni** fare clic su **App Service Push** (Push servizio app), quindi fare clic sul nome dell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="82683-102">Under **Settings**, click **App Service Push**, and then click your notification hub name.</span></span>
2. <span data-ttu-id="82683-103">Passare a **Google (GCM)**, immettere il valore **Chiave server** ottenuto da Firebase nella procedura precedente, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="82683-103">Go to **Google (GCM)**, enter the **Server Key** value that you obtained from Firebase in the previous procedure, and then click **Save**.</span></span>

    ![Impostare la chiave API di GCM nel portale](./media/app-service-mobile-android-configure-push/mobile-push-api-key.png)

<span data-ttu-id="82683-105">Il back-end dell'app per dispositivi mobili è ora configurato per l'uso di Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="82683-105">The Mobile Apps back end is now configured to use Firebase Cloud Messaging.</span></span> <span data-ttu-id="82683-106">Questo consente di inviare notifiche push all'app in esecuzione su un dispositivo Android usando l'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="82683-106">This enables you to send push notifications to your app running on an Android device, by using the notification hub.</span></span>

<!-- URLs. -->


<!-- images -->
