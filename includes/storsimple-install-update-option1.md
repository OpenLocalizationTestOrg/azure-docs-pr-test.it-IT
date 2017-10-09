<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>aggiornamenti rapidi toodownload
Eseguire hello seguendo i passaggi toodownload hello software update.

1. Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.
    ![Installare il catalogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload, ad esempio **3063418**, quindi fare clic su **ricerca**.
4. Verrà visualizzato hello **StorSimple Appliance 1.2 aggiornamento** bundle. Fare clic su **Aggiungi**. aggiornamento di Hello verrà aggiunto toohello carrello.
5. Cercare gli aggiornamenti rapidi di aggiuntivi elencate nella tabella hello precedente (**3043005** e **3063416**) e aggiungere ogni carrello hello.
6. Fare clic su **Visualizza carrello**.
   
    ![Visualizza carrello](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. Fare clic su **Download**. Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear. Hello gli aggiornamenti vengono scaricati toohello percorso specificato e inserito in una sottocartella con stesso nome come aggiornamento hello hello. cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.

> [!NOTE]
> Hello hotfix deve essere accessibile da entrambi i controller toodetect qualsiasi errore potenziale dei messaggi dal controller peer hello.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall e verificare gli aggiornamenti rapidi alla modalità normale
Eseguire i seguenti passaggi tooinstall hello e verificare gli aggiornamenti rapidi di hello in modalità normale. Se è già stato installato utilizzando hello del portale di Azure andare troppo[installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall hello di aggiornamento software, interfaccia di Windows PowerShell di accesso hello nella console seriale del dispositivo StorSimple. Seguire hello dettagliate in [console seriale di usare PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Al prompt dei comandi di hello, premere **invio**.
2. Selezionare **opzione 1** toolog toohello dispositivo con accesso completo.
3. pacchetto di aggiornamento il tooinstall hello, al prompt dei comandi di hello, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Utilizzare IP anziché DNS nel percorso di condivisione in hello in precedenza di comando. parametro credential Hello viene utilizzata solo se si accede a una condivisione autenticata.
   
    È consigliabile utilizzare condivisioni tooaccess parametro delle credenziali di hello. Anche le condivisioni che sono aperte troppo "everyone" è in genere non aprire toounauthenticated utenti.
   
    Di seguito è riportato un output di esempio.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Tipo **Y** quando richiesta tooconfirm hello installazione dell'hotfix.
5. Monitorare l'aggiornamento di hello utilizzando hello `Get-HcsUpdateStatus` cmdlet.
   
    Hello output di esempio seguente viene illustrato hello aggiornamento in corso. Hello `RunInprogress` sarà `True` quando hello aggiornamento è in corso.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato. Hello `RunInProgress` sarà `False` quando hello aggiornamento completato.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > In alcuni casi, hello cmdlet report `False` quando aggiornamento hello è ancora in corso. tooensure che hello hotfix è stata completata, attendere qualche minuto, eseguire nuovamente il comando e verificare che hello `RunInProgress` è `False`. Se si tratta, hotfix hello è stata completata.
   > 
   > 
6. Al termine dell'aggiornamento software hello, verificare le versioni di software di hello del sistema. Digitare hello comando seguente:
   
    `Get-HcsSystem`
   
    È necessario visualizzare hello seguenti versioni:
   
   * HcsSoftwareVersion: 6.3.9600.17584
   * CisAgentVersion: 1.0.9049.0
   * MdsAgentVersion: 26.0.4696.1433
     
     Se non viene modificata dopo l'applicazione hello aggiornamento numeri di versione di hello, significa che tale hotfix hello tooapply non riuscita. In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.
7. Ripetere i passaggi da 3 a 5 tooinstall hello rimanenti hotfix in modalità normale (KB3043005).

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall e verificare l'hotfix in modalità manutenzione
Usare gli aggiornamenti del firmware di KB3063416 tooinstall disco. Questi aggiornamenti comportano interruzioni del servizio e richiedere intorno toocomplete 30 a 45 minuti. È possibile scegliere tooinstall in una finestra di manutenzione pianificata per la connessione console seriale del dispositivo toohello.

aggiornamenti del firmware di tooinstall hello disco, seguire le istruzioni di hello riportato di seguito.

1. Dispositivo di hello sul posto in modalità di manutenzione. Si noti che è necessario non utilizzare Windows PowerShell in remoto quando ci si connette il dispositivo tooa in modalità di manutenzione. È necessario toorun questo cmdlet nel controller del dispositivo hello quando si è connessi tramite console seriale del dispositivo hello. Digitare:
   
    `Enter-HcsMaintenanceMode`
   
    Di seguito è riportato un output di esempio.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Riavviare entrambi i controller hello in modalità manutenzione.
2. aggiornamento di firmware del disco con hello di tooinstall, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Di seguito è riportato un output di esempio.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Monitoraggio hello installa lo stato di avanzamento utilizzando `Get-HcsUpdateStatus` comando. Hello aggiornamento è stata completata quando hello `RunInProgress` cambia troppo`False`.
4. Al termine dell'installazione di hello, controller hello in cui è stato installato l'hotfix di modalità di manutenzione hello verrà riavviato. Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco hello. Digitare:
   
   `Get-HcsFirmwareVersion`
   
   Hello previsti sono le versioni del firmware del disco:
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Eseguire hello `Get-HcsFirmwareVersion` comando hello secondo controller tooverify che hello versione del software è stato aggiornato. È quindi possibile uscire dalla modalità di manutenzione hello. Digitare hello comando per ogni controller del dispositivo seguente:
   
   `Exit-HcsMaintenanceMode`
5. controller Hello riavviare quando si esce dalla modalità di manutenzione. Dopo il firmware del disco hello gli aggiornamenti sono stati correttamente applicati e dispositivo hello è uscito dalla modalità di manutenzione, restituito toohello portale di Azure classico. Si noti che il portale di hello potrebbe non visualizzare installato gli aggiornamenti in modalità manutenzione hello per 24 ore.

