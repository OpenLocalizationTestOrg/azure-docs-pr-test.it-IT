### <a name="prerequisites"></a>Prerequisiti
* Un account Azure, che è possibile [creare gratuitamente](https://azure.microsoft.com/free)
* Un [account di archiviazione Blob di Azure](../articles/storage/common/storage-create-storage-account.md) inclusi nome account di archiviazione hello e relativa chiave di accesso. Queste informazioni sono elencate nella proprietà hello hello dell'account di archiviazione nel portale di Azure hello. Altre informazioni sull'[archiviazione di Azure](../articles/storage/common/storage-introduction.md).

Prima di utilizzare l'account di archiviazione Blob di Azure in un'app di logica, connettersi tooyour account di archiviazione Blob di Azure. È possibile farlo facilmente all'interno dell'app logica su hello portale di Azure.  

Collegare l'account di archiviazione Blob di Azure tooyour utilizzando hello alla procedura seguente:  

1. Creare un'app per la logica. Nella finestra di progettazione logica App hello, aggiungere un trigger e quindi aggiungere un'azione. Selezionare **Mostra Microsoft API gestite** hello nell'elenco a discesa e quindi immettere "blob" nella casella di ricerca hello. Selezionare una delle azioni hello:  
   
    ![Passaggio per la creazione della connessione ad archiviazione BLOB di Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. Se è stata creata in precedenza tutte le connessioni archiviazione tooAzure, richiesto per i dettagli della connessione hello:   
   
    ![Passaggio per la creazione della connessione ad archiviazione BLOB di Azure](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Immettere i dettagli di account di archiviazione hello. Le proprietà con l'asterisco sono obbligatorie.
   
   | Proprietà | Dettagli |
   | --- | --- |
   | Nome connessione * |Immettere un nome per la connessione. |
   | Nome dell'account di archiviazione di Azure * |Immettere nome account di archiviazione hello. nome account di archiviazione Hello viene visualizzato nelle proprietà di archiviazione hello in hello portale di Azure. |
   | Chiave di accesso dell'account di archiviazione di Azure * |Immettere una chiave dell'account di archiviazione hello. vengono visualizzate le chiavi di accesso di Hello nelle proprietà di archiviazione hello in hello portale di Azure. |
   
    Queste credenziali vengono utilizzate tooauthorize tooconnect di app la logica e accedere ai dati. 
4. Selezionare **Crea**.
5. Si noti hello connessione è stata creata. A questo punto, procedere con hello altri passaggi nell'app logica: 
   
    ![Passaggio per la creazione della connessione ad archiviazione BLOB di Azure](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

