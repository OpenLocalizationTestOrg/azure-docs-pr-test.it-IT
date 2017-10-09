<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="737d4-101">tooconfigure e registrare il dispositivo di hello</span><span class="sxs-lookup"><span data-stu-id="737d4-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="737d4-102">Accedere all'interfaccia di Windows PowerShell hello nella console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="737d4-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="737d4-103">Vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="737d4-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="737d4-104">**Essere procedure hello che toofollow esattamente o non sarà in grado di tooaccess console di hello.**</span><span class="sxs-lookup"><span data-stu-id="737d4-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="737d4-105">Nella sessione hello aperta, premere INVIO una volta tooget un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="737d4-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span> 
3. <span data-ttu-id="737d4-106">Sarà richiesto toochoose hello lingua che si desidera tooset per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="737d4-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="737d4-107">Specificare la lingua hello e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="737d4-107">Specify hello language, and then press Enter.</span></span> 
   
    ![StorSimple configurare e registrare il dispositivo 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="737d4-109">Nel menu di console seriale hello che viene visualizzato, scegliere toolog opzione 1 con accesso completo.</span><span class="sxs-lookup"><span data-stu-id="737d4-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span> 
   
    ![StorSimple registrare il dispositivo 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="737d4-111">Eseguire hello seguendo i passaggi tooconfigure hello minimo richiesto le impostazioni di rete per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="737d4-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="737d4-112">Questi passaggi di configurazione necessario toobe eseguiti nel controller attivo di hello del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="737d4-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="737d4-113">menu della console seriale Hello indica lo stato di controller hello in messaggio hello del banner.</span><span class="sxs-lookup"><span data-stu-id="737d4-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="737d4-114">Se non si sono connette controller attivo toohello, disconnettersi e quindi connettersi controller attivo toohello.</span><span class="sxs-lookup"><span data-stu-id="737d4-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="737d4-115">Al prompt dei comandi di hello, digitare la password.</span><span class="sxs-lookup"><span data-stu-id="737d4-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="737d4-116">password del dispositivo predefinito Hello è **Password1**.</span><span class="sxs-lookup"><span data-stu-id="737d4-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="737d4-117">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="737d4-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="737d4-118">Una procedura guidata verrà visualizzato toohelp configurare impostazioni di rete hello per dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="737d4-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="737d4-119">Fornire hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="737d4-119">Supply hello following information:</span></span> 
      
      * <span data-ttu-id="737d4-120">Indirizzo IP per l'interfaccia di rete DATA 0</span><span class="sxs-lookup"><span data-stu-id="737d4-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="737d4-121">Subnet mask</span><span class="sxs-lookup"><span data-stu-id="737d4-121">Subnet mask</span></span>
      * <span data-ttu-id="737d4-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="737d4-122">Gateway</span></span>
      * <span data-ttu-id="737d4-123">Indirizzo IP per il server DNS primario</span><span class="sxs-lookup"><span data-stu-id="737d4-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="737d4-124">Indirizzo IP per il server NTP primario</span><span class="sxs-lookup"><span data-stu-id="737d4-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="737d4-125">È possibile toowait per alcuni minuti per hello subnet mask e toobe impostazioni DNS applicato.</span><span class="sxs-lookup"><span data-stu-id="737d4-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="737d4-126">Facoltativamente, configurare il server proxy Web.</span><span class="sxs-lookup"><span data-stu-id="737d4-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="737d4-127">Sebbene la configurazione del proxy Web sia facoltativa, tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui.</span><span class="sxs-lookup"><span data-stu-id="737d4-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="737d4-128">Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="737d4-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="737d4-129">Premere Ctrl + C installazione guidata di tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="737d4-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="737d4-130">Installare gli aggiornamenti di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="737d4-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="737d4-131">Utilizzare hello seguente cmdlet tooset gli indirizzi IP in entrambi i controller hello:</span><span class="sxs-lookup"><span data-stu-id="737d4-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="737d4-132">Al prompt dei comandi di hello, eseguire `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="737d4-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="737d4-133">L’utente dovrebbe ricevere una notifica che sono disponibili aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="737d4-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="737d4-134">Eseguire `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="737d4-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="737d4-135">È possibile eseguire questo comando su qualsiasi nodo.</span><span class="sxs-lookup"><span data-stu-id="737d4-135">You can run this command on any node.</span></span> <span data-ttu-id="737d4-136">Aggiornamenti verranno applicati nel primo controller di hello, controller hello verrà eseguito il failover e quindi hello aggiornamenti verranno applicati in hello altro controller.</span><span class="sxs-lookup"><span data-stu-id="737d4-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="737d4-137">È possibile monitorare lo stato di avanzamento hello di hello aggiornamento eseguendo `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="737d4-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="737d4-138">Hello output di esempio seguente viene illustrato hello aggiornamento in corso.</span><span class="sxs-lookup"><span data-stu-id="737d4-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="737d4-139">Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato.</span><span class="sxs-lookup"><span data-stu-id="737d4-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="737d4-140">Potrebbe richiedere ore too11 hello di tooapply tutti hello gli aggiornamenti, inclusi gli aggiornamenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="737d4-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>

8. <span data-ttu-id="737d4-141">Dopo che tutti hello gli aggiornamenti sono installati correttamente, hello eseguire tooconfirm cmdlet seguenti che hello software aggiornamenti siano stati applicati correttamente:</span><span class="sxs-lookup"><span data-stu-id="737d4-141">After all hello updates are successfully installed, run hello following cmdlet tooconfirm that hello software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="737d4-142">È necessario visualizzare hello seguenti versioni:</span><span class="sxs-lookup"><span data-stu-id="737d4-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="737d4-143">HcsSoftwareVersion: 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="737d4-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="737d4-144">CisAgentVersion: 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="737d4-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="737d4-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="737d4-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="737d4-146">Esecuzione hello seguente tooconfirm cmdlet che l'aggiornamento del firmware hello è stato applicato correttamente:</span><span class="sxs-lookup"><span data-stu-id="737d4-146">Run hello following cmdlet tooconfirm that hello firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="737d4-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="737d4-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="737d4-148">deve essere stato firmware Hello **UpToDate**.</span><span class="sxs-lookup"><span data-stu-id="737d4-148">hello firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="737d4-149">Eseguire hello seguenti del portale di Microsoft Azure per enti pubblici toohello cmdlet toopoint hello dispositivi (in quanto punta toohello pubblica portale di Azure classico per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="737d4-149">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="737d4-150">Entrambi i controller verranno riavviati.</span><span class="sxs-lookup"><span data-stu-id="737d4-150">This will restart both controllers.</span></span> <span data-ttu-id="737d4-151">È consigliabile utilizzare due sessioni PuTTY toosimultaneously connettersi tooboth controller in modo da visualizzare quando viene riavviato ogni controller.</span><span class="sxs-lookup"><span data-stu-id="737d4-151">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="737d4-152">Verrà visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="737d4-152">You will see a confirmation message.</span></span> <span data-ttu-id="737d4-153">Accettare l'impostazione predefinita di hello (**Y**).</span><span class="sxs-lookup"><span data-stu-id="737d4-153">Accept hello default (**Y**).</span></span>
11. <span data-ttu-id="737d4-154">Eseguire hello dopo l'installazione di tooresume cmdlet:</span><span class="sxs-lookup"><span data-stu-id="737d4-154">Run hello following cmdlet tooresume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![Riprendere la configurazione guidata](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="737d4-156">Quando si ripristina il programma di installazione, la procedura guidata hello sarà versione hello Update 1 (che corrisponde a tooversion 17469).</span><span class="sxs-lookup"><span data-stu-id="737d4-156">When you resume setup, hello wizard will be hello Update 1 version (which corresponds tooversion 17469).</span></span> 
12. <span data-ttu-id="737d4-157">Accettare le impostazioni di rete hello.</span><span class="sxs-lookup"><span data-stu-id="737d4-157">Accept hello network settings.</span></span> <span data-ttu-id="737d4-158">Dopo aver accettato ciascuna impostazione, verrà visualizzato un messaggio di convalida.</span><span class="sxs-lookup"><span data-stu-id="737d4-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="737d4-159">Per motivi di sicurezza, password amministratore del dispositivo hello scade dopo hello prima sessione e sarà necessario toochange subito.</span><span class="sxs-lookup"><span data-stu-id="737d4-159">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="737d4-160">Quando richiesto, fornire una password di amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="737d4-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="737d4-161">Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="737d4-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="737d4-162">Hello password deve contenere tre dei seguenti hello: caratteri minuscoli, maiuscoli, numerici e speciali.</span><span class="sxs-lookup"><span data-stu-id="737d4-162">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple registrare il dispositivo 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="737d4-164">passaggio finale di Hello in Installazione guidata di hello registra il dispositivo con hello servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="737d4-164">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="737d4-165">A tale scopo, sarà necessario hello chiave di registrazione del servizio ottenuta nel [passaggio 2: chiave di registrazione del servizio Get hello](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="737d4-165">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="737d4-166">Dopo aver fornito la chiave di registrazione hello, potrebbe essere necessario toowait 2-3 minuti prima di hello dispositivo è registrato.</span><span class="sxs-lookup"><span data-stu-id="737d4-166">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="737d4-167">È possibile premere Ctrl + C in qualsiasi installazione guidata di tempo tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="737d4-167">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="737d4-168">Se è stato immesso tutte le impostazioni di rete hello (indirizzo IP per Subnet mask, Gateway e Data 0), le voci selezionate verranno mantenute.</span><span class="sxs-lookup"><span data-stu-id="737d4-168">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Registrazione di StorSimple in corso](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="737d4-170">Dopo aver registrato il dispositivo di hello, verrà visualizzata una chiave DEK del servizio.</span><span class="sxs-lookup"><span data-stu-id="737d4-170">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="737d4-171">Copiare questo codice e salvarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="737d4-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="737d4-172">**Questa chiave sarà necessaria con hello servizio registrazione tooregister chiave ulteriori dispositivi con hello servizio StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="737d4-172">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="737d4-173">Fare riferimento troppo[sicurezza in StorSimple](../articles/storsimple/storsimple-security.md) per ulteriori informazioni sulla chiave.</span><span class="sxs-lookup"><span data-stu-id="737d4-173">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="737d4-175">testo hello toocopy dalla finestra della console seriale hello, selezionare semplicemente il testo hello.</span><span class="sxs-lookup"><span data-stu-id="737d4-175">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="737d4-176">È quindi deve essere in grado di toopaste in Appunti hello o qualsiasi editor di testo.</span><span class="sxs-lookup"><span data-stu-id="737d4-176">You should then be able toopaste it in hello clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="737d4-177">NON utilizzare Ctrl + C toocopy hello chiave DEK del servizio.</span><span class="sxs-lookup"><span data-stu-id="737d4-177">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="737d4-178">Utilizzando Ctrl + C causerà tooexit hello l'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="737d4-178">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="737d4-179">Di conseguenza, non verrà modificata password amministratore del dispositivo hello e dispositivo hello diventerà una password predefinita toohello.</span><span class="sxs-lookup"><span data-stu-id="737d4-179">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
16. <span data-ttu-id="737d4-180">Console seriale hello di uscita.</span><span class="sxs-lookup"><span data-stu-id="737d4-180">Exit hello serial console.</span></span>
17. <span data-ttu-id="737d4-181">Restituire toohello portale di Azure per enti pubblici e completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="737d4-181">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="737d4-182">Fare doppio clic sui hello tooaccess di servizio StorSimple Manager **avvio rapido** pagina.</span><span class="sxs-lookup"><span data-stu-id="737d4-182">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="737d4-183">Fare clic su **Visualizza dispositivi connessi**.</span><span class="sxs-lookup"><span data-stu-id="737d4-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="737d4-184">In hello **dispositivi** pagina, verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="737d4-184">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="737d4-185">deve essere stato del dispositivo Hello **Online**.</span><span class="sxs-lookup"><span data-stu-id="737d4-185">hello device status should be **Online**.</span></span>
       
        ![Pagina Dispositivi StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="737d4-187">Se lo stato del dispositivo hello **Offline**, attendere un paio di minuti per hello online toocome di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="737d4-187">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span> 
       
        <span data-ttu-id="737d4-188">Se dispositivo hello sia ancora offline dopo alcuni minuti, quindi è necessario assicurarsi che la rete firewall è stata configurata come descritto in toomake [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="737d4-188">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="737d4-189">Verificare che la porta 9354 sia aperta per le comunicazioni in uscita come viene utilizzato dal bus di servizio hello per le comunicazioni di servizio nel dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="737d4-189">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager service-to-device communication.</span></span>

