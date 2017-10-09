<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>aggiornamenti in modalità manutenzione tooinstall tramite Windows PowerShell per StorSimple
1. Se non è già fatto, accedere a console seriale del dispositivo hello e selezionare l'opzione 1, **Accedi con accesso completo**. 
2. Digitare la password hello. password predefinita Hello è **Password1**.
3. Al prompt dei comandi di hello, digitare:
   
     `Get-HcsUpdateAvailability` 
4. Si riceverà la notifica se sono disponibili aggiornamenti e se gli aggiornamenti di hello siano dannose o non comportano interruzioni del servizio. aggiornamenti che possono causare interruzioni tooapply, è necessario che il dispositivo di hello tooput in modalità manutenzione. Per istruzioni, vedere [Passaggio 2: Attivare la modalità di manutenzione](../articles/storsimple/storsimple-update-device.md#step2).
5. Quando il dispositivo è in modalità manutenzione, al prompt dei comandi di hello, digitare:`Start-HcsUpdate`
6. Verrà richiesto di confermare. Dopo aver confermato aggiornamenti hello, verranno installati sul controller hello che si è attualmente connessi. Una volta installati gli aggiornamenti di hello, controller hello verrà riavviato. 
7. Monitorare lo stato di hello degli aggiornamenti. Digitare:
   
    `Get-HcsUpdateStatus`
   
    Se hello `RunInProgress` è `True`, hello aggiornamento è ancora in corso. Se `RunInProgress` è `False`, indica che gli aggiornamenti di hello sono stata completata.  
8. Quando aggiornamento hello è installato sul controller corrente hello e si è riavviato, connettersi toohello altri controller ed eseguire i passaggi da 1 a 6.
9. Dopo l'aggiornamento di entrambi i controller, uscire dalla modalità di manutenzione. Per istruzioni, vedere [Passaggio 4: Uscire dalla modalità di manutenzione](../articles/storsimple/storsimple-update-device.md#step4).

