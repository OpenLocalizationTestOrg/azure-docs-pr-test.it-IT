<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Risoluzione degli errori di aggiornamento
**Cosa accade se è visualizzata una notifica che hello controlli di pre-aggiornamento non è stato?**

Se un controllo preliminare non riesce, assicurarsi che siano presenti sulla barra di notifica dettagliata hello nella parte inferiore di hello della pagina hello. Questo fornisce informazioni aggiuntive come pre-controllo toowhich non riuscito. Hello figura seguente mostra un'istanza in cui viene visualizzata una notifica. In questo caso, controllo di integrità del controller hello e controllo di integrità del componente hardware non sono riusciti. In hello **stato Hardware** sezione, è possibile vedere che entrambi **Controller 0** e **Controller 1** componenti richiedono attenzione.

  ![Errore di pre-controllo](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

È necessario che entrambi i controller siano integri e online toomake. È necessario anche assicurarsi che tutti i componenti hardware hello nel dispositivo StorSimple hello vengono mostrati toobe integro nella pagina Manutenzione hello toomake. È quindi possibile provare tooinstall aggiornamenti. Se non si dispone di problemi di componenti hardware in grado di toofix hello, occorrerà toocontact supporto Microsoft per i passaggi successivi.

**Cosa accade se si ricezione un messaggio di errore "Impossibile installare gli aggiornamenti" e hello raccomandazione è toorefer toohello aggiornamento risoluzione Guida toodetermine hello causa dell'errore hello?**

Una causa probabile di questo potrebbe essere che non si dispone server Microsoft Update toohello di connettività. Si tratta di una verifica manuale che deve eseguire toobe. Se si perde server di aggiornamento toohello di connettività, il processo di aggiornamento avrà esito negativo. È possibile verificare la connettività hello eseguendo i seguenti cmdlet dall'interfaccia di Windows PowerShell hello del dispositivo StorSimple hello:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Eseguire i cmdlet di hello in entrambi i controller.

Se si verifica presenza di connettività di hello e continuare toosee questo problema, contattare il supporto Microsoft per i passaggi successivi.

**Cosa accade se viene visualizzato un errore di aggiornamento quando si aggiorna il tooUpdate dispositivo 4 ed entrambi i controller hello eseguono l'aggiornamento 4?**

Se entrambi i controller hello sono in esecuzione hello stessa versione del software e se si verifica un errore di aggiornamento, a partire da aggiornamento 4, i controller di hello non passi alla modalità di ripristino. Questa situazione può verificarsi se hello hotfix software di dispositivo (1 ° ordine aggiornamento) è applicato tooboth hello controller correttamente ma altri aggiornamenti rapidi (ordine 2 e 3 ordine) sono ancora toobe applicato. A partire da Update 4, i controller di hello entra in modalità di ripristino solo se i due controller di hello eseguono varie versioni software. 

Se l'utente hello rileva un errore di aggiornamento quando entrambi i controller sono in esecuzione l'aggiornamento 4, è consigliabile che essi attendere qualche minuto e ripetere l'operazione di aggiornamento. Se il tentativo di hello non riuscirà, quindi contattare il supporto Microsoft.
