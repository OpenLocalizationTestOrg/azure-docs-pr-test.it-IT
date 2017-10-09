Dopo aver aggiunto una condizione, toodo relativo tempo qualcosa interessante con i dati di hello generato da trigger hello. Seguire questi hello tooadd passaggi **Salesforce - oggetto Get** azione. Questa azione riceverà dati hello ogni volta che viene creato un nuovo cliente potenziale. Si aggiungeranno inoltre una seconda azione che verrà utilizzato dati hello hello Salesforce - Get un toosend azione oggetto un messaggio di posta elettronica utilizzando il connettore hello Office 365.  

tooconfigure hello questa azione, sarà necessario hello tooprovide le seguenti informazioni. Si noterà che è facile toouse dati generati da trigger hello come input per alcune delle proprietà di hello per il nuovo file hello:

| Creare proprietà file | Descrizione |
| --- | --- |
| Tipo di oggetto |Questo è il tipo di hello dell'oggetto di Salesforce in questione. Alcuni esempi sono Lead, Account, ecc. |
| ID oggetto |Rappresenta un identificatore per l'oggetto hello. |

1. Selezionare il collegamento **Aggiungi un'azione** . Questa casella di ricerca hello viene visualizzata in cui è possibile cercare qualsiasi azione si desidera tootake. In questo esempio, l'interesse è rivolto alle azioni di Salesforce.      
   ![Immagine di azione Salesforce 1](./media/connectors-create-api-salesforce/action-1.png)  
2. Immettere *salesforce* toosearch per azioni correlate toosalesforce.
3. Selezionare **Salesforce - oggetto Get** come hello tootake di azione.   **Nota**: si sarà richiesta tooauthorize il tooaccess app logica del Salesforce account se si è già stato in precedenza.    
   ![Immagine di azione Salesforce 2](./media/connectors-create-api-salesforce/action-2.png)    
4. Hello **oggetto Get** controllo viene visualizzata.  
5. Selezionare *causare* come tipo di oggetto hello.
6. Seleziona hello **ID oggetto** controllo.
7. Selezionare **...**  elenco hello tooexpand di token che può essere utilizzato come input per le azioni.       
   ![Immagine di azione Salesforce 3](./media/connectors-create-api-salesforce/action-3.png)    
8. Selezionare il controllo **ID lead** per visualizzarlo.   
   ![Immagine di azione Salesforce 4](./media/connectors-create-api-salesforce/action-4.png)     
9. Si noti che il token ID cliente potenziale hello è ora in hello controllo ID oggetto, che indica che hello Get oggetto azione cercherà un lead con un ID responsabile toohello uguale ID responsabile che ha attivato questa app per la logica.  
   ![Immagine di azione Salesforce 5](./media/connectors-create-api-salesforce/action-5.png)  
10. Salvare il lavoro. Questo è tutto, aggiunti hello Get oggetto azione tooyour logica app. Il controllo Ottenere oggetto dovrebbe assomigliare a:     
    ![Immagine di azione Salesforce 6](./media/connectors-create-api-salesforce/action-6.png)  

Dopo aver aggiunto un tooget azione un lead, è consigliabile toodo qualcosa interessanti lead hello appena creato. In un'organizzazione, è consigliabile toosend un toonotify di posta elettronica una lista di distribuzione che è stato creato un nuovo cliente potenziale. Utilizziamo toosend connettore hello Office 365 tramite posta elettronica con alcune delle informazioni pertinenti di hello dal nuovo oggetto lead hello in Salesforce.  

1. Selezionare **aggiungere un'azione** quindi immettere *posta elettronica* nel controllo di ricerca hello. Consente di filtrare hello azioni toothose che toosending correlati e la ricezione di posta elettronica.  
2. Seleziona hello **Office 365 Outlook - invia un messaggio di posta elettronica** voce di elenco. Se è ancora stato creato un *connessione* tooyour account Office 365, sarà possibile tooenter richiesta il toocreate le credenziali di Office 365 it ora. Dopo avere completato, hello **invia un messaggio di posta elettronica** controllo viene visualizzata.        
   ![Immagine di azione Salesforce 7](./media/connectors-create-api-salesforce/action-7.png)  
3. Immettere l'indirizzo di posta elettronica hello che si desidera hello tooin di posta elettronica toosend **a** controllo.
4. In hello **soggetto** di controllo, immettere *nuovo Lead creati* , quindi selezionare hello *aziendale* token. Verrà visualizzata hello *aziendale* campo nuovo lead hello creata in Salesforce.  
5. In hello **corpo** controllo, è possibile selezionare uno dei token hello da hello nuovo cliente potenziale oggetto ed è inoltre possibile immettere il testo desiderato toodisplay nel corpo di hello di hello posta elettronica. Ad esempio:  
   ![Immagine di azione Salesforce 8](./media/connectors-create-api-salesforce/action-8.png)   
6. Salvare il flusso di lavoro.  

È tutto. Ora l'app per la logica è completa.  

A questo punto, è possibile testare l'applicazione di logica: in Salesforce, creare un nuovo cliente potenziale che soddisfa la condizione di hello è stato creato.  Se ci si è attenuti pienamente a questa procedura dettagliata, è sufficiente creare un lead con un indirizzo di posta elettronica che contenga la dicitura *amazon.com* . Dopo pochi secondi dovrebbe essere attivata l'app per la logica e i risultati di hello possono sembrare toothis simile:  
![Immagine di azione Salesforce 9](./media/connectors-create-api-salesforce/action-9.png)  

