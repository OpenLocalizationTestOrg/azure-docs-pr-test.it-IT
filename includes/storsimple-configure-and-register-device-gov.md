<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure e registrare il dispositivo di hello
1. Accedere all'interfaccia di Windows PowerShell hello nella console seriale del dispositivo StorSimple. Vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) per le istruzioni. **Essere procedure hello che toofollow esattamente o non sarà in grado di tooaccess console di hello.**
2. Nella sessione hello aperta, premere INVIO una volta tooget un prompt dei comandi. 
3. Sarà richiesto toochoose hello lingua che si desidera tooset per il dispositivo. Specificare la lingua hello e quindi premere INVIO. 
   
    ![StorSimple configurare e registrare il dispositivo 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. Nel menu di console seriale hello che viene visualizzato, scegliere toolog opzione 1 con accesso completo. 
   
    ![StorSimple registrare il dispositivo 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. Eseguire hello seguendo i passaggi tooconfigure hello minimo richiesto le impostazioni di rete per il dispositivo.
   
   > [!IMPORTANT]
   > Questi passaggi di configurazione necessario toobe eseguiti nel controller attivo di hello del dispositivo hello. menu della console seriale Hello indica lo stato di controller hello in messaggio hello del banner. Se non si sono connette controller attivo toohello, disconnettersi e quindi connettersi controller attivo toohello.
   > 
   > 
   
   1. Al prompt dei comandi di hello, digitare la password. password del dispositivo predefinito Hello è **Password1**.
   2. Digitare hello comando seguente:
      
        `Invoke-HcsSetupWizard`
   3. Una procedura guidata verrà visualizzato toohelp configurare impostazioni di rete hello per dispositivo hello. Fornire hello le seguenti informazioni: 
      
      * Indirizzo IP per l'interfaccia di rete DATA 0
      * Subnet mask
      * Gateway
      * Indirizzo IP per il server DNS primario
      * Indirizzo IP per il server NTP primario
      
      > [!NOTE]
      > È possibile toowait per alcuni minuti per hello subnet mask e toobe impostazioni DNS applicato. 
      > 
      > 
   4. Facoltativamente, configurare il server proxy Web.
      
      > [!IMPORTANT]
      > Sebbene la configurazione del proxy Web sia facoltativa, tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui. Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md). 
      > 
      > 
6. Premere Ctrl + C installazione guidata di tooexit hello.
7. Installare gli aggiornamenti di hello come indicato di seguito:
   
   1. Utilizzare hello seguente cmdlet tooset gli indirizzi IP in entrambi i controller hello:
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. Al prompt dei comandi di hello, eseguire `Get-HcsUpdateAvailability`. L’utente dovrebbe ricevere una notifica che sono disponibili aggiornamenti.
   3. Eseguire `Start-HcsUpdate`. È possibile eseguire questo comando su qualsiasi nodo. Aggiornamenti verranno applicati nel primo controller di hello, controller hello verrà eseguito il failover e quindi hello aggiornamenti verranno applicati in hello altro controller.
      
      È possibile monitorare lo stato di avanzamento hello di hello aggiornamento eseguendo `Get-HcsUpdateStatus`.    
      
      Hello output di esempio seguente viene illustrato hello aggiornamento in corso.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato.
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      Potrebbe richiedere ore too11 hello di tooapply tutti hello gli aggiornamenti, inclusi gli aggiornamenti di Windows.

8. Dopo che tutti hello gli aggiornamenti sono installati correttamente, hello eseguire tooconfirm cmdlet seguenti che hello software aggiornamenti siano stati applicati correttamente:
   
     `Get-HcsSystem`
   
    È necessario visualizzare hello seguenti versioni:
   
   * HcsSoftwareVersion: 6.3.9600.17491
   * CisAgentVersion: 1.0.9037.0
   * MdsAgentVersion: 26.0.4696.1433
9. Esecuzione hello seguente tooconfirm cmdlet che l'aggiornamento del firmware hello è stato applicato correttamente:
   
    `Start-HcsFirmwareCheck`.
   
     deve essere stato firmware Hello **UpToDate**.
10. Eseguire hello seguenti del portale di Microsoft Azure per enti pubblici toohello cmdlet toopoint hello dispositivi (in quanto punta toohello pubblica portale di Azure classico per impostazione predefinita). Entrambi i controller verranno riavviati. È consigliabile utilizzare due sessioni PuTTY toosimultaneously connettersi tooboth controller in modo da visualizzare quando viene riavviato ogni controller.
    
     `Set-CloudPlatform -AzureGovt_US`
    
    Verrà visualizzato un messaggio di conferma. Accettare l'impostazione predefinita di hello (**Y**).
11. Eseguire hello dopo l'installazione di tooresume cmdlet:
    
     `Invoke-HcsSetupWizard`
    
     ![Riprendere la configurazione guidata](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    Quando si ripristina il programma di installazione, la procedura guidata hello sarà versione hello Update 1 (che corrisponde a tooversion 17469). 
12. Accettare le impostazioni di rete hello. Dopo aver accettato ciascuna impostazione, verrà visualizzato un messaggio di convalida.
13. Per motivi di sicurezza, password amministratore del dispositivo hello scade dopo hello prima sessione e sarà necessario toochange subito. Quando richiesto, fornire una password di amministratore del dispositivo. Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri. Hello password deve contenere tre dei seguenti hello: caratteri minuscoli, maiuscoli, numerici e speciali.
    
    <br/>![StorSimple registrare il dispositivo 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. passaggio finale di Hello in Installazione guidata di hello registra il dispositivo con hello servizio StorSimple Manager. A tale scopo, sarà necessario hello chiave di registrazione del servizio ottenuta nel [passaggio 2: chiave di registrazione del servizio Get hello](#step-2-get-the-service-registration-key). Dopo aver fornito la chiave di registrazione hello, potrebbe essere necessario toowait 2-3 minuti prima di hello dispositivo è registrato.
    
    > [!NOTE]
    > È possibile premere Ctrl + C in qualsiasi installazione guidata di tempo tooexit hello. Se è stato immesso tutte le impostazioni di rete hello (indirizzo IP per Subnet mask, Gateway e Data 0), le voci selezionate verranno mantenute.
    > 
    > 
    
    ![Registrazione di StorSimple in corso](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. Dopo aver registrato il dispositivo di hello, verrà visualizzata una chiave DEK del servizio. Copiare questo codice e salvarlo in un luogo sicuro. **Questa chiave sarà necessaria con hello servizio registrazione tooregister chiave ulteriori dispositivi con hello servizio StorSimple Manager.** Fare riferimento troppo[sicurezza in StorSimple](../articles/storsimple/storsimple-security.md) per ulteriori informazioni sulla chiave.
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > testo hello toocopy dalla finestra della console seriale hello, selezionare semplicemente il testo hello. È quindi deve essere in grado di toopaste in Appunti hello o qualsiasi editor di testo. 
    > 
    > NON utilizzare Ctrl + C toocopy hello chiave DEK del servizio. Utilizzando Ctrl + C causerà tooexit hello l'installazione guidata. Di conseguenza, non verrà modificata password amministratore del dispositivo hello e dispositivo hello diventerà una password predefinita toohello.
    > 
    > 
16. Console seriale hello di uscita.
17. Restituire toohello portale di Azure per enti pubblici e completare hello alla procedura seguente:
    
    1. Fare doppio clic sui hello tooaccess di servizio StorSimple Manager **avvio rapido** pagina.
    2. Fare clic su **Visualizza dispositivi connessi**.
    3. In hello **dispositivi** pagina, verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello. deve essere stato del dispositivo Hello **Online**.
       
        ![Pagina Dispositivi StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        Se lo stato del dispositivo hello **Offline**, attendere un paio di minuti per hello online toocome di dispositivo. 
       
        Se dispositivo hello sia ancora offline dopo alcuni minuti, quindi è necessario assicurarsi che la rete firewall è stata configurata come descritto in toomake [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Verificare che la porta 9354 sia aperta per le comunicazioni in uscita come viene utilizzato dal bus di servizio hello per le comunicazioni di servizio nel dispositivo StorSimple Manager.

