<!--author=alkohli last changed: 01/18/2017-->


#### <a name="to-configure-and-register-the-device"></a>Per configurare e registrare il dispositivo

1. Accedere all'interfaccia di Windows PowerShell sulla console seriale del dispositivo StorSimple. Per istruzioni, vedere [Utilizzare PuTTY per connettersi alla console seriale del dispositivo](#use-putty-to-connect-to-the-device-serial-console) . **Assicurarsi di seguire la procedura esattamente o non si sarà in grado di accedere alla console.**

2. Nella sessione che viene aperta premere **INVIO** una volta per visualizzare un prompt dei comandi.

3. Verrà richiesto di scegliere la lingua che si desidera impostare per il dispositivo. Specificare la lingua e quindi premere **INVIO**.

4. Nel menu della console seriale che viene visualizzato scegliere l'opzione 1 per eseguire la **Connessione con accesso completo**.
     Completare i passaggi da 5 a 12 per configurare le impostazioni di rete minime richieste per il dispositivo. **È necessario eseguire questa procedura sul controller attivo del dispositivo.** Nel messaggio dell’intestazione del menu della console seriale è indicato lo stato del controller. Se non si è connessi al controller attivo, disconnettersi e quindi connettersi al controller attivo.

5. Al prompt dei comandi, digitare la password. La password predefinita è **Password1**.

6. Digitare il seguente comando: `Invoke-HcsSetupWizard`.

7. Verrà visualizzata una procedura guidata per configurare le impostazioni di rete per il dispositivo. Fornire le informazioni seguenti:
   
   * Indirizzo IP per l'interfaccia di rete DATA 0
   * Subnet mask
   * Gateway
   * Indirizzo IP per il server DNS primario

   Di seguito è riportato un output di esempio.

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
    Nell'output di esempio precedente il sistema convalida le impostazioni di rete dopo ogni passaggio del processo.

     > [!NOTE]
     > Potrebbe essere necessario attendere alcuni minuti affinché la subnet mask e le impostazioni DNS vengano applicate. Se viene visualizzato un messaggio di errore "Controllare la connettività di rete a Data 0", controllare la connessione di rete fisica nell’interfaccia di rete DATA 0 del controllore attivo.

8. (Facoltativo) configurare il server proxy Web. Sebbene la configurazione del proxy Web sia facoltativa, **tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui**. Per ulteriori informazioni, andare a [Configurare il proxy Web per il dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Configurare un server NTP primario per il dispositivo. I server NTP sono obbligatori, in quanto il dispositivo deve sincronizzare l'ora in modo da poter eseguire l’autenticazione con i provider del servizio cloud. Assicurarsi che la rete consenta il traffico NTP dal data center a Internet. Se non è possibile, specificare un server NTP interno.

    Di seguito è riportato un output di esempio.

    ```
        Would you like to configure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Per motivi di sicurezza la password di amministratore del dispositivo scade dopo la prima sessione e sarà necessario modificarla ora. Quando richiesto, fornire una password di amministratore del dispositivo. Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri. La password deve contenere tre dei seguenti tipi di caratteri: minuscole, maiuscole, numeri e caratteri speciali.

    ```
        The device administrator password must be between 8 and 15 characters. The password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. Il passaggio finale dell'installazione guidata registra il dispositivo nel servizio Gestione dispositivi StorSimple. A tale scopo, è necessario il codice di registrazione del servizio ottenuto nel passaggio 2. Dopo aver fornito il codice di registrazione, potrebbe essere necessario attendere 2-3 minuti prima che il dispositivo venga registrato.
    
    > [!NOTE]
    > È possibile premere Ctrl + C in qualsiasi momento per uscire dall'installazione guidata. Se sono state immesse tutte le impostazioni di rete (indirizzo IP per Data 0, Subnet mask e Gateway), le voci verranno conservate.
    
    Di seguito è riportato un output di esempio.

    ```
        The service registration key is available in the StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Dopo la registrazione del dispositivo, verrà visualizzato un codice di crittografia dei dati di servizio. Copiare questo codice e salvarlo in un luogo sicuro. **Il codice verrà richiesto con il codice di registrazione del servizio allo scopo di registrare altri dispositivi nel servizio Gestione dispositivi StorSimple.** Per ulteriori informazioni sul codice, consultare [Sicurezza di StorSimple](../articles/storsimple/storsimple-security.md) .
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > Per copiare il testo dalla finestra della console seriale, è sufficiente selezionarlo. È quindi possibile incollarlo negli Appunti o in qualsiasi editor di testo. NON usare CTRL+C per copiare la chiave DEK del servizio. Se si usa CTRL+C l'installazione guidata verrà chiusa. Di conseguenza, la password di amministratore del dispositivo non verrà modificata e verrà ripristinata la password predefinita del dispositivo.
    
13. Uscire dalla console seriale.
14. Tornare al portale di Azure e seguire questa procedura:
    
    1. Passare al servizio Gestione dispositivi StorSimple.
    2. Fare clic su **Dispositivi**.
    3. Nell'elenco tabulare dei dispositivi controllare lo stato del dispositivo per verificare che sia connesso al servizio. Lo stato del dispositivo deve essere **Pronto per la configurazione**.
       
        ![Pagina Dispositivi StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Potrebbe essere necessario attendere un paio di minuti prima che lo stato del dispositivo passi a **Pronto per la configurazione**.
       
        Se il dispositivo non viene visualizzato in questo elenco, assicurarsi che la rete firewall sia stata configurata come descritto nei [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md). Verificare che la porta 9354 sia aperta per le comunicazioni in uscita, perché viene usata dal bus di servizio per le comunicazioni da servizio a dispositivo di Gestione dispositivi StorSimple.

