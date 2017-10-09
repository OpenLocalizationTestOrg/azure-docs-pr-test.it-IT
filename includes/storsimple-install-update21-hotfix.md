<!--author=alkohli last changed: 05/19/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="aac28-101">aggiornamenti rapidi toodownload</span><span class="sxs-lookup"><span data-stu-id="aac28-101">toodownload hotfixes</span></span>
<span data-ttu-id="aac28-102">Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="aac28-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="aac28-103">Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="aac28-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="aac28-104">Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="aac28-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="aac28-105">![Installare il catalogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="aac28-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="aac28-106">Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload, ad esempio **3179904**, quindi fare clic su **ricerca**.</span><span class="sxs-lookup"><span data-stu-id="aac28-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="aac28-107">Hello hotfix elenco viene visualizzato, ad esempio, **cumulativo Software Bundle di aggiornamento 2.2 per StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="aac28-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="aac28-109">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="aac28-109">Click **Add**.</span></span> <span data-ttu-id="aac28-110">aggiornamento di Hello viene aggiunto toohello carrello.</span><span class="sxs-lookup"><span data-stu-id="aac28-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="aac28-111">Cercare gli aggiornamenti rapidi di aggiuntivi elencate nella tabella hello precedente (**3103616**, **3146621**) e aggiungere ogni carrello toohello.</span><span class="sxs-lookup"><span data-stu-id="aac28-111">Search for any additional hotfixes listed in hello table above (**3103616**, **3146621**), and add each toohello basket.</span></span>
6. <span data-ttu-id="aac28-112">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="aac28-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="aac28-113">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="aac28-113">Click **Download**.</span></span> <span data-ttu-id="aac28-114">Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear.</span><span class="sxs-lookup"><span data-stu-id="aac28-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="aac28-115">Hello gli aggiornamenti vengono scaricati toohello percorso specificato e inserita in una sottocartella con stesso nome come aggiornamento hello hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-115">hello updates are downloaded toohello specified location and placed in a sub-folder with hello same name as hello update.</span></span> <span data-ttu-id="aac28-116">cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="aac28-117">Hello hotfix deve essere accessibile da entrambi i controller toodetect qualsiasi errore potenziale dei messaggi dal controller peer hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="aac28-118">tooinstall e verificare gli aggiornamenti rapidi alla modalità normale</span><span class="sxs-lookup"><span data-stu-id="aac28-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="aac28-119">Eseguire i seguenti passaggi tooinstall hello e verificare gli aggiornamenti rapidi in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="aac28-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="aac28-120">Se è già stato installato utilizzando hello del portale di Azure andare troppo[installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="aac28-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="aac28-121">tooinstall hello hotfixes interfaccia di Windows PowerShell di accesso hello nella console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="aac28-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="aac28-122">Seguire hello dettagliate in [console seriale di usare PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="aac28-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="aac28-123">Al prompt dei comandi di hello, premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="aac28-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="aac28-124">Selezionare **opzione 1** toolog toohello dispositivo con accesso completo.</span><span class="sxs-lookup"><span data-stu-id="aac28-124">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="aac28-125">È consigliabile installare hotfix hello sul controller passivo hello prima.</span><span class="sxs-lookup"><span data-stu-id="aac28-125">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="aac28-126">hotfix hello tooinstall, al prompt dei comandi di hello, tipo:</span><span class="sxs-lookup"><span data-stu-id="aac28-126">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="aac28-127">Utilizzare IP anziché DNS nel percorso di condivisione in hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="aac28-127">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="aac28-128">parametro credential Hello viene utilizzata solo se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="aac28-128">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="aac28-129">È consigliabile utilizzare condivisioni tooaccess parametro delle credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-129">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="aac28-130">Anche le condivisioni che sono aperte troppo "everyone" è in genere non aprire toounauthenticated utenti.</span><span class="sxs-lookup"><span data-stu-id="aac28-130">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="aac28-131">Specificare la password hello quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="aac28-131">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="aac28-132">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="aac28-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="aac28-133">Tipo **Y** quando richiesta tooconfirm hello installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="aac28-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="aac28-134">Se l'installazione di aggiornamento 2.2, installare solo file binari di hello preceduti da 'all-hcsmdssoftwareudpate'.</span><span class="sxs-lookup"><span data-stu-id="aac28-134">If installing Update 2.2, only install hello binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="aac28-135">Non installare hello hello e ci MDS agente Aggiorna preceduto da all cismdsagentupdatebundle.</span><span class="sxs-lookup"><span data-stu-id="aac28-135">Do not install hello Cis and hello MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="aac28-136">Errore toodo operazione genererà un errore.</span><span class="sxs-lookup"><span data-stu-id="aac28-136">Failure toodo so will result in an error.</span></span> 

