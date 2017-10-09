<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="f5cbf-101">aggiornamenti rapidi toodownload</span><span class="sxs-lookup"><span data-stu-id="f5cbf-101">toodownload hotfixes</span></span>
<span data-ttu-id="f5cbf-102">Eseguire hello seguendo i passaggi toodownload hello software update.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-102">Perform hello following steps toodownload hello software update.</span></span>

1. <span data-ttu-id="f5cbf-103">Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f5cbf-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="f5cbf-104">Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="f5cbf-105">![Installare il catalogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="f5cbf-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="f5cbf-106">Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload, ad esempio **3063418**, quindi fare clic su **ricerca**.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="f5cbf-107">Verrà visualizzato hello **StorSimple Appliance 1.2 aggiornamento** bundle.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-107">You will see hello **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="f5cbf-108">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-108">Click **Add**.</span></span> <span data-ttu-id="f5cbf-109">aggiornamento di Hello verrà aggiunto toohello carrello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-109">hello update will be added toohello basket.</span></span>
5. <span data-ttu-id="f5cbf-110">Cercare gli aggiornamenti rapidi di aggiuntivi elencate nella tabella hello precedente (**3043005** e **3063416**) e aggiungere ogni carrello hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-110">Search for any additional hotfixes listed in hello table above (**3043005** and **3063416**), and add each hello basket.</span></span>
6. <span data-ttu-id="f5cbf-111">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-111">Click **View Basket**.</span></span>
   
    ![Visualizza carrello](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="f5cbf-113">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-113">Click **Download**.</span></span> <span data-ttu-id="f5cbf-114">Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="f5cbf-115">Hello gli aggiornamenti vengono scaricati toohello percorso specificato e inserito in una sottocartella con stesso nome come aggiornamento hello hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="f5cbf-116">cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="f5cbf-117">Hello hotfix deve essere accessibile da entrambi i controller toodetect qualsiasi errore potenziale dei messaggi dal controller peer hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="f5cbf-118">tooinstall e verificare gli aggiornamenti rapidi alla modalità normale</span><span class="sxs-lookup"><span data-stu-id="f5cbf-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="f5cbf-119">Eseguire i seguenti passaggi tooinstall hello e verificare gli aggiornamenti rapidi di hello in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-119">Perform hello following steps tooinstall and verify hello regular-mode hotfixes.</span></span> <span data-ttu-id="f5cbf-120">Se è già stato installato utilizzando hello del portale di Azure andare troppo[installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="f5cbf-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="f5cbf-121">tooinstall hello di aggiornamento software, interfaccia di Windows PowerShell di accesso hello nella console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-121">tooinstall hello software update, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="f5cbf-122">Seguire hello dettagliate in [console seriale di usare PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f5cbf-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="f5cbf-123">Al prompt dei comandi di hello, premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="f5cbf-124">Selezionare **opzione 1** toolog toohello dispositivo con accesso completo.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="f5cbf-125">pacchetto di aggiornamento il tooinstall hello, al prompt dei comandi di hello, tipo:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-125">tooinstall hello update package, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f5cbf-126">Utilizzare IP anziché DNS nel percorso di condivisione in hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="f5cbf-127">parametro credential Hello viene utilizzata solo se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="f5cbf-128">È consigliabile utilizzare condivisioni tooaccess parametro delle credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="f5cbf-129">Anche le condivisioni che sono aperte troppo "everyone" è in genere non aprire toounauthenticated utenti.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="f5cbf-130">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="f5cbf-131">Tipo **Y** quando richiesta tooconfirm hello installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="f5cbf-132">Monitorare l'aggiornamento di hello utilizzando hello `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="f5cbf-133">Hello output di esempio seguente viene illustrato hello aggiornamento in corso.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="f5cbf-134">Hello `RunInprogress` sarà `True` quando hello aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="f5cbf-135">Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="f5cbf-136">Hello `RunInProgress` sarà `False` quando hello aggiornamento completato.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="f5cbf-137">In alcuni casi, hello cmdlet report `False` quando aggiornamento hello è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="f5cbf-138">tooensure che hello hotfix è stata completata, attendere qualche minuto, eseguire nuovamente il comando e verificare che hello `RunInProgress` è `False`.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="f5cbf-139">Se si tratta, hotfix hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-139">If it is, then hello hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="f5cbf-140">Al termine dell'aggiornamento software hello, verificare le versioni di software di hello del sistema.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-140">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="f5cbf-141">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-141">Type hello following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="f5cbf-142">È necessario visualizzare hello seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="f5cbf-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="f5cbf-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="f5cbf-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="f5cbf-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="f5cbf-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="f5cbf-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="f5cbf-146">Se non viene modificata dopo l'applicazione hello aggiornamento numeri di versione di hello, significa che tale hotfix hello tooapply non riuscita.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-146">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="f5cbf-147">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="f5cbf-148">Ripetere i passaggi da 3 a 5 tooinstall hello rimanenti hotfix in modalità normale (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="f5cbf-148">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="f5cbf-149">tooinstall e verificare l'hotfix in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="f5cbf-149">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="f5cbf-150">Usare gli aggiornamenti del firmware di KB3063416 tooinstall disco.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-150">Use KB3063416 tooinstall disk firmware updates.</span></span> <span data-ttu-id="f5cbf-151">Questi aggiornamenti comportano interruzioni del servizio e richiedere intorno toocomplete 30 a 45 minuti.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-151">These are disruptive updates and take around 30-45 minutes toocomplete.</span></span> <span data-ttu-id="f5cbf-152">È possibile scegliere tooinstall in una finestra di manutenzione pianificata per la connessione console seriale del dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-152">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="f5cbf-153">aggiornamenti del firmware di tooinstall hello disco, seguire le istruzioni di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-153">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="f5cbf-154">Dispositivo di hello sul posto in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-154">Place hello device in Maintenance mode.</span></span> <span data-ttu-id="f5cbf-155">Si noti che è necessario non utilizzare Windows PowerShell in remoto quando ci si connette il dispositivo tooa in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-155">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="f5cbf-156">È necessario toorun questo cmdlet nel controller del dispositivo hello quando si è connessi tramite console seriale del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-156">You will need toorun this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="f5cbf-157">Digitare:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="f5cbf-158">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="f5cbf-159">Riavviare entrambi i controller hello in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-159">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="f5cbf-160">aggiornamento di firmware del disco con hello di tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-160">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f5cbf-161">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="f5cbf-162">Monitoraggio hello installa lo stato di avanzamento utilizzando `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-162">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="f5cbf-163">Hello aggiornamento è stata completata quando hello `RunInProgress` cambia troppo`False`.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-163">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="f5cbf-164">Al termine dell'installazione di hello, controller hello in cui è stato installato l'hotfix di modalità di manutenzione hello verrà riavviato.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-164">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="f5cbf-165">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-165">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="f5cbf-166">Digitare:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="f5cbf-167">Hello previsti sono le versioni del firmware del disco:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-167">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="f5cbf-168">Eseguire hello `Get-HcsFirmwareVersion` comando hello secondo controller tooverify che hello versione del software è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-168">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="f5cbf-169">È quindi possibile uscire dalla modalità di manutenzione hello.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-169">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="f5cbf-170">Digitare hello comando per ogni controller del dispositivo seguente:</span><span class="sxs-lookup"><span data-stu-id="f5cbf-170">Type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="f5cbf-171">controller Hello riavviare quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-171">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="f5cbf-172">Dopo il firmware del disco hello gli aggiornamenti sono stati correttamente applicati e dispositivo hello è uscito dalla modalità di manutenzione, restituito toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-172">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="f5cbf-173">Si noti che il portale di hello potrebbe non visualizzare installato gli aggiornamenti in modalità manutenzione hello per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="f5cbf-173">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

