<!--author=SharS last changed: 03/17/2016-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="92b80-101">Scaricare gli hotfix</span><span class="sxs-lookup"><span data-stu-id="92b80-101">To download hotfixes</span></span>
<span data-ttu-id="92b80-102">Attenersi alla seguente procedura per scaricare l'aggiornamento del software.</span><span class="sxs-lookup"><span data-stu-id="92b80-102">Perform the following steps to download the software update.</span></span>

1. <span data-ttu-id="92b80-103">Avviare Internet Explorer e accedere al sito [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="92b80-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="92b80-104">Se si usa Microsoft Update Catalog nel computer per la prima volta, fare clic su **Installa** quando viene richiesto di installare il componente aggiuntivo Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="92b80-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="92b80-105">![Installare il catalogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="92b80-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="92b80-106">Nella casella di ricerca di Microsoft Update Catalog, immettere il numero della Knowledge Base (KB) dell'hotfix da scaricare, ad esempio **3063418**, quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="92b80-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="92b80-107">Verrà visualizzato il bundle **StorSimple Update 1.2 Appliance Update** .</span><span class="sxs-lookup"><span data-stu-id="92b80-107">You will see the **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="92b80-108">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="92b80-108">Click **Add**.</span></span> <span data-ttu-id="92b80-109">L'aggiornamento verrà aggiunto al carrello.</span><span class="sxs-lookup"><span data-stu-id="92b80-109">The update will be added to the basket.</span></span>
5. <span data-ttu-id="92b80-110">Cercare gli eventuali hotfix aggiuntivi elencati nella tabella precedente (**3043005** e **3063416**) e aggiungerli al carrello.</span><span class="sxs-lookup"><span data-stu-id="92b80-110">Search for any additional hotfixes listed in the table above (**3043005** and **3063416**), and add each the basket.</span></span>
6. <span data-ttu-id="92b80-111">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="92b80-111">Click **View Basket**.</span></span>
   
    ![Visualizza carrello](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="92b80-113">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="92b80-113">Click **Download**.</span></span> <span data-ttu-id="92b80-114">Specificare o **selezionare** il percorso locale in cui salvare i file scaricati.</span><span class="sxs-lookup"><span data-stu-id="92b80-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="92b80-115">Gli aggiornamenti vengono scaricati nel percorso specificato e inseriti in una sottocartella con lo stesso nome dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="92b80-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="92b80-116">Inoltre, la cartella può essere copiata in una condivisione di rete raggiungibile dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92b80-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="92b80-117">Gli aggiornamenti rapidi devono essere accessibili da entrambi i controller per rilevare eventuali messaggi di errore potenziali dal controller peer.</span><span class="sxs-lookup"><span data-stu-id="92b80-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="92b80-118">Per installare e verificare gli hotfix in modalità normale</span><span class="sxs-lookup"><span data-stu-id="92b80-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="92b80-119">Eseguire i passaggi seguenti per installare e verificare gli aggiornamenti rapidi in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="92b80-119">Perform the following steps to install and verify the regular-mode hotfixes.</span></span> <span data-ttu-id="92b80-120">Se sono già stati installati tramite il portale di Azure, passare direttamente a [installare e verificare gli aggiornamenti rapidi in modalità di manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="92b80-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="92b80-121">Per installare l'aggiornamento del software, accedere all'interfaccia di Windows PowerShell dalla console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="92b80-121">To install the software update, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="92b80-122">Seguire le istruzioni riportate in [Usare PuTTY per connettersi alla console seriale](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="92b80-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="92b80-123">Al prompt dei comandi, premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="92b80-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="92b80-124">Selezionare l' **opzione 1** per eseguire l'accesso completo al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92b80-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="92b80-125">Per installare il pacchetto di aggiornamento, al prompt dei comandi, digitare:</span><span class="sxs-lookup"><span data-stu-id="92b80-125">To install the update package, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="92b80-126">Utilizzare l’IP anziché il DNS nel percorso condivisione nel comando precedente.</span><span class="sxs-lookup"><span data-stu-id="92b80-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="92b80-127">Il parametro di credenziale viene utilizzato soltanto se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="92b80-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="92b80-128">È consigliabile utilizzare il parametro delle credenziali per accedere alle condivisioni.</span><span class="sxs-lookup"><span data-stu-id="92b80-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="92b80-129">Anche le condivisioni aperte a "tutti" non sono in genere aperte agli utenti non autenticati.</span><span class="sxs-lookup"><span data-stu-id="92b80-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="92b80-130">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="92b80-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="92b80-131">Digitare **Y** quando viene richiesto di confermare l'installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="92b80-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="92b80-132">Monitorare l'aggiornamento utilizzando il cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="92b80-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="92b80-133">Il seguente output di esempio indica che l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="92b80-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="92b80-134">Il `RunInprogress` sarà `True` quando l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="92b80-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="92b80-135">Il seguente output di esempio indica che l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="92b80-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="92b80-136">Il `RunInProgress` sarà `False` quando l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="92b80-136">The `RunInProgress` will be `False` when the update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="92b80-137">In alcuni casi, i cmdlet mostrano`False` quando l'aggiornamento è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="92b80-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="92b80-138">Per assicurarsi che l'aggiornamento rapido è stato completato, attendere alcuni minuti, eseguire nuovamente il comando e verificare che `RunInProgress` sia `False`.</span><span class="sxs-lookup"><span data-stu-id="92b80-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="92b80-139">In caso affermativo, l'aggiornamento rapido è stato completato.</span><span class="sxs-lookup"><span data-stu-id="92b80-139">If it is, then the hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="92b80-140">Dopo aver installato gli aggiornamenti del software, verificare le versioni del software del sistema.</span><span class="sxs-lookup"><span data-stu-id="92b80-140">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="92b80-141">Digitare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="92b80-141">Type the following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="92b80-142">Dovrebbero essere visualizzate le seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="92b80-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="92b80-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="92b80-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="92b80-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="92b80-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="92b80-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="92b80-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="92b80-146">Se i numeri di versione non vengono modificati dopo aver applicato l'aggiornamento, significa che non è stato possibile applicare l'aggiornamento rapido.</span><span class="sxs-lookup"><span data-stu-id="92b80-146">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="92b80-147">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="92b80-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="92b80-148">Ripetere i passaggi da 3 a 5 per installare il resto degli aggiornamenti rapidi in modalità normale (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="92b80-148">Repeat steps 3-5 to install the remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="92b80-149">Per installare e verificare gli aggiornamenti rapidi in modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="92b80-149">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="92b80-150">Usare KB3063416 per installare gli aggiornamenti del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="92b80-150">Use KB3063416 to install disk firmware updates.</span></span> <span data-ttu-id="92b80-151">Si tratta di aggiornamenti con interruzione del servizio che richiedono circa 30-45 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="92b80-151">These are disruptive updates and take around 30-45 minutes to complete.</span></span> <span data-ttu-id="92b80-152">È possibile scegliere di installare tali aggiornamenti in una finestra di manutenzione pianificata tramite la connessione alla console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92b80-152">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="92b80-153">Per installare gli aggiornamenti del firmware del disco, seguire le istruzioni riportate sotto.</span><span class="sxs-lookup"><span data-stu-id="92b80-153">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="92b80-154">Attivare la modalità di manutenzione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92b80-154">Place the device in Maintenance mode.</span></span> <span data-ttu-id="92b80-155">Notare che non si deve utilizzare Windows PowerShell in remoto quando ci si connette a un dispositivo in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="92b80-155">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="92b80-156">È necessario eseguire questo cmdlet nel controller del dispositivo quando si è connessi tramite console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92b80-156">You will need to run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="92b80-157">Digitare:</span><span class="sxs-lookup"><span data-stu-id="92b80-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="92b80-158">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="92b80-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="92b80-159">Entrambi i controller si riavviano in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="92b80-159">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="92b80-160">Per installare l'aggiornamento firmware del disco, digitare:</span><span class="sxs-lookup"><span data-stu-id="92b80-160">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="92b80-161">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="92b80-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="92b80-162">Monitorare l'avanzamento dell'installazione con il comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="92b80-162">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="92b80-163">L'aggiornamento è completo quando `RunInProgress` diventa `False`.</span><span class="sxs-lookup"><span data-stu-id="92b80-163">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="92b80-164">Una volta completata l'installazione, il controller in cui è stato installato l'hotfix in modalità di manutenzione viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="92b80-164">After the installation is complete, the controller on which the maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="92b80-165">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="92b80-165">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="92b80-166">Digitare:</span><span class="sxs-lookup"><span data-stu-id="92b80-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="92b80-167">Le versioni del firmware del disco previste sono:</span><span class="sxs-lookup"><span data-stu-id="92b80-167">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="92b80-168">Eseguire il comando `Get-HcsFirmwareVersion` sul secondo controller per verificare che la versione del software sia stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="92b80-168">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="92b80-169">È quindi possibile chiudere la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="92b80-169">You can then exit the maintenance mode.</span></span> <span data-ttu-id="92b80-170">Digitare il comando seguente per ogni controller del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="92b80-170">Type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="92b80-171">I controller si riavviano quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="92b80-171">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="92b80-172">Dopo la corretta istallazione degli aggiornamenti del firmware del disco e dopo che il dispositivo ha terminato la modalità manutenzione, tornare al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="92b80-172">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="92b80-173">Sul portale potrebbe non essere visualizzata l’installazione degli aggiornamenti di modalità manutenzione per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="92b80-173">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

