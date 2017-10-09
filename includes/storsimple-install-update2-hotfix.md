<!--author=alkohli last changed: 03/17/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="38771-101">aggiornamenti rapidi toodownload</span><span class="sxs-lookup"><span data-stu-id="38771-101">toodownload hotfixes</span></span>
<span data-ttu-id="38771-102">Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="38771-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="38771-103">Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="38771-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="38771-104">Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="38771-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="38771-105">![Installare il catalogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="38771-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="38771-106">Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload, ad esempio **3121901**, quindi fare clic su **ricerca**.</span><span class="sxs-lookup"><span data-stu-id="38771-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="38771-107">Hello hotfix elenco viene visualizzato, ad esempio, **cumulativo Software Bundle di aggiornamento 2.0 per StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="38771-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="38771-109">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="38771-109">Click **Add**.</span></span> <span data-ttu-id="38771-110">aggiornamento di Hello viene aggiunto toohello carrello.</span><span class="sxs-lookup"><span data-stu-id="38771-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="38771-111">Cercare gli aggiornamenti rapidi di aggiuntivi elencate nella tabella hello precedente (**3121900**, **3080728**, **3090322**, e **3121899**) e aggiungere ogni carrello Hello.</span><span class="sxs-lookup"><span data-stu-id="38771-111">Search for any additional hotfixes listed in hello table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each hello basket.</span></span>
6. <span data-ttu-id="38771-112">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="38771-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="38771-113">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="38771-113">Click **Download**.</span></span> <span data-ttu-id="38771-114">Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear.</span><span class="sxs-lookup"><span data-stu-id="38771-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="38771-115">Hello gli aggiornamenti vengono scaricati toohello percorso specificato e inserito in una sottocartella con stesso nome come aggiornamento hello hello.</span><span class="sxs-lookup"><span data-stu-id="38771-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="38771-116">cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="38771-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="38771-117">Hello hotfix deve essere accessibile da entrambi i controller toodetect qualsiasi errore potenziale dei messaggi dal controller peer hello.</span><span class="sxs-lookup"><span data-stu-id="38771-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="38771-118">tooinstall e verificare gli aggiornamenti rapidi alla modalità normale</span><span class="sxs-lookup"><span data-stu-id="38771-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="38771-119">Eseguire i seguenti passaggi tooinstall hello e verificare gli aggiornamenti rapidi in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="38771-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="38771-120">Se è già stato installato utilizzando hello del portale di Azure andare troppo[installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="38771-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="38771-121">tooinstall hello hotfixes interfaccia di Windows PowerShell di accesso hello nella console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="38771-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="38771-122">Seguire hello dettagliate in [console seriale di usare PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="38771-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="38771-123">Al prompt dei comandi di hello, premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="38771-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="38771-124">Selezionare **opzione 1** toolog toohello dispositivo con accesso completo.</span><span class="sxs-lookup"><span data-stu-id="38771-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="38771-125">hotfix hello tooinstall, al prompt dei comandi di hello, tipo:</span><span class="sxs-lookup"><span data-stu-id="38771-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="38771-126">Utilizzare IP anziché DNS nel percorso di condivisione in hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="38771-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="38771-127">parametro credential Hello viene utilizzata solo se si accede a una condivisione autenticata.</span><span class="sxs-lookup"><span data-stu-id="38771-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="38771-128">È consigliabile utilizzare condivisioni tooaccess parametro delle credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="38771-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="38771-129">Anche le condivisioni che sono aperte troppo "everyone" è in genere non aprire toounauthenticated utenti.</span><span class="sxs-lookup"><span data-stu-id="38771-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="38771-130">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="38771-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="38771-131">Tipo **Y** quando richiesta tooconfirm hello installazione dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="38771-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="38771-132">Monitorare l'aggiornamento di hello utilizzando hello `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38771-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="38771-133">Hello output di esempio seguente viene illustrato hello aggiornamento in corso.</span><span class="sxs-lookup"><span data-stu-id="38771-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="38771-134">Hello `RunInprogress` sarà `True` quando hello aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="38771-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="38771-135">Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato.</span><span class="sxs-lookup"><span data-stu-id="38771-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="38771-136">Hello `RunInProgress` sarà `False` quando hello aggiornamento completato.</span><span class="sxs-lookup"><span data-stu-id="38771-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="38771-137">In alcuni casi, hello cmdlet report `False` quando aggiornamento hello è ancora in corso.</span><span class="sxs-lookup"><span data-stu-id="38771-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="38771-138">tooensure che hello hotfix è stata completata, attendere qualche minuto, eseguire nuovamente il comando e verificare che hello `RunInProgress` è `False`.</span><span class="sxs-lookup"><span data-stu-id="38771-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="38771-139">Se si tratta, hotfix hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="38771-139">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="38771-140">Dopo il software di hello aggiornamento è completo, ripetere i passaggi 3-5 agente SaaS hello tooinstall e monitoraggio e l'agente MDS.</span><span class="sxs-lookup"><span data-stu-id="38771-140">After hello software update is complete, repeat steps 3-5 tooinstall and monitor hello SaaS agent and MDS agent .</span></span> <span data-ttu-id="38771-141">Assicurarsi che `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` venga installato prima di `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="38771-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="38771-142">Verificare le versioni di software di hello del sistema.</span><span class="sxs-lookup"><span data-stu-id="38771-142">Verify hello system software versions.</span></span> <span data-ttu-id="38771-143">Digitare:</span><span class="sxs-lookup"><span data-stu-id="38771-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="38771-144">È necessario visualizzare hello seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="38771-144">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="38771-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="38771-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="38771-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="38771-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="38771-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="38771-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="38771-148">Se non viene modificata dopo l'applicazione hello aggiornamento numeri di versione di hello, significa che tale hotfix hello tooapply non riuscita.</span><span class="sxs-lookup"><span data-stu-id="38771-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="38771-149">In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="38771-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="38771-150">Ripetere i passaggi da 3 a 5 tooinstall hello rimanenti hotfix in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="38771-150">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="38771-151">Hello driver LSI - KB3121900</span><span class="sxs-lookup"><span data-stu-id="38771-151">hello LSI driver - KB3121900</span></span>
   * <span data-ttu-id="38771-152">Hello aggiornamento Storport - KB3080728</span><span class="sxs-lookup"><span data-stu-id="38771-152">hello Storport update - KB3080728</span></span>
   * <span data-ttu-id="38771-153">aggiornamento di Spaceport - KB3090322 Hello</span><span class="sxs-lookup"><span data-stu-id="38771-153">hello Spaceport update - KB3090322</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="38771-154">tooinstall e verificare l'hotfix in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="38771-154">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="38771-155">Usare gli aggiornamenti del firmware di KB3121899 tooinstall disco.</span><span class="sxs-lookup"><span data-stu-id="38771-155">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="38771-156">Questi aggiornamenti comportano interruzioni e e richiedere toocomplete circa 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="38771-156">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="38771-157">È possibile scegliere tooinstall in una finestra di manutenzione pianificata per la connessione console seriale del dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="38771-157">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="38771-158">Si noti che se il firmware del disco è già stato aggiornato, non sarà necessario tooinstall questi aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="38771-158">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="38771-159">Eseguire hello `Get-HcsUpdateAvailability` da hello dispositivo console seriale toocheck se sono disponibili aggiornamenti che indica se hello Aggiorna sono comportano interruzioni del servizio (modalità di manutenzione) o non comportano interruzioni del servizio (modalità normale) gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="38771-159">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="38771-160">aggiornamenti del firmware di tooinstall hello disco, seguire le istruzioni di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="38771-160">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="38771-161">Dispositivo di hello sul posto in modalità manutenzione hello.</span><span class="sxs-lookup"><span data-stu-id="38771-161">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="38771-162">Si noti che è necessario non utilizzare Windows PowerShell in remoto quando ci si connette il dispositivo tooa in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="38771-162">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="38771-163">In alternativa, eseguire questo cmdlet nel controller del dispositivo hello quando si è connessi tramite console seriale del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="38771-163">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="38771-164">Digitare:</span><span class="sxs-lookup"><span data-stu-id="38771-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="38771-165">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="38771-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="38771-166">Riavviare entrambi i controller hello in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="38771-166">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="38771-167">aggiornamento di firmware del disco con hello di tooinstall, tipo:</span><span class="sxs-lookup"><span data-stu-id="38771-167">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="38771-168">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="38771-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="38771-169">Monitoraggio hello installa lo stato di avanzamento utilizzando `Get-HcsUpdateStatus` comando.</span><span class="sxs-lookup"><span data-stu-id="38771-169">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="38771-170">Hello aggiornamento è stata completata quando hello `RunInProgress` cambia troppo`False`.</span><span class="sxs-lookup"><span data-stu-id="38771-170">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="38771-171">Al termine dell'installazione di hello, hello del controller in cui hello è stato installato l'hotfix di modalità di manutenzione viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="38771-171">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="38771-172">Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco hello.</span><span class="sxs-lookup"><span data-stu-id="38771-172">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="38771-173">Digitare:</span><span class="sxs-lookup"><span data-stu-id="38771-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="38771-174">Hello previsti sono le versioni del firmware del disco:</span><span class="sxs-lookup"><span data-stu-id="38771-174">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="38771-175">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="38771-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
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
   
    <span data-ttu-id="38771-176">Eseguire hello `Get-HcsFirmwareVersion` comando hello secondo controller tooverify che hello versione del software è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="38771-176">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="38771-177">È quindi possibile uscire dalla modalità di manutenzione hello.</span><span class="sxs-lookup"><span data-stu-id="38771-177">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="38771-178">toodo in tal caso, digitare hello comando per ogni controller del dispositivo seguente:</span><span class="sxs-lookup"><span data-stu-id="38771-178">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="38771-179">controller Hello riavviare quando si esce dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="38771-179">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="38771-180">Dopo il firmware del disco hello gli aggiornamenti sono stati correttamente applicati e dispositivo hello è uscito dalla modalità di manutenzione, restituito toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="38771-180">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="38771-181">Si noti che il portale di hello potrebbe non visualizzare installato gli aggiornamenti in modalità manutenzione hello per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="38771-181">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

