<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure e registrare il dispositivo di hello
1. Accedere all'interfaccia di Windows PowerShell hello nella console seriale del dispositivo StorSimple. Vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) per le istruzioni. **Essere procedure hello che toofollow esattamente o non sarà in grado di tooaccess console di hello.**
2. Nella sessione hello aperta, premere INVIO una volta tooget un prompt dei comandi. 
3. Sarà richiesto toochoose hello lingua che si desidera tooset per il dispositivo. Specificare la lingua hello e quindi premere INVIO. 
   
    ![StorSimple configurare e registrare il dispositivo 1](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. Nel menu di console seriale hello che viene visualizzato, scegliere toolog opzione 1 con accesso completo. 
   
    ![StorSimple registrare il dispositivo 2](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Completare i passaggi 5-12 tooconfigure hello minimo richiesto le impostazioni di rete per il dispositivo. **Questi passaggi di configurazione necessario toobe eseguiti nel controller attivo di hello del dispositivo hello.** menu della console seriale Hello indica lo stato di controller hello in messaggio hello del banner. Se non si è connessi toohello controller attivo, disconnettersi e quindi connettersi controller attivo toohello.
5. Al prompt dei comandi di hello, digitare la password. password del dispositivo predefinito Hello è **Password1**.
6. Hello tipo comando seguente: `Invoke-HcsSetupWizard`. 
7. Una procedura guidata verrà visualizzato toohelp configurare impostazioni di rete hello per dispositivo hello. Fornire hello hello le seguenti informazioni: 
   
   * Indirizzo IP per l'interfaccia di rete 0 hello dati
   * Subnet mask
   * Gateway
   * Indirizzo IP per il server DNS primario
     
        Si noti che il sistema hello convalida le impostazioni di rete dopo ogni passaggio nel processo di hello.
     
     > [!NOTE]
     > È possibile toowait per alcuni minuti per hello subnet mask e hello DNS impostazioni toobe applicato. Se viene visualizzato un messaggio di errore "Controllo hello rete connettività tooData 0", controllare connessione di rete fisica hello sull'interfaccia di rete 0 dati hello del controller attivo.
     > 
     > 
8. (Facoltativo) configurare il server proxy Web. Sebbene la configurazione del proxy Web sia facoltativa, **tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui**. Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Configurare un server NTP primario per il dispositivo. I server NTP sono obbligatori, in quanto il dispositivo deve sincronizzare l'ora in modo da poter eseguire l’autenticazione con i provider del servizio cloud. Verificare che la rete consenta toopass traffico NTP dal toohello datacenter Internet. Se non è possibile, specificare un server NTP interno. 
10. Per motivi di sicurezza, password amministratore del dispositivo hello scade dopo hello prima sessione e sarà necessario toochange subito. Quando richiesto, fornire una password di amministratore del dispositivo. Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri. Hello password deve contenere tre dei seguenti hello: caratteri minuscoli, maiuscoli, numerici e speciali.
    
    <br/>![StorSimple registrare il dispositivo 5](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. passaggio finale di Hello in Installazione guidata di hello registra il dispositivo con hello servizio StorSimple Manager. A tale scopo, è necessario hello registrazione chiave del servizio ottenuta nel passaggio 2. Dopo aver fornito la chiave di registrazione hello, potrebbe essere necessario toowait 2-3 minuti prima di hello dispositivo è registrato.
    
    > [!NOTE]
    > È possibile premere Ctrl + C in qualsiasi installazione guidata di tempo tooexit hello. Se è stato immesso tutte le impostazioni di rete hello (indirizzo IP per Subnet mask, Gateway e Data 0), le voci selezionate verranno mantenute.
    > 
    > 
    
    ![StorSimple registrare il dispositivo 6](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Dopo aver registrato il dispositivo di hello, verrà visualizzata una chiave DEK del servizio. Copiare questo codice e salvarlo in un luogo sicuro. **Questa chiave sarà necessaria con hello servizio registrazione tooregister chiave ulteriori dispositivi con hello servizio StorSimple Manager.** Fare riferimento troppo[sicurezza in StorSimple](../articles/storsimple/storsimple-security.md) per ulteriori informazioni sulla chiave.
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > testo hello toocopy dalla finestra della console seriale hello, selezionare semplicemente il testo hello. È quindi deve essere in grado di toopaste in Appunti hello o qualsiasi editor di testo. NON utilizzare Ctrl + C toocopy hello chiave DEK del servizio. Utilizzando Ctrl + C causerà tooexit hello l'installazione guidata. Di conseguenza, non verrà modificata password amministratore del dispositivo hello e dispositivo hello diventerà una password predefinita toohello.
    > 
    > 
13. Console seriale hello di uscita.
14. Restituire toohello portale di Azure classico e completare hello alla procedura seguente:
    
    1. Fare doppio clic sui hello tooaccess di servizio StorSimple Manager **avvio rapido** pagina.
    2. Fare clic su **Visualizza dispositivi connessi**.
    3. In hello **dispositivi** pagina, verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello. deve essere stato del dispositivo Hello **Online**.
       
        ![Pagina Dispositivi StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Se lo stato del dispositivo hello **Offline**, attendere un paio di minuti per hello online toocome di dispositivo. 
       
        Se dispositivo hello sia ancora offline dopo alcuni minuti, quindi è necessario assicurarsi che la rete firewall è stata configurata come descritto in toomake [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Verificare che la porta 9354 sia aperta per le comunicazioni in uscita come viene utilizzato dal bus di servizio hello per le comunicazioni di StorSimple Manager servizio al dispositivo.

