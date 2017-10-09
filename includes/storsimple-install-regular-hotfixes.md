<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall hotfix periodici tramite Windows PowerShell per StorSimple
1. Connettersi toohello console seriale del dispositivo. Per ulteriori informazioni, vedere [passaggio 1: connessione alla console seriale toohello](../articles/storsimple/storsimple-update-device.md#step1).
2. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**. Digitare la password hello. password predefinita Hello è **Password1**.
3. Al prompt dei comandi di hello, digitare:
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Questo comando si applica solo aggiornamenti rapidi tooregular. È possibile eseguire questo comando in un solo controller, ma verranno aggiornati entrambi i controller.
    > È possibile riscontrare un failover del controller durante il processo di aggiornamento hello; Tuttavia, hello failover non influiranno la disponibilità del sistema o l'operazione.

4. Quando richiesto, fornire hello percorso toohello cartella di rete condivisa che contiene i file dell'hotfix hello.
5. Verrà richiesto di confermare. Tipo **Y** tooproceed con l'installazione dell'hotfix hello.

