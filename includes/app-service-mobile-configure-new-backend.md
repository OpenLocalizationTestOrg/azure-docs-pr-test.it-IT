
1. <span data-ttu-id="19e70-101">Fare clic su hello **servizi App** pulsante, selezionare l'App per dispositivi mobili di back-end, **delle Guide rapide**, quindi selezionare la piattaforma (iOS, Android, Xamarin, Cordova) dei client.</span><span class="sxs-lookup"><span data-stu-id="19e70-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Portale di Azure con Avvio rapido per le app per dispositivi mobili evidenziato][quickstart]

2. <span data-ttu-id="19e70-103">Se non è configurata una connessione al database, crearne una eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="19e70-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Portale di Azure con App Mobile Connect toodatabase][connect]

    <span data-ttu-id="19e70-105">a.</span><span class="sxs-lookup"><span data-stu-id="19e70-105">a.</span></span> <span data-ttu-id="19e70-106">Creare un nuovo server e un nuovo database SQL.</span><span class="sxs-lookup"><span data-stu-id="19e70-106">Create a new SQL database and server.</span></span>

    ![Portale di Azure con creazione di un nuovo database e un nuovo server per le app per dispositivi mobili][server]

    <span data-ttu-id="19e70-108">b.</span><span class="sxs-lookup"><span data-stu-id="19e70-108">b.</span></span> <span data-ttu-id="19e70-109">Attendere finché non viene creato correttamente connessione dati hello.</span><span class="sxs-lookup"><span data-stu-id="19e70-109">Wait until hello data connection is successfully created.</span></span>

    ![Notifica del completamento della creazione della connessione dati nel portale di Azure][notification]

    <span data-ttu-id="19e70-111">c.</span><span class="sxs-lookup"><span data-stu-id="19e70-111">c.</span></span> <span data-ttu-id="19e70-112">La connessione dati deve avere esito positivo.</span><span class="sxs-lookup"><span data-stu-id="19e70-112">Data connection must be successful.</span></span>

    ![Notifica "Esiste già una connessione dati" nel portale di Azure][already-connection]

3. <span data-ttu-id="19e70-114">In **2. Creare un'API di tabella** selezionare Node.js per **Linguaggio back-end**.</span><span class="sxs-lookup"><span data-stu-id="19e70-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="19e70-115">Accettare il riconoscimento di hello e quindi selezionare **tabella TodoItem creare**.</span><span class="sxs-lookup"><span data-stu-id="19e70-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="19e70-116">Con questa azione viene creata una nuova tabella di attività nel database.</span><span class="sxs-lookup"><span data-stu-id="19e70-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="19e70-117">Cambio di un tooNode.js back-end esistente verrà sovrascritto tutto il contenuto.</span><span class="sxs-lookup"><span data-stu-id="19e70-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="19e70-118">un back-end .NET, vedere toocreate [funziona con server hello back-end .NET SDK per App per dispositivi mobili][instructions].</span><span class="sxs-lookup"><span data-stu-id="19e70-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
