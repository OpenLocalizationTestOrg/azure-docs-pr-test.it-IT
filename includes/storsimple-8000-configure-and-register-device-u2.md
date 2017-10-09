<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure e registrare il dispositivo di hello

1. Accedere all'interfaccia di Windows PowerShell hello nella console seriale del dispositivo StorSimple. Vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) per le istruzioni. **Essere procedure hello che toofollow esattamente o non sarà in grado di tooaccess console di hello.**

2. Nella sessione hello aperta, premere **invio** una volta tooget un prompt dei comandi.

3. Sarà richiesto toochoose hello lingua che si desidera tooset per il dispositivo. Specificare la lingua hello e quindi premere **invio**.

4. Nel menu console seriale hello visualizzato, scegliere l'opzione 1 troppo**Accedi con accesso completo**.
     Completare i passaggi 5-12 tooconfigure hello minimo richiesto le impostazioni di rete per il dispositivo. **Questi passaggi di configurazione necessario toobe eseguiti nel controller attivo di hello del dispositivo hello.** menu della console seriale Hello indica lo stato di controller hello in messaggio hello del banner. Se non si è connessi toohello controller attivo, disconnettersi e quindi connettersi controller attivo toohello.

5. Al prompt dei comandi di hello, digitare la password. password del dispositivo predefinito Hello è **Password1**.

6. Hello tipo comando seguente: `Invoke-HcsSetupWizard`.

7. Una procedura guidata verrà visualizzato toohelp configurare impostazioni di rete hello per dispositivo hello. Fornire hello hello le seguenti informazioni:
   
   * Indirizzo IP per l'interfaccia di rete 0 hello dati
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
    Nel precedente esempio di output di hello, si noterà che il sistema hello convalida le impostazioni di rete dopo ogni passaggio nel processo di hello.

     > [!NOTE]
     > È possibile toowait per alcuni minuti per hello subnet mask e hello DNS impostazioni toobe applicato. Se viene visualizzato un messaggio di errore "Controllo hello rete connettività tooData 0", controllare connessione di rete fisica hello sull'interfaccia di rete 0 dati hello del controller attivo.

8. (Facoltativo) configurare il server proxy Web. Sebbene la configurazione del proxy Web sia facoltativa, **tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui**. Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Configurare un server NTP primario per il dispositivo. I server NTP sono obbligatori, in quanto il dispositivo deve sincronizzare l'ora in modo da poter eseguire l’autenticazione con i provider del servizio cloud. Verificare che la rete consenta toopass traffico NTP dal toohello datacenter Internet. Se non è possibile, specificare un server NTP interno.

    Di seguito è riportato un output di esempio.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Per motivi di sicurezza, password amministratore del dispositivo hello scade dopo hello prima sessione e sarà necessario toochange subito. Quando richiesto, fornire una password di amministratore del dispositivo. Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri. Hello password deve contenere tre dei seguenti hello: caratteri minuscoli, maiuscoli, numerici e speciali.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. passaggio finale di Hello in Installazione guidata di hello registra il dispositivo con il servizio di gestione di dispositivi StorSimple hello. A tale scopo, è necessario hello registrazione chiave del servizio ottenuta nel passaggio 2. Dopo aver fornito la chiave di registrazione hello, potrebbe essere necessario toowait 2-3 minuti prima di hello dispositivo è registrato.
    
    > [!NOTE]
    > È possibile premere Ctrl + C in qualsiasi installazione guidata di tempo tooexit hello. Se è stato immesso tutte le impostazioni di rete hello (indirizzo IP per Subnet mask, Gateway e Data 0), le voci selezionate verranno mantenute.
    
    Di seguito è riportato un output di esempio.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Dopo aver registrato il dispositivo di hello, verrà visualizzata una chiave DEK del servizio. Copiare questo codice e salvarlo in un luogo sicuro. **Questa chiave sarà necessaria con hello registrazione tooregister chiave ulteriori dispositivi del servizio con il servizio di gestione di dispositivi StorSimple hello.** Fare riferimento troppo[sicurezza in StorSimple](../articles/storsimple/storsimple-security.md) per ulteriori informazioni sulla chiave.
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > testo hello toocopy dalla finestra della console seriale hello, selezionare semplicemente il testo hello. È quindi deve essere in grado di toopaste in Appunti hello o qualsiasi editor di testo. NON utilizzare Ctrl + C toocopy hello chiave DEK del servizio. Utilizzando Ctrl + C causerà tooexit hello l'installazione guidata. Di conseguenza, non verrà modificata password amministratore del dispositivo hello e dispositivo hello diventerà una password predefinita toohello.
    
13. Console seriale hello di uscita.
14. Restituire toohello portale di Azure e completare hello alla procedura seguente:
    
    1. Passare il servizio di gestione di dispositivi StorSimple tooyour.
    2. Fare clic su **Dispositivi**.
    3. In hello tabulare elenco di dispositivi, verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello. deve essere stato del dispositivo Hello **pronto tooset backup**.
       
        ![Pagina Dispositivi StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Per un paio di minuti per hello dispositivo stato toochange potrebbe essere troppo toowait**pronto tooset backup**.
       
        Se dispositivo hello non viene visualizzato nell'elenco, quindi è necessario assicurarsi che la rete firewall è stata configurata come descritto in toomake [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md). Verificare che la porta 9354 sia aperta per le comunicazioni in uscita come viene utilizzato dal bus di servizio hello per le comunicazioni di servizio al dispositivo dispositivo StorSimple Manager.

