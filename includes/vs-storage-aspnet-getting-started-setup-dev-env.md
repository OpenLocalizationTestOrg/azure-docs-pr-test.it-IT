## <a name="set-up-hello-development-environment"></a><span data-ttu-id="6fcbb-101">Configurare un ambiente di sviluppo hello</span><span class="sxs-lookup"><span data-stu-id="6fcbb-101">Set up hello development environment</span></span>

<span data-ttu-id="6fcbb-102">Questa sezione descrive l'impostazione dell'ambiente di sviluppo, inclusa la creazione di un'applicazione MVC ASP.NET, aggiunta di una connessione di servizi connessi, aggiunta di un controller, e specificando hello necessari direttive dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6fcbb-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying hello required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="6fcbb-103">Creare un progetto di app ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="6fcbb-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="6fcbb-104">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fcbb-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="6fcbb-105">Selezionare **File -> Nuovo -> progetto** dal menu principale hello</span><span class="sxs-lookup"><span data-stu-id="6fcbb-105">Select **File->New->Project** from hello main menu</span></span>

1. <span data-ttu-id="6fcbb-106">In hello **nuovo progetto** finestra di dialogo, specificare le opzioni di hello come hello evidenziato nella seguente illustrazione:</span><span class="sxs-lookup"><span data-stu-id="6fcbb-106">On hello **New Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Creazione di un progetto ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="6fcbb-108">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fcbb-108">Select **OK**.</span></span>

1. <span data-ttu-id="6fcbb-109">In hello **nuovo progetto ASP.NET** finestra di dialogo, specificare le opzioni di hello come hello evidenziato nella seguente illustrazione:</span><span class="sxs-lookup"><span data-stu-id="6fcbb-109">On hello **New ASP.NET Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Specificare MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="6fcbb-111">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fcbb-111">Select **OK**.</span></span>

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a><span data-ttu-id="6fcbb-112">Utilizzare l'account di archiviazione di Azure tooan tooconnect servizi connessi</span><span class="sxs-lookup"><span data-stu-id="6fcbb-112">Use Connected Services tooconnect tooan Azure storage account</span></span>

1. <span data-ttu-id="6fcbb-113">In hello **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **Aggiungi -> servizio connesso**.</span><span class="sxs-lookup"><span data-stu-id="6fcbb-113">In hello **Solution Explorer**, right-click hello project, and from hello context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="6fcbb-114">In hello **Aggiungi servizio connesso** finestra di dialogo Seleziona **di archiviazione di Azure**, quindi selezionare **configura**.</span><span class="sxs-lookup"><span data-stu-id="6fcbb-114">On hello **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Finestra di dialogo Servizi connessi](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="6fcbb-116">In hello **di archiviazione di Azure** finestra di dialogo Seleziona hello desiderato account di archiviazione Azure a cui desidera toowork e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6fcbb-116">On hello **Azure Storage** dialog, select hello desired Azure storage account with which you want toowork, and select **Add**.</span></span>
