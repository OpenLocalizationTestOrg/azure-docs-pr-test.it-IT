<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="9c654-101">tooconfigure e registrare il dispositivo di hello</span><span class="sxs-lookup"><span data-stu-id="9c654-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="9c654-102">Accedere all'interfaccia di Windows PowerShell hello nella console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9c654-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="9c654-103">Vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="9c654-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="9c654-104">**Essere procedure hello che toofollow esattamente o non sarà in grado di tooaccess console di hello.**</span><span class="sxs-lookup"><span data-stu-id="9c654-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="9c654-105">Nella sessione hello aperta, premere **invio** una volta tooget un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9c654-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="9c654-106">Sarà richiesto toochoose hello lingua che si desidera tooset per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9c654-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="9c654-107">Specificare la lingua hello e quindi premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="9c654-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="9c654-108">Nel menu console seriale hello visualizzato, scegliere l'opzione 1 troppo**Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="9c654-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="9c654-109">Completare i passaggi 5-12 tooconfigure hello minimo richiesto le impostazioni di rete per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9c654-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="9c654-110">**Questi passaggi di configurazione necessario toobe eseguiti nel controller attivo di hello del dispositivo hello.**</span><span class="sxs-lookup"><span data-stu-id="9c654-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="9c654-111">menu della console seriale Hello indica lo stato di controller hello in messaggio hello del banner.</span><span class="sxs-lookup"><span data-stu-id="9c654-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="9c654-112">Se non si è connessi toohello controller attivo, disconnettersi e quindi connettersi controller attivo toohello.</span><span class="sxs-lookup"><span data-stu-id="9c654-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="9c654-113">Al prompt dei comandi di hello, digitare la password.</span><span class="sxs-lookup"><span data-stu-id="9c654-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="9c654-114">password del dispositivo predefinito Hello è **Password1**.</span><span class="sxs-lookup"><span data-stu-id="9c654-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="9c654-115">Hello tipo comando seguente: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="9c654-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="9c654-116">Una procedura guidata verrà visualizzato toohelp configurare impostazioni di rete hello per dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9c654-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="9c654-117">Fornire hello hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="9c654-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="9c654-118">Indirizzo IP per l'interfaccia di rete 0 hello dati</span><span class="sxs-lookup"><span data-stu-id="9c654-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="9c654-119">Subnet mask</span><span class="sxs-lookup"><span data-stu-id="9c654-119">Subnet mask</span></span>
   * <span data-ttu-id="9c654-120">Gateway</span><span class="sxs-lookup"><span data-stu-id="9c654-120">Gateway</span></span>
   * <span data-ttu-id="9c654-121">Indirizzo IP per il server DNS primario</span><span class="sxs-lookup"><span data-stu-id="9c654-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="9c654-122">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="9c654-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="9c654-123">Nel precedente esempio di output di hello, si noterà che il sistema hello convalida le impostazioni di rete dopo ogni passaggio nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="9c654-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9c654-124">È possibile toowait per alcuni minuti per hello subnet mask e hello DNS impostazioni toobe applicato.</span><span class="sxs-lookup"><span data-stu-id="9c654-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="9c654-125">Se viene visualizzato un messaggio di errore "Controllo hello rete connettività tooData 0", controllare connessione di rete fisica hello sull'interfaccia di rete 0 dati hello del controller attivo.</span><span class="sxs-lookup"><span data-stu-id="9c654-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="9c654-126">(Facoltativo) configurare il server proxy Web.</span><span class="sxs-lookup"><span data-stu-id="9c654-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="9c654-127">Sebbene la configurazione del proxy Web sia facoltativa, **tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui**.</span><span class="sxs-lookup"><span data-stu-id="9c654-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="9c654-128">Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="9c654-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="9c654-129">Configurare un server NTP primario per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9c654-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="9c654-130">I server NTP sono obbligatori, in quanto il dispositivo deve sincronizzare l'ora in modo da poter eseguire l’autenticazione con i provider del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9c654-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="9c654-131">Verificare che la rete consenta toopass traffico NTP dal toohello datacenter Internet.</span><span class="sxs-lookup"><span data-stu-id="9c654-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="9c654-132">Se non è possibile, specificare un server NTP interno.</span><span class="sxs-lookup"><span data-stu-id="9c654-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="9c654-133">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="9c654-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="9c654-134">Per motivi di sicurezza, password amministratore del dispositivo hello scade dopo hello prima sessione e sarà necessario toochange subito.</span><span class="sxs-lookup"><span data-stu-id="9c654-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="9c654-135">Quando richiesto, fornire una password di amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9c654-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="9c654-136">Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9c654-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="9c654-137">Hello password deve contenere tre dei seguenti hello: caratteri minuscoli, maiuscoli, numerici e speciali.</span><span class="sxs-lookup"><span data-stu-id="9c654-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="9c654-138">passaggio finale di Hello in Installazione guidata di hello registra il dispositivo con il servizio di gestione di dispositivi StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="9c654-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="9c654-139">A tale scopo, è necessario hello registrazione chiave del servizio ottenuta nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="9c654-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="9c654-140">Dopo aver fornito la chiave di registrazione hello, potrebbe essere necessario toowait 2-3 minuti prima di hello dispositivo è registrato.</span><span class="sxs-lookup"><span data-stu-id="9c654-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9c654-141">È possibile premere Ctrl + C in qualsiasi installazione guidata di tempo tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="9c654-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="9c654-142">Se è stato immesso tutte le impostazioni di rete hello (indirizzo IP per Subnet mask, Gateway e Data 0), le voci selezionate verranno mantenute.</span><span class="sxs-lookup"><span data-stu-id="9c654-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="9c654-143">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="9c654-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="9c654-144">Dopo aver registrato il dispositivo di hello, verrà visualizzata una chiave DEK del servizio.</span><span class="sxs-lookup"><span data-stu-id="9c654-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="9c654-145">Copiare questo codice e salvarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="9c654-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="9c654-146">**Questa chiave sarà necessaria con hello registrazione tooregister chiave ulteriori dispositivi del servizio con il servizio di gestione di dispositivi StorSimple hello.**</span><span class="sxs-lookup"><span data-stu-id="9c654-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="9c654-147">Fare riferimento troppo[sicurezza in StorSimple](../articles/storsimple/storsimple-security.md) per ulteriori informazioni sulla chiave.</span><span class="sxs-lookup"><span data-stu-id="9c654-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="9c654-149">testo hello toocopy dalla finestra della console seriale hello, selezionare semplicemente il testo hello.</span><span class="sxs-lookup"><span data-stu-id="9c654-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="9c654-150">È quindi deve essere in grado di toopaste in Appunti hello o qualsiasi editor di testo.</span><span class="sxs-lookup"><span data-stu-id="9c654-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="9c654-151">NON utilizzare Ctrl + C toocopy hello chiave DEK del servizio.</span><span class="sxs-lookup"><span data-stu-id="9c654-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="9c654-152">Utilizzando Ctrl + C causerà tooexit hello l'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="9c654-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="9c654-153">Di conseguenza, non verrà modificata password amministratore del dispositivo hello e dispositivo hello diventerà una password predefinita toohello.</span><span class="sxs-lookup"><span data-stu-id="9c654-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="9c654-154">Console seriale hello di uscita.</span><span class="sxs-lookup"><span data-stu-id="9c654-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="9c654-155">Restituire toohello portale di Azure e completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9c654-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="9c654-156">Passare il servizio di gestione di dispositivi StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="9c654-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="9c654-157">Fare clic su **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="9c654-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="9c654-158">In hello tabulare elenco di dispositivi, verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="9c654-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="9c654-159">deve essere stato del dispositivo Hello **pronto tooset backup**.</span><span class="sxs-lookup"><span data-stu-id="9c654-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Pagina Dispositivi StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="9c654-161">Per un paio di minuti per hello dispositivo stato toochange potrebbe essere troppo toowait**pronto tooset backup**.</span><span class="sxs-lookup"><span data-stu-id="9c654-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="9c654-162">Se dispositivo hello non viene visualizzato nell'elenco, quindi è necessario assicurarsi che la rete firewall è stata configurata come descritto in toomake [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9c654-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="9c654-163">Verificare che la porta 9354 sia aperta per le comunicazioni in uscita come viene utilizzato dal bus di servizio hello per le comunicazioni di servizio al dispositivo dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="9c654-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

