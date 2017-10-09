Ora che è stato aggiunto un trigger, toodo relativo tempo qualcosa interessante con i dati di hello generato da trigger hello. Seguire questi tooadd passaggi un hello **SFTP - cartella estrazione** azione. Questa azione consentirà di estrarre contenuto hello di un file se vengono soddisfatte le condizioni di hello definite. 

tooconfigure hello questa azione, sarà necessario hello tooprovide le seguenti informazioni. Si noterà che è facile toouse dati generati da trigger hello come input per alcune delle proprietà di hello per il nuovo file hello:

| SFTP - Proprietà della cartella di estrazione | Descrizione |
| --- | --- |
| Percorso file di archiviazione di origine |Questo è il percorso di hello per file hello vengono estratti. È possibile selezionare uno dei token hello da un'azione precedente o percorso del file hello toofind server SFTP hello Sfoglia. |
| Percorso cartella di destinazione |Si tratta hello percorso in cui verranno inserito il file hello estratto. È possibile selezionare uno dei token hello da un'azione precedente come percorso di destinazione hello o server SFTP hello Sfoglia e selezionare un percorso. |
| Sovrascrivere? |Indica se un file con hello stesso nome di file estratto hello viene trovato nel percorso di cartella di destinazione hello se il file esistente hello deve essere sovrascritti o non. |

È possibile iniziare subito l'aggiunta di hello azione tooextract hello file se hello definita in precedenza Condition troppo*True*. 

1. Selezionare **Aggiungi un'azione**.        
   ![Immagine di condizione dell'azione SFTP 6](./media/connectors-create-api-sftp/condition-6.png)   
2. Seleziona hello **SFTP - cartella estrazione** azione      
   ![Immagine di condizione dell'azione SFTP 7](./media/connectors-create-api-sftp/condition-7.png)   
3. Selezionare **Percorso file di archiviazione di origine**              
   ![Immagine di condizione dell'azione SFTP 9](./media/connectors-create-api-sftp/condition-9.png)   
4. Seleziona hello **percorso del File** token. Ciò indica che si utilizzerà percorso del file hello hello trigger trovato come percorso del file di archivio origine hello file hello.           
   ![Immagine di condizione dell'azione SFTP 10](./media/connectors-create-api-sftp/condition-10.png)   
5. Selezionare **Percorso cartella di destinazione**           
   ![Immagine di condizione dell'azione SFTP 11](./media/connectors-create-api-sftp/condition-11.png)   
6. Seleziona hello **percorso del File** token. Ciò indica che si utilizzerà percorso del file hello hello trigger trovato come percorso di destinazione hello per i file estratto hello file hello.   
7. Immettere *\ExtractedFile* in hello **percorso cartella di destinazione** controllo. Eseguire questa operazione solo dopo il token di percorso di file hello in hello controllo percorso cartella di destinazione.         
   ![Immagine di condizione dell'azione SFTP 12](./media/connectors-create-api-sftp/condition-12.png)   
8. Immettere *True* in hello **sovrascrittura?* tooindicate di controllo che i file esistenti devono essere sovrascritti se hanno hello stesso nome come hello estratti.      
   ![Immagine di condizione dell'azione SFTP 13](./media/connectors-create-api-sftp/condition-13.png)   
9. Salva flusso di lavoro tooyour hello modifiche  

