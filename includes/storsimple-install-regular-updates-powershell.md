<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a>Per installare aggiornamenti regolari tramite Windows PowerShell per StorSimple
1. Aprire la console seriale del dispositivo e scegliere l'opzione 1, **Accedi con accesso completo**. Digitare la password. La password predefinita è *Password1*. 
2. Al prompt dei comandi digitare:
   
     `Get-HcsUpdateAvailability`
   
    Verrà notificato se sono disponibili aggiornamenti e se gli aggiornamenti sono problematici o meno.
3. Al prompt dei comandi digitare:
   
     `Start-HcsUpdate`
   
    Il processo di aggiornamento verrà avviato.

> [!IMPORTANT]
> * Questo comando si applica solo agli aggiornamenti regolari. È possibile eseguire questo comando in un solo controller, ma verranno aggiornati entrambi i controller. 
> * Durante il processo di aggiornamento è possibile che venga eseguito il failover di un controller. Tale failover, tuttavia, non avrà effetti sulla disponibilità o sul funzionamento del sistema.
> 
> 

