### <a name="prerequisites"></a>Prerequisiti
* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [Database SQL di Azure](../articles/sql-database/sql-database-get-started.md) con le informazioni di connessione, inclusi nome hello del server, nome del database e nome utente/password. Queste informazioni sono incluse nella stringa di connessione di Database SQL di hello:
  
    Server=tcp:*yoursqlservername*.database.windows.net,1433;Initial Catalog=*yourqldbname*;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
  
    Altre informazioni sui [database SQL di Azure](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Quando si crea un Database SQL di Azure, è anche possibile creare il database di esempio hello inclusi in SQL. 
> 
> 

Prima di usare Database SQL di Azure in un'app di logica, connettersi tooyour Database SQL. È possibile farlo facilmente all'interno dell'app logica su hello portale di Azure.  

Connettersi tooyour Database SQL di Azure utilizzando hello seguendo i passaggi:  

1. Creare un'app per la logica. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'azione. Selezionare **Mostra Microsoft API gestite** in hello nell'elenco a discesa e quindi immettere "sql" nella casella di ricerca hello. Selezionare una delle azioni hello:  
   
    ![Passaggio di creazione della connessione a SQL Azure](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Se è stata creata in precedenza qualsiasi tooSQL le connessioni del Database, richiesto per i dettagli della connessione hello:  
   
    ![Passaggio di creazione della connessione a SQL Azure](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Immettere i dettagli del Database SQL hello. Le proprietà con l'asterisco sono obbligatorie.
   
   | Proprietà | Dettagli |
   | --- | --- |
   | Connessione tramite gateway |Lasciare deselezionata. Viene utilizzato quando la connessione tooan SQL Server locale. |
   | Nome connessione * |Immettere un nome per la connessione. |
   | Nome di SQL Server* |Immettere il nome di server hello; che è simile al seguente *servername.database.windows.net*. nome del server Hello è visualizzato nelle proprietà del Database di SQL hello nel portale di Azure hello e visualizzato anche nella stringa di connessione hello. |
   | Nome del database SQL* |Immettere il nome di hello è assegnato il Database SQL. Questo è elencato nelle proprietà del Database di SQL hello nella stringa di connessione hello: Initial Catalog =*yoursqldbname*. |
   | Nome utente* |Immettere nome utente hello creato quando hello Database SQL è stato creato. Questo è elencato nelle proprietà del Database di SQL hello in hello portale di Azure. |
   | Password* |Immettere password hello creata quando hello Database SQL è stato creato. |
   
    Queste credenziali vengono utilizzate tooauthorize tooconnect di app la logica e accedere ai dati SQL. Al termine dell'operazione, i dettagli di connessione aspetto simile toohello seguenti:  
   
    ![Passaggio di creazione della connessione a SQL Azure](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Selezionare **Crea**. 
5. Si noti hello connessione è stata creata. A questo punto, procedere con hello altri passaggi nell'app logica: 
   
    ![Passaggio di creazione della connessione a SQL Azure](./media/connectors-create-api-sqlazure/table.png)

