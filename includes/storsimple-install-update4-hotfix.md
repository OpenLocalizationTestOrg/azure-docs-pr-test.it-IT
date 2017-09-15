<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="b6487-101">Scaricare gli hotfix</span><span class="sxs-lookup"><span data-stu-id="b6487-101">To download hotfixes</span></span>

<span data-ttu-id="b6487-102">Eseguire i passaggi seguenti per scaricare l'aggiornamento del software da Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="b6487-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="b6487-103">Avviare Internet Explorer e accedere al sito [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b6487-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="b6487-104">Se si usa Microsoft Update Catalog nel computer per la prima volta, fare clic su **Installa** quando viene richiesto di installare il componente aggiuntivo Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="b6487-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Installare il catalogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="b6487-106">Nella casella di ricerca di Microsoft Update Catalog immettere il numero della Knowledge Base (KB) relativo all'hotfix da scaricare, ad esempio **4011839**, quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="b6487-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="b6487-107">Verrà visualizzato l'elenco degli hotfix, ad esempio, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**(Aggiornamento cumulativo del pacchetto software 4.0 per StorSimple serie 8000).</span><span class="sxs-lookup"><span data-stu-id="b6487-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="b6487-109">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="b6487-109">Click **Download**.</span></span> <span data-ttu-id="b6487-110">Specificare o **sfogliare** il percorso locale in cui si desidera salvare il file scaricato.</span><span class="sxs-lookup"><span data-stu-id="b6487-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="b6487-111">Fare clic sui file da scaricare nel percorso e nella cartella specificati.</span><span class="sxs-lookup"><span data-stu-id="b6487-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="b6487-112">Inoltre, la cartella può essere copiata in una condivisione di rete raggiungibile dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6487-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="b6487-113">Cercare gli eventuali hotfix aggiuntivi elencati nella tabella precedente (**4011841**) e scaricare i file corrispondenti nelle cartelle specifiche indicate in tale tabella.</span><span class="sxs-lookup"><span data-stu-id="b6487-113">Search for any additional hotfixes listed in the table above (**4011841**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="b6487-114">Gli aggiornamenti rapidi devono essere accessibili da entrambi i controller per rilevare eventuali messaggi di errore potenziali dal controller peer.</span><span class="sxs-lookup"><span data-stu-id="b6487-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="b6487-115">È necessario copiare gli hotfix in tre cartelle separate.</span><span class="sxs-lookup"><span data-stu-id="b6487-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="b6487-116">Ad esempio, l'aggiornamento del software del dispositivo o dell'agente Cis/MDS può essere copiato nella cartella _FirstOrderUpdate_, tutti gli altri aggiornamenti che non comportano interruzioni del servizio possono essere copiati nella cartella _SecondOrderUpdate_ e gli aggiornamenti per la modalità di manutenzione possono essere copiati nella cartella _ThirdOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="b6487-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="b6487-117">Per installare e verificare gli hotfix in modalità normale</span><span class="sxs-lookup"><span data-stu-id="b6487-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="b6487-118">Per installare e verificare gli aggiornamenti rapidi in modalità normale, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="b6487-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="b6487-119">Se sono già stati installati tramite il portale di Azure classico, passare direttamente a [installare e verificare gli hotfix per la modalità di manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="b6487-119">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="b6487-120">Per installare gli hotfix, accedere all'interfaccia di Windows PowerShell dalla console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6487-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="b6487-121">Seguire le istruzioni riportate in [Usare PuTTY per connettersi alla console seriale](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b6487-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="b6487-122">Al prompt dei comandi, premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="b6487-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="b6487-123">Selezionare l' **opzione 1** per eseguire l'accesso completo al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6487-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="b6487-124">È consigliabile installare innanzitutto l'hotfix sul controller passivo.</span><span class="sxs-lookup"><span data-stu-id="b6487-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="b6487-125">Per installare l'hotfix, al prompt dei comandi, digitare:</span><span class="sxs-lookup"><span data-stu-id="b6487-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="b6487-126">Utilizzare l’IP anziché il DNS nel percorso condivisione nel comando precedente.</span><span class="sxs-lookup"><span data-stu-id="b6487-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="b6487-127">Il parametro di credenziale viene utilizzato soltanto se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="b6487-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="b6487-128">È consigliabile utilizzare il parametro delle credenziali per accedere alle condivisioni.</span><span class="sxs-lookup"><span data-stu-id="b6487-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="b6487-129">Anche le condivisioni aperte a "tutti" non sono in genere aperte agli utenti non autenticati.</span><span class="sxs-lookup"><span data-stu-id="b6487-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="b6487-130">Specificare la password quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="b6487-130">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="b6487-131">Di seguito è riportato un output di esempio per l'installazione degli aggiornamenti di primo livello.</span><span class="sxs-lookup"><span data-stu-id="b6487-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="b6487-132">Per l'aggiornamento di primo livello, è necessario fare riferimento al file specifico.</span><span class="sxs-lookup"><span data-stu-id="b6487-132">For the first order update, you need to point to the specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="b6487-133">Digitare **Y** quando viene richiesto di confermare l'installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="b6487-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="b6487-134">Monitorare l'aggiornamento utilizzando il cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="b6487-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="b6487-135">L'aggiornamento verrà innanzitutto completato sul controller passivo.</span><span class="sxs-lookup"><span data-stu-id="b6487-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="b6487-136">Dopo aver aggiornato il controller passivo, si verificherà un failover e l'aggiornamento verrà quindi applicato all'altro controller.</span><span class="sxs-lookup"><span data-stu-id="b6487-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="b6487-137">L'aggiornamento è completato quando entrambi i controller vengono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="b6487-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="b6487-138">Il seguente output di esempio indica che l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="b6487-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="b6487-139">Il `RunInprogress` sarà `True` quando l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="b6487-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="b6487-140">Il seguente output di esempio indica che l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="b6487-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="b6487-141">Il `RunInProgress` sarà `False` quando l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="b6487-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="b6487-142">In alcuni casi, i cmdlet mostrano`False` quando l'aggiornamento è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="b6487-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="b6487-143">Per assicurarsi che l'aggiornamento rapido è stato completato, attendere alcuni minuti, eseguire nuovamente il comando e verificare che `RunInProgress` sia `False`.</span><span class="sxs-lookup"><span data-stu-id="b6487-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="b6487-144">In caso affermativo, l'aggiornamento rapido è stato completato.</span><span class="sxs-lookup"><span data-stu-id="b6487-144">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="b6487-145">Dopo aver installato gli aggiornamenti del software, verificare le versioni del software del sistema.</span><span class="sxs-lookup"><span data-stu-id="b6487-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="b6487-146">Digitare:</span><span class="sxs-lookup"><span data-stu-id="b6487-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="b6487-147">Dovrebbero essere visualizzate le seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="b6487-147">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="b6487-148">Se il numero di versione non cambia dopo aver applicato l'aggiornamento, non è stato possibile applicare l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="b6487-148">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="b6487-149">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="b6487-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="b6487-150">Prima di applicare l'aggiornamento successivo è necessario riavviare il controller attivo tramite il cmdlet `Restart-HcsController`.</span><span class="sxs-lookup"><span data-stu-id="b6487-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
7. <span data-ttu-id="b6487-151">Ripetere i passaggi 3-5 per installare l'agente Cis/MDS scaricato nella cartella _FirstOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="b6487-151">Repeat steps 3-5 to install the Cis/MDS agent downloaded to your _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="b6487-152">Ripetere i passaggi da 3 a 5 per installare gli aggiornamenti di secondo livello.</span><span class="sxs-lookup"><span data-stu-id="b6487-152">Repeat steps 3-5 to install the second order updates.</span></span> <span data-ttu-id="b6487-153">**Per gli aggiornamenti di secondo livello, è possibile installare più aggiornamenti eseguendo semplicemente `Start-HcsHotfix cmdlet` e puntando alla cartella in cui si trovano gli aggiornamenti di secondo livello. Il cmdlet eseguirà tutti gli aggiornamenti disponibili nella cartella.**</span><span class="sxs-lookup"><span data-stu-id="b6487-153">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span></span> <span data-ttu-id="b6487-154">Se è già installato un aggiornamento, la logica di aggiornamento lo rileva e non applica l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="b6487-154">If an update is already installed, the update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="b6487-155">Dopo aver installato tutti gli hotfix, usare il cmdlet `Get-HcsSystem`.</span><span class="sxs-lookup"><span data-stu-id="b6487-155">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="b6487-156">Le versioni devono essere:</span><span class="sxs-lookup"><span data-stu-id="b6487-156">The versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="b6487-157">Per installare e verificare gli aggiornamenti rapidi in modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="b6487-157">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="b6487-158">Usare KB4011837 per installare gli aggiornamenti del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="b6487-158">Use KB4011837 to install disk firmware updates.</span></span> <span data-ttu-id="b6487-159">Si tratta di aggiornamenti problematici che richiedono circa 30 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="b6487-159">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="b6487-160">È possibile scegliere di installare tali aggiornamenti in una finestra di manutenzione pianificata tramite la connessione alla console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6487-160">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="b6487-161">Se il firmware del disco è già aggiornato, non è necessario installare questi aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="b6487-161">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="b6487-162">Eseguire il cmdlet `Get-HcsUpdateAvailability` dalla console seriale del dispositivo per verificare se sono disponibili aggiornamenti e se questi comportano o meno interruzioni del servizio e vanno quindi installati, rispettivamente, in modalità di manutenzione o in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="b6487-162">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="b6487-163">Per installare gli aggiornamenti del firmware del disco, seguire le istruzioni riportate sotto.</span><span class="sxs-lookup"><span data-stu-id="b6487-163">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="b6487-164">Attivare la modalità di manutenzione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6487-164">Place the device in the maintenance mode.</span></span> <span data-ttu-id="b6487-165">**Non è consigliabile usare Windows PowerShell in remoto quando ci si connette a un dispositivo in modalità di manutenzione. Eseguire questo cmdlet nel controller del dispositivo quando si è connessi tramite la console seriale del dispositivo.**</span><span class="sxs-lookup"><span data-stu-id="b6487-165">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span></span> <span data-ttu-id="b6487-166">Digitare:</span><span class="sxs-lookup"><span data-stu-id="b6487-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="b6487-167">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="b6487-167">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="b6487-168">Entrambi i controller si riavviano in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="b6487-168">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="b6487-169">Per installare l'aggiornamento firmware del disco, digitare:</span><span class="sxs-lookup"><span data-stu-id="b6487-169">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="b6487-170">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="b6487-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="b6487-171">Monitorare l'avanzamento dell'installazione con il comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="b6487-171">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="b6487-172">L'aggiornamento è completo quando `RunInProgress` diventa `False`.</span><span class="sxs-lookup"><span data-stu-id="b6487-172">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="b6487-173">Al termine dell'installazione, il controller in cui è stato installato l'aggiornamento rapido in modalità di manutenzione viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="b6487-173">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="b6487-174">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="b6487-174">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="b6487-175">Digitare:</span><span class="sxs-lookup"><span data-stu-id="b6487-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="b6487-176">Le versioni del firmware del disco previste sono:</span><span class="sxs-lookup"><span data-stu-id="b6487-176">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="b6487-177">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="b6487-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="b6487-178">Eseguire il comando `Get-HcsFirmwareVersion` sul secondo controller per verificare che la versione del software sia stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="b6487-178">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="b6487-179">È quindi possibile chiudere la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="b6487-179">You can then exit the maintenance mode.</span></span> <span data-ttu-id="b6487-180">A tale scopo, digitare il comando seguente per ogni controller del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b6487-180">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="b6487-181">I controller si riavviano quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="b6487-181">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="b6487-182">Dopo la corretta istallazione degli aggiornamenti del firmware del disco e dopo che il dispositivo ha terminato la modalità manutenzione, tornare al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="b6487-182">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="b6487-183">Si noti che il portale potrebbe non mostrare che sono stati installati gli aggiornamenti per la modalità di manutenzione prima di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="b6487-183">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

