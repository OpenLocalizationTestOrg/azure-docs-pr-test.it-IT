<!--author=alkohli last changed: 07/07/17-->

#### <a name="to-install-an-update-from-the-azure-portal"></a><span data-ttu-id="ec6b1-101">Per installare un aggiornamento dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ec6b1-101">To install an update from the Azure portal</span></span>

1. <span data-ttu-id="ec6b1-102">Nella pagina del servizio StorSimple, selezionare il proprio dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-102">On the StorSimple service page, select your device.</span></span>

    ![Selezionare il dispositivo](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="ec6b1-104">Andare a **Impostazioni del dispositivo** > **Aggiornamenti del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-104">Navigate to **Device settings** > **Device updates**.</span></span>

    ![Fare clic su Aggiornamenti del dispositivo](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="ec6b1-106">Se sono disponibili nuovi aggiornamenti, viene visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="ec6b1-107">In alternativa, nel pannello **Aggiornamenti del dispositivo** fare clic su **Verifica la disponibilità di aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-107">Alternatively, in the **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="ec6b1-108">Viene creato un processo per verificare la disponibilità di aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-108">A job is created to scan for available updates.</span></span> <span data-ttu-id="ec6b1-109">Al termine del processo si riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-109">You are notified when the job completes successfully.</span></span>

    ![Fare clic su Aggiornamenti del dispositivo](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="ec6b1-111">Si consiglia di leggere le note sulla versione prima di installare un aggiornamento nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-111">We recommend that you review the release notes before you apply an update on your device.</span></span> <span data-ttu-id="ec6b1-112">Per applicare gli aggiornamenti, fare clic su **Installa aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-112">To apply updates, click **Install updates**.</span></span> <span data-ttu-id="ec6b1-113">Nel pannello **Confermare gli aggiornamenti regolari** rivedere i prerequisiti da completare prima di applicare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-113">In the **Confirm regular updates** blade, review the prerequisites to complete before you apply updates.</span></span> <span data-ttu-id="ec6b1-114">Selezionare la casella di controllo per indicare che si è pronti per aggiornare il dispositivo e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-114">Select the checkbox to indicate that you are ready to update the device and then click **Install**.</span></span>

    ![Fare clic su Aggiornamenti del dispositivo](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="ec6b1-116">Viene avviato un set di controlli dei prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="ec6b1-117">I controlli includono quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ec6b1-117">These checks include:</span></span>
   
   * <span data-ttu-id="ec6b1-118">**Controlli di integrità del controller** per verificare che entrambi i controller dei dispositivi siano integri e online.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-118">**Controller health checks** to verify that both the device controllers are healthy and online.</span></span>
   * <span data-ttu-id="ec6b1-119">**Controlli di integrità del componente hardware** per verificare che tutti i componenti hardware del dispositivo StorSimple siano integri.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-119">**Hardware component health checks** to verify that all the hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="ec6b1-120">**Controlla DATA 0** per verificare che DATA 0 è attivato sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-120">**DATA 0 checks** to verify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="ec6b1-121">Se questa interfaccia non è abilitata, è necessario abilitarla e riprovare.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="ec6b1-122">L'aggiornamento viene scaricato e installato solo se tutti i controlli vengono completati correttamente.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-122">The update is downloaded and installed only if all the checks are successfully completed.</span></span> <span data-ttu-id="ec6b1-123">Quando i controlli sono in corso si riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-123">You are notified when the checks are in progress.</span></span> <span data-ttu-id="ec6b1-124">Se le verifiche preliminari hanno esito negativo, verranno indicate le cause dell'errore.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-124">If the prechecks fail, then you will be provided with the reasons for failure.</span></span> <span data-ttu-id="ec6b1-125">Risolvere tali problemi e quindi provare a eseguire di nuovo l'operazione.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-125">Address those issues and then retry the operation.</span></span> <span data-ttu-id="ec6b1-126">Se non è possibile risolvere tali problemi in autonomia, contattare il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-126">You may need to contact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="ec6b1-127">Dopo aver completato tutte le verifiche preliminari, viene creato un processo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-127">After the prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="ec6b1-128">Dopo la creazione di tale processo si riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-128">You are notified when the update job is successfully created.</span></span>
   
    ![Creazione del processo di aggiornamento](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="ec6b1-130">A questo punto, l'aggiornamento viene applicato al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-130">The update is then applied on your device.</span></span>

9. <span data-ttu-id="ec6b1-131">Per completare l'aggiornamento possono essere necessarie alcune ore.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-131">The update takes a few hours to complete.</span></span> <span data-ttu-id="ec6b1-132">Selezionare il processo di aggiornamento e fare clic su **Dettagli** per visualizzare i dettagli del processo in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-132">Select the update job and click **Details** to view the details of the job at any time.</span></span>

    ![Creazione del processo di aggiornamento](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="ec6b1-134">È anche possibile monitorare lo stato del processo di aggiornamento da **Impostazioni del dispositivo > Processi**.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-134">You can also monitor the progress of the update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="ec6b1-135">Nel pannello **Processi** è possibile visualizzare lo stato dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-135">On the **Jobs** blade, you can see the update progress.</span></span>

     ![Creazione del processo di aggiornamento](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="ec6b1-137">Al termine del processo, passare a **Impostazioni del dispositivo > Aggiornamenti del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-137">After the job is complete, navigate to the **Device settings > Device updates**.</span></span> <span data-ttu-id="ec6b1-138">La versione del software ora risulterà aggiornata.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-138">The software version should now be updated.</span></span>

    ![Creazione del processo di aggiornamento](./media/storsimple-8000-install-update4-via-portal/update9.png)