5. <span data-ttu-id="aac28-137">Monitorare l'aggiornamento di hello utilizzando hello `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aac28-137">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="aac28-138">aggiornamento di Hello completerà innanzitutto nel controller passivo hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-138">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="aac28-139">Una volta che viene aggiornato il controller passivo hello, sarà presente un failover e aggiornamento hello verrà quindi applicata in hello altro controller.</span><span class="sxs-lookup"><span data-stu-id="aac28-139">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="aac28-140">aggiornamento di Hello è completa quando entrambi i controller hello vengono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="aac28-140">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="aac28-141">Hello output di esempio seguente viene illustrato hello aggiornamento in corso.</span><span class="sxs-lookup"><span data-stu-id="aac28-141">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="aac28-142">Hello `RunInprogress` sarà `True` quando hello aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="aac28-142">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="aac28-143">Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato.</span><span class="sxs-lookup"><span data-stu-id="aac28-143">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="aac28-144">Hello `RunInProgress` sarà `False` quando hello aggiornamento completato.</span><span class="sxs-lookup"><span data-stu-id="aac28-144">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="aac28-145">In alcuni casi, hello cmdlet report `False` quando aggiornamento hello è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="aac28-145">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="aac28-146">tooensure che hello hotfix è stata completata, attendere qualche minuto, eseguire nuovamente il comando e verificare che hello `RunInProgress` è `False`.</span><span class="sxs-lookup"><span data-stu-id="aac28-146">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="aac28-147">Se si tratta, hotfix hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="aac28-147">If it is, then hello hotfix has completed.</span></span>

1. <span data-ttu-id="aac28-148">Al termine dell'aggiornamento software hello, verificare le versioni di software di hello del sistema.</span><span class="sxs-lookup"><span data-stu-id="aac28-148">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="aac28-149">Digitare:</span><span class="sxs-lookup"><span data-stu-id="aac28-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="aac28-150">È necessario visualizzare hello seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="aac28-150">You should see hello following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="aac28-151">Se non viene modificata dopo l'applicazione hello aggiornamento numeri di versione di hello, significa che tale hotfix hello tooapply non riuscita.</span><span class="sxs-lookup"><span data-stu-id="aac28-151">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="aac28-152">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="aac28-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="aac28-153">È necessario riavviare il controller attivo di hello mediante hello `Restart-HcsController` cmdlet prima di applicare gli aggiornamenti rimanenti hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-153">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="aac28-154">Ripetere i passaggi da 3 a 5 tooinstall hello rimanenti hotfix in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="aac28-154">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="aac28-155">aggiornamento di iSCSI Hello KB3146621</span><span class="sxs-lookup"><span data-stu-id="aac28-155">hello iSCSI update KB3146621</span></span>
   * <span data-ttu-id="aac28-156">aggiornamento WMI Hello KB3103616</span><span class="sxs-lookup"><span data-stu-id="aac28-156">hello WMI update KB3103616</span></span>
