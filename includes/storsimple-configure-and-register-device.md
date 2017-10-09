<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure e registrare il dispositivo di hello
1. Accedere all'interfaccia di Windows PowerShell hello nella console seriale del dispositivo StorSimple. Vedere [console seriale del dispositivo usare PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) per le istruzioni. **Essere procedure hello che toofollow esattamente o non sarà in grado di tooaccess console di hello.**
2. Nella sessione hello aperta, premere INVIO una volta tooget un prompt dei comandi. 
3. Sarà richiesto toochoose hello lingua che si desidera tooset per il dispositivo. Specificare la lingua hello e quindi premere INVIO. 
   
    ![StorSimple configurare e registrare il dispositivo 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. Nel menu di console seriale hello che viene visualizzato, scegliere toolog opzione 1 con accesso completo. 
   
    ![StorSimple registrare il dispositivo 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Completare i passaggi 5-12 tooconfigure hello minimo richiesto le impostazioni di rete per il dispositivo. **Questi passaggi di configurazione necessario toobe eseguiti nel controller attivo di hello del dispositivo hello.** menu della console seriale Hello indica lo stato di controller hello in messaggio hello del banner. Se non si è connessi toohello controller attivo, disconnettersi e quindi connettersi controller attivo toohello.
5. Al prompt dei comandi di hello, digitare la password. password del dispositivo predefinito Hello è **Password1**.
6. Digitare hello comando seguente:
   
     `Invoke-HcsSetupWizard` 
7. Una procedura guidata verrà visualizzato toohelp configurare impostazioni di rete hello per dispositivo hello. Fornire hello hello le seguenti informazioni: 
   
   * Indirizzo IP per l'interfaccia di rete 0 hello dati
   * Subnet mask
   * Gateway
   * Indirizzo IP per il server DNS primario
   * Indirizzo IP per il server NTP primario
     
     > [!NOTE]
     > È possibile toowait per alcuni minuti per hello subnet mask e hello DNS impostazioni toobe applicato. Se viene visualizzato un "hello dispositivo non è pronto." messaggio di errore, connessione di rete fisica hello controllo sull'interfaccia di rete 0 dati hello del controller attivo.
     > 
     > 
8. (Facoltativo) configurare il server proxy Web. Sebbene la configurazione del proxy Web sia facoltativa, **tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui**. Per ulteriori informazioni, visitare troppo[configurare il proxy web per il dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md). Se si verificano problemi durante questo passaggio, fare riferimento a materiale sussidiario tootroubleshooting per [errori durante la configurazione del proxy web](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > È possibile premere Ctrl + C in qualsiasi installazione guidata di tempo tooexit hello. Qualsiasi impostazione applicata prima di emettere questo comando verrà conservata.

1. Per motivi di sicurezza, password amministratore del dispositivo hello scade dopo hello prima sessione e sarà necessario toochange per le sessioni successive. Quando richiesto, fornire una password di amministratore del dispositivo. Una password di amministratore dispositivo valida deve avere una lunghezza compresa tra gli 8 e i 15 caratteri. password di Hello deve contenere una combinazione di caratteri minuscoli, lettere maiuscole, numeri e caratteri speciali.
2. password gestione Snapshot StorSimple Hello viene impostata anche qui. È possibile utilizzare questa password quando si autentica un dispositivo con l'host Windows che esegue Gestione snapshot StorSimple. Quando richiesto, specificare una password di 14 too15 caratteri. Hello password deve contenere una combinazione di tre delle seguenti hello: caratteri minuscoli, maiuscoli, numerici e speciali. 
   
   ![StorSimple registrare il dispositivo 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   È possibile reimpostare la password di StorSimple Snapshot Manager hello dall'interfaccia del servizio StorSimple Manager hello. Per informazioni dettagliate, visitare troppo[modificare le password di StorSimple hello tramite il servizio StorSimple Manager hello](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot eventuali problemi durante questo passaggio, fare riferimento tootroubleshooting indicazioni per [errori correlati toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. passaggio finale di Hello in Installazione guidata di hello registra il dispositivo con hello servizio StorSimple Manager. A tale scopo, è necessario hello registrazione chiave del servizio ottenuta nel passaggio 2. Dopo aver fornito la chiave di registrazione hello, potrebbe essere necessario toowait 2-3 minuti prima di hello dispositivo è registrato.
   
   tootroubleshoot eventuali errori di registrazione del dispositivo possibili, vedere troppo[errori durante la registrazione del dispositivo](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Per risoluzione dei problemi dettagliata, è anche possibile fare riferimento troppo[esempio dettagliato di risoluzione dei problemi](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Dopo aver registrato il dispositivo di hello, verrà visualizzata una chiave DEK del servizio. Copiare questo codice e salvarlo in un luogo sicuro.
   
   > [!WARNING]
   > Questa chiave sarà necessaria con hello servizio registrazione tooregister chiave ulteriori dispositivi con hello servizio StorSimple Manager. Fare riferimento troppo[sicurezza in StorSimple](../articles/storsimple/storsimple-security.md) per ulteriori informazioni sulla chiave.
   > 
   > 
   
    ![StorSimple registrare il dispositivo 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    testo hello toocopy dalla finestra della console seriale hello, selezionare semplicemente il testo hello. È quindi deve essere in grado di toopaste in Appunti hello o qualsiasi editor di testo. NON utilizzare Ctrl + C toocopy hello chiave DEK del servizio. Utilizzando Ctrl + C causerà tooexit hello l'installazione guidata. Di conseguenza, password amministratore del dispositivo hello e una password di StorSimple Snapshot Manager hello non verranno modificate e il dispositivo di hello verranno ripristinate le password predefinite toohello.
5. Console seriale hello di uscita.
6. Restituire toohello portale di Azure classico e completare hello alla procedura seguente:
   
   1. Fare doppio clic sui hello tooaccess di servizio StorSimple Manager **avvio rapido** pagina.
   2. Fare clic su **Visualizza dispositivi connessi**.
   3. In hello **dispositivi** pagina, verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello. deve essere stato del dispositivo Hello **Online**. Se lo stato del dispositivo hello **Offline**, attendere un paio di minuti per hello online toocome di dispositivo.
   
   ![Pagina Dispositivi StorSimple](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Quando il dispositivo hello è online, collegare i cavi di rete hello che è stato scollegato inizio hello di questo passaggio.
   > 
   > 

Dopo il dispositivo di hello viene registrato correttamente e non viene portato online, è possibile eseguire hello `Test-HcsmConnection -Verbose` tooensure che hello connettività di rete è integro. Per hello dettagliate sull'utilizzo di questo cmdlet, vedere troppo[riferimento ai cmdlet per Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Video disponibile](./media/storsimple-configure-and-register-device/Video_icon.png)**Video disponibile**

toowatch un video che illustra come tooconfigure e registrare il dispositivo tramite Windows PowerShell per StorSimple, fare clic su [qui](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

