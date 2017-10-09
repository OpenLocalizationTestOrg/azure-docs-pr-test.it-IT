## <a name="repeatability-during-copy"></a>Ripetibilità durante la copia
Quando la copia di dati tooAzure SQL di SQL Server da altri dati archivia uno esigenze tookeep ripetibilità in presente tooavoid risultati imprevisti. 

Quando si copiano dati tooAzure Database SQL o SQL Server, attività di copia verrà tabella di sink toohello predefinita APPEND hello set di dati per impostazione predefinita. La copia dei dati da un'origine di file CSV (dati di valori separati da virgole) che contiene due record tooAzure Database SQL o SQL Server, ad esempio, questo è quale tabella hello ha un aspetto simile:

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Si supponga che si trovati errori nel file di origine e la quantità di hello aggiornato di Tube verso il basso dalla too4 2 nel file di origine hello. Se si esegue nuovamente la sezione dati hello durante tale periodo, sono disponibili due nuovi record accodato tooAzure Database SQL o SQL Server. Hello seguente si presuppone che nessuna delle colonne hello nella tabella hello è il vincolo di chiave primaria di hello.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid, sarà necessario semantica UPSERT toospecify mediante l'utilizzo di uno di hello seguito 2 meccanismi indicato di seguito.

> [!NOTE]
> Una sezione può essere nuovamente eseguita automaticamente in Data Factory di Azure in base ai criteri di ripetizione hello specificato.
> 
> 

### <a name="mechanism-1"></a>Meccanismo 1
È possibile sfruttare **sqlWriterCleanupScript** toofirst proprietà eseguire l'azione di pulizia quando viene eseguita una sezione. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Hello script di pulizia verrà eseguito prima durante la copia di una sezione specificata in cui verrà eliminati dati hello dall'intervallo di toothat hello tabella SQL corrispondente. attività Hello verrà successivamente inserire dati hello hello tabella SQL. 

Se la sezione hello è ora eseguire di nuovo, quindi si troverà quantità hello viene aggiornata come desiderato.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Si supponga che hello record rondellapiatta viene rimosso da file csv originale hello. Quindi eseguire di nuovo sezione hello produrrebbe hello seguente risultato: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Non è una novità era toobe eseguita. esecuzione dell'attività di copia Hello hello pulizia dati dello script toodelete hello corrispondente per tale sezione. Quindi leggere l'input di hello da file csv hello (contenute quindi solo 1 record) e viene inserita nella tabella hello. 

### <a name="mechanism-2"></a>Meccanismo 2
> [!IMPORTANT]
> Attualmente sliceIdentifierColumnName non è supportato per SQL Data Warehouse di Azure. 

Ripetibilità di tooachieve un altro meccanismo consiste nel disporre di una colonna dedicata (**sliceIdentifierColumnName**) in hello tabella di destinazione. Questa colonna verrà usata dalla Data Factory di Azure tooensure hello origine e destinazione la sincronizzazione. Questo approccio funziona quando è disponibile una flessibilità nella modifica o la definizione di schema di tabella SQL di destinazione hello. 

Questa colonna viene utilizzata da Data Factory di Azure per scopi di ripetibilità e nel processo di hello Azure Data Factory non apporterà qualsiasi schema cambia toohello tabella. Modo toouse questo approccio:

1. Definire una colonna di tipo binary (32) di destinazione hello tabella SQL. in cui non sia presente alcun vincolo. Ai fini di questo esempio, la colonna viene denominata "ColumnForADFuseOnly".
2. Utilizzarlo nell'attività di copia hello come segue:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

Azure Data Factory popola questa colonna in base alle necessità tooensure hello origine e destinazione mantenere la sincronizzazione. i valori Hello di questa colonna non utilizzare di fuori di questo contesto utente hello. 

Toomechanism simile 1, verrà di attività di copia automaticamente prima pulizia dei dati di hello per hello assegnato slice dalla destinazione hello tabella SQL e quindi eseguire attività di copia hello in genere dati hello tooinsert toodestination di origine per tale sezione. 

