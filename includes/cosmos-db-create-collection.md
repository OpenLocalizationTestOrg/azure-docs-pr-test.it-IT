È ora possibile usare insieme e strumento di esplorazione dei dati hello in hello toocreate portale Azure un database. 

1. Nel portale di Azure, nel menu di navigazione sinistro hello, hello fare clic su **Esplora dati (anteprima)**. 

2. In hello **Esplora dati (anteprima)** pannello, fare clic su **nuova raccolta**, quindi fornire hello le seguenti informazioni:

    ![Hello Azure-pannello Esplora dati portale](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Impostazione|Valore consigliato|Descrizione
    ---|---|---
    ID database|Attività|nome Hello per il nuovo database. I nomi dei database devono avere una lunghezza compresa tra 1 e 255 caratteri e non possono contenere /, \\, #, ? o spazi finali.
    ID raccolta|Items|nome Hello per la nuova raccolta. I nomi di raccolta sono hello stesso carattere requisiti come ID di database.
    Capacità di archiviazione| Fissa (10 GB)|Utilizzare il valore di predefinito hello. Questo valore è la capacità di archiviazione hello del database hello.
    Velocità effettiva|400 UR|Utilizzare il valore di predefinito hello. Se si desidera tooreduce latenza, è possibile scalare in verticale della velocità effettiva hello in un secondo momento.
    Chiave di partizione|/category|Una chiave di partizione che distribuisce i dati in modo uniforme tooeach partizione. Chiave di partizione corretto selezionando hello è importante creare una raccolta ad alte prestazioni. vedere, più toolearn [progettazione per il partizionamento](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Dopo aver completato il modulo di hello, fare clic su **OK**.

Viene illustrato Esplora dati hello Nuovo Database e la raccolta. 