3. <span data-ttu-id="aac28-157">Ignorare questo passaggio se si aggiorna da Update 2.</span><span class="sxs-lookup"><span data-stu-id="aac28-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="aac28-158">Se si sta aggiornando un tooUpdate precedente versione 2, è necessario anche toodownload:</span><span class="sxs-lookup"><span data-stu-id="aac28-158">If you are updating from a version prior tooUpdate 2, you will also need toodownload:</span></span>

    - <span data-ttu-id="aac28-159">driver Hello LSI KB3121900</span><span class="sxs-lookup"><span data-stu-id="aac28-159">hello LSI driver KB3121900</span></span>

    - <span data-ttu-id="aac28-160">aggiornamento di Spaceport Hello KB3090322</span><span class="sxs-lookup"><span data-stu-id="aac28-160">hello Spaceport update KB3090322</span></span>

    - <span data-ttu-id="aac28-161">aggiornamento di Storport Hello KB3080728</span><span class="sxs-lookup"><span data-stu-id="aac28-161">hello Storport update KB3080728</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="aac28-162">tooinstall e verificare l'hotfix in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="aac28-162">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="aac28-163">Usare gli aggiornamenti del firmware di KB3121899 tooinstall disco.</span><span class="sxs-lookup"><span data-stu-id="aac28-163">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="aac28-164">Questi aggiornamenti comportano interruzioni e e richiedere toocomplete circa 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="aac28-164">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="aac28-165">È possibile scegliere tooinstall in una finestra di manutenzione pianificata per la connessione console seriale del dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="aac28-165">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="aac28-166">Si noti che se il firmware del disco è già stato aggiornato, non sarà necessario tooinstall questi aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="aac28-166">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="aac28-167">Eseguire hello `Get-HcsUpdateAvailability` da hello dispositivo console seriale toocheck se sono disponibili aggiornamenti che indica se hello Aggiorna sono comportano interruzioni del servizio (modalità di manutenzione) o non comportano interruzioni del servizio (modalità normale) gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="aac28-167">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="aac28-168">aggiornamenti del firmware di tooinstall hello disco, seguire le istruzioni di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="aac28-168">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="aac28-169">Dispositivo di hello sul posto in modalità manutenzione hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-169">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="aac28-170">Si noti che è necessario non utilizzare Windows PowerShell in remoto quando ci si connette il dispositivo tooa in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="aac28-170">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="aac28-171">In alternativa, eseguire questo cmdlet nel controller del dispositivo hello quando si è connessi tramite console seriale del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-171">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="aac28-172">Digitare:</span><span class="sxs-lookup"><span data-stu-id="aac28-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="aac28-173">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="aac28-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="aac28-174">Riavviare entrambi i controller hello in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="aac28-174">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="aac28-175">aggiornamento di firmware del disco con hello di tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="aac28-175">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="aac28-176">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="aac28-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="aac28-177">Monitoraggio hello installa lo stato di avanzamento utilizzando `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="aac28-177">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="aac28-178">Hello aggiornamento è stata completata quando hello `RunInProgress` cambia troppo`False`.</span><span class="sxs-lookup"><span data-stu-id="aac28-178">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="aac28-179">Al termine dell'installazione di hello, hello del controller in cui hello è stato installato l'hotfix di modalità di manutenzione viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="aac28-179">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="aac28-180">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-180">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="aac28-181">Digitare:</span><span class="sxs-lookup"><span data-stu-id="aac28-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="aac28-182">Hello previsti sono le versioni del firmware del disco:</span><span class="sxs-lookup"><span data-stu-id="aac28-182">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="aac28-183">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="aac28-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="aac28-184">Eseguire hello `Get-HcsFirmwareVersion` comando hello secondo controller tooverify che hello versione del software è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="aac28-184">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="aac28-185">È quindi possibile uscire dalla modalità di manutenzione hello.</span><span class="sxs-lookup"><span data-stu-id="aac28-185">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="aac28-186">toodo in tal caso, digitare hello comando per ogni controller del dispositivo seguente:</span><span class="sxs-lookup"><span data-stu-id="aac28-186">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="aac28-187">controller Hello riavviare quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="aac28-187">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="aac28-188">Dopo il firmware del disco hello gli aggiornamenti sono stati correttamente applicati e dispositivo hello è uscito dalla modalità di manutenzione, restituito toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="aac28-188">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="aac28-189">Si noti che il portale di hello potrebbe non visualizzare installato gli aggiornamenti in modalità manutenzione hello per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="aac28-189">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

