<!--author=alkohli last changed: 09/01/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="5acc9-101">Scaricare gli hotfix</span><span class="sxs-lookup"><span data-stu-id="5acc9-101">To download hotfixes</span></span>
<span data-ttu-id="5acc9-102">Eseguire i passaggi seguenti per scaricare l'aggiornamento del software da Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="5acc9-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="5acc9-103">Avviare Internet Explorer e accedere al sito [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5acc9-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="5acc9-104">Se si usa Microsoft Update Catalog nel computer per la prima volta, fare clic su **Installa** quando viene richiesto di installare il componente aggiuntivo Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="5acc9-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="5acc9-105">![Installare il catalogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="5acc9-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="5acc9-106">Nella casella di ricerca di Microsoft Update Catalog, immettere il numero della Knowledge Base (KB) dell'hotfix da scaricare, ad esempio **3186843**, quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="5acc9-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3186843**, and then click **Search**.</span></span>
   
    <span data-ttu-id="5acc9-107">Verrà visualizzato l'elenco degli hotfix, ad esempio, **Cumulative Software Bundle Update 3.0 for StorSimple 8000 Series**(Aggiornamento cumulativo del pacchetto software 3.0 per StorSimple serie 8000).</span><span class="sxs-lookup"><span data-stu-id="5acc9-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 3.0 for StorSimple 8000 Series**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="5acc9-109">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5acc9-109">Click **Add**.</span></span> <span data-ttu-id="5acc9-110">L'aggiornamento viene aggiunto al carrello.</span><span class="sxs-lookup"><span data-stu-id="5acc9-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="5acc9-111">Cercare gli eventuali hotfix aggiuntivi elencati nella tabella precedente (**3186859**) e aggiungerli al carrello.</span><span class="sxs-lookup"><span data-stu-id="5acc9-111">Search for any additional hotfixes listed in the table above (**3186859**), and add each to the basket.</span></span>
