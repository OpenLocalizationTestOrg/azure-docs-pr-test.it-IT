<!--author=SharS last changed: 06/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure e registrare il dispositivo di hello
1. Accedere all'interfaccia di Windows PowerShell hello nella console seriale del dispositivo StorSimple. Vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) per le istruzioni. **Essere procedure hello che toofollow esattamente o non sarà in grado di tooaccess console di hello.**
2. Nella sessione hello aperta, premere **invio** una volta tooget un prompt dei comandi.
3. Sarà richiesto toochoose hello lingua che si desidera tooset per il dispositivo. Specificare la lingua hello e quindi premere **invio**.
   
    ![StorSimple configurare e registrare il dispositivo 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. Nel menu di console seriale hello che viene visualizzato, scegliere toolog opzione 1 con accesso completo.
   
    ![StorSimple registrare il dispositivo 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Eseguire hello seguendo i passaggi tooconfigure hello minimo richiesto le impostazioni di rete per il dispositivo.
   
   > [!IMPORTANT]
   > Questi passaggi di configurazione necessario toobe eseguiti nel controller attivo di hello del dispositivo hello. menu della console seriale Hello indica lo stato di controller hello in messaggio hello del banner. Se non si sono connette controller attivo toohello, disconnettersi e quindi connettersi controller attivo toohello.
   
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
    
   4. Facoltativamente, configurare il server proxy Web.
      
      > [!IMPORTANT]
      > Sebbene la configurazione del proxy Web sia facoltativa, tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui. Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md).
     
6. Premere Ctrl + C installazione guidata di tooexit hello.
8. Eseguire hello seguenti del portale di Microsoft Azure per enti pubblici toohello cmdlet toopoint hello dispositivi (in quanto punta toohello pubblica portale di Azure classico per impostazione predefinita). Entrambi i controller verranno riavviati. È consigliabile utilizzare due sessioni PuTTY toosimultaneously connettersi tooboth controller in modo da visualizzare quando viene riavviato ogni controller.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Verrà visualizzato un messaggio di conferma. Accettare l'impostazione predefinita di hello (**Y**).
9. Eseguire hello dopo l'installazione di tooresume cmdlet:
   
    `Invoke-HcsSetupWizard`
   
    ![Riprendere la configurazione guidata](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
10. Accettare le impostazioni di rete hello. Dopo aver accettato ciascuna impostazione, verrà visualizzato un messaggio di convalida.
11. Per motivi di sicurezza, password amministratore del dispositivo hello scade dopo hello prima sessione e sarà necessario toochange subito. Quando richiesto, fornire una password di amministratore del dispositivo. Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri. Hello password deve contenere tre dei seguenti hello: caratteri minuscoli, maiuscoli, numerici e speciali.
    
    <br/>![StorSimple registrare il dispositivo 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. passaggio finale di Hello in Installazione guidata di hello registra il dispositivo con il servizio di gestione di dispositivi StorSimple hello. A tale scopo, sarà necessario hello chiave di registrazione del servizio ottenuta nel [passaggio 2: chiave di registrazione del servizio Get hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Dopo aver fornito la chiave di registrazione hello, potrebbe essere necessario toowait 2-3 minuti prima di hello dispositivo è registrato.
    
    > [!NOTE]
    > È possibile premere Ctrl + C in qualsiasi installazione guidata di tempo tooexit hello. Se è stato immesso tutte le impostazioni di rete hello (indirizzo IP per Subnet mask, Gateway e Data 0), le voci selezionate verranno mantenute.
    
    ![Registrazione di StorSimple in corso](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Dopo aver registrato il dispositivo di hello, verrà visualizzata una chiave DEK del servizio. Copiare questo codice e salvarlo in un luogo sicuro. **Questa chiave è necessaria con hello registrazione tooregister chiave ulteriori dispositivi del servizio con il servizio di gestione di dispositivi StorSimple hello.** Fare riferimento troppo[sicurezza in StorSimple](../articles/storsimple/storsimple-8000-security.md) per ulteriori informazioni sulla chiave.
    
    ![StorSimple registrare il dispositivo 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)
    > [!IMPORTANT]
    > testo hello toocopy dalla finestra della console seriale hello, selezionare semplicemente il testo hello. È quindi deve essere in grado di toopaste in Appunti hello o qualsiasi editor di testo.
    > 
    > NON utilizzare **Ctrl + C** toocopy hello chiave DEK. Utilizzando **Ctrl + C** comporta la creazione guidata di installazione di tooexit hello. Di conseguenza, non verrà modificata password amministratore del dispositivo hello e dispositivo hello diventerà una password predefinita toohello.
    
14. Console seriale hello di uscita.
15. Restituire toohello portale di Azure per enti pubblici e completare hello alla procedura seguente:
    
    1. Passare il servizio di gestione di dispositivi StorSimple tooyour.
    2. Fare clic su **Dispositivi**. Elenco di hello dei dispositivi, identificare il dispositivo di hello siano ddeploying. Verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello. deve essere stato del dispositivo Hello **Online**.
            
        Se lo stato del dispositivo hello **Offline**, attendere un paio di minuti per hello online toocome di dispositivo.
       
        Se dispositivo hello sia ancora offline dopo alcuni minuti, quindi è necessario assicurarsi che la rete firewall è stata configurata come descritto in toomake [requisiti di rete per il dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).
       
        Verificare che la porta 9354 sia aperta per le comunicazioni in uscita come viene utilizzato dal bus di servizio hello per le comunicazioni di gestione di dispositivi StorSimple nel dispositivo di servizio.

