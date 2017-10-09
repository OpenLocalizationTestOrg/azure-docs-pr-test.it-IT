Ora che è stato aggiunto un trigger, toodo relativo tempo qualcosa interessante con i dati di hello generato da trigger hello. Seguire questi hello tooadd passaggi **SharePoint Online - creare file** azione. Verrà creato un file in SharePoint Online generato di trigger ogni ora hello nuovo elemento. 

tooconfigure hello questa azione, sarà necessario hello tooprovide le seguenti informazioni. Come fornire queste informazioni, si noterà che è facile toouse dati generati da trigger hello come input per alcune delle proprietà di hello per il nuovo file hello:

| Creare proprietà file | Descrizione |
| --- | --- |
| Site URL |Si tratta hello URL del sito di SharePoint Online hello in cui si desidera toocreate hello nuovo file. Selezionare il sito hello hello elenco visualizzato. |
| Percorso della cartella |Questo è hello cartella (all'URL del sito selezionato nel passaggio precedente hello Buongiorno) in cui verrà inserito il nuovo file di hello. Cercare e selezionare la cartella hello. |
| Nome file |Questo è il nome di hello del file hello creato. |
| Contenuto del file |contenuto Hello che verrà scritto il file toohello. |

1. Selezionare **+ nuovo passaggio** azione hello tooadd.  
   ![Immagine di azione SharePoint Online 1](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Seleziona hello **aggiungere un'azione** collegamento. Questa casella di ricerca hello viene visualizzata in cui è possibile cercare qualsiasi azione si desidera tootake. In questo esempio, l'interesse è rivolto alle azioni di SharePoint.    
   ![Immagine di azione SharePoint Online 2](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Immettere *sharepoint* toosearch per azioni correlate tooSharePoint.
4. Selezionare **SharePoint Online - creare file** come hello tootake di azione.   **Nota**: si sarà richiesta tooauthorize il tooaccess app logica SharePoint account se non è stato creato in precedenza un tooSharePoint connessione Online.    
   ![Immagine di azione SharePoint Online 3](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Hello **crea file** controllo viene visualizzata.   
   ![Immagine di azione SharePoint Online 4](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Selezionare **URL del sito** e Sfoglia toofind hello sito in cui si desidera file hello toocreate.     
   ![Immagine di azione SharePoint Online 5](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Selezionare **percorso della cartella** e Sfoglia toofind hello cartella in cui verrà inserito il nuovo file di hello.  
   ![Immagine di azione SharePoint Online 6](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Seleziona hello **nome File** controllo e immettere il nome di hello del file hello desiderato toocreate. In questo caso, è possibile immettere direttamente il nome di file hello o è possibile utilizzare le proprietà di hello da trigger hello creato in precedenza. Questo scopo, selezionare le proprietà dall'elenco di hello di **gli output di quando si crea un nuovo elemento**. Questo elenco viene visualizzato solo dopo aver selezionato hello **nome File** controllo. In questa procedura dettagliata, selezionato ID (ID hello della nuova voce di elenco hello) come nome di hello del file hello vengono creati da hello **SharePoint Online - creare file** azione.    
   ![Immagine di azione SharePoint Online 7](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Seleziona hello **il contenuto di File** controllo e immettere hello contenuto che verrà scritto il file toohello che verrà creato. Per il contenuto di file hello, si noti che è possibile utilizzare le proprietà di hello da trigger hello creato in precedenza. Selezionare semplicemente le proprietà di hello elenco hello presentato. In alternativa, è possibile immettere hello **il contenuto di File** testo direttamente nel controllo hello. In questo esempio, sono state selezionate alcune proprietà e sono stati aggiunti degli spazi e un trattino tra le diverse proprietà.        
   ![Immagine di azione SharePoint Online 8](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Salva flusso di lavoro tooyour hello modifiche  
11. Congratulazioni, ora è un'applicazione completamente funzionale logica che viene attivata quando un nuovo elemento viene aggiunto l'elenco di SharePoint Online tooa. app Hello creerà quindi un file, utilizzando alcune delle proprietà di hello dalla nuova voce di elenco hello.  È ora possibile testare creando un nuovo elemento nell'elenco di SharePoint hello. 

