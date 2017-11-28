<!--author=alkohli last changed: 03/17/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="72823-101">Scaricare gli hotfix</span><span class="sxs-lookup"><span data-stu-id="72823-101">To download hotfixes</span></span>
<span data-ttu-id="72823-102">Eseguire i passaggi seguenti per scaricare l'aggiornamento del software da Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="72823-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="72823-103">Avviare Internet Explorer e accedere al sito [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="72823-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="72823-104">Se si usa Microsoft Update Catalog nel computer per la prima volta, fare clic su **Installa** quando viene richiesto di installare il componente aggiuntivo Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="72823-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="72823-105">![Installare il catalogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="72823-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="72823-106">Nella casella di ricerca di Microsoft Update Catalog, immettere il numero della Knowledge Base (KB) dell'hotfix da scaricare, ad esempio **3121901**, quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="72823-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="72823-107">Viene visualizzato l'elenco degli aggiornamenti rapidi, ad esempio, **Aggiornamento cumulativo del pacchetto software 2.0 per StorSimple serie 8000**.</span><span class="sxs-lookup"><span data-stu-id="72823-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="72823-109">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72823-109">Click **Add**.</span></span> <span data-ttu-id="72823-110">L'aggiornamento viene aggiunto al carrello.</span><span class="sxs-lookup"><span data-stu-id="72823-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="72823-111">Cercare gli eventuali hotfix aggiuntivi elencati nella tabella precedente (**3121900**, **3080728**, **3090322** e **3121899**) e aggiungerli al carrello.</span><span class="sxs-lookup"><span data-stu-id="72823-111">Search for any additional hotfixes listed in the table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each the basket.</span></span>
6. <span data-ttu-id="72823-112">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="72823-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="72823-113">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="72823-113">Click **Download**.</span></span> <span data-ttu-id="72823-114">Specificare o **selezionare** il percorso locale in cui salvare i file scaricati.</span><span class="sxs-lookup"><span data-stu-id="72823-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="72823-115">Gli aggiornamenti vengono scaricati nel percorso specificato e inseriti in una sottocartella con lo stesso nome dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="72823-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="72823-116">Inoltre, la cartella può essere copiata in una condivisione di rete raggiungibile dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72823-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="72823-117">Gli aggiornamenti rapidi devono essere accessibili da entrambi i controller per rilevare eventuali messaggi di errore potenziali dal controller peer.</span><span class="sxs-lookup"><span data-stu-id="72823-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="72823-118">Per installare e verificare gli hotfix in modalità normale</span><span class="sxs-lookup"><span data-stu-id="72823-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="72823-119">Per installare e verificare gli aggiornamenti rapidi in modalità normale, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="72823-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="72823-120">Se sono già stati installati tramite il portale di Azure, passare direttamente a [installare e verificare gli aggiornamenti rapidi in modalità di manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="72823-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="72823-121">Per installare gli hotfix, accedere all'interfaccia di Windows PowerShell dalla console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="72823-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="72823-122">Seguire le istruzioni riportate in [Usare PuTTY per connettersi alla console seriale](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="72823-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="72823-123">Al prompt dei comandi, premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="72823-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="72823-124">Selezionare l' **opzione 1** per eseguire l'accesso completo al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72823-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="72823-125">Per installare l'hotfix, al prompt dei comandi, digitare:</span><span class="sxs-lookup"><span data-stu-id="72823-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="72823-126">Utilizzare l’IP anziché il DNS nel percorso condivisione nel comando precedente.</span><span class="sxs-lookup"><span data-stu-id="72823-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="72823-127">Il parametro di credenziale viene utilizzato soltanto se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="72823-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="72823-128">È consigliabile utilizzare il parametro delle credenziali per accedere alle condivisioni.</span><span class="sxs-lookup"><span data-stu-id="72823-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="72823-129">Anche le condivisioni aperte a "tutti" non sono in genere aperte agli utenti non autenticati.</span><span class="sxs-lookup"><span data-stu-id="72823-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="72823-130">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="72823-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="72823-131">Digitare **Y** quando viene richiesto di confermare l'installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="72823-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="72823-132">Monitorare l'aggiornamento utilizzando il cmdlet `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="72823-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="72823-133">Il seguente output di esempio indica che l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="72823-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="72823-134">Il `RunInprogress` sarà `True` quando l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="72823-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="72823-135">Il seguente output di esempio indica che l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="72823-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="72823-136">Il `RunInProgress` sarà `False` quando l'aggiornamento è stato completato.</span><span class="sxs-lookup"><span data-stu-id="72823-136">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="72823-137">In alcuni casi, i cmdlet mostrano`False` quando l'aggiornamento è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="72823-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="72823-138">Per assicurarsi che l'aggiornamento rapido è stato completato, attendere alcuni minuti, eseguire nuovamente il comando e verificare che `RunInProgress` sia `False`.</span><span class="sxs-lookup"><span data-stu-id="72823-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="72823-139">In caso affermativo, l'aggiornamento rapido è stato completato.</span><span class="sxs-lookup"><span data-stu-id="72823-139">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="72823-140">Al termine dell'aggiornamento del software, ripetere i passaggi da 3 a 5 per installare e monitorare l'agente SaaS e l'agente MDS.</span><span class="sxs-lookup"><span data-stu-id="72823-140">After the software update is complete, repeat steps 3-5 to install and monitor the SaaS agent and MDS agent .</span></span> <span data-ttu-id="72823-141">Assicurarsi che `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` venga installato prima di `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="72823-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="72823-142">Verificare le versioni del software di sistema.</span><span class="sxs-lookup"><span data-stu-id="72823-142">Verify the system software versions.</span></span> <span data-ttu-id="72823-143">Digitare:</span><span class="sxs-lookup"><span data-stu-id="72823-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="72823-144">Dovrebbero essere visualizzate le seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="72823-144">You should see the following versions:</span></span>
   
   * <span data-ttu-id="72823-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="72823-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="72823-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="72823-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="72823-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="72823-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="72823-148">Se i numeri di versione non vengono modificati dopo aver applicato l'aggiornamento, significa che non è stato possibile applicare l'aggiornamento rapido.</span><span class="sxs-lookup"><span data-stu-id="72823-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="72823-149">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="72823-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="72823-150">Ripetere i passaggi da 3 a 5 per installare il resto degli aggiornamenti rapidi in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="72823-150">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="72823-151">Driver LSI, KB3121900</span><span class="sxs-lookup"><span data-stu-id="72823-151">The LSI driver - KB3121900</span></span>
   * <span data-ttu-id="72823-152">Aggiornamento di Storport, KB3080728</span><span class="sxs-lookup"><span data-stu-id="72823-152">The Storport update - KB3080728</span></span>
   * <span data-ttu-id="72823-153">Aggiornamento di Spaceport, KB3090322</span><span class="sxs-lookup"><span data-stu-id="72823-153">The Spaceport update - KB3090322</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="72823-154">Per installare e verificare gli aggiornamenti rapidi in modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="72823-154">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="72823-155">Usare KB3121899 per installare gli aggiornamenti del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="72823-155">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="72823-156">Si tratta di aggiornamenti problematici che richiedono circa 30 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="72823-156">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="72823-157">È possibile scegliere di installare tali aggiornamenti in una finestra di manutenzione pianificata tramite la connessione alla console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72823-157">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="72823-158">Se il firmware del disco è già aggiornato, non è necessario installare questi aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="72823-158">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="72823-159">Eseguire il cmdlet `Get-HcsUpdateAvailability` dalla console seriale del dispositivo per verificare se sono disponibili aggiornamenti e se questi comportano o meno interruzioni del servizio e vanno quindi installati, rispettivamente, in modalità di manutenzione o in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="72823-159">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="72823-160">Per installare gli aggiornamenti del firmware del disco, seguire le istruzioni riportate sotto.</span><span class="sxs-lookup"><span data-stu-id="72823-160">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="72823-161">Attivare la modalità di manutenzione per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72823-161">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="72823-162">Notare che non si deve utilizzare Windows PowerShell in remoto quando ci si connette a un dispositivo in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="72823-162">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="72823-163">Eseguire questo cmdlet nel controller del dispositivo quando si è connessi tramite console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="72823-163">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="72823-164">Digitare:</span><span class="sxs-lookup"><span data-stu-id="72823-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="72823-165">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="72823-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="72823-166">Entrambi i controller si riavviano in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="72823-166">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="72823-167">Per installare l'aggiornamento firmware del disco, digitare:</span><span class="sxs-lookup"><span data-stu-id="72823-167">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="72823-168">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="72823-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="72823-169">Monitorare l'avanzamento dell'installazione con il comando `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="72823-169">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="72823-170">L'aggiornamento è completo quando `RunInProgress` diventa `False`.</span><span class="sxs-lookup"><span data-stu-id="72823-170">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="72823-171">Al termine dell'installazione, il controller in cui è stato installato l'aggiornamento rapido in modalità di manutenzione viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="72823-171">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="72823-172">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="72823-172">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="72823-173">Digitare:</span><span class="sxs-lookup"><span data-stu-id="72823-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="72823-174">Le versioni del firmware del disco previste sono:</span><span class="sxs-lookup"><span data-stu-id="72823-174">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="72823-175">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="72823-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
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
   
    <span data-ttu-id="72823-176">Eseguire il comando `Get-HcsFirmwareVersion` sul secondo controller per verificare che la versione del software sia stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="72823-176">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="72823-177">È quindi possibile chiudere la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="72823-177">You can then exit the maintenance mode.</span></span> <span data-ttu-id="72823-178">A tale scopo, digitare il comando seguente per ogni controller del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="72823-178">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="72823-179">I controller si riavviano quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="72823-179">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="72823-180">Dopo la corretta istallazione degli aggiornamenti del firmware del disco e dopo che il dispositivo ha terminato la modalità manutenzione, tornare al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="72823-180">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="72823-181">Sul portale potrebbe non essere visualizzata l’installazione degli aggiornamenti di modalità manutenzione per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="72823-181">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

