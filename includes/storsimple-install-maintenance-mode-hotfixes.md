<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall hotfix in modalità manutenzione tramite Windows PowerShell per StorSimple
> [!IMPORTANT]
> In modalità manutenzione, è necessario innanzitutto tooapply hello hotfix su un controller e quindi su hello altri controller.
> 
> 

1. Portare il dispositivo hello in modalità manutenzione. Vedere [passaggio 2: la modalità di manutenzione immettere](../articles/storsimple/storsimple-update-device.md#step2) per istruzioni sulla modalità di manutenzione tooenter.
2. tooapply hello hotfix, tipo:
   
     `Start-HcsHotfix` 
3. Quando richiesto, fornire hello percorso toohello cartella di rete condivisa che contiene i file dell'hotfix hello.
4. Verrà richiesto di confermare. Tipo **Y** tooproceed con l'installazione dell'hotfix hello.
5. Dopo che è stato applicato hello hotfix su un controller, accesso toohello altro controller. Come è stato fatto per controller precedente hello, è necessario applicare l'hotfix hello.
6. Dopo l'applicazione hello hotfix, disattivare la modalità di manutenzione. Per istruzioni, vedere [Passaggio 4: Uscire dalla modalità di manutenzione](../articles/storsimple/storsimple-update-device.md#step4).

