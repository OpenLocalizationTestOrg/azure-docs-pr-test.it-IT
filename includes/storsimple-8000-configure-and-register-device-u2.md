<!--author=alkohli last changed: 01/18/2017-->


#### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="8db06-101">Per configurare e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="8db06-101">To configure and register the device</span></span>

1. <span data-ttu-id="8db06-102">Accedere all'interfaccia di Windows PowerShell sulla console seriale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8db06-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="8db06-103">Per istruzioni, vedere [Utilizzare PuTTY per connettersi alla console seriale del dispositivo](#use-putty-to-connect-to-the-device-serial-console) .</span><span class="sxs-lookup"><span data-stu-id="8db06-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="8db06-104">**Assicurarsi di seguire la procedura esattamente o non si sarà in grado di accedere alla console.**</span><span class="sxs-lookup"><span data-stu-id="8db06-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>

2. <span data-ttu-id="8db06-105">Nella sessione che viene aperta premere **INVIO** una volta per visualizzare un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8db06-105">In the session that opens up, press **Enter** one time to get a command prompt.</span></span>

3. <span data-ttu-id="8db06-106">Verrà richiesto di scegliere la lingua che si desidera impostare per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="8db06-107">Specificare la lingua e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="8db06-107">Specify the language, and then press **Enter**.</span></span>

4. <span data-ttu-id="8db06-108">Nel menu della console seriale che viene visualizzato scegliere l'opzione 1 per eseguire la **Connessione con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="8db06-108">In the serial console menu that is presented, choose option 1 to **log in with full access**.</span></span>
     <span data-ttu-id="8db06-109">Completare i passaggi da 5 a 12 per configurare le impostazioni di rete minime richieste per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-109">Complete steps 5-12 to configure the minimum required network settings for your device.</span></span> <span data-ttu-id="8db06-110">**È necessario eseguire questa procedura sul controller attivo del dispositivo.**</span><span class="sxs-lookup"><span data-stu-id="8db06-110">**These configuration steps need to be performed on the active controller of the device.**</span></span> <span data-ttu-id="8db06-111">Nel messaggio dell’intestazione del menu della console seriale è indicato lo stato del controller.</span><span class="sxs-lookup"><span data-stu-id="8db06-111">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="8db06-112">Se non si è connessi al controller attivo, disconnettersi e quindi connettersi al controller attivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-112">If you are not connected to the active controller, disconnect and then connect to the active controller.</span></span>

5. <span data-ttu-id="8db06-113">Al prompt dei comandi, digitare la password.</span><span class="sxs-lookup"><span data-stu-id="8db06-113">At the command prompt, type your password.</span></span> <span data-ttu-id="8db06-114">La password predefinita è **Password1**.</span><span class="sxs-lookup"><span data-stu-id="8db06-114">The default device password is **Password1**.</span></span>

