
1. <span data-ttu-id="b190e-101">Fare clic su di **servizi App** pulsante, selezionare l'App per dispositivi mobili di back-end, **Guida introduttiva**, quindi selezionare la piattaforma (iOS, Android, Xamarin, Cordova) dei client.</span><span class="sxs-lookup"><span data-stu-id="b190e-101">Click the **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Portale di Azure con avvio rapido di applicazioni mobili evidenziato][quickstart]

2. <span data-ttu-id="b190e-103">Se non è configurata una connessione al database, crearne uno attenendosi alla seguente:</span><span class="sxs-lookup"><span data-stu-id="b190e-103">If a database connection is not configured, create one by doing the following:</span></span>

    ![Portale di Azure con App Mobile Connect al database][connect]

    <span data-ttu-id="b190e-105">a.</span><span class="sxs-lookup"><span data-stu-id="b190e-105">a.</span></span> <span data-ttu-id="b190e-106">Creare un nuovo database SQL e server.</span><span class="sxs-lookup"><span data-stu-id="b190e-106">Create a new SQL database and server.</span></span>

    ![Portale di Azure con applicazioni per dispositivi mobili creare server e un nuovo database][server]

    <span data-ttu-id="b190e-108">b.</span><span class="sxs-lookup"><span data-stu-id="b190e-108">b.</span></span> <span data-ttu-id="b190e-109">Attendere la creazione della connessione dati.</span><span class="sxs-lookup"><span data-stu-id="b190e-109">Wait until the data connection is successfully created.</span></span>

    ![Notifica del portale di Azure di creazione della connessione dati][notification]

    <span data-ttu-id="b190e-111">c.</span><span class="sxs-lookup"><span data-stu-id="b190e-111">c.</span></span> <span data-ttu-id="b190e-112">La connessione dati deve avere esito positivo.</span><span class="sxs-lookup"><span data-stu-id="b190e-112">Data connection must be successful.</span></span>

    ![Notifica del portale di Azure, "già disponibile una connessione dati"][already-connection]

3. <span data-ttu-id="b190e-114">In **2. Creare un'API di tabella** selezionare Node.js per **Linguaggio back-end**.</span><span class="sxs-lookup"><span data-stu-id="b190e-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="b190e-115">Accettare il riconoscimento e quindi selezionare **tabella TodoItem creare**.</span><span class="sxs-lookup"><span data-stu-id="b190e-115">Accept the acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="b190e-116">Questa azione crea una nuova tabella elemento attività da eseguire nel database.</span><span class="sxs-lookup"><span data-stu-id="b190e-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="b190e-117">Il passaggio di un back-end esistente a Node.js sovrascrive tutti i contenuti.</span><span class="sxs-lookup"><span data-stu-id="b190e-117">Switching an existing back end to Node.js overwrites all contents.</span></span> <span data-ttu-id="b190e-118">Per creare invece un back-end .NET, vedere [di lavoro con il server back-end .NET SDK per App per dispositivi mobili][instructions].</span><span class="sxs-lookup"><span data-stu-id="b190e-118">To create a .NET back end instead, see [Work with the .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