6. <span data-ttu-id="5acc9-112">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="5acc9-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="5acc9-113">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="5acc9-113">Click **Download**.</span></span> <span data-ttu-id="5acc9-114">Specificare o **sfogliare** il percorso locale in cui si desidera salvare il file scaricato.</span><span class="sxs-lookup"><span data-stu-id="5acc9-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="5acc9-115">Gli aggiornamenti vengono scaricati nel percorso specificato e inseriti in una sottocartella con lo stesso nome dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="5acc9-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="5acc9-116">Inoltre, la cartella può essere copiata in una condivisione di rete raggiungibile dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5acc9-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="5acc9-117">Gli aggiornamenti rapidi devono essere accessibili da entrambi i controller per rilevare eventuali messaggi di errore potenziali dal controller peer.</span><span class="sxs-lookup"><span data-stu-id="5acc9-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="5acc9-118">Per installare e verificare gli hotfix in modalità normale</span><span class="sxs-lookup"><span data-stu-id="5acc9-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="5acc9-119">Per installare e verificare gli aggiornamenti rapidi in modalità normale, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="5acc9-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="5acc9-120">Se sono già stati installati tramite il portale di Azure, passare direttamente a [installare e verificare gli aggiornamenti rapidi in modalità di manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="5acc9-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="5acc9-121">Per installare gli hotfix, accedere all'interfaccia di Windows PowerShell dalla console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5acc9-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="5acc9-122">Seguire le istruzioni riportate in [Usare PuTTY per connettersi alla console seriale](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="5acc9-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="5acc9-123">Al prompt dei comandi, premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="5acc9-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="5acc9-124">Selezionare l' **opzione 1** per eseguire l'accesso completo al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5acc9-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="5acc9-125">È consigliabile installare innanzitutto l'hotfix sul controller passivo.</span><span class="sxs-lookup"><span data-stu-id="5acc9-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="5acc9-126">Per installare l'hotfix, al prompt dei comandi, digitare:</span><span class="sxs-lookup"><span data-stu-id="5acc9-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="5acc9-127">Utilizzare l’IP anziché il DNS nel percorso condivisione nel comando precedente.</span><span class="sxs-lookup"><span data-stu-id="5acc9-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="5acc9-128">Il parametro di credenziale viene utilizzato soltanto se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="5acc9-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="5acc9-129">È consigliabile utilizzare il parametro delle credenziali per accedere alle condivisioni.</span><span class="sxs-lookup"><span data-stu-id="5acc9-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="5acc9-130">Anche le condivisioni aperte a "tutti" non sono in genere aperte agli utenti non autenticati.</span><span class="sxs-lookup"><span data-stu-id="5acc9-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="5acc9-131">Specificare la password quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="5acc9-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="5acc9-132">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="5acc9-132">A sample output is shown below.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="5acc9-133">Digitare **Y** quando viene richiesto di confermare l'installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="5acc9-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="5acc9-134">Monitorare l'aggiornamento utilizzando il cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="5acc9-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="5acc9-135">L'aggiornamento verrà innanzitutto completato sul controller passivo.</span><span class="sxs-lookup"><span data-stu-id="5acc9-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="5acc9-136">Dopo aver aggiornato il controller passivo, si verificherà un failover e l'aggiornamento verrà quindi applicato all'altro controller.</span><span class="sxs-lookup"><span data-stu-id="5acc9-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="5acc9-137">L'aggiornamento è completato quando entrambi i controller vengono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="5acc9-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="5acc9-138">Il seguente output di esempio indica che l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="5acc9-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="5acc9-139">Il `RunInprogress` sarà `True` quando l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="5acc9-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="5acc9-140">Il seguente output di esempio indica che l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="5acc9-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="5acc9-141">Il `RunInProgress` sarà `False` quando l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="5acc9-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > <span data-ttu-id="5acc9-142">In alcuni casi, i cmdlet mostrano`False` quando l'aggiornamento è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="5acc9-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="5acc9-143">Per assicurarsi che l'aggiornamento rapido è stato completato, attendere alcuni minuti, eseguire nuovamente il comando e verificare che `RunInProgress` sia `False`.</span><span class="sxs-lookup"><span data-stu-id="5acc9-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="5acc9-144">In caso affermativo, l'aggiornamento rapido è stato completato.</span><span class="sxs-lookup"><span data-stu-id="5acc9-144">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="5acc9-145">Dopo aver installato gli aggiornamenti del software, verificare le versioni del software del sistema.</span><span class="sxs-lookup"><span data-stu-id="5acc9-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="5acc9-146">Digitare:</span><span class="sxs-lookup"><span data-stu-id="5acc9-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="5acc9-147">Dovrebbero essere visualizzate le seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="5acc9-147">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     <span data-ttu-id="5acc9-148">Se i numeri di versione non vengono modificati dopo aver applicato l'aggiornamento, significa che non è stato possibile applicare l'aggiornamento rapido.</span><span class="sxs-lookup"><span data-stu-id="5acc9-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="5acc9-149">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="5acc9-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="5acc9-150">È necessario riavviare il controller attivo tramite il cmdlet `Restart-HcsController` prima di applicare gli altri aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5acc9-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="5acc9-151">Ripetere i passaggi da 3 a 5 per installare il driver LSI e l'hotfix del firmware **KB3186859**.</span><span class="sxs-lookup"><span data-stu-id="5acc9-151">Repeat steps 3-5 to install the LSI driver and firmware hotfix **KB3186859**.</span></span> <span data-ttu-id="5acc9-152">Dopo aver installato l'hotfix, usare il cmdlet `Get-HcsSystem` .</span><span class="sxs-lookup"><span data-stu-id="5acc9-152">After the hotfix is installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="5acc9-153">La versione LSI deve essere:</span><span class="sxs-lookup"><span data-stu-id="5acc9-153">The LSI version should be:</span></span>
   
   * `Lsisas2Version: 2.0.78.00`
3. <span data-ttu-id="5acc9-154">Ripetere i passaggi da 3 a 5 per installare l'aggiornamento Storport e Spaceport **KB3121261**.</span><span class="sxs-lookup"><span data-stu-id="5acc9-154">Repeat steps 3-5 to install the Storport and Spaceport update **KB3121261**.</span></span>
4. <span data-ttu-id="5acc9-155">Se l'aggiornamento viene eseguito da Update 2 o una versione precedente, è anche necessario scaricare:</span><span class="sxs-lookup"><span data-stu-id="5acc9-155">If you are updating from Update 2 or earlier version, you will also need to download:</span></span>
   
   * <span data-ttu-id="5acc9-156">Fix iSCSI con KB3146621</span><span class="sxs-lookup"><span data-stu-id="5acc9-156">iSCSI fix using KB3146621</span></span>
   * <span data-ttu-id="5acc9-157">Fix WMI con KB3103616</span><span class="sxs-lookup"><span data-stu-id="5acc9-157">WMI fix using KB3103616</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="5acc9-158">Per installare e verificare gli aggiornamenti rapidi in modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="5acc9-158">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="5acc9-159">Usare KB3121899 per installare gli aggiornamenti del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="5acc9-159">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="5acc9-160">Si tratta di aggiornamenti problematici che richiedono circa 30 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="5acc9-160">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="5acc9-161">È possibile scegliere di installare tali aggiornamenti in una finestra di manutenzione pianificata tramite la connessione alla console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5acc9-161">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="5acc9-162">Se il firmware del disco è già aggiornato, non è necessario installare questi aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5acc9-162">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="5acc9-163">Eseguire il cmdlet `Get-HcsUpdateAvailability` dalla console seriale del dispositivo per verificare se sono disponibili aggiornamenti e se questi comportano o meno interruzioni del servizio e vanno quindi installati, rispettivamente, in modalità di manutenzione o in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="5acc9-163">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="5acc9-164">Per installare gli aggiornamenti del firmware del disco, seguire le istruzioni riportate sotto.</span><span class="sxs-lookup"><span data-stu-id="5acc9-164">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="5acc9-165">Attivare la modalità di manutenzione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5acc9-165">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="5acc9-166">Notare che non si deve utilizzare Windows PowerShell in remoto quando ci si connette a un dispositivo in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5acc9-166">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="5acc9-167">Eseguire questo cmdlet nel controller del dispositivo quando si è connessi tramite console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5acc9-167">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="5acc9-168">Digitare:</span><span class="sxs-lookup"><span data-stu-id="5acc9-168">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="5acc9-169">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="5acc9-169">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="5acc9-170">Entrambi i controller si riavviano in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5acc9-170">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="5acc9-171">Per installare l'aggiornamento firmware del disco, digitare:</span><span class="sxs-lookup"><span data-stu-id="5acc9-171">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="5acc9-172">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="5acc9-172">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="5acc9-173">Monitorare l'avanzamento dell'installazione con il comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="5acc9-173">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="5acc9-174">L'aggiornamento è completo quando `RunInProgress` diventa `False`.</span><span class="sxs-lookup"><span data-stu-id="5acc9-174">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="5acc9-175">Al termine dell'installazione, il controller in cui è stato installato l'aggiornamento rapido in modalità di manutenzione viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="5acc9-175">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="5acc9-176">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="5acc9-176">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="5acc9-177">Digitare:</span><span class="sxs-lookup"><span data-stu-id="5acc9-177">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="5acc9-178">Le versioni del firmware del disco previste sono:</span><span class="sxs-lookup"><span data-stu-id="5acc9-178">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="5acc9-179">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="5acc9-179">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="5acc9-180">Eseguire il comando `Get-HcsFirmwareVersion` sul secondo controller per verificare che la versione del software sia stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="5acc9-180">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="5acc9-181">È quindi possibile chiudere la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5acc9-181">You can then exit the maintenance mode.</span></span> <span data-ttu-id="5acc9-182">A tale scopo, digitare il comando seguente per ogni controller del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="5acc9-182">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="5acc9-183">I controller si riavviano quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5acc9-183">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="5acc9-184">Dopo la corretta istallazione degli aggiornamenti del firmware del disco e dopo che il dispositivo ha terminato la modalità manutenzione, tornare al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="5acc9-184">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="5acc9-185">Sul portale potrebbe non essere visualizzata l’installazione degli aggiornamenti di modalità manutenzione per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="5acc9-185">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