6. <span data-ttu-id="8db06-115">Digitare il seguente comando: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="8db06-115">Type the following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="8db06-116">Verrà visualizzata una procedura guidata per configurare le impostazioni di rete per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-116">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="8db06-117">Fornire le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8db06-117">Supply the the following information:</span></span>
   
   * <span data-ttu-id="8db06-118">Indirizzo IP per l'interfaccia di rete DATA 0</span><span class="sxs-lookup"><span data-stu-id="8db06-118">IP address for the DATA 0 network interface</span></span>
   * <span data-ttu-id="8db06-119">Subnet mask</span><span class="sxs-lookup"><span data-stu-id="8db06-119">Subnet mask</span></span>
   * <span data-ttu-id="8db06-120">Gateway</span><span class="sxs-lookup"><span data-stu-id="8db06-120">Gateway</span></span>
   * <span data-ttu-id="8db06-121">Indirizzo IP per il server DNS primario</span><span class="sxs-lookup"><span data-stu-id="8db06-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="8db06-122">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="8db06-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Active
        ---------------------------------------------------------------

        Your device needs to be registered with the Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' to set up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like to configure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="8db06-123">Nell'output di esempio precedente il sistema convalida le impostazioni di rete dopo ogni passaggio del processo.</span><span class="sxs-lookup"><span data-stu-id="8db06-123">In the preceding sample output, you can see that the system is validating network settings after each step in the process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8db06-124">Potrebbe essere necessario attendere alcuni minuti affinché la subnet mask e le impostazioni DNS vengano applicate.</span><span class="sxs-lookup"><span data-stu-id="8db06-124">You may have to wait for a few minutes for the subnet mask and the DNS settings to be applied.</span></span> <span data-ttu-id="8db06-125">Se viene visualizzato un messaggio di errore "Controllare la connettività di rete a Data 0", controllare la connessione di rete fisica nell’interfaccia di rete DATA 0 del controllore attivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-125">If you get a "Check the network connectivity to Data 0" error message, check the physical network connection on the DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="8db06-126">(Facoltativo) configurare il server proxy Web.</span><span class="sxs-lookup"><span data-stu-id="8db06-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="8db06-127">Sebbene la configurazione del proxy Web sia facoltativa, **tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui**.</span><span class="sxs-lookup"><span data-stu-id="8db06-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="8db06-128">Per ulteriori informazioni, andare a [Configurare il proxy Web per il dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="8db06-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="8db06-129">Configurare un server NTP primario per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="8db06-130">I server NTP sono obbligatori, in quanto il dispositivo deve sincronizzare l'ora in modo da poter eseguire l’autenticazione con i provider del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="8db06-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="8db06-131">Assicurarsi che la rete consenta il traffico NTP dal data center a Internet.</span><span class="sxs-lookup"><span data-stu-id="8db06-131">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span> <span data-ttu-id="8db06-132">Se non è possibile, specificare un server NTP interno.</span><span class="sxs-lookup"><span data-stu-id="8db06-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="8db06-133">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="8db06-133">A sample output is shown below.</span></span>

    ```
        Would you like to configure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="8db06-134">Per motivi di sicurezza la password di amministratore del dispositivo scade dopo la prima sessione e sarà necessario modificarla ora.</span><span class="sxs-lookup"><span data-stu-id="8db06-134">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="8db06-135">Quando richiesto, fornire una password di amministratore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="8db06-136">Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="8db06-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="8db06-137">La password deve contenere tre dei seguenti tipi di caratteri: minuscole, maiuscole, numeri e caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="8db06-137">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        The device administrator password must be between 8 and 15 characters. The password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="8db06-138">Il passaggio finale dell'installazione guidata registra il dispositivo nel servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8db06-138">The final step in the setup wizard registers your device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="8db06-139">A tale scopo, è necessario il codice di registrazione del servizio ottenuto nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="8db06-139">For this, you will need the service registration key that you obtained in step 2.</span></span> <span data-ttu-id="8db06-140">Dopo aver fornito il codice di registrazione, potrebbe essere necessario attendere 2-3 minuti prima che il dispositivo venga registrato.</span><span class="sxs-lookup"><span data-stu-id="8db06-140">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="8db06-141">È possibile premere Ctrl + C in qualsiasi momento per uscire dall'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="8db06-141">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="8db06-142">Se sono state immesse tutte le impostazioni di rete (indirizzo IP per Data 0, Subnet mask e Gateway), le voci verranno conservate.</span><span class="sxs-lookup"><span data-stu-id="8db06-142">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="8db06-143">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="8db06-143">A sample output is shown below.</span></span>

    ```
        The service registration key is available in the StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="8db06-144">Dopo la registrazione del dispositivo, verrà visualizzato un codice di crittografia dei dati di servizio.</span><span class="sxs-lookup"><span data-stu-id="8db06-144">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="8db06-145">Copiare questo codice e salvarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="8db06-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="8db06-146">**Il codice verrà richiesto con il codice di registrazione del servizio allo scopo di registrare altri dispositivi nel servizio Gestione dispositivi StorSimple.**</span><span class="sxs-lookup"><span data-stu-id="8db06-146">**This key will be required with the service registration key to register additional devices with the StorSimple Device Manager service.**</span></span> <span data-ttu-id="8db06-147">Per ulteriori informazioni sul codice, consultare [Sicurezza di StorSimple](../articles/storsimple/storsimple-security.md) .</span><span class="sxs-lookup"><span data-stu-id="8db06-147">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="8db06-149">Per copiare il testo dalla finestra della console seriale, è sufficiente selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="8db06-149">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="8db06-150">È quindi possibile incollarlo negli Appunti o in qualsiasi editor di testo.</span><span class="sxs-lookup"><span data-stu-id="8db06-150">You should then be able to paste it in the clipboard or any text editor.</span></span> <span data-ttu-id="8db06-151">NON usare CTRL+C per copiare la chiave DEK del servizio.</span><span class="sxs-lookup"><span data-stu-id="8db06-151">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="8db06-152">Se si usa CTRL+C l'installazione guidata verrà chiusa.</span><span class="sxs-lookup"><span data-stu-id="8db06-152">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="8db06-153">Di conseguenza, la password di amministratore del dispositivo non verrà modificata e verrà ripristinata la password predefinita del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8db06-153">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    
13. <span data-ttu-id="8db06-154">Uscire dalla console seriale.</span><span class="sxs-lookup"><span data-stu-id="8db06-154">Exit the serial console.</span></span>
14. <span data-ttu-id="8db06-155">Tornare al portale di Azure e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8db06-155">Return to the Azure portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="8db06-156">Passare al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8db06-156">Go to your StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="8db06-157">Fare clic su **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8db06-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="8db06-158">Nell'elenco tabulare dei dispositivi controllare lo stato del dispositivo per verificare che sia connesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="8db06-158">In the tabular listing of devices, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="8db06-159">Lo stato del dispositivo deve essere **Pronto per la configurazione**.</span><span class="sxs-lookup"><span data-stu-id="8db06-159">The device status should be **Ready to set up**.</span></span>
       
        ![Pagina Dispositivi StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="8db06-161">Potrebbe essere necessario attendere un paio di minuti prima che lo stato del dispositivo passi a **Pronto per la configurazione**.</span><span class="sxs-lookup"><span data-stu-id="8db06-161">You may need to wait for a couple of minutes for the device status to change to **Ready to set up**.</span></span>
       
        <span data-ttu-id="8db06-162">Se il dispositivo non viene visualizzato in questo elenco, assicurarsi che la rete firewall sia stata configurata come descritto nei [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8db06-162">If the device does not show up in this list, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="8db06-163">Verificare che la porta 9354 sia aperta per le comunicazioni in uscita, perché viene usata dal bus di servizio per le comunicazioni da servizio a dispositivo di Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8db06-163">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Device Manager service-to-device communication.</span></span>

