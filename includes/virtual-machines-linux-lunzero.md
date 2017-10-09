Quando si aggiungono dati dischi tooa VM Linux, si potrebbero verificare errori se un disco non esiste nel LUN 0. Se si aggiunge un disco manualmente tramite hello `azure vm disk attach-new` comando e si specifica un numero di unità LOGICA (`--lun`) anziché consentire hello toodetermine piattaforma Azure hello LUN appropriati, verificare che esista già un disco o sarà disponibile nel LUN 0. 

Prendere in considerazione hello seguente esempio viene mostrato un frammento di codice dell'output di hello dalle `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

Esistono dischi dati Hello due LUN 0 e LUN 1 (hello prima colonna hello `lsscsi` dettagli output `[host:channel:target:lun]`). Entrambi i dischi siano accessbile all'interno di hello macchina virtuale. Se è stato specificato manualmente hello primo disco toobe a LUN 1 e disco secondo hello LUN 2, si potrebbero non visualizzare dischi hello correttamente da all'interno di una macchina virtuale.

> [!NOTE]
> Hello Azure `host` valore è 5 in questi esempi, ma questo può variare in base al tipo hello di archiviazione selezionato.
> 
> 

Questo comportamento disco non è un problema di Azure, ma il modo di hello in cui hello Linux kernel segue specifiche SCSI hello. Quando il kernel Linux hello analizza il bus SCSI hello per le periferiche collegate, un dispositivo deve essere trovato nel LUN 0 affinché hello sistema toocontinue l'analisi per altri dispositivi. Di conseguenza:

* Esaminare l'output di hello di `lsscsi` dopo l'aggiunta di un tooverify disco dati dispone di un disco al LUN 0.
* Se il disco non viene visualizzato correttamente nella VM, verificare che sia presente un disco nel LUN 0.

