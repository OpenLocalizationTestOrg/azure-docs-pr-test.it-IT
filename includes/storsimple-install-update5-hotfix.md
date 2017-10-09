<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="272f7-101">aggiornamenti rapidi toodownload</span><span class="sxs-lookup"><span data-stu-id="272f7-101">toodownload hotfixes</span></span>

<span data-ttu-id="272f7-102">Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="272f7-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="272f7-103">Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="272f7-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="272f7-104">Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="272f7-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Installare il catalogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="272f7-106">Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload, ad esempio **4037264**, quindi fare clic su **ricerca**.</span><span class="sxs-lookup"><span data-stu-id="272f7-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="272f7-107">Hello hotfix elenco viene visualizzato, ad esempio, **cumulativo Software Bundle di aggiornamento 5.0 per StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="272f7-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="272f7-109">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="272f7-109">Click **Download**.</span></span> <span data-ttu-id="272f7-110">Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear.</span><span class="sxs-lookup"><span data-stu-id="272f7-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="272f7-111">Fare clic su file hello toodownload toohello specificato posizione e la cartella.</span><span class="sxs-lookup"><span data-stu-id="272f7-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="272f7-112">cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="272f7-113">Cercare gli aggiornamenti rapidi di aggiuntivi elencate nella tabella hello precedente (**4037266**), e i file nelle cartelle specifiche toohello download hello corrispondente come indicato nella tabella precedente hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="272f7-114">Hello hotfix deve essere accessibile da entrambi i controller toodetect qualsiasi errore potenziale dei messaggi dal controller peer hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="272f7-115">gli aggiornamenti rapidi Hello devono essere copiati in cartelle separate 3.</span><span class="sxs-lookup"><span data-stu-id="272f7-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="272f7-116">Ad esempio, l'aggiornamento dell'agente di elementi di configurazione/software/MDS hello dispositivo può essere copiato _FirstOrderUpdate_ cartella, tutti hello altri aggiornamenti non comportano interruzioni del servizio è stato possibile copiare in hello _SecondOrderUpdate_ cartella, e gli aggiornamenti in modalità manutenzione copiati _ThirdOrderUpdate_ cartella.</span><span class="sxs-lookup"><span data-stu-id="272f7-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="272f7-117">tooinstall e verificare gli aggiornamenti rapidi alla modalità normale</span><span class="sxs-lookup"><span data-stu-id="272f7-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="272f7-118">Eseguire i seguenti passaggi tooinstall hello e verificare gli aggiornamenti rapidi in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="272f7-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="272f7-119">Se è già stato installato utilizzando hello portale di Azure andare troppo[installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="272f7-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="272f7-120">tooinstall hello hotfixes interfaccia di Windows PowerShell di accesso hello nella console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="272f7-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="272f7-121">Seguire hello dettagliate in [console seriale di usare PuTTy tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="272f7-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="272f7-122">Al prompt dei comandi di hello, premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="272f7-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="272f7-123">Selezionare **opzione 1** toolog toohello dispositivo con accesso completo.</span><span class="sxs-lookup"><span data-stu-id="272f7-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="272f7-124">È consigliabile installare hotfix hello sul controller passivo hello prima.</span><span class="sxs-lookup"><span data-stu-id="272f7-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="272f7-125">hotfix hello tooinstall, al prompt dei comandi di hello, tipo:</span><span class="sxs-lookup"><span data-stu-id="272f7-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="272f7-126">Utilizzare IP anziché DNS nel percorso di condivisione in hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="272f7-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="272f7-127">parametro credential Hello viene utilizzata solo se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="272f7-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="272f7-128">È consigliabile utilizzare condivisioni tooaccess parametro delle credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="272f7-129">Anche le condivisioni che sono aperte troppo "everyone" è in genere non aprire toounauthenticated utenti.</span><span class="sxs-lookup"><span data-stu-id="272f7-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="272f7-130">Specificare la password hello quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="272f7-130">Supply hello password when prompted.</span></span> <span data-ttu-id="272f7-131">Un esempio di output per l'installazione di aggiornamenti degli ordini prima hello è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="272f7-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="272f7-132">Per l'aggiornamento dell'ordine prima di hello, è necessario toopoint toohello specifici file.</span><span class="sxs-lookup"><span data-stu-id="272f7-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="272f7-133">È necessario installare hello _HcsSoftwareUpdate.exe_ prima.</span><span class="sxs-lookup"><span data-stu-id="272f7-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="272f7-134">Al termine, installare quindi _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="272f7-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="272f7-135">Tipo **Y** quando richiesta tooconfirm hello installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="272f7-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="272f7-136">Monitorare l'aggiornamento di hello utilizzando hello `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="272f7-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="272f7-137">aggiornamento di Hello completerà innanzitutto nel controller passivo hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="272f7-138">Una volta che viene aggiornato il controller passivo hello, sarà presente un failover e aggiornamento hello verrà quindi applicata in hello altro controller.</span><span class="sxs-lookup"><span data-stu-id="272f7-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="272f7-139">aggiornamento di Hello è completa quando entrambi i controller hello vengono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="272f7-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="272f7-140">Hello output di esempio seguente viene illustrato hello aggiornamento in corso.</span><span class="sxs-lookup"><span data-stu-id="272f7-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="272f7-141">Hello `RunInprogress` è `True` quando hello aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="272f7-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="272f7-142">Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato.</span><span class="sxs-lookup"><span data-stu-id="272f7-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="272f7-143">Hello `RunInProgress` è `False` quando aggiornamento hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="272f7-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="272f7-144">In alcuni casi, hello cmdlet report `False` quando aggiornamento hello è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="272f7-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="272f7-145">tooensure che hello hotfix è stata completata, attendere qualche minuto, eseguire nuovamente il comando e verificare che hello `RunInProgress` è `False`.</span><span class="sxs-lookup"><span data-stu-id="272f7-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="272f7-146">Se si tratta, hotfix hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="272f7-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="272f7-147">Al termine dell'aggiornamento software hello, verificare le versioni di software di hello del sistema.</span><span class="sxs-lookup"><span data-stu-id="272f7-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="272f7-148">Digitare:</span><span class="sxs-lookup"><span data-stu-id="272f7-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="272f7-149">È necessario visualizzare hello seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="272f7-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="272f7-150">Se il numero di versione di hello rimane invariato dopo l'applicazione hello aggiornamento, significa che tale hotfix hello tooapply non riuscita.</span><span class="sxs-lookup"><span data-stu-id="272f7-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="272f7-151">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="272f7-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="272f7-152">È necessario riavviare il controller attivo di hello mediante hello `Restart-HcsController` cmdlet prima di applicare hello successivo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="272f7-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="272f7-153">Ripetere i passaggi da 3 a 6 tooinstall hello _CisMDSAgentupdate.exe_ agente scaricato tooyour _FirstOrderUpdate_ cartella.</span><span class="sxs-lookup"><span data-stu-id="272f7-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="272f7-154">Ripetere i passaggi da 3 a 6 tooinstall hello secondo aggiornamenti degli ordini.</span><span class="sxs-lookup"><span data-stu-id="272f7-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="272f7-155">Per secondo aggiornamenti degli ordini, è possono installare più aggiornamenti eseguendo semplicemente hello `Start-HcsHotfix cmdlet` e scegliendo toohello cartella in cui si trovano secondo aggiornamenti degli ordini.</span><span class="sxs-lookup"><span data-stu-id="272f7-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="272f7-156">cmdlet di Hello eseguirà tutti gli aggiornamenti di hello disponibili nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="272f7-157">Se è già installato un aggiornamento, la logica di aggiornamento hello rileverà che e non applicare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="272f7-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="272f7-158">Una volta installati tutti gli hotfix hello, utilizzare hello `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="272f7-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="272f7-159">versioni di Hello devono essere:</span><span class="sxs-lookup"><span data-stu-id="272f7-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="272f7-160">tooinstall e verificare l'hotfix in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="272f7-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="272f7-161">Usare gli aggiornamenti del firmware di KB4037263 tooinstall disco.</span><span class="sxs-lookup"><span data-stu-id="272f7-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="272f7-162">Questi aggiornamenti comportano interruzioni e e richiedere toocomplete circa 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="272f7-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="272f7-163">È possibile scegliere tooinstall in una finestra di manutenzione pianificata per la connessione console seriale del dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="272f7-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="272f7-164">Se il firmware del disco è già stato aggiornato, non sarà necessario tooinstall questi aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="272f7-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="272f7-165">Eseguire hello `Get-HcsUpdateAvailability` da hello dispositivo console seriale toocheck se sono disponibili aggiornamenti che indica se hello Aggiorna sono comportano interruzioni del servizio (modalità di manutenzione) o non comportano interruzioni del servizio (modalità normale) gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="272f7-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="272f7-166">aggiornamenti del firmware di tooinstall hello disco, seguire le istruzioni di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="272f7-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="272f7-167">Dispositivo di hello sul posto in modalità manutenzione hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="272f7-168">Usa la comunicazione remota di Windows PowerShell quando ci si connette il dispositivo tooa in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="272f7-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="272f7-169">In alternativa, eseguire questo cmdlet nel controller del dispositivo hello quando si è connessi tramite console seriale del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="272f7-170">controller hello tooplace in modalità manutenzione, digitare:</span><span class="sxs-lookup"><span data-stu-id="272f7-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="272f7-171">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="272f7-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="272f7-172">Riavviare entrambi i controller hello in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="272f7-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="272f7-173">aggiornamento di firmware del disco con hello di tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="272f7-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="272f7-174">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="272f7-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="272f7-175">Monitoraggio hello installa lo stato di avanzamento utilizzando `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="272f7-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="272f7-176">Hello aggiornamento è stata completata quando hello `RunInProgress` cambia troppo`False`.</span><span class="sxs-lookup"><span data-stu-id="272f7-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="272f7-177">Al termine dell'installazione di hello, hello del controller in cui hello è stato installato l'hotfix di modalità di manutenzione viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="272f7-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="272f7-178">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="272f7-179">Digitare:</span><span class="sxs-lookup"><span data-stu-id="272f7-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="272f7-180">Hello previsti sono le versioni del firmware del disco:</span><span class="sxs-lookup"><span data-stu-id="272f7-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="272f7-181">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="272f7-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="272f7-182">Eseguire hello `Get-HcsFirmwareVersion` comando hello secondo controller tooverify che hello versione del software è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="272f7-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="272f7-183">È quindi possibile uscire dalla modalità di manutenzione hello.</span><span class="sxs-lookup"><span data-stu-id="272f7-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="272f7-184">toodo in tal caso, digitare hello comando per ogni controller del dispositivo seguente:</span><span class="sxs-lookup"><span data-stu-id="272f7-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="272f7-185">controller Hello riavviare quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="272f7-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="272f7-186">Dopo il firmware del disco hello gli aggiornamenti sono stati correttamente applicati e dispositivo hello è uscito dalla modalità di manutenzione, restituito toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="272f7-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="272f7-187">Si noti che il portale di hello potrebbe non visualizzare installato gli aggiornamenti in modalità manutenzione hello per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="272f7-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

