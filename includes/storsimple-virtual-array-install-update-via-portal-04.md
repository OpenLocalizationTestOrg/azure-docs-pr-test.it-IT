<!--author=alkohli last changed: 01/18/17 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="3faa0-101">Per installare gli aggiornamenti tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3faa0-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="3faa0-102">Passare a Gestione dispositivi StorSimple e selezionare **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="3faa0-103">Dall'elenco dei dispositivi connessi al servizio selezionare e fare clic sul dispositivo che si vuole aggiornare.</span><span class="sxs-lookup"><span data-stu-id="3faa0-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate1m.png) 

2. <span data-ttu-id="3faa0-105">Nel pannello **Impostazioni** fare clic su **Aggiornamenti del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate2m.png)  

3. <span data-ttu-id="3faa0-107">Se sono disponibili aggiornamenti software, verrà visualizzato un messaggio.</span><span class="sxs-lookup"><span data-stu-id="3faa0-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="3faa0-108">Per cercare gli aggiornamenti è anche possibile fare clic su **Analizza**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-108">To check for updates, you can also click **Scan**.</span></span>

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate3m1.png)

    <span data-ttu-id="3faa0-110">Si riceverà una notifica dell'avvio dell'analisi e del completamento.</span><span class="sxs-lookup"><span data-stu-id="3faa0-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate5m.png)

4. <span data-ttu-id="3faa0-112">Dopo aver eseguito l'analisi degli aggiornamenti fare clic su **Scarica aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate6m.png)

5. <span data-ttu-id="3faa0-114">Nel pannello **Nuovi aggiornamenti** esaminare le informazioni sugli aggiornamenti scaricati e confermare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="3faa0-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="3faa0-115">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-115">Click **OK**.</span></span>

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate7m.png)

6. <span data-ttu-id="3faa0-117">Si riceverà una notifica dell'avvio del caricamento e del completamento.</span><span class="sxs-lookup"><span data-stu-id="3faa0-117">You are notified when the upload starts and completes successfully.</span></span>

     ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate8m.png)

5. <span data-ttu-id="3faa0-119">Nel pannello **Aggiornamenti del dispositivo** fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-119">In the **Device updates** blade, click **Install**.</span></span>

     ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate11m1.png)   

6. <span data-ttu-id="3faa0-121">Nel pannello **Nuovi aggiornamenti** viene visualizzato un avviso che comunica che l'aggiornamento è problematico.</span><span class="sxs-lookup"><span data-stu-id="3faa0-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="3faa0-122">Poiché l'array virtuale è un dispositivo a nodo singolo, il dispositivo viene riavviato dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="3faa0-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="3faa0-123">Tutti gli IO in corso verranno interrotti.</span><span class="sxs-lookup"><span data-stu-id="3faa0-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="3faa0-124">Fare clic su **OK** per installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="3faa0-124">Click **OK** to install the updates.</span></span> 

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate12m.png) 

7. <span data-ttu-id="3faa0-126">Si riceverà una notifica dell'avvio del processo di installazione.</span><span class="sxs-lookup"><span data-stu-id="3faa0-126">You are notified when the install job starts.</span></span> 

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate13m.png)

8.  <span data-ttu-id="3faa0-128">Al termine del processo di installazione, fare clic sul collegamento **Visualizzare il processo** nel pannello **Aggiornamenti del dispositivo** per monitorare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="3faa0-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate15m1.png)

    <span data-ttu-id="3faa0-130">Viene visualizzato il pannello **Installa aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="3faa0-131">Nel pannello sono visualizzate informazioni dettagliate sul processo.</span><span class="sxs-lookup"><span data-stu-id="3faa0-131">You can view detailed information about the job here.</span></span>

    ![aggiornamento dispositivo](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate16m1.png)

9. <span data-ttu-id="3faa0-133">Al termine dell'installazione degli aggiornamenti viene visualizzato un messaggio nel pannello **Aggiornamenti del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3faa0-133">After the updates are successfully installed, you see a message to this effect in the **Device updates** blade.</span></span> 