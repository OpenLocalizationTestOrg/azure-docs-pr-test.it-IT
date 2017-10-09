<!--author=alkohli last changed: 09/01/16-->

#### <a name="toodownload-hotfixes"></a>aggiornamenti rapidi toodownload
Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.

1. Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.
    ![Installare il catalogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload, ad esempio **3186843**, quindi fare clic su **ricerca**.
   
    Hello hotfix elenco viene visualizzato, ad esempio, **cumulativo Software Bundle di aggiornamento 3.0 per StorSimple 8000 Series**.
   
    ![Cercare nel catalogo](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. Fare clic su **Aggiungi**. aggiornamento di Hello viene aggiunto toohello carrello.
5. Cercare gli aggiornamenti rapidi di aggiuntivi elencate nella tabella hello precedente (**3186859**) e aggiungere ogni carrello toohello.
6. Fare clic su **Visualizza carrello**.
7. Fare clic su **Download**. Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear. Hello gli aggiornamenti vengono scaricati toohello percorso specificato e inserita in una sottocartella con stesso nome come aggiornamento hello hello. cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.

> [!NOTE]
> Hello hotfix deve essere accessibile da entrambi i controller toodetect qualsiasi errore potenziale dei messaggi dal controller peer hello.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall e verificare gli aggiornamenti rapidi alla modalità normale
Eseguire i seguenti passaggi tooinstall hello e verificare gli aggiornamenti rapidi in modalità normale. Se è già stato installato utilizzando hello del portale di Azure andare troppo[installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall hello hotfixes interfaccia di Windows PowerShell di accesso hello nella console seriale del dispositivo StorSimple. Seguire hello dettagliate in [console seriale di usare PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Al prompt dei comandi di hello, premere **invio**.
2. Selezionare **opzione 1** toolog toohello dispositivo con accesso completo. È consigliabile installare hotfix hello sul controller passivo hello prima.
3. hotfix hello tooinstall, al prompt dei comandi di hello, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Utilizzare IP anziché DNS nel percorso di condivisione in hello in precedenza di comando. parametro credential Hello viene utilizzata solo se si accede a una condivisione autenticata.
   
    È consigliabile utilizzare condivisioni tooaccess parametro delle credenziali di hello. Anche le condivisioni che sono aperte troppo "everyone" è in genere non aprire toounauthenticated utenti.
   
    Specificare la password hello quando richiesto.
   
    Di seguito è riportato un output di esempio.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. Tipo **Y** quando richiesta tooconfirm hello installazione dell'hotfix.
5. Monitorare l'aggiornamento di hello utilizzando hello `Get-HcsUpdateStatus` cmdlet. aggiornamento di Hello completerà innanzitutto nel controller passivo hello. Una volta che viene aggiornato il controller passivo hello, sarà presente un failover e aggiornamento hello verrà quindi applicata in hello altro controller. aggiornamento di Hello è completa quando entrambi i controller hello vengono aggiornati.
   
    Hello output di esempio seguente viene illustrato hello aggiornamento in corso. Hello `RunInprogress` sarà `True` quando hello aggiornamento è in corso.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello seguente esempio di output indica che gli aggiornamenti di hello sono terminato. Hello `RunInProgress` sarà `False` quando hello aggiornamento completato.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > In alcuni casi, hello cmdlet report `False` quando aggiornamento hello è ancora in corso. tooensure che hello hotfix è stata completata, attendere qualche minuto, eseguire nuovamente il comando e verificare che hello `RunInProgress` è `False`. Se si tratta, hotfix hello è stata completata.

1. Al termine dell'aggiornamento software hello, verificare le versioni di software di hello del sistema. Digitare:
   
    `Get-HcsSystem`
   
    È necessario visualizzare hello seguenti versioni:
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     Se non viene modificata dopo l'applicazione hello aggiornamento numeri di versione di hello, significa che tale hotfix hello tooapply non riuscita. In questo caso contattare il [Supporto tecnico Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) per assistenza.
     
     > [!IMPORTANT]
     > È necessario riavviare il controller attivo di hello mediante hello `Restart-HcsController` cmdlet prima di applicare gli aggiornamenti rimanenti hello. 
     > 
     > 
2. Ripetere i passaggi 3-5 driver hello LSI tooinstall e firmware hotfix **KB3186859**. Dopo aver installato l'hotfix hello, utilizzare hello `Get-HcsSystem` cmdlet. la versione di Hello LSI deve essere:
   
   * `Lsisas2Version: 2.0.78.00`
3. Ripetere i passaggi da 3 a 5 tooinstall hello Storport e aggiornamento Spaceport **KB3121261**.
4. Se si sta aggiornando da Update 2 o versioni precedenti, è necessario anche toodownload:
   
   * Fix iSCSI con KB3146621
   * Fix WMI con KB3103616

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall e verificare l'hotfix in modalità manutenzione
Usare gli aggiornamenti del firmware di KB3121899 tooinstall disco. Questi aggiornamenti comportano interruzioni e e richiedere toocomplete circa 30 minuti. È possibile scegliere tooinstall in una finestra di manutenzione pianificata per la connessione console seriale del dispositivo toohello.

Si noti che se il firmware del disco è già stato aggiornato, non sarà necessario tooinstall questi aggiornamenti. Eseguire hello `Get-HcsUpdateAvailability` da hello dispositivo console seriale toocheck se sono disponibili aggiornamenti che indica se hello Aggiorna sono comportano interruzioni del servizio (modalità di manutenzione) o non comportano interruzioni del servizio (modalità normale) gli aggiornamenti.

aggiornamenti del firmware di tooinstall hello disco, seguire le istruzioni di hello riportato di seguito.

1. Dispositivo di hello sul posto in modalità manutenzione hello. Si noti che è necessario non utilizzare Windows PowerShell in remoto quando ci si connette il dispositivo tooa in modalità di manutenzione. In alternativa, eseguire questo cmdlet nel controller del dispositivo hello quando si è connessi tramite console seriale del dispositivo hello. Digitare:
   
    `Enter-HcsMaintenanceMode`
   
    Di seguito è riportato un output di esempio.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
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
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Monitoraggio hello installa lo stato di avanzamento utilizzando `Get-HcsUpdateStatus` comando. Hello aggiornamento è stata completata quando hello `RunInProgress` cambia troppo`False`.
4. Al termine dell'installazione di hello, hello del controller in cui hello è stato installato l'hotfix di modalità di manutenzione viene riavviato. Accedere all'opzione 1 con accesso completo e verificare la versione del firmware del disco hello. Digitare:
   
   `Get-HcsFirmwareVersion`
   
   Hello previsti sono le versioni del firmware del disco:
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   Di seguito è riportato un output di esempio.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    Eseguire hello `Get-HcsFirmwareVersion` comando hello secondo controller tooverify che hello versione del software è stato aggiornato. È quindi possibile uscire dalla modalità di manutenzione hello. toodo in tal caso, digitare hello comando per ogni controller del dispositivo seguente:
   
   `Exit-HcsMaintenanceMode`
5. controller Hello riavviare quando si esce dalla modalità di manutenzione. Dopo il firmware del disco hello gli aggiornamenti sono stati correttamente applicati e dispositivo hello è uscito dalla modalità di manutenzione, restituito toohello portale di Azure classico. Si noti che il portale di hello potrebbe non visualizzare installato gli aggiornamenti in modalità manutenzione hello per 24 ore.

