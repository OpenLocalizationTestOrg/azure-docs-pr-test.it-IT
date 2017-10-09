<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>tooinstall aggiornamenti periodici tramite Windows PowerShell per StorSimple
1. Aprire console seriale del dispositivo hello e selezionare l'opzione 1, **Accedi con accesso completo**. Digitare la password hello. password predefinita Hello è *Password1*. 
2. Al prompt dei comandi di hello, digitare:
   
     `Get-HcsUpdateAvailability`
   
    Si riceverà la notifica se sono disponibili aggiornamenti e se gli aggiornamenti di hello siano dannose o non comportano interruzioni del servizio.
3. Al prompt dei comandi di hello, digitare:
   
     `Start-HcsUpdate`
   
    verrà avviato il processo di aggiornamento Hello.

> [!IMPORTANT]
> * Questo comando si applica solo aggiornamenti di tooregular. È possibile eseguire questo comando in un solo controller, ma verranno aggiornati entrambi i controller. 
> * È possibile riscontrare un failover del controller durante il processo di aggiornamento hello; Tuttavia, hello failover non influiranno la disponibilità del sistema o l'operazione.
> 
> 

