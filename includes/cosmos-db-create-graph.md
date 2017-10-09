A questo punto, è possibile utilizzare strumento di esplorazione dei dati hello in hello toocreate portale Azure un database di grafico. 

1. Nel portale di Azure, nel menu di navigazione sinistro hello, hello fare clic su **Esplora dati (anteprima)**. 
2. In hello **Esplora dati (anteprima)** pannello, fare clic su **nuovo grafico**, quindi immettere nella pagina di hello mediante hello le seguenti informazioni.

    ![Esplora dati in hello portale di Azure](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Impostazione|Valore consigliato|Descrizione
    ---|---|---
    ID database|sample-database|Hello ID per il nuovo database. I nomi dei database devono avere una lunghezza compresa tra 1 e 255 caratteri e non possono contenere `/ \ # ?` o spazi finali.
    Graph id (ID grafo)|sample-graph|Hello ID per il nuovo grafico. I nomi dei grafici sono hello stesso carattere requisiti come ID di database.
    Capacità di archiviazione| 10 GB|Lasciare il valore di predefinito hello. Questa è la capacità di archiviazione hello del database hello.
    Velocità effettiva|400 UR/s|Lasciare il valore di predefinito hello. È possibile scalare in verticale della velocità effettiva hello in un secondo momento se si desidera tooreduce latenza.
    Chiave di partizione|/userId|Una chiave di partizione che verrà distribuiti uniformemente dati tooeach partizione. Grafico di selezione hello corretto la chiave di partizione è importante per la creazione di un ad alte prestazioni, per ulteriori informazioni su esso in [progettazione per il partizionamento](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Una volta compilato il modulo di hello, fare clic su **OK**.
